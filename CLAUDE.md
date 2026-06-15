# INSTRUÇÕES DO PROJETO — DESAPEGO

> **Página de desapego do Renato** — site de uma página só (single-file) para vender
> móveis e eletros usados. Cada item tem botão "dar um lance" que abre o WhatsApp
> pré-preenchido. Sem banco de dados: tudo vive dentro do `index.html`.

## O QUE É ESTE PROJETO

- **Tipo:** Site estático de uma página (HTML + CSS + JS embutidos num arquivo só).
- **Arquivo principal:** `docs/index.html` — contém o estilo, a lógica e as fotos (base64 inline).
  Fica em `docs/` porque essa é a pasta pública servida pelo Cloudflare (pasta limpa só com o
  index → nada de interno é exposto). **Nunca mover de volta pra raiz** sem reconfigurar o `wrangler.jsonc`.
- **Como atualizar:** editar a lista `ITEMS` dentro do `<script>` em `docs/index.html`. As
  instruções completas estão no comentário "COMO ATUALIZAR ESTE SITE" no topo do script.
- **Contato:** `OWNER = { name: "Renato", whatsapp: "5519996614321" }` (55 + DDD 19 + número).
- **Hospedagem:** **Cloudflare Workers** (host único) — `wrangler.jsonc`, assets=`./docs`,
  URL `desapego.renattowolf.workers.dev`. (GitHub Pages foi desativado em 2026-06-14.)
  O link é compartilhado com compradores para darem lances via WhatsApp.

### Tarefas comuns
- **Marcar item como vendido:** trocar `"sold": false` por `"sold": true` no item.
- **Adicionar item:** copiar um bloco `{ ... }` inteiro dentro de `ITEMS` e ajustar
  `title`, `description`, `pricePaid` (preço "de"), `askingPrice` (preço "por"),
  `refs` (links de referência) e `photos` (imagens em base64 / data URL).
- **Publicar mudança:** `npx wrangler deploy` (publica no Cloudflare em segundos), depois
  `git add docs/index.html && git commit -m "..." && git push` pra versionar.

---

## COMPORTAMENTO-BASE

**Antes de toda resposta, leia o arquivo `ARQUITETURA-MENTAL.md` nesta pasta.** Ele define como você processa informação e é a base de todo o seu comportamento.

Hierarquia obrigatória — nunca inverta esta ordem:

```
1. DISCERNIR    → O que realmente está sendo pedido?
2. CONHECER     → Para onde? Por quê?
3. ENTENDER     → Como funciona?
3.5 MODO DE CAÇA → Existe forma de vencer sem lutar? Big Domino?
4. SABEDORIA    → Ação certa?
5. AGIR         → O que aprender disso?
```

**Nunca pule etapas. Nunca comece pela solução.**

Frase-âncora:
```
Discernir primeiro.
Entender depois.
Caçar a alavanca.
Agir certo.
Separar o resultado.
Acumular vantagem.
Recomeçar mais alto.
```

---

## SISTEMA DE MEMÓRIA DO PROJETO

Este projeto usa 3 níveis de memória. **Leia sempre nesta ordem — do menor para o maior:**

1. `.memoria-ultimas-tarefas.md` — Leia **primeiro**. As 3 tarefas mais recentes. Rápido e direto ao ponto.
2. `.memoria-do-dia.md` — Leia **segundo**. Log cronológico do dia atual.
3. `.memoria-projeto.md` — Leia **por último**, e somente se precisar de contexto mais amplo.

**Ao terminar qualquer tarefa, atualize os 3 níveis:**

- `.memoria-ultimas-tarefas.md` → Adicione a tarefa recém-concluída. Mantenha **apenas as 3 mais recentes** — remova a mais antiga ao adicionar nova.
- `.memoria-do-dia.md` → Adicione uma linha: hora + o que foi feito.
- `.memoria-projeto.md` → Atualize **apenas em mudanças estruturais**: nova feature implementada, decisão de arquitetura importante, bug crítico corrigido. Não registre detalhes do dia a dia aqui.

### Enforcement Automatico

Hooks globais em ~/.claude/settings.json detectam tarefas completadas e injetam lembretes obrigatorios antes da compactacao de contexto. Para funcionar:
- Os 3 arquivos de memoria DEVEM existir no projeto
- Hook PreCompact: detecta tarefas nao registradas e forca atualizacao
- Hook Stop: audita se memorias foram atualizadas na sessao
- Hook Estudador: detecta 2+ falhas sem solucao e recomenda ativacao do Estudador

---

## NOMENCLATURA

Use sempre nomes óbvios e descritivos que qualquer pessoa entenda sem explicação.

❌ ERRADO: `btn-cta`, `handleEvt`, `processData`, `util.js`, `x`, `data2`, `fix`, `wip`, `temp`
✅ CERTO: `botao-comprar-agora`, `ao-clicar-em-enviar`, `calcular-total-do-carrinho`, `formatar-data.js`, `preco-com-desconto`, `corrigir-calculo-de-frete`

**Regra:** Se você precisar de um comentário para explicar o que o nome significa, o nome está errado. Mude o nome.

---

## COMUNICAÇÃO

Toda vez que mencionar qualquer termo técnico, conceito de programação, nome de tecnologia, ou decisão que envolva escolha de ferramentas, inclua uma explicação simples em linguagem acessível.

**Formato:** escreva o termo técnico + inclua a explicação entre colchetes: o **quê** é + **por quê** estou usando + **analogia** (quando ajudar).

**Quando NÃO precisa explicar:** termos que o próprio usuário digitou na mensagem, ou que já usou antes na conversa.

---

## AMBIENTE DE TRABALHO

No início de cada sessão, identifique como o usuário está usando o Claude e adapte suas ações ao ambiente. No Claude.ai web, não tente criar arquivos locais.

---

# currentDate
Today's date is 2026-06-14.
