# Plano de escrita do artigo – Kelly (Tecnologia em Sistemas para Internet)

**Projeto pai:** iFIC – Desenvolvimento de Funcionalidades de Autenticação, Administração e Gerenciamento de Cursos de Formação Inicial e Continuada (ver `.llm/ific/projeto.md`).

**Temática:** S7 – Busca de cursos: comparação entre a busca textual do MySQL e uma camada de busca dedicada (ver `.llm/ific/tematicas.md`).

**Plano de desenvolvimento correspondente:** `01_kelly_ific_tarefas_desenvolvimento.md`.

**Base de estilo e normas:** o arquivo `README.md` deste repositório. Tudo o que está lá vale aqui. Este documento **não repete** as regras da ABNT já descritas no `README.md`; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copie estas frases para o artigo. Elas dizem o **assunto** de cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você leu.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do artigo será **criado e compartilhado pelo coordenador em uma pasta do Google Drive**. Você não cria arquivo novo nem trabalha em cópia local.

- **Escreva sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico de revisões do Drive é o que permite ao orientador ver o que mudou de uma semana para a outra.
- **Não crie cópias** ("Artigo v2", "Artigo final", "Artigo final revisado"). Cópia paralela é a forma mais rápida de perder trabalho. O Drive já guarda as versões em **Arquivo → Histórico de versões**.
- **Marque as entregas no histórico.** Ao terminar uma seção, use **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 29/09`.
- **Avise por mensagem quando entregar.** O orientador não fica olhando o documento; ele precisa saber que há algo novo para ler.
- **Comentários se resolvem, não se apagam.** Responda a cada comentário e só então marque como resolvido.
- **Figuras e tabelas** vão dentro do documento, no lugar certo, com a identificação em cima e a fonte embaixo. Não mande imagem em anexo separado.
- **Mantenha uma seção "Referências" desde o primeiro dia**, no fim do documento, e acrescente cada obra assim que ler. Deixar para o fim garante referência faltando.

---

## Cronograma de entregas

Data de referência: **22/09/2026**.

| # | Entrega | Prazo |
|---|---|---|
| 1 | Introdução e Objetivo Geral | **29/09/2026** |
| 2 | Referencial Teórico | **13/10/2026** |
| 3 | Metodologia | **20/10/2026** |
| 4 | Materiais e Métodos | **27/10/2026** |
| 5 | Resultados | **10/11/2026** |
| 6 | Conclusão | **17/11/2026** |
| 7 | Resumo, Objetivos Específicos e Título | **24/11/2026** |

### Como a escrita conversa com o desenvolvimento

| Semana | Sprint de desenvolvimento | Entrega de escrita |
|---|---|---|
| 22/09 a 28/09 | Sprint 1 – ambiente e MySQL | Introdução e Objetivo Geral (29/09) |
| 29/09 a 12/10 | Sprints 2 e 3 – catálogo, Busca 1 e coleção de teste | Referencial Teórico (13/10) |
| 13/10 a 19/10 | Sprint 4 – Busca 2 (`FULLTEXT` do MySQL) | Metodologia (20/10) |
| 20/10 a 26/10 | Sprint 5 – Busca 3 com radical das palavras | Materiais e Métodos (27/10) |
| 27/10 a 09/11 | Sprints 6 e 7 – correção, sinônimos e tempo | Resultados (10/11) |
| 10/11 a 16/11 | Sprint 8 – análise de erros e gráficos | Conclusão (17/11) |
| 17/11 a 23/11 | — | Resumo, Objetivos Específicos e Título (24/11) |

**Repare em duas coisas que o cronograma faz de propósito:**

1. **A Metodologia vence antes de você ter todos os resultados.** Isso é normal. Escreva no tempo futuro ("serão comparadas três abordagens...") e converta para o passado na revisão final;
2. **O Referencial vence logo depois da Sprint 3**, que é quando você estará programando as notas P@5, revocação e MRR. **Isso é de propósito**: escreva a seção que define essas notas na mesma semana em que estiver programando-as. Sai muito mais fácil, porque você estará pensando nas duas coisas ao mesmo tempo.

**Vá preenchendo as tabelas de Resultados a cada sprint que fecha.** Quem deixa os Resultados para a última semana não entrega.

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Um texto pela metade dá para comentar; um texto que não chega, não.
- Toda entrega é: seção escrita + versão nomeada no histórico + aviso ao orientador.
- Resolva **todos** os comentários da entrega anterior antes de avisar sobre a próxima.

---

## Que tipo de artigo é este

Escreva no formato de **artigo científico**, de 8 a 10 páginas, no modelo do evento ou periódico de destino. **Confirme com o orientador qual é o destino antes de começar** — dele vêm o modelo, o limite de páginas e o idioma.

O seu trabalho tem duas vantagens que nem todo TCC tem:

1. **Ele produz números.** Não é "eu achei a Busca 3 melhor", é "a Busca 3 obteve P@5 de 0,68 contra 0,31 da Busca 1, nas mesmas 30 consultas";
2. **Ele mede o banco que o projeto usa de verdade.** Como o experimento roda sobre **MySQL**, que é o SGBD do iFIC, a conclusão é diretamente aplicável à plataforma — não é uma aproximação que alguém teria de confirmar depois. Diga isso na Introdução e retome na Conclusão: é o que faz o trabalho ser útil, e não apenas correto.

Para aproveitar essas vantagens:

- **Trate o trabalho como uma comparação medida, não como um relato de programação.** O leitor não quer saber que você "fez um buscador"; quer saber **qual abordagem encontra melhor os cursos, em que tipo de consulta e a que custo**;
- **Faça perguntas de pesquisa explícitas** (Seção 5.2) e responda uma a uma nos Resultados e na Conclusão;
- **Descreva o método com detalhe suficiente para outra pessoa repetir**: o catálogo, as consultas, o gabarito, o critério de relevância e como cada busca foi feita;
- **Mostre também o que não funcionou.** Todo trabalho que só mostra o lado bom levanta suspeita.

Estrutura sugerida das seções:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Recuperação da informação
2.2 Índice invertido e preparação do texto
2.3 Busca textual em bancos de dados relacionais
2.4 Recursos de uma camada de busca dedicada
2.5 Como se avalia um sistema de busca
2.6 Trabalhos relacionados
3 METODOLOGIA
3.1 Classificação da pesquisa
3.2 Perguntas de pesquisa
3.3 Desenho da comparação
3.4 Construção da coleção de teste
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
6 CONCLUSÃO
REFERÊNCIAS
```

---

# 1. Introdução
**Prazo: 29/09/2026**

Cinco blocos de parágrafos, nesta ordem (é a sequência definida no `README.md`). Uma a duas páginas no total.

## 1.1 Contextualização (1 a 2 parágrafos)

**Pesquise sobre:**

- os **Cursos de Formação Inicial e Continuada (FIC)** e o papel da Rede Federal na qualificação profissional. Fontes: Lei nº 11.892/2008, Guia Pronatec de Cursos FIC, Plataforma Nilo Peçanha, portal do IFRN. **Procure um número** (quantidade de cursos, de vagas ou de concluintes) para usar no texto — número concreto vale mais que adjetivo;
- o **perfil do candidato** a um curso FIC: público amplo, com escolaridade e familiaridade digital variadas, que muitas vezes acessa pelo celular. Procure dados de inclusão digital no Brasil (pesquisa TIC Domicílios, do Cetic.br, e a PNAD Contínua TIC, do IBGE);
- **busca como principal forma de navegação** em catálogos grandes. Procure por "*information seeking behavior*" e "*search vs. browse*". A ideia a fundamentar: quando o catálogo tem centenas de itens, a pessoa não navega por categorias, ela digita.

**Escreva sobre:** a oferta de cursos FIC pelo IFRN e o papel do iFIC como plataforma de divulgação. Depois estreite para o ponto: um catálogo com centenas de cursos só é realmente acessível se a pessoa **conseguir encontrar** o curso que procura. Feche assim: a busca não é um detalhe de interface, é a **porta de entrada** — um curso que existe mas não é encontrado é, para o candidato, um curso que não existe.

Essa ligação entre **qualidade da busca e acesso à qualificação profissional** é o que faz o seu trabalho ser mais do que um exercício técnico. Ela conversa direto com o objetivo social do projeto iFIC. Use-a aqui e retome na Conclusão.

## 1.2 Problemática (1 a 2 parágrafos)

**Pesquise sobre:**

- as **limitações da busca com `LIKE`**: não há noção de relevância, não há separação em palavras, não há tratamento de variações da palavra, e o banco precisa ler todas as linhas, porque o índice comum não serve quando o texto procurado pode estar no meio do campo (procure por "*full table scan*" e "*leading wildcard*");
- o **vocabulário do usuário contra o vocabulário do catálogo** — é o coração do seu problema. Procure por "*vocabulary mismatch*" e pelo trabalho clássico de Furnas e colegas sobre o problema do vocabulário. A ideia: a pessoa digita "faxina" e o catálogo diz "Serviços domésticos"; digita "computador" e o catálogo diz "Informática básica";
- **erros de digitação em buscas**: são frequentes, e mais ainda em teclado de celular. Procure por "*spelling errors in search queries*".

**Escreva sobre:** o problema concreto, **usando os exemplos que você anotou no diário da Sprint 2**. Exemplo do seu próprio catálogo convence muito mais do que exemplo genérico. A busca simples falha de quatro maneiras, e vale nomear cada uma:

1. **não ordena por relevância** — o curso que tem o termo no título aparece depois de outro que o cita de passagem;
2. **não trata consulta de várias palavras** — "básica informática" não encontra "Informática básica";
3. **não tolera erro de digitação** — "exel" devolve tela vazia;
4. **não conhece o vocabulário do usuário** — "faxina" não chega a "Serviços domésticos".

Explique a consequência: **tela vazia**. E tela vazia, para quem está tentando se inscrever, não é um erro técnico — é uma desistência. Esse é o custo real do problema.

**Faça então a ponte para o que ainda não se sabe**, que é o que justifica pesquisar: existem duas famílias de solução — usar os recursos de busca textual do **próprio banco de dados** ou construir uma **camada de busca separada** —, e a escolha entre elas costuma ser feita por preferência da equipe, não por medição. Há pouca avaliação publicada que compare as duas **sobre o mesmo catálogo, com as mesmas consultas e medindo a qualidade dos resultados**, ainda menos em português. É essa lacuna que o seu trabalho preenche.

**Evite:** dizer que "a busca do iFIC é ruim". Você não mediu o iFIC em funcionamento, e o seu objeto é um protótipo. Fale do problema como um fenômeno conhecido da literatura, aplicado a um cenário representativo.

## 1.3 Caminho para a solução (1 a 2 parágrafos)

**Pesquise sobre:**

- o **índice invertido**, a estrutura por trás de qualquer busca textual séria, e como ele difere de ler a tabela inteira;
- os recursos de **busca textual dos bancos relacionais**: o `FULLTEXT` com `MATCH ... AGAINST` do MySQL — que é o que você vai usar — e, para dar panorama, o `tsvector` do PostgreSQL e o FTS5 do SQLite. Citar os três mostra que o suporte varia bastante entre bancos, o que reforça a sua pergunta;
- o que uma **camada de busca dedicada** oferece a mais: redução da palavra ao radical, sinônimos, tolerância a erro de digitação, ordenação configurável;
- os recursos de **linguagem** de que uma busca em português precisa: remoção de acentos, palavras vazias, *stemming*, sinônimos.

**Escreva sobre:** o leque de alternativas, mostrando que há um **gradiente**: começa no que já existe no banco e não custa nada (`LIKE`), passa pelo que o banco oferece sem componente novo (`FULLTEXT`) e chega ao que resolve mais problemas ao preço de uma camada a mais para construir e manter.

Justifique o recorte: avaliar **três abordagens**, sobre o **mesmo catálogo** e as **mesmas consultas**, medindo **qualidade** dos resultados e **custo** (tempo e espaço).

Deixe claro o que o trabalho **não** faz: não trata de busca semântica com modelos de linguagem nem de busca vetorial, porque exigem infraestrutura fora do alcance desta etapa. Isso fica como trabalho futuro. **Recorte declarado é recorte defendido.**

## 1.4 Apresentação da solução (1 a 2 parágrafos)

**Escreva sobre:** o que foi construído e como foi avaliado. Concretamente: um protótipo com o catálogo de cursos FIC armazenado em **MySQL** e **três formas de busca que convivem no mesmo sistema** — busca com `LIKE`, busca com o índice `FULLTEXT` do MySQL, e um buscador em Python com recursos de linguagem.

Explique **por que as três ao mesmo tempo**: porque assim respondem às mesmas consultas, sobre o mesmo catálogo, na mesma máquina, no mesmo dia. Essa é a decisão de método mais importante do trabalho e merece uma frase de destaque já aqui.

**Diga também, e com destaque, que o banco utilizado é o MySQL — o mesmo do iFIC.** Isso não é detalhe de implementação: é o que garante que o resultado seja diretamente aproveitável pela plataforma, em vez de precisar ser reconfirmado em outro banco.

Diga como foi avaliado: uma **coleção de teste** montada para o domínio, com 30 consultas distribuídas em seis categorias (termo exato, termo genérico, sem acento, erro de digitação, plural e sinônimo) e um **gabarito** com as respostas certas, elaborado **antes** de rodar as buscas; as notas **P@5, revocação e MRR**; e a medição do tempo de resposta e do espaço ocupado.

Registre que o catálogo parte de **fonte pública** (Guia Pronatec de Cursos FIC), que **não há nenhum dado pessoal** envolvido — conformidade com a LGPD (Lei nº 13.709/2018) — e que **não há participantes de pesquisa**: os julgamentos de relevância foram feitos pelo próprio autor, como parte da construção do instrumento de medida, o que dispensa submissão ao Comitê de Ética em Pesquisa.

## 1.5 Vínculo com o projeto e escopo (1 parágrafo)

**Escreva sobre:** o vínculo com o projeto de pesquisa iFIC, do IFRN, cuja etapa atual trata de autenticação, painel administrativo e gerenciamento de cursos FIC. Explique que o protótipo foi construído **de forma independente**, para avaliar as abordagens antes de decidir qual adotar na plataforma, e que a **incorporação ao iFIC é trabalho futuro**, fora do escopo deste artigo.

Feche a Introdução com um parágrafo curto dizendo como o texto está organizado.

---

# 2. Objetivo Geral
**Prazo: 29/09/2026 (junto com a Introdução)**

Uma **única frase**, com **uma única ação principal**, coerente com o título e com a conclusão. Modelo do `README.md`:

> "O objetivo principal do presente trabalho consiste no [ação] de [o quê] para [finalidade]."

**Direcionamentos:**

- o verbo principal **não** é "desenvolver". O protótipo é meio, não fim: o que o trabalho entrega é conhecimento medido sobre qual abordagem funciona melhor. Verbos adequados: **comparar**, **avaliar**, **analisar**;
- nomeie **o que** é comparado (as três abordagens de busca) e **sobre o quê** (o catálogo de cursos FIC);
- nomeie **em que dimensão** a comparação é feita (qualidade dos resultados e tempo de resposta). Sem isso, "melhorar a busca" fica vago demais;
- **não** empilhe ações. "Desenvolver, comparar, avaliar e integrar" são quatro objetivos, não um;
- **não** prometa o que não vai medir.

**Teste antes de enviar:** leia o objetivo geral e depois a primeira frase da sua Conclusão. Se as duas não estiverem falando exatamente da mesma coisa, uma das duas está errada.

---

# 3. Objetivos Específicos
**Prazo: 24/11/2026 (com o Resumo e o Título)**

Ficam para o final de propósito: precisam descrever o que foi **realmente alcançado**. Até lá, trabalhe com uma versão provisória.

**Direcionamentos:**

- de 4 a 5 itens, verbo no infinitivo, minúscula no início, ponto e vírgula no fim de cada um e ponto no último;
- na **mesma ordem** das etapas da Metodologia e das subseções dos Resultados;
- cada um **verificável**: na Conclusão você terá de mostrar, com número, que foi atingido;
- "instalar uma biblioteca" não é objetivo específico — é tarefa.

**Esqueleto do que cada item deve cobrir** (redija com as suas palavras ao fechar o texto):

1. revisar a literatura sobre recuperação da informação, busca textual em bancos de dados e avaliação de sistemas de busca;
2. construir um catálogo de cursos FIC em MySQL e implementar as três abordagens de busca sobre ele;
3. elaborar uma coleção de teste do domínio, com consultas categorizadas e gabarito documentado;
4. medir e comparar a qualidade dos resultados das três abordagens, por categoria de consulta;
5. analisar as falhas de cada abordagem e indicar em que situação cada uma é adequada.

---

# 4. Referencial Teórico
**Prazo: 13/10/2026**

**Explicação em vídeo (assista antes de começar):** https://youtu.be/8Qztq1Q5vb0

Comece a procurar referências **na primeira semana**. Neste trabalho o referencial não é enfeite: ele **define as notas** que você vai apresentar e **explica** por que cada busca acerta ou erra. Se você apresentar MRR nos Resultados sem ter definido antes, o texto trava.

**Você tem uma sorte que nem todo tema oferece:** recuperação da informação é uma área madura, com livros-texto consagrados. Procure as obras de Manning, Raghavan e Schütze (*Introduction to Information Retrieval*), de Baeza-Yates e Ribeiro-Neto (*Modern Information Retrieval*, com edição em português) e de Croft, Metzler e Strohman. **Com dois desses livros você cobre quase todo o seu referencial com fonte de primeira linha.** Comece por eles, não pelo Google.

Vá do geral para o específico e escreva **apenas sobre o que reaparece** na Metodologia ou nos Resultados. Meta: 6 a 8 páginas de leitura viram 3 a 4 páginas de texto.

## 4.1 Recuperação da informação

**Pesquise:** "recuperação da informação", "*information retrieval*", "*ranking*", "*relevance*", "*TF-IDF*", "*BM25*".

**Escreva:** o que é recuperação da informação e **como ela difere de uma consulta comum a banco de dados** — este é o parágrafo mais importante da subseção. Em um `SELECT ... WHERE` a resposta é exata e binária: a linha satisfaz ou não a condição. Em recuperação da informação a resposta é **ordenada por relevância**, aproximada, e o que interessa é o que está no topo.

É um bom lugar para uma observação que interessa ao seu trabalho: **um mesmo SGBD oferece os dois modos**. O `LIKE` responde do primeiro jeito; o `MATCH ... AGAINST` responde do segundo. Depois explique o que é uma **pontuação de relevância** e apresente o **TF-IDF** e o **BM25** — não precisa deduzir fórmula, precisa explicar a ideia: uma palavra rara que aparece muitas vezes em um documento curto pesa mais que uma palavra comum.

## 4.2 Índice invertido e preparação do texto

**Pesquise:** "*inverted index*", "*tokenization*", "*stop words*", "*stemming*", e para o português o algoritmo **RSLP** e o **Snowball**. Procure também "*edit distance*" e "**distância de Levenshtein**".

**Escreva:** o que é um **índice invertido** e por que ele permite buscar em milhares de documentos sem ler todos — compare explicitamente com o que o `LIKE '%termo%'` faz, que é ler todos. Depois, a cadeia de preparação do texto, na mesma ordem em que você programou:

- **tokenização** — separar o texto em palavras;
- **normalização** — minúsculas e remoção de acentos;
- **palavras vazias** (*stop words*) — por que "de", "para" e "curso" não ajudam a distinguir nada;
- **redução ao radical** (*stemming*) — por que "costureiras" e "costureiro" deveriam casar, e o que é preciso para que casem.

Termine com a **distância de Levenshtein**: a definição, um exemplo mínimo (de "exel" para "excel" é uma inserção) e por que os buscadores usam limites diferentes conforme o tamanho da palavra.

**Escreva esta subseção pensando na sua análise de erros:** cada conceito daqui vai ser usado lá para explicar uma falha. É o vocabulário do seu trabalho.

## 4.3 Busca textual em bancos de dados relacionais

**Esta subseção é o centro técnico do seu artigo.** Trate com cuidado.

**Pesquise:** a documentação do MySQL 8 sobre *full-text search* — índice `FULLTEXT`, `MATCH ... AGAINST`, modo de linguagem natural, modo booleano, `innodb_ft_min_token_size`, tabela de palavras vazias — e o conceito de **collation** (procure por "*accent-insensitive collation*"). Para dar panorama, veja também o `tsvector` do PostgreSQL e o FTS5 do SQLite.

**Escreva:** o que os bancos relacionais oferecem de busca textual e no que isso difere do `LIKE`: existe um índice invertido, existe separação em palavras e existe pontuação de relevância. Explique o `FULLTEXT` do MySQL — como o índice é construído, o que é o modo de linguagem natural e como a pontuação é obtida.

Trate também da **collation**, que é um recurso que o seu trabalho usa e que costuma passar despercebido: é a regra de comparação de texto do banco, e é ela que faz "informatica" casar com "informática" sem nenhum código adicional. Você mediu isso; fundamente aqui.

E então — **ponto central do trabalho** — o que o `FULLTEXT` do MySQL **não** oferece:

- **sem redução ao radical**: o índice guarda a palavra inteira, então "costureiras" não casa com "costureiro";
- **lista de palavras vazias em inglês**: "de", "para" e "com" são indexadas em um catálogo em português;
- **tamanho mínimo de palavra**: por padrão, palavras de 1 ou 2 letras não são indexadas;
- **sem tolerância a erro de digitação**: não há mecanismo equivalente à distância de edição.

**Formule isso de forma neutra e comparativa, não como reclamação.** O suporte a busca textual **varia entre SGBDs**, e o MySQL oferece menos recursos linguísticos que o PostgreSQL, por exemplo. Esse é um fato relevante para quem escolhe arquitetura, e é parte do seu resultado — dito assim, informa; dito como crítica, enfraquece o texto.

Acrescente, e isto conta a seu favor: as três primeiras limitações **exigem alteração na configuração do servidor**, que nem sempre está ao alcance da equipe de desenvolvimento. Isso é um argumento prático forte, e você viveu exatamente essa situação.

## 4.4 Recursos de uma camada de busca dedicada

**Pesquise:** o que ferramentas de busca oferecem além do banco — procure por "*search engine*", "*typo tolerance*", "*synonym expansion*", "*ranking rules*" — e cite as ferramentas do mercado (Elasticsearch, Solr, Meilisearch, Typesense), ainda que você não as tenha usado.

**Escreva:** o que caracteriza uma camada de busca separada do banco e quais recursos ela acrescenta — exatamente os três que faltam no `FULLTEXT` e que você implementou: radical das palavras, sinônimos e tolerância a erro de digitação. **Amarre esta subseção à anterior**: cada recurso apresentado aqui responde a uma limitação nomeada lá. Essa amarração é o que dá unidade ao seu referencial.

E, com o mesmo destaque, **o que essa camada custa**: o índice passa a viver **fora do banco**, o que cria um problema que antes não existia — **mantê-lo sincronizado** com os dados. Se um curso muda e o índice não é refeito, a busca passa a mentir, e sem dar erro nenhum. Apresente as formas usuais de tratar isso (refazer o índice a cada alteração, ou periodicamente). Essa subseção prepara uma das suas melhores discussões nos Resultados.

**Declare aqui, ou em Materiais e Métodos, uma limitação importante e honesta:** as ferramentas de busca do mercado rodam como serviço separado e não puderam ser instaladas no ambiente disponível. Por isso a camada dedicada foi **implementada em Python**, com bibliotecas que reproduzem os mesmos mecanismos. Dizer isso com clareza fortalece o texto; esconder, enfraquece.

## 4.5 Como se avalia um sistema de busca

**Esta é a subseção que sustenta a validade do trabalho inteiro.**

**Pesquise:** "*Cranfield paradigm*", "*test collection*", "*relevance judgments*", "*precision*", "*recall*", "*precision at k*", "*mean reciprocal rank*". Os livros-texto citados no começo desta seção cobrem tudo isso em um capítulo só.

**Escreva:** como se avalia um sistema de busca, começando pelo **paradigma de Cranfield** e suas três peças (a coleção de documentos, o conjunto de consultas e o gabarito de relevância). Depois **cada nota que você usou**, com a definição e o significado prático:

- **precisão** e **revocação**, e a tensão entre as duas;
- **P@5** — e por que ela é a nota mais adequada quando o usuário olha só a primeira tela;
- **MRR** — e o que ela captura que a precisão não captura: a **posição** do primeiro acerto.

Trate também das **limitações desse método**: o julgamento de relevância é subjetivo e depende de quem julga, e uma coleção pequena limita a generalização. Diga como isso se atenua — critério escrito e conferência por um segundo avaliador. Você fez as duas coisas; fundamentá-las aqui é o que permite afirmá-las na Metodologia.

## 4.6 Trabalhos relacionados

**Pesquise:** trabalhos que **comparem** formas de busca textual — banco relacional contra ferramenta de busca, avaliações de busca em catálogos e bibliotecas digitais, trabalhos brasileiros sobre busca em português. Onde procurar: SBC OpenLib (`sol.sbc.org.br`), BDTD, repositórios de institutos federais, Google Acadêmico, SciELO, ACM DL e IEEE Xplore. Termos úteis: "busca textual MySQL", "*MySQL full-text search*", "avaliação de sistema de busca", "*full-text search comparison*", "recuperação da informação em português".

**Escreva:** de **4 trabalhos**, um parágrafo cada, dizendo: o que foi comparado, **como foi avaliado** (esta é a informação que mais importa para você) e qual a limitação. Feche com um **quadro comparativo** entre eles e o seu trabalho, com colunas como: abordagens comparadas, SGBD utilizado, idioma, domínio, tamanho da coleção, número de consultas, existe gabarito documentado?, o que foi medido (só tempo? ou também qualidade?).

**Esse quadro é o argumento de originalidade do seu artigo.** Preste atenção a um ponto: é muito comum que trabalhos comparando busca em banco com ferramenta de busca meçam **apenas tempo de resposta**, e não a **qualidade dos resultados**. Se for esse o caso do que você encontrar, **diga isso explicitamente** — a sua contribuição passa a ser justamente medir a qualidade, com gabarito documentado, em português, em domínio educacional e sobre o MySQL.

## Regras que valem para o referencial inteiro

- **Toda afirmação técnica precisa de referência.**
- **Não empilhe citações.** Explique com as suas palavras e amarre ao seu trabalho.
- **Documentação oficial** (MySQL, Django, bibliotecas) serve para descrever a ferramenta, **não** para fundamentar conceito. Para conceito, use livro ou artigo.
- **Nada de blog, Stack Overflow ou site sem autoria** nas Referências. Você vai usar muito esse tipo de material para resolver problema de programação — isso é normal —, mas ele não entra.
- **Nunca cite uma referência que você não leu.** Ferramentas de IA inventam referências com naturalidade; se você não abriu o texto, ele não entra.
- Meta para este trabalho: **12 a 18 referências**.

---

# 5. Metodologia
**Prazo: 20/10/2026**

Como o trabalho foi conduzido. Verbos no passado e linguagem impessoal. Duas páginas.

**Pasta com metodologias prontas para consulta:** https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

## 5.1 Classificação da pesquisa

**Pesquise:** Gil (2017) e Prodanov e Freitas (2013) — referências completas no `README.md`. Leia os capítulos de classificação antes de escrever.

**Escreva:** a classificação pelos quatro critérios, **justificando cada uma** com uma frase que ligue o critério ao seu trabalho. Enquadramento mais provável:

- **Natureza:** aplicada — gera conhecimento para uma decisão concreta no iFIC, sobre o mesmo SGBD que a plataforma utiliza;
- **Objetivos:** explicativa — busca relacionar a abordagem de busca adotada à qualidade dos resultados;
- **Abordagem:** quantitativa — os resultados são notas numéricas, apoiadas por uma análise qualitativa dos erros;
- **Procedimentos:** **experimental**, combinada com pesquisa bibliográfica. Você muda uma coisa (a abordagem de busca), mantém tudo o mais igual (catálogo, consultas, gabarito, banco, máquina) e observa o efeito nas notas.

Aproveite para **dizer quais são as variáveis**: o que você mudou (a abordagem de busca e, dentro da terceira, cada recurso acrescentado), o que você mediu (P@5, revocação, MRR e tempo) e o que manteve fixo (catálogo, consultas, gabarito, limite de 20 resultados, servidor MySQL, máquina).

## 5.2 Perguntas de pesquisa

Enuncie **3 perguntas** objetivas, que os Resultados vão responder uma a uma. Sugestões (reescreva com as suas palavras):

- qual das três abordagens encontra melhor os cursos relevantes, medido por P@5, revocação e MRR?
- **em quais tipos de consulta** cada abordagem se mostra superior, e por quê? (esta é a pergunta mais interessante do trabalho — é ela que gera a figura por categoria);
- qual o custo de cada abordagem em tempo de resposta, espaço ocupado e esforço de manutenção?

Depois responda todas na Conclusão, **com recomendação explícita** para o iFIC. Trabalho aplicado que não recomenda nada desperdiça o próprio resultado.

## 5.3 Desenho da comparação

**Escreva:** a lógica das **três buscas convivendo no mesmo sistema**, com a justificativa — mesmo catálogo, mesmo servidor MySQL, mesmas consultas, mesma máquina, mesmo dia. Dedique um parágrafo a isso.

Descreva também as **padronizações** que tornam a comparação válida:

- o mesmo limite de 20 resultados nas três;
- a mesma forma de resposta (lista ordenada de códigos de curso), avaliada pelo mesmo script;
- as mesmas consultas, na mesma ordem;
- **o mesmo driver de acesso ao banco** nas três buscas, de modo que o custo de conexão incide igualmente sobre todas.

E explique a lógica de **acrescentar um recurso por vez** na terceira busca (primeiro o radical das palavras, depois a correção de digitação, depois os sinônimos), medindo cada versão separadamente. **Diga por que:** assim é possível atribuir o ganho a cada recurso isoladamente. Se tudo entrasse de uma vez, você saberia que melhorou, mas não saberia por causa de quê.

Uma **figura** com o desenho do experimento (o catálogo no MySQL, as consultas, as três buscas, o gabarito, o script de avaliação e as notas) ajuda muito o leitor. Use o draw.io.

## 5.4 Construção da coleção de teste

Subseção própria, porque a coleção **é** uma contribuição do trabalho. Descreva:

- **a origem do catálogo:** o Guia Pronatec de Cursos FIC como fonte pública, o número de cursos e **quantas ementas foram escritas pelo autor** (declare — é uma limitação, e declará-la fortalece o texto);
- **as consultas:** quantas, como foram elaboradas e o critério das seis categorias. Apresente a distribuição em um quadro e **justifique as categorias**: cada uma corresponde a um fenômeno que você explicou no Referencial (falta de relevância, acentuação, erro de digitação, variação da palavra, vocabulário diferente);
- **o gabarito:** como foi montado, **o critério escrito** que você seguiu, e o fato de ter sido feito **antes** de rodar as buscas — explicando por quê: para não construir um gabarito que favoreça a busca que você já viu funcionar. Descreva a conferência de 10 consultas pelo orientador e o resultado dessa comparação;
- **a declaração ética:** não há participantes de pesquisa; o julgamento de relevância faz parte da construção do instrumento de medida, feita pelo autor; não há dado pessoal no catálogo (LGPD); logo, não há submissão ao Comitê de Ética.

Termine descrevendo o **protocolo de medição**, e **justificando cada escolha**, não apenas declarando:

- as notas de qualidade foram calculadas uma vez, porque não variam entre execuções;
- o tempo foi medido 6 vezes por consulta, descartando a primeira (aquecimento, porque o MySQL mantém páginas de dados em memória e a primeira consulta é sempre a mais lenta) e usando a mediana (que não é distorcida por uma execução atípica);
- a máquina estava sem outros programas abertos durante as medições.

---

# 6. Materiais e Métodos
**Prazo: 27/10/2026**

Vale a analogia do `README.md`: **lista de ingredientes** mais **modo de preparo**. Aqui, esta seção é o que permite (ou impede) outra pessoa repetir o trabalho.

## 6.1 Materiais

Para **cada** item: **o que é** (uma ou duas frases), **para que foi usado** e **por que foi escolhido**.

| Ferramenta | O que dizer além da versão |
|---|---|
| Python 3.x | Linguagem do trabalho; alinhamento com a pilha do iFIC |
| MySQL 8 | SGBD do catálogo e base da Busca 2; **é o banco do projeto iFIC** |
| Índice `FULLTEXT` do MySQL | Recurso de busca textual avaliado: índice invertido e pontuação de relevância |
| `PyMySQL` | Driver de acesso ao banco; **justifique a escolha** (ver abaixo) |
| `rank_bm25` | Cálculo do BM25 na busca em Python |
| `snowballstemmer` | Redução das palavras ao radical, em português |
| `difflib` (padrão do Python) | Correção de erro de digitação por semelhança entre palavras |
| `matplotlib` | Gráficos |
| Django | Página web do protótipo |
| Git | Versionamento, em subpasta própria do repositório do projeto |

**Três justificativas são obrigatórias, e as três são técnicas:**

1. **Por que MySQL** (e não PostgreSQL, como previa a temática original): porque é o SGBD do projeto iFIC, e o trabalho existe para informar uma decisão desse projeto. **Este é um ponto forte, não uma concessão** — diga isso com clareza: medir sobre o banco que a plataforma realmente usa é o que torna o resultado aplicável sem reconfirmação. Acrescente a consequência técnica: o MySQL oferece menos recursos linguísticos que o PostgreSQL, o que **amplia** a distância esperada entre a busca do banco e a camada dedicada — e torna a comparação mais informativa para a equipe;

2. **Por que `PyMySQL`** e não `mysqlclient`: instalação sem compilação, o que importa em um ambiente onde não é possível instalar ferramentas de desenvolvimento. Declare que **as três buscas usam o mesmo driver**, de modo que essa escolha não favorece nenhuma delas;

3. **Por que uma camada de busca em Python**, e não uma ferramenta pronta (Elasticsearch, Meilisearch): as duas rodam como serviço separado e exigem instalação, o que o ambiente não permite. A camada em Python reproduz os mesmos mecanismos — índice invertido, BM25, radical das palavras, sinônimos e tolerância a erro de digitação — dentro do próprio processo. Declare o que isso custa em generalização: os números não se transferem diretamente para uma ferramenta de mercado. Isso vai também para as limitações e para os trabalhos futuros.

**Configuração do banco — sem isto o artigo não é reproduzível.** Informe a **collation** utilizada e o que ela implica para a acentuação, o valor de `innodb_ft_min_token_size`, a situação da lista de palavras vazias do servidor, e o mecanismo de armazenamento (InnoDB). Informe também processador, memória RAM, sistema operacional e versão, e o fato de banco e aplicação rodarem na mesma máquina.

Registre ainda, com honestidade, que **você não tinha permissão de administrar o servidor MySQL**, de modo que os parâmetros de configuração do índice de texto foram mantidos no padrão. Isso explica limitações que aparecem nos Resultados e é uma condição realista de muitos ambientes de produção — o que, aliás, reforça a validade prática do seu trabalho.

## 6.2 Métodos

**a) O catálogo.** Quantos cursos, de onde vieram, quais campos, quantas ementas são do guia e quantas foram escritas pelo autor. Uma figura com um exemplo de registro (um curso completo) ajuda o leitor a entender o que está sendo buscado.

**b) As três buscas.** Um parágrafo curto por busca, dizendo **exatamente** o que foi feito, com um trecho curto de código ou de SQL quando ele esclarecer:

- **Busca 1:** o filtro `LIKE` sobre nome e ementa, com ordenação alfabética;
- **Busca 2:** os dois índices `FULLTEXT` separados (um sobre o nome, outro sobre a ementa) e **por que foram separados** — só assim é possível combinar as duas pontuações com pesos diferentes, já que o `MATCH()` exige um índice exatamente sobre as colunas consultadas. Informe o modo utilizado (linguagem natural), a fórmula de combinação e **o peso escolhido para o nome, com o critério numérico da escolha**;
- **Busca 3:** a preparação do texto (tokenização, remoção de acentos, palavras vazias em português, radical com o algoritmo Snowball), a repetição do nome do curso para dar-lhe mais peso (**declare isso — é uma decisão de projeto**), o cálculo do BM25, a correção de digitação com o valor de corte utilizado e o critério das palavras curtas, e a lista de sinônimos (quantos e com que critério foram escolhidos).

Seja preciso. "As palavras foram reduzidas ao radical com o algoritmo Snowball para português" é informação reproduzível; "o texto foi tratado adequadamente" não é.

**c) Como as notas foram obtidas.** O script de avaliação: lê as consultas, chama cada busca, compara com o gabarito e calcula P@5, revocação e MRR, gravando uma linha por consulta. Diga que o detalhe por consulta foi preservado, e que é ele que permite a análise por categoria.

**d) Como o tempo e o espaço foram medidos.** Repetições, descarte do aquecimento, mediana e desvio; a medição separada do tempo de montagem do índice da Busca 3; o teste com o catálogo ampliado, deixando claro que **nele só se mediu tempo**, porque o gabarito não vale para um catálogo artificial; e a consulta ao `information_schema` para o espaço dos índices. **Se a medição de espaço não tiver sido confiável** — o MySQL guarda os índices `FULLTEXT` do InnoDB em tabelas internas auxiliares —, diga isso em vez de apresentar um número duvidoso.

---

# 7. Resultados e Discussão
**Prazo: 10/11/2026**

A seção mais importante. Três a quatro páginas. Organize respondendo às **perguntas de pesquisa**, na mesma ordem.

> **Regra sem exceção:** toda figura ou tabela é **anunciada no texto antes** de aparecer e **explicada depois**. Nada de duas figuras seguidas sem texto entre elas.

## 7.1 O catálogo e a coleção de teste

Curta e objetiva. Apresente os números do catálogo (cursos, ementas próprias e complementadas), o quadro de distribuição das 30 consultas por categoria, e uma captura da página de busca funcionando.

**Apresente também o resultado da conferência do gabarito com o orientador.** É um dado curto, e dá credibilidade a todos os números que vêm depois.

## 7.2 Qualidade geral das três buscas

A tabela principal: uma linha por busca, colunas com P@5, revocação e MRR, e a variação em relação à Busca 1. Vírgula como separador decimal e o mesmo número de casas decimais por coluna.

Acompanhe do gráfico de barras. **Discuta:** qual busca venceu em cada nota, e se alguma nota discorda das demais. Um caso interessante que pode acontecer: uma busca com **revocação alta e P@5 baixa** — ela encontra os cursos certos, mas não os coloca no topo. Se isso aparecer, explore: é a diferença entre **encontrar** e **ordenar**, e é exatamente o que separa o `LIKE` do `MATCH ... AGAINST`.

## 7.3 Qualidade por categoria de consulta

**Esta é a subseção central do artigo.** Tabela e gráfico de barras com o P@5 por categoria e por busca.

É aqui que o trabalho deixa de responder "qual é melhor" e passa a responder "**melhor para quê**". Discuta categoria por categoria:

- **termo exato:** provavelmente as três vão bem. **Diga isso.** Reconhecer onde a solução simples já basta é sinal de honestidade e é informação útil para quem vai decidir;
- **termo genérico:** aqui o `FULLTEXT` deve se separar do `LIKE`, porque passa a haver separação em palavras e ordenação por relevância;
- **sem acento:** explique o mecanismo — a collation do MySQL, que ignora acentos na comparação — e não apenas o número. É um resultado interessante justamente por ser um recurso que o banco oferece de graça e que quase ninguém menciona;
- **erro de digitação:** é onde a Busca 3 deve abrir a maior distância. Quantifique, e explique **por quê**: é a distância de edição, e o `FULLTEXT` do MySQL não oferece nada equivalente;
- **plural:** é o efeito do radical das palavras, e você mediu esse efeito isoladamente na Sprint 5. Mostre, e relacione com a ausência de *stemming* no MySQL;
- **sinônimo:** apresente **os dois números, com e sem a lista de sinônimos**, e discuta o que isso significa. O recurso não é mágico: depende de alguém montar e manter a lista, o que é **trabalho humano recorrente**. Esse custo escondido merece um parágrafo.

**Feche com a conclusão prática:** a diferença entre as abordagens **não é uniforme** — ela se concentra em categorias específicas. Portanto, a decisão de construir uma camada de busca deveria depender de **quanto** dessas consultas problemáticas o sistema realmente recebe. É uma afirmação forte, útil, e que nasce direto dos seus dados.

## 7.4 Tempo de resposta e espaço

Apresente a tabela de tempos (mediana e desvio, nos dois tamanhos de catálogo), o espaço ocupado pelos índices (ou a ressalva sobre a medição) e o tempo de montagem do índice da Busca 3.

Acompanhe do gráfico de tempo × tamanho do catálogo. **Discuta o crescimento**, que é o resultado mais bonito daqui: a Busca 1 obriga o MySQL a ler todas as linhas, porque o índice comum não serve quando o texto pode estar no meio do campo, e o tempo cresce junto com o catálogo; as Buscas 2 e 3 crescem bem menos, porque usam índice invertido. Ligue ao Referencial, que é onde o índice invertido foi explicado — resultado ligado à teoria vale o dobro.

**Não omita o outro lado.** Em um catálogo de poucas centenas de cursos, é bem possível que **as três respondam rápido o suficiente** para o usuário não perceber diferença. Se for o caso dos seus dados, **diga com todas as letras**: no porte atual do catálogo de cursos FIC, o tempo **não** é o critério de decisão — a qualidade dos resultados é. É uma conclusão contraintuitiva, sustentada por número, e é justamente o tipo de achado que dá valor a um artigo. Não a esconda por parecer "menos impressionante".

## 7.5 Análise das falhas

Apresente a tabela de erros: consulta, busca, o que foi devolvido e a causa, com a causa **nomeada em termos do Referencial** (ausência de ordenação por relevância, ausência de *stemming*, palavra abaixo do tamanho mínimo indexado pelo MySQL, palavra fora do vocabulário do catálogo, ausência de tolerância a erro de digitação).

Inclua obrigatoriamente **um caso em que a Busca 3 perdeu** — a correção de digitação trocando uma palavra por outra parecida e errada, por exemplo. Encontrar, mostrar e explicar um caso assim é o que impede o artigo de parecer propaganda da própria solução, e é o que um avaliador experiente procura.

Discuta também o **custo de manter o índice sincronizado**: a Busca 2 vive dentro do MySQL e é atualizada pelo próprio banco, junto com os dados, portanto nunca fica desatualizada; a Busca 3 monta o índice em memória e precisa refazê-lo quando o catálogo muda. Explique a consequência — se o índice não for refeito, a busca passa a mentir sem dar erro nenhum. **Este é o argumento mais forte a favor de ficar no banco**, e ele é invisível em qualquer comparação que meça só tempo e precisão.

## 7.6 Quadro-síntese

Um quadro final com uma linha por busca e colunas: qualidade geral, categorias em que se destaca, tempo, esforço de implementação, custo de manutenção e **recomendação de uso**.

**Este quadro é a contribuição prática do seu trabalho** — é o que a equipe do iFIC vai olhar para decidir. Se o artigo tiver uma única figura memorável, que seja esta. E não fuja da recomendação: diga, com base nos seus números, o que você faria no lugar da equipe, e sob que condição a resposta mudaria.

## 7.7 Limitações do trabalho

Subseção curta e honesta. Quatro pontos bastam:

- **o gabarito foi feito por uma pessoa**, que é também a autora do trabalho — atenuado pelo critério escrito, pelo julgamento feito antes de rodar as buscas e pela conferência de uma amostra pelo orientador;
- **o catálogo é de porte modesto e parte das ementas foi redigida pela autora**, o que limita a generalização;
- **as consultas foram elaboradas pela autora**, e não coletadas de uso real do sistema — esta é a limitação mais relevante, e vira trabalho futuro;
- **a camada de busca dedicada foi implementada em Python**, por restrição do ambiente, e os parâmetros de configuração do índice de texto do MySQL foram mantidos no padrão, porque não havia acesso de administração ao servidor. Os resultados precisam ser confirmados com uma ferramenta de busca de mercado e com o servidor ajustado.

Note que várias dessas limitações são atenuadas pelo fato de o estudo ser **comparativo**: a mesma limitação incide sobre as três buscas. Diga isso — é um bom argumento, desde que você não o use para varrer tudo para baixo do tapete.

---

# 8. Conclusão
**Prazo: 17/11/2026**

Curta e direta. Nada de resultado, conceito ou citação que não tenha aparecido antes.

**Escreva, nesta ordem:**

1. **Retomada do problema e do objetivo geral**, afirmando que foi alcançado **com o motivo e com número**: "[...] uma vez que a comparação das três abordagens, sobre um catálogo de X cursos e Y consultas, resultou em P@5 de A, B e C, respectivamente."

2. **Um comentário por objetivo específico**, na mesma ordem, cada um apontando o resultado que o comprova.

3. **Resposta direta às três perguntas de pesquisa.** Uma ou duas frases cada. É o fecho mais elegante que este artigo pode ter. E responda mesmo à terceira: **recomende** uma abordagem para o iFIC.

4. **Contribuições:** uma coleção de teste para busca de cursos FIC em português, com consultas categorizadas e gabarito documentado, que outros trabalhos podem reaproveitar; a comparação de três abordagens sobre o mesmo catálogo e sobre o mesmo SGBD utilizado pela plataforma, medindo qualidade e não apenas tempo; a análise das falhas por tipo de consulta; e um protótipo com código disponível. **Destaque que o experimento foi feito sobre MySQL**, o banco do iFIC — é o que permite aplicar a recomendação diretamente.

5. **Limitações e dificuldades:** retome brevemente as limitações e acrescente as dificuldades reais do desenvolvimento — montar o catálogo e o gabarito, as armadilhas encontradas (a necessidade de dois índices `FULLTEXT` separados para poder ponderar colunas, o uso de `HAVING` em vez de `WHERE`, o tamanho mínimo de palavra indexada, a lista de palavras vazias em inglês, o valor de corte da correção de digitação). É aqui que o `docs/diario.md` se paga.

6. **Trabalhos futuros**, concretos e ligados ao que você encontrou:
   - aplicar a abordagem recomendada ao catálogo público do iFIC (principal);
   - repetir a avaliação com o servidor MySQL ajustado — lista de palavras vazias em português e tamanho mínimo de palavra reduzido — para medir quanto dessas limitações é do banco e quanto é da configuração padrão;
   - comparar com uma ferramenta de busca de mercado, em ambiente que permita instalá-la;
   - repetir a avaliação com **consultas reais**, coletadas do uso do sistema depois de implantado — a limitação mais importante deste trabalho;
   - implementar e avaliar a sugestão "você quis dizer...?" e o preenchimento automático.

**Não escreva:** que "a Busca 3 é melhor" sem dizer em qual nota, sobre qual catálogo e em que tipo de consulta. E não generalize para "sistemas de busca" o que você mediu em um catálogo, em um idioma, em um SGBD e com 30 consultas escritas por você.

---

# 9. Resumo, Título e revisão final
**Prazo: 24/11/2026**

## 9.1 Resumo

Escrito **por último**, depois do texto aprovado. Parágrafo único, 150 a 500 palavras, impessoal, sem citações, sem siglas pouco conhecidas e sem menção a figuras ou tabelas (NBR 6028:2021).

Uma ou duas frases para cada item:

1. **contexto e problema:** o catálogo público de cursos FIC e a dificuldade de encontrar cursos com busca textual simples;
2. **objetivo:** o que o trabalho se propôs a comparar;
3. **método:** três abordagens de busca sobre MySQL, catálogo de N cursos, coleção de teste com M consultas categorizadas e gabarito de relevância;
4. **resultados:** os números principais — o P@5 de cada abordagem e a categoria em que a diferença foi maior;
5. **conclusão:** a recomendação que os números sustentam e o encaminhamento (aplicação ao iFIC como trabalho futuro).

**Coloque números no resumo.** Resumo sem número é resumo fraco — é o que faz o avaliador decidir se lê o resto.

O **Abstract** é a versão em inglês. Os termos técnicos têm forma consagrada em inglês (*information retrieval*, *full-text search*, *typo tolerance*, *precision at k*); use-as, e não a tradução literal. Não entregue tradução automática sem revisão.

**Palavras-chave** (3 a 5), separadas por ponto e vírgula. Campo semântico: recuperação da informação; busca textual; MySQL; avaliação de sistemas de busca; cursos de formação inicial e continuada. Escolha termos pelos quais alguém **procuraria** o seu trabalho.

## 9.2 Título

**Última coisa a ser definida**, em acordo com o orientador. Deve indicar **o que foi feito** e **em que contexto**, e ser coerente com o objetivo geral.

Pontos a cobrir: a ação (comparação ou avaliação comparativa), o objeto (abordagens de busca textual), a tecnologia (MySQL, se couber no tamanho) e o contexto (catálogo de cursos FIC / plataforma iFIC). Subtítulo separado por dois-pontos, se precisar. Evite títulos genéricos ("Sistema de busca de cursos") e evite prometer no título mais do que o artigo mede.

## 9.3 Revisão final — checklist

Além do checklist do `README.md`:

- [ ] O objetivo geral, os objetivos específicos, as perguntas de pesquisa, as subseções de Resultados e os parágrafos da Conclusão estão na mesma ordem e falando das mesmas coisas?
- [ ] Todos os números citados no Resumo, nos Resultados e na Conclusão são **exatamente** os mesmos? (Erro mais comum: refazer a medição e esquecer de atualizar o resumo.)
- [ ] Toda nota apresentada nos Resultados (P@5, revocação, MRR) foi definida no Referencial?
- [ ] Está escrito que o gabarito foi montado **antes** de rodar as buscas?
- [ ] A escolha do MySQL está justificada, e está dito que é o SGBD do projeto iFIC?
- [ ] A escolha de implementar a camada de busca em Python está justificada, com a restrição do ambiente declarada?
- [ ] A configuração do banco está informada (collation, tamanho mínimo de palavra indexada, palavras vazias, InnoDB)?
- [ ] Toda tabela e figura é citada no texto antes de aparecer e explicada depois?
- [ ] Todas as tabelas e figuras têm identificação em cima, centralizada, e fonte embaixo?
- [ ] Os gráficos informam unidade e, se o eixo não começa em zero, o aviso na legenda?
- [ ] O ambiente de execução está completo (processador, memória, sistema operacional, versões)?
- [ ] Há pelo menos um resultado em que a abordagem mais simples se mostrou suficiente, e um em que a mais completa falhou?
- [ ] As limitações estão declaradas?
- [ ] As siglas (FIC, IFRN, SGBD, LGPD, MRR, CEP) foram escritas por extenso na primeira vez que aparecem?
- [ ] A numeração das seções está sem ponto após o número?
- [ ] O texto está impessoal e no passado?
- [ ] Está declarado que não há dados pessoais e que não houve participantes de pesquisa?
- [ ] O link do repositório está no texto, e o orientador autorizou divulgar esse endereço?
- [ ] Todos os comentários do orientador foram respondidos e resolvidos?
- [ ] A versão final foi nomeada no histórico do Drive?

---

## Referências mínimas a garantir

- **2 obras de metodologia científica** — Gil (2017) e Prodanov e Freitas (2013), já no `README.md`;
- **2 livros-texto de recuperação da informação** — são a espinha dorsal do seu referencial e cobrem as Seções 4.1, 4.2 e 4.5;
- **2 fontes sobre preparação de texto e *stemming* em português** (Seção 4.2), incluindo o algoritmo Snowball ou o RSLP;
- **2 fontes sobre busca textual em bancos relacionais** (Seção 4.3), combinando a documentação oficial do MySQL e literatura de banco de dados;
- **1 a 2 fontes sobre ferramentas de busca** (Seção 4.4);
- **4 trabalhos relacionados** (Seção 4.6);
- **a legislação e as fontes institucionais** — Lei nº 13.709/2018 (LGPD), Lei nº 11.892/2008 e o Guia Pronatec de Cursos FIC;
- **a documentação oficial das ferramentas** — Python, MySQL e as bibliotecas utilizadas.

Registre a referência completa de **tudo** o que ler, na seção de Referências do documento do Drive, desde o primeiro dia. Zotero e Mendeley ajudam a montar, mas confira cada entrada contra a NBR 6023:2018 antes de entregar: esses gerenciadores erram com frequência.
