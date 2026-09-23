# Orientações de Escrita e Prazos – Mariana (Projeto TiParaElas)

Este documento reúne as orientações individuais do trabalho acadêmico da Mariana. Ele complementa as [orientações gerais](../../README.md), que continuam valendo para a estrutura do trabalho, a formatação ABNT, as citações, as referências, as figuras e as tabelas.

> **Importante:** a análise do código foi feita em 11/09/2026 na cópia local do repositório [nicifrn/tiparaelas](https://github.com/nicifrn/tiparaelas) (privado), na *branch* `feature/dashboard-transparencia` (commit `db6588b`). Essa *branch* ainda não foi integrada à `main` (commit `ff0d958`). A página de Transparência corresponde aos arquivos `apps/core/templates/dashboard.html` (rota `/transparencia/`), `static/assets/css/transparencia.css` e `templates/publico/mapa-brasil.html`. Não existe um arquivo `transparencia.html`. Sempre prevalecem os acordos feitos com o orientador.

## Sumário

- [1. Temática do trabalho](#1-temática-do-trabalho)
- [2. O que falta implementar](#2-o-que-falta-implementar)
- [3. Orientações de escrita](#3-orientações-de-escrita)
- [4. Prazos](#4-prazos)

---

## 1. Temática do trabalho

### 1.1 Tema e recorte

**Tema:** acessibilidade e design inclusivo na web, segundo as Diretrizes de Acessibilidade para Conteúdo Web (WCAG).

**Especialização:** desenvolvimento web com foco em padrões de acessibilidade. É uma competência central do curso de Tecnologia em Sistemas para Internet (TSI) e muito valorizada no mercado.

**Recorte:** o trabalho **não** é um manual do TiParaElas. Ele usa a plataforma como **caso real** para avaliar e corrigir a acessibilidade segundo a **WCAG 2.2, níveis A e AA**, combinando:

- **avaliação automática** com axe, WAVE, Lighthouse e ASES (ferramenta do governo federal que avalia segundo o eMAG);
- **inspeção manual**, critério a critério;
- **teste com tecnologias assistivas**: navegação só por teclado, leitor de tela (NVDA no computador; TalkBack ou VoiceOver no celular), ampliação de 200% e 400% e contraste;
- **correção** das barreiras no código e **reavaliação** com os mesmos procedimentos (comparação antes e depois);
- se possível, **teste com usuárias reais** que usam tecnologia assistiva.

**Marco brasileiro:** o trabalho deve se ancorar no Modelo de Acessibilidade em Governo Eletrônico (eMAG 3.1) e na Lei Brasileira de Inclusão da Pessoa com Deficiência (LBI, Lei nº 13.146/2015), que torna obrigatória a acessibilidade nos sítios mantidos por empresas e por órgãos de governo (art. 63). O TiParaElas é um projeto de uma instituição pública federal (IFRN), o que reforça a pertinência do eMAG.

**Enquadramento:** a inclusão de mulheres na computação e a inclusão de pessoas com deficiência fazem parte da **mesma agenda de equidade**. Uma plataforma criada para dar visibilidade a mulheres na tecnologia não pode excluir mulheres com deficiência, que enfrentam as duas barreiras ao mesmo tempo. Esse argumento dá coerência e relevância ao tema.

**Título provisório** (o título definitivo é a última informação a ser definida): *Acessibilidade em uma plataforma de visibilidade de mulheres na tecnologia: avaliação de conformidade com a WCAG 2.2 e o eMAG no projeto TiParaElas*.

### 1.2 O caso estudado: a plataforma TiParaElas

O TiParaElas é uma plataforma web do NIC – IFRN Campus Canguaretama, desenvolvida em Django, que divulga ações (iniciativas voltadas a mulheres na TI), perfis de "Inspirações", atividades do projeto e indicadores de transparência. As usuárias cadastradas (por exemplo, coordenadoras de iniciativas) publicam conteúdo por um painel interno. Partes que interessam à acessibilidade:

| Área | Onde está | Por que interessa |
|---|---|---|
| Layout público | `templates/publico/` (`base.html`, `head.html`, `menu.html`, `rodape.html`), `static/assets/css/styles.css` e `static/assets/js/script.js` | Aparece em todas as páginas públicas: um erro aqui se repete no site inteiro |
| Páginas públicas | `apps/core/templates/`: início, galeria de ações (filtros e paginação), detalhe de ação (galeria de imagens e vídeos do YouTube), inspirações, detalhe de inspiração, sobre, atividades, transparência (gráficos e mapa), contato, privacidade e termos | São as páginas usadas pelo público e o núcleo da amostra de avaliação |
| Autenticação | `apps/usuarios/templates/`: login (e-mail e senha ou SUAP), cadastro (estado e cidade carregados dinamicamente), recuperação de senha | Formulários são uma das maiores fontes de barreiras |
| Painel interno | `templates/privado/` e 36 telas `admin_*` (cadastro de ações, perfil de inspiração, validações) | É onde as usuárias produzem o conteúdo, inclusive as imagens que precisam de texto alternativo |

Números levantados em 11/09/2026:

| Indicador | Valor |
|---|---|
| Commits na *branch* analisada | 69 (de 25/06/2025 a 10/07/2026) |
| *Templates* HTML | 83 arquivos, com cerca de 11,8 mil linhas |
| Folhas de estilo | 16 arquivos CSS |
| Testes automatizados | 569 linhas em `tests.py`, nenhum teste de acessibilidade |
| Integração contínua (CI) | não há |
| Versões principais | Django 5.1.3, Python 3.11, Chart.js (via CDN, sem versão fixada) |

**O que já está bem encaminhado** (registre como parte do diagnóstico inicial, pois mostra que a acessibilidade existe de forma parcial):

- `lang="pt-BR"` nas bases pública e privada e `<title>` específico em cada página;
- rótulos (`<label for>`) associados na maioria dos campos, e `fieldset`/`legend` no filtro por tipo de ação;
- `autocomplete` nos formulários de login, cadastro e contato;
- ícones decorativos com `aria-hidden="true"` e botões só com ícone com `aria-label`;
- trilha de navegação (*breadcrumb*) e paginação com `aria-current="page"`;
- `title` nos `iframe` dos vídeos;
- visualizador de imagens (*lightbox*) com `role="dialog"` e fechamento pela tecla Esc;
- indicador de força da senha anunciado com `aria-live`;
- ausência de CAPTCHA, o que favorece o critério 3.3.8 (Autenticação acessível).

> A página de **Transparência** foi criada no contexto do painel de dados (outro trabalho do projeto). Combine com o orientador e com o colega responsável pelo painel: ele implementa os gráficos, e você define os requisitos de acessibilidade, avalia e corrige ou valida as correções. Deixe essa divisão explícita no texto.

### 1.3 Pergunta de pesquisa

**Pergunta principal:** em que medida a plataforma TiParaElas atende à WCAG 2.2 (níveis A e AA) e ao eMAG, quais barreiras afetam pessoas que usam tecnologias assistivas e qual é o efeito das correções aplicadas?

Para que a pergunta possa ser respondida com evidências em um artigo, desdobre-a em questões de pesquisa (QP) menores (confirme com o orientador):

- **QP1:** qual é o nível de conformidade inicial da plataforma e quais barreiras são encontradas, por critério de sucesso e por tipo de página?
- **QP2:** quais barreiras cada método detecta (ferramentas automáticas, inspeção manual e tecnologias assistivas), e o que as ferramentas automáticas **não** conseguem detectar?
- **QP3:** qual é o efeito das correções na conformidade (antes e depois) e, se houver teste com usuárias, no sucesso das tarefas?

### 1.4 Formato e onde publicar

**Formato:** estudo de avaliação de conformidade (estudo de caso), contendo:

- método claro e reproduzível, baseado na metodologia WCAG-EM, do W3C;
- amostra de páginas e de processos completos;
- catálogo de barreiras encontradas, com o critério WCAG, a recomendação do eMAG, a severidade e o método que detectou cada uma;
- correções aplicadas, com exemplos de código;
- comparação antes e depois;
- se possível, resultados do teste com usuárias que usam tecnologia assistiva;
- lições aprendidas e padrões de correção reutilizáveis em outros projetos Django.

**Onde publicar.** Confira sempre a chamada vigente: prazos, trilhas, limite de páginas, modelo e se a revisão é às cegas.

- **IHC** (Simpósio Brasileiro sobre Fatores Humanos em Sistemas Computacionais, da SBC), a comunidade brasileira que mais publica sobre acessibilidade;
- **WebMedia** (Simpósio Brasileiro de Sistemas Multimídia e Web, da SBC);
- **WIT** (*Women in Information Technology*), evento do CSBC, onde o enquadramento de equidade de gênero e acessibilidade é especialmente bem-vindo;
- **JIS** (*Journal on Interactive Systems*, da SBC) e **iSys** (Revista Brasileira de Sistemas de Informação), para uma versão estendida;
- internacionais, com exigência maior: **W4A** (*International Web for All Conference*) e **ASSETS** (*ACM SIGACCESS Conference on Computers and Accessibility*), em trilhas de pôster ou de relato de experiência.

Os artigos dos veículos da SBC estão na SBC OpenLib (SOL): https://sol.sbc.org.br. **Antes de começar a escrever, leia pelo menos três artigos de avaliação de acessibilidade publicados neles** para entender o formato esperado.

---

## 2. O que falta implementar

### 2.1 Antes de corrigir: congele a linha de base

A comparação antes e depois é o eixo do artigo. Se você corrigir algo antes de medir, perde o "antes". Por isso, **nenhuma correção deve ser feita antes de concluir a avaliação inicial**.

1. **Defina a versão avaliada.** Combine com o orientador se a *branch* `feature/dashboard-transparencia` será integrada à `main` antes da avaliação (a página de Transparência precisa estar na amostra). Crie uma *tag* no commit avaliado, por exemplo `a11y-linha-de-base`.
2. **Use dados fictícios e realistas.** A avaliação depende do conteúdo (imagens, textos, vídeos). Popule o banco local com ações e perfis fictícios, com imagens na galeria e vídeos. Não use dados reais de pessoas em capturas de tela nem nos relatórios.
3. **Defina o escopo e a amostra** (passos 1 a 3 da WCAG-EM). Amostra sugerida:

| Tipo | Páginas ou processos |
|---|---|
| Páginas públicas | Início; galeria de ações (com filtros aplicados e com paginação); detalhe de ação (com galeria e vídeo); inspirações; detalhe de inspiração; sobre; atividades; transparência; contato; política de privacidade; página de erro 404 |
| Autenticação | Login; cadastro (vazio e com erros de validação); recuperação de senha |
| Painel interno | Cadastro de ação; edição do perfil de inspiração |
| Processos completos | Criar conta; entrar; filtrar ações e abrir um detalhe; enviar mensagem pelo contato; cadastrar uma ação com imagem |

4. **Registre o ambiente:** navegadores e versões, versões das ferramentas e do leitor de tela, largura de tela e data de cada avaliação.
5. **Guarde as evidências** em `docs/acessibilidade/antes/`: relatórios exportados das ferramentas, capturas de tela e a planilha de barreiras (item 29).

### 2.2 Lista de pendências

- **Prioridade 1:** barreiras no layout global. Uma correção resolve o problema em todas as páginas.
- **Prioridade 2:** barreiras em páginas e componentes específicos (Transparência, formulários, imagens e mídia).
- **Prioridade 3:** conformidade legal, processo e evidências para o artigo.

Crie uma *issue* no GitHub para cada item, com a etiqueta `acessibilidade` e o critério WCAG no título. Os critérios indicados são da WCAG 2.2.

> **Atenção ao método:** a lista abaixo vem de uma **leitura do código** e serve como ponto de partida. Ela **não substitui** a avaliação. O artigo deve relatar o que o **procedimento de avaliação** encontrou (seção 3.4), incluindo quais itens as ferramentas detectaram ou não. Registre também as barreiras que não estão nesta lista.

#### Prioridade 1 – Layout global

| # | Situação encontrada | Critério WCAG 2.2 | O que fazer |
|---|---|---|---|
| 1 | Não há link "Pular para o conteúdo" em `templates/publico/base.html` nem em `templates/privado/base.html`. Quem navega por teclado precisa passar pelos 7 links e 2 botões do menu em todas as páginas | 2.4.1 Ignorar blocos (A) | Inserir um link como primeiro elemento focável, visível ao receber foco, apontando para `<main id="conteudo" tabindex="-1">`. Avaliar a barra de acessibilidade com atalhos recomendada pelo eMAG (ir para o conteúdo, o menu e o rodapé) |
| 2 | Cada *template* declara o próprio `<main>`, e ele **não existe** em 11 páginas públicas (`acoes.html`, `acao_detalhe.html`, `inspiracoes.html`, `inspiracao_detalhe.html`, `sobre.html`, `atividades.html`, `excluir_conta.html`, `reaceitar_termos.html` e erros 400, 403 e 404) nem nas 36 telas `admin_*` | 1.3.1 Informações e relações (A) | Colocar `<main id="conteudo">` nas bases, envolvendo o `{% block conteudo %}`, e remover os `<main>` dos *templates* filhos |
| 3 | Não existe regra global de foco. Os campos de formulário usam `outline: none` em 9 folhas de estilo, e a substituição é fraca: na busca da galeria, uma sombra com 12% de opacidade (`acoes.css`); em `inspiracoes.css` e `sobre.css`, apenas a troca da cor da borda de 1px. O campo do formulário do rodapé (`styles.css`) remove o contorno sem substituto | 2.4.7 Foco visível (AA); 1.4.11 Contraste não textual (AA) | Criar uma regra global `:focus-visible` (por exemplo, `outline: 3px solid` com `outline-offset`), com contraste mínimo de 3:1 com as cores vizinhas, e remover os `outline: none` sem substituto equivalente. Testar com Tab em todas as páginas da amostra |
| 4 | O cabeçalho é fixo no topo (`position: sticky`, 76px de altura) e pode encobrir o elemento que recebe foco, principalmente ao voltar com Shift+Tab ou ao seguir uma âncora | 2.4.11 Foco não obscurecido – mínimo (AA), **novo na 2.2** | Testar. Se confirmar, usar `scroll-padding-top` no `html` com a altura do cabeçalho |
| 5 | O item "Sobre" do menu é um `<span role="button" tabindex="0" aria-expanded="false">`. O `aria-expanded` **nunca muda** (não há código para isso em `script.js`), e a lista usa `role="menu"`/`role="menuitem"`, que exigem navegação por setas não implementada | 4.1.2 Nome, função, valor (A) | Trocar por `<button type="button" aria-expanded aria-controls>`, alternado por JavaScript (Enter, Espaço e Esc), e remover `role="menu"` e `role="menuitem"`. Seguir o padrão *Disclosure Navigation Menu* do ARIA APG |
| 6 | O menu móvel (`menu-toggle`) e o painel de filtros da galeria não levam o foco para dentro ao abrir, não devolvem o foco ao botão ao fechar e não fecham com Esc. O `acoes.js`, que trata o Esc, **não é carregado** por nenhum *template* | 2.4.3 Ordem do foco (A) | Mover o foco ao abrir e devolvê-lo ao fechar, fechar com Esc e verificar se os links do menu fechado ficam fora da ordem de tabulação. Remover o `acoes.js` ou passar a usá-lo |
| 7 | Rodapé (`rodape.html`): o `</div>` que fecha `.footer-top` ficou **dentro de um comentário HTML** (linha 54), deixando a estrutura quebrada; os títulos são `<h4>` sem `<h2>` ou `<h3>` antes; os 4 links das redes sociais usam `href="#"` e não levam a lugar nenhum | 1.3.1 (A); 2.4.4 Finalidade do link (A) | Fechar a `div` fora do comentário; usar o nível de título correto e ajustar o tamanho por CSS; preencher os links reais ou removê-los. Validar o HTML no W3C Nu HTML Checker (a WCAG 2.2 removeu o critério 4.1.1, mas o eMAG pede respeito aos padrões web) |
| 8 | **Contraste insuficiente**, calculado a partir das cores de `styles.css`: (a) `--c-accent` (#B8755F) tem 3,65:1 sobre branco e 3,49:1 sobre o fundo, e é usado em textos de tamanho normal (marca, *hover* de links); (b) `--c-muted` (#76707E) tem 4,28:1 sobre `--c-bg-2`, usado na trilha de navegação e no subtítulo do cabeçalho das páginas internas (`.page-head`); (c) nos selos do *ranking* da Transparência, texto branco de 13,5px sobre degradê dourado (1,40 a 1,97:1), prateado (1,82 a 3,95:1) e bronze (3,14 a 5,62:1) | 1.4.3 Contraste mínimo (AA): 4,5:1 para texto normal e 3:1 para texto grande | Criar variantes mais escuras das cores para uso em texto (por exemplo, `--c-accent-texto`), até atingir 4,5:1, e reavaliar com o WebAIM Contrast Checker. Preservar a identidade visual nos elementos grandes e decorativos |
| 9 | O CSS global remove o sublinhado de todos os links (`a { text-decoration: none }`). Só algumas folhas o recolocam (`legal.css`, `login.css`, `contato.css`) | 1.4.1 Uso de cor (A) | Verificar cada link dentro de texto corrido. Se ele se distinguir só pela cor (sem 3:1 em relação ao texto e sem outra pista visual), sublinhar |
| 10 | Nenhum `prefers-reduced-motion`: há animação de revelação ao rolar (`.reveal`), contadores animados, `scroll-behavior: smooth` e deslocamentos no *hover* | 2.3.3 Animação a partir de interações (AAA), boa prática além do AA | Desativar animações e rolagem suave em `@media (prefers-reduced-motion: reduce)` e verificar `matchMedia` no JavaScript antes de animar. No artigo, apresente como melhoria além do nível AA |
| 11 | Tamanho de alvo **a verificar**: ícones das redes sociais no rodapé (SVG de 18×18px), caixas de seleção dos filtros, botão de fechar filtros e setas dos *cards* | 2.5.8 Tamanho do alvo – mínimo (AA), **novo na 2.2** | Medir a área clicável (mínimo de 24×24px CSS ou espaçamento equivalente) e ajustar o *padding* |
| 12 | Área interna: o link ativo da barra lateral é indicado só pela classe `is-active`, sem `aria-current="page"`; não há link para pular o menu nem `<main>` na base. Há ainda 4 *templates* antigos com `lang="en"` (`apps/acoes/templates/acao.html`, `acao_cadastrar.html`, `usuario.html` e `usuario_cadastrar.html`) que nenhuma *view* renderiza | 1.3.1 (A); 2.4.1 (A); 3.1.1 Idioma da página (A) | Adicionar `aria-current="page"` e aplicar os itens 1 e 2 à base privada. Remover os *templates* antigos, após confirmar com a equipe |

#### Prioridade 2 – Página de Transparência (gráficos e mapa)

| # | Situação encontrada | Critério WCAG 2.2 | O que fazer |
|---|---|---|---|
| 13 | Os 3 gráficos (Chart.js) são desenhados em `<canvas>` sem nenhuma alternativa: sem `aria-label`, sem conteúdo alternativo e sem tabela de dados. Quem usa leitor de tela não recebe nenhuma informação | 1.1.1 Conteúdo não textual (A); 1.3.1 (A) | Para cada gráfico: `role="img"` com um `aria-label` que resuma a informação e uma **tabela de dados** real (visível ou em `<details>` "Ver dados em tabela"), com `<caption>` e `<th scope>`. Consulte a seção de acessibilidade da documentação do Chart.js |
| 14 | Mapa do Brasil (SVG): o valor de cada estado aparece só no *tooltip* do `mousemove`, que é inacessível por teclado, toque e leitor de tela (e tem `aria-hidden="true"`). A intensidade é indicada só pela cor: a faixa mais clara tem 1,17:1 de contraste com o fundo, e os estados sem registro têm a mesma cor do fundo, separados apenas por bordas brancas (1,12:1). A legenda é um degradê sem números | 1.1.1 (A); 1.4.1 (A); 1.4.11 (AA); 2.1.1 Teclado (A); 1.4.13 Conteúdo em foco ou *hover* (AA) | Oferecer a tabela "Estado × quantidade" como alternativa principal; legenda com faixas discretas e valores numéricos; bordas e cores com contraste de 3:1. Se a interação for mantida, tornar os estados focáveis, com nome acessível, e exibir o *tooltip* também no foco |
| 15 | O mesmo SVG é incluído duas vezes na página (`{% include 'publico/mapa-brasil.html' %}`), o que **duplica os `id`** (`Layer_1`, `MG`, `SP` etc.) | 1.3.1 (A) e validade do HTML | Trocar os `id` por atributos `data-uf` ou gerar um prefixo por instância |
| 16 | Os contadores de "Dados gerais" começam com o texto "0" no HTML e só mostram o valor real quando o *card* aparece na tela. Quem lê com o cursor virtual do leitor de tela pode ouvir "0". Na página inicial isso não acontece, porque o valor real já está no HTML | 1.3.1 (A) | Renderizar o valor real no HTML, animar só visualmente e respeitar o item 10 |
| 17 | No *ranking*, o `aria-label="Posição 1"` está em uma `<div>` sem função (o ARIA 1.2 proíbe `aria-label` em elementos genéricos, e os leitores de tela o ignoram); os títulos são cortados com reticências (`text-overflow: ellipsis`); as `<section>` usam `aria-label` que repete o `<h2>` visível | 1.3.1 (A); 1.4.10 Refluxo (AA) | Usar lista ordenada (`<ol>`, que já informa a posição), permitir quebra de linha nos títulos e usar `aria-labelledby` apontando para o `<h2>` |
| 18 | O Chart.js é carregado de `https://cdn.jsdelivr.net/npm/chart.js`, **sem versão fixada** | – (reprodutibilidade) | Fixar a versão, de preferência servindo o arquivo localmente. Sem isso, a biblioteca pode mudar entre a avaliação "antes" e a "depois" |

#### Prioridade 2 – Formulários

| # | Situação encontrada | Critério WCAG 2.2 | O que fazer |
|---|---|---|---|
| 19 | As mensagens de erro (`<span class="form-error">` no login e no cadastro; `field-hint` colorido no painel) **não são associadas** aos campos: não há `aria-describedby`, e não há nenhum `aria-invalid` no projeto. Após enviar com erro, o foco não vai para o primeiro erro nem para um resumo | 3.3.1 Identificação do erro (A); 1.3.1 (A); 4.1.2 (A) | Criar um componente reutilizável (por exemplo, `templates/componentes/campo.html`) que renderize rótulo, campo com `aria-invalid="true"` e `aria-describedby`, e mensagem de erro com `id`. Com erros, exibir um resumo no topo com links para os campos e levar o foco até ele. É uma boa contribuição técnica para o artigo |
| 20 | Campos obrigatórios: no login e no cadastro não há indicação visual; no contato, o `*` tem `aria-hidden="true"` e o significado dele não é explicado; no painel, o `*` é só vermelho (estilo em linha). Os formulários usam `novalidate` | 3.3.2 Rótulos ou instruções (A) | Explicar "Campos marcados com * são obrigatórios" no início de cada formulário e marcar os campos com `required` (pelos *widgets* em `forms.py`) |
| 21 | O carregamento das cidades (cadastro, galeria de ações e painel) troca o conteúdo do `<select>` para "Carregando…" ou "Erro ao carregar cidades" sem nenhum anúncio. O campo cidade fica desabilitado até a escolha do estado, sem explicação associada | 4.1.3 Mensagens de status (AA) | Usar uma região `aria-live="polite"` para as mensagens de estado e associar a instrução ao campo com `aria-describedby` |
| 22 | Ajustes de semântica: o link "Entrar com SUAP" tem `role="button"`, mas navega para outra página; no cadastro, o botão de mostrar senha não tem `aria-pressed` (no login tem); há 54 links com `target="_blank"` sem aviso de nova aba, inclusive para páginas internas (Política de Privacidade no cadastro) | 4.1.2 (A); 3.2.5 Mudança mediante solicitação (AAA). O eMAG recomenda não abrir novas instâncias sem solicitação do usuário | Remover o `role="button"`, padronizar o `aria-pressed`, evitar nova aba em páginas internas e, nos links externos, avisar "(abre em nova aba)" no nome acessível |
| 23 | Verificar os formulários **não** cobertos pelo diagnóstico inicial: meus dados, perfil de inspiração, redefinição de senha e cadastro de ação (incluindo `autocomplete`, que já existe no login, no cadastro e no contato) | 1.3.5 Identificar o propósito de entrada (AA); 3.3.8 Autenticação acessível – mínimo (AA), **novo na 2.2** | Aplicar os itens 19 a 22 também a esses formulários |

#### Prioridade 2 – Imagens, mídia e estrutura do conteúdo

| # | Situação encontrada | Critério WCAG 2.2 | O que fazer |
|---|---|---|---|
| 24 | **Nenhum modelo de imagem tem campo de texto alternativo** (`Acao.imagem_principal`, `AcaoImagem`, `UsuarioPerfil.foto_principal`, `UsuarioPerfilImagem`, `Parceiros`, `DadosSite`). Os *templates* geram textos genéricos ("Imagem 1 — título da ação", "Imagem 2 de Nome") que não descrevem a imagem. Na página inicial, a imagem principal tem `aria-label="Mulher trabalhando em tecnologia"` fixo, mesmo quando a administração envia outra imagem | 1.1.1 Conteúdo não textual (A) | Criar o campo `texto_alternativo` (com opção "imagem decorativa") nos modelos e formulários, com migração e um texto de ajuda que ensine a escrever uma boa descrição. Usar o campo nos *templates* e no *lightbox*. Ponto importante para a discussão: **a acessibilidade também depende de quem cadastra o conteúdo** |
| 25 | *Lightbox* (detalhe de ação e de inspiração): ao abrir, o foco não vai para a janela; ao fechar, não volta para a imagem clicada; e a página ao fundo continua acessível pelo Tab | 2.4.3 Ordem do foco (A); 4.1.2 (A) | Usar o elemento nativo `<dialog>` com `showModal()`, que resolve foco e fundo inerte, ou seguir o padrão *Dialog (Modal)* do ARIA APG |
| 26 | Vídeos do YouTube: os `iframe` têm `title` (bom), mas o cadastro de ação não orienta sobre legendas e não há campo para transcrição | 1.2.2 Legendas – pré-gravadas (A); 1.2.5 Audiodescrição – pré-gravada (AA) | Orientar, no formulário, a conferir se o vídeo tem legendas revisadas (não apenas automáticas) e criar um campo opcional de transcrição. No artigo, discuta a responsabilidade sobre o **conteúdo de terceiros** e como declará-lo |
| 27 | Hierarquia de títulos com saltos: `atividades.html` passa de `<h1>` para `<h3>`; em `acao_detalhe.html`, os vídeos usam `<h4>` logo após um `<h2>`; o rodapé usa `<h4>` | 1.3.1 (A); 2.4.6 Cabeçalhos e rótulos (AA) | Corrigir os níveis e ajustar o tamanho visual por classe CSS, e não pela escolha da *tag* |

#### Prioridade 3 – Conformidade, processo e evidências

| # | Situação encontrada | O que fazer |
|---|---|---|
| 28 | Não há declaração de acessibilidade | Criar a página `/acessibilidade/` com: padrão adotado (WCAG 2.2 AA e eMAG 3.1), data da última avaliação, limitações conhecidas, atalhos de teclado e um canal para relatar barreiras. Colocar o link no rodapé e na barra de atalhos. Confira no art. 63 da LBI a exigência do símbolo de acessibilidade. Manter o contato no mesmo lugar em todas as páginas (critério 3.2.6 Ajuda consistente, **novo na 2.2**) |
| 29 | Não há estrutura para registrar a avaliação | Criar `docs/acessibilidade/` com: amostra, versões das ferramentas, relatórios "antes" e "depois" e uma **planilha de barreiras** com as colunas: identificador, página, componente, critério WCAG, nível, recomendação eMAG, método que detectou (axe, WAVE, Lighthouse, ASES, manual, teclado, leitor de tela ou usuária), severidade, evidência (captura), situação e commit da correção |
| 30 | Não há testes automatizados de acessibilidade nem CI | Criar um *workflow* no GitHub Actions com `pa11y-ci` ou axe-core com Playwright, rodando nas páginas da amostra a cada *pull request*. Deixe claro no texto que isso **evita regressões**, mas não substitui a avaliação manual |
| 31 | Teste com usuárias ainda não planejado | **Decidir com o orientador até 18/09/2026.** Se for feito, é preciso submeter o projeto ao Comitê de Ética em Pesquisa (CEP), pela Plataforma Brasil, com Termo de Consentimento Livre e Esclarecido (TCLE) em formato acessível. Para o recrutamento, procure o NAPNE do IFRN. A tramitação no CEP costuma levar semanas: veja o alerta na seção 4 |
| 32 | Processo | Uma *issue* por barreira, uma *branch* e um *pull request* por correção e mensagens de commit que citem o critério, por exemplo `fix(a11y): adiciona foco visível global [WCAG 2.4.7]`. Assim, cada correção fica rastreável até a barreira e o critério, o que gera dados para o artigo |

**Métricas sugeridas** (colete antes e depois, com a data e o *hash* do commit):

| Métrica | Como obter |
|---|---|
| Violações por página e por ferramenta | axe (violações e elementos afetados, por impacto), WAVE (erros, erros de contraste e alertas), Lighthouse (pontuação de acessibilidade) e ASES (percentual de conformidade com o eMAG) |
| Barreiras únicas por critério, nível (A/AA) e princípio | Planilha consolidada, após remover duplicidades entre ferramentas e páginas |
| Situação de cada critério por página (satisfeito, não satisfeito ou não se aplica) | Inspeção manual seguindo a WCAG-EM. A WCAG 2.2 tem 55 critérios nos níveis A e AA |
| Barreiras detectadas por método | Cruzamento da planilha: só pelas ferramentas, só pela inspeção manual ou por tecnologia assistiva, ou por ambos. É o dado central da QP2 |
| Esforço de correção | Commits, arquivos e linhas alterados por item (`git log --numstat`) |
| Teste com usuárias (se houver) | Sucesso por tarefa, tempo, erros, pedidos de ajuda e comentários (protocolo de pensar em voz alta) |

> **Cuidado com a pontuação do Lighthouse:** ela não mede conformidade. Uma página pode ter pontuação 100 e continuar inacessível. Use-a apenas como um dos indicadores.

---

## 3. Orientações de escrita

Escreva o TCC no modelo ABNT, seguindo as [orientações gerais](../../README.md), mas pense no **artigo** desde o início. Toda afirmação sobre acessibilidade precisa de uma evidência: critério de sucesso, relatório de ferramenta, captura de tela, commit ou referência.

Dois cuidados de linguagem:

- evite "o sistema é acessível" ou "100% acessível". Escreva o que foi verificado: "na amostra avaliada, os critérios X e Y passaram a ser atendidos";
- use "pessoa com deficiência", termo adotado pela LBI e pela Convenção sobre os Direitos das Pessoas com Deficiência. Evite "portador de deficiência", "pessoa especial" e "deficiente".

### 3.1 Introdução

- **Contextualização:**
  - pesquise dados do IBGE sobre pessoas com deficiência no Brasil (a PNAD Contínua 2022 estimou cerca de 18,6 milhões de pessoas, 8,9% da população de 2 anos ou mais; confira na fonte e veja também os dados do Censo 2022) e fale sobre a internet como meio de acesso a informação, educação e trabalho;
  - fale sobre a acessibilidade digital como direito: a Convenção sobre os Direitos das Pessoas com Deficiência (promulgada pelo Decreto nº 6.949/2009, art. 9º) e a LBI (art. 63);
  - pesquise sobre a baixa participação de mulheres na computação (por exemplo, dados do Censo da Educação Superior, do INEP, e iniciativas como o Programa Meninas Digitais, da SBC);
  - conecte os dois temas: plataformas que promovem a equidade de gênero precisam ser acessíveis para não reproduzir outra exclusão. Pesquise sobre interseccionalidade e mulheres com deficiência na tecnologia.
- **Problemática:**
  - pesquise o relatório mais recente do *WebAIM Million* e os levantamentos do Movimento Web para Todos sobre sítios brasileiros, e fale sobre as falhas mais comuns: baixo contraste, imagens sem texto alternativo, campos sem rótulo e links vazios;
  - fale sobre a acessibilidade tratada tardiamente no desenvolvimento e sobre a dependência do conteúdo cadastrado pelas usuárias (texto alternativo de imagens e legendas de vídeos);
  - fale sobre a limitação das ferramentas automáticas, que detectam só parte das barreiras (Vigo; Brown; Conway, 2013), e sobre problemas reais que nem estão cobertos pelas diretrizes (Power *et al.*, 2012). Isso justifica combinar métodos.
- **Caminho para a solução:**
  - apresente a WCAG 2.2, o eMAG 3.1 e a norma brasileira ABNT NBR 17225 (confira a edição vigente);
  - fale sobre os métodos de avaliação: ferramentas automáticas, inspeção por especialista (WCAG-EM) e testes com usuários de tecnologias assistivas;
  - cite estudos parecidos (SOL: IHC e WebMedia) que avaliaram a acessibilidade de sítios brasileiros, como portais de governo e de instituições de ensino. Mostre a lacuna: poucos relatam o **ciclo completo** (avaliação, correção e reavaliação) com comparação entre métodos, e menos ainda em plataformas voltadas à equidade de gênero. **Confirme essa lacuna na sua revisão da literatura** antes de afirmá-la.
- **Apresentação da solução:**
  - apresente o TiParaElas: público, funcionalidades e tecnologias (Django);
  - diga o que este trabalho faz: avalia a conformidade de uma amostra de páginas e processos com a WCAG 2.2 (A e AA) e o eMAG, corrige as barreiras no código (*templates*, CSS, JavaScript e modelos de dados) e reavalia com os mesmos procedimentos;
  - informe se houve teste com usuárias e onde a plataforma foi testada (ambiente local ou produção). Não mencione avaliações que não aconteceram.
- **Vínculo com projetos:** fale sobre o NIC, o histórico do TiParaElas (repositório criado em 25/06/2025) e a equipe. Deixe explícito o que é **contribuição sua**: no histórico do Git constam a criação do banco de dados, o cadastro e a autenticação, a redefinição de senha (2025) e o gerenciamento de tipos de evento (2026); o escopo deste TCC é a acessibilidade. Informe que a página de Transparência pertence ao trabalho do painel de dados e qual foi a sua participação nela.
- **Pergunta de pesquisa e contribuições:** feche a Introdução com a pergunta de pesquisa e as QPs (seção 1.3) e com uma lista curta de contribuições. Por exemplo: o relatório de conformidade da plataforma; o catálogo de barreiras por método de detecção; um conjunto de correções reutilizáveis em projetos Django (formulário acessível, alternativa textual para gráficos e mapas, campo de texto alternativo para conteúdo cadastrado por usuárias); a comparação antes e depois; e as lições aprendidas.

### 3.2 Objetivo geral

- Escreva uma frase, com um único verbo principal, coerente com a pergunta de pesquisa;
- o objeto do objetivo é a **acessibilidade da plataforma**, e não "desenvolver um sistema";
- estrutura para você completar:

> "O objetivo principal do presente trabalho consiste em avaliar e aprimorar a acessibilidade da plataforma web TiParaElas segundo [...] e o [...], identificando [...] e verificando [...] antes e depois das correções."

### 3.3 Referencial Teórico

Explique somente os conceitos que aparecem depois nos Resultados. Detalhes de instalação e uso das ferramentas vão para Materiais e Métodos. Estrutura sugerida:

```
2 REFERENCIAL TEÓRICO
2.1 Deficiência, inclusão e equidade na computação
2.2 Acessibilidade digital e tecnologias assistivas
2.3 Diretrizes e marco legal
2.4 Tecnologias web e acessibilidade
2.5 Métodos de avaliação de acessibilidade
2.6 Trabalhos relacionados
```

- **2.1 Deficiência, inclusão e equidade na computação:** pesquise sobre o modelo social da deficiência e o conceito de pessoa com deficiência e de barreira na LBI (arts. 2º e 3º). Fale sobre desenho universal, design inclusivo e a relação entre equidade de gênero e acessibilidade (por exemplo, o método GenderMag e o livro *Design Justice*). Seja breve: é a base do enquadramento, não o foco do trabalho.
- **2.2 Acessibilidade digital e tecnologias assistivas:** pesquise sobre a definição de acessibilidade na web, as barreiras enfrentadas por pessoas com deficiência visual, auditiva, motora e cognitiva e as tecnologias assistivas: leitores de tela (NVDA, VoiceOver, TalkBack), ampliadores, navegação por teclado e o VLibras. Fale sobre a relação entre acessibilidade e usabilidade (Petrie; Kheir, 2007).
- **2.3 Diretrizes e marco legal:** explique a estrutura da WCAG 2.2 (4 princípios, 13 diretrizes, critérios de sucesso e níveis A, AA e AAA), o que mudou em relação à 2.1 (nove critérios novos e a remoção do 4.1.1) e o eMAG 3.1 (seis seções: Marcação, Comportamento, Conteúdo/Informação, Apresentação/Design, Multimídia e Formulário). Fale sobre a LBI, o Decreto nº 5.296/2004 e a ABNT NBR 17225. Monte um **quadro de correspondência WCAG × eMAG** apenas com os critérios que aparecem nos Resultados.
- **2.4 Tecnologias web e acessibilidade:** pesquise sobre HTML semântico e regiões (*landmarks*), WAI-ARIA 1.2 e as regras de uso do ARIA (prefira sempre o elemento HTML nativo), os padrões do ARIA *Authoring Practices Guide* (menu de navegação e janela modal), o cálculo do nome acessível, a fórmula de contraste da WCAG e a acessibilidade de visualizações de dados (gráficos e mapas).
- **2.5 Métodos de avaliação de acessibilidade:** pesquise sobre ferramentas automáticas (como funcionam e suas limitações), inspeção por especialista e a metodologia WCAG-EM, testes com usuários de tecnologias assistivas e o efeito da experiência do avaliador nos resultados (Brajnik; Yesilada; Harper, 2010).
- **2.6 Trabalhos relacionados:** busque avaliações de acessibilidade de sítios, principalmente brasileiros. Termos de busca (use em português e em inglês):
  - `"avaliação de acessibilidade" AND "eMAG"`;
  - `"acessibilidade web" AND "ASES"`;
  - `"web accessibility evaluation" AND "automated tools" AND "manual"`;
  - `"WCAG 2.2" AND "conformance"`;
  - `"screen reader" AND "user study" AND "web"`;
  - `"accessible data visualization"`;
  - `"accessibility" AND "women in computing"`.

  Termine a seção com um quadro comparativo usando critérios como: tipo de sítio avaliado, diretriz e versão (WCAG ou eMAG), ferramentas usadas, inspeção manual, teste com tecnologia assistiva, teste com usuários, correções implementadas e reavaliação.

**Leituras de partida.** Localize a fonte original, confira os dados e só depois inclua nas Referências:

- W3C. *Web Content Accessibility Guidelines (WCAG) 2.2*, com os documentos *Understanding WCAG 2.2* e *Techniques for WCAG 2.2*;
- W3C. *Website Accessibility Conformance Evaluation Methodology (WCAG-EM) 1.0*;
- W3C. *WAI-ARIA 1.2*, *ARIA Authoring Practices Guide* e *Using ARIA*;
- BRASIL. *eMAG – Modelo de Acessibilidade em Governo Eletrônico*, versão 3.1;
- BRASIL. Lei nº 13.146/2015 (LBI), Decreto nº 5.296/2004 e Decreto nº 6.949/2009;
- ABNT NBR 17225 (acessibilidade em conteúdo e aplicações web);
- IBGE. PNAD Contínua: pessoas com deficiência (2022);
- LAZAR, J.; GOLDSTEIN, D.; TAYLOR, A. *Ensuring Digital Accessibility through Process and Policy* (2015);
- LAZAR, J.; FENG, J. H.; HOCHHEISER, H. *Research Methods in Human-Computer Interaction* (2. ed., 2017), especialmente o capítulo sobre pesquisa com pessoas com deficiência;
- YESILADA, Y.; HARPER, S. (ed.). *Web Accessibility: A Foundation for Research* (2. ed., 2019);
- VIGO, M.; BROWN, J.; CONWAY, V. *Benchmarking web accessibility evaluation tools: measuring the harm of sole reliance on automated tests* (W4A, 2013);
- POWER, C. *et al.* *Guidelines are only half of the picture: accessibility problems encountered by blind users on the web* (CHI, 2012);
- PETRIE, H.; KHEIR, O. *The relationship between accessibility and usability of websites* (CHI, 2007);
- BRAJNIK, G.; YESILADA, Y.; HARPER, S. *Testability and validity of WCAG 2.0: the expertise effect* (ASSETS, 2010);
- BURNETT, M. *et al.* *GenderMag: A Method for Evaluating Software's Gender Inclusiveness* (*Interacting with Computers*, 2016);
- COSTANZA-CHOCK, S. *Design Justice* (MIT Press, 2020);
- WebAIM. *The WebAIM Million* (relatório anual mais recente);
- documentação oficial do axe-core, do WAVE, do Lighthouse, do ASES, do NVDA e do Chart.js (seção de acessibilidade).

### 3.4 Metodologia

- **Classificação da pesquisa:** fale sobre a natureza aplicada, os objetivos exploratórios e descritivos e a abordagem quali-quantitativa (contagem de violações e de critérios atendidos e análise qualitativa das barreiras). Nos procedimentos, fale sobre a pesquisa bibliográfica e o **estudo de caso** com avaliação de conformidade antes e depois. Combine com o orientador a classificação final.
- **Pesquisa bibliográfica:** informe as bases consultadas, os termos de busca (seção 3.3), o período das publicações e os critérios de inclusão e exclusão.
- **Etapas:** descreva em ordem cronológica, com uma figura do fluxo. Elas seguem a WCAG-EM:
  1. revisão da literatura e do marco normativo;
  2. definição do escopo: WCAG 2.2 nível AA e eMAG 3.1, navegadores, tecnologias assistivas e versão avaliada (*tag* do commit);
  3. exploração da plataforma e seleção da amostra de páginas e de processos completos (seção 2.1);
  4. avaliação inicial em três frentes: (a) ferramentas automáticas; (b) inspeção manual critério a critério; (c) teclado, leitor de tela, ampliação de 200% e 400% e refluxo em 320px de largura;
  5. consolidação das barreiras: remoção de duplicidades e classificação por critério, severidade e método de detecção;
  6. correção incremental, por prioridade, com *issues* e *pull requests*;
  7. reavaliação com os mesmos procedimentos e, quando possível, as mesmas versões das ferramentas;
  8. teste com usuárias que usam tecnologias assistivas (somente se aprovado pelo CEP);
  9. análise antes e depois e extração das lições aprendidas.
- **Escala de severidade:** defina e justifique uma escala antes de avaliar. Por exemplo: crítica (impede concluir a tarefa), alta (dificulta muito), média e baixa.
- **Revisão da inspeção manual:** se possível, peça ao orientador ou a outra pessoa que revise uma parte das páginas avaliadas, para reduzir o viés de um único avaliador.
- **Teste com usuárias (se houver):**
  - descreva o perfil das participantes, sem identificá-las;
  - informe o recrutamento, as tarefas (as mesmas dos processos da amostra), o protocolo (pensar em voz alta, remoto ou presencial), as métricas e a aprovação no CEP;
  - com poucas participantes, trate os resultados como qualitativos e formativos;
  - prefira que as participantes usem o próprio dispositivo e a própria tecnologia assistiva, já configurados.
- **Ameaças à validade:** o artigo precisa de uma subseção sobre isso. Fale sobre:
  - o caso único e a amostra de páginas, que limitam a generalização;
  - a mesma pessoa avaliando e corrigindo, o que pode gerar viés;
  - a subjetividade da inspeção manual;
  - a mudança de versão das ferramentas e das bibliotecas entre as avaliações;
  - os dados fictícios, que podem ser diferentes do conteúdo real;
  - o número pequeno de usuárias (se houver teste);
  - o fato de parte das barreiras já ser conhecida antes da avaliação (seção 2.2). Seja transparente sobre isso.

### 3.5 Materiais e Métodos

**Materiais.** Monte o quadro-resumo com as versões **efetivamente usadas**, registradas no dia de cada avaliação:

| Ferramenta | Versão | Finalidade no trabalho |
|---|---|---|
| Python / Django | 3.11 / 5.1.3 | Plataforma avaliada e corrigida (*templates*, modelos e formulários) |
| Chart.js | a fixar (item 18) | Gráficos da página de Transparência |
| axe DevTools (axe-core) | registrar | Avaliação automática (regras WCAG 2.2 A e AA) |
| WAVE | registrar | Avaliação automática e visualização de estrutura e contraste |
| Lighthouse | registrar | Avaliação automática (usa o axe-core internamente) |
| ASES | registrar | Avaliação segundo o eMAG 3.1 |
| W3C Nu HTML Checker | – | Validação do HTML |
| WebAIM Contrast Checker ou Colour Contrast Analyser | – | Medição de contraste |
| NVDA | registrar | Leitor de tela no computador |
| TalkBack ou VoiceOver | registrar | Leitor de tela no celular |
| Google Chrome e Mozilla Firefox | registrar | Navegadores da avaliação |
| pa11y-ci ou axe-core com Playwright | registrar | Testes automatizados no CI (item 30) |
| Git e GitHub | – | Versionamento, *issues* e *pull requests* |
| Planilha eletrônica | – | Registro e consolidação das barreiras |

**Métodos.** Para cada item, explique o que é, para que foi usado e por que foi escolhido:

- **configuração das ferramentas:** conjunto de regras do axe (etiquetas `wcag2a`, `wcag2aa`, `wcag21a`, `wcag21aa` e `wcag22aa`), modo e dispositivo do Lighthouse (celular ou computador) e forma de envio ao ASES (URL pública ou código-fonte da página renderizada, no caso do ambiente local);
- **inspeção manual:** roteiro por critério de sucesso, com o que foi verificado em cada um;
- **teste com tecnologias assistivas:** versão e configuração do leitor de tela (voz em português, navegador usado), roteiro de teclado (Tab, Shift+Tab, Enter, Espaço, Esc e setas) e procedimento de ampliação e refluxo;
- **correções:** como foram implementadas (bases de *templates*, variáveis de cor no CSS, JavaScript, modelos com migração) e como foram verificadas;
- **testes automatizados e CI;**
- **teste com usuárias (se houver):** roteiro de tarefas, instrumentos e forma de análise.

> **Dica para o artigo:** os revisores valorizam o "por que X e não Y". Quando houver alternativas **de fato consideradas**, explique a escolha. Por exemplo: `<dialog>` nativo *versus* janela modal feita à mão; tabela de dados *versus* mapa interativo acessível por teclado. Não invente comparações.

### 3.6 Resultados (e Discussão)

Organize o capítulo pelas questões de pesquisa, e não por telas. Estrutura sugerida:

- **Caracterização da amostra:** quadro com as páginas e os processos avaliados e o ambiente de avaliação.
- **Conformidade inicial (QP1):**
  - tabela de critérios × páginas (satisfeito, não satisfeito ou não se aplica);
  - barreiras por princípio (perceptível, operável, compreensível e robusto) e por nível;
  - resultados de cada ferramenta, incluindo o percentual do ASES;
  - exemplos das barreiras mais graves, com captura de tela e trecho de código curto (por exemplo, o gráfico sem alternativa textual e o foco invisível).
- **Comparação entre métodos (QP2):**
  - tabela ou diagrama com as barreiras detectadas por cada método e as sobreposições;
  - exemplos de barreiras encontradas **só** manualmente (candidatas: o `aria-expanded` que nunca muda, os contadores que começam em "0", o foco que não entra no *lightbox*);
  - discussão à luz de Vigo, Brown e Conway (2013).
- **Correções (QP3):**
  - quadro com as colunas *Barreira*, *Critério*, *Correção* e *Commit*;
  - os padrões reutilizáveis que surgiram: link para pular o menu e `<main>` na base, foco visível global, componente de campo de formulário acessível, tabela alternativa para gráficos e mapas, campo de texto alternativo com orientação às autoras do conteúdo.
- **Antes e depois:** tabela e gráfico com as métricas da seção 2.2 e o que continuou pendente, com a justificativa (por exemplo, conteúdo de terceiros, como o YouTube).
- **Teste com usuárias (se houver):** resultados por tarefa e problemas relatados que não aparecem nas diretrizes, em comparação com Power *et al.* (2012).
- **Discussão:**
  - acessibilidade "incidental" *versus* planejada;
  - o papel de quem cadastra o conteúdo;
  - a transparência de dados só é real se os dados forem acessíveis;
  - a relação com o enquadramento de equidade;
  - as limitações.

Cuidados:

- só afirme conformidade total se **todas** as páginas e processos da amostra atenderem a todos os critérios do nível. Caso contrário, fale em conformidade parcial e diga quais critérios faltam;
- use dados fictícios nas capturas. A página de Transparência mostra nomes de pessoas: anonimize-os nas figuras.

### 3.7 Conclusão

- Responda **diretamente** à pergunta de pesquisa e a cada QP;
- comente cada objetivo específico;
- retome as principais contribuições e lições aprendidas;
- apresente as limitações com honestidade: caso único, amostra, avaliadora única e pendências não corrigidas;
- sugira trabalhos futuros, por exemplo:
  - avaliação contínua no CI;
  - testes com mais usuárias e com outros tipos de deficiência (pessoas surdas usuárias de Libras, deficiências cognitivas);
  - formação da equipe em acessibilidade;
  - combinação da avaliação de acessibilidade com a de inclusão de gênero (GenderMag).

### 3.8 Objetivos específicos

Serão entregues no final, junto com o Resumo, para refletirem o que foi **realmente feito**. Siga as regras das orientações gerais: 3 a 5 itens, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Verbos e temas que combinam com este trabalho:

- **revisar** a literatura e o marco normativo sobre ...;
- **avaliar** a conformidade inicial ... segundo ... por meio de ...;
- **identificar** e **classificar** as barreiras ...;
- **implementar** correções ...;
- **reavaliar** e **comparar** ... antes e depois ...;
- **avaliar** ... com usuárias de tecnologias assistivas (somente se o teste for realizado).

Não transforme correções pontuais em objetivos (por exemplo, "adicionar um link para pular o menu").

### 3.9 Resumo e *Abstract*

- **Tamanho:** no TCC, parágrafo único com 150 a 500 palavras (NBR 6028:2021). No artigo, siga o limite da chamada. Os veículos da seção 1.4 exigem resumo em português e em inglês, e os internacionais só em inglês.
- **Sequência:** contexto (acessibilidade e equidade), problema, objetivo, método (estudo de caso com WCAG-EM, ferramentas, inspeção e tecnologias assistivas), principais resultados **com números** (barreiras encontradas, critérios atendidos antes e depois) e principal conclusão.
- **Palavras-chave possíveis:** acessibilidade web; WCAG 2.2; eMAG; avaliação de acessibilidade; tecnologias assistivas; mulheres na computação.

### 3.10 Do TCC ao artigo

- **Estrutura típica de um estudo de avaliação:** Introdução; Fundamentação e trabalhos relacionados; Contexto (a plataforma); Método; Resultados da avaliação; Correções e reavaliação; Discussão e lições aprendidas; Ameaças à validade; Conclusão.
- **O artigo também precisa ser acessível:** figuras com texto alternativo, contraste adequado, tabelas reais (não imagens) e PDF com marcação. Eventos da área costumam exigir isso, e um artigo sobre acessibilidade inacessível perde credibilidade.
- **Modelo:** use o exigido pela chamada (em geral, o modelo da SBC, também disponível no Overleaf).
- **Revisão às cegas:** se for o caso, retire da versão submetida os nomes, a instituição e o nome da plataforma.
- **Material suplementar:** o repositório é privado. Para permitir a reprodução, combine com a equipe e com o orientador a publicação de um pacote com a planilha de barreiras, os relatórios das ferramentas e os roteiros de avaliação, sem dados pessoais.
- **Autoria:** defina a autoria do artigo (estudante, orientador e, se for o caso, demais integrantes, como o responsável pela página de Transparência) antes da submissão.
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

**Alinhamento sugerido das implementações.** É uma recomendação; os prazos oficiais são os da tabela acima. Os Resultados dependem da avaliação e das correções:

| Até | O que deve estar pronto | Por quê |
|---|---|---|
| 18/09/2026 | Decisão sobre o teste com usuárias (item 31) e, se for feito, projeto submetido ao CEP; escopo, amostra e versão avaliada definidos, com *tag* (seção 2.1); *issues* criadas | A linha de base precisa existir antes de qualquer correção, e o CEP leva tempo |
| 02/10/2026 | Avaliação inicial concluída (ferramentas, inspeção manual, teclado, leitor de tela e ampliação) e planilha consolidada (item 29) | A Metodologia (05/10) descreve um procedimento já executado |
| 09/10/2026 | Prioridade 1 corrigida (itens 1 a 12) | As correções do layout global afetam todas as páginas e mudam os números das demais |
| 19/10/2026 | Prioridades 2 e 3 corrigidas (itens 13 a 32), reavaliação feita com os mesmos procedimentos e métricas "depois" coletadas | Sobra uma semana para escrever os Resultados com os dados fechados |

> **Sobre o teste com usuárias:** pelo calendário, é pouco provável que o parecer do CEP saia a tempo dos Resultados do TCC (26/10/2026). Combine com o orientador uma das opções: (a) apresentar o TCC com a avaliação por especialista e por tecnologias assistivas, deixando o teste com usuárias como segunda fase, incluída na versão do artigo; ou (b) submeter ao CEP imediatamente e incluir o teste só se o parecer sair até o início de outubro. **Não realize testes com pessoas sem a aprovação necessária.**

Antes de cada envio, use o [checklist das orientações gerais](../../README.md#checklist-antes-de-enviar-uma-versão-ao-orientador).
