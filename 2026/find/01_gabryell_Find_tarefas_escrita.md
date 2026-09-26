# Plano de escrita do TCC – Gabryell (Projeto FIND)

**Projeto pai:** FIND – Plataforma e Aplicativo Móvel para Gestão de Objetos Perdidos e Encontrados (ver [projeto.md](../projeto.md)).

**Temática:** avaliação de técnicas para a **correspondência automática entre itens perdidos e encontrados** — um mecanismo que sugere correspondências entre um objeto cadastrado como perdido e outro cadastrado como encontrado, usando **técnicas clássicas de similaridade textual e visual, sem inteligência artificial**.

**Repositórios de referência:**

- Projeto Web: https://github.com/gabryellgs/projeto-find — o experimento é feito **dentro dele**, na *branch* `tcc-correspondencia`, em uma app Django nova chamada `correspondencia` (ver o [plano de desenvolvimento](01_gabryell_Find_tarefas_desenvolvimento.md));
- Projeto Mobile: https://github.com/gabryellgs/find-app (fora do escopo deste trabalho).

**Base de estilo e de normas ABNT:** o arquivo [README.md](../../../README.md) deste repositório. Tudo o que está lá vale aqui — estrutura, citações, referências, figuras, tabelas e formatação. Este documento **não repete** as regras da ABNT; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copie estas frases para o TCC. Elas dizem sobre o que é cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você leu.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do TCC **já foi criado e compartilhado pelo coordenador** em uma pasta do Google Drive. Você não cria arquivo novo nem trabalha em cópia local.

- **Escreva sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico do Drive é o que me permite ver o que mudou de uma semana para outra.
- **Não crie cópias** ("TCC v2", "TCC final", "TCC final revisado"). O Drive já guarda tudo em **Arquivo → Histórico de versões**.
- **Marque cada entrega no histórico:** **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 02/10`.
- **Avise por mensagem quando entregar.** Eu não fico olhando o documento; preciso saber que há algo novo.
- **Comentário se responde, não se apaga — e quem resolve sou eu.** Ao atender um comentário, responda na própria conversa dizendo o que foi feito (por exemplo, "Reescrevi o segundo parágrafo e incluí a referência pedida"). **Não clique em "Resolver":** eu confiro a alteração e, se estiver atendida, marco como resolvido; se não estiver, deixo um novo comentário na mesma conversa.
- **Figuras e tabelas:** cole a figura no documento e guarde o arquivo original (PNG em 300 dpi, gerado pelo comando `avaliar`) em uma subpasta `figuras/` da mesma pasta do Drive.

---

## Cronograma de entregas

Data de referência: **25/09/2026**. Cada prazo conta a partir da conclusão da etapa anterior; as datas abaixo consideram que cada etapa é concluída no prazo. Entregar antes é bem-vindo.

| # | Entrega | Duração | Prazo | Tamanho aproximado |
|---|---|---|---|---|
| 1 | Introdução e Objetivo Geral | 1 semana a partir de hoje | **02/10/2026** (sexta-feira) | 2 a 3 páginas |
| 2 | Referencial Teórico | 2 semanas após a Introdução | **16/10/2026** (sexta-feira) | 8 a 12 páginas |
| 3 | Metodologia | 1 semana após o Referencial | **23/10/2026** (sexta-feira) | 2 a 3 páginas |
| 4 | Materiais e Métodos | 1 semana após a Metodologia | **30/10/2026** (sexta-feira) | 5 a 8 páginas |
| 5 | Resultados e Discussão | 2 semanas após Materiais e Métodos | **13/11/2026** (sexta-feira) | 8 a 12 páginas |
| 6 | Conclusão | 1 semana após os Resultados | **20/11/2026** (sexta-feira) | 1 a 2 páginas |
| 7 | Resumo, Objetivos Específicos e Título | 1 semana após a Conclusão | **27/11/2026** (sexta-feira) | 1 página |

**Escrita e desenvolvimento andam juntos.** O [plano de desenvolvimento](01_gabryell_Find_tarefas_desenvolvimento.md#8-cronograma) foi montado para que cada seção tenha material quando você for escrevê-la:

- a **Metodologia (23/10)** descreve o protocolo dos dados, que fica pronto na semana 2;
- **Materiais e Métodos (30/10)** descreve as estratégias, implementadas nas semanas 3 e 4;
- os **Resultados (13/11)** usam as tabelas e os gráficos fechados até 30/10 — você tem **duas semanas inteiras** só para analisar e escrever. **Cole cada tabela no documento assim que ela sair do comando**, mesmo sem o texto de análise. Tabela no lugar é meia seção escrita.

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Texto pela metade dá para comentar; texto que não chega, não.
- Cada entrega é: seção escrita + revisão feita com o [checklist das orientações gerais](../../../README.md#checklist-antes-de-enviar-uma-versão-ao-orientador) + versão nomeada no histórico + aviso por mensagem.
- Responda a **todos** os comentários da entrega anterior, dizendo o que foi feito, antes de avisar sobre a próxima.

---

## Como escrever cada seção (vale para todas)

Siga sempre estes cinco passos. Eles evitam a folha em branco e o texto sem referência.

1. **Leia as orientações da seção** neste documento e anote as perguntas que ela precisa responder.
2. **Pesquise e fiche.** Para cada fonte lida, anote em um arquivo à parte: a referência completa, a página e **uma ou duas frases, com as suas palavras**, sobre o que ela diz de útil. Esse fichamento é o que você vai citar depois.
3. **Monte o esqueleto.** Antes de escrever, coloque no documento **uma linha por parágrafo**, dizendo o assunto de cada um e quais fontes ele vai citar. Ex.: "§1 – perda de objetos em locais de grande circulação (números do metrô – fonte X)".
4. **Escreva um parágrafo por vez**, transformando cada linha do esqueleto em um parágrafo de 4 a 8 linhas: uma frase que apresenta a ideia, frases que a desenvolvem (com citação) e uma frase que liga ao próximo parágrafo.
5. **Revise** com o checklist das orientações gerais e **leia o texto em voz alta**. Frase que você não consegue ler de uma vez está longa demais.

**Quantas referências?** Como regra prática: a Introdução com 6 a 10; o Referencial com 15 a 25; o TCC inteiro com pelo menos 25. Dê preferência a livros, artigos de eventos e periódicos e documentação oficial. Blogs e vídeos só em último caso.

---

## Que tipo de trabalho é este

Um **TCC no modelo ABNT**, com o método de **pesquisa experimental**: você constrói um conjunto de dados com gabarito, implementa algumas estratégias de correspondência e as compara com métricas objetivas. Escreva pensando no TCC; depois de aprovado, vamos **extrair dele um artigo** (seção 10).

Os artigos dos eventos e revistas da Sociedade Brasileira de Computação (SBC) estão na SBC OpenLib (SOL): https://sol.sbc.org.br. **Antes de começar a escrever, leia pelo menos três artigos experimentais** publicados lá — de preferência, trabalhos que comparam técnicas de busca ou de recomendação. Eles mostram o nível de detalhe e o tipo de tabela esperados.

Quatro coisas fazem a diferença entre um relatório de sistema e um trabalho de pesquisa:

1. **O objeto do trabalho não é o FIND.** É a **avaliação das técnicas de correspondência**. O FIND é o **cenário real** que dá origem ao problema e à linha de base (a heurística que ele já usa).
2. **Toda afirmação sobre desempenho precisa de um número** vindo do experimento, e toda afirmação sobre uma técnica precisa de uma referência. Frases como "o algoritmo encontra os objetos com precisão", sem métrica, não se sustentam.
3. **"Sem IA" é uma escolha, e precisa ser defendida.** O trabalho mostra até onde técnicas clássicas, leves e explicáveis conseguem chegar — sem GPU, sem custo de API, sem enviar fotos a terceiros e com uma pontuação que dá para explicar ao usuário.
4. **O experimento tem de dar para repetir.** Semente fixa, versões fixas, conjunto de dados descrito e repositório com o passo a passo.

Estrutura sugerida:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Recuperação de informação e sua avaliação
2.2 Similaridade de textos
2.3 Similaridade de imagens
2.4 Trabalhos relacionados
3 METODOLOGIA
4 MATERIAIS E MÉTODOS
4.1 Materiais
4.2 Métodos
5 RESULTADOS E DISCUSSÃO
6 CONCLUSÃO
REFERÊNCIAS
```

A Introdução e a Metodologia são escritas em **texto corrido, sem subtítulos**: a organização vem da ordem dos parágrafos, e não de subseções.

---

## O experimento em uma página

Use este resumo como mapa. Os detalhes de implementação estão no [plano de desenvolvimento](01_gabryell_Find_tarefas_desenvolvimento.md).

**A ideia.** A correspondência é tratada como uma **busca**: a **consulta** é o item perdido, os **documentos** são os itens achados, e cada estratégia ordena os achados por uma pontuação. Como os dados têm gabarito, dá para medir **em que posição** cada estratégia colocou o achado correto.

**O que já existe no FIND (linha de base).** A função `_calcular_match_score` (`mainpage/views.py`) pontua cada item achado para um item perdido: **categoria igual (35 pontos) + proporção de palavras do título em comum (até 40) + proporção de palavras da descrição em comum (até 25)**, e mostra até **6 sugestões** com pontuação **≥ 30**. A busca por imagem (`buscar_por_imagem`, `items/models.py`) combina **pHash** e **histograma de cor HSV**. Nenhuma das duas foi avaliada.

**As estratégias comparadas:**

| Código | Estratégia | Fonte de evidência |
|---|---|---|
| B0 | Heurística atual do FIND (linha de base), chamada diretamente | Categoria + palavras em comum |
| T1 | TF-IDF com similaridade do cosseno, sobre trechos de 3 a 5 letras | Texto |
| V | pHash + histograma de cor HSV (como no FIND) | Imagem |
| F | Soma ponderada: 0,6 × T1 + 0,3 × V + 0,1 × categoria; avaliada **com foto** e **sem foto** | Combinação |

Todas as configurações e os pesos são **fixados antes** do experimento e não são ajustados depois.

**Os dados.** 40 objetos reais fotografados por você. Cada objeto vira três itens: um **achado** (foto "de quem achou" e descrição padrão), um **perdido** (foto "do dono", tirada em outro lugar, ângulo e luz, e descrição escrita de outro jeito) e um **distrator "quase igual"** (achado sem foto, com a mesma descrição, mas outra cor). Total: 40 perdidos e 80 achados. Os perdidos são divididos em **4 grupos de 10**, cada um com um tipo de variação no texto: nenhuma, sinônimo, erro de digitação e falta de acento. O gabarito existe **por construção**.

**As métricas.** Recall@1, Recall@6 (6 é o número de sugestões que o FIND mostra) e MRR; as mesmas métricas por grupo de variação (robustez); e o tempo por consulta com 1.000 itens cadastrados.

---

# 1. Introdução
**Prazo: 02/10/2026**

**Texto corrido, sem subtítulos.** Não crie itens como "Contextualização" ou "Problemática" dentro da Introdução: os blocos abaixo indicam **a ordem dos parágrafos** (a sequência fixa do [README.md](../../../README.md#introdução)), e a passagem de um bloco para o outro deve ser feita com frases de transição. Duas a três páginas.

Cada bloco traz **as perguntas que ele precisa responder**. Se, ao reler o bloco, alguma pergunta ficou sem resposta, falta um parágrafo ou uma referência.

**Primeiro bloco — contexto (2 a 3 parágrafos)**

*Perguntas que o bloco responde:* Onde as pessoas mais perdem objetos? Quantos objetos são perdidos e quantos voltam para o dono? Como os achados e perdidos funcionam hoje? O que já existe de digital?

*Pesquise sobre:*

- a perda de objetos em locais de grande circulação: instituições de ensino, transporte público, aeroportos e eventos. Procure números em fontes confiáveis — relatórios de empresas de metrô e de aeroportos, notícias de grandes veículos que citem a fonte, artigos. Ex.: quantos objetos o metrô de São Paulo recebe por ano e quantos são devolvidos. **Não use números sem fonte**;
- o que acontece com os objetos que ninguém procura (doação, descarte, leilão);
- plataformas digitais de achados e perdidos e como elas funcionam.

*Fale sobre:* o processo tradicional (balcão, caderno, mural e grupos de mensagens), que depende de alguém **procurar manualmente**; a digitalização desse processo, que centraliza os registros, mas quase sempre como um **mural com busca manual**; e a ideia de o próprio sistema **sugerir** as correspondências, como sistemas de recomendação fazem em outros domínios.

**Segundo bloco — o problema (2 parágrafos)**

*Perguntas que o bloco responde:* Por que é difícil encontrar automaticamente o par certo? Por que a comparação por palavras em comum não basta? Alguém mede se essas sugestões acertam?

O problema do trabalho é **encontrar automaticamente o par certo**, e não "as pessoas perdem objetos".

*Fale sobre:*

- quem perdeu e quem achou **descrevem o mesmo objeto de jeitos diferentes**: palavras diferentes ("garrafa" × "squeeze"), erros de digitação, falta de acento; as fotos são tiradas em lugares, ângulos e luz diferentes; e existem **objetos muito parecidos** entre si (várias garrafas azuis);
- a comparação por **palavras em comum** — como a do FIND — falha exatamente nesses casos. Dê **um** exemplo curto ("squeeze azul" e "garrafa azul" têm só uma palavra em comum, e ela é a cor);
- a **falta de avaliação**: sistemas que anunciam "correspondência automática" raramente medem se ela acerta.

**Terceiro bloco — caminhos possíveis (2 parágrafos)**

*Perguntas que o bloco responde:* Que tipos de técnica poderiam resolver o problema? Por que olhar primeiro para as técnicas clássicas? O que ainda não foi estudado?

*Pesquise sobre:* recuperação de informação (a correspondência vista como um problema de **ranqueamento**); TF-IDF; comparação de imagens por hash perceptual e por histograma de cor; técnicas baseadas em aprendizado de máquina (*embeddings*, redes neurais).

*Fale sobre:*

- as duas famílias de soluções: as **técnicas clássicas** (leves e explicáveis) e as **técnicas de IA** (mais poderosas, mas que exigem modelos grandes, GPU ou APIs pagas, enviam dados a terceiros e produzem pontuações difíceis de explicar);
- por que, para instituições com pouca infraestrutura — como um campus de instituto federal —, faz sentido saber **até onde as técnicas clássicas conseguem chegar** antes de adotar IA;
- **o que falta** na literatura: avaliações controladas de técnicas clássicas **de texto e de imagem**, com **textos curtos em português**, no domínio de achados e perdidos. **Confirme essa lacuna na revisão da literatura** (seção 4.4); se encontrar um trabalho que já faça isso, ajuste a contribuição.

**Quarto bloco — a solução estudada (1 a 2 parágrafos)**

*Perguntas que o bloco responde:* O que exatamente este trabalho faz? Com o que as técnicas são comparadas?

*Fale sobre:* o mecanismo de correspondência (recebe um item perdido e devolve os itens achados ordenados, usando texto, imagem e categoria) e o que **este trabalho** faz: constrói um conjunto de avaliação com gabarito; compara uma técnica textual, a técnica visual já presente no FIND e uma combinação delas com a heurística atual do FIND; e analisa o efeito de sinônimos, erros de digitação, falta de acento e falta de foto. **Não antecipe resultados** que ainda não existem.

**Quinto bloco — vínculo com o projeto e escopo (1 parágrafo)**

*Perguntas que o bloco responde:* De onde veio o trabalho? Qual foi a sua participação? O que fica de fora?

*Fale sobre:* o histórico do FIND (desde novembro de 2025, inicialmente para o IFRN Campus Canguaretama), a equipe, o projeto institucional ao qual ele está vinculado (nome e edital) e **a sua participação no desenvolvimento**; que a correspondência automática estava prevista como **evolução futura** e que este trabalho a transforma em objeto de pesquisa; que o experimento foi feito como um **módulo separado dentro do próprio FIND**, sem alterar o sistema em uso; e o que **não** é escopo: técnicas de IA, geolocalização, notificações e o aplicativo móvel. Cite o trabalho paralelo do João Gabriel sobre a arquitetura do FIND.

**Fechamento — pergunta de pesquisa e contribuições (1 parágrafo)**

**Pergunta principal:** técnicas clássicas de similaridade textual (TF-IDF) e visual (hash perceptual e histograma de cor), isoladas ou combinadas, melhoram a sugestão de correspondências entre itens perdidos e encontrados em relação à heurística atual do FIND?

Desdobre em três questões de pesquisa (QP), que vão organizar os Resultados:

- **QP1:** a técnica textual (TF-IDF) supera a heurística atual do FIND?
- **QP2:** a técnica visual usada no FIND reconhece o mesmo objeto fotografado em condições diferentes?
- **QP3:** a combinação de texto, imagem e categoria supera as técnicas isoladas, e como ela se comporta diante de sinônimos, erros de digitação, falta de acento e falta de foto?

Termine com as **contribuições**, em texto corrido e ligadas por "(i)", "(ii)"..., como é comum em artigos de computação: um conjunto de avaliação com gabarito, com textos em português; a avaliação de técnicas clássicas tendo como linha de base uma heurística em uso; e a análise do efeito de cada tipo de variação.

**Antes de entregar, confira:** os cinco blocos estão na ordem? Todo número tem fonte? A pergunta de pesquisa aparece no último parágrafo? Não há subtítulos dentro da Introdução?

---

# 2. Objetivo Geral
**Prazo: 02/10/2026** (junto com a Introdução)

- Uma frase, com **um único verbo principal**, coerente com a pergunta de pesquisa (regras em [README.md](../../../README.md#objetivo-geral));
- o objeto do objetivo é **a avaliação das técnicas de correspondência**, e não "desenvolver um sistema de achados e perdidos";
- estrutura para você completar:

> "O objetivo principal do presente trabalho consiste em avaliar [...] para a sugestão automática de correspondências entre itens perdidos e encontrados, comparando [...] com a heurística utilizada pela plataforma FIND por meio de [...]."

Verbos que combinam: **avaliar**, **comparar**. Evite "desenvolver" e "implementar": a implementação é o meio, e não o fim.

**Teste rápido:** leia a pergunta de pesquisa e, em seguida, o objetivo geral. O objetivo tem de soar como "o que eu vou fazer para responder a essa pergunta".

---

# 3. Objetivos Específicos

**Não escreva agora.** Eles serão entregues no final (27/11/2026), junto com o Resumo e o Título, para refletirem o que foi **realmente feito**. Siga as regras das orientações gerais: 3 a 5 itens, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Verbos e temas que combinam com este trabalho:

- **identificar**, na literatura, técnicas clássicas de similaridade ...;
- **construir** um conjunto de avaliação com gabarito ...;
- **implementar** estratégias de correspondência textual, visual e combinada ...;
- **comparar** o desempenho das estratégias ... por meio de métricas de recuperação de informação ...;
- **analisar** o efeito das variações ... e o tempo de resposta ...

Não transforme funcionalidades em objetivos (por exemplo, "mostrar seis sugestões na tela do item").

---

# 4. Referencial Teórico
**Prazo: 16/10/2026**

Antes de começar, assista ao vídeo sobre Referencial Teórico: https://youtu.be/8Qztq1Q5vb0.

**Regra de ouro:** explique **somente os conceitos que aparecem depois nos Resultados**. Se "MRR" vai aparecer em uma tabela dos Resultados, o leitor precisa ter aprendido aqui o que é MRR. Bibliotecas (Django, scikit-learn, ImageHash) **não** ganham seção própria: elas são apresentadas em Materiais e Métodos.

**Use exemplos do próprio domínio** para explicar cada técnica — "mochila preta" × "bolsa preta", "squeeze" × "garrafa" —, em vez de exemplos abstratos. Cada subseção deve terminar dizendo **o que a técnica consegue e o que ela não consegue** no problema deste trabalho.

**Sugestão de organização das duas semanas:**

| Quando | O que fazer |
|---|---|
| 1ª semana, início | Ler os capítulos indicados do Manning e fichar a seção 4.1 |
| 1ª semana, fim | Escrever 4.1 e 4.2 |
| 2ª semana, início | Escrever 4.3 e fazer as buscas da seção 4.4 |
| 2ª semana, fim | Escrever 4.4, montar o quadro comparativo e revisar tudo |

## 4.1 Recuperação de informação e sua avaliação (2 a 3 páginas)

**Pesquise sobre:** consulta, documento e relevância; o problema de **ranqueamento**; coleções de teste com gabarito (paradigma de Cranfield); as métricas Recall@k e MRR.

**Fale sobre:**

- por que a correspondência perdido × achado pode ser tratada como uma busca em que a **consulta é o item perdido** e os **documentos são os itens achados**;
- o que é uma coleção de teste com gabarito e por que ela permite comparar técnicas de forma justa;
- o que cada métrica significa, com a fórmula e **um exemplo numérico** (ex.: três consultas com o correto em 1º, 2º e 4º lugar), e o que ela diz ao usuário (Recall@6 = a chance de o dono **ver** o seu objeto entre as 6 sugestões).

## 4.2 Similaridade de textos (2 a 3 páginas)

**Pesquise sobre:** pré-processamento de textos em português (tokenização, *stopwords*, remoção de acentos); o modelo vetorial e a similaridade do cosseno; TF-IDF; n-gramas de caracteres; limitações da representação por "saco de palavras" (sinônimos); dificuldades dos **textos curtos**.

**Fale sobre:**

- o pré-processamento, com um exemplo de entrada e saída ("Óculos de sol, pretos!" → "oculos sol pretos");
- como um texto vira um vetor e como o cosseno mede a semelhança entre dois vetores (um desenho simples ajuda);
- o que o TF-IDF faz: valoriza os termos raros ("Stanley") e reduz o peso dos comuns;
- por que usar **trechos de letras** (n-gramas de caracteres) em vez de palavras inteiras: "garafa" e "garrafa" têm a maioria dos trechos em comum;
- o que **nenhuma** dessas técnicas resolve: elas não sabem que "squeeze" e "garrafa" são a mesma coisa. Essa limitação é o que justifica, mais adiante, citar as técnicas de IA como trabalho futuro.

## 4.3 Similaridade de imagens (2 a 3 páginas)

**Pesquise sobre:** representação digital de imagens e espaços de cor (RGB e HSV); histograma de cor e interseção de histogramas; hash perceptual (pHash) e distância de Hamming; combinação de pontuações (CombSUM).

**Fale sobre:**

- como uma imagem é representada no computador e por que o HSV separa a cor da iluminação;
- o que o histograma de cor captura (a "paleta" da foto) e o que ele perde (a forma e a posição);
- para que o hash perceptual foi criado (encontrar **a mesma imagem** redimensionada ou comprimida) e por que isso é diferente de encontrar **o mesmo objeto** em outra foto;
- por que o fundo e a luz podem pesar mais que o próprio objeto;
- **para fechar a seção, um parágrafo sobre combinar evidências:** por que somar as pontuações de texto e de imagem pode acertar mais do que cada uma sozinha, por que as pontuações precisam estar na mesma escala (de 0 a 1) e o que fazer quando uma delas não existe (item sem foto).

## 4.4 Trabalhos relacionados (2 a 3 páginas e um quadro)

**Onde buscar:** SBC OpenLib (SOL), IEEE Xplore, ACM Digital Library, Portal de Periódicos da CAPES e Google Acadêmico.

**Termos de busca** (use em português e em inglês):

- `"lost and found" AND (matching OR retrieval OR recommendation)`;
- `"lost and found" AND (system OR application)`;
- `"achados e perdidos" AND (sistema OR aplicativo)`;
- `"lost item" AND ("image retrieval" OR "text similarity")`;
- `"product matching" OR "record linkage"`;
- `"short text similarity" AND TF-IDF`.

**Como fazer:**

1. Rode cada busca e anote quantos resultados apareceram (isso vai para a Metodologia).
2. Leia título e resumo dos primeiros 20 a 30 resultados de cada busca e separe os que **comparam ou avaliam** alguma técnica de correspondência.
3. Escolha de **6 a 10 trabalhos** e leia cada um inteiro. Para cada um, preencha uma linha do quadro abaixo.
4. Escreva **um parágrafo por trabalho** (ou por grupo de trabalhos parecidos): o que fizeram, como avaliaram e o que falta em relação ao seu.

Muitos trabalhos sobre achados e perdidos **descrevem o sistema sem avaliá-lo**; isso reforça a lacuna, mas cite-os com cuidado. Trabalhos de *record linkage* e *product matching* são importantes porque resolvem um problema parecido (decidir se dois registros descrevem a mesma coisa).

Termine a seção com o **quadro comparativo**:

| Trabalho | Domínio | Texto? | Imagem? | Técnicas | Usa IA? | Avaliação (métricas) |
|---|---|---|---|---|---|---|
| Autor (ano) | ... | sim/não | sim/não | ... | sim/não | ... ou "não avalia" |
| **Este trabalho** | achados e perdidos | sim | sim | TF-IDF, pHash, histograma, combinação | não | Recall@1, Recall@6, MRR |

A última linha é o seu trabalho: o quadro deve deixar visível a lacuna que ele ocupa.

## Leituras de partida

Localize a fonte original, confira os dados e só depois inclua nas Referências:

- MANNING, C. D.; RAGHAVAN, P.; SCHÜTZE, H. *Introduction to Information Retrieval* (Cambridge University Press, 2008; disponível gratuitamente on-line) — capítulos 2, 6 e 8. **Comece por aqui**;
- BAEZA-YATES, R.; RIBEIRO-NETO, B. *Recuperação de informação: conceitos e tecnologia das máquinas de busca* (2. ed., Bookman, 2013);
- SALTON, G.; BUCKLEY, C. *Term-weighting approaches in automatic text retrieval* (Information Processing & Management, 1988);
- VOORHEES, E. M. *The TREC-8 Question Answering Track Report* (1999) — origem do MRR;
- CHRISTEN, P. *Data Matching* (Springer, 2012) — correspondência de registros;
- SWAIN, M. J.; BALLARD, D. H. *Color indexing* (International Journal of Computer Vision, 1991) — interseção de histogramas;
- ZAUNER, C. *Implementation and Benchmarking of Perceptual Image Hash Functions* (dissertação, 2010);
- GONZALEZ, R. C.; WOODS, R. E. *Processamento digital de imagens* (Pearson) — espaços de cor e histogramas;
- FOX, E. A.; SHAW, J. A. *Combination of multiple searches* (TREC-2, 1994) — CombSUM;
- BRASIL. Lei nº 13.709, de 14 de agosto de 2018 (Lei Geral de Proteção de Dados Pessoais) — para justificar o cuidado com os dados.

Regras de citação e de referência: [README.md](../../../README.md#como-citar-nbr-105202023) e [README.md](../../../README.md#referências).

---

# 5. Metodologia
**Prazo: 23/10/2026**

Antes de escrever, consulte as metodologias prontas na pasta de orientações anteriores: https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing.

**Texto corrido, sem subtítulos**, como na Introdução. Os blocos abaixo indicam a ordem dos parágrafos. Duas a três páginas. A Metodologia diz **como a pesquisa foi planejada**; os detalhes técnicos (fórmulas, parâmetros, versões) ficam para Materiais e Métodos.

**Primeiro bloco — classificação da pesquisa (1 a 2 parágrafos)**

*Fale sobre:* natureza **aplicada**; objetivo **explicativo** (busca entender por que uma técnica acerta ou erra); abordagem **quantitativa**, complementada por uma análise qualitativa dos erros; procedimentos: **pesquisa bibliográfica** e **pesquisa experimental**. Cite um autor de metodologia para cada classificação (por exemplo, Gil e Wazlawick — este último escreve sobre metodologia de pesquisa em computação).

Deixe claras as **variáveis do experimento**:

- **independentes** (o que muda): a estratégia de correspondência, o tipo de variação no texto e a presença ou não da foto;
- **dependentes** (o que é medido): Recall@1, Recall@6, MRR e tempo por consulta;
- **controladas** (o que fica igual): o mesmo conjunto de dados, a mesma semente, as mesmas versões das bibliotecas e as configurações das estratégias.

**Segundo bloco — pesquisa bibliográfica (1 parágrafo)**

*Fale sobre:* as bases consultadas, os termos de busca (seção 4.4), quantos trabalhos foram encontrados e quantos foram escolhidos, e os critérios de escolha (por exemplo: incluir trabalhos que avaliem técnicas de correspondência com alguma métrica; excluir trabalhos que usem exclusivamente IA, que ficam apenas citados na discussão).

**Terceiro bloco — o cenário, a linha de base e os dados (2 parágrafos)**

*Fale sobre:*

- a plataforma FIND como cenário do problema e a heurística atual como **linha de base**, chamada diretamente pelo experimento, sem reescrita. O experimento foi feito como um **módulo separado dentro do próprio FIND**, o que garante que a linha de base é a original e não interfere no sistema em uso;
- o conjunto de dados: objetos reais fotografados em duas condições; descrições geradas por *script* a partir de um catálogo, com **variações controladas** que imitam o modo como quem perdeu descreve o objeto; distratores "quase iguais"; gabarito por construção. Justifique por que os dados são controlados: permitem **isolar o efeito de cada variação** (algo impossível com dados reais) e evitam o uso de dados pessoais;
- por que **não há ajuste de parâmetros**: as configurações e os pesos foram definidos antes do experimento, com base na literatura e no funcionamento do FIND;
- os **cuidados éticos**: não há participantes humanos; as fotos são de objetos, sem pessoas ou documentos, e têm os metadados de localização removidos; os usuários donos dos itens são fictícios. Por isso a pesquisa não precisou de submissão ao Comitê de Ética (ver [Pesquisas com pessoas](../../../README.md#pesquisas-com-pessoas)).

**Quarto bloco — etapas do trabalho (1 parágrafo e uma figura)**

Descreva as etapas em ordem, com uma **figura do fluxo** (caixas ligadas por setas, feita no draw.io ou no próprio Google Docs):

1. revisão da literatura;
2. análise da correspondência existente no FIND;
3. construção do conjunto de avaliação;
4. implementação das estratégias;
5. avaliação das estratégias e medição do tempo;
6. análise dos erros.

A ordem dessas etapas é a ordem que os Objetivos Específicos vão seguir.

**Quinto bloco — planejamento da avaliação e ameaças à validade (1 parágrafo e um quadro)**

Apresente um **quadro** que ligue cada QP às estratégias comparadas e às métricas:

| QP | Estratégias comparadas | Métricas | Como é respondida |
|---|---|---|---|
| QP1 | B0 e T1 | Recall@1, Recall@6 e MRR | Comparação das métricas com a B0 |
| QP2 | ... | ... | ... |
| QP3 | ... | ... | ... |

Feche com as **ameaças à validade** que você já conhece: o conjunto é controlado e pequeno (40 perdidos, 10 por grupo); as variações do texto foram definidas pelo próprio pesquisador; as fotos foram tiradas por uma só pessoa e um só celular; as configurações e os pesos não foram otimizados. Elas voltam a ser discutidas nos Resultados.

---

# 6. Materiais e Métodos
**Prazo: 30/10/2026**

Relembre a analogia da receita de bolo do [README.md](../../../README.md#materiais-e-métodos): outra pessoa precisa conseguir **repetir o experimento** e obter os mesmos números. Aqui entram os detalhes que a Metodologia deixou de fora.

## 6.1 Materiais

Monte um **quadro-resumo** com as versões **efetivamente usadas** — copie do `requirements.txt` do FIND e do `correspondencia/requirements-tcc-versoes.txt`:

| Ferramenta | Versão | Finalidade no trabalho |
|---|---|---|
| Python | 3.12.x | Linguagem do FIND e dos experimentos |
| Django | ... | *Framework* do FIND; modelos de dados e comandos do experimento |
| SQLite | ... | Banco de dados local do FIND em desenvolvimento |
| NLTK | ... | Lista de *stopwords* do português |
| scikit-learn | ... | TF-IDF e similaridade do cosseno (T1) |
| Pillow / ImageHash / NumPy | ... | Tratamento das fotos, hash perceptual e histogramas (V) |
| pandas / matplotlib | ... | Tabelas e gráficos dos resultados |
| pytest / pytest-django | ... | Testes automatizados |
| Celular usado nas fotos | modelo | Captura das imagens |
| Computador dos experimentos | processador, memória, Windows | Necessário para interpretar os tempos medidos |

Depois do quadro, uma ou duas frases para cada biblioteca, dizendo o que ela é, com a citação da documentação oficial.

## 6.2 Métodos

Para cada item, responda sempre às mesmas três perguntas: **o que é, como foi feito e por que foi escolhido**. Use esta ordem:

1. **Organização do experimento no FIND:** a app `correspondencia`, a *branch* própria e o que foi alterado fora dela.
2. **Modelagem dos dados:** os modelos `Categoria` e `Item` do FIND, usados sem alteração, e o modelo `ParGabarito`, criado para ligar cada perdido ao seu achado. Inclua um **diagrama entidade-relacionamento** pequeno.
3. **Conjunto de dados:** as quantidades (40 objetos, 40 perdidos, 80 achados); a distribuição por categoria; os grupos de objetos parecidos; como as fotos foram tiradas (as duas condições) e tratadas (orientação, 800 px, remoção do EXIF); os modelos de texto do achado e do perdido; os 4 grupos de variação, com um exemplo de cada; o distrator com outra cor; e a semente. Coloque **uma figura com dois ou três pares de exemplo** (foto A, foto B e os dois textos).
4. **Candidatos:** quais itens entram na comparação (os mesmos status que o FIND considera).
5. **Pré-processamento do texto:** os passos da normalização, com um exemplo de entrada e saída.
6. **Estratégias:** a **fórmula de cada uma** — a regra da B0 (35 + 40 + 25, dividida por 100); TF-IDF e cosseno sobre trechos de 3 a 5 letras (T1); `1 − Hamming/256` do pHash e a interseção de histogramas, em 50/50 (V); e a F, com os pesos 0,6, 0,3 e 0,1, a versão sem foto (pesos divididos por 0,7) e a regra para achados sem foto (parte visual igual a 0).
7. **Justificativa das configurações:** por que trechos de letras na T1 (tolerância a erros de digitação), por que a V reproduz o FIND e por que esses pesos na F. Deixe claro que foram **fixados antes** do experimento.
8. **Métricas:** as fórmulas de Recall@k e MRR, por que k = 1 e 6, como os empates foram tratados, e por que a B0 foi avaliada sem o corte de 30 pontos.
9. **Medição de tempo:** 1.000 itens adicionais só de texto, 30 consultas, descarte da primeira e média.
10. **Reprodutibilidade:** o repositório, a *branch*, a *tag* `tcc-resultados` e o README com os comandos.

> **Dica:** os revisores valorizam o "por que X e não Y". Diga por que cada configuração foi escolhida, citando a literatura. Não invente comparações que não foram feitas.

---

# 7. Resultados e Discussão
**Prazo: 13/11/2026**

Organize o capítulo pelas **questões de pesquisa**, e não pela ordem em que as coisas foram feitas.

**Como escrever cada subseção (use sempre o mesmo roteiro):**

1. **Apresente** a tabela ou o gráfico, citando-o no texto antes de ele aparecer ("A Tabela 3 apresenta...").
2. **Descreva** o que os números mostram, sem opinião: quem foi melhor, quem foi pior e por quanto ("A T1 alcançou Recall@6 de 0,850, contra 0,600 da B0").
3. **Interprete:** por que isso aconteceu, ligando ao Referencial ("o resultado era esperado, pois os trechos de letras toleram...").
4. **Responda** à QP em uma frase.

## 7.1 Caracterização do conjunto de dados

**Apresente:** uma tabela com o total de objetos, perdidos, achados e distratores; a distribuição por categoria; quantos objetos pertencem a grupos de objetos parecidos; e quantos perdidos há em cada grupo de variação. Isso mostra ao leitor que o teste é difícil e diverso.

## 7.2 Estratégia textual (QP1)

**Apresente:** uma tabela com B0 e T1 nas linhas e Recall@1, Recall@6 e MRR nas colunas (arquivo `metricas.csv`). Informe também **em quantos perdidos a B0 deu ao item correto menos de 0,30** — ou seja, em quantos casos o FIND de hoje **nem mostraria** a sugestão certa (o comando `avaliar` mostra esse número).

**Discuta:** quanto a T1 ganhou (ou perdeu) em relação à B0 e por quê, relacionando com o que o Referencial disse sobre cada técnica.

## 7.3 Estratégia visual (QP2)

**Apresente:** a linha da V na mesma tabela e **uma figura com um par em que a V acertou e outro em que errou** (as duas fotos lado a lado).

**Discuta:** se o hash perceptual e o histograma reconhecem o mesmo objeto em outra foto ou se se comportam como a teoria prevê (feitos para a mesma imagem); se a cor ajuda ou confunde (duas garrafas azuis em fundos diferentes). Um resultado ruim aqui **é um resultado**, e dos mais úteis: ele mostra ao FIND o que não vale a pena manter.

## 7.4 Combinação e robustez (QP3)

**Apresente:**

- a F (com foto e sem foto) ao lado das estratégias isoladas — esta é a **tabela principal** do trabalho;
- o **gráfico de robustez** (`robustez.png`): Recall@6 da B0, da T1 e da F em cada grupo de variação (nenhuma, sinônimo, erro de digitação e sem acento);
- em uma frase, o resultado para os objetos parecidos (`robustez_parecido.csv`).

**Discuta:** se combinar compensa; quanto a foto acrescenta (F com foto × F sem foto); em qual grupo todas as técnicas falham (é esperado que **sinônimos** sejam o ponto fraco das técnicas clássicas — se isso acontecer, é o argumento para os trabalhos futuros). Lembre que cada grupo tem **10 perdidos**: uma diferença de 0,1 no Recall@6 é **um** perdido.

## 7.5 Tempo de resposta

**Apresente:** a tabela `tempos.csv` (tempo de preparação e tempo médio por consulta, com 1.000 itens adicionais; tempo do histograma de uma foto) e a configuração do computador.

**Discuta:** se as técnicas são viáveis na escala de um campus; o que pode ser calculado uma vez, no cadastro do item, e o que precisa ser calculado a cada consulta.

## 7.6 Análise de erros e explicabilidade

**Apresente:** um quadro com 3 a 5 casos em que a F errou (correto fora dos 6 primeiros) e 1 caso em que a F acertou e a B0 errou: os dois textos, as fotos e a posição do correto. Inclua **uma** saída do comando `sugerir`, mostrando as 6 sugestões com as partes da pontuação.

**Discuta:** a causa de cada erro (sinônimo desconhecido, objeto parecido com o mesmo vocabulário, foto escura, fundo dominante) e a **explicabilidade**: o usuário pode ver *por que* o item foi sugerido (texto parecido, foto parecida, mesma categoria) — algo difícil de oferecer com técnicas de IA.

## 7.7 Discussão geral e limitações

Duas páginas, em texto corrido, nesta ordem:

1. **Resposta à pergunta principal (1 parágrafo).** A melhor estratégia, com os números principais, comparada à B0.
2. **Relação com os trabalhos relacionados (1 parágrafo).** Volte ao quadro da seção 4.4: o que os seus resultados confirmam e o que acrescentam. Cuidado ao comparar números: os conjuntos de dados são diferentes.
3. **Recomendação para o FIND (1 parágrafo).** O que o FIND deveria adotar, o que deveria abandonar e o que precisa ser calculado no cadastro do item.
4. **Limitações (1 a 2 parágrafos).** Retome as ameaças à validade da Metodologia e, para cada uma, diga o que foi feito para reduzi-la (por exemplo: as variações do texto foram definidas pelo pesquisador, mas o gerador e o catálogo estão publicados e podem ser conferidos).

**Cuidados gerais nos Resultados:**

- apresente **todas** as estratégias, inclusive as que foram mal, e não arredonde números a seu favor (use 3 casas decimais nas métricas);
- nenhum parâmetro pode ter sido alterado depois de ver os resultados;
- trechos de código só quando ilustrarem uma fórmula, com poucas linhas e numerados como figura ou quadro;
- figuras e tabelas seguem o [README.md](../../../README.md#como-incluir-imagens): título acima, fonte abaixo, citadas no texto antes de aparecerem. Nas tabelas e gráficos produzidos por você, a fonte é "Elaborado pelo autor (2026)".

---

# 8. Conclusão
**Prazo: 20/11/2026**

**Fale sobre, nesta ordem:**

1. a resposta **direta** à pergunta de pesquisa e a cada QP, com os números principais;
2. se o objetivo geral foi atingido;
3. as principais contribuições (conjunto de avaliação, avaliação das técnicas, análise do efeito de cada variação);
4. as limitações, com honestidade;
5. trabalhos futuros **coerentes com os resultados**, por exemplo: dicionário de sinônimos do domínio (se sinônimos foram o ponto fraco); ajuste dos pesos com uma parte dos dados reservada para isso; outras técnicas clássicas de texto (BM25, similaridade de *strings*); uso da localização e da data como evidência; avaliação com dados reais do FIND; comparação com técnicas de IA (*embeddings* de texto e de imagem) sobre o **mesmo conjunto de dados**; integração da estratégia vencedora à versão em uso do FIND.

Não traga informação nova nem citações na Conclusão (regras em [README.md](../../../README.md#conclusão)).

---

# 9. Resumo, Título e Objetivos Específicos
**Prazo: 27/11/2026**

## 9.1 Resumo e *Abstract*

- **Tamanho:** parágrafo único com 150 a 500 palavras (NBR 6028:2021).
- **Sequência:** contexto (plataformas de achados e perdidos), problema (encontrar automaticamente o par certo), objetivo, método (conjunto de avaliação, estratégias e métricas), principais resultados **com números** (por exemplo, "a combinação ... alcançou Recall@6 de ..., contra ... da heurística atual") e a principal conclusão.
- **Dica:** escreva uma frase para cada item da sequência e só depois junte as frases em um parágrafo.
- **Palavras-chave possíveis:** achados e perdidos; recuperação de informação; similaridade textual; similaridade de imagens; correspondência de registros.

## 9.2 Título

Definido por último, depois da aprovação do texto. Deve deixar claro que o trabalho é uma **avaliação** de técnicas **clássicas** para a **correspondência** de itens perdidos e encontrados. Título provisório para referência:

> *Correspondência automática entre itens perdidos e encontrados: uma avaliação de técnicas clássicas de similaridade textual e visual*

## 9.3 Objetivos Específicos

Escreva agora, olhando para as etapas da Metodologia e para o que foi realmente feito (ver seção 3 deste documento).

---

# 10. Do TCC ao artigo

Esta etapa começa **depois** que o TCC estiver aprovado.

- **Onde publicar:** eventos e revistas da SBC — por exemplo, o SBSI (Simpósio Brasileiro de Sistemas de Informação), o WebMedia e o seu workshop de iniciação científica (WTICG) e o ENCOMPIF (Encontro Nacional de Computação dos Institutos Federais). Como primeira publicação, a SECITEX (IFRN) também é uma boa opção.
- **Estrutura típica de um artigo experimental:** Introdução; Trabalhos relacionados; Fundamentação (curta); Protocolo experimental (dados, estratégias e métricas); Resultados; Discussão e ameaças à validade; Conclusão.
- **Enxugar:** no artigo, o Referencial vira uma fundamentação curta; o foco fica no protocolo, na tabela principal, no gráfico de robustez e na análise de erros.
- **Revisão às cegas:** se for o caso, retire da versão submetida os nomes, a instituição e os links dos repositórios.
- **Artefatos:** publique o gerador, o catálogo, as fotos tratadas e os *scripts* de avaliação (por exemplo, no Zenodo, que gera um DOI).
- **Uso de IA generativa na escrita:** siga a seção [Uso de inteligência artificial generativa](../../../README.md#uso-de-inteligência-artificial-generativa) das orientações gerais e as regras do veículo escolhido.
- **Submissão:** nenhum artigo é submetido sem a minha revisão final.
