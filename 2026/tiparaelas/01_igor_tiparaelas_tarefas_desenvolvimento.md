# TiParaElas — Plano de Desenvolvimento (Ciclo 1) — Igor

**Estudante:** Igor — Curso Superior de Tecnologia em Sistemas para Internet (conhecimentos intermediários em Python)
**Orientação:** Prof. Bruno Gomes — NIC
**Período:** 23/09/2026 a 24/11/2026 — 9 sprints de 1 semana (quarta a terça)
**Projeto:** TiParaElas (Python/Django), em `../tiparaelas/` — repositório privado `https://github.com/nicifrn/tiparaelas`
**Fluxo de trabalho no repositório:** `https://github.com/nicifrn/nic_projetos_tarefas` — **leia antes de criar a primeira *branch***; ele é a norma e prevalece sobre o resumo da seção 4.

**Temática escolhida:** Painel público de indicadores de gênero na computação com dados abertos do INEP.

> **Leia este documento inteiro antes de começar a Sprint 1.** Ele diz *o que* fazer, *como* fazer e *o que precisa estar pronto* ao final de cada semana. O documento complementar de escrita do TCC é `01_igor_tiparaelas_tarefas_escrita.md`.

---

## Sumário

- [1. A ideia do trabalho](#1-a-ideia-do-trabalho)
- [2. O que será entregue](#2-o-que-será-entregue)
- [3. Estado atual do código](#3-estado-atual-do-código)
- [4. Fluxo de trabalho no repositório](#4-fluxo-de-trabalho-no-repositório)
- [5. Ambiente de trabalho](#5-ambiente-de-trabalho)
- [6. Rotina de trabalho (ritual das sprints)](#6-rotina-de-trabalho-ritual-das-sprints)
- [7. Sprints](#7-sprints)
- [8. Definição de pronto (vale para todas as sprints)](#8-definição-de-pronto-vale-para-todas-as-sprints)
- [9. Riscos e planos B](#9-riscos-e-planos-b)
- [10. Trabalhos futuros (Ciclo 2)](#10-trabalhos-futuros-ciclo-2)
- [11. Checklist de encerramento](#11-checklist-de-encerramento)

---

## 1. A ideia do trabalho

A plataforma TiParaElas tem **poucos dados próprios** (menos de 30 ações cadastradas) — insuficiente para sustentar um artigo baseado no acervo dela. Mas existe um conjunto de dados **público, abundante e oficial** sobre exatamente o tema do projeto: o **Censo da Educação Superior**, do **INEP**, que informa matrículas, ingressantes e concluintes **por ano, por UF, por curso e por sexo**.

**A ideia em uma frase:**

> Construir, dentro do TiParaElas, um painel público que visualiza a participação feminina nos cursos de computação no Brasil, a partir dos dados abertos do INEP e das estimativas de população do IBGE.

**Por que isso é um bom trabalho:**

- **Resolve o problema do volume de dados.** São milhares de registros oficiais, prontos e citáveis. Você não precisa levantar nada, nem classificar nada subjetivamente;
- **É o tema exato do WIT** (*Women in Information Technology*, da SBC), que é o alvo de publicação;
- **É trabalho de engenharia que você já sabe fazer:** importar dados, modelar, calcular indicadores e visualizar. Não há técnica nova difícil;
- **Entrega algo útil e permanente** para o projeto: um painel que qualquer pessoa pode consultar, e que se atualiza a cada novo Censo.

**Perguntas de pesquisa:**

- **QP1:** como evoluiu a participação feminina nos cursos de computação no Brasil ao longo da série disponível, em matrículas, ingressos e conclusões?
- **QP2:** como essa participação se distribui entre as unidades da federação e as regiões, em termos absolutos e proporcionais à população?
- **QP3:** a participação feminina varia entre as subáreas da computação, e o percentual de mulheres entre concluintes difere do percentual entre ingressantes?

> **QP3 é a pergunta com maior potencial de achado original.** Se a proporção de mulheres entre concluintes for sistematicamente **menor** que entre ingressantes, isso é evidência quantitativa de evasão diferencial por sexo ao longo do curso — e é exatamente o tipo de resultado que rende publicação.

**Um cuidado desde já:** a afirmação de que "a proporção de mulheres na computação caiu a partir dos anos 1980" é **verdadeira, mas vem da literatura**, não dos seus dados. A série do Censo disponível online não alcança os anos 1980. Use a literatura para contextualizar e **os seus dados apenas para o período que eles de fato cobrem**. Misturar as duas coisas é um erro que o revisor pega.

---

## 2. O que será entregue

1. **Indicadores da tela de transparência atual corrigidos** (Sprints 1, 2 e 6) — os erros de contagem conhecidos, diagnosticados e resolvidos, com testes que impedem que voltem.
2. **Base de dados oficial importada e modelada** — indicadores do Censo da Educação Superior para os cursos de computação, por ano, UF e área, com a procedência de cada registro rastreável até o arquivo de origem.
3. **Comando de importação reproduzível** — `python manage.py importar_censo`, com `--dry-run`, de modo que outra pessoa refaça a carga do zero.
4. **Painel público** dentro do TiParaElas, com 7 visualizações que respondem às três QPs.
5. **Menu de Transparência reorganizado** — submenus separando **os dados da plataforma** dos **dados do cenário nacional**.
6. **Exportação em CSV** dos agregados + **dicionário de dados**.
7. **Testes automatizados** dos indicadores, novos e antigos.
8. **TCC completo**, pronto para virar artigo (ver documento de escrita).

> **Por que a correção dos indicadores antigos entra no escopo:** o seu painel novo vai ficar **na mesma seção do site** que a tela de transparência atual, que hoje exibe números errados. Se um visitante vê um número confiável ao lado de um número errado, o site inteiro perde credibilidade — inclusive o seu trabalho. Além disso, corrigir os indicadores antigos produz o **módulo único de consultas** que o painel novo vai espelhar, e rende uma subseção de Resultados no TCC. É trabalho que se paga duas vezes.

---

## 3. Estado atual do código

Verificado no repositório local em 23/09/2026:

| Fato | Onde |
|---|---|
| A tela de transparência está na *branch* `feature/dashboard-transparencia`, commit `db6588b`, **ainda não integrada** à `main` nem à `develop` | `git log`, `git branch -a` |
| A *view* está em `apps/core/views.py` (*view* `transparencia`); o *template* é `apps/core/templates/dashboard.html` | — |
| O app `apps/dashboard/` está **vazio**, mas **já está registrado** em `INSTALLED_APPS` | `tiparaelas/settings/base.py:40` |
| A rota do app está **comentada** — basta descomentar | `tiparaelas/urls.py` |
| **Todos os três gráficos são de barras** (`type: 'bar'`), inclusive as séries mensais, que são dados temporais e pedem **linha** | `dashboard.html:347, 381, 414` |
| O mapa do Brasil em SVG é um *template* incluído **duas vezes** na mesma página, o que gera **`id` duplicados** (`SP`, `MG`, `Layer_1`...) | `dashboard.html:105 e 189`, `templates/publico/mapa-brasil.html` |
| O Chart.js vem do CDN **sem versão fixada** — não dá para informar a versão em Materiais e Métodos | `dashboard.html:279` |
| `Estado` tem apenas `sigla` e `nome`. **Não existe região nem população** | `apps/usuarios/models.py:587` |
| Convenção obrigatória do projeto: **nunca usar `choices`** — categorias são modelos próprios, com CRUD | `CLAUDE.md:238` do TiParaElas |
| **Boa notícia:** o menu **já tem um padrão de submenu pronto** — o item "Sobre" usa `nav-has-dropdown` / `nav-dropdown-trigger` / `nav-dropdown` / `nav-dropdown-item`, com os atributos ARIA | `templates/publico/menu.html` |
| O submenu é **100% CSS**, por `:hover` e `:focus-within` — **não há JavaScript envolvido**, e já existe a versão para telas pequenas | `static/assets/css/styles.css:249–309` e `1290–1309` |
| "Transparência" é hoje um item simples, sem submenu | `menu.html`, linha do `{% url 'transparencia' %}` |

### 3.1 Os erros de contagem que você vai corrigir

Estes erros **fazem parte do seu trabalho** (Sprints 1, 2 e 6). Eles estão listados aqui para você ter tudo em um lugar só:

| # | Problema | Efeito no número |
|---|---|---|
| 1 | Os indicadores de inspirações filtram só `is_ativo` e `is_avaliacao`, **sem verificar se a última avaliação foi aprovada**. A função `_qs_perfis_aprovados()` faz essa verificação, está no mesmo arquivo e **não é usada**. O mesmo ocorre na *view* `index` | Perfil **reprovado** entra na contagem e pode aparecer no *ranking* com um link que leva a **erro 404** |
| 2 | As consultas de ações divergem entre páginas: transparência e `index` filtram `is_validado`, `is_active` e `status`; a galeria (`acoes_galeria`) filtra só `is_validado` e `is_active` | O total do painel **não bate** com o que a galeria mostra |
| 3 | O *ranking* de inspirações monta a variável `nome` a partir do **e-mail** da usuária, e carrega `usuario__email` na consulta — mas o *template* exibe `nome_completo`, então `nome` nunca é usado | Carrega dado pessoal sem necessidade (contraria a **minimização de dados** da LGPD) |
| 4 | `tipos` é relação muitos-para-muitos: **uma ação com dois tipos é contada duas vezes** no gráfico por tipo. Ações sem tipo aparecem como "Outros" | A soma das barras fica **maior que o total de ações**, e "Outros" se confunde com um tipo real |
| 5 | Séries mensais: a janela cobre **6 meses**, mas o texto diz "últimos 5 meses". **Meses sem cadastro somem do gráfico** e o rótulo não mostra o ano | Gráfico com buraco silencioso e legenda ambígua ("set." de qual ano?) |
| 6 | `TruncMonth` com `USE_TZ = True` no **MySQL** depende das tabelas de fuso horário do servidor. Sem elas, o banco devolve `NULL` e a formatação da data gera **erro 500**. Em SQLite o problema não aparece | A página **quebra em produção** e funciona em desenvolvimento |
| 7 | Textos afirmam mais do que os dados mostram: "em tempo real" e "Cada ponto e barra acima representa mulheres liderando projetos de TI" (as barras são contagens de **ações**, não de mulheres) | Afirmação incorreta em página pública |

> **Quando cada um é resolvido:** o diagnóstico é a Sprint 1; os erros **1, 2, 3 e 6** (os que produzem número errado ou derrubam a página) são a Sprint 2; os erros **4, 5 e 7** (apresentação e texto) são a Sprint 6, quando você já estará mexendo nos gráficos dessa tela.

---

## 4. Fluxo de trabalho no repositório

Você trabalha **no repositório principal**, com *branches*. **Antes de criar a primeira, leia `https://github.com/nicifrn/nic_projetos_tarefas`.** Se houver divergência com o resumo abaixo, **ele prevalece** — e avise o orientador para eu corrigir este documento.

**Resumo do fluxo:**

1. **Confirme com o orientador qual é a *branch* base** — o repositório tem `main` e `develop`, e isso muda para onde o seu *pull request* aponta;
2. **Uma *issue* por tarefa** relevante da sprint;
3. **Uma *branch* por sprint** (ou por conjunto coeso de tarefas):
   ```
   git checkout develop
   git pull
   git checkout -b feat/painel-inep-modelagem
   ```
4. **Conventional Commits** — você já usou o padrão no commit `db6588b`:
   ```
   feat: adiciona modelo IndicadorEducacao e AreaCine
   feat: cria comando importar_censo com dry-run
   fix: usa grafico de linha na serie historica
   test: cobre calculo do percentual feminino
   docs: documenta o dicionario de dados do painel INEP
   ```
5. ***Pull request* ao final de cada sprint**, referenciando as *issues* ("Closes #12"), com print do antes e do depois. **Não acumule duas sprints em um PR.**
6. **Antes de abrir o PR:** `python manage.py test` passando, sem `print()` esquecido, sem importação não usada, sem arquivo de dados pesado versionado.

**Primeira coisa a resolver:** os seus commits aparecem com **dois nomes diferentes** (`adrian5g` e `Igor Ádrian`). Você vai precisar delimitar a sua contribuição no TCC, e isso atrapalha:

```
git config --global user.name "Igor Adrian"
git config --global user.email "seu-email@dominio"
```

Crie também um `.mailmap` na raiz unificando os dois nomes (combine com o orientador antes de commitar).

**Cuidado com conflitos:** a *branch* `feature/gerenciamento-tipos-evento` também altera `tiparaelas/urls.py`, `tiparaelas/settings/base.py` e os menus — os mesmos arquivos que você vai tocar ao ativar a rota do app `dashboard`. Combine a ordem de integração com a equipe.

---

## 5. Ambiente de trabalho

Restrições do laboratório, já confirmadas:

- **Windows**, máquinas **bloqueadas para instalação de aplicativos** — apenas bibliotecas via `pip` e ferramentas web gratuitas;
- **Já instalados:** Python, MySQL, Git, VS Code, MySQL Workbench/DBeaver, Chrome/Edge atualizado;
- **Sem Docker.**

Bibliotecas a instalar via `pip`, além do `requirements.txt` do projeto:

```
pandas
openpyxl
matplotlib
```

`openpyxl` é o que permite ler os arquivos `.xlsx` das sinopses do INEP pelo `pandas`. Opcional, se quiser explorar os dados em *notebook*: `pip install notebook` (roda no navegador, sem instalador).

**Ferramentas web gratuitas:**

| Ferramenta | Para quê |
|---|---|
| Portal do INEP (`gov.br/inep`) | Sinopses Estatísticas da Educação Superior |
| Portal do IBGE (`ibge.gov.br`) | Estimativas da população por UF |
| Google Planilhas | Explorar as sinopses e montar a planilha normalizada |
| Google Acadêmico, SBC OpenLib (`sol.sbc.org.br`), SciELO, BDTD | Referências |
| Zotero Web (`zotero.org`) | Gestão das referências (não há Zotero desktop nas máquinas) |
| draw.io (`app.diagrams.net`) | Diagramas (fluxo das etapas, modelo de dados) |

---

## 6. Rotina de trabalho (ritual das sprints)

| Quando | O quê |
|---|---|
| **Quarta (início da sprint)** | Reler as tarefas, abrir as *issues*, criar a *branch*, tirar dúvidas antes de começar |
| **Todo dia que trabalhar** | Anotar no diário de bordo: o que fez, o que travou, **o que decidiu e por quê**. Commits pequenos e frequentes |
| **Terça (fim da sprint)** | Rodar os testes, abrir o *pull request*, conferir a "Definição de pronto", enviar os entregáveis |
| **Reunião semanal** | Mostrar funcionando (não só falar sobre), apresentar dificuldades, combinar ajustes |

**Crie um diário de bordo** em `docs/tcc-igor/diario/`, um arquivo `.md` por sprint. **Metade do capítulo de Materiais e Métodos sai dele.** Neste trabalho, em especial, anote **toda decisão sobre os dados**: qual tabela da sinopse você usou, qual critério definiu "curso de computação", o que fez quando um valor veio em branco. É isso que o revisor vai querer saber.

**Quando travar (regra dos 45 minutos):** tente sozinho por 45 minutos. Se não resolver, escreva no diário o que tentou e mande a dúvida com: (a) o que queria fazer, (b) o que fez, (c) a mensagem de erro completa, (d) o que já tentou.

---

## 7. Sprints

---

### Sprint 1 — Ambiente, diagnóstico e localização das fontes (23/09 a 29/09/2026)

**Objetivo:** ambiente rodando, fluxo de *branches* dominado, **os erros da tela atual reproduzidos e documentados** e **os arquivos de dados do INEP e do IBGE baixados e guardados**.

#### Tarefa 1.1 — Ambiente com MySQL

*Ajuda/direcionamento:*

1. `python --version` — anote a versão exata (vai para Materiais e Métodos);
2. Ambiente virtual e dependências:
   ```
   python -m venv venv
   .\venv\Scripts\Activate.ps1
   pip install -r requirements.txt
   pip install pandas openpyxl matplotlib
   ```
   Se o PowerShell bloquear a ativação: `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`;
3. No MySQL Workbench:
   ```sql
   CREATE DATABASE tiparaelas_dev CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   ```
4. Configure o `.env` para o MySQL local. **Nunca faça commit do `.env`**;
5. `python manage.py migrate`, `createsuperuser`, `runserver`;
6. Gere `pip freeze > requirements-dev.txt` e guarde — as versões exatas entram no TCC.

#### Tarefa 1.2 — Git e fluxo de trabalho

*Ajuda/direcionamento:* execute o que está na seção 4 — `git config`, `.mailmap`, leitura do `nic_projetos_tarefas`, confirmação da *branch* base com o orientador. Escreva no diário, em 10 linhas, o fluxo que você entendeu. Se estiver errado, o orientador corrige agora, e não depois de um PR problemático.

#### Tarefa 1.3 — Diagnosticar a tela de transparência atual

O seu painel novo vai conviver com essa tela, reaproveitar partes dela e — a partir da Sprint 2 — corrigi-la. **Não basta ler o diagnóstico: você precisa ver cada erro acontecer**, porque isso vira uma subseção dos seus Resultados no TCC.

*Ajuda/direcionamento:* crie `docs/tcc-igor/diagnostico_inicial.md`. Primeiro, a leitura do código:

1. Quais visualizações existem hoje e **qual tipo de gráfico** cada uma usa? (Confira `dashboard.html:347, 381, 414` — você vai encontrar `type: 'bar'` nas três, **inclusive nas séries mensais**. Anote: série temporal em barras é uma escolha inadequada de canal visual, e você vai corrigir isso na Sprint 6);
2. Como o mapa do Brasil é desenhado? Abra `templates/publico/mapa-brasil.html` e veja onde ele é incluído (`dashboard.html:105` e `189`). Anote que **o mesmo SVG entra duas vezes na página**, gerando `id` duplicados — você vai precisar resolver isso ao reaproveitar o mapa;
3. Como o Chart.js é carregado? (`dashboard.html:279` — CDN **sem versão**);
4. Como o menu está montado? Abra `templates/publico/menu.html` e repare que o item **"Sobre" já usa um padrão de submenu** pronto. Anote as classes — você vai replicá-las na Sprint 6.

Depois, **reproduza cada erro da tabela da seção 3.1**, com print e com **o número errado ao lado do número correto**:

- **Erro 1 (perfil reprovado).** Cadastre 3 perfis com `is_ativo=True` e `is_avaliacao=True`. Em um deles, registre uma `AvaliacaoInspiracao` com `is_aprovado=False`. Abra `/transparencia/`: o cartão conta **3**. Agora abra a página pública do perfil reprovado — dá **404**. Compare com o valor correto no *shell*:
  ```
  python manage.py shell
  >>> from apps.core.views import _qs_perfis_aprovados
  >>> _qs_perfis_aprovados().count()
  ```
- **Erro 2 (divergência entre páginas).** Crie uma ação com `status=False` e compare o número de ações em `/transparencia/`, na *home* e na galeria. Print dos três.
- **Erro 4 (dupla contagem).** Cadastre 3 ações e dê **2 tipos** a uma delas. O cartão dirá 3; a soma das barras do gráfico por tipo dará 4. Print dos dois.
- **Erro 5 (meses sumindo).** Conte quantos meses aparecem na série e compare com o texto da página. Veja que o rótulo não traz o ano.
- **Erro 6 (fuso horário).** Rode no MySQL local:
  ```sql
  SELECT CONVERT_TZ('2026-01-01 12:00:00', 'UTC', 'America/Sao_Paulo');
  ```
  Se retornar `NULL`, as tabelas de fuso não estão carregadas — e é isso que derruba a página. **Peça ao orientador para rodar o mesmo comando no servidor de produção** e anote as duas respostas.
- **Erros 3 e 7.** Confirme lendo o código e copie as frases problemáticas da página.

5. Tire prints da tela atual e salve em `docs/tcc-igor/figuras/baseline/`. **Guarde esses prints com cuidado** — eles são o "antes" do quadro antes/depois do TCC.

#### Tarefa 1.4 — Localizar e baixar os dados do INEP

Esta é a tarefa mais importante da semana. **Se os dados não estiverem em mãos até terça, a sprint não fechou.**

*Ajuda/direcionamento:*

1. Acesse o portal do INEP (`gov.br/inep`) e procure por **"Sinopses Estatísticas da Educação Superior"**. São planilhas `.xlsx` já agregadas, publicadas uma por ano;
2. **Use as sinopses, não os microdados.** Os microdados do Censo trazem um registro por aluno e ocupam vários gigabytes — inviável no laboratório. As sinopses já vêm agregadas por UF, curso e sexo, que é exatamente o recorte de que você precisa;
3. **Baixe os últimos 10 anos disponíveis** (ou o máximo que conseguir). **Confirme qual é o ano mais recente publicado** — não assuma; anote a data de acesso de cada arquivo;
4. Guarde os arquivos em `docs/tcc-igor/dados/inep/`, **com o nome original**, e crie um `FONTES.md` registrando, para cada arquivo: ano de referência, nome da tabela, URL completa, data de acesso e tamanho. Essa rastreabilidade é exigência do método;
5. **Não versione os arquivos grandes no Git.** Acrescente `docs/tcc-igor/dados/` ao `.gitignore` e mantenha os arquivos em backup na nuvem, combinando com o orientador onde.

#### Tarefa 1.5 — Baixar as estimativas de população do IBGE

*Ajuda/direcionamento:* no portal do IBGE, procure por **"Estimativas da População"** — a tabela por UF, do ano mais recente. Você vai usá-la para o indicador proporcional ("matrículas femininas por 100 mil habitantes"), que é o que evita que o mapa apenas reproduza o mapa da população. Registre a URL e a data de acesso no mesmo `FONTES.md`.

*Definição de pronto da Sprint 1:*
- [ ] Projeto rodando com MySQL local; versões anotadas
- [ ] `git config` e `.mailmap` resolvidos; fluxo lido; *branch* base confirmada
- [ ] `diagnostico_inicial.md` com as respostas de leitura do código **e os 7 erros reproduzidos**, com print e número errado × número correto
- [ ] Resultado do `CONVERT_TZ` anotado, no local **e em produção**
- [ ] Prints da linha de base salvos
- [ ] Sinopses do INEP de ~10 anos baixadas, com `FONTES.md` preenchido
- [ ] Estimativas do IBGE baixadas e registradas
- [ ] Pasta de dados fora do controle de versão
- [ ] *Issues* criadas no GitHub para as correções da Sprint 2

---

### Sprint 2 — Entender os dados e corrigir os indicadores (30/09 a 06/10/2026)

**Objetivo:** duas frentes — (a) saber exatamente **quais números do INEP você vai usar** e de onde eles saem, antes de escrever qualquer importação; e (b) **corrigir os erros de contagem** que produzem número errado na tela atual.

> **Não pule a primeira frente para "começar logo a programar".** Importar dados que você não entendeu é a forma mais rápida de produzir um painel com números errados — e números errados em um artigo sobre gênero na computação são um problema sério.

**Como dividir a semana:** as tarefas 2.1 a 2.4 são de análise (planilha, leitura, documentação) e as tarefas 2.5 e 2.6 são de código. Faça **as de código na primeira metade da semana** — elas são mecânicas, você já conhece os erros da Sprint 1, e assim a sprint não termina com código pela metade. Reserve a segunda metade para a análise dos dados, que exige mais concentração.

> *Branch* sugerida: `fix/indicadores-transparencia` (abra um PR só para as correções, separado do trabalho do INEP — é mais fácil de revisar e de descrever no TCC).

#### Tarefa 2.1 — Explorar as sinopses

*Ajuda/direcionamento:* abra uma sinopse no Google Planilhas (ou com `pandas`) e responda, por escrito:

1. Quantas abas/tabelas tem o arquivo, e qual delas traz **cursos de graduação por UF e por sexo**?
2. Quais colunas existem: matrículas, ingressos (ou "ingressantes"), concluintes? Elas vêm separadas por sexo?
3. As linhas trazem **cada curso** ou **grupos de curso** (áreas)?
4. Há diferenciação por **modalidade** (presencial e a distância) e por **grau acadêmico** (bacharelado, licenciatura, tecnológico)? Se houver, decida com o orientador se o seu recorte inclui tudo ou só presencial — **e registre a decisão**.

Para ler com `pandas`:

```python
import pandas as pd

# Sinopses costumam ter linhas de cabecalho antes da tabela de verdade.
# Ajuste skiprows ate a saida fazer sentido.
df = pd.read_excel('docs/tcc-igor/dados/inep/arquivo.xlsx',
                   sheet_name=None, skiprows=0)
for nome, tabela in df.items():
    print(nome, tabela.shape)
```

#### Tarefa 2.2 — Definir o recorte "cursos de computação"

*Ajuda/direcionamento:* esta é **a decisão metodológica central do trabalho**. Você precisa de um critério **explícito e citável** — não pode ser "escolhi os cursos que me pareceram de computação".

1. O INEP classifica os cursos pela **CINE Brasil** (Classificação Internacional Normalizada da Educação, adaptada para o Brasil). A área geral que interessa é a de **Computação e Tecnologias da Informação e Comunicação (TIC)**, que se desdobra em áreas específicas e detalhadas;
2. **Confirme no próprio documento da classificação, publicado pelo INEP**, quais são os códigos e nomes exatos dos níveis (geral, específica e detalhada) — e **anote a referência completa**, porque ela vai para o TCC;
3. Escreva em `docs/tcc-igor/recorte_cursos.md`: quais códigos entram, quais não entram, e **os casos de fronteira** com a decisão tomada (por exemplo: Engenharia de Computação costuma ser classificada em Engenharias, e não em Computação — entra ou não entra? Qualquer decisão é aceitável **desde que declarada**);
4. **Atenção à quebra de série:** a CINE Brasil passou a ser usada a partir de determinado ano do Censo; antes disso, a classificação era outra. Isso significa que **uma série longa pode não ser diretamente comparável**. Você tem duas saídas, e precisa escolher uma com o orientador:
   - **(a)** restringir a série aos anos que usam a mesma classificação — mais seguro, e é o que eu recomendo;
   - **(b)** montar uma correspondência entre as classificações e **declarar a limitação** no TCC.

   Seja qual for a escolha, **registre no diário qual classificação cada ano usa.** Esse parágrafo, sozinho, já diferencia o seu trabalho de um TCC descuidado.

#### Tarefa 2.3 — Planilha piloto de um ano

*Ajuda/direcionamento:* antes de automatizar, faça **um ano na mão** para saber como é o resultado certo. Produza `docs/tcc-igor/dados/piloto_2024.csv` (ajuste o ano) no formato "longo", uma linha por combinação:

```
ano,uf,codigo_area,nome_area,matriculas_total,matriculas_fem,ingressantes_total,ingressantes_fem,concluintes_total,concluintes_fem
2024,RN,0613,Desenvolvimento e analise de software,1234,210,300,55,180,30
```

**Confira dois totais à mão:** a soma das UFs bate com o total Brasil da sinopse? A soma de feminino + masculino bate com o total? Se não bater, você entendeu a tabela errado — e é muito melhor descobrir agora do que depois de importar 10 anos.

#### Tarefa 2.4 — Protocolo de extração

*Ajuda/direcionamento:* escreva `docs/tcc-igor/protocolo_extracao.md`, com: fonte, anos cobertos, tabela usada em cada ano, recorte de cursos, tratamento de valores ausentes ou suprimidos pelo INEP, e as conferências de totais que você fará. Outra pessoa precisa conseguir repetir a extração lendo só esse arquivo.

#### Tarefa 2.5 — Criar o módulo único de consultas e mover a *view* para `apps/dashboard`

*Ajuda/direcionamento:* esta é a decisão de arquitetura mais importante da tela antiga — e a que evita que o **erro 2** (divergência entre páginas) volte a acontecer. Hoje cada página monta a própria consulta, e por isso os números não batem. Crie `apps/dashboard/indicadores.py` com **uma função por indicador**, e faça o painel, a *home* e a galeria usarem as mesmas funções:

```python
"""Consultas dos indicadores da plataforma. Fonte unica destes numeros."""
from django.db.models import OuterRef, Subquery

from apps.acoes.models import Acao
from apps.inspiracoes.models import AvaliacaoInspiracao, UsuarioPerfil


def acoes_publicas():
    """Acoes que o site exibe publicamente. Use SEMPRE esta funcao como base."""
    return Acao.objects.filter(is_validado=True, is_active=True, status=True)


def perfis_aprovados():
    """Perfis cuja ULTIMA avaliacao foi aprovada.

    Move para ca a funcao _qs_perfis_aprovados(), hoje em apps/core/views.py:32.
    """
    ultima = (
        AvaliacaoInspiracao.objects
        .filter(usuario_perfil=OuterRef('pk'))
        .order_by('-data_hora_aprovado')
        .values('is_aprovado')[:1]
    )
    return (
        UsuarioPerfil.objects
        .filter(is_ativo=True, is_avaliacao=True)
        .annotate(ultima_ap_valor=Subquery(ultima))
        .filter(ultima_ap_valor=True)
    )

# TODO: acoes_por_uf(), acoes_por_tipo(), acoes_por_mes(), perfis_por_uf(), ranking_*()
```

Em seguida, **mova a *view* `transparencia` e o *template* `dashboard.html` de `apps/core` para `apps/dashboard`** e ative a rota:

1. o app `apps.dashboard` **já está em `INSTALLED_APPS`** (`settings/base.py:40`) — falta só descomentar a linha `#path('dashboard/', include('apps.dashboard.urls'))` em `tiparaelas/urls.py`;
2. **mantenha a URL pública `/transparencia/` funcionando.** Ela já pode ter sido divulgada; se o caminho mudar, deixe um redirecionamento. Combine com o orientador;
3. aproveite e remova as importações não usadas e duplicadas do arquivo (há um `from multiprocessing import context` sobrando);
4. **Combine com a equipe antes de tocar em `tiparaelas/urls.py`** — a *branch* `feature/gerenciamento-tipos-evento` altera o mesmo arquivo.

#### Tarefa 2.6 — Corrigir os erros que produzem número errado

*Ajuda/direcionamento:* um erro por vez, **um commit por erro**, todos referenciando a *issue* correspondente:

- **Erro 1 — perfil reprovado na contagem.** Faça **todos** os indicadores de inspirações (cartão, mapa, *ranking* e série mensal) usarem `perfis_aprovados()`. **Não esqueça a *view* `index`**, que tem o mesmo problema em `total_inspiracoes`;
- **Erro 2 — divergência entre páginas.** Painel, `index` e `acoes_galeria` passam a usar `acoes_publicas()`. Depois, **confira na tela**: o número do painel tem de bater com o da galeria;
- **Erro 3 — e-mail na consulta do *ranking*.** Exiba `nome`, retire `usuario__email` da consulta e use um rótulo genérico ("Inspiradora") no lugar do nome derivado do e-mail. **Cite esse caso no TCC como aplicação do princípio de minimização de dados da LGPD** — é um exemplo concreto e curto;
- **Erro 6 — fuso horário no MySQL.** Trate valores nulos vindos do `TruncMonth` para que a página **nunca quebre**, mesmo sem as tabelas de fuso carregadas. Nunca formate uma data que pode ser `None`. Se o teste em produção (Sprint 1) tiver dado `NULL`, avise o orientador para acionar o responsável pelo servidor — a correção no código evita o erro 500, mas os meses continuarão agrupados errado até as tabelas serem carregadas.

**Escreva um teste para cada erro corrigido**, em `apps/dashboard/tests.py`:

```python
from django.test import TestCase

from apps.dashboard import indicadores


class IndicadoresPlataformaTest(TestCase):
    def test_perfil_reprovado_nao_entra_na_contagem(self):
        ...

    def test_acao_nao_validada_fica_fora_de_acoes_publicas(self):
        ...

    def test_painel_e_galeria_usam_a_mesma_consulta(self):
        ...

    def test_ranking_nao_expoe_email(self):
        ...
```

> **Por que os testes importam aqui:** sem eles, a próxima pessoa que mexer na *view* reintroduz o erro sem perceber. E, no TCC, eles são a evidência de que a correção é permanente, e não pontual. Meta desta sprint: **≥ 4 testes passando**.

*Definição de pronto da Sprint 2:*
- [ ] Estrutura das sinopses compreendida e documentada
- [ ] `recorte_cursos.md` com os códigos que entram, os que não entram e os casos de fronteira
- [ ] Quebra de classificação identificada e decisão tomada com o orientador
- [ ] Planilha piloto de um ano, com os dois totais conferindo
- [ ] `protocolo_extracao.md` escrito
- [ ] `apps/dashboard/indicadores.py` criado; painel, `index` e galeria usando as mesmas funções
- [ ] *View* e *template* movidos para `apps/dashboard`, rota ativa, `/transparencia/` ainda funcionando
- [ ] Erros 1, 2, 3 e 6 corrigidos, com print do antes e do depois
- [ ] ≥ 4 testes passando; PR das correções aberto **separado** do trabalho do INEP

---

### Sprint 3 — Modelagem dos dados (07/10 a 13/10/2026)

**Objetivo:** criar no banco a estrutura que vai receber os dados oficiais.

> **Convenção obrigatória:** nunca use `choices`. Categorias são modelos próprios, com CRUD (`CLAUDE.md:238`).
> *Branch* sugerida: `feat/painel-inep-modelagem`

#### Tarefa 3.1 — `Regiao` e complementos em `Estado`

*Ajuda/direcionamento:* `Estado` hoje tem só `sigla` e `nome` (`apps/usuarios/models.py:587`).

1. Crie `Regiao` (nome, sigla, status) e uma FK `regiao` em `Estado`;
2. Acrescente em `Estado`: `populacao_estimada` e `ano_estimativa`;
3. Faça **uma migração de dados** (`migrations.RunPython`) que crie as 5 regiões, associe as 27 UFs e preencha a população a partir do arquivo do IBGE. Migração de dados fica versionada e é reproduzível — preencher na mão, não.

```python
def popular_regioes_e_populacao(apps, schema_editor):
    Regiao = apps.get_model('usuarios', 'Regiao')
    Estado = apps.get_model('usuarios', 'Estado')
    # TODO: criar as 5 regioes do IBGE
    # TODO: associar cada uma das 27 UFs a sua regiao
    # TODO: preencher populacao_estimada e ano_estimativa (fonte: IBGE)
```

#### Tarefa 3.2 — `AreaCine`

*Ajuda/direcionamento:* modelo para as áreas da classificação, com hierarquia resolvida por auto-relacionamento (assim você não precisa de `choices` para o nível):

```python
class AreaCine(models.Model):
    codigo = models.CharField(max_length=10, unique=True, verbose_name='código')
    nome = models.CharField(max_length=200, verbose_name='nome')
    area_pai = models.ForeignKey(
        'self', on_delete=models.PROTECT, null=True, blank=True,
        related_name='subareas', verbose_name='área superior',
    )
    status = models.BooleanField(default=True, verbose_name='status')

    class Meta:
        verbose_name = 'área CINE'
        verbose_name_plural = 'áreas CINE'
        ordering = ['codigo']

    def __str__(self):
        return f'{self.codigo} — {self.nome}'
```

Popule por migração de dados, com os códigos confirmados na Sprint 2.

#### Tarefa 3.3 — `FonteDados`

*Ajuda/direcionamento:* este modelo é o que torna o trabalho **reproduzível e verificável** — e é o que você vai citar quando o revisor perguntar de onde vem cada número.

```python
class FonteDados(models.Model):
    nome = models.CharField(max_length=200, verbose_name='nome')           # ex.: Sinopse Estatistica da Educacao Superior
    orgao = models.CharField(max_length=100, verbose_name='órgão')         # ex.: INEP
    ano_referencia = models.PositiveSmallIntegerField(verbose_name='ano de referência')
    tabela_origem = models.CharField(max_length=200, blank=True, verbose_name='tabela de origem')
    url = models.URLField(verbose_name='URL')
    data_acesso = models.DateField(verbose_name='data de acesso')
    arquivo_origem = models.CharField(max_length=255, blank=True, verbose_name='arquivo de origem')
    observacao = models.TextField(blank=True, verbose_name='observação')
```

#### Tarefa 3.4 — `IndicadorEducacao`

*Ajuda/direcionamento:* o modelo central. Note que **o sexo não vira uma dimensão separada** — ele vira colunas. Isso simplifica muito o cálculo dos percentuais e evita criar um modelo `Sexo` desnecessário:

```python
class IndicadorEducacao(models.Model):
    ano = models.PositiveSmallIntegerField(verbose_name='ano')
    estado = models.ForeignKey(Estado, on_delete=models.PROTECT,
                               related_name='indicadores', verbose_name='UF')
    area = models.ForeignKey(AreaCine, on_delete=models.PROTECT,
                             related_name='indicadores', verbose_name='área')
    fonte = models.ForeignKey(FonteDados, on_delete=models.PROTECT,
                              related_name='indicadores', verbose_name='fonte')

    matriculas_total = models.PositiveIntegerField(default=0, verbose_name='matrículas (total)')
    matriculas_fem = models.PositiveIntegerField(default=0, verbose_name='matrículas (feminino)')
    ingressantes_total = models.PositiveIntegerField(default=0, verbose_name='ingressantes (total)')
    ingressantes_fem = models.PositiveIntegerField(default=0, verbose_name='ingressantes (feminino)')
    concluintes_total = models.PositiveIntegerField(default=0, verbose_name='concluintes (total)')
    concluintes_fem = models.PositiveIntegerField(default=0, verbose_name='concluintes (feminino)')

    class Meta:
        verbose_name = 'indicador educacional'
        verbose_name_plural = 'indicadores educacionais'
        unique_together = [('ano', 'estado', 'area')]
        ordering = ['-ano', 'estado__sigla']

    @property
    def percentual_fem_matriculas(self):
        """Percentual de mulheres nas matriculas. None quando nao ha matricula."""
        if not self.matriculas_total:
            return None
        return self.matriculas_fem / self.matriculas_total * 100

    # TODO: percentual_fem_ingressantes e percentual_fem_concluintes
```

**Por que `unique_together`:** garante que você não importe o mesmo ano duas vezes por engano. É a rede de segurança mais barata que existe aqui.

**Por que os percentuais retornam `None` e não zero** quando o denominador é zero: zero significa "nenhuma mulher entre as matrículas"; `None` significa "não há matrícula nenhuma nesta UF/área/ano". São coisas diferentes, e tratá-las igual produz mapas errados. Nos gráficos, `None` aparece como "não informado" — nunca como 0%.

*Definição de pronto da Sprint 3:*
- [ ] `Regiao` criada; 5 regiões e 27 UFs associadas por migração de dados
- [ ] População por UF preenchida, com ano e fonte registrados
- [ ] `AreaCine` criada e populada com os códigos do recorte
- [ ] `FonteDados` e `IndicadorEducacao` criados, com `unique_together` e propriedades de percentual
- [ ] Migrações aplicadas sem erro; modelos registrados no `admin.py`; PR aberto

---

### Sprint 4 — Comando de importação (14/10 a 20/10/2026)

**Objetivo:** carregar todos os anos no banco, de forma reproduzível e conferida.

#### Tarefa 4.1 — Escrever o comando

*Ajuda/direcionamento:* crie `apps/dashboard/management/commands/importar_censo.py`:

```python
from django.core.management.base import BaseCommand, CommandError


class Command(BaseCommand):
    help = 'Importa indicadores do Censo da Educacao Superior (INEP) a partir de um arquivo'

    def add_arguments(self, parser):
        parser.add_argument('--arquivo', required=True, help='Caminho do .xlsx ou .csv')
        parser.add_argument('--ano', type=int, required=True, help='Ano de referencia')
        parser.add_argument('--url', required=True, help='URL de origem, para a FonteDados')
        parser.add_argument('--data-acesso', required=True, help='AAAA-MM-DD')
        parser.add_argument('--dry-run', action='store_true',
                            help='Mostra o que seria importado, sem gravar nada')

    def handle(self, *args, **options):
        # 1. Ler o arquivo com pandas
        # 2. Filtrar apenas as areas do recorte (AreaCine)
        # 3. Normalizar nomes de UF para a sigla
        # 4. Validar: soma das UFs == total Brasil? fem <= total?
        # 5. Criar/obter a FonteDados
        # 6. update_or_create por (ano, estado, area)
        # 7. Imprimir o resumo: N linhas lidas, N importadas, N ignoradas e por que
        ...
```

**Regras que o comando precisa seguir:**

- **`--dry-run` é obrigatório e você deve usá-lo sempre primeiro.** Ele imprime o que faria, sem gravar;
- **Validar antes de gravar.** No mínimo: `matriculas_fem <= matriculas_total` em toda linha (se falhar, você leu a coluna errada); e a soma por UF conferindo com o total Brasil da sinopse, com tolerância declarada;
- **`update_or_create`**, e não `create` — assim reimportar o mesmo ano corrige em vez de duplicar;
- **Nunca deixe erro silencioso.** Linha ignorada precisa aparecer no resumo, com o motivo;
- **Valores suprimidos ou em branco** na sinopse: decida (e documente) se viram 0 ou se a linha é ignorada. São coisas diferentes.

#### Tarefa 4.2 — Importar todos os anos e conferir

*Ajuda/direcionamento:*

1. Rode com `--dry-run` para cada ano, confira o resumo, e só então rode de verdade;
2. Depois da carga, **confira no banco** (Workbench ou `shell`): total de registros; anos presentes; UFs presentes (devem ser 27 por ano, salvo ausência real); e o percentual feminino nacional de cada ano. **Esse percentual precisa fazer sentido** — se algum ano der 3% ou 70%, há erro de leitura;
3. Anote a sequência exata de comandos em `docs/tcc-igor/COMO_REPLICAR.md`.

#### Tarefa 4.3 — Primeiros testes

*Ajuda/direcionamento:* em `apps/dashboard/tests.py`:

```python
from django.test import TestCase


class ImportacaoTest(TestCase):
    def test_reimportar_mesmo_ano_nao_duplica(self):
        ...

    def test_linha_com_feminino_maior_que_total_e_rejeitada(self):
        ...


class PercentualTest(TestCase):
    def test_percentual_feminino_calculado_corretamente(self):
        ...

    def test_percentual_e_none_quando_nao_ha_matricula(self):
        ...
```

*Definição de pronto da Sprint 4:*
- [ ] `importar_censo` funcionando, com `--dry-run` e validações
- [ ] Todos os anos do recorte importados, sem duplicatas
- [ ] Conferências feitas e registradas (totais, UFs por ano, percentual nacional por ano)
- [ ] ≥ 4 testes passando
- [ ] `COMO_REPLICAR.md` iniciado; PR aberto

---

### Sprint 5 — Módulo de indicadores (21/10 a 27/10/2026)

**Objetivo:** todos os números do painel saindo de **um único lugar**, com testes.

#### Tarefa 5.1 — Criar `apps/dashboard/indicadores_inep.py`

*Ajuda/direcionamento:* uma função por indicador. A página só chama essas funções — nenhuma consulta solta no *template* ou na *view*.

```python
"""Indicadores do painel INEP. Fonte unica dos numeros deste painel."""
from django.db.models import Sum

from apps.dashboard.models import IndicadorEducacao


def serie_nacional(anos=None):
    """Percentual feminino por ano, em matriculas, ingressos e conclusoes (Brasil)."""
    qs = IndicadorEducacao.objects.all()
    if anos:
        qs = qs.filter(ano__in=anos)
    dados = (
        qs.values('ano')
        .annotate(
            mat_total=Sum('matriculas_total'), mat_fem=Sum('matriculas_fem'),
            ing_total=Sum('ingressantes_total'), ing_fem=Sum('ingressantes_fem'),
            con_total=Sum('concluintes_total'), con_fem=Sum('concluintes_fem'),
        )
        .order_by('ano')
    )
    # TODO: calcular os tres percentuais por ano, tratando denominador zero como None
    return list(dados)


def percentual_por_uf(ano):
    """Percentual feminino nas matriculas, por UF, em um ano."""
    ...


def ranking_ufs(ano, quantidade=10):
    ...


def percentual_por_area(ano):
    """Percentual feminino por area detalhada da computacao."""
    ...


def funil_ingresso_conclusao(anos=None):
    """Compara o percentual feminino entre ingressantes e entre concluintes."""
    ...


def matriculas_fem_por_100mil(ano):
    """Matriculas femininas por 100 mil habitantes, por UF (usa populacao do IBGE)."""
    ...
```

**Dica de desempenho:** faça a agregação **no banco** (`Sum`, `values`, `annotate`) e o cálculo de percentual **em Python**, depois. Trazer todos os registros para a memória e somar em laço funciona, mas fica lento e é o tipo de coisa que o orientador vai apontar.

#### Tarefa 5.2 — Testes dos indicadores

*Ajuda/direcionamento:* **meta acumulada: ≥ 10 testes.** Cubra:

- percentual calculado corretamente com números conhecidos (monte o cenário no `setUp`);
- denominador zero devolve `None`, não 0;
- `serie_nacional` soma as UFs corretamente;
- `ranking_ufs` ordena e limita como esperado;
- `percentual_por_area` não mistura níveis da hierarquia (área geral não é somada junto com as detalhadas — **este é o erro mais fácil de cometer aqui**, porque somaria tudo duas vezes);
- `matriculas_fem_por_100mil` usa a população certa e trata UF sem população cadastrada.

*Definição de pronto da Sprint 5:*
- [ ] `indicadores_inep.py` com as 6 funções implementadas
- [ ] Agregações feitas no banco
- [ ] ≥ 10 testes passando, incluindo o caso da hierarquia de áreas
- [ ] PR aberto

---

### Sprint 6 — Painel, menu e correções de apresentação (28/10 a 03/11/2026)

**Objetivo:** a primeira metade do painel no ar, o menu reorganizado e os erros de apresentação da tela antiga resolvidos — além dos primeiros resultados para o TCC.

> Esta é a sprint mais variada do ciclo: tem *back-end*, *template*, JavaScript e menu. Faça na ordem das tarefas — a página precisa existir antes de você apontar o menu para ela.

#### Tarefa 6.1 — Criar a página no app `dashboard`

*Ajuda/direcionamento:* o app já está ativo e a rota já foi descomentada na Sprint 2 — agora é só acrescentar a **segunda** página. Crie a *view* e o *template* da página de indicadores do INEP (sugestão de rota: `/transparencia/panorama-nacional/`, para que as duas páginas fiquem sob o mesmo caminho e a relação entre elas fique óbvia na URL).

Reaproveite o visual da tela de transparência (cartões, *grid*, CSS) para manter a identidade do site.

#### Tarefa 6.2 — Submenus no item "Transparência"

Agora existem **duas páginas de transparência com fontes de dados diferentes**, e o menu precisa deixar a diferença clara.

*Ajuda/direcionamento:* **você não vai precisar escrever CSS nem JavaScript.** O menu já tem um padrão de submenu pronto — o item "Sobre" — e ele é **100% CSS**, funcionando por `:hover` e `:focus-within` (`styles.css:249–309`), com versão para telas pequenas já resolvida (`styles.css:1290–1309`). Copie a estrutura.

Em `templates/publico/menu.html`, troque a linha atual:

```django
<li><a href="{% url 'transparencia' %}" class="nav-link">Transparência</a></li>
```

por um item com submenu, **exatamente no molde do "Sobre"**:

```django
<li class="nav-item nav-has-dropdown">
  <span class="nav-link nav-dropdown-trigger" tabindex="0" role="button" aria-haspopup="true" aria-expanded="false">
    Transparência
    <svg class="nav-chevron" viewBox="0 0 16 16" width="14" height="14" fill="none" aria-hidden="true"><path d="M4 6l4 4 4-4" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/></svg>
  </span>
  <ul class="nav-dropdown" role="menu">
    <li><a href="{% url 'transparencia' %}" class="nav-dropdown-item" role="menuitem">TiParaElas</a></li>
    <li><a href="{% url 'panorama_nacional' %}" class="nav-dropdown-item" role="menuitem">Panorama Nacional</a></li>
  </ul>
</li>
```

**Sobre o nome do segundo submenu.** "Dados Gerais" descreve mal o conteúdo: não diz **de quem** são os dados nem **sobre o quê**. Como as duas páginas vêm de fontes diferentes, o rótulo precisa tornar a diferença evidente para quem nunca entrou no site. Opções, da mais recomendada para a menos:

| Opção | Comentário |
|---|---|
| **TiParaElas** + **Panorama Nacional** | **Recomendada.** Curto, cabe no menu, e o contraste "nossa plataforma × país" é imediato |
| **Dados da Plataforma** + **Dados do Brasil** | Muito claro, e o paralelismo ajuda. Fica um pouco mais longo |
| **Nossos Dados** + **Mulheres na Computação no Brasil** | O segundo é o mais explícito de todos, mas é longo demais para um menu |
| **TiParaElas** + **Dados Gerais** | O rótulo original. "Gerais" é vago — evite |

Decida com o orientador e **mantenha o mesmo par de nomes no menu, no título das páginas e no TCC**.

**Três cuidados:**

- **acrescente um link cruzado entre as duas páginas** ("Veja também: os dados da plataforma TiParaElas" / "Veja também: o panorama nacional"). Quem chega por busca cai direto em uma delas e precisa descobrir que a outra existe;
- **deixe explícita a fonte no topo de cada página.** Uma diz "dados da plataforma TiParaElas, atualizados em ..."; a outra diz "dados do Censo da Educação Superior (INEP), ano de referência ...". Duas páginas vizinhas com fontes diferentes **precisam** dizer de onde vêm, ou o visitante mistura as duas coisas — e isso vale um parágrafo no seu TCC;
- o padrão existente mantém `aria-expanded="false"` fixo, porque não há JavaScript. **Siga o padrão** para ficar consistente com o "Sobre"; melhorar isso é assunto da bolsista de acessibilidade, não seu.

> **Conflito à vista:** a *branch* `feature/gerenciamento-tipos-evento` **também altera os menus**. Avise a equipe antes de mexer em `menu.html` e combine quem integra primeiro.

#### Tarefa 6.3 — Série histórica nacional **em linha** (QP1)

*Ajuda/direcionamento:* é a figura principal do trabalho. Três linhas no mesmo gráfico — percentual feminino em matrículas, ingressos e conclusões, ano a ano.

```javascript
new Chart(ctxSerie, {
  type: 'line',          // serie temporal e LINHA, nao barra
  data: {
    labels: anos,
    datasets: [
      { label: 'Matrículas', data: pctMatriculas },
      { label: 'Ingressantes', data: pctIngressantes },
      { label: 'Concluintes', data: pctConcluintes },
    ],
  },
  options: {
    scales: { y: { title: { display: true, text: '% de mulheres' } } },
  },
});
```

**Três cuidados:**

- **não force o eixo Y a começar em zero nem a terminar em 100** sem pensar: se os valores ficam entre 12% e 18%, um eixo de 0 a 100 achata a linha e esconde a variação. Escolha a escala e **justifique a escolha no TCC** — é uma decisão de visualização que merece um parágrafo;
- **passe os dados pelo `json_script` do Django**, e não por laços no *template*:
  ```django
  {{ serie_json|json_script:"dados-serie" }}
  ```
  ```javascript
  const serie = JSON.parse(document.getElementById('dados-serie').textContent);
  ```
- **fixe a versão do Chart.js.** Hoje vem do CDN sem versão (`dashboard.html:279`). Baixe o arquivo para `static/assets/js/` e sirva localmente, ou fixe a versão na URL. Anote a versão — ela vai para Materiais e Métodos.

#### Tarefa 6.4 — Ranking de UFs (QP2)

*Ajuda/direcionamento:* barras horizontais com as UFs ordenadas pelo percentual feminino no ano mais recente. Barras horizontais são a escolha certa quando os rótulos são nomes — e você pode justificar isso no TCC. **Destaque o RN** com cor diferente.

#### Tarefa 6.5 — Corrigir os erros de apresentação da tela de transparência

Agora que você domina o gráfico de linha e já está mexendo nesse arquivo, resolva os **erros 4, 5 e 7** da seção 3.1 — os que sobraram da Sprint 2.

*Ajuda/direcionamento:*

- **Erro 5 — séries mensais.** Duas correções no mesmo lugar (`dashboard.html:381` e `414`):
  1. **troque `type: 'bar'` por `type: 'line'`** — são dados temporais;
  2. **gere todos os meses do período**, preenchendo com zero os meses sem cadastro, use rótulo no formato `set./2026` e **corrija o texto** que diz "últimos 5 meses" enquanto a janela é de 6.

  ```python
  # TODO: montar a lista de meses do periodo
  # TODO: transformar o resultado do banco em dict {mes: total}
  # TODO: percorrer a lista de meses preenchendo com 0 os ausentes
  ```
  > Um mês com zero cadastros **é informação**. Hoje ele simplesmente desaparece, e o gráfico sugere continuidade onde não houve.

- **Erro 4 — dupla contagem por tipo.** Rotule as ações sem tipo como **"Sem tipo"** (e não "Outros", que parece um tipo real), **escreva no subtítulo do gráfico** que uma ação pode ter mais de um tipo — por isso a soma das barras pode exceder o total — e mostre também o percentual sobre o total de ações.

- **Erro 7 — textos que afirmam mais do que os dados.** Revise as frases da página ("em tempo real"; "Cada ponto e barra acima representa mulheres liderando projetos de TI" — as barras são contagens de **ações**). Acrescente **"Dados atualizados em ..."** e um bloco **"Como os números são calculados"**, com a definição de cada indicador em uma linha.

> O bloco "Como os números são calculados" é a versão pública do seu dicionário de dados, e você vai repeti-lo na página do INEP (Sprint 8). Escreva-o aqui de um jeito que dê para reaproveitar.

*Definição de pronto da Sprint 6:*
- [ ] Página do painel INEP no ar
- [ ] Menu "Transparência" com os dois submenus, nomes definidos com o orientador e link cruzado entre as páginas
- [ ] Fonte dos dados declarada no topo de **cada** uma das duas páginas
- [ ] Série histórica em **linha**, com 3 séries, escala justificada e dados via `json_script`
- [ ] Ranking de UFs com o RN destacado
- [ ] Chart.js com versão fixada e anotada
- [ ] Erros 4, 5 e 7 corrigidos, com print do antes e do depois
- [ ] Testes passando; PR aberto

---

### Sprint 7 — Painel: mapa e indicador proporcional (04/11 a 10/11/2026)

**Objetivo:** a segunda metade do painel — e o material que fecha a entrega dos Resultados em 11/11.

#### Tarefa 7.1 — Mapa coroplético por UF

*Ajuda/direcionamento:* reaproveite `templates/publico/mapa-brasil.html`, mas resolva os problemas dele:

- o mesmo SVG é incluído duas vezes na página de transparência, gerando **`id` duplicados**. Se você incluir o mapa mais de uma vez na sua página, **use `data-uf` no lugar de `id`** para identificar os estados;
- **registre a origem e a licença do SVG** — será exigida na legenda da figura no TCC. Se não houver registro, pergunte ao orientador de onde veio o arquivo.

#### Tarefa 7.2 — Legenda em classes numéricas

*Ajuda/direcionamento:* o mapa da tela atual usa escala linear pelo valor máximo e legenda sem números ("Menos"/"Mais"). **Isso não serve para uma figura de artigo.**

1. Defina classes com intervalos explícitos (ex.: `< 10%`, `10–15%`, `15–20%`, `20–25%`, `≥ 25%`);
2. Mostre os intervalos **com números** na legenda;
3. Use uma **paleta sequencial segura para daltonismo** e com contraste adequado;
4. **Escreva no TCC como as classes foram definidas** (intervalos iguais? quebras naturais? quantis?). Classes escolhidas de um jeito ou de outro mudam a aparência do mapa — e isso é uma decisão de visualização que merece justificativa.

#### Tarefa 7.3 — Indicador proporcional à população (QP2)

*Ajuda/direcionamento:* implemente a alternância entre dois mapas:

- **percentual de mulheres** entre as matrículas de computação na UF (indicador de equidade);
- **matrículas femininas por 100 mil habitantes** da UF (indicador de oferta, usando a população do IBGE).

**Comente a diferença entre os dois no TCC.** Uma UF pode ter percentual feminino alto e, ao mesmo tempo, pouquíssimas mulheres em computação em termos absolutos. Os dois mapas juntos contam uma história que nenhum deles conta sozinho — e essa comparação costuma ser o achado mais interessante deste tipo de trabalho.

#### Tarefa 7.4 — Recorte Nordeste / RN

*Ajuda/direcionamento:* uma seção da página com: a série histórica do Nordeste comparada à do Brasil; a posição do RN no ranking; e a evolução do RN ano a ano. Isso aproxima o trabalho do contexto do projeto e ajuda muito em eventos regionais.

#### Tarefa 7.5 — "Ver dados em tabela"

*Ajuda/direcionamento:* abaixo de cada gráfico e do mapa, um botão que exibe os mesmos dados em tabela. É o mínimo de acessibilidade — **e resolve um problema seu**: essa tabela é exatamente o que você vai colar no TCC.

> A acessibilidade completa (WCAG 2.2, navegação por teclado, leitores de tela) é a temática de outra bolsista do projeto. Faça só o "ver dados em tabela" e a paleta segura, e **combine o resto com ela** para não haver retrabalho nem conflito de *merge*.

*Definição de pronto da Sprint 7:*
- [ ] Mapa coroplético funcionando, com `data-uf`, fonte e licença registradas
- [ ] Legenda com classes numéricas e paleta acessível; critério das classes documentado
- [ ] Alternância entre percentual e valor por 100 mil habitantes
- [ ] Seção Nordeste/RN
- [ ] "Ver dados em tabela" em cada visualização
- [ ] Testes passando; PR aberto

---

### Sprint 8 — Subáreas, funil e exportação (11/11 a 17/11/2026)

**Objetivo:** responder à QP3 — a pergunta com maior potencial de achado — e deixar os dados exportáveis.

#### Tarefa 8.1 — Percentual feminino por subárea (QP3)

*Ajuda/direcionamento:* gráfico de barras comparando as áreas detalhadas da computação no ano mais recente, e uma pequena série mostrando se o padrão se mantém ao longo dos anos.

**Cuidado que vale um teste:** não some a área geral junto com as detalhadas — isso contaria tudo duas vezes. Use apenas um nível da hierarquia por gráfico.

#### Tarefa 8.2 — Funil ingresso → conclusão (QP3)

*Ajuda/direcionamento:* para cada ano, compare o **percentual feminino entre ingressantes** com o **percentual feminino entre concluintes**. Se o segundo for sistematicamente menor, isso é indício de que a proporção de mulheres diminui ao longo do curso.

**Seja rigoroso na interpretação.** Ingressantes e concluintes de um mesmo ano **não são a mesma coorte** — quem conclui em 2024 ingressou anos antes. Você tem duas saídas:

- comparar o percentual de concluintes do ano *t* com o de ingressantes do ano *t − 4* (defasagem aproximada da duração do curso), **declarando que é uma aproximação**; ou
- comparar apenas as tendências das duas séries ao longo do tempo, sem tratar como coorte.

Qualquer uma serve **desde que você diga qual usou e por quê**. Tratar como se fosse a mesma coorte, sem ressalva, é o erro que derruba o artigo.

#### Tarefa 8.3 — Exportação em CSV e dicionário de dados

*Ajuda/direcionamento:*

1. Botão de exportação em CSV dos **agregados** de cada visualização, com a data de geração e a fonte no próprio arquivo;
2. **Dicionário de dados** publicado (`docs/tcc-igor/dicionario_dados.md` e uma versão na própria página): para cada campo — nome, tipo, definição, o que entra e o que não entra, fonte e ano;
3. Bloco **"Como os números são calculados"** na página, com a definição de cada indicador em uma linha e o link para a fonte no INEP.

#### Tarefa 8.4 — Gerar as figuras do TCC

*Ajuda/direcionamento:* com `pandas` e `matplotlib`, gere as versões estáticas das figuras para o texto, em `docs/tcc-igor/figuras/`, com `dpi=200`, rótulos legíveis e **sem depender de print de tela** (print de gráfico interativo costuma sair com texto pequeno e borrado). Toda figura leva na fonte: *"Fonte: Elaborado pelo autor (2026), a partir de INEP (ano) e IBGE (ano)."*

*Definição de pronto da Sprint 8:*
- [ ] Comparação por subárea, sem misturar níveis da hierarquia
- [ ] Funil ingresso → conclusão, com a abordagem de coorte declarada
- [ ] Exportação CSV + dicionário de dados + bloco "Como os números são calculados"
- [ ] Figuras do TCC geradas em 200 dpi
- [ ] ≥ 12 testes passando; PR aberto

---

### Sprint 9 — Documentação, integração e fechamento (18/11 a 24/11/2026)

**Objetivo:** integrar, documentar e fechar o ciclo.

#### Tarefa 9.1 — Integração final

*Ajuda/direcionamento:*

- resolva a situação da *branch* `feature/dashboard-transparencia`, que tem um único commit e nunca foi integrada — combine com o orientador se ela entra antes ou junto do seu trabalho;
- resolva conflitos com `feature/gerenciamento-tipos-evento`;
- revise o seu próprio PR linha a linha antes de pedir revisão: sem `print()`, sem código comentado, sem importação não usada, sem arquivo de dados pesado versionado;
- `python manage.py test` passando.

#### Tarefa 9.2 — Documentação

*Ajuda/direcionamento:*

- **`COMO_REPLICAR.md`** — do zero até as figuras: migrar, importar cada ano (com os comandos exatos), rodar os testes, gerar as figuras. **Teste você mesmo, em uma base limpa;**
- **`CLAUDE.md` e README do projeto** — documente a nova rota, o módulo `indicadores_inep.py` e os modelos novos;
- **Dicionário de dados** finalizado;
- **Diagrama do modelo de dados** (draw.io), mostrando `IndicadorEducacao` no centro e `Estado`/`Regiao`, `AreaCine` e `FonteDados` como dimensões — essa figura vai para os Resultados do TCC.

#### Tarefa 9.3 — Base agregada publicável (opcional, combinar)

*Ajuda/direcionamento:* os dados são públicos e já agregados, então **não há impedimento de privacidade**. Combine com o orientador a publicação do CSV consolidado (a série tratada, por ano/UF/área) no **Zenodo** (gratuito, com DOI). Uma base citável valoriza o artigo — e neste caso o valor está no **tratamento**: alguém que queira a série pronta de computação por UF e sexo não precisa refazer a extração.

#### Tarefa 9.4 — Quadro antes/depois das correções

*Ajuda/direcionamento:* monte o quadro que vai para os Resultados do TCC, com uma linha por erro corrigido: **problema → efeito no número → correção aplicada → teste que o protege**. Use os prints e os valores que você anotou na Sprint 1 como "antes", e os atuais como "depois".

Confira também, uma última vez, que **os números batem entre as páginas**: painel, *home* e galeria devem mostrar o mesmo total de ações; o cartão de inspirações deve bater com o que a listagem pública exibe.

#### Tarefa 9.5 — Fechamento

*Ajuda/direcionamento:* apresentação de 10 minutos (10 a 12 *slides*): problema, dados usados, o que foi construído, os três achados principais, limitações e trabalhos futuros. Apresente no NIC e finalize a submissão do artigo com o orientador.

*Definição de pronto da Sprint 9:*
- [ ] PRs integrados, sem conflito pendente
- [ ] `COMO_REPLICAR.md` testado do zero
- [ ] `CLAUDE.md`, README, dicionário de dados e diagrama prontos
- [ ] Quadro antes/depois das correções montado, com evidência
- [ ] Números conferidos entre painel, *home* e galeria
- [ ] Decisão sobre a base no Zenodo registrada
- [ ] Apresentação feita e artigo submetido

---

## 8. Definição de pronto (vale para todas as sprints)

- [ ] `python manage.py test` passando
- [ ] Trabalho em *branch* própria, com Conventional Commits
- [ ] *Pull request* aberto, referenciando as *issues*
- [ ] Nenhuma senha, `.env`, `venv/` ou arquivo de dados pesado versionado
- [ ] Diário da semana com as decisões **e as justificativas**
- [ ] Evidências (prints, CSVs, figuras) salvas com nome que diz o que são
- [ ] Entregável enviado ao orientador **antes** da reunião

---

## 9. Riscos e planos B

| Risco | Sinal de alerta | Plano B |
|---|---|---|
| Formato das sinopses muda de um ano para outro | O código funciona para 2024 e quebra em 2019 | **Esperado.** Faça o comando aceitar um mapeamento de colunas por ano, ou normalize cada ano em CSV antes de importar. Reduza a série se necessário — **6 anos bem tratados valem mais que 12 mal tratados** |
| Quebra de classificação dos cursos (CINE) | Série com salto inexplicável em um ano | Restrinja a série aos anos com a mesma classificação e **declare a limitação** |
| Totais não conferem com a sinopse | Soma das UFs diferente do total Brasil | Pare e releia a tabela. Provavelmente há linha de subtotal sendo somada junto, ou o recorte de área está errado |
| Microdados baixados por engano | Arquivo de vários GB, máquina travando | Use **sinopses**. Se precisar de microdados, restrinja a 3 anos e trate com `pandas` em blocos (`chunksize`) |
| Percentual nacional com valor estranho (3% ou 70%) | Qualquer ano fora da faixa plausível | Erro de leitura de coluna. Confira contra o valor publicado na própria sinopse antes de seguir |
| **Sprint 2 sobrecarregada** (duas frentes na mesma semana) | Sexta-feira com as correções pela metade **e** a análise dos dados não iniciada | Faça as correções primeiro (são mecânicas). Se ainda assim estourar, **os erros 1, 2 e 3 são obrigatórios** e o erro 6 pode ir para a Sprint 6, junto com os de apresentação |
| Conflito de *merge* com outras *branches* | `feature/gerenciamento-tipos-evento` mexe em `urls.py`, `settings/base.py` **e nos menus** | Combine a ordem de integração com a equipe **antes** de tocar nesses arquivos. O `menu.html` é o ponto mais provável de conflito, na Sprint 6 |
| Mover a *view* quebra a URL `/transparencia/` | Link divulgado deixa de funcionar após a Sprint 2 | Mantenha a rota antiga com redirecionamento e teste no navegador antes de abrir o PR |
| Retrabalho com a bolsista de acessibilidade | Os dois mexendo em cor, foco e *tooltip* | Faça só "ver dados em tabela" e paleta segura; siga o padrão de submenu já existente sem alterá-lo; combine o resto na Sprint 7 |
| Sprint atrasada | Duas sprints seguidas sem fechar a definição de pronto | Replanejar com o orientador. **Ordem de corte:** primeiro o funil (Sprint 8), depois o recorte Nordeste/RN, depois o indicador proporcional. **Nunca corte os testes, a rastreabilidade das fontes nem as correções dos erros 1, 2 e 3** |

---

## 10. Trabalhos futuros (Ciclo 2)

Esta lista vai para a seção "Trabalhos futuros" da Conclusão:

1. **Cruzar os dados do INEP com o acervo da plataforma** — comparar onde estão as iniciativas cadastradas no TiParaElas com onde estão as matrículas femininas, para identificar UFs com muita demanda e pouca iniciativa. Depende de o acervo crescer.
2. **Incluir dados de evasão e de permanência**, se houver fonte pública com esse recorte.
3. **Recorte por raça/cor e por tipo de instituição** (pública × privada) — o Censo permite, e a interseccionalidade é uma lacuna reconhecida na literatura.
4. **Atualização automática anual**, com verificação de publicação de nova sinopse.
5. **Comparação internacional**, com dados da UNESCO ou da OCDE.
6. **Avaliação do painel com usuárias** (tarefas analíticas, SUS, TAM) — exige tratamento ético e não coube neste ciclo.
7. **Acessibilidade completa do painel** (WCAG 2.2, navegação por teclado, leitores de tela), em conjunto com a bolsista responsável pelo tema — incluindo o `aria-expanded` dinâmico dos submenus do menu principal, que hoje é fixo porque o *dropdown* é apenas CSS.
8. **Histórico de validação das ações** (modelo `AvaliacaoAcao`, no padrão de `AvaliacaoInspiracao`) — sem ele não há como medir tempo médio de validação nem taxa de aprovação, indicadores que a gestão do projeto pediria.
9. **Painéis restritos para a coordenadora e para a gestão**, com as próprias ações, fila de validação e lacunas — o painel deste ciclo é apenas o público.

---

## 11. Checklist de encerramento

- [ ] **Os 7 erros de contagem corrigidos**, com quadro antes/depois e um teste protegendo cada um
- [ ] **Números batendo entre painel, *home* e galeria**
- [ ] **Menu "Transparência" com os dois submenus**, nomes definidos, link cruzado e fonte declarada em cada página
- [ ] Sinopses do INEP importadas, com fonte, URL e data de acesso de cada registro
- [ ] Recorte de cursos definido a partir de classificação oficial e documentado
- [ ] `importar_censo` reproduzível, com `--dry-run` e validações
- [ ] Painel no ar com as 7 visualizações respondendo às 3 QPs
- [ ] Série histórica em linha; mapa com classes numéricas; indicador proporcional
- [ ] Exportação CSV, dicionário de dados e bloco "Como os números são calculados"
- [ ] ≥ 12 testes passando
- [ ] Figuras do TCC geradas em 200 dpi
- [ ] PRs integrados; `COMO_REPLICAR.md` testado do zero
- [ ] TCC entregue e artigo submetido (ver documento de escrita)
- [ ] Diários de bordo das 9 sprints preenchidos
- [ ] Apresentação de fechamento realizada no NIC
