# Plano de escrita do artigo – Victor (Tecnologia em Sistemas para Internet)

**Projeto pai:** AgroAgreste – Observatório Territorial da Agricultura Familiar no Agreste do Rio Grande do Norte (ver [projeto.md](../projeto.md)).

**Temática:** S4 – Monitoramento da vegetação e das áreas agrícolas por imagens de satélite, com o índice NDVI (ver [tematicas.md](../tematicas.md)).

**Plano de desenvolvimento correspondente:** `01_victor_agro_tarefas_desenvolvimento.md`.

**Base de estilo e de normas ABNT:** o arquivo [README.md](../../../README.md) deste repositório. Tudo o que está lá vale aqui — estrutura, citações, referências, figuras, tabelas, formatação. Este documento **não repete** as regras da ABNT; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copie estas frases para o artigo. Elas dizem sobre o que é cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você leu.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do artigo será **criado e compartilhado pelo coordenador em uma pasta do Google Drive**. Você não cria arquivo novo nem trabalha em cópia local.

Como trabalhar nele:

- **Escreva sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico do Drive é o que permite ao orientador ver o que mudou de uma semana para outra.
- **Não crie cópias** ("Artigo v2", "Artigo final", "Artigo final revisado"). É a forma mais rápida de perder trabalho. O Drive já guarda tudo em **Arquivo → Histórico de versões**.
- **Marque cada entrega no histórico.** Ao terminar uma seção, use **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 29/09`.
- **Avise por mensagem quando entregar.** O orientador não fica olhando o documento; ele precisa saber que há algo novo.
- **Comentário se responde, não se apaga.** Responda a cada comentário e só então marque como resolvido.
- **Figuras e mapas** vão dentro do documento, no lugar certo, com identificação em cima e fonte embaixo. Não mande imagem em anexo separado.
- **Crie a seção "Referências" no primeiro dia** e acrescente cada obra assim que ler. Deixar para o fim garante referência faltando.
- **Não dê acesso a terceiros** sem falar com o coordenador.

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
| 22/09 a 28/09 | Sprint 1 – ambiente e catálogo de imagens | Introdução e Objetivo Geral (29/09) |
| 29/09 a 12/10 | Sprints 2 e 3 – primeiro NDVI e máscara de nuvem | Referencial Teórico (13/10) |
| 13/10 a 19/10 | Sprint 4 – série temporal de um município | Metodologia (20/10) |
| 20/10 a 26/10 | Sprint 5 – demais municípios e chuva | Materiais e Métodos (27/10) |
| 27/10 a 09/11 | Sprints 6 e 7 – correlações e mapas | Resultados (10/11) |
| 10/11 a 16/11 | Sprint 8 – custo e recomendação | Conclusão (17/11) |
| 17/11 a 23/11 | — | Resumo, Objetivos e Título (24/11) |

**Um aviso sobre o cronograma.** A Metodologia vence em 20/10, quando você terá processado apenas um município. E os Resultados vencem em 10/11, logo depois das sprints de análise. Isso é normal e tem solução:

- escreva a Metodologia falando do **plano** ("serão processados quatro municípios...") e depois passe tudo para o passado;
- **vá colando as figuras e as tabelas no documento a cada sprint**, mesmo sem o texto de análise pronto. Quem deixa os Resultados para a última semana não entrega.

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Texto pela metade dá para comentar; texto que não chega, não.
- Cada entrega é: seção escrita + versão nomeada no histórico + aviso ao orientador.
- Resolva **todos** os comentários da entrega anterior antes de avisar sobre a próxima.

---

## Que tipo de trabalho é este

Um **artigo científico** de 8 a 12 páginas, para um congresso ou uma revista. **Confirme com o orientador qual é o destino antes de começar** — dele vêm o modelo de formatação e o limite de páginas. Como o tema cruza tecnologia e agricultura, há duas famílias possíveis de destino (eventos de computação aplicada e eventos de agricultura, geoprocessamento ou desenvolvimento regional), e a escolha muda o tom do texto.

Quatro coisas fazem a diferença entre um relato e um artigo publicável:

1. **O objeto do trabalho não é o programa que você escreveu.** É o **indicador construído e validado**. O observatório AgroAgreste é o contexto que justifica a pergunta. Se o texto virar um manual dos seus scripts, o trabalho perde o valor.
2. **O leitor quer saber quanto, não o quê.** Não interessa que você calculou NDVI; interessa que a correlação com a chuva de dois meses antes foi de 0,X, e o que isso significa para o Agreste.
3. **O método tem de dar para repetir.** Municípios, período, satélite, bandas, critério de nuvem, versões das bibliotecas, máquina.
4. **Declare as limitações.** Este trabalho tem várias, e algumas são interessantes de discutir: nuvem, resolução, média que mistura usos da terra diferentes. Reconhecê-las aumenta a confiança no trabalho.

Estrutura sugerida:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Agricultura familiar e o Agreste potiguar
2.2 Sensoriamento remoto e imagens de satélite
2.3 Índices de vegetação e o NDVI
2.4 Vegetação do semiárido, chuva e séries temporais de NDVI
2.5 Trabalhos relacionados
3 METODOLOGIA
3.1 Classificação da pesquisa
3.2 Área de estudo
3.3 Etapas do trabalho
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
6 CONCLUSÃO
REFERÊNCIAS
```

---

# 1. Introdução
**Prazo: 29/09/2026**

Cinco blocos de parágrafos, nesta ordem (é a sequência fixa do `README.md`). Duas a três páginas.

## 1.1 Contextualização (2 a 3 parágrafos)

**Pesquise sobre:**

- **a agricultura familiar no Agreste do Rio Grande do Norte**: seu peso econômico e social, e as culturas principais da região. O `projeto.md` já lhe dá um ponto de partida com a mandioca e a referência de Cousteau e Silva (2013). Procure também dados do **IBGE** — a Produção Agrícola Municipal e o Censo Agropecuário de 2017 — para ter números de área plantada, produção e número de estabelecimentos familiares;
- **o semiárido e a caatinga**: a delimitação oficial do Semiárido (feita pela SUDENE), o regime de chuvas concentrado em poucos meses, a irregularidade entre anos e as secas. Procure por "semiárido brasileiro", "caatinga", "regime pluviométrico do Rio Grande do Norte";
- **o papel da informação no planejamento territorial**: por que indicadores organizados ajudam gestores, associações e agricultores a decidir.

**Escreva sobre:** a importância da agricultura familiar no Agreste potiguar e a dependência direta que ela tem da chuva. Traga **pelo menos um dado numérico** (área plantada de mandioca na região, número de estabelecimentos familiares, algo do IBGE) — dado numérico dá peso imediato ao texto.

Depois apresente o projeto AgroAgreste como o observatório que está sendo construído para reunir e organizar essas informações, e diga qual parte dele o seu trabalho atende: o **indicador ambiental de vegetação**.

## 1.2 Problemática (2 a 3 parágrafos)

**Pesquise sobre:**

- a **ausência de monitoramento contínuo** da vegetação e das lavouras em escala municipal. Levantamentos de campo são caros e pouco frequentes; os dados do IBGE são anuais e saem com atraso;
- os **impactos da seca** na agricultura familiar do semiárido: perda de safra, perda de renda, insegurança alimentar. Procure por trabalhos sobre secas no Nordeste e pelo **Monitor de Secas**, da ANA;
- por que **acompanhar a vegetação ao longo do ano** faz diferença: uma seca percebida cedo permite reação; percebida na colheita, não.

**Escreva sobre:** o problema concreto, em duas camadas.

Primeiro, **o que falta hoje**: não existe acompanhamento contínuo das condições da vegetação no Agreste. Sabe-se que um ano foi seco ou chuvoso, mas não há um número que descreva, mês a mês e município a município, como a vegetação respondeu. Sem isso, o observatório não tem como oferecer um indicador ambiental, e o planejamento territorial fica sem base objetiva.

Segundo, **por que a solução óbvia não é óbvia**: as imagens de satélite que permitiriam calcular esse indicador são **gratuitas e públicas há anos**. O obstáculo não é o dado, é o caminho até ele — é preciso saber onde procurar as imagens, como filtrar nuvem, como recortar por município, como calcular o índice e como transformar tudo isso em uma série temporal. Esse conhecimento técnico não está disponível dentro do projeto, e é exatamente essa lacuna que o trabalho preenche.

**Feche enunciando a pergunta de pesquisa**, de forma direta: *é possível construir, com imagens de satélite gratuitas, um indicador mensal de vigor da vegetação para os municípios do Agreste potiguar? E esse indicador se comporta como a literatura prevê?*

Desdobre em três perguntas menores, que vão organizar o capítulo de Resultados:

- o indicador reproduz o **ciclo anual** esperado da vegetação do semiárido?
- ele **responde à chuva**, e com quantos meses de atraso?
- ele distingue **anos secos de anos chuvosos** reconhecidos na região?

**Não escreva** que "o AgroAgreste não tem indicadores". Ele está em construção — e esse é o argumento: é o momento certo de validar a técnica antes de a equipe implementá-la.

## 1.3 Caminho para a solução (1 a 2 parágrafos)

**Pesquise sobre:**

- as formas de acompanhar a vegetação: levantamento de campo, declaração dos produtores, dados agregados anuais do IBGE e **sensoriamento remoto**;
- os satélites disponíveis gratuitamente e suas diferenças: **Sentinel-2** (10 a 20 m, a cada poucos dias), **Landsat** (30 m, série histórica longa) e **MODIS** (250 m, diário). Compare resolução espacial, frequência e volume de dados;
- os **índices de vegetação** que se pode calcular a partir dessas imagens: NDVI, SAVI, EVI.

**Escreva sobre:** as alternativas, dizendo o que cada uma resolve e o que custa. Mostre que o sensoriamento remoto se destaca por três razões: cobre **todo** o território (inclusive municípios sem nenhuma estação de medição), é **retroativo** (dá para reconstruir a série de anos passados, o que nenhum levantamento de campo permite) e é **gratuito**.

Justifique então as escolhas do trabalho: o **Sentinel-2**, pela resolução compatível com o tamanho das propriedades da agricultura familiar; e o **NDVI**, por ser o índice de vegetação mais consolidado e mais comparável com a literatura.

Diga também o que **não** foi feito e por quê: não foram usados dados de campo, porque o projeto ainda não os coletou e porque envolveriam pessoas; e não foram usados serviços pagos de processamento. Recorte declarado é recorte defendido.

## 1.4 Apresentação da solução (2 parágrafos)

**Escreva sobre:** o que foi construído, de forma concreta. Um processo em Python que, para cada município e cada mês entre 2021 e 2025, busca no catálogo aberto a imagem Sentinel-2 menos nublada, recorta apenas a área do município, descarta os pixels cobertos por nuvem, calcula o NDVI e registra o valor médio em uma série temporal.

Destaque a decisão de projeto que tornou o trabalho viável: **o processo não armazena imagens**. Ele baixa apenas o recorte necessário, calcula o indicador e descarta o dado bruto, guardando somente o valor agregado. Isso reduz drasticamente a necessidade de disco e de banda — e é justamente o que permite que o observatório rode isso em infraestrutura modesta.

Diga **como o indicador foi validado**, que é o que sustenta o artigo:

- comparação da série de NDVI com a série de **chuva** da NASA POWER, testando diferentes defasagens;
- comparação entre os **anos mais secos e mais chuvosos** da série, conferida com uma fonte independente (o Monitor de Secas, da ANA);
- comparação **entre municípios** com perfis territoriais diferentes;
- medição do **custo computacional**: tempo de processamento e volume de dados transferidos por município e por ano.

Registre que **todos os dados são públicos e secundários**, de órgãos oficiais, e que **o trabalho não envolveu pessoas** — logo, não houve necessidade de submissão ao Comitê de Ética em Pesquisa.

## 1.5 Vínculo com o projeto e escopo (1 parágrafo)

**Escreva sobre:** o vínculo com o projeto AgroAgreste, do IFRN, que está construindo um observatório territorial da agricultura familiar no Agreste potiguar. Explique que este trabalho foi desenvolvido **de forma independente**, como protótipo, para validar a técnica antes de incorporá-la à plataforma.

Deixe claro que a **integração ao observatório é trabalho futuro**, fora do escopo deste artigo, e que o que se entrega é um indicador validado e uma recomendação fundamentada em medição.

Feche a Introdução com um parágrafo curto dizendo como o texto está organizado.

---

# 2. Objetivo Geral
**Prazo: 29/09/2026 (junto com a Introdução)**

Uma **única frase**, com **uma única ação principal**. Modelo do `README.md`:

> "O objetivo principal do presente trabalho consiste [na ação] de [o quê] para [finalidade]."

**Direcionamentos:**

- aqui cabem dois verbos, e vale decidir com o orientador qual predomina: **desenvolver** (se a ênfase for no processo construído) ou **avaliar** (se a ênfase for na validação do indicador). Uma formulação que junta os dois em uma ação só costuma funcionar melhor — algo como "avaliar a viabilidade de um indicador mensal de vigor da vegetação, obtido por imagens de satélite, para os municípios do Agreste potiguar";
- diga **o que** é construído: um indicador mensal de vigor da vegetação, a partir do NDVI;
- diga **sobre qual território**: os municípios selecionados do Agreste potiguar;
- diga **para quê**: apoiar o monitoramento ambiental do observatório AgroAgreste;
- **não** empilhe ações. "Desenvolver, avaliar e integrar" são três objetivos, não um;
- **não** prometa o que não mediu. Se você não separou as áreas agrícolas com o MapBiomas, não escreva "áreas agrícolas" no objetivo geral — escreva "vegetação".

**Confira antes de entregar:** leia o objetivo geral e, logo depois, a primeira frase da sua Conclusão. Se as duas não estiverem falando da mesma coisa, uma delas está errada.

---

# 3. Objetivos Específicos
**Prazo: 24/11/2026 (com o Resumo e o Título)**

Ficam para o fim de propósito: eles descrevem o que foi **realmente alcançado**. Até lá, use uma versão provisória.

**Direcionamentos:**

- de 4 a 5 itens, verbo no infinitivo, minúscula no início, ponto e vírgula no fim de cada um e ponto no último;
- na **mesma ordem** das etapas da Metodologia e das seções dos Resultados;
- cada um **verificável**: na Conclusão você terá de mostrar, com número, que foi atingido;
- não confunda objetivo com tarefa. "Instalar as bibliotecas" não é objetivo específico.

**O que cada item deve cobrir** (redija com as suas palavras depois):

1. revisar a literatura sobre sensoriamento remoto, índices de vegetação e comportamento da vegetação do semiárido;
2. implementar um processo automatizado de obtenção, recorte, filtragem de nuvem e cálculo do NDVI a partir de imagens Sentinel-2;
3. construir séries temporais mensais de NDVI para os municípios selecionados, entre 2021 e 2025;
4. avaliar a relação entre o NDVI e a precipitação, testando diferentes defasagens, e comparar anos secos e chuvosos;
5. medir o custo computacional do processo e recomendar sua adoção pelo observatório AgroAgreste.

---

# 4. Referencial Teórico
**Prazo: 13/10/2026**

**Vídeo com a explicação (assista antes de começar):** https://youtu.be/8Qztq1Q5vb0

Comece a procurar referências **na primeira semana**. Este é o capítulo que mais consome tempo, e no seu caso ele tem uma dificuldade a mais: o tema é **interdisciplinar**, e você vai precisar ler tanto material de computação quanto de sensoriamento remoto e de agronomia.

Uma regra prática resolve metade dos problemas: **tudo o que vai aparecer nos Resultados precisa estar explicado antes**. Se a tabela mostra "correlação com defasagem de dois meses", esses conceitos têm de estar definidos aqui.

## 4.1 Agricultura familiar e o Agreste potiguar

**Pesquise:** "agricultura familiar", Lei nº 11.326/2006 (que define a agricultura familiar no Brasil), Censo Agropecuário 2017 do IBGE, "Agreste potiguar", "semiárido brasileiro", delimitação do Semiárido pela SUDENE, "cultivo da mandioca no Rio Grande do Norte". Use também a referência já citada no `projeto.md` (Cousteau e Silva, 2013).

**Escreva:** o que caracteriza a agricultura familiar e seu peso no Agreste potiguar; as características do território (clima semiárido, chuva concentrada em poucos meses, irregularidade entre anos); e a dependência da produção em relação à chuva.

Esta subseção é o que amarra o seu trabalho técnico ao projeto. Ela justifica **por que** faz diferença monitorar a vegetação justamente aqui: em uma região de chuva regular, o NDVI varia pouco; no semiárido, ele varia muito, e essa variação carrega informação.

## 4.2 Sensoriamento remoto e imagens de satélite

**Pesquise:** "sensoriamento remoto", "resolução espacial, temporal e espectral", "reflectância", "correção atmosférica", "Sentinel-2", "Landsat", "MODIS". Para os fundamentos, procure os livros brasileiros consagrados da área — por exemplo, os de **Evlyn Novo** e de **Ponzoni e Shimabukuro** — e a tradução do livro de **Jensen**. Para o Sentinel-2, use a documentação oficial da Agência Espacial Europeia.

**Escreva:** o que é sensoriamento remoto e como um satélite "enxerga" — que ele mede a **energia refletida** pela superfície em diferentes faixas do espectro, inclusive faixas invisíveis ao olho humano.

Explique os **quatro tipos de resolução** e o que cada um significa na prática:

- **espacial**: o tamanho do pixel no chão (10, 20, 30 ou 250 metros). Determina o menor objeto distinguível — e é por isso que ela importa para a agricultura familiar, cujas áreas são pequenas;
- **temporal**: de quantos em quantos dias o satélite passa no mesmo lugar;
- **espectral**: quais faixas de luz o sensor mede;
- **radiométrica**: quantos níveis de intensidade ele distingue.

Explique também a diferença entre os **níveis de processamento** L1C e L2A do Sentinel-2, e por que o L2A (já corrigido dos efeitos da atmosfera) é o indicado para calcular índices de vegetação. Você usou o L2A — fundamente a escolha aqui.

Por fim, trate do **problema da nuvem**, que é central no seu trabalho: sensores ópticos não enxergam através de nuvem, e em região de estação chuvosa isso significa perder justamente os meses mais interessantes. Isso prepara o leitor para os meses sem dado que vão aparecer nos seus Resultados.

## 4.3 Índices de vegetação e o NDVI

**Pesquise:** "índice de vegetação", "NDVI", "*Normalized Difference Vegetation Index*". As referências fundamentais da área são **Rouse e colaboradores (1974)**, que propuseram o índice, e **Tucker (1979)**, publicado na *Remote Sensing of Environment*. Procure também o **SAVI**, proposto por **Huete (1988)** para áreas de vegetação rala — ele é especialmente pertinente ao seu caso.

**Escreva:** por que o NDVI funciona, explicando o mecanismo físico: a vegetação saudável **absorve** a luz vermelha para a fotossíntese e **reflete fortemente** o infravermelho próximo. Quanto maior a diferença entre as duas, maior o vigor. Apresente a fórmula e explique a faixa de valores, com a interpretação típica (água, solo exposto, vegetação rala, vegetação densa).

Explique **por que o índice é "normalizado"**: dividir pela soma faz o resultado ficar entre −1 e 1 e reduz o efeito de diferenças de iluminação entre imagens, o que é o que permite comparar datas diferentes. Esse detalhe é o que torna a série temporal possível, então vale um parágrafo.

E trate das **limitações do NDVI**, porque elas voltam na sua discussão:

- **saturação**: em vegetação muito densa, o índice para de crescer;
- **influência do solo**: quando a vegetação é rala e o solo aparece entre as plantas — exatamente o caso da caatinga — o solo interfere na medida. Foi para corrigir isso que o SAVI foi proposto. **Mencione isso aqui**, porque é a principal ressalva técnica do seu trabalho e um bom candidato a trabalho futuro.

## 4.4 Vegetação do semiárido, chuva e séries temporais de NDVI

Esta é a subseção que fundamenta a sua validação. Dedique atenção a ela.

**Pesquise:** "fenologia da caatinga", "vegetação decídua", "NDVI e precipitação", "séries temporais de NDVI", "*NDVI rainfall lag*", "resposta da vegetação à precipitação no semiárido", "monitoramento de secas por satélite". Busque na SciELO, no Google Acadêmico, na Revista Brasileira de Engenharia Agrícola e Ambiental, na revista *Remote Sensing* e nos anais do Simpósio Brasileiro de Sensoriamento Remoto (SBSR), que é o principal evento da área no Brasil.

**Escreva:** o comportamento da caatinga, que é uma vegetação **decídua** — perde as folhas na estiagem e rebrota rapidamente com as primeiras chuvas. Isso produz uma variação sazonal de NDVI muito mais forte do que em outros biomas, e é o que torna o índice um bom indicador nessa região.

Explique o conceito de **defasagem** (*lag*): a vegetação não responde à chuva no mesmo instante. Há um intervalo entre a chuva e o pico de verde, e a literatura costuma relatar respostas de algumas semanas a poucos meses. **Diga o que a literatura encontrou**, com a referência — porque na sua análise você vai comparar o seu resultado com esse valor esperado, e é essa comparação que valida o seu indicador.

Apresente também, brevemente, o uso de séries de NDVI para **monitoramento de secas**, citando o Monitor de Secas da ANA como exemplo de aplicação operacional no Brasil.

## 4.5 Trabalhos relacionados

**Pesquise:** trabalhos que tenham usado NDVI para monitorar vegetação ou lavouras no Nordeste, na caatinga ou no semiárido; trabalhos que relacionaram NDVI e precipitação; trabalhos sobre observatórios territoriais ou painéis de indicadores ambientais. Busque nos anais do **SBSR**, na **BDTD**, em repositórios de institutos federais e universidades, na SciELO e no Google Acadêmico.

Termos úteis: "NDVI caatinga", "NDVI semiárido precipitação", "monitoramento agrícola sensoriamento remoto Nordeste", "série temporal NDVI município".

**Escreva:** de 4 a 6 trabalhos, um parágrafo cada, dizendo qual área estudaram, qual satélite e qual período usaram, **como validaram** e quais as limitações.

Feche com um **quadro comparativo** entre esses trabalhos e o seu, com colunas como: área de estudo, satélite e resolução, período analisado, escala de agregação (pixel, município, bacia), forma de validação, e se o processo é automatizado e reprodutível.

**Esse quadro é a justificativa do seu trabalho.** O seu diferencial provavelmente vai aparecer em duas colunas: o **recorte municipal do Agreste potiguar**, que é o território do observatório, e o fato de o trabalho entregar um **processo automatizado e reprodutível** com medição do custo computacional — muitos trabalhos da área apresentam o resultado, mas não o caminho nem o custo para repeti-lo. Se você encontrar um trabalho que já faça exatamente isso na mesma região, avise o orientador: em outubro ainda dá tempo de ajustar o recorte.

## Regras para o referencial inteiro

- **Toda afirmação técnica precisa de referência.**
- **Não empilhe citações.** Explique com suas palavras, relacione os autores e ligue ao seu trabalho.
- **Documentação oficial** (ESA, NASA POWER, IBGE, MapBiomas) serve para descrever a fonte de dados, não para fundamentar conceito. Para conceito, use livro ou artigo.
- **Nada de blog ou site sem autoria** nas Referências. Você vai usar muito esse material para resolver problema técnico — isso é normal —, mas ele não entra na lista.
- **Nunca cite o que não leu.** Ferramentas de IA inventam referências com muita naturalidade, e nesta área elas inventam também valores de correlação e nomes de satélite. Confira tudo na fonte.
- Meta para este trabalho: **18 a 25 referências**, equilibradas entre o lado técnico e o lado ambiental/agrícola.

---

# 5. Metodologia
**Prazo: 20/10/2026**

Como o trabalho foi feito. Verbos no passado e linguagem impessoal ("foi realizado", "realizou-se"). Duas a três páginas.

**Pasta com metodologias prontas para consulta:** https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

## 5.1 Classificação da pesquisa

**Pesquise:** Gil (2017) e Prodanov e Freitas (2013) — referências completas no `README.md`. Leia os capítulos de classificação antes de escrever; não classifique de ouvido.

**Escreva:** a classificação pelos quatro critérios, **justificando cada uma** com uma frase ligada ao seu trabalho (o erro mais comum é só listar os rótulos). O enquadramento mais provável:

- **Natureza:** aplicada — o resultado responde a uma necessidade concreta do observatório AgroAgreste;
- **Objetivos:** exploratória e descritiva — investiga a viabilidade de uma técnica ainda não aplicada neste território e descreve o comportamento medido do indicador;
- **Abordagem:** quantitativa — todos os resultados são numéricos;
- **Procedimentos:** pesquisa bibliográfica combinada com **pesquisa documental**, já que os dados são secundários e vêm de bases públicas oficiais. Alguns autores também aceitariam "experimental" para a parte de comparação com a chuva — **defenda a sua escolha** com o orientador.

## 5.2 Área de estudo

Esta subseção é obrigatória em trabalho com recorte territorial, e costuma faltar em trabalhos de iniciação.

**Escreva:** onde fica o Agreste potiguar, que municípios foram selecionados, **por que esses** e não outros, qual a área de cada um, e as características relevantes (clima, regime de chuvas, principais culturas, cobertura vegetal predominante).

**Um mapa de localização é praticamente obrigatório** aqui: o Brasil, com o Rio Grande do Norte destacado, e os municípios selecionados marcados. Você já tem os contornos do IBGE — é um gráfico a mais no `matplotlib`. Identificação em cima, fonte embaixo.

Informe também o **período analisado** (2021 a 2025) e justifique: cinco anos é o mínimo para ter anos secos e chuvosos na mesma série, e o Sentinel-2 tem cobertura consistente nesse intervalo.

## 5.3 Etapas do trabalho

**Escreva:** as etapas em ordem cronológica. Uma **figura com o fluxo do processamento** ajuda muito e é quase esperada em trabalho de sensoriamento remoto: busca no catálogo → seleção da imagem → recorte → máscara de nuvem → cálculo do NDVI → agregação mensal → série temporal → análise. Use o draw.io, que é gratuito.

As etapas:

1. levantamento bibliográfico;
2. definição da área de estudo e do período;
3. implementação do processo de obtenção e recorte das imagens;
4. implementação da máscara de nuvem e definição do critério de aceitação;
5. geração das séries temporais mensais de NDVI;
6. obtenção dos dados de precipitação;
7. análise da relação entre NDVI e precipitação, com defasagens;
8. comparação entre anos secos e chuvosos e entre municípios;
9. medição do custo computacional e elaboração da recomendação.

**Justifique as decisões que a banca ou o revisor vão questionar** — e neste trabalho elas são específicas:

- **por que uma imagem por mês**, e não todas as disponíveis: para manter o volume de dados compatível com a infraestrutura disponível, e porque o interesse é a variação sazonal, não a diária. Diga qual critério escolheu a imagem do mês (a de menor cobertura de nuvem);
- **por que o critério de X% de pixels válidos**: apresente a análise de sensibilidade que você fez na Sprint 3, comparando limiares, e a escolha final;
- **por que a média do município**, e não outra agregação: é a escala em que o observatório trabalha. Mas diga também que a média mistura usos da terra diferentes (lavoura, pastagem, caatinga, área urbana), o que é uma limitação declarada e o motivo de o MapBiomas aparecer nos trabalhos futuros;
- **por que os pixels de água não foram tratados à parte** (ou foram, se você tratou): açudes têm NDVI negativo e puxam a média para baixo. Se você não os removeu, diga isso.

---

# 6. Materiais e Métodos
**Prazo: 27/10/2026**

Vale a analogia da receita de bolo do `README.md`: **lista de ingredientes** mais **modo de preparo**. Em trabalho com dados de satélite, é esta seção que permite (ou impede) a reprodução — e revisores da área são exigentes com ela.

## 6.1 Materiais

**As fontes de dados** merecem uma tabela própria, com endereço e **data de acesso**:

| Fonte | O que forneceu | Detalhes a informar |
|---|---|---|
| Sentinel-2 L2A, via Microsoft Planetary Computer | Imagens de satélite | Bandas usadas e a resolução de cada uma; nome da coleção no catálogo |
| NASA POWER | Precipitação mensal | Nome exato do parâmetro, a unidade e o ponto de consulta (centro do município) |
| IBGE – API de malhas | Limites municipais | Versão da malha e o nível de detalhe |
| ANA – Monitor de Secas | Conferência dos anos secos | Período consultado |
| MapBiomas *(se usado)* | Uso e cobertura da terra | **Número da coleção** e ano |

**As ferramentas**, cada uma com **o que é**, **para que foi usada** e **por que foi escolhida**:

| Biblioteca | Para quê |
|---|---|
| `pystac-client` | Busca no catálogo de imagens |
| `planetary-computer` | Acesso aos arquivos de imagem |
| `rioxarray` / `rasterio` | Leitura e recorte das imagens |
| `shapely` | Manipulação dos limites municipais |
| `requests` | Acesso às APIs do IBGE e da NASA POWER |
| `pandas` | Organização das séries e cálculo das correlações |
| `matplotlib` | Gráficos e mapas |

**Informe as versões de tudo.** Em sensoriamento remoto, versão de biblioteca muda resultado com mais frequência do que se imagina.

**O ambiente de execução:** processador, memória RAM, tipo de disco, sistema operacional e a conexão de internet. A internet importa de verdade neste trabalho, porque parte do tempo medido é tempo de transferência — e você vai apresentar esses tempos.

**Declare também o que não foi usado e por quê:** não foi usado banco de dados, porque o volume de resultados cabe em arquivos CSV; não foi usado Google Earth Engine nem serviço pago de processamento, porque o objetivo incluía verificar a viabilidade em infraestrutura comum. Justificar o que você **não** usou mostra que a escolha foi consciente.

## 6.2 Métodos

**a) Seleção das imagens.** Como o catálogo foi consultado, o filtro de nuvem aplicado na busca, o critério de escolha da imagem do mês, e o que acontecia quando a imagem escolhida era reprovada (a tentativa com a segunda e a terceira menos nubladas).

**b) Recorte.** Como o limite municipal foi obtido e aplicado, e — este é um detalhe técnico que vale mencionar — que as imagens foram lidas em formato COG, o que permite transferir **apenas a janela de interesse** em vez da cena completa. Essa é a decisão que tornou o trabalho viável na infraestrutura disponível, e ela merece uma frase.

**c) Máscara de nuvem.** Qual camada foi usada (a classificação de cena do Sentinel-2), quais classes foram descartadas e por quê, o critério mínimo de pixels válidos e a análise de sensibilidade entre limiares.

**d) Cálculo do NDVI.** A fórmula, as bandas usadas com sua resolução, e como a agregação municipal foi feita (média e mediana dos pixels válidos).

**e) Dados de precipitação.** O parâmetro consultado, a unidade, o ponto de consulta e o período.

**f) Análise.** Como as defasagens foram construídas (dentro de cada município, com a série ordenada), qual coeficiente de correlação foi usado, como os meses sem dado foram tratados, e como os anos foram classificados em secos e chuvosos.

**g) Medição do custo.** Como o tempo e o volume transferido foram registrados, e em que condições de rede.

---

# 7. Resultados e Discussão
**Prazo: 10/11/2026**

A seção mais importante. Três a quatro páginas. Organize-a respondendo às **três perguntas** enunciadas na Introdução.

> **Regra sem exceção:** toda figura, tabela ou mapa é **anunciado no texto antes** de aparecer e **explicado depois**. Nunca duas figuras seguidas sem texto entre elas. Em trabalho com muitos mapas, esse cuidado é ainda mais importante.

## 7.1 Cobertura de dados obtida

Comece por aqui, porque é o que sustenta todo o resto. Tabela com, por município: meses processados, meses sem dado, e a distribuição dos meses sem dado ao longo do ano.

**Discuta:** os meses sem dado provavelmente se concentram na estação chuvosa, o que é esperado e é uma limitação real do satélite óptico. Comente quantos por cento da série foi perdida e o que isso significa para um observatório que pretenda usar o indicador operacionalmente. **Esse achado é um resultado, não uma falha** — e é uma informação de que a equipe do projeto precisa.

## 7.2 O ciclo anual da vegetação

A primeira pergunta. Apresente o gráfico da série temporal de NDVI, por município, e uma tabela com NDVI médio, mínimo, máximo e amplitude por município.

**Discuta:**

- **o padrão sazonal**: em que meses o NDVI sobe e desce, e se o padrão se repete nos cinco anos. Compare com o que a literatura descreve sobre a fenologia da caatinga — essa comparação é a sua primeira validação;
- **as diferenças entre municípios**: algum mantém NDVI mais alto na estiagem? Algum varia mais? Relacione com o que se sabe do território (mais agricultura, mais caatinga, presença de açudes, irrigação);
- **a amplitude**: a diferença entre o pico e o mínimo. Ela é a assinatura da vegetação decídua, e quanto maior, mais marcada é a sazonalidade.

Inclua também **um mapa de NDVI** de uma data do pico verde, para o leitor ver a distribuição espacial dentro do município — a média esconde essa variação.

## 7.3 A relação entre NDVI e chuva

A segunda pergunta, e o resultado central do trabalho.

Comece pelo **gráfico combinado**: NDVI em linha e chuva em barras, no mesmo eixo de tempo. A olho nu já se vê a vegetação respondendo com atraso. Provavelmente esta será a figura mais citada do seu artigo.

Depois a **tabela de correlações**, por município e por defasagem (sem defasagem, 1, 2 e 3 meses), e o gráfico de dispersão da defasagem de maior correlação.

**Discuta:**

- **qual defasagem deu a maior correlação**, e se ela é igual em todos os municípios;
- **compare com a literatura**: o valor que você encontrou está na faixa que os trabalhos da área relatam para o semiárido? Se estiver, você validou o seu indicador contra o conhecimento consolidado. Se não estiver, investigue e discuta por quê — pode ser característica do território, pode ser efeito do seu método;
- **a força da correlação**: um valor alto confirma que o indicador capta o que deveria captar;
- **as duas ressalvas honestas**: correlação não demonstra causa, e as duas séries têm sazonalidade, o que infla a correlação. Se você tiver calculado a correlação dentro de cada mês ao longo dos anos (removendo o efeito do calendário), apresente também esse número — ele é mais conservador e mais convincente.

## 7.4 Anos secos e anos chuvosos

A terceira pergunta. Tabela com o total de chuva e o NDVI médio de cada ano, por município, e a identificação dos anos extremos.

Os **dois mapas lado a lado** — mesmo mês, ano seco e ano chuvoso, **na mesma escala de cores** — são a figura mais imediata do artigo. Diga na legenda que a escala é idêntica nos dois, porque é isso que torna a comparação legítima.

**Discuta:**

- a diferença de NDVI entre os anos extremos, em número;
- **a conferência com o Monitor de Secas**: os anos que a sua análise apontou como secos foram reconhecidos como anos de seca pela fonte oficial? Se sim, você tem uma **validação externa e independente** do indicador, o que é um argumento forte. Diga isso com todas as letras;
- se houve algum ano em que NDVI e chuva não conversaram como esperado, e o que pode explicar.

## 7.5 Custo computacional

Tabela com tempo total, volume transferido, tempo médio por mês e volume por mês, por município. E a projeção: quanto custaria rodar o processo para todos os municípios do Agreste, mensalmente.

**Discuta:** a viabilidade operacional. Destaque a decisão de projeto de **não armazenar as imagens**, que mantém a necessidade de disco praticamente nula. Um observatório de projeto de extensão não tem infraestrutura de servidor de imagens, e mostrar que o indicador cabe em uma máquina comum é um resultado prático relevante.

## 7.6 Limitações do trabalho

Subseção curta e honesta. Reconhecer limite aumenta a confiança no trabalho:

- **nuvem**: meses perdidos, concentrados na estação chuvosa, que é justamente o período mais relevante;
- **resolução espacial**: um pixel de 20 m pode misturar culturas diferentes em propriedades pequenas, o que é a realidade da agricultura familiar;
- **a média municipal mistura usos da terra**: lavoura, pastagem, caatinga, área urbana e água entram na mesma conta. Foi por isso que a separação por classes do MapBiomas foi identificada como o próximo passo;
- **limitação do próprio NDVI**: a influência do solo em vegetação rala, que é característica da caatinga, e para a qual existem índices alternativos como o SAVI;
- **a precipitação vem de um único ponto** por município (o centro), enquanto a chuva no semiárido é notoriamente irregular no espaço;
- **período de cinco anos**, que é curto para afirmações sobre tendência — e aqui vale ser explícito: o trabalho descreve variação sazonal e interanual, **não** tendência de longo prazo.

Depois de listar, note que várias dessas limitações incidem igualmente sobre todos os municípios e anos analisados, o que preserva a validade das **comparações** feitas, ainda que os valores absolutos devam ser lidos com cautela.

---

# 8. Conclusão
**Prazo: 17/11/2026**

Curta e direta. Nada de resultado, conceito ou citação que não tenha aparecido antes.

**Escreva, nesta ordem:**

1. **Retomada do problema e do objetivo geral**, afirmando que ele foi alcançado **e dizendo por quê, com número**: "[...] foi alcançado, uma vez que o processo desenvolvido gerou séries mensais de NDVI para N municípios ao longo de cinco anos, com correlação de X com a precipitação defasada em Y meses."

2. **Um comentário por objetivo específico**, na mesma ordem, cada um apontando o resultado que o comprova.

3. **A resposta às três perguntas** da Introdução, uma ou duas frases cada: o indicador reproduz o ciclo anual? responde à chuva, e com que atraso? distingue anos secos de chuvosos?

4. **Contribuições:** um processo automatizado, documentado e reprodutível de geração de um indicador de vegetação para escala municipal; a série temporal de NDVI dos municípios analisados, que pode ser reaproveitada por outros trabalhos do projeto; a medição do custo computacional, que informa a decisão de adoção; e uma recomendação técnica para o observatório AgroAgreste.

5. **Limitações e dificuldades:** retome brevemente as limitações e acrescente as dificuldades reais do desenvolvimento — a cobertura de nuvem, o tempo de transferência das imagens, a definição do critério de pixels válidos, o alinhamento entre bandas de resoluções diferentes. É aqui que o `docs/diario.md` das sprints se paga.

6. **Trabalhos futuros**, concretos e ligados ao que você encontrou:
   - separar o NDVI por classe de uso da terra, com o MapBiomas, para distinguir lavoura de caatinga (esta é a principal);
   - estender o processo a todos os municípios do Agreste e integrá-lo ao observatório AgroAgreste;
   - testar índices alternativos, como o SAVI, mais adequados a vegetação rala sobre solo exposto;
   - ampliar a série histórica usando também imagens Landsat, que cobrem décadas anteriores;
   - comparar o indicador com os dados de produção agrícola do IBGE, para verificar se o NDVI antecipa variações de safra;
   - validar com observações de campo, quando o projeto dispuser delas.

**Não escreva** que "o NDVI mede a produtividade agrícola" — ele mede vigor da vegetação, que é outra coisa. E não generalize para o semiárido inteiro o que você mediu em alguns municípios do Agreste potiguar.

---

# 9. Resumo, Título e revisão final
**Prazo: 24/11/2026**

## 9.1 Resumo

Escrito **por último**, depois de o texto todo estar aprovado pelo orientador. Parágrafo único, 150 a 500 palavras, linguagem impessoal, sem citações, sem siglas pouco conhecidas e sem menção a figuras ou tabelas (NBR 6028:2021).

Uma ou duas frases para cada item:

1. **contexto e problema:** a dependência da agricultura familiar do Agreste em relação à chuva e a ausência de monitoramento contínuo da vegetação;
2. **objetivo:** o que o trabalho se propôs a construir e avaliar;
3. **método:** imagens Sentinel-2, N municípios, 2021 a 2025, máscara de nuvem, NDVI mensal, comparação com precipitação;
4. **resultados:** os números principais — correlação e defasagem, diferença entre anos secos e chuvosos, cobertura de dados obtida;
5. **conclusão:** a viabilidade do indicador e o encaminhamento para o observatório.

**Coloque números no resumo.** Em um trabalho que mede coisas, resumo sem número é resumo fraco — e é o resumo que faz alguém decidir se lê o resto.

O **Abstract** é a versão em inglês. Os termos da área têm forma consagrada (*remote sensing*, *vegetation index*, *time series*, *cloud masking*, *smallholder farming*); use-as, e não a tradução literal. Não entregue tradução automática sem revisar.

**Palavras-chave** (3 a 5), separadas por ponto e vírgula. Campo de ideias: sensoriamento remoto; NDVI; agricultura familiar; semiárido; Sentinel-2; série temporal. Escolha os termos pelos quais alguém **procuraria** o seu trabalho, equilibrando o lado técnico e o territorial.

## 9.2 Título

**Última coisa a ser definida**, em acordo com o orientador. Deve indicar **o que foi feito** e **onde**, e combinar com o objetivo geral.

Pontos a cobrir: a ação (monitoramento, avaliação ou análise), o objeto (vigor da vegetação por NDVI, a partir de imagens Sentinel-2) e o recorte territorial (municípios do Agreste potiguar). Se houver subtítulo, separe com dois-pontos. Em trabalho com recorte territorial, **incluir o território no título é quase obrigatório** — é o que faz o trabalho ser encontrado por quem pesquisa a região.

Evite título genérico demais ("Uso de satélites na agricultura") e não prometa mais do que o trabalho mediu: se você não separou áreas agrícolas, não use "áreas agrícolas" no título.

## 9.3 Revisão final — checklist

Além do checklist do `README.md`:

- [ ] O objetivo geral, os objetivos específicos, as seções dos Resultados e os parágrafos da Conclusão estão na mesma ordem e falando das mesmas coisas?
- [ ] As três perguntas da Introdução foram respondidas nos Resultados e retomadas na Conclusão?
- [ ] Todos os números citados no Resumo, nos Resultados e na Conclusão são **exatamente** os mesmos?
- [ ] Toda métrica que aparece nos Resultados foi explicada no Referencial?
- [ ] O mapa de localização da área de estudo está presente?
- [ ] Todos os mapas comparativos usam a **mesma escala de cores**, e isso está dito na legenda?
- [ ] Todas as fontes de dados têm endereço e **data de acesso**?
- [ ] As bandas usadas, suas resoluções e o nível de processamento (L2A) estão informados?
- [ ] O critério de nuvem e o limiar de pixels válidos estão justificados?
- [ ] Os meses sem dado estão informados, e não escondidos?
- [ ] Toda figura e tabela é citada no texto antes de aparecer e explicada depois?
- [ ] Todas as figuras e tabelas têm identificação em cima, centralizada, e fonte embaixo?
- [ ] Os gráficos têm unidade no eixo e legenda?
- [ ] O ambiente de execução está descrito (máquina, sistema, versões, internet)?
- [ ] A seção de limitações está presente e honesta?
- [ ] As siglas (NDVI, SAVI, STAC, COG, IBGE, ANA, SUDENE, CEP) foram escritas por extenso na primeira ocorrência?
- [ ] A numeração das seções está sem ponto após o número ("2.3 Índices de vegetação e o NDVI")?
- [ ] O texto está impessoal e no passado?
- [ ] Está declarado que os dados são públicos e secundários e que não houve participantes humanos?
- [ ] Todos os comentários do orientador no documento do Drive foram respondidos?
- [ ] A versão final foi nomeada no histórico de versões do Drive?

---

## Referências mínimas a garantir

Como o trabalho é interdisciplinar, o referencial precisa ser equilibrado:

**Lado ambiental e territorial:**

- **2 a 3 fontes sobre agricultura familiar e o Agreste potiguar** (Seção 4.1), incluindo dados do IBGE e a Lei nº 11.326/2006;
- **2 a 3 fontes sobre caatinga, semiárido e regime de chuvas** (Seção 4.4);

**Lado técnico:**

- **3 a 4 obras sobre sensoriamento remoto** (Seção 4.2), incluindo pelo menos um livro de referência da área;
- **3 a 4 obras sobre índices de vegetação** (Seção 4.3), obrigatoriamente com os trabalhos fundadores do NDVI e, se possível, o do SAVI;
- **4 a 6 trabalhos relacionados** (Seção 4.5), de preferência sobre o Nordeste ou o semiárido;

**Obrigatórias:**

- **2 obras de metodologia científica** — Gil (2017) e Prodanov e Freitas (2013), já no `README.md`;
- **a documentação oficial das fontes de dados** — Sentinel-2 (ESA), NASA POWER, IBGE, e MapBiomas se tiver sido usado.

Anote a referência completa de **tudo** o que ler, na seção de Referências do documento do Drive, desde o primeiro dia. Zotero e Mendeley ajudam a montar, mas confira cada entrada contra a NBR 6023:2018 antes de entregar: esses gerenciadores erram com frequência.
