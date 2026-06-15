# desapego do Renato 👋

Página de uma página só (single-file) para vender móveis e eletros usados.
Cada item mostra preço "de / por", fotos e um botão **"dar um lance"** que abre o
WhatsApp já com a mensagem pronta. **Não tem banco de dados** — está tudo dentro do
`docs/index.html` (HTML, CSS, JavaScript e fotos em base64).

> A página fica em `docs/index.html` porque essa é a pasta pública servida pelo
> **Cloudflare Workers** (host único) — uma pasta limpa só com o `index.html`, assim
> nada de interno (memórias, CLAUDE.md) é exposto no site.

🔗 **Site no ar:** https://desapego.renattowolf.workers.dev/  (Cloudflare Workers)
📦 **Repositório:** https://github.com/renattomoreira/desapego
📱 **Contato dos lances:** WhatsApp `+55 19 99661-4321` (Renato)

---

## Como atualizar o site

Tudo é editado no `docs/index.html`, na lista `ITEMS` dentro do `<script>` (tem um comentário
"COMO ATUALIZAR ESTE SITE" explicando lá no topo). Cada item é assim:

```js
{
  "id": "geladeira-lg",                 // identificador único (sem espaços)
  "title": "Geladeira LG ...",          // nome do objeto
  "description": "Detalhes ...",        // descrição
  "pricePaid": 16990,                   // preço "de" (quanto custou / na internet)
  "askingPrice": 10000,                 // preço "por" (quanto você quer)
  "refs": ["https://..."],              // links de referência (pode deixar [])
  "photos": ["data:image/jpeg;base64,..."], // fotos como data URL (base64)
  "sold": false                         // true = VENDIDO (fica cinza, sem botão de lance)
}
```

### Tarefas rápidas

| Quero... | O que fazer |
|----------|-------------|
| **Marcar como vendido** | trocar `"sold": false` por `"sold": true` no item |
| **Adicionar item novo** | copiar um bloco `{ ... }` inteiro e ajustar os campos |
| **Trocar o contato** | editar `OWNER = { name, whatsapp }` (formato `55` + DDD + número) |
| **Trocar uma foto** | substituir a string `data:image/...;base64,...` em `photos` |

### Publicar a mudança

```bash
# 1) publica no Cloudflare (jeito garantido)
npx wrangler deploy

# 2) versiona a mudança no GitHub
git add docs/index.html && git commit -m "atualiza itens do desapego" && git push
```

O `wrangler deploy` atualiza o site em segundos. (Se o projeto estiver conectado ao
GitHub no painel do Cloudflare, o `git push` também dispara um rebuild automático.)

---

## Itens atuais

| Item | Preço (por) | Status |
|------|-------------|--------|
| Geladeira LG Side by Side InstaView 598L | R$ 10.000 | disponível |
| Mesa de Jantar Artzzi — vidro preto (até 8 lugares) | R$ 5.000 | disponível |
| 8 Cadeiras de Jantar Biju — estofado cinza | R$ 4.000 | disponível |
| 2 Poltronas Dot — madeira imbuia e pés dourados | R$ 4.000 | disponível |
| 2 Mesas de Centro Artzzi — formato orgânico | R$ 10.000 | disponível |
| Mesa de Canto Artzzi — vidro e base preta | R$ 1.700 | disponível |
| Lava e Seca Samsung 11kg Ecobubble — branca | R$ 1.500 | disponível |
| Esteira NordicTrack (dobrável) | R$ 800 | ✅ vendido |
| Geladeira Expositora Gelopar — porta de vidro | R$ 2.500 | ✅ vendido |

---

## Stack

- **HTML + CSS + JS** num único arquivo (`docs/index.html`).
- Fontes via Google Fonts (Fredoka + Nunito).
- Hospedagem: **Cloudflare Workers** (assets estáticos), servindo `docs/`.
- Zero dependências, zero build. É só abrir o arquivo ou acessar o link.

## Rodar localmente

Basta abrir o `docs/index.html` no navegador (duplo clique), ou servir a pasta:

```bash
cd docs && python3 -m http.server 8000
# depois acesse http://localhost:8000
```

## Deploy no Cloudflare (manual, se precisar)

O `wrangler.jsonc` já está configurado (serve `docs/` como assets estáticos). Para
publicar direto do terminal (sem depender do build automático):

```bash
npx wrangler login      # só na 1a vez / quando o token expirar
npx wrangler deploy     # publica em https://desapego.renattowolf.workers.dev/
```
