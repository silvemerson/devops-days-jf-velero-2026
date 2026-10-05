# Velero + RustFS: roteiro da palestra

Written for: você, apresentando a palestra. Texto de apoio para a fala e para os slides.

A palestra tem duas partes: a argumentação sobre por que Kubernetes precisa de backup e DR, e a prática, com prints do lab.

---

## Parte 1: Por que Kubernetes precisa de backup

Abertura: se o cluster de produção sumir amanhã, quanto tempo leva para voltar? Quase ninguém tem o número na ponta da língua, e essa pergunta já introduz o tema.

### HA não é backup

Kubernetes resolve disponibilidade da aplicação: réplicas, self-healing, rolling update. Mas não resolve recuperação de desastre.

O ponto central é que réplicas replicam o estado ruim. Se alguém roda `kubectl delete namespace` no cluster errado, todas as réplicas somem juntas. Outros casos que réplicas não resolvem:

- remoção acidental de namespace ou de recursos;
- GitOps que sincronizou uma remoção indesejada;
- corrupção do etcd ou perda do control plane;
- perda de uma zona ou região inteira;
- credencial comprometida usada para apagar recursos.

### RPO, RTO e o que proteger

- **RPO** (Recovery Point Objective): quanto dado você aceita perder. Backup a cada 6 horas significa RPO de até 6 horas.
- **RTO** (Recovery Time Objective): quanto tempo você aceita ficar fora do ar, incluindo detectar, decidir, restaurar e validar.

Esses dois números definem a frequência do backup e o quanto o restore precisa ser automatizado e testado.

Um backup de Kubernetes precisa cobrir duas coisas: os recursos da API (Deployments, Services, ConfigMaps, Secrets, CRDs, RBAC) e os dados dos volumes persistentes (bancos, uploads, filas). Backup só de manifesto é restauração parcial, e muitos times descobrem isso no dia do desastre.

### Estratégias de DR

Três estratégias comuns, em ordem crescente de custo:

- **Backup e restore**: snapshots periódicos em armazenamento externo, restore sob demanda. RPO de horas, RTO de dezenas de minutos.
- **Warm standby**: cluster secundário provisionado, com dados replicados e aplicação reduzida.
- **Active-active**: dois ambientes servindo tráfego. RTO e RPO próximos de zero, com complexidade e custo altos.

Para a maioria dos times, backup e restore bem testado entrega mais valor do que um active-active mal operado. E o backup precisa sair do cluster que pode cair: se ele mora no mesmo cluster, o desastre leva os dois.

### Velero

Velero é uma ferramenta open source, originalmente da VMware, para backup e restore de clusters Kubernetes. Roda como controlador dentro do cluster.

Componentes que aparecem na demo:

- **Velero server**: executa backups, restores e schedules.
- **node-agent**: move dados de volumes quando não há snapshot disponível.
- **BackupStorageLocation (BSL)**: onde os backups são gravados. No lab, um bucket S3 no RustFS.
- **Backup e Restore**: recursos do Kubernetes que representam cada operação.

O fluxo: o Velero lê a API, empacota e envia para o BSL. No restore, lê o BSL e recria os recursos no cluster de destino. Para restaurar em outro cluster, os dois precisam enxergar o mesmo armazenamento. Essa é a parte que vai para a demo.

### RustFS

RustFS é um object storage compatível com a API S3, escrito em Rust. Roda em modo distribuído, com erasure coding, o que permite tolerar a perda de nós sem perder dados. O próprio projeto descreve o modo distribuído como em fase de testes, e isso vale dizer no slide.

### Arquitetura da demo

Dois clusters Kubernetes (produção e DR), um RustFS de quatro nós, e Velero instalado nos dois clusters apontando para o RustFS.

---

## Parte 2: Prática com prints

Sequência de prints sugerida:

1. Os dois clusters existem (`kubectl get nodes` nos contextos de produção e DR).
2. RustFS com quatro nós no ar (`docker compose ps`).
3. Buckets do lab (`aws s3 ls` contra o endpoint do RustFS).
4. Velero instalado, com os BSLs em "Available" nos dois clusters, incluindo o `from-prd` somente leitura.
5. Aplicação rodando em produção (`kubectl -n demo-app get all,configmap`).
6. Backup criado com `velero backup create ... --wait`, com status "Completed".
7. Detalhes do backup com `velero backup describe --details`.
8. O backup aparecendo no cluster de DR (`velero backup get`).
9. Restore disparado com `velero restore create ... --wait`.
10. Recursos recriados no DR (`kubectl -n demo-app get all,configmap`).
11. Conteúdo do ConfigMap conferindo com a mensagem original.
12. Objeto do backup armazenado no bucket do RustFS.
13. Um nó do RustFS derrubado (`docker compose stop node2`) e o cluster continuando a responder.
14. Nó de volta (`docker compose start node2`).

Antes da palestra, rodar `smoke-test.sh` do zero para confirmar que os prints saem como descritos. Deixar `cleanup-demo.sh` pronto para resetar entre ensaios.

### Limitações para o slide final

- O modo distribuído do RustFS ainda é descrito como em fase de testes.
- No lab, os discos do erasure coding compartilham o mesmo dispositivo físico, então a checagem de discos distintos foi desabilitada. Isso é só para lab.
- Volumes Docker nascem com dono root, então os containers rodam como root no lab.
- O fluxo de demo protege só recursos da API, sem dados de PVC.
- Próximos passos: volumes persistentes, snapshots CSI, retenção e RTO medido.
