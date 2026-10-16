---
marp: true
theme: gaia
class:
  - lead
  - invert
paginate: true
backgroundColor: #0B1426
footer: '![height:40px](4linux-logo/logo-4linux.png)'
lang: pt-BR
style: |
  /* @theme 4linux */
  @import 'gaia';

  :root {
    --color-background: #0B1426;
    --color-foreground: #FFFFFF;
    --color-highlight: #00E6CC;
    --color-accent: #00C4A7;
    --color-secondary: #4ECDC4;
    --color-dimmed: #8B9DC3;
    --4linux-green: #00E6CC;
    --4linux-dark-green: #00C4A7;
    --4linux-blue: #4ECDC4;
    --4linux-dark: #0B1426;
  }

  section {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
    background-color: var(--4linux-dark);
    background: linear-gradient(135deg, #0B1426 0%, #1a2332 100%);
    color: var(--color-foreground);
    font-size: 28px;
    line-height: 1.4;
    padding: 60px;
    max-width: 1280px;
    margin: 0 auto;
    box-sizing: border-box;
    position: relative;
  }

  section::before {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 4px;
    background: linear-gradient(90deg, var(--4linux-green) 0%, #f15a29 100%) !important;
    z-index: 10;
  }

  section p {
    margin-bottom: 0.8em;
    max-width: 100%;
    word-wrap: break-word;
    hyphens: auto;
  }

  section ul {
    margin-left: 1.2em;
    max-width: calc(100% - 1.2em);
  }

  section li {
    margin-bottom: 0.5em;
    line-height: 1.3;
    word-wrap: break-word;
    hyphens: auto;
  }

  section h1 {
    font-size: 2.4em;
    font-weight: 700;
    color: var(--4linux-green);
    text-shadow: 0 0 20px rgba(0, 230, 204, 0.3);
    margin-bottom: 0.8em;
    line-height: 1.1;
    border-bottom: none;
    white-space: normal;
  }

  section h2 {
    font-size: 2.2em;
    font-weight: 600;
    color: var(--color-foreground);
    margin-bottom: 0.8em;
    position: relative;
  }

  section h2::before {
    content: "";
    position: absolute;
    left: -25px;
    top: 50%;
    transform: translateY(-50%);
    width: 4px;
    height: 50px;
    background: linear-gradient(135deg, var(--4linux-green), var(--4linux-blue));
    border-radius: 2px;
  }

  section h3 {
    font-size: 1.6em;
    font-weight: 500;
    color: var(--4linux-blue);
    margin-bottom: 0.6em;
  }

  section strong {
    color: var(--4linux-green);
    font-weight: 700;
  }

  section code {
    background: rgba(0, 230, 204, 0.1);
    color: var(--4linux-green);
    padding: 0.2em 0.5em;
    border-radius: 4px;
    font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', monospace;
    border: 1px solid rgba(0, 230, 204, 0.2);
  }

  section pre {
    background: #060e1a;
    border: 1px solid rgba(0, 230, 204, 0.25);
    border-radius: 8px;
    padding: 1em 1.2em;
    margin: 0.6em 0;
  }

  section pre code {
    background: transparent;
    border: none;
    padding: 0;
    color: #e2e8f0;
    font-size: 0.82em;
    line-height: 1.6;
  }

  section ul li::marker {
    color: var(--4linux-green);
  }

  section::after {
    font-weight: 500;
    content: attr(data-marpit-pagination) ' / ' attr(data-marpit-pagination-total);
    font-size: 14px;
    color: var(--4linux-green);
    background: none;
    border: none;
    box-shadow: none;
    backdrop-filter: none;
    padding: 0;
    border-radius: 0;
    position: fixed;
    top: 25px;
    right: 30px;
  }

---
<!-- _paginate: false -->
<!-- _footer: "" -->
<style scoped>
section {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 50px 70px;
  text-align: left;
}
.tag {
  align-self: flex-start;
  background: rgba(0, 230, 204, 0.12);
  border: 1px solid rgba(0, 230, 204, 0.45);
  color: #00E6CC;
  padding: 6px 16px;
  border-radius: 20px;
  font-size: 0.7em;
  font-weight: 700;
}
.content { display: flex; justify-content: space-between; align-items: center; gap: 40px; }
h1 { font-size: 2.2em; line-height: 1.2; margin: 0 0 20px 0; color: #F8FAFC; text-align: left; }
.highlight { color: #00E6CC; }
.speaker { margin-top: 25px; border-left: 4px solid #00E6CC; padding-left: 15px; }
.logo-card { background: #FFFFFF; border-radius: 16px; padding: 18px; box-shadow: 0 0 30px rgba(0, 230, 204, 0.15); }
.footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 14px;
  font-size: 0.7em;
  color: #8B9DC3;
}
</style>

<div class="tag">DevOps Days Juiz de Fora 2026</div>

<div class="content">
<div>
<h1>Velero + RustFS:<br><span class="highlight">backup open source</span><br>para clusters Kubernetes</h1>

<div class="speaker">
<strong style="font-size: 1.2em; color: #F8FAFC;">Emerson Silva</strong>
</div>
</div>

<div class="logo-card"><img src="logos/event-logo.png" width="220"></div>
</div>

<div class="footer">
<span>Cloud Native &amp; Open Source Infrastructure</span>
<img src="4linux-logo/logo-4linux.png" height="36">
</div>

---
<!-- _paginate: false -->
<style scoped>
section {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  gap: 50px;
}
.wi-photo {
  flex-shrink: 0;
  width: 230px;
  height: 230px;
  object-fit: cover;
  border-radius: 20px;
  border: 3px solid rgba(0, 230, 204, 0.35);
  box-shadow: 0 0 30px rgba(0, 230, 204, 0.15);
}
</style>

<div>

# 🇧🇷 Emerson Silva

* Engenheiro DevOps na **4Linux**
* +9 anos em ambientes DevOps críticos
* Foco em **Kubernetes**, IaC e confiabilidade
* Palestrante, instrutor,escritor , ex-zagueiro 
* Community Lead de Kubernetes na DOUGBrazil
* Organizador do CNCF Campinas

</div>

<div style="display:flex; flex-direction:column; align-items:center; gap:20px;">
  <img class="wi-photo" src="eu-rsrs/perfil2.png">
  <div style="display:flex; align-items:center; gap:24px;">
    <img src="images/cncf-campinas.png" height="60">
    <img src="images/doug.png" height="60">
  </div>
</div>

---
<!-- _paginate: false -->
<!-- _footer: "" -->
<style scoped>
section { padding: 50px 60px 70px 60px; text-align: center; }
h2 { font-size: 1.4em; color: #8B9DC3; font-weight: 400; margin-bottom: 0.3em; letter-spacing: 0.05em; text-transform: uppercase; }
h2::before { display: none; }
p { font-size: 0.85em; color: #c8d4e8; line-height: 1.6; max-width: 72%; margin: 0 auto 1.6em auto; text-align: center; }
.timeline { display: flex; align-items: flex-start; gap: 0; width: 100%; margin-top: 0.5em; position: relative; }
.timeline::before { content: ""; position: absolute; top: 22px; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, #00E6CC, #4ECDC4, #f15a29); }
.tl-item { flex: 1; text-align: center; position: relative; padding-top: 40px; }
.tl-item::before { content: ""; position: absolute; top: 16px; left: 50%; transform: translateX(-50%); width: 12px; height: 12px; border-radius: 50%; background: #00E6CC; border: 2px solid #0B1426; z-index: 1; }
.tl-year { font-size: 0.9em; font-weight: 700; color: #00E6CC; display: block; }
.tl-label { font-size: 0.6em; color: #8B9DC3; display: block; margin-top: 2px; line-height: 1.2; }
</style>

![height:52px](4linux-logo/logo-4linux.png)

Fundada em 2001, a 4Linux participou das principais transformações da área de tecnologia. Começamos com Linux e software livre, navegamos por Cloud, DevOps e Containers — e hoje atuamos com agentes de IA, sempre com base em **inovação aberta**.

<div class="timeline">
  <div class="tl-item"><span class="tl-year">2001</span><span class="tl-label">Linux &<br>Software Livre</span></div>
  <div class="tl-item"><span class="tl-year">2008</span><span class="tl-label">DevOps</span></div>
  <div class="tl-item"><span class="tl-year">2016</span><span class="tl-label">Containers &<br>Kubernetes</span></div>
  <div class="tl-item"><span class="tl-year">2019</span><span class="tl-label">Machine<br>Learning</span></div>
  <div class="tl-item"><span class="tl-year">2020</span><span class="tl-year" style="color:#4ECDC4">Cloud</span></div>
  <div class="tl-item"><span class="tl-year">2024+</span><span class="tl-label">IA com<br>Open Source</span></div>
</div>


---
<!-- _paginate: false -->

## O que veremos hoje

1. Kubernetes não é backup
2. RPO e RTO
3. Estratégias de DR
4. Velero e RustFS
5. Demo: backup e restore entre clusters

---

## Kubernetes não é backup

* Kubernetes resolve **disponibilidade**: réplicas, self-healing, rolling update
* Não resolve **recuperação**: o que é apagado some em todas as réplicas
* **Réplicas replicam o estado ruim**

---

## O que pode dar errado

* `kubectl delete namespace` no cluster errado
* GitOps que sincronizou uma remoção indesejada
* Corrupção do etcd ou perda do control plane
* Perda de zona ou região inteira
* Credencial comprometida usada para apagar recursos

---

## RPO e RTO

| | Pergunta | Exemplo |
|--|--|--|
| **RPO** | Quanto dado posso perder? | Backup a cada 6h: até 6h perdidas |
| **RTO** | Quanto tempo fora do ar? | Detectar, decidir, restaurar, validar |

> Esses dois números definem a frequência do backup e o quanto o restore precisa ser automatizado

---

## O que um backup precisa cobrir

* **Recursos da API**: Deployments, Services, ConfigMaps, Secrets, CRDs, RBAC
* **Dados de volumes**: bancos, uploads, filas
* Backup só de manifesto é **restauração parcial**

---

## Estratégias de DR

| Estratégia | Como funciona | Quando faz sentido |
|--|--|--|
| Backup e restore | Snapshots em storage externo, restore sob demanda | Maioria dos casos |
| Warm standby | Cluster secundário reduzido, dados replicados | RTO menor, com custo de manter dois ambientes |
| Active-active | Dois ambientes servindo tráfego | RTO e RPO próximos de zero, complexidade alta |

> Para a maioria dos times, backup e restore bem testado entrega mais valor

---

## O backup precisa sair do cluster que pode cair

* Se o backup mora no mesmo cluster, o desastre leva os dois
* Armazenamento externo, independente do cluster
* Object storage S3: barato, escalável, retenção longa
* O cluster de DR precisa **enxergar** o backup

---

<style scoped>
section { justify-content: flex-start !important; padding-top: 10px !important; }
</style>

<div style="text-align:center; margin-top:-70px;"><div style="background:#FFFFFF; border-radius:16px; padding:18px 26px; display:inline-block;"><img src="images/velero-logo.svg" height="110"></div></div>

* Ferramenta open source, originalmente da VMware
* Roda como controlador dentro do cluster
* Lê os recursos da API, empacota e envia para o storage
* No restore, recria os recursos em outro cluster que enxergue o mesmo storage

---

## Componentes do Velero

* **Velero server**: executa backups, restores e schedules
* **node-agent**: move dados de volumes quando não há snapshot
* **BackupStorageLocation (BSL)**: onde os backups são gravados
* **Backup, Restore, Schedule**: recursos que representam cada operação

---

<style scoped>
section { justify-content: flex-start !important; padding-top: 10px !important; }
</style>

<div style="text-align:center;"><div style="background:#FFFFFF; border-radius:16px; padding:18px 26px; display:inline-block;"><img src="logos/rustfs.png" height="90"></div></div>

* Object storage **compatível com S3**
* Escrito em **Rust**
* Modo distribuído com **erasure coding**: tolera a perda de nós
* Console web e API S3 no mesmo serviço


---

## Como o Velero fala com o RustFS

* Plugin AWS (`velero-plugin-for-aws`), porque o RustFS é S3
* `s3Url` apontando para o endpoint do RustFS
* `s3ForcePathStyle=true`
* `region=minio`, já que o RustFS aceita qualquer valor
* BSL `from-prd` **somente leitura** no DR

---

## Arquitetura

![w:1000](images/demo-arquitetura.svg)

---

## Demo

Prints do lab, na ordem do fluxo: storage, instalação, backup e restore.

---

## RustFS com um bucket por cluster

![w:1150](images/lab/03.png)

---

## Os dois clusters

![w:1150](images/lab/04.png)

---

## Velero instalado em produção

![w:1150](images/lab/05.png)

---

## BackupStorageLocation disponível

![w:1150](images/lab/06.png)

---

## BSL somente leitura no DR

![w:1150](images/lab/08.png)

---

## Aplicação rodando em produção

![w:1150](images/lab/10.png)

---

## Backup criado

![w:1150](images/lab/11.png)

---

## Detalhes do backup

![h:500](images/lab/13.png)

---

![h:620](images/lab/14.png)

---

## Antes do restore: o DR não tem a aplicação

![w:1150](images/lab/15.png)

---

## Backup visível no DR e restore disparado

![w:1150](images/lab/16.png)

---

## Restore concluído

![h:520](images/lab/17.png)

<!-- Warning esperado: o ConfigMap kube-root-ca.crt já existe no DR. Explicar que é esperado e não afeta o restore. -->

---

## Recursos recriados no DR

![w:1150](images/lab/18.png)

---

## Schedule diário

![w:1150](images/lab/19.png)

<!-- Extra: mostrar só se sobrar tempo. -->

---
<!-- _paginate: false -->

## Conclusão

* **Backup de Kubernetes é obrigatório**
* **Teste o restore antes do desastre**
* **Velero + RustFS: open source de ponta a ponta**

<div class="final-message">
  <p>Backup que nunca foi restaurado <strong>não é backup</strong></p>
</div>

---
<!-- _paginate: false -->

## Curso gratuito

![bg right:45% 70%](images/qrcode-curso.png)

### DevOps, AIOps e SRE Fundamentals

Curso gratuito da 4Linux

Escaneie o QR code pra se inscrever

* 🎓 4linux.com.br/cursos

---
<!-- _paginate: false -->
<!-- _footer: "" -->

## Obrigado!

![bg right:45% 70%](images/qrcode.png)

### Contato

* 💻 github.com/silvemerson/infra-velero-rustfs
* 📖 velero.io
* 📝 emerson-silva.blog.br
* 💬 @silvemerson

Vamos manter contato!

<img src="4linux-logo/logo-4linux.png" height="60" style="margin-top:1rem;">
