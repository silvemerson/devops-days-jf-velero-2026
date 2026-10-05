# Velero + RustFS: backup open source para clusters Kubernetes

Slides da palestra apresentada no **DevOps Days Juiz de Fora 2026**.

Lab usado para os prints da parte prática: [`silvemerson/infra-velero-rustfs`](https://github.com/silvemerson/infra-velero-rustfs) (repositório do lab).

---

<img src="logos/event-logo.png" height="200">

> `logos/event-logo.png` é o logo do evento. O logo da 4Linux fica em
> `4linux-logo/logo-4linux.png` e já aparece no rodapé de todo slide.

## Estrutura

```
slides.md          # conteúdo dos slides (Marp)
slides.html        # HTML de conferência gerado a partir do slides.md
docs/              # roteiro de texto da palestra
images/lab/        # prints do lab usados na parte prática
images/            # QR code e logos de comunidade
logos/             # logo do evento
4linux-logo/       # logo da 4Linux (rodapé)
eu-rsrs/           # foto do palestrante (slide de whoami)
```

## Como usar os slides

### Pré-requisito

```bash
npm install -g @marp-team/marp-cli
```

### Visualizar no browser com live reload

```bash
marp --watch slides.md
```

### Abrir o HTML já gerado

```bash
xdg-open slides.html
```

### Exportar para PDF

```bash
marp slides.md --pdf --allow-local-files -o slides.pdf
```

> `--allow-local-files` é necessário para carregar imagens e logos locais.

### Exportar para HTML

```bash
marp slides.md --html --allow-local-files -o slides.html
```
