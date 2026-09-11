# Orientações de Escrita e Prazos – Igor (Projeto TiParaElas)

Este documento reúne as orientações individuais do trabalho acadêmico do Igor. Ele complementa as [orientações gerais](../../README.md), que continuam valendo para a estrutura do trabalho, a formatação ABNT, as citações, as referências, as figuras e as tabelas.

> **Importante:** a análise do código foi feita em 11/09/2026, na *branch* `feature/dashboard-transparencia` (commit `db6588b`, de 10/07/2026). A tela iniciada fica em `apps/core/templates/dashboard.html`, e não em `transparencia.html`: esse é o nome da rota (`/transparencia/`), da *view* (`transparencia`) e do CSS (`static/assets/css/transparencia.css`). Sempre prevalecem os acordos feitos com o orientador.

## Sumário

- [1. Temática do trabalho](#1-temática-do-trabalho)
- [2. O que falta implementar](#2-o-que-falta-implementar)
- [3. Orientações de escrita](#3-orientações-de-escrita)
- [4. Prazos](#4-prazos)

---

## 1. Temática do trabalho

### 1.1 Tema e recorte

**Tema:** painel de dados e visualização do ecossistema de iniciativas de mulheres na computação.

**Especialização:** *back-end*, modelagem de dados e visualização (*dashboards*, bibliotecas de gráficos e *Business Intelligence* – BI).

**O que fazer:** um painel que transforma o acervo de **ações** e **perfis** da plataforma TiParaElas em uma visão analítica, com a distribuição por região, subárea da computação, tipo de iniciativa e evolução no tempo. O painel atende a dois públicos:

- **as coordenadoras que cadastram ações:** acompanham as próprias iniciativas e as situam no conjunto da plataforma;
- **a gestão do projeto:** acompanha o crescimento da plataforma, a fila de validação e as lacunas (regiões, subáreas e públicos sem iniciativas).

O trabalho **não** é um manual da tela de transparência. O centro do trabalho é a **modelagem dos dados para análise**, as **decisões de visualização** e a **evidência** de que o painel é útil ou de que os dados revelam algo sobre o ecossistema.

### 1.2 O caso estudado: a plataforma TiParaElas

O TiParaElas é uma plataforma Django para cadastro, validação e divulgação de ações voltadas às mulheres na computação e de perfis públicos de mulheres da área ("Seja Inspiração").

| Elemento | Onde está | O que interessa ao painel |
|---|---|---|
| Ações | `apps/acoes/models.py` (`Acao`, `TipoAcao`, `AcaoContagem`) | Título, tipos (M2M), cidade/UF, data de cadastro, validação e visitas |
| Perfis "Seja Inspiração" | `apps/inspiracoes/models.py` (`UsuarioPerfil`, `AvaliacaoInspiracao`) | Palavras-chave, ano de início na área, avaliação e visitas |
| Usuárias e localização | `apps/usuarios/models.py` (`Usuario`, `Estado`, `Cidade`, `Ocupacao`, `UsuarioContagem`) | Cidade/UF, ocupação, grupos e visitas aos perfis |
| Tela de transparência (sua) | `apps/core/views.py` (*view* `transparencia`), `apps/core/templates/dashboard.html`, `templates/publico/mapa-brasil.html` | Primeira versão do painel público |
| App `dashboard` | `apps/dashboard/` | Criado para o painel, mas **vazio** e com a rota comentada em `tiparaelas/urls.py` |

**O que a tela de transparência já mostra** (commit `db6588b`: 1.648 linhas adicionadas):

- três cartões: ações cadastradas, inspirações cadastradas e usuários cadastrados;
- ações: mapa coroplético por UF, gráfico de barras por tipo, cadastros por mês e as 3 ações mais acessadas;
- inspirações: mapa por UF, os 3 perfis mais acessados e cadastros por mês;
- gráficos com Chart.js e mapa em SVG colorido por JavaScript.

É um bom ponto de partida: a estrutura visual está pronta. O que falta está na seção 2, e é principalmente **dado para analisar** (subárea, região, período da iniciativa) e **correção dos indicadores**.

### 1.3 Dois caminhos para publicar

A mesma implementação serve aos dois caminhos, mas **o artigo deve seguir um deles**. Defina o caminho com o orientador **até 18/09/2026**, porque ele muda a Introdução, a Metodologia e os Resultados.

#### Caminho A – O painel como ferramenta avaliada

O painel é o artefato, e a contribuição é mostrar que ele apoia a decisão das coordenadoras e da gestão.

- **Pergunta principal:** um painel analítico construído sobre os dados da plataforma TiParaElas apoia a tomada de decisão das coordenadoras de ações e da gestão do projeto?
- **QP1:** quais informações e tarefas analíticas as coordenadoras e a gestão precisam realizar sobre o acervo?
- **QP2:** como os dados foram modelados e as visualizações foram projetadas para atender a essas tarefas?
- **QP3:** qual é a utilidade percebida, a facilidade de uso e o apoio à decisão do painel, segundo as participantes?
- **Evidências:** tarefas analíticas executadas pelas participantes (sucesso e tempo), questionário SUS, itens adaptados do TAM e entrevista curta.
- **Condição:** ter acesso a um grupo de coordenadoras disposto a participar e resolver a questão ética (item 29).

**Título provisório:** *Painel analítico para apoio à gestão de iniciativas de mulheres na computação: desenvolvimento e avaliação no projeto TiParaElas*.

#### Caminho B – O painel como lente para um artigo descritivo

O painel é o instrumento, e a contribuição é o **panorama** das iniciativas de mulheres na computação no Brasil a partir dos dados da plataforma.

- **Pergunta principal:** como se configuram as iniciativas de mulheres na computação cadastradas na plataforma TiParaElas?
- **QP1:** como as iniciativas se distribuem por região, UF, subárea, tipo e público-alvo?
- **QP2:** como as iniciativas evoluíram ao longo do tempo?
- **QP3:** quais lacunas aparecem (regiões, subáreas e públicos pouco atendidos) e como a distribuição se relaciona com indicadores externos, como população e matrículas de mulheres em cursos de computação?
- **Evidências:** base de dados congelada em uma **data de corte**, classificação das ações com livro de códigos, tabelas e gráficos do panorama.
- **Condição:** a base de produção precisa ter volume e diversidade suficientes.

**Título provisório:** *Panorama das iniciativas de mulheres na computação no Brasil: uma análise a partir dos dados da plataforma TiParaElas*.

#### Como escolher

- Consulte com o orientador os números **da base de produção** (ações validadas, UFs e regiões cobertas, perfis aprovados). O banco de desenvolvimento local tem só 2 ações, 1 perfil e 3 usuários, então não serve para essa decisão.
- Se houver poucas ações ou elas estiverem concentradas em poucos estados, o caminho B fica frágil. Nesse caso, prefira o A.
- Se não for possível reunir coordenadoras para a avaliação neste semestre, ou se a aprovação ética não couber no prazo, prefira o B.

O título definitivo é a última informação a ser definida.

### 1.4 Onde publicar

Confira sempre a chamada vigente: prazos, trilhas, limite de páginas, modelo e se a revisão é às cegas.

- **WIT – Women in Information Technology** (*workshop* do CSBC, da SBC): o veículo mais alinhado ao tema, para os dois caminhos;
- **IHC – Simpósio Brasileiro sobre Fatores Humanos em Sistemas Computacionais:** caminho A (avaliação com usuárias);
- **SBSI – Simpósio Brasileiro de Sistemas de Informação** e **iSys – Revista Brasileira de Sistemas de Informação:** caminho A (apoio à decisão) ou B;
- **WEI – Workshop sobre Educação em Computação** (CSBC): caminho B, se a maior parte das ações for educacional;
- **SIBGRAPI**, nas trilhas de trabalhos de graduação ou de visualização: caminho A, com foco no projeto das visualizações;
- **Cadernos de Gênero e Tecnologia** (UTFPR): caminho B.

Os artigos dos eventos da SBC estão na SBC OpenLib (SOL): https://sol.sbc.org.br. **Antes de começar a escrever, leia pelo menos três artigos do WIT** e, conforme o caminho, três do IHC (A) ou três panoramas/mapeamentos (B) para entender o formato esperado.

---

## 2. O que falta implementar

### 2.1 Visão geral

A tela de transparência já tem a parte visual, mas ainda não sustenta um artigo, por três motivos:

1. **alguns indicadores estão incorretos ou divergem de outras páginas** (itens 1 a 9). Um número errado em uma figura do artigo compromete todo o trabalho;
2. **os dados necessários à temática não existem no modelo**: não há subárea, não há região e a única data da ação é a data de **cadastro na plataforma**, e não a data da iniciativa (itens 10 a 18);
3. **o painel ainda é só uma página pública**: não tem filtros, não tem visão para a coordenadora nem para a gestão e não permite exportar os dados (itens 19 a 26).

Recomendação de organização: concentre as consultas em um único módulo (por exemplo, `apps/dashboard/indicadores.py`), com uma função por indicador. As *views* públicas, os painéis privados, a exportação e os testes passam a usar as mesmas funções, e o mesmo número aparece igual em todos os lugares.

- **Prioridade 1:** fazer imediatamente.
- **Prioridade 2:** necessário para existir "região", "subárea" e "evolução no tempo".
- **Prioridade 3:** necessário para ser um painel analítico para os dois públicos.
- **Prioridade 4:** necessário para publicar (testes, reprodutibilidade e avaliação).

Crie uma *issue* no GitHub para cada item e trabalhe com *branches* e *pull requests*.

### 2.2 Lista de pendências

#### Prioridade 1 – Confiabilidade dos indicadores existentes

| # | Situação encontrada | O que fazer |
|---|---|---|
| 1 | A *branch* `feature/dashboard-transparencia` tem um único commit (`db6588b`) e **não foi integrada** à `main` nem à `develop` | Abrir um *pull request* depois das correções desta prioridade e integrar com a revisão do orientador |
| 2 | Os indicadores de inspirações filtram só `is_ativo=True` e `is_avaliacao=True`, sem verificar se a **última avaliação foi aprovada**. A função `_qs_perfis_aprovados()`, que faz essa verificação, está no mesmo arquivo e não é usada. Um perfil **reprovado** entra na contagem e pode aparecer no *ranking* com um link que leva a um erro 404 (`inspiracao_detalhe` exige aprovação). O mesmo acontece com `total_inspiracoes` na *view* `index` | Usar `_qs_perfis_aprovados()` em todos os indicadores de inspirações (cartão, mapa, *ranking* e série mensal) e no `index` |
| 3 | As consultas de ações divergem entre as páginas: a transparência e o `index` filtram `is_validado`, `is_active` e `status`, mas a galeria (`acoes_galeria`) filtra só `is_validado` e `is_active`. O número do painel pode não bater com o que aparece na galeria | Criar uma única consulta de "ações públicas" e usá-la no painel, no `index` e na galeria. Definir no dicionário de dados o significado de `status` e de `is_active` (ver item 16) |
| 4 | *Ranking* de inspirações: o *template* exibe `nome_completo`, mas a *view* monta um nome alternativo em `nome`, que nunca é usado. Esse nome alternativo é derivado do **e-mail** da usuária, e a consulta carrega `usuario__email` sem necessidade | Exibir `nome`, retirar o e-mail da consulta e do nome alternativo (usar, por exemplo, "Inspiradora"). Isso atende ao princípio da minimização de dados da LGPD |
| 5 | Ações por tipo: como `tipos` é M2M, **uma ação com dois tipos é contada duas vezes** e a soma das barras fica maior que o total de ações. Ações sem tipo aparecem como "Outros", que pode ser confundido com um tipo real | Rotular como "Sem tipo", informar no gráfico que uma ação pode ter mais de um tipo e mostrar também o percentual de ações em cada tipo |
| 6 | Séries mensais: a janela cobre **6 meses** (mês atual e os 5 anteriores), mas o texto diz "últimos 5 meses". **Meses sem cadastro somem do gráfico**, e o rótulo mostra só o nome do mês, sem o ano | Gerar todos os meses do período, preenchendo com zero, usar rótulos como "set./2026" e corrigir o texto (depois, o período vira filtro, item 19) |
| 7 | `TruncMonth` com `USE_TZ = True` no **MySQL** depende das tabelas de fuso horário do servidor. Sem elas, o banco devolve `NULL` e `date_format(None, "F")` gera **erro 500** na página. Em desenvolvimento (SQLite) o problema não aparece | Verificar em produção (`SELECT CONVERT_TZ('2026-01-01 12:00:00', 'UTC', 'America/Sao_Paulo');`). Se vier `NULL`, carregar as tabelas (`mysql_tzinfo_to_sql`) com o responsável pelo servidor e tratar valores nulos no código |
| 8 | "Usuários cadastrados" conta **todas** as contas: superusuários, contas de teste e cadastros sem e-mail confirmado. Na área privada, `perfil_view` também usa `Acao.objects.count()`, que inclui ações não validadas | Definir com o orientador o que cada cartão mede e documentar a definição na própria página |
| 9 | Textos da página afirmam mais do que os dados mostram: "em tempo real" e "Cada ponto e barra acima representa mulheres liderando projetos de TI" (as barras são contagens de ações, e não de mulheres). O botão "Cadastrar-me como Inspiração" leva ao cadastro geral. A *view* está em `apps/core`, embora exista o app `apps/dashboard`, e há importações sem uso (`from multiprocessing import context`) e duplicadas | Revisar os textos, incluir "Dados atualizados em ..." e um bloco "Como os números são calculados". Mover a *view* e as consultas para `apps/dashboard`, ativar a rota e limpar as importações |

#### Prioridade 2 – Modelo de dados para análise

Siga a convenção do projeto (`CLAUDE.md` do TiParaElas): **nunca use `choices`**. Categorias e tipos são modelos próprios, com CRUD. Não crie todos os campos abaixo sem conversar com o orientador. Cada campo novo precisa responder a uma pergunta do artigo.

| # | Situação encontrada | O que fazer |
|---|---|---|
| 10 | **Não existe subárea da computação** em `Acao` nem em `UsuarioPerfil`. Sem isso, a temática ("distribuição por subárea") não pode ser atendida | Criar o modelo `Subarea` (nome, descrição e status), com M2M em `Acao` e em `UsuarioPerfil`, CRUD e campo obrigatório no formulário. Definir a lista com o orientador, a partir de uma taxonomia de referência citável (por exemplo, a *ACM Computing Classification System* ou as comissões especiais da SBC) |
| 11 | **Não existe região**: `Estado` tem apenas `sigla` e `nome` | Criar o modelo `Regiao` e uma FK em `Estado`, populada por migração de dados com as 5 regiões do IBGE. Para permitir indicadores proporcionais, guardar a população estimada por UF, com o ano da estimativa |
| 12 | **Não existe a data da iniciativa.** `Acao` tem `data_cadastro` e `criado_em`, os dois com `auto_now_add` (duplicados), e ambos registram a data de **cadastro na plataforma**. Uma ação que existe desde 2015 e foi cadastrada em 2026 aparece como de 2026. A "evolução no tempo" hoje mede a adoção da plataforma, e não o ecossistema | Criar `ano_inicio` (obrigatório) e `ano_fim` (opcional, vazio = em andamento) em `Acao`. No painel, separar as duas séries: "iniciativas por ano de início" e "cadastros na plataforma por mês" |
| 13 | Faltam outras dimensões comuns em panoramas: para quem é a ação, como ocorre e qual o alcance | Avaliar com o orientador: `PublicoAlvo` (M2M: ensino fundamental, ensino médio, graduação, profissionais etc.), `Modalidade` (FK: presencial, remota, híbrida), instituição vinculada com `TipoInstituicao` e número estimado de participantes (opcional). Para o caminho B, esses campos são as variáveis do artigo |
| 14 | Os tipos de ação não têm definição. No banco local existem "Comunidade", "Grupo" e "Projeto", que podem se sobrepor | Conferir a lista de produção, escrever a definição de cada tipo em `TipoAcao.descricao` e usá-la no livro de códigos (item 29) |
| 15 | As ações já cadastradas não têm os campos novos | Fazer a curadoria das ações existentes (preencher subárea, ano de início etc.), registrando quem classificou e quando. No painel, mostrar "não informado" enquanto houver lacunas |
| 16 | Dados dos perfis difíceis de agregar: palavras-chave em texto livre (até 20 caracteres, sem padronização), `Usuario.cidade` opcional (logins via SUAP podem ficar sem cidade). Em `Acao`, três booleanos (`is_validado`, `is_active` e `status`) têm significados sobrepostos | Normalizar as palavras-chave (minúsculas, sem espaços extras e com sinônimos unificados) ou associá-las a `Subarea`. Medir e exibir o percentual de perfis sem UF. Criar um **dicionário de dados** com a definição de cada campo usado nos indicadores |
| 17 | **Não há histórico de validação das ações.** As *views* de cadastro e de edição (`apps/acoes/views.py`) voltam `is_validado` para `False` a cada salvamento, e `data_hora_validacao` guarda só a última validação. Não é possível calcular tempo médio de validação nem taxa de reprovação | Criar `AvaliacaoAcao` (aprovado, observação, data/hora e avaliador), no mesmo padrão de `AvaliacaoInspiracao`, e registrar uma linha a cada validação ou reprovação |
| 18 | Visitas: `AcaoContagem` nunca é apagada, mas `UsuarioContagem` é removida após 365 dias pelo `expurgar_dados` (quando `EXPURGO_ATIVO` está ligado). A série de visitas aos perfis some com o tempo, e as duas contagens seguem regras diferentes. Além disso, a contagem é por sessão (30 minutos) e inclui robôs | Criar uma tabela de visitas **agregadas por mês**, sem sessão nem dado pessoal, preenchida antes do expurgo. Alinhar a retenção de `AcaoContagem` à política de privacidade. No texto, chamar de "visualizações registradas", e não de "pessoas" |

#### Prioridade 3 – Painel analítico

| # | Situação encontrada | O que fazer |
|---|---|---|
| 19 | Não há filtros: todos os números são fixos | Filtros por período, região/UF, tipo, subárea e público-alvo, passados por parâmetros na URL (o *link* filtrado pode ser compartilhado). Todos os gráficos da página respondem aos filtros |
| 20 | **Não existe painel da coordenadora.** A página inicial da área privada (`/usuarios/`) mostra apenas o total geral de ações e de usuários | Criar o painel da coordenadora, com as **próprias** ações: situação da validação, visualizações por mês e posição em relação à média da plataforma e da subárea |
| 21 | **Não existe painel de gestão** | Criar o painel de gestão, protegido por uma permissão própria (por exemplo, `dashboard.ver_painel_gestao`), com: fila de validação de ações e de perfis (com o tempo de espera), tempo médio até a validação, taxa de aprovação, crescimento de usuárias por grupo, **lacunas** (UFs, regiões e subáreas sem ações) e qualidade dos dados (percentual de ações sem cidade, tipo ou subárea) |
| 22 | O mapa usa uma escala linear pelo valor máximo, e a legenda não tem números ("Menos ações"/"Mais ações"). Contagens absolutas por UF tendem a reproduzir o mapa da população | Legenda com classes numéricas, opção de valor proporcional (por exemplo, ações por milhão de habitantes), gráfico por região, gráfico por subárea e cruzamento subárea × região. Cada visualização deve responder a uma pergunta escrita no subtítulo |
| 23 | Acessibilidade: o mapa usa **só cor**, o *tooltip* funciona **só com mouse** e o mesmo SVG é incluído duas vezes, o que gera **`id` duplicados** na página (`MG`, `SP`, `Layer_1` etc.). A origem e a licença do SVG do mapa não estão registradas | Oferecer "ver dados em tabela" para cada gráfico e mapa, foco por teclado e `<title>` por UF, paleta segura para daltonismo e contraste conforme a WCAG 2.2. Usar `data-uf` no lugar de `id`. Registrar a fonte e a licença do mapa, que também será exigida na figura do trabalho |
| 24 | O Chart.js é carregado do CDN **sem versão** (`https://cdn.jsdelivr.net/npm/chart.js`): uma nova versão pode quebrar os gráficos, e não é possível informar a versão usada no trabalho. Os dados chegam ao JavaScript por laços no *template* | Fixar a versão (ou servir o arquivo em `static/`) e passar os dados com o filtro `json_script` do Django |
| 25 | Não há exportação dos dados | Exportar em CSV os indicadores **agregados**, com os filtros aplicados e a data de geração, acompanhados do dicionário de dados. Ao cruzar duas ou mais dimensões com dados de perfis, suprimir células com poucos casos (por exemplo, menos de 3) para evitar a identificação de pessoas |
| 26 | A página faz cerca de 10 consultas por acesso e não usa *cache* | Usar *cache* por alguns minutos, com chave pelos filtros, e exibir a data da última atualização |

#### Prioridade 4 – Qualidade, reprodutibilidade e avaliação

| # | Situação encontrada | O que fazer |
|---|---|---|
| 27 | Não há testes para a transparência (`apps/core/tests.py` não testa a *view*, e `apps/dashboard/tests.py` está vazio) | Escrever testes para cada função de indicador, cobrindo: perfil reprovado, ação com dois tipos, ação sem tipo, mês sem cadastros, ação não validada ou inativa, filtros e permissões dos painéis privados. Os casos dos itens 2 a 7 devem virar testes |
| 28 | Os números do artigo precisam ser reproduzíveis, e o banco local não representa a produção | Solicitar ao orientador acesso aos dados de produção. Criar um comando (por exemplo, `python manage.py exportar_panorama --data-corte 2026-10-16`) que gere CSVs agregados e anonimizados e um arquivo com a data de corte, o *hash* do commit e as definições dos indicadores. **Todo número do artigo sai desse *snapshot***. Não versione arquivos com dados pessoais |
| 29 | Não há instrumentos de pesquisa | **Caminho A:** roteiro de tarefas analíticas (por exemplo, "quantas ações de robótica há no Nordeste?"), questionário SUS, itens adaptados do TAM (utilidade e facilidade de uso percebidas), roteiro de entrevista e TCLE. Verifique com o orientador se a avaliação precisa passar pelo Comitê de Ética em Pesquisa (CEP) ou se se enquadra nas exceções da Resolução CNS nº 510/2016. Se precisar do CEP, submeta **imediatamente**, pois a aprovação pode não caber no prazo. **Caminho B:** livro de códigos com a definição de cada subárea, tipo e público-alvo. Duas pessoas classificam uma amostra das ações de forma independente, e a concordância é medida pelo coeficiente kappa de Cohen |
| 30 | Processo e documentação: seus commits aparecem com dois nomes (`adrian5g` e `Igor Ádrian`). O `CLAUDE.md` do projeto não documenta a rota `/transparencia/`. A *branch* `feature/gerenciamento-tipos-evento` (18/07/2026) também altera `tiparaelas/urls.py`, `tiparaelas/settings/base.py` e os menus | Configurar `user.name` e `user.email` e criar um `.mailmap`. Manter o padrão Conventional Commits, que você já usou (`feat:`). Documentar as rotas e os indicadores no `CLAUDE.md` e no README. Combinar com a equipe a ordem de integração das *branches* para evitar conflitos |

### 2.3 Indicadores sugeridos

| Indicador | Pergunta que responde | Público | Fonte |
|---|---|---|---|
| Ações por região e por UF (absoluto e por milhão de habitantes) | Onde estão as iniciativas? | Público, gestão | `Acao.cidade` → `Estado` → `Regiao` (itens 3 e 11) |
| Ações por subárea | Quais áreas da computação são mais e menos atendidas? | Público, gestão | `Acao.subareas` (item 10) |
| Ações por tipo e por público-alvo | Que formato têm as iniciativas e para quem são? | Público, gestão | `Acao.tipos`, `Acao.publicos_alvo` (itens 5 e 13) |
| Iniciativas por ano de início | Como o ecossistema evoluiu? | Público | `Acao.ano_inicio` (item 12) |
| Cadastros na plataforma por mês | Como a plataforma está sendo adotada? | Gestão | `Acao.criado_em`, `UsuarioPerfil.criado_em` (item 6) |
| Subárea × região | Onde estão as lacunas? | Público, gestão | Itens 10 e 11 |
| Perfis por UF, subárea e tempo na área | Quem são as mulheres visíveis na plataforma? | Público | `UsuarioPerfil`, `ano_inicio_area` (itens 2 e 16) |
| Fila e tempo de validação, taxa de aprovação | O fluxo de curadoria está funcionando? | Gestão | `AvaliacaoAcao`, `AvaliacaoInspiracao` (item 17) |
| Qualidade dos dados | Os números são confiáveis? | Gestão | Percentual de campos não informados (itens 15 e 16) |
| Visualizações das minhas ações por mês | Minha ação está alcançando o público? | Coordenadora | Visitas agregadas (item 18) |

---

## 3. Orientações de escrita

Escreva o TCC no modelo ABNT, seguindo as [orientações gerais](../../README.md), mas pense no **artigo** desde o início. Todo número precisa ter origem clara (*snapshot*, data de corte e definição do indicador), e toda afirmação sobre utilidade precisa de evidência coletada com as participantes. Frases como "o painel facilita a tomada de decisão", sem dados, são cortadas pelos revisores.

Onde as orientações mudam conforme o caminho, elas estão marcadas com **(A)** ou **(B)**.

### 3.1 Introdução

- **Contextualização:**
  - pesquise dados sobre a participação das mulheres na computação no Brasil (por exemplo, os microdados do Censo da Educação Superior, do INEP, para matrículas e concluintes em cursos de computação por sexo) e fale sobre a sub-representação feminina na área;
  - fale sobre as iniciativas que buscam mudar esse cenário, como o Programa Meninas Digitais, da SBC, e projetos de extensão, grupos e comunidades;
  - fale sobre a importância de dados e de transparência para dar visibilidade a essas iniciativas e orientar ações.
- **Problemática:**
  - fale sobre a dispersão das iniciativas: estão espalhadas em redes sociais, *sites* institucionais e editais, sem uma visão consolidada de onde estão, em quais subáreas atuam e para quem;
  - fale sobre o problema do ponto de vista de quem decide: sem indicadores, as coordenadoras não sabem como suas ações se situam e a gestão não sabe onde estão as lacunas;
  - pesquise se já existem mapeamentos ou panoramas nacionais dessas iniciativas e mostre o que falta neles (atualização, abrangência, dados abertos, recorte por subárea).
- **Caminho para a solução:**
  - pesquise sobre visualização de dados, painéis (*dashboards*) e BI como apoio à decisão, e sobre plataformas de transparência e dados abertos;
  - cite trabalhos que mapearam iniciativas de mulheres na computação e trabalhos que desenvolveram painéis para projetos sociais, educacionais ou de extensão, sempre com a referência.
- **Apresentação da solução:**
  - fale sobre a plataforma TiParaElas (cadastro e validação de ações e perfis) e sobre o painel analítico construído sobre esses dados, com os dois públicos (coordenadoras e gestão);
  - **(A)** diga que o painel foi avaliado com coordenadoras e com a gestão, e como (tarefas, questionários e entrevista);
  - **(B)** diga que o painel foi usado para produzir um panorama das iniciativas cadastradas até a data de corte;
  - não mencione avaliações ou análises que não aconteceram.
- **Vínculo com projetos:** fale sobre o histórico do TiParaElas (o repositório começa em junho de 2025), o NIC e a equipe (confirme com o orientador o nome oficial do projeto, o edital e a instituição). O repositório tem vários autores, então **deixe explícito que a sua contribuição é o painel analítico** (modelagem para análise, indicadores e visualizações) e que o cadastro de ações, os perfis e a validação foram desenvolvidos pela equipe.
- **Pergunta de pesquisa e contribuições:** feche a Introdução com a pergunta e as QPs do caminho escolhido (seção 1.3) e com uma lista curta de contribuições. Por exemplo: **(A)** o modelo de dados analítico, o painel com dois perfis de uso e os resultados da avaliação; **(B)** o panorama, a base de dados agregada e o livro de códigos para classificar iniciativas.

### 3.2 Objetivo geral

- Escreva uma frase, com um único verbo principal, coerente com a pergunta de pesquisa;
- o objeto do objetivo é o **painel** (A) ou o **panorama** (B), e não "desenvolver uma tela de transparência";
- estruturas para você completar:

> **(A)** "O objetivo principal do presente trabalho consiste no desenvolvimento e na avaliação de um painel analítico [...] da plataforma TiParaElas, para apoiar [...] das coordenadoras de ações e da gestão do projeto."
>
> **(B)** "O objetivo principal do presente trabalho consiste em analisar a distribuição [...] das iniciativas de mulheres na computação cadastradas na plataforma TiParaElas, por meio de um painel analítico [...]."

### 3.3 Referencial Teórico

Explique somente os conceitos que aparecem depois nos Resultados. Detalhes de Django e Chart.js vão para Materiais e Métodos, com referência à documentação oficial. Estrutura sugerida:

```
2 REFERENCIAL TEÓRICO
2.1 Mulheres na computação
2.2 Visualização de dados
2.3 Painéis (dashboards) e apoio à decisão
2.4 Modelagem de dados para análise
2.5 Transparência, dados abertos e proteção de dados
2.6 Avaliação de ferramentas de visualização (A) ou Classificação e análise descritiva de dados (B)
2.7 Trabalhos relacionados
```

- **2.1 Mulheres na computação:** pesquise sobre a história da participação feminina na área, os dados atuais de matrículas e concluintes e as barreiras apontadas pela literatura. Fale sobre as iniciativas de incentivo, com destaque para o Programa Meninas Digitais e para os trabalhos publicados no WIT.
- **2.2 Visualização de dados:** pesquise sobre os tipos de dados e as tarefas de visualização, os canais visuais (posição, tamanho, cor) e sua eficácia, a escolha do gráfico conforme a pergunta, os mapas coropléticos e seus cuidados (normalização pela população e classes de cor), e a acessibilidade de gráficos.
- **2.3 Painéis e apoio à decisão:** pesquise sobre a definição de *dashboard*, os tipos de painel (estratégico, analítico e operacional), boas práticas de projeto, BI e o mantra de Shneiderman ("visão geral primeiro, *zoom* e filtro, detalhes sob demanda").
- **2.4 Modelagem de dados para análise:** pesquise sobre a diferença entre o modelo transacional (OLTP) e o analítico (OLAP), fatos e dimensões (modelagem dimensional), agregações e qualidade de dados (completude, consistência, atualidade). Relacione com o que foi feito: `Acao` como fato e região, subárea, tipo e tempo como dimensões.
- **2.5 Transparência, dados abertos e proteção de dados:** pesquise sobre transparência ativa, dados abertos e a LGPD, principalmente a minimização de dados, a anonimização e o risco de reidentificação em dados agregados.
- **2.6 (A) Avaliação de ferramentas de visualização:** pesquise sobre os cenários de avaliação em visualização, o modelo aninhado de Munzner, a *Design Science Research*, o SUS e o TAM.
- **2.6 (B) Classificação e análise descritiva:** pesquise sobre análise de conteúdo e livro de códigos, a concordância entre avaliadores (kappa de Cohen) e a estatística descritiva (frequências, proporções e taxas).
- **2.7 Trabalhos relacionados:** busque mapeamentos de iniciativas de mulheres na computação e painéis ou observatórios de dados de projetos sociais e educacionais. Termos de busca (use em português e em inglês):
  - `"women in computing" AND ("initiatives" OR "mapping")`;
  - `"mulheres na computação" AND ("iniciativas" OR "mapeamento")`;
  - `"Meninas Digitais"`;
  - `"dashboard" AND "decision support" AND "evaluation"`;
  - `"painel" AND "visualização de dados" AND "extensão"`;
  - `"gender" AND "computing" AND "Brazil"`.

  Termine a seção com um quadro comparativo usando critérios como: abrangência geográfica, período dos dados, dimensões analisadas (região, subárea, tipo, público), atualização contínua, disponibilidade dos dados e, no caminho A, se houve avaliação com usuárias.

**Leituras de partida.** Localize a fonte original, confira os dados e só depois inclua nas Referências:

- FEW, S. *Information Dashboard Design: Displaying Data for At-a-Glance Monitoring*;
- MUNZNER, T. *Visualization Analysis and Design* (CRC Press, 2014);
- MUNZNER, T. *A Nested Model for Visualization Design and Validation* (IEEE TVCG, 2009);
- SHNEIDERMAN, B. *The Eyes Have It: A Task by Data Type Taxonomy for Information Visualizations* (1996);
- SARIKAYA, A. *et al.* *What Do We Talk About When We Talk About Dashboards?* (IEEE TVCG, 2019);
- TUFTE, E. R. *The Visual Display of Quantitative Information*;
- KIMBALL, R.; ROSS, M. *The Data Warehouse Toolkit*;
- LAM, H. *et al.* *Empirical Studies in Information Visualization: Seven Scenarios* (IEEE TVCG, 2012);
- **(A)** HEVNER, A. R. *et al.* *Design Science in Information Systems Research* (MIS Quarterly, 2004); DAVIS, F. D. *Perceived Usefulness, Perceived Ease of Use, and User Acceptance of Information Technology* (MIS Quarterly, 1989); BROOKE, J. *SUS: A "Quick and Dirty" Usability Scale* (1996);
- **(B)** LANDIS, J. R.; KOCH, G. G. *The Measurement of Observer Agreement for Categorical Data* (Biometrics, 1977); obras de análise de conteúdo indicadas pelo orientador;
- LIMA, M. P. *As mulheres na Ciência da Computação* (Revista Estudos Feministas, 2013);
- UNESCO. *Decifrar o código: educação de meninas e mulheres em ciências, tecnologia, engenharia e matemática (STEM)*;
- publicações do Programa Meninas Digitais e dos anais do WIT (SOL);
- INEP. Microdados do Censo da Educação Superior; IBGE. Estimativas da população e divisão regional;
- Lei nº 13.709/2018 (LGPD) e Lei nº 12.527/2011 (Lei de Acesso à Informação);
- W3C. *Web Content Accessibility Guidelines (WCAG) 2.2*; ISO/IEC 25012 (qualidade de dados);
- documentação oficial do Django (agregações) e do Chart.js.

### 3.4 Metodologia

- **Classificação da pesquisa:**
  - **(A)** natureza aplicada; objetivos exploratórios e descritivos; abordagem quali-quantitativa (pontuações do SUS e do TAM e análise das entrevistas); procedimentos: pesquisa bibliográfica, desenvolvimento do artefato (*Design Science Research*) e estudo de avaliação com usuárias;
  - **(B)** natureza aplicada; objetivos exploratórios e descritivos; abordagem quantitativa, com análise qualitativa na classificação das ações; procedimentos: pesquisa bibliográfica e **pesquisa documental** sobre a base da plataforma, congelada na data de corte.
- **Pesquisa bibliográfica:** informe as bases consultadas, os termos de busca (seção 3.3), o período das publicações e os critérios de inclusão e exclusão.
- **Etapas:** descreva em ordem cronológica, com uma figura do fluxo:
  1. revisão da literatura;
  2. diagnóstico da tela de transparência e dos dados disponíveis (seção 2);
  3. levantamento das perguntas e tarefas analíticas das coordenadoras e da gestão;
  4. modelagem dos dados para análise (subárea, região, período, público-alvo e histórico de validação) e curadoria das ações existentes;
  5. correção dos indicadores e desenvolvimento dos painéis público, da coordenadora e da gestão;
  6. testes automatizados dos indicadores;
  7. **(A)** avaliação com as participantes; **(B)** congelamento da base na data de corte, classificação com livro de códigos e análise descritiva;
  8. análise e discussão dos resultados.
- **(A) Participantes e procedimento:** quem participou (perfil, sem identificar), quantas pessoas, como foram convidadas, onde e quando a avaliação ocorreu, quais tarefas foram executadas, quais instrumentos foram aplicados, como os dados foram analisados e como foram tratados os aspectos éticos (TCLE e CEP ou enquadramento na Resolução CNS nº 510/2016).
- **(B) Base de dados:** data de corte, critérios de inclusão (por exemplo, apenas ações validadas e ativas), número de registros, tratamento de campos não informados, definição de cada variável (dicionário de dados), como a classificação foi feita e o valor do kappa.
- **Ameaças à validade:** o artigo precisa de uma subseção sobre isso. Fale sobre:
  - **(A)** o número pequeno de participantes, a participação de pessoas próximas ao projeto (viés de cordialidade) e a avaliação em sessão curta, e não em uso real prolongado;
  - **(B)** o **viés de autosseleção**: a base contém apenas as iniciativas que foram cadastradas na plataforma, então **não é um censo** das iniciativas brasileiras. Fale também sobre a subjetividade da classificação, os campos preenchidos retroativamente e a concentração geográfica da rede de divulgação do projeto;
  - nos dois caminhos: a sua participação no desenvolvimento, que pode gerar viés.

### 3.5 Materiais e Métodos

**Materiais.** Monte o quadro-resumo com as versões **efetivamente usadas**: confira o `requirements.txt` e rode `pip freeze` na data da escrita. Várias dependências estão sem versão fixada, e o Chart.js precisa ser fixado antes (item 24). Versões encontradas em 11/09/2026:

| Ferramenta | Versão | Finalidade no trabalho |
|---|---|---|
| Python | 3.11 ou superior (README) | Linguagem do *back-end* |
| Django | 5.1.3 | *Framework* web, ORM e agregações dos indicadores |
| SQLite / MySQL | – | Banco de dados em desenvolvimento / em produção |
| Chart.js | sem versão fixada (fixar) | Gráficos do painel |
| Mapa do Brasil em SVG | – (registrar fonte e licença) | Mapa coroplético por UF |
| pandas e Jupyter (opcional) | – | Análise do *snapshot* **(B)** |
| Google Forms ou similar | – | Questionários SUS e TAM **(A)** |
| Git e GitHub | – | Versionamento |

**Métodos.** Para cada item, explique o que é, para que foi usado e por que foi escolhido:

- **modelagem dos dados para análise:** as dimensões criadas, a migração dos dados existentes e a curadoria das ações;
- **definição dos indicadores:** a regra de cada indicador (o que entra e o que não entra na contagem) e o módulo único de consultas;
- **projeto das visualizações:** por que cada gráfico foi escolhido para cada pergunta, como os valores do mapa foram normalizados e como a acessibilidade foi tratada;
- **controle de acesso dos painéis:** o que a coordenadora vê, o que a gestão vê e as permissões usadas;
- **testes automatizados** dos indicadores;
- **(A)** instrumentos de avaliação (roteiro de tarefas, SUS, itens do TAM e entrevista) e forma de análise;
- **(B)** exportação do *snapshot*, livro de códigos, procedimento de dupla classificação e cálculo do kappa.

> **Dica para o artigo:** os revisores valorizam o "por que X e não Y". Por exemplo: por que desenvolver o painel dentro da plataforma, com Django e Chart.js, e não usar uma ferramenta de BI pronta (Power BI, Metabase ou Looker Studio)? Informe só as alternativas **que foram de fato consideradas**. Se nenhuma foi avaliada, diga isso e trate como limitação. Não invente comparações.

### 3.6 Resultados (e Discussão)

Organize o capítulo pelas questões de pesquisa, e não por telas.

**Comum aos dois caminhos:**

- **Diagnóstico inicial:** mostre, de forma resumida, os problemas encontrados na primeira versão (itens 2 a 7 e 12) e por que eles mudariam as conclusões. Isso mostra rigor e justifica as decisões de modelagem.
- **Modelo de dados analítico:** apresente o diagrama das entidades usadas no painel, com o fato e as dimensões, e o dicionário de dados resumido em um quadro.
- **Qualidade da base:** apresente uma tabela com o número de registros e o percentual de campos não informados na data de corte.

**(A) Painel como ferramenta avaliada:**

- **Tarefas analíticas (QP1):** apresente em um quadro as perguntas das coordenadoras e da gestão e a visualização que responde a cada uma.
- **Painel (QP2):** mostre poucas telas (painel público, da coordenadora e de gestão), explicando a pergunta que cada visualização responde e as decisões de projeto (tipo de gráfico, normalização, filtros e acessibilidade).
- **Avaliação (QP3):** apresente o perfil das participantes (sem identificar), uma tabela com a taxa de sucesso e o tempo por tarefa, a pontuação média do SUS com a interpretação, os resultados do TAM e os temas das entrevistas, com trechos curtos e anônimos.
- **Discussão:** relacione os resultados com o Referencial Teórico e aponte o que precisa melhorar.

**(B) Painel como lente para o panorama:**

- **Distribuição geográfica (QP1):** mapa e tabela por região e por UF, em valores absolutos **e** proporcionais à população. Comente a diferença entre os dois.
- **Subáreas, tipos e públicos (QP1):** gráficos e tabelas, e o cruzamento subárea × região.
- **Evolução no tempo (QP2):** iniciativas por ano de início, separadas dos cadastros na plataforma.
- **Lacunas e comparação externa (QP3):** regiões, subáreas e públicos pouco atendidos. Se possível, compare com a distribuição de matrículas de mulheres em cursos de computação (INEP).
- **Confiabilidade da classificação:** o valor do kappa e como as divergências foram resolvidas.
- **Discussão:** relacione com os mapeamentos e os estudos citados no Referencial Teórico e retome o viés de autosseleção ao interpretar cada resultado.

Cuidados:

- toda tabela e todo gráfico devem informar a **data de corte** na fonte. Exemplo: "Fonte: Dados da plataforma TiParaElas, extraídos em 16/10/2026.";
- siga as regras de tabelas do IBGE das orientações gerais. Use "x" para dados omitidos para evitar identificação;
- não exponha nomes, e-mails ou dados pessoais de usuárias em figuras, trechos de código ou tabelas. No *ranking* de perfis, prefira não citar nomes no artigo;
- capturas de tela devem usar dados fictícios ou já públicos, com autorização.

### 3.7 Conclusão

- Responda **diretamente** à pergunta de pesquisa e a cada QP;
- comente cada objetivo específico;
- retome as principais contribuições;
- apresente as limitações com honestidade: **(A)** número de participantes e avaliação em sessão curta; **(B)** base não censitária e classificação retroativa;
- sugira trabalhos futuros, por exemplo: acompanhar o uso real do painel ao longo de um semestre, integrar os eventos da plataforma (app `eventos`, em desenvolvimento) como nova fonte de dados, publicar a base agregada como dados abertos e repetir o panorama anualmente.

### 3.8 Objetivos específicos

Serão entregues no final, junto com o Resumo, para refletirem o que foi **realmente feito**. Siga as regras das orientações gerais: 3 a 5 itens, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Verbos e temas que combinam com este trabalho:

- **revisar** a literatura sobre ...;
- **identificar** as tarefas analíticas ... / **diagnosticar** os indicadores ...;
- **modelar** os dados ... para análise ...;
- **desenvolver** o painel ... com ...;
- **(A)** **avaliar** a utilidade percebida ... com ...;
- **(B)** **classificar** as iniciativas ... e **analisar** a distribuição ...

Não transforme funcionalidades do sistema em objetivos (por exemplo, "permitir filtrar por estado").

### 3.9 Resumo e *Abstract*

- **Tamanho:** no TCC, parágrafo único com 150 a 500 palavras (NBR 6028:2021). No artigo, siga o limite da chamada. O WIT e os demais veículos da SBC normalmente exigem resumo em português e em inglês.
- **Sequência:** contexto (mulheres na computação), problema, objetivo, método (**A:** desenvolvimento e avaliação com participantes; **B:** análise documental da base na data de corte), principais resultados **com números** e principal conclusão.
- **Palavras-chave possíveis:** mulheres na computação; visualização de dados; painel analítico; *dashboard*; transparência; apoio à decisão; panorama.

### 3.10 Do TCC ao artigo

- **Estrutura típica:**
  - **(A)** Introdução; Fundamentação e trabalhos relacionados; O painel (dados e projeto); Método de avaliação; Resultados; Discussão; Ameaças à validade; Conclusão;
  - **(B)** Introdução; Fundamentação e trabalhos relacionados; Método (base, variáveis e classificação); Panorama; Discussão; Limitações; Conclusão.
- **Modelo:** use o exigido pela chamada (em geral, o modelo da SBC, também disponível no Overleaf).
- **Revisão às cegas:** se for o caso, retire da versão submetida os nomes, a instituição e o nome da plataforma, ou substitua por "[omitido]".
- **Dados e código:** o repositório é **privado**. Combine com o orientador o que pode ser divulgado: a base agregada (**B**) pode ser publicada com DOI (por exemplo, no Zenodo), o que valoriza o artigo, mas nunca com dados pessoais.
- **Autoria:** defina a autoria do artigo (aluno, orientador e, se for o caso, demais integrantes) antes da submissão.
- **Submissão:** nenhum artigo deve ser submetido sem a revisão final do orientador.

---

## 4. Prazos

Hoje é **11/09/2026**. Cada prazo conta a partir da conclusão da etapa anterior, e as datas abaixo consideram que cada etapa é concluída no prazo. Entregar antes é bem-vindo. Envie cada parte ao orientador até a data indicada.

| Etapa de escrita | Duração | Data-limite |
|---|---|---|
| Introdução e Objetivo geral | 1 semana a partir de hoje | **18/09/2026** (sexta-feira) |
| Referencial Teórico | 1 semana e meia após a Introdução | **28/09/2026** (segunda-feira) |
| Metodologia | 1 semana após o Referencial Teórico | **05/10/2026** (segunda-feira) |
| Materiais e Métodos | 1 semana após a Metodologia | **12/10/2026** (segunda-feira) |
| Resultados | 2 semanas após Materiais e Métodos | **26/10/2026** (segunda-feira) |
| Conclusão | 1 semana após os Resultados | **02/11/2026** (segunda-feira) |
| Resumo e Objetivos específicos | 1 semana após a Conclusão | **09/11/2026** (segunda-feira) |

> **Atenção:** 12/10/2026 e 02/11/2026 são feriados nacionais. Combine com o orientador se a entrega deve ser antecipada para o dia útil anterior.

**Alinhamento sugerido das implementações.** É uma recomendação; os prazos oficiais são os da tabela acima. Os Resultados dependem das implementações, dos dados e, no caminho A, da avaliação:

| Até | O que deve estar pronto | Por quê |
|---|---|---|
| 18/09/2026 | Caminho (A ou B) definido com o orientador; acesso aos dados de produção solicitado; itens 1 a 9 (confiabilidade dos indicadores); *issues* criadas. **(A)** Coordenadoras convidadas e a questão do CEP resolvida (se for necessário, submeter já) | A Introdução depende do caminho, e nenhum número deve ser usado antes das correções |
| 05/10/2026 | Itens 10 a 18 (modelo de dados, migrações, dicionário de dados e curadoria das ações existentes); item 27 iniciado. **(A)** Roteiro de tarefas e questionários prontos. **(B)** Livro de códigos pronto e dupla classificação iniciada | A Metodologia descreve esse processo |
| 16/10/2026 | Itens 19 a 30 (painéis, filtros, acessibilidade, exportação, testes e documentação); *snapshot* gerado na data de corte (item 28). **(A)** Avaliação aplicada. **(B)** Classificação concluída e kappa calculado | Sobram 10 dias para analisar e escrever os Resultados com os dados fechados |

Antes de cada envio, use o [checklist das orientações gerais](../../README.md#checklist-antes-de-enviar-uma-versão-ao-orientador).
