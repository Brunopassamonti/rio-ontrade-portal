# Rio On-Trade Portal — como levar pro Claude Code

Pasta pronta pra continuar o projeto no Claude Code e publicar no GitHub Pages.

## O que tem aqui

```
rio-ontrade-portal/
├─ index.html        → o portal (já renomeado pra index.html, padrão do Pages)
├─ CLAUDE.md         → briefing que o Claude Code lê sozinho ao abrir a pasta
├─ README.md         → este arquivo
└─ assets/
   └─ Plano_OnTrade_Rio_Tracker.xlsx   → o tracker (referência/dados)
```

## Passo a passo

**1. Descompacte** o zip numa pasta sua, ex.: `~/projetos/rio-ontrade-portal`.

**2. Abra a pasta no Claude Code.**
- No app desktop: aba **Code** → abrir a pasta.
- No terminal: `cd ~/projetos/rio-ontrade-portal` e rode `claude`.

Ao abrir, o Claude Code lê o `CLAUDE.md` e já entende o projeto, o estilo e o que falta.

**3. Veja rodando (opcional):**
```bash
python3 -m http.server 8000
```
Abra `http://localhost:8000`.

**4. Publique no GitHub Pages** (você já usa `brunopassamonti.github.io`). Peça ao Claude Code:
> "Inicia o git, cria o repositório no GitHub e ativa o GitHub Pages na branch main / raiz. Me devolve a URL."

Ou na mão: cria o repo, `git init && git add . && git commit -m "portal" && git push`, e em **Settings → Pages** aponta pra `main` / `/root`. A URL fica tipo `https://brunopassamonti.github.io/rio-ontrade-portal/`.

**5. Com a URL na mão, feche o ciclo.** Peça:
> "Coloca um back-link '⌂ Portal' no topo de cada aba da planilha e no tracker, apontando pra <URL>."

Na planilha, é uma célula com `=HYPERLINK("<URL>";"⌂ Portal")`.

**6. Conecte as apresentações que faltam.** Conforme você for mandando os links (Shots & Friends, KSM, Visita do Board), peça ao Code pra trocar o `href="#"` do item certo. O mapa de pendências está no `CLAUDE.md`.

## O que já está feito

- Portal completo: hero, cards de BA descontraídos (@Instagram + "tocando agora"), projetos em accordion, sistema, pilares (com **Execução**), fluxo e dock mobile.
- Linguagem revisada (sem termo genérico de IA), fonte Inter carregada.
- Já ligados: **Feierstarters** (deck), **Manual do BA** e **Guia de Onboarding**.

## O que falta (resumo — detalhe no CLAUDE.md)

1. Publicar no Pages → URL viva.
2. Back-links "⌂ Portal" nas planilhas.
3. Apresentações ainda em `#`: Shots & Friends, KSM, Visita do Board.
4. Posicionar 2 PDFs: Book de Materiais e Copa Brand Ambassadors.
5. Conferir números do hero e os gids dos hubs.
6. @Instagram da Julia.

## Como configurar a home (após o refactor)

Todos os links do `index.html` vêm de um único objeto de configuração, dentro da tag `<script>` no fim do arquivo (`APP_LINKS`, perto da linha 300). Nunca edite uma URL direto num `<a>` — troque no objeto e o link se atualiza em todo lugar que usa aquela chave via `data-link="..."`.

**Links de planilha** — `APP_LINKS.jerryHub`, `.dashboardRio`, `.pilarPessoas` etc. são todos gerados a partir de `SHEET_ID` + `gid`. Se o gid de uma aba mudar, troque só o número passado pra função `sheet("...")`.

**Apresentação estratégica** — `APP_LINKS.strategicPresentation` está vazio de propósito (não tínhamos o link). Enquanto estiver `""`, o botão do hero fica desabilitado. Cole a URL aí quando o Bruno mandar.

**Pastas do Drive (Biblioteca de arquivos)** — três chaves vazias esperando URL:
- `APP_LINKS.driveStrategyUrl` → Estratégia e apresentações
- `APP_LINKS.driveBrandUrl` → Brand assets
- `APP_LINKS.driveProjectsUrl` → Projetos e ações

Enquanto vazias, os cards aparecem como "Configurar pasta" e não são clicáveis. Basta colar o link da pasta do Drive em cada chave.

**Números dos indicadores (Score Rio e cards de BA)** — não vêm de fórmula, são texto fixo no HTML: procure a seção `id="score"` (contas na base, projetos ativos) e `id="time"` (métricas de cada BA, dentro de `.ba-metrics`). Indicadores marcados com "—" ainda não têm fórmula validada — só troque o "—" por um número quando o cálculo (cobertura, perfect outlets, contratos ativos consolidados) estiver fechado.

**Textos dos Brand Ambassadors** (cargo, foco, status) — ficam em texto direto dentro de cada `.ba-card`, seção `id="time"`.

## O que ficou de fora da home nesse refactor

O accordion de projetos (Shots & Friends, Feierstarters, KSM, Visita do Board, Formação), o painel "Seis bases" e o "Fluxo da semana" (5 passos do BAM) saíram da página inicial — a nova home segue à risca a ordem pedida (hero, Score Rio, BA, pilares, central de arquivos, acessos, footer) e não tenta mostrar o sistema inteiro. Esse conteúdo não foi apagado do histórico do projeto, só não está mais na home; se quiser manter em algum lugar (uma página `/sistema.html` separada, por exemplo), é só pedir.

## Observação

O tracker (`assets/…xlsx`) tem os conectores do Google Sheets já usados no Claude.ai. Se quiser continuar mexendo em dado/planilha, dá pra fazer no Claude.ai (conectores prontos) e deixar o Claude Code focado no site — ou trazer tudo pro Code, como preferir.
