# Plano de escrita do artigo – Teófilo e dupla (Tecnologia em Sistemas para Internet)

**Projeto pai:** AgroAgreste – Observatório Territorial da Agricultura Familiar no Agreste do Rio Grande do Norte (ver [projeto.md](../projeto.md)).

**Temática:** S5 – Previsão da produção de mandioca com aprendizado de máquina a partir de dados climáticos (ver [tematicas.md](../tematicas.md)).

**Plano de desenvolvimento correspondente:** `01_teofilo_agro_tarefas_desenvolvimento.md`.

**Base de estilo e de normas ABNT:** o arquivo [README.md](../../../README.md) deste repositório. Tudo o que está lá vale aqui — estrutura, citações, referências, figuras, tabelas, formatação. Este documento **não repete** as regras da ABNT; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copiem estas frases para o artigo. Elas dizem sobre o que é cada parágrafo; o texto tem de ser escrito por vocês, com as suas palavras e com as referências que vocês leram.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do artigo será **criado e compartilhado pelo coordenador em uma pasta do Google Drive**. Vocês não criam arquivo novo nem trabalham em cópia local.

Como trabalhar nele:

- **Escrevam sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico do Drive é o que permite ao orientador ver o que mudou de uma semana para outra — e, no caso de vocês, **quem** escreveu o quê.
- **Não criem cópias** ("Artigo v2", "Artigo final", "Artigo final revisado"). É a forma mais rápida de perder trabalho, e em dupla o risco dobra. O Drive já guarda tudo em **Arquivo → Histórico de versões**.
- **Marquem cada entrega no histórico.** Ao terminar uma seção, usem **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 29/09`.
- **Avisem por mensagem quando entregar.** O orientador não fica olhando o documento; ele precisa saber que há algo novo.
- **Comentário se responde, não se apaga.** Respondam a cada comentário e só então marquem como resolvido.
- **Figuras e tabelas** vão dentro do documento, no lugar certo, com identificação em cima e fonte embaixo. Não mandem imagem em anexo separado.
- **Criem a seção "Referências" no primeiro dia** e acrescentem cada obra assim que lerem. Deixar para o fim garante referência faltando.
- **Não deem acesso a terceiros** sem falar com o coordenador.

### Como dois autores escrevem um texto só

Este é o ponto que costuma estragar artigo de dupla. O resultado típico de dois autores sem combinado é um texto em que dá para ver exatamente onde um parou e o outro começou. Três regras resolvem:

1. **Cada seção tem um redator principal.** A divisão está na tabela do cronograma, mais abaixo. Quem não é o redator **comenta, não reescreve** — use os comentários do Drive.
2. **Nunca escrevam a mesma seção ao mesmo tempo.** Mesmo com o Google Docs aguentando edição simultânea, dois textos crescendo no mesmo parágrafo viram remendo.
3. **Uma revisão de uniformização por entrega.** Antes de avisar o orientador, **um** dos dois (alternem a cada entrega) lê a seção inteira em voz alta e uniformiza: tempo verbal, pessoa do discurso, vocabulário. "Acurácia" e "precisão" não podem estar sendo usadas como sinônimo em um parágrafo e como coisas diferentes no seguinte.

E uma regra que vale para a apresentação: **os dois precisam poder defender o trabalho inteiro.** Quem escreveu a Metodologia tem de saber explicar os Resultados.

---

## Cronograma de entregas

Data de referência: **22/09/2026**.

| # | Entrega | Prazo | Redator principal |
|---|---|---|---|
| 1 | Introdução e Objetivo Geral | **29/09/2026** | Os dois (ver divisão abaixo) |
| 2 | Referencial Teórico | **13/10/2026** | Dividido por subseção |
| 3 | Metodologia | **20/10/2026** | Aluno A |
| 4 | Materiais e Métodos | **27/10/2026** | Aluno B |
| 5 | Resultados | **10/11/2026** | Os dois |
| 6 | Conclusão | **17/11/2026** | Aluno A, revisão do B |
| 7 | Resumo, Objetivos Específicos e Título | **24/11/2026** | Aluno B, revisão do A |

A divisão fina, para não haver dúvida:

| Trecho | Quem escreve |
|---|---|
| 1.1 Contextualização e 1.2 Problemática | Aluno A |
| 1.3 Caminho para a solução e 1.4 Apresentação da solução | Aluno B |
| 1.5 Vínculo com o projeto + Objetivo Geral | Os dois, juntos |
| 2.1 e 2.2 (agricultura familiar, mandioca, clima) | Aluno A |
| 2.3 e 2.4 (aprendizado de máquina, avaliação de modelos) | Aluno B |
| 2.5 Trabalhos relacionados | Os dois, metade cada |
| 4.x Resultados sobre a base de dados e o erro | Aluno A |
| 4.x Resultados sobre modelos e importância das variáveis | Aluno B |

### Como a escrita conversa com o desenvolvimento

| Semana | Sprint de desenvolvimento | Entrega de escrita |
|---|---|---|
| 22/09 a 28/09 | Sprint 1 – ambiente, municípios, APIs | Introdução e Objetivo Geral (29/09) |
| 29/09 a 12/10 | Sprints 2 e 3 – série da mandioca e série de clima | Referencial Teórico (13/10) |
| 13/10 a 19/10 | Sprint 4 – base de modelagem | Metodologia (20/10) |
| 20/10 a 26/10 | Sprint 5 – linha de base e validação temporal | Materiais e Métodos (27/10) |
| 27/10 a 09/11 | Sprints 6 e 7 – modelos, importância, análise de erro | Resultados (10/11) |
| 10/11 a 16/11 | Sprint 8 – reprodutibilidade, MySQL, recomendação | Conclusão (17/11) |
| 17/11 a 23/11 | — | Resumo, Objetivos e Título (24/11) |

**Um aviso sobre o cronograma.** A Metodologia vence em 20/10, quando vocês ainda não terão rodado um modelo sequer. E os Resultados vencem em 10/11, um dia depois da última sprint de análise. Isso é normal e tem solução:

- escrevam a Metodologia falando do **plano** ("serão treinados e comparados três modelos...") e depois passem tudo para o passado;
- **vão colando as figuras e as tabelas no documento a cada sprint**, mesmo sem o texto de análise pronto. Quem deixa os Resultados para a última semana não entrega;
- a tabela de métricas da Sprint 6 pode entrar no documento no dia em que for gerada, ainda incompleta, com as células faltando. Tabela no lugar é meia seção escrita.

### Regras de entrega

- Entreguem **no prazo, mesmo incompleto**. Texto pela metade dá para comentar; texto que não chega, não.
- Cada entrega é: seção escrita + revisão de uniformização feita + versão nomeada no histórico + aviso ao orientador.
- Resolvam **todos** os comentários da entrega anterior antes de avisar sobre a próxima.

---

## Que tipo de trabalho é este

Um **artigo científico** de 8 a 12 páginas, para um congresso ou uma revista. **Confirmem com o orientador qual é o destino antes de começar** — dele vêm o modelo de formatação e o limite de páginas. Como o tema cruza computação e agricultura, há duas famílias possíveis de destino (eventos de computação aplicada e informática na agricultura, ou eventos de agronomia, agrometeorologia e desenvolvimento regional), e a escolha muda o tom: no primeiro caso, o leitor quer detalhe do protocolo de avaliação; no segundo, quer interpretação agronômica dos resultados.

Cinco coisas fazem a diferença entre um relato e um artigo publicável — e a terceira é a que decide o valor deste trabalho:

1. **O objeto do trabalho não é o programa que vocês escreveram.** É a **pergunta respondida com medição**: o clima público explica o rendimento da mandioca no Agreste? O observatório AgroAgreste é o contexto que justifica a pergunta.
2. **O leitor quer saber quanto, não o quê.** Não interessa que vocês treinaram um Random Forest; interessa que o erro foi de X kg/ha, que isso é Y% do rendimento médio e que representa Z% de ganho (ou de perda) em relação a repetir o ano anterior.
3. **Sem linha de base não há resultado.** Um erro de 1.500 kg/ha não é bom nem ruim; é apenas um número. Só a comparação com a previsão ingênua lhe dá significado. **Toda métrica apresentada no artigo aparece ao lado da métrica da linha de base.** Se houver uma única regra a seguir neste documento, é esta.
4. **O método tem de dar para repetir.** Fontes, códigos de tabela do IBGE, parâmetros da NASA POWER, variáveis criadas, protocolo de separação treino/teste, versões das bibliotecas, máquina.
5. **Resultado negativo é resultado.** Se nenhum modelo bater a linha de base, o artigo não morre — ele muda de foco e fica, em alguns aspectos, mais interessante: passa a ser sobre **os limites de prever safra municipal com dados públicos de clima**. Literatura de previsão agrícola está cheia de trabalhos que só mostram o que deu certo, e é por isso que tanta gente perde tempo refazendo o que já se sabia que não funcionava. Escrevam isso com todas as letras na discussão.

Estrutura sugerida:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Agricultura familiar e a mandioca no Agreste potiguar
2.2 Clima, chuva e produtividade agrícola no semiárido
2.3 Aprendizado de máquina aplicado à previsão agrícola
2.4 Avaliação de modelos preditivos com dados temporais
2.5 Trabalhos relacionados
3 METODOLOGIA
3.1 Classificação da pesquisa
3.2 Área de estudo e período
3.3 Etapas do trabalho
4 MATERIAIS E MÉTODOS
4.1 Materiais
4.2 Métodos
5 RESULTADOS E DISCUSSÃO
6 CONCLUSÃO
REFERÊNCIAS
```

---

# 1. Introdução
**Prazo: 29/09/2026**

Cinco blocos de parágrafos, nesta ordem (é a sequência fixa do `README.md`). Duas a três páginas.

## 1.1 Contextualização (2 a 3 parágrafos) — Aluno A

**Pesquisem sobre:**

- **a agricultura familiar no Agreste do Rio Grande do Norte**: peso econômico e social, número de estabelecimentos familiares, principais culturas. O `projeto.md` já dá um ponto de partida, com a informação de que a mandioca abrange cerca de 85% do território potiguar e a referência de Cousteau e Silva (2013). Procurem números no **IBGE** — Produção Agrícola Municipal e Censo Agropecuário de 2017;
- **a mandioca**: por que ela é a cultura característica da agricultura familiar do semiárido. Procurem material da **Embrapa Mandioca e Fruticultura** sobre o ciclo da cultura, a resistência à seca, o uso alimentar e a produção de farinha. Interessam especialmente o **ciclo longo** (12 a 18 meses entre plantio e colheita) e a **tolerância ao déficit hídrico** — esses dois fatos vão reaparecer na discussão dos resultados;
- **o papel da informação no planejamento territorial**: por que estimar a safra antes da colheita ajuda gestores, cooperativas e programas públicos a se organizar.

**Escrevam sobre:** a importância da agricultura familiar no Agreste potiguar, o lugar da mandioca dentro dela, e a dependência direta que essa produção tem do regime de chuvas. Tragam **pelo menos dois dados numéricos** do IBGE — área plantada de mandioca na região, produção total, número de estabelecimentos familiares. Dado numérico dá peso imediato ao texto.

Apresentem então o projeto AgroAgreste como o observatório territorial que está sendo construído para reunir e organizar essas informações, e digam qual parte dele este trabalho atende: o **indicador de estimativa de produção**, previsto nos objetivos específicos do projeto.

## 1.2 Problemática (2 a 3 parágrafos) — Aluno A

**Pesquisem sobre:**

- a **variabilidade interanual da produção** no semiárido: quebras de safra, o impacto econômico sobre famílias que dependem de uma colheita por ciclo;
- o **atraso e a natureza dos dados oficiais**: a PAM do IBGE é anual e sai com meses de defasagem, e boa parte dos valores municipais é **estimada** por levantamento junto a técnicos locais, não medida. Procurem a documentação metodológica da própria PAM — citar a metodologia da fonte que vocês usam é sinal de rigor;
- as **secas do Nordeste**, em especial a de 2012 a 2017. Procurem o **Monitor de Secas** da ANA e trabalhos sobre impacto de seca na agricultura do semiárido;
- por que **prever antes da colheita** faz diferença: uma estimativa que chega junto com a safra não serve para decidir nada.

**Escrevam sobre:** o problema concreto, em duas camadas.

Primeiro, **o que falta hoje**: não existe, para os municípios do Agreste potiguar, nenhuma estimativa de safra disponível antes da publicação oficial do IBGE. Quem planeja ação no território trabalha olhando para trás. Sem isso, o observatório não tem como oferecer o indicador de estimativa de produção previsto no projeto.

Segundo, **por que a solução aparentemente óbvia não é óbvia**: os dados necessários existem, são públicos e são gratuitos há décadas — a série histórica de produção do IBGE e as séries climáticas globais da NASA. O que não existe é a **verificação** de que essas duas bases, cruzadas, sustentam uma previsão útil nesta região, nesta escala e para esta cultura. Há três obstáculos concretos, e vale enunciá-los: o dado municipal do IBGE é em parte estimado e tem pouca variação de um ano para outro; o ciclo da mandioca atravessa dois anos civis, o que desalinha a colheita da chuva que a produziu; e a mandioca é justamente uma das culturas mais tolerantes à seca, o que pode atenuar o sinal climático que se quer captar.

**Fechem enunciando a pergunta de pesquisa**, de forma direta: *é possível estimar o rendimento da mandioca dos municípios do Agreste potiguar a partir de dados climáticos públicos? E modelos de aprendizado de máquina superam uma previsão ingênua baseada apenas na série histórica?*

Desdobrem em três perguntas menores, que vão organizar o capítulo de Resultados:

- os modelos treinados com variáveis climáticas **superam a linha de base** de persistência?
- **quais variáveis climáticas** mais contribuem para a previsão, e em que janela do ciclo da cultura?
- o desempenho **se mantém nos anos extremos**, que são os que mais importam para o planejamento?

**Não escrevam** que "o AgroAgreste não tem indicadores". Ele está em construção — e esse é justamente o argumento: é o momento certo de verificar a técnica antes de a equipe implementá-la.

## 1.3 Caminho para a solução (1 a 2 parágrafos) — Aluno B

**Pesquisem sobre:**

- as formas de estimar safra: levantamento de campo e declaração de produtores (caros e lentos), modelos agronômicos de crescimento de cultura (exigem dados de solo e manejo que não existem por município), sensoriamento remoto (NDVI e afins) e **modelos estatísticos e de aprendizado de máquina sobre dados climáticos**;
- as **fontes gratuitas de dados climáticos**: NASA POWER, CHIRPS, INMET/BDMEP. Comparem cobertura espacial, resolução, período disponível e facilidade de acesso. Vale explicar por que a rede de estações do INMET, sozinha, não resolve: são poucas estações para muitos municípios;
- os **modelos** que serão usados: regressão linear, florestas aleatórias (*Random Forest*) e árvores com *gradient boosting*. Nesta seção basta uma frase sobre cada um; a explicação completa fica no Referencial.

**Escrevam sobre:** as alternativas, dizendo o que cada uma resolve e o que custa. Mostrem que a combinação de dados climáticos públicos com aprendizado de máquina se destaca por três razões: cobre **todos** os municípios (inclusive os que não têm estação meteorológica), é **retroativa** (dá para reconstruir e testar a previsão em vinte anos passados, o que nenhum levantamento de campo permite) e é **gratuita**.

Justifiquem então as escolhas do trabalho: a **NASA POWER**, pela cobertura completa e pelo acesso livre; o **rendimento (kg/ha)** como alvo em vez da produção total, porque isola melhor o efeito do clima da decisão de quanto plantar; e a comparação de **modelos de complexidade crescente contra uma linha de base**, que é o que permite dizer se a complexidade se pagou.

Digam também o que **não** foi feito e por quê: não foram usados dados de campo nem de solo, porque não existem nessa escala e porque coletá-los envolveria pessoas; não foram usados índices de vegetação por satélite, porque são objeto de outro trabalho do mesmo projeto (citem, se o orientador autorizar); e não foram usadas redes neurais, porque o volume de dados — cerca de mil observações — não as justifica. Recorte declarado é recorte defendido.

## 1.4 Apresentação da solução (2 parágrafos) — Aluno B

**Escrevam sobre:** o que foi construído, de forma concreta. Uma base de dados que reúne, para cada município do Agreste potiguar e cada ano do período estudado, o rendimento da mandioca registrado pelo IBGE e um conjunto de variáveis climáticas derivadas da série diária da NASA POWER — chuva acumulada em diferentes janelas do ciclo da cultura, maior sequência de dias secos, número de dias com chuva e temperaturas médias, tanto do ano da colheita quanto do anterior.

Destaquem a decisão de projeto que dá sentido ao trabalho: **as variáveis foram construídas respeitando o ciclo da mandioca**, que atravessa dois anos civis, e **todas usam apenas informação anterior ao ano previsto**. É isso que torna a previsão utilizável antes da colheita — e é isso que impede que o resultado seja artificialmente bom.

Digam **como os modelos foram avaliados**, que é o que sustenta o artigo:

- **validação temporal com janela expansiva**: o modelo treina apenas com anos anteriores e é testado em cada ano seguinte, um de cada vez, reproduzindo a situação real de uso;
- **três linhas de base** — repetir o rendimento do ano anterior, a média móvel de três anos e a média histórica do município — contra as quais todos os modelos são comparados;
- **três métricas de erro** (MAE, RMSE e MAPE) e o **ganho percentual** de cada modelo sobre a linha de base;
- **análise da importância das variáveis** por permutação, e do erro por ano e por município.

Registrem que **todos os dados são públicos e secundários**, de órgãos oficiais, e que **o trabalho não envolveu pessoas** — logo, não houve necessidade de submissão ao Comitê de Ética em Pesquisa.

## 1.5 Vínculo com o projeto e escopo (1 parágrafo) — os dois

**Escrevam sobre:** o vínculo com o projeto AgroAgreste, do IFRN, que está construindo um observatório territorial da agricultura familiar no Agreste potiguar. Expliquem que este trabalho foi desenvolvido **de forma independente**, como protótipo, para verificar a viabilidade da técnica antes de incorporá-la à plataforma.

Deixem claro que a **integração ao observatório é trabalho futuro**, fora do escopo deste artigo — ainda que a base final tenha sido preparada para carga em banco de dados, justamente pensando nessa integração. O que se entrega é **uma resposta fundamentada em medição** sobre adotar ou não a previsão.

Fechem a Introdução com um parágrafo curto dizendo como o texto está organizado.

---

# 2. Objetivo Geral
**Prazo: 29/09/2026 (junto com a Introdução)**

Uma **única frase**, com **uma única ação principal**. Modelo do `README.md`:

> "O objetivo principal do presente trabalho consiste [na ação] de [o quê] para [finalidade]."

**Direcionamentos:**

- o verbo que melhor descreve este trabalho é **avaliar**, não "desenvolver". Vocês vão construir uma base e treinar modelos, mas a **entrega intelectual é a avaliação**: eles servem ou não servem? Um objetivo que começa com "desenvolver um sistema de previsão" promete um produto que este TCC não entrega, e um revisor vai cobrar o produto;
- digam **o que** é avaliado: modelos de aprendizado de máquina para estimativa do rendimento da mandioca a partir de variáveis climáticas públicas;
- digam **sobre qual território e período**: os municípios do Agreste potiguar, no período analisado;
- digam **para quê**: subsidiar o indicador de estimativa de produção do observatório AgroAgreste;
- **não** empilhem ações. "Coletar, integrar, treinar e avaliar" são quatro objetivos específicos, não um objetivo geral;
- **não** prometam o que não foi medido. Se o trabalho só tratou de mandioca, o objetivo não fala em "culturas da agricultura familiar".

Uma formulação no caminho certo seria algo como *"avaliar a viabilidade de estimar o rendimento da mandioca nos municípios do Agreste potiguar por meio de modelos de aprendizado de máquina alimentados por dados climáticos públicos"*. **Não copiem essa frase** — usem-na como referência de escopo e escrevam a de vocês.

**Confiram antes de entregar:** leiam o objetivo geral e, logo depois, a primeira frase da Conclusão. Se as duas não estiverem falando da mesma coisa, uma delas está errada.

---

# 3. Objetivos Específicos
**Prazo: 24/11/2026 (com o Resumo e o Título)**

Ficam para o fim de propósito: eles descrevem o que foi **realmente alcançado**. Até lá, usem uma versão provisória no documento.

**Direcionamentos:**

- de 4 a 5 itens, verbo no infinitivo, minúscula no início, ponto e vírgula no fim de cada um e ponto no último;
- na **mesma ordem** das etapas da Metodologia e das seções dos Resultados;
- cada um **verificável**: na Conclusão vocês terão de mostrar, com número, que foi atingido;
- não confundam objetivo com tarefa. "Instalar as bibliotecas" e "aprender pandas" não são objetivos específicos.

**O que cada item deve cobrir** (redijam com as suas palavras depois):

1. revisar a literatura sobre previsão de safra, relação entre clima e produtividade no semiárido e aprendizado de máquina aplicado à agricultura;
2. construir uma base de dados integrando a série histórica de produção de mandioca do IBGE e variáveis climáticas derivadas da NASA POWER, para os municípios do Agreste potiguar;
3. estabelecer linhas de base e um protocolo de validação temporal adequado a dados de série anual;
4. treinar e comparar modelos de regressão e de árvores, medindo o ganho de cada um sobre as linhas de base;
5. identificar as variáveis climáticas mais relevantes e analisar o comportamento do erro por ano e por município;
6. recomendar, com base nas medições, a adoção ou não da abordagem pelo observatório AgroAgreste.

Se ficarem seis itens, junte o 5 com o 4 ou o 6 com o 5 — cinco é o limite confortável.

---

# 4. Referencial Teórico
**Prazo: 13/10/2026**

**Vídeo com a explicação (assistam antes de começar):** https://youtu.be/8Qztq1Q5vb0

Comecem a procurar referências **na primeira semana**. Este é o capítulo que mais consome tempo, e no caso de vocês ele tem uma dificuldade a mais: o tema é **interdisciplinar**, e vocês vão precisar ler material de computação, de agronomia e de climatologia.

Uma regra prática resolve metade dos problemas: **tudo o que vai aparecer nos Resultados precisa estar explicado antes**. Se a tabela mostra "MAE", "RMSE", "validação temporal" e "importância por permutação", esses conceitos têm de estar definidos aqui.

Dividam por subseção conforme a tabela do cronograma e **leiam o que o outro escreveu** antes de entregar — é comum o mesmo conceito aparecer definido duas vezes, de formas diferentes.

## 4.1 Agricultura familiar e a mandioca no Agreste potiguar — Aluno A

**Pesquisem:** "agricultura familiar", Lei nº 11.326/2006 (que define a agricultura familiar no Brasil), Censo Agropecuário 2017 do IBGE, "Agreste potiguar", "semiárido brasileiro", delimitação do Semiárido pela SUDENE, "cultivo da mandioca no Rio Grande do Norte", "cadeia produtiva da mandioca no Nordeste". Usem também a referência já citada no `projeto.md` (Cousteau e Silva, 2013) e material da **Embrapa** sobre a cultura.

**Escrevam:** o conceito legal de agricultura familiar e o peso dela no território; a caracterização do Agreste potiguar; e uma caracterização agronômica da mandioca que o leitor vá precisar mais adiante — **ciclo de 12 a 18 meses**, plantio no início do período chuvoso, tolerância ao déficit hídrico, possibilidade de a colheita ser adiada pelo produtor conforme o preço e a necessidade.

Esse último ponto merece uma frase própria, porque volta na discussão: **a mandioca pode ficar no solo esperando uma hora melhor**. Isso significa que a "colheita de 2022" pode conter raízes de ciclos diferentes, o que embaralha a relação entre o clima de um ano e o número registrado. É uma limitação real do trabalho e é melhor que ela apareça já fundamentada aqui.

## 4.2 Clima, chuva e produtividade agrícola no semiárido — Aluno A

**Pesquisem:** "regime pluviométrico do Rio Grande do Norte", "variabilidade interanual da precipitação no Nordeste", "El Niño e seca no Nordeste", "déficit hídrico e produtividade agrícola", "veranico", "índices agroclimáticos". Procurem também trabalhos que relacionem chuva e produtividade de culturas de sequeiro no semiárido.

**Escrevam:** como funciona a estação chuvosa no Agreste potiguar (concentração em poucos meses, alta variabilidade entre anos), o que é **déficit hídrico** e por que a **distribuição** da chuva pode importar mais que o **total** — um total de 600 mm bem distribuído e um total de 600 mm concentrado em três semanas produzem safras diferentes.

Expliquem também as variáveis agroclimáticas que vocês construíram, já as nomeando: chuva acumulada por janela, **maior sequência de dias secos consecutivos** (veranico), número de dias com chuva acima de um limiar, temperatura média e máxima. Cada uma precisa de uma justificativa agronômica com referência — não basta dizer que "foram calculadas".

Fechem dizendo por que a defasagem importa nesta cultura, o que liga esta subseção à anterior e prepara a Metodologia.

## 4.3 Aprendizado de máquina aplicado à previsão agrícola — Aluno B

**Pesquisem:** "aprendizado de máquina", "aprendizado supervisionado", "regressão", "árvores de decisão", "Random Forest" (Breiman, 2001 — é a referência fundadora, procurem o artigo original), "gradient boosting", "crop yield prediction machine learning", "previsão de safra aprendizado de máquina". Há artigos de revisão recentes sobre previsão de safra com aprendizado de máquina; **um bom artigo de revisão vale por dez artigos avulsos** para montar esta subseção.

**Escrevam:**

- o que é aprendizado supervisionado e o que distingue um problema de **regressão** de um de classificação (o de vocês é regressão: o alvo é um número contínuo);
- **regressão linear**: a ideia, a interpretabilidade dos coeficientes, as limitações (supõe relação linear, sofre com variáveis correlacionadas entre si). Mencionem a regularização (Ridge) e por que ela ajuda;
- **Random Forest**: árvores de decisão, o conjunto de muitas árvores treinadas em amostras diferentes, a média das previsões, e por que isso captura relações não lineares — como "chuva ajuda até certo ponto, e o excesso atrapalha";
- **gradient boosting**: árvores construídas em sequência, cada uma corrigindo o erro da anterior;
- **sobreajuste** (*overfitting*): o que é, por que é o risco central quando se tem muitas variáveis e poucas observações, e como se defende dele (limitar a profundidade das árvores, exigir um mínimo de amostras por folha, validar em dados não vistos).

Fechem com uma frase que amarra: modelos mais complexos **não são automaticamente melhores**, e o que decide é a medição — o que emenda diretamente na subseção seguinte.

## 4.4 Avaliação de modelos preditivos com dados temporais — Aluno B

**Esta é a subseção que sustenta o artigo de vocês.** É onde o rigor do trabalho é demonstrado, e é a que um revisor de computação vai ler com mais atenção. Não a deixem curta.

**Pesquisem:** "validação cruzada", "time series cross-validation", "walk-forward validation", "data leakage machine learning", "naive forecast", "baseline model forecasting", "MAE RMSE MAPE", "métricas de avaliação de regressão". Um livro de referência sobre previsão de séries temporais (Hyndman e Athanasopoulos, *Forecasting: principles and practice*, disponível gratuitamente na internet) resolve boa parte desta subseção e é uma referência forte.

**Escrevam:**

- por que a **validação cruzada aleatória é inadequada** para dados com ordem temporal: ao sortear as linhas, o modelo pode treinar com anos posteriores e ser testado em anos anteriores, usando o futuro para prever o passado. Digam com clareza que isso **superestima o desempenho** e produz resultados que não se sustentam em uso real;
- o que é **validação temporal com janela expansiva**, com um esquema ou uma figura simples mostrando treino e teste avançando no tempo. **Essa figura é barata de fazer e valoriza muito o artigo**;
- o que é **vazamento de dados** (*data leakage*), com exemplos concretos do próprio trabalho: usar a média histórica calculada sobre a série completa; padronizar as variáveis antes de separar treino e teste; incluir entre as variáveis a produção e a área colhida do ano que se quer prever, que juntas reconstroem exatamente o alvo;
- o que é uma **linha de base** e por que ela é obrigatória. Definam as três que vocês usaram: persistência (repetir o ano anterior), média móvel e média histórica. Digam que, em séries com forte inércia, **a persistência é um adversário difícil** — e que é por isso que ela foi escolhida como referência principal;
- as **três métricas**, com a fórmula de cada uma, a unidade e o que cada uma penaliza: MAE (erro médio em kg/ha, fácil de interpretar), RMSE (penaliza mais os erros grandes, útil quando errar feio em ano de seca é pior que errar pouco sempre) e MAPE (erro percentual, comparável entre municípios de rendimentos diferentes, mas instável quando o valor real é próximo de zero).

## 4.5 Trabalhos relacionados — os dois, metade cada

**Pesquisem:** trabalhos que tenham previsto produtividade agrícola com aprendizado de máquina a partir de dados climáticos, de preferência no Brasil e, se possível, no Nordeste ou no semiárido; trabalhos sobre previsão de safra com dados do IBGE; trabalhos sobre modelagem da produção de mandioca. Busquem nos anais do **SBIAgro** (Congresso Brasileiro de Agroinformática), da **SBC**, em revistas como a *Revista Brasileira de Engenharia Agrícola e Ambiental* e a *Pesquisa Agropecuária Brasileira*, na **BDTD**, na SciELO e no Google Acadêmico.

Termos úteis: "previsão de produtividade aprendizado de máquina Brasil", "crop yield prediction climate data machine learning", "previsão safra IBGE Random Forest", "modelagem produtividade mandioca", "yield prediction cassava".

**Escrevam:** de 4 a 6 trabalhos, um parágrafo cada, dizendo qual cultura e região estudaram, quais variáveis usaram, quais modelos compararam, **como validaram** (com que protocolo e contra qual linha de base) e quais as limitações declaradas.

Fechem com um **quadro comparativo** entre esses trabalhos e o de vocês, com colunas como: cultura, região, escala (talhão, município, estado), período, fonte de dados climáticos, modelos comparados, **uso de linha de base**, **tipo de validação** e reprodutibilidade.

**Esse quadro é a justificativa do trabalho de vocês.** O diferencial vai aparecer provavelmente em três colunas: o **recorte municipal do Agreste potiguar**, que é o território do observatório e sobre o qual dificilmente haverá trabalho publicado; a **cultura**, já que a maior parte da literatura de previsão de safra trata de soja, milho e trigo, e muito pouco de mandioca; e — prestem atenção nesta — a **comparação explícita com linha de base e validação temporal**, que uma parte considerável dos trabalhos da área simplesmente não faz.

Se encontrarem um trabalho que já faça exatamente isso, para a mesma cultura e a mesma região, **avisem o orientador**: em outubro ainda dá tempo de ajustar o recorte.

## Regras para o referencial inteiro

- **Toda afirmação técnica precisa de referência.**
- **Não empilhem citações.** Expliquem com as suas palavras, relacionem os autores e liguem ao trabalho de vocês.
- **Documentação oficial** (IBGE, NASA POWER, `scikit-learn`) serve para descrever a fonte ou a ferramenta, não para fundamentar conceito. Para conceito, usem livro ou artigo.
- **Nada de blog ou site sem autoria** nas Referências. Vocês vão usar muito esse material para resolver problema de código — isso é normal —, mas ele não entra na lista.
- **Nunca citem o que não leram.** Ferramentas de IA inventam referências com muita naturalidade, e nesta área inventam também nomes de algoritmo e valores de métrica. Confiram tudo na fonte.
- Meta para este trabalho: **20 a 28 referências**, equilibradas entre o lado computacional e o lado agrícola/climático. Se o referencial tiver vinte artigos de aprendizado de máquina e dois de agricultura, o trabalho vai parecer — e ser — desequilibrado.

---

# 5. Metodologia
**Prazo: 20/10/2026 — redator principal: Aluno A**

Como o trabalho foi feito. Verbos no passado e linguagem impessoal ("foi realizado", "realizou-se"). Duas a três páginas.

**Pasta com metodologias prontas para consulta:** https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

## 5.1 Classificação da pesquisa

**Pesquisem:** Gil (2017) e Prodanov e Freitas (2013) — referências completas no `README.md`. Leiam os capítulos de classificação antes de escrever; não classifiquem de ouvido.

**Escrevam:** a classificação pelos quatro critérios, **justificando cada uma** com uma frase ligada ao trabalho de vocês (o erro mais comum é só listar os rótulos). O enquadramento mais provável:

- **Natureza:** aplicada — o resultado responde a uma necessidade concreta do observatório AgroAgreste;
- **Objetivos:** exploratória e descritiva — investiga a viabilidade de uma abordagem ainda não aplicada a esta cultura neste território, e descreve o desempenho medido dos modelos;
- **Abordagem:** quantitativa — todos os resultados são numéricos;
- **Procedimentos:** pesquisa bibliográfica combinada com **pesquisa documental**, já que os dados são secundários e vêm de bases públicas oficiais. A parte de comparação controlada entre modelos aproxima o trabalho do procedimento **experimental** — vocês podem defender esse enquadramento, desde que justifiquem. **Combinem com o orientador.**

## 5.2 Área de estudo e período

Esta subseção é obrigatória em trabalho com recorte territorial e costuma faltar em trabalhos de iniciação.

**Escrevam:** onde fica o Agreste potiguar, quantos e quais municípios foram considerados, **qual divisão territorial foi usada** (a mesorregião do IBGE de 2010, hoje substituída pelas regiões intermediárias e imediatas — digam isso, e digam por que a mantiveram), e as características relevantes da região: clima, regime de chuvas, principais culturas.

Informem quantos municípios **efetivamente entraram** na análise e quantos foram descartados por não ter produção de mandioca registrada ou por não atender ao filtro de área mínima. **Número de exclusões é informação de método, não é vergonha.**

**Um mapa de localização é praticamente obrigatório**: o Brasil com o Rio Grande do Norte destacado e os municípios analisados marcados. Identificação em cima, fonte embaixo.

Informem o **período analisado** e justifiquem: por que começa no ano em que começa (disponibilidade das duas fontes) e por que termina no ano em que termina (último ano publicado da PAM). Digam quantos pares município-ano a base final tem — esse número é a "amostra" do trabalho e o leitor precisa dele cedo.

## 5.3 Etapas do trabalho

**Escrevam:** as etapas em ordem cronológica. Uma **figura com o fluxo do processo** ajuda muito e é esperada em trabalho de aprendizado de máquina: coleta IBGE + coleta NASA POWER → construção das variáveis → base município-ano → linhas de base → treino com validação temporal → métricas e análise. Usem o draw.io, que é gratuito.

As etapas:

1. levantamento bibliográfico;
2. definição da área de estudo, do período e da cultura;
3. coleta e tratamento dos dados de produção do IBGE, com cálculo do rendimento;
4. coleta dos dados climáticos diários e construção das variáveis agroclimáticas anuais;
5. integração das duas bases em uma tabela município-ano;
6. definição das linhas de base e do protocolo de validação temporal;
7. treino e avaliação dos modelos;
8. análise da importância das variáveis e do comportamento do erro;
9. elaboração da recomendação para o observatório.

**Justifiquem as decisões que a banca ou o revisor vão questionar** — e neste trabalho elas são específicas:

- **por que o rendimento (kg/ha) e não a produção total**: porque a produção depende da área plantada, que é decisão econômica do produtor e não é explicada por clima;
- **por que as janelas climáticas são as que são**: liguem cada janela ao ciclo de 12 a 18 meses da mandioca. Digam com honestidade se o calendário agrícola usado veio da literatura, do regime de chuvas da região ou de informação do orientador;
- **por que a validação é temporal e não aleatória**: já fundamentado na seção 4.4, aqui basta retomar em duas frases e dizer qual foi o primeiro ano de teste;
- **por que estas linhas de base**: e por que a persistência foi tomada como referência principal;
- **por que o filtro de área mínima**: e quantas linhas ele removeu;
- **como os valores faltantes foram tratados**: os códigos especiais do IBGE (`-`, `..`, `...`, `X`) e os `-999` da NASA POWER. Digam explicitamente que "não disponível" **não** foi convertido em zero, e por quê.

---

# 6. Materiais e Métodos
**Prazo: 27/10/2026 — redator principal: Aluno B**

Vale a analogia da receita de bolo do `README.md`: **lista de ingredientes** mais **modo de preparo**. Em trabalho com dados e modelos, é esta seção que permite (ou impede) a reprodução.

## 6.1 Materiais

**As fontes de dados** merecem uma tabela própria, com endereço e **data de acesso**:

| Fonte | O que forneceu | Detalhes a informar |
|---|---|---|
| IBGE – Produção Agrícola Municipal | Área plantada, área colhida, produção e rendimento da mandioca | **Número da tabela do SIDRA, códigos das variáveis e o código do produto**; nível territorial; período |
| IBGE – API de Localidades e malhas | Lista de municípios e coordenadas | Qual divisão territorial; como o ponto de cada município foi obtido |
| NASA POWER | Chuva e temperatura diárias | **Nomes exatos dos parâmetros** (`PRECTOTCORR`, `T2M`, `T2M_MAX`, `T2M_MIN`), unidades, comunidade (`AG`), período |

Os códigos do SIDRA não são detalhe burocrático: sem eles, ninguém repete a coleta. Vocês os anotaram na Sprint 1 exatamente para isto.

**As ferramentas**, cada uma com **o que é**, **para que foi usada** e **por que foi escolhida**:

| Biblioteca | Para quê |
|---|---|
| `requests` | Acesso às APIs do IBGE e da NASA POWER |
| `pandas` | Tratamento, integração e agregação dos dados |
| `scikit-learn` | Modelos, métricas e importância por permutação |
| `matplotlib` | Gráficos |
| `SQLAlchemy` / `PyMySQL` | Carga da base final no MySQL |

**Informem as versões de tudo**, inclusive a do Python. Mudança de versão do `scikit-learn` muda resultado — sem isso, o método não é reprodutível.

**O ambiente de execução:** processador, memória RAM, sistema operacional e conexão de internet.

**Declarem também o que não foi usado e por quê** — e aqui há dois pontos que valem parágrafo:

- **o banco de dados.** O processamento foi feito em arquivos CSV, adequados ao volume (cerca de mil registros); o MySQL foi utilizado apenas na etapa final, como camada de persistência voltada à integração futura com o observatório. Justificar a ferramenta dimensionada ao problema é sinal de maturidade técnica, e deixa claro que a escolha foi consciente;
- **as redes neurais.** Não foram consideradas por causa do volume de dados. Digam isso explicitamente — alguém vai perguntar.

## 6.2 Métodos

**a) Coleta dos dados de produção.** Como a API do SIDRA foi consultada, quais variáveis, qual filtro territorial, e **como os valores especiais do IBGE foram tratados**, um a um. Informem o percentual de pares município-ano com valor omitido ou indisponível.

**b) Cálculo do rendimento.** A fórmula usada (produção em toneladas × 1000 ÷ área colhida em hectares) e — importante — a **conferência contra o rendimento publicado pelo IBGE**, com a diferença média obtida. Isso é uma validação da base e deve aparecer com número.

**c) Coleta dos dados climáticos.** O endpoint, os parâmetros, o ponto de consulta de cada município (a sede ou o centroide — digam qual e por quê), o período e o tratamento dos valores `-999`.

**d) Construção das variáveis agroclimáticas.** Uma **tabela com todas as variáveis**, dizendo o nome, a janela temporal, a unidade e a justificativa agronômica de cada uma. Essa tabela é o coração da reprodutibilidade do trabalho.

Expliquem também a construção das variáveis defasadas: como as variáveis do ano anterior foram associadas a cada linha, e o cuidado de fazer isso **dentro de cada município**.

**e) Integração das bases.** A chave usada (código IBGE de sete dígitos), o tipo de junção, quantas linhas entraram e quantas se perderam, e por quê. Digam o número final de observações.

**f) Linhas de base.** As três, com a definição exata de cada uma. Para a média histórica, **digam explicitamente que foi calculada apenas sobre os anos de treino**.

**g) Protocolo de validação.** A janela expansiva, o primeiro ano de teste, quantas iterações, e o fato de que um modelo novo foi treinado a cada ano. Digam que as previsões de todos os anos de teste foram reunidas para o cálculo das métricas.

**h) Modelos e hiperparâmetros.** Cada modelo com os parâmetros efetivamente usados (`n_estimators`, `min_samples_leaf`, `learning_rate`, `alpha`, a semente aleatória). **Se testaram mais de uma configuração, digam todas as que testaram e como escolheram** — apresentar só a melhor, sem dizer que houve busca, é uma forma silenciosa de inflar o resultado.

**i) Padronização das variáveis.** Que foi aplicada apenas aos modelos lineares e **dentro do fluxo de treino**, para não vazar informação do conjunto de teste.

**j) Métricas e importância.** As três métricas, o tratamento dado aos valores muito baixos no cálculo do MAPE, e o método de importância por permutação (número de repetições, conjunto usado, métrica de referência).

**k) Persistência em banco.** As tabelas criadas no MySQL e o que cada uma guarda. Se a carga foi validada em SQLite por falta de acesso ao servidor, **digam isso** — é uma limitação de infraestrutura, não um defeito do método.

---

# 7. Resultados e Discussão
**Prazo: 10/11/2026 — os dois**

A seção mais importante. Três a quatro páginas. Organizem-na respondendo às **três perguntas** enunciadas na Introdução.

> **Regra sem exceção:** toda figura ou tabela é **anunciada no texto antes** de aparecer e **explicada depois**. Nunca duas figuras seguidas sem texto entre elas.

> **Segunda regra sem exceção:** **nenhuma métrica aparece sozinha.** Toda vez que um erro de modelo for citado, o erro da linha de base aparece ao lado. Isso vale na tabela, no texto, no Resumo e na Conclusão.

## 7.1 A base de dados obtida — Aluno A

Comecem por aqui, porque é o que sustenta todo o resto. Uma tabela com: número de municípios, período, número de pares município-ano, quantos foram descartados e por qual motivo (valor omitido pelo IBGE, área abaixo do filtro, ausência do ano anterior).

Apresentem também a **estatística descritiva do rendimento**: média, desvio, mínimo, máximo e a variação entre municípios e entre anos.

**Discutam** duas coisas que vão ser decisivas mais adiante:

- **quanta variação existe de um ano para outro** no mesmo município. Se a série for muito estável, digam isso com número (por exemplo, a variação percentual mediana entre anos consecutivos) — é essa estabilidade que torna a linha de base de persistência difícil de superar, e o leitor precisa saber disso **antes** de ver a tabela de modelos;
- **a natureza do dado**: a PAM municipal é em boa parte estimada. Se vocês encontraram municípios com o mesmo valor repetido por vários anos seguidos, **apresentem o número**. Isso é uma característica da fonte que limita o que qualquer modelo pode alcançar, e apontá-la é uma contribuição do trabalho.

## 7.2 O comportamento do clima e da produção — Aluno A

Apresentem a série histórica do rendimento médio do Agreste e a série de chuva no mesmo eixo de tempo, e a dispersão entre a chuva e o rendimento.

**Discutam:**

- **os anos de queda** de produção coincidem com anos secos conhecidos na região? A seca de 2012 a 2017 aparece na série? Se aparecer, digam com todas as letras: essa é a **primeira validação externa** da base, obtida antes de qualquer modelo;
- **a correlação direta** entre as variáveis climáticas e o rendimento, em tabela. Sejam honestos com a magnitude: se as correlações forem fracas, esse é um resultado, e ele antecipa e explica o que vem na próxima subseção;
- **a diferença entre municípios**: a relação clima-produção é igual em todos, ou há municípios em que o clima parece explicar mais?

## 7.3 Desempenho dos modelos — Aluno B

A primeira pergunta do artigo, e o resultado central.

A **tabela comparativa** é a peça principal do trabalho:

| Modelo | MAE (kg/ha) | RMSE (kg/ha) | MAPE (%) | Ganho sobre a persistência |
|---|---|---|---|---|
| B1 – persistência | | | | — |
| B2 – média móvel (3 anos) | | | | |
| B3 – média histórica | | | | |
| Regressão linear | | | | |
| Ridge | | | | |
| Random Forest | | | | |
| Gradient boosting | | | | |

Acompanhem com o gráfico de **real × previsto** do melhor modelo, com a reta de 45 graus.

**Discutam**, e aqui há dois caminhos possíveis — escrevam o que os números mostrarem, sem torcer:

**Se algum modelo superou a linha de base:** digam de quanto foi o ganho, em kg/ha e em percentual, e **o que isso significa na prática** — um ganho de 3% sobre a persistência provavelmente não justifica a complexidade de manter o modelo em produção; um ganho de 20% justifica. Comparem o MAE com o rendimento médio, para dar ao leitor a ordem de grandeza do erro relativo. Comparem também os modelos entre si: o Random Forest ganhou da regressão linear? Se sim, é indício de relações não lineares entre clima e produção, e vale dizer.

**Se nenhum modelo superou a linha de base:** digam isso claramente, no começo da subseção, sem rodeios e sem pedir desculpa. Depois discutam as causas, que vocês têm elementos para sustentar: a inércia da série municipal (mostrada em 7.1); a natureza estimada do dado da PAM; a tolerância da mandioca ao déficit hídrico, que atenua o sinal climático justamente nesta cultura; o ciclo que atravessa dois anos civis e a possibilidade de a colheita ser adiada pelo produtor; e o volume reduzido de observações. **Esse conjunto de argumentos é uma contribuição científica real** — ele diz à comunidade e ao observatório o que não adianta tentar por este caminho, e por quê.

Observem também o comportamento da dispersão real × previsto: se os pontos se achatarem em torno da média, o modelo está prevendo aproximadamente a média para todo mundo. Digam isso — é um diagnóstico, não um detalhe.

## 7.4 Quais variáveis importam — Aluno B

A segunda pergunta. O gráfico de barras da importância por permutação, com o desvio.

**Discutam:**

- **o que ficou no topo.** Se for `rendimento_ant`, o resultado é que o melhor preditor do rendimento é o próprio histórico, e as variáveis climáticas acrescentam pouco — o que é coerente com o que a subseção anterior mostrou;
- **qual variável climática foi a mais relevante**, e em qual janela do ciclo. Se for uma variável do ano anterior, isso **confirma a defasagem prevista pelo ciclo da cultura**, e é um achado bonito de escrever;
- **total contra distribuição**: se a maior sequência de dias secos pesou mais que a chuva acumulada, vocês têm um resultado com significado agronômico direto — importa mais **como** a chuva se distribuiu do que **quanto** choveu. Liguem isso ao que foi fundamentado na seção 4.2;
- **o sinal dos coeficientes** da regressão linear: mais chuva no ano anterior está associada a mais rendimento? A magnitude faz sentido agronômico?

Sejam cuidadosos com a linguagem: importância de variável indica **associação**, não causa. Escrevam "está associado a", não "causa".

## 7.5 Onde o modelo erra — Aluno A

A terceira pergunta, e a mais relevante para o observatório.

Gráfico de MAE por ano, com as barras do modelo e da linha de base lado a lado, e uma tabela com os municípios de maior e de menor erro.

**Discutam:**

- **o erro nos anos extremos.** Cruzem com os anos secos identificados em 7.2 e com o Monitor de Secas. Se o erro for maior justamente nos anos de seca, **isso é o achado mais importante da seção** e precisa estar em destaque: significa que o modelo falha exatamente quando seria mais necessário. Um erro médio baixo obtido às custas de acertar os anos normais e errar os extremos **não serve ao planejamento territorial**;
- **os municípios de maior erro**: o que eles têm em comum? Área plantada pequena? Série com muitos valores omitidos? Rendimento historicamente instável? Ofereçam uma hipótese fundamentada para cada padrão encontrado;
- se houver um mapa do erro por município, comentem se existe algum padrão espacial.

## 7.6 Custo computacional — Aluno B

Uma tabela curta: tempo de coleta de cada fonte, tempo de construção da base, tempo de treino de um modelo, tempo da validação temporal completa.

**Discutam:** a viabilidade operacional. A conclusão provável é que **todo o processo cabe em minutos em um computador comum, e a atualização é anual**. Para um observatório de projeto de extensão, sem servidor dedicado, essa é uma informação prática relevante — e ela vale tanto se o modelo for adotado quanto se a recomendação for publicar apenas a base integrada.

## 7.7 Limitações do trabalho

Subseção curta e honesta. Reconhecer limite aumenta a confiança no trabalho:

- **a qualidade do dado alvo**: a PAM municipal é parcialmente estimada, e nenhum modelo pode ser mais preciso do que o dado com que é treinado. Esta é a limitação central e merece vir primeiro;
- **a escala municipal**: a previsão é sobre a média de muitas propriedades, com solos, manejos e datas de plantio diferentes. **Ela não vale para uma propriedade individual** — digam isso explicitamente;
- **o clima de um único ponto por município**, enquanto a chuva no semiárido é notoriamente irregular no espaço;
- **o ciclo da mandioca**, que atravessa anos civis e pode ser prolongado por decisão do produtor, desalinhando o ano da colheita do ano climático;
- **as variáveis ausentes**: solo, manejo, variedade plantada, uso de insumos, preço, acesso a crédito e a assistência técnica. Nada disso está no modelo, e tudo isso afeta a produção;
- **o número de observações**, pequeno para os padrões do aprendizado de máquina;
- **a ausência de validação de campo**, que exigiria envolver pessoas e, portanto, aprovação do comitê de ética.

Depois de listar, notem que essas limitações incidem igualmente sobre todos os modelos comparados, **o que preserva a validade da comparação entre eles**, ainda que os valores absolutos devam ser lidos com cautela. Essa frase é importante: ela protege o resultado principal do trabalho.

---

# 8. Conclusão
**Prazo: 17/11/2026 — redator principal: Aluno A, revisão do B**

Curta e direta. Nada de resultado, conceito ou citação que não tenha aparecido antes.

**Escrevam, nesta ordem:**

1. **Retomada do problema e do objetivo geral**, afirmando se ele foi alcançado **e dizendo por quê, com número**. Reparem que o objetivo era *avaliar a viabilidade* — e ele é alcançado tanto se a resposta for "sim" quanto se for "não". O que não pode é não ter resposta.

2. **Um comentário por objetivo específico**, na mesma ordem, cada um apontando o resultado que o comprova.

3. **A resposta às três perguntas** da Introdução, uma ou duas frases cada: os modelos superaram a linha de base? quais variáveis importaram? o desempenho se manteve nos anos extremos?

4. **Contribuições**, que existem independentemente de os modelos terem ganhado ou não:
   - uma base de dados integrada e reprodutível, cruzando produção de mandioca e clima para os municípios do Agreste potiguar, que pode ser reaproveitada por outros trabalhos do projeto;
   - um protocolo de avaliação temporal com linhas de base, aplicável a outras culturas e outros indicadores do observatório;
   - a medição do que dados climáticos públicos conseguem e não conseguem explicar da produção municipal de mandioca;
   - uma recomendação técnica fundamentada para o AgroAgreste.

5. **Limitações e dificuldades:** retomem brevemente as limitações e acrescentem as dificuldades reais do desenvolvimento — o tratamento dos valores especiais do IBGE, o alinhamento entre o ciclo da cultura e o ano civil, o cuidado para evitar vazamento de dados na construção das variáveis defasadas. É aqui que o `docs/diario.md` das sprints se paga.

6. **Trabalhos futuros**, concretos e ligados ao que vocês encontraram:
   - incorporar índices de vegetação por satélite (NDVI), que medem a lavoura diretamente e não apenas o clima a que ela foi exposta — este é o encaminhamento mais forte, e liga o trabalho ao TCC do colega sobre NDVI;
   - testar a abordagem em culturas de ciclo curto e mais sensíveis à chuva, como feijão e milho, onde o sinal climático tende a ser mais claro;
   - prever a **variação** do rendimento em vez do valor absoluto, removendo a inércia da série;
   - estender a análise a todo o Rio Grande do Norte ou ao semiárido, aumentando o número de observações;
   - integrar a base e o modelo ao observatório AgroAgreste, aproveitando a carga em banco já implementada;
   - validar contra dados de campo, quando o projeto dispuser deles.

**Não escrevam** que "o modelo prevê a safra de um agricultor" — a previsão é municipal. E não generalizem para o semiárido inteiro, nem para outras culturas, o que foi medido para a mandioca em alguns dezenas de municípios do Agreste potiguar.

**E não transformem um resultado negativo em promessa.** Se os modelos não superaram a linha de base, a conclusão não é "com mais dados funcionaria" — é "com estes dados, nesta escala, não funcionou, e estas são as razões e os caminhos". A primeira frase é torcida; a segunda é ciência.

---

# 9. Resumo, Título e revisão final
**Prazo: 24/11/2026 — redator principal: Aluno B, revisão do A**

## 9.1 Resumo

Escrito **por último**, depois de o texto todo estar aprovado pelo orientador. Parágrafo único, 150 a 500 palavras, linguagem impessoal, sem citações, sem siglas pouco conhecidas e sem menção a figuras ou tabelas (NBR 6028:2021).

Uma ou duas frases para cada item:

1. **contexto e problema:** a dependência da agricultura familiar do Agreste em relação à chuva e a ausência de estimativa de safra antes da publicação oficial;
2. **objetivo:** o que o trabalho se propôs a avaliar;
3. **método:** as duas fontes de dados, os municípios, o período, o número de observações, os modelos comparados e **o protocolo de validação temporal com linhas de base** — essa última parte não pode faltar, é o que dá credibilidade ao resumo;
4. **resultados:** os números principais — MAE do melhor modelo **e da linha de base**, o ganho percentual, a variável mais importante;
5. **conclusão:** a recomendação para o observatório.

**Coloquem números no resumo, e sempre em par com a linha de base.** Em um trabalho que mede coisas, resumo sem número é resumo fraco — e é o resumo que faz alguém decidir se lê o resto.

O **Abstract** é a versão em inglês. Os termos da área têm forma consagrada (*machine learning*, *crop yield prediction*, *baseline model*, *time series cross-validation*, *smallholder farming*, *cassava*, *semi-arid*); usem-nas, e não a tradução literal. Não entreguem tradução automática sem revisar.

**Palavras-chave** (3 a 5), separadas por ponto e vírgula. Campo de ideias: aprendizado de máquina; previsão de safra; mandioca; agricultura familiar; semiárido; dados climáticos. Escolham os termos pelos quais alguém **procuraria** o trabalho de vocês, equilibrando o lado técnico e o territorial.

## 9.2 Título

**Última coisa a ser definida**, em acordo com o orientador. Deve indicar **o que foi feito** e **onde**, e combinar com o objetivo geral.

Pontos a cobrir: a ação (avaliação, análise ou comparação), o objeto (modelos de aprendizado de máquina para estimativa do rendimento da mandioca a partir de dados climáticos) e o recorte territorial (municípios do Agreste potiguar). Se houver subtítulo, separem com dois-pontos. Em trabalho com recorte territorial, **incluir o território no título é quase obrigatório** — é o que faz o trabalho ser encontrado por quem pesquisa a região.

Evitem título genérico ("Inteligência artificial na agricultura") e **não prometam mais do que o trabalho mediu**. Em especial: se os modelos não superaram a linha de base, o título não pode ser "Previsão da produção de mandioca com aprendizado de máquina" — isso anuncia um resultado que o artigo não tem. Nesse caso, um título que comece por "Avaliação de..." ou "Limites de..." é mais honesto **e mais interessante**.

## 9.3 Revisão final — checklist

Além do checklist do `README.md`:

- [ ] O objetivo geral, os objetivos específicos, as seções dos Resultados e os parágrafos da Conclusão estão na mesma ordem e falando das mesmas coisas?
- [ ] As três perguntas da Introdução foram respondidas nos Resultados e retomadas na Conclusão?
- [ ] **Toda métrica citada no texto aparece ao lado da métrica da linha de base?**
- [ ] Todos os números citados no Resumo, nos Resultados e na Conclusão são **exatamente** os mesmos?
- [ ] Toda métrica que aparece nos Resultados foi explicada no Referencial?
- [ ] O protocolo de validação temporal está descrito com clareza suficiente para alguém repetir?
- [ ] Está dito explicitamente que a média histórica foi calculada apenas com anos de treino?
- [ ] Os hiperparâmetros usados e as configurações testadas estão informados?
- [ ] As sementes aleatórias estão informadas?
- [ ] **Os códigos da tabela do SIDRA** (tabela, variáveis, produto) estão no texto?
- [ ] Os nomes exatos dos parâmetros da NASA POWER estão no texto?
- [ ] O tratamento dos valores faltantes das duas fontes está descrito?
- [ ] O mapa de localização da área de estudo está presente?
- [ ] Todas as fontes de dados têm endereço e **data de acesso**?
- [ ] Toda figura e tabela é citada no texto antes de aparecer e explicada depois?
- [ ] Todas as figuras e tabelas têm identificação em cima, centralizada, e fonte embaixo?
- [ ] Os gráficos têm unidade no eixo e legenda?
- [ ] O ambiente de execução está descrito (máquina, sistema, versões)?
- [ ] A seção de limitações está presente e honesta?
- [ ] A linguagem distingue associação de causa?
- [ ] As siglas (MAE, RMSE, MAPE, PAM, IBGE, ANA, SUDENE, CEP, API) foram escritas por extenso na primeira ocorrência?
- [ ] A numeração das seções está sem ponto após o número ("2.3 Aprendizado de máquina aplicado à previsão agrícola")?
- [ ] O texto está impessoal e no passado?
- [ ] **O texto tem voz única?** Um dos dois leu tudo em voz alta procurando emendas entre os trechos de cada autor?
- [ ] Está declarado que os dados são públicos e secundários e que não houve participantes humanos?
- [ ] Os dois autores estão na folha de rosto, na ordem combinada com o orientador?
- [ ] Todos os comentários do orientador no documento do Drive foram respondidos?
- [ ] A versão final foi nomeada no histórico de versões do Drive?

---

## Referências mínimas a garantir

Como o trabalho é interdisciplinar, o referencial precisa ser equilibrado:

**Lado agrícola e territorial:**

- **2 a 3 fontes sobre agricultura familiar e o Agreste potiguar** (Seção 4.1), incluindo dados do IBGE e a Lei nº 11.326/2006;
- **2 a 3 fontes sobre a mandioca** — ciclo, exigências, tolerância à seca —, de preferência da Embrapa;
- **2 a 3 fontes sobre clima do semiárido e relação entre chuva e produtividade** (Seção 4.2);

**Lado computacional:**

- **3 a 4 obras sobre aprendizado de máquina** (Seção 4.3), incluindo a referência original do Random Forest e pelo menos um livro-texto da área;
- **2 a 3 obras sobre avaliação de modelos e validação temporal** (Seção 4.4). Esta é a subseção que mais precisa de referência sólida, e é a que os trabalhos de iniciação costumam deixar sem fundamentação;
- **4 a 6 trabalhos relacionados** (Seção 4.5), de preferência sobre previsão de safra no Brasil;

**Obrigatórias:**

- **2 obras de metodologia científica** — Gil (2017) e Prodanov e Freitas (2013), já no `README.md`;
- **a documentação oficial das fontes e ferramentas** — a metodologia da PAM do IBGE, a NASA POWER e o `scikit-learn`.

Anotem a referência completa de **tudo** o que lerem, na seção de Referências do documento do Drive, desde o primeiro dia — e combinem entre vocês **um único gerenciador** ou nenhum. Dois gerenciadores diferentes na mesma lista de referências geram formatação inconsistente, que é uma das coisas mais fáceis de um revisor notar. Zotero e Mendeley ajudam a montar, mas confiram cada entrada contra a NBR 6023:2018 antes de entregar: esses gerenciadores erram com frequência.
