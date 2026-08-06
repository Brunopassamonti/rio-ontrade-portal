# Jägermeister · Rio On-Trade — Portal + Tracker

Contexto para o agente. Projeto do Bruno Passamonti (Regional On-Trade & Trade Marketing Manager, Jägermeister Brasil / Interfood — SP e RJ). Tudo em **português do Brasil**.

## O que é

Dois artefatos que trabalham juntos:

1. **`index.html`** — o **portal** (site estático, um arquivo só). É a "porta de entrada" do sistema: entra por BA (Jerry, Julia, Iasmin) ou por projeto (Shots & Friends, Feierstarters, KSM, Visita do Board, Formação & Onboarding). Ele **não guarda dado** — só linka pra planilha-sistema do Google Sheets e pros decks no Drive.
2. **`assets/Plano_OnTrade_Rio_Tracker.xlsx`** — o **tracker** operacional (11 abas: Leia-me, Contas & Rota, Contratos, Tailor Made & Projetos, Account Excellence, Tracker de Decisões, BAM Rio, Radar ON6 Rio, Carteira Julia, Rota Semanal, Aprovação Contratos, Parâmetros Contrato). É o "motor" de dados. Mantido aqui como referência/base.

O objetivo imediato no Code é **publicar o portal no GitHub Pages** (o Bruno já usa `brunopassamonti.github.io`) para ele ganhar uma URL fixa — o que destrava os botões "voltar ao portal" nas planilhas.

## Identidade visual (NÃO alterar sem pedir)

Paleta atualizada em 06/08/2026 a pedido do Bruno (refactor da home — ver seção seguinte). Tokens no `:root` do `index.html`:
- Verde escuro: `--forest:#10271F` · Verde floresta: `--forest-3:#1F4A3A`
- Laranja: `--orange:#E87924`, `--orange-2:#FFB25D`
- Creme: `--cream:#F4F1E9` · Branco quente/papel: `--paper:#FBFAF6`
- Texto escuro: `--ink:#17201C` · Texto secundário: `--muted:#68736D`
- Fonte: **Inter** (importada do Google Fonts)
- Raio grande, sombras suaves, cards translúcidos, bastante espaço em branco. Estética executiva, sóbria — evitar excesso de ícones e gráficos decorativos.

**Regra de linguagem:** nada de termo genérico de IA (ex.: "transformar X em Y", "única verdade / single source of truth", "visões automáticas", "solução robusta", "jornada"). Tom de campo, frase curta e concreta, voz do Bruno.

## Estrutura da home (index.html) — refeita em 06/08/2026

A home é a porta de entrada executiva: responde rápido "como está o resultado", "como está cada BA", "onde está a estratégia", "onde preencher planilha", "onde estão os arquivos". Não tenta mostrar o sistema inteiro. Ordem fixa:

1. **Hero curto** (`#top`) — título "JÄGERMEISTER RIO ON-TRADE", sem painel de métricas (isso é o bloco seguinte). Botões: Abrir sistema completo · Apresentação estratégica.
2. **`#score`** — "Score atual Rio", bloco inteiro clicável (abre o Dashboard Rio, gid `567808762`). 5 indicadores: contas na base (132), cobertura do ciclo (—), Perfect Outlets (—), contratos ativos (—), projetos ativos (13). "—" = sem fórmula validada, não inventar número.
3. **`#time`** — 3 cards de Brand Ambassador (Jerry, Julia, Iasmin), versão executiva — sem Instagram/"tocando agora" (removido nesse refactor). Cada um linka pro próprio hub.
4. **`#pilares`** — "Arquitetura de gestão": Pessoas · Estratégia · **Operação** (era "Execução") · Governança.
5. **`#arquivos`** — Central de arquivos: accordion "Preenchimento de planilhas" (6 links) + 3 cards de Biblioteca (Estratégia/Brand assets/Projetos) apontando pra pastas do Drive ainda não configuradas (`APP_LINKS.driveStrategyUrl/driveBrandUrl/driveProjectsUrl` vazios — ver README).
6. **`#acessos`** — atalhos: BAM semanal, Projetos, Contratos, Biblioteca (scroll interno), Decisões.
7. **Footer + dock mobile** (5 itens: Home/Score/Time/Pilares/Arquivos).

Todos os links vêm de `APP_LINKS` (objeto no `<script>` no fim do arquivo) via atributo `data-link`/`data-drive` — nunca hardcodar URL direto num `<a>`. Detalhe de cada chave no `README.md`.

**Removido da home nesse refactor** (não apagado do projeto, só fora da capa por enquanto — decidir com o Bruno se volta em outro lugar): o accordion de projetos (Shots & Friends, Feierstarters, KSM, Visita do Board, Formação), o painel "Seis bases" (system-grid) e o "Fluxo da semana" (5 passos do BAM). Isso também significa que a pendência antiga "trocar `href=\"#\"` nas apresentações de Shots/KSM/Board" não se aplica mais à home — esses cards não estão mais aqui.

## PENDÊNCIAS (o que falta — trabalhar por aqui)

1. **Publicar no GitHub Pages** → obter a URL viva. (desbloqueia o item 2)
2. **Back-links "⌂ Portal"**: colocar em cada aba da planilha-sistema E no tracker, apontando pra URL viva. Na planilha, célula com `=HYPERLINK("<URL>";"⌂ Portal")`.
3. ~~Apresentações com placeholder `#` (Shots & Friends, KSM, Visita do Board)~~ — **obsoleto**: esse accordion saiu da home no refactor de 06/08/2026. Só volta a valer se esse conteúdo voltar pra algum lugar (ver nota em "Estrutura da home").
4. **Dois PDFs sem lugar definido** (decidir com o Bruno):
   - `Book Materiais Jäger Interfood Ontrade.pdf` — catálogo de materiais/contrapartidas. Candidato natural: card "Estratégia e apresentações" ou "Brand assets" na Central de Arquivos, uma vez que a pasta do Drive for configurada.
   - `Copa Brand Ambassadors.pdf` — deck de BAs pra Copa. Sem card óbvio na home atual (não tem mais seção de projetos) — decidir com o Bruno onde entra.
5. **Números do Score Rio** (132 contas, 13 projetos confirmados; cobertura/Perfect Outlets/contratos ativos ainda "—") — falta a fórmula consolidada pra tirar os "—".
6. **Gids dos hubs por BA** (`203608001/2/3`) — são sequenciais/placeholder; confirmar se as abas existem ou repontar.
7. ~~@ do Instagram da Julia~~ — **obsoleto**: os cards de BA na home não mostram mais Instagram/"tocando agora" (removido no refactor de 06/08/2026, era considerado "excesso de ícone" pro tom executivo pedido).
8. **3 pastas do Drive não configuradas** na Central de Arquivos: `driveStrategyUrl`, `driveBrandUrl`, `driveProjectsUrl` em `APP_LINKS` (index.html) — hoje mostram "Configurar pasta" e ficam desabilitadas.
9. **Link da Apresentação estratégica** (botão do hero) — `APP_LINKS.strategicPresentation` está vazio, botão desabilitado até o Bruno mandar o link.

## IDs e links úteis (pra não precisar buscar de novo)

- **Planilha-sistema** (Google Sheets): `1hpSocZz0uyTp9FD0gmG1giaBdN0Kyvt9cMVXsQFpzRY`
  - gids: Master de Contas `1816223299` · BAM Semanal `1371488152` · Rota `1219122168` · Account Excellence `313439215` · Contratos & Investimentos `757531670` · Projetos & Eventos `966247200` · Tracker de Decisões `1919488920` · Scorecards `1405195389` · Dashboard `567808762` / `936608885` · hubs BA `203608001` (Jerry) / `203608002` (Julia) / `203608003` (Iasmin) / arquitetura `203608004`
- **Feierstarters (deck, Slides):** `1DuvnR93YTCv9me5UN1qhI5McLUFPlEuAomDIayuD2Vg` — JÁ LIGADO
- **Manual do BA (Doc):** `1QkvfqrielIvv3oNL7Y8YmwgsDn69PIC0ivOdRaoI4LE` — JÁ LIGADO
- **Guia de Onboarding (Doc):** `1EslX32CrlXz5I8JcwyIqY7mTt2vbF_UYl5SEMGL0bmY` — JÁ LIGADO
- **Book Materiais (PDF):** `1MXH_bKKPS9-l99QJQqVrFnE42YBkuCqF` — a posicionar
- **Copa Brand Ambassadors (PDF):** `1uptKZa7TYbEDJXC7DSoLuUCSb2yDrCeW` — a posicionar
- **Pasta Drive dos projetos:** `11fpUvZksz5fifkcqazcQVBk3Fpawyew7`

## Convenções técnicas

- É um único HTML, sem build. CSS e (mínimo) JS inline. Sem framework.
- Não usar `localStorage`/`sessionStorage`.
- Preview local: `python3 -m http.server 8000` e abrir `http://localhost:8000`.
- Ao editar o portal, **não** aninhar `<a>` dentro de `<a>` (os cards de BA já foram convertidos pra `<div>` por isso).
