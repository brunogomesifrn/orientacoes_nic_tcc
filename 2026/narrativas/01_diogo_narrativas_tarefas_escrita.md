# Plano de escrita do TCC – Diogo (Tecnologia em Sistemas para Internet)

**Projeto pai:** Narrativas – plataforma digital para registro, organização e difusão das narrativas populares do Rio Grande do Norte (ver [projeto.md](../projeto.md)).

**Temática:** 4.3 – Narração automática das narrativas: conversão de texto em áudio (ver [tematicas.md](../tematicas.md)).

**Plano de desenvolvimento correspondente:** `01_diogo_narrativas_tarefas_desenvolvimento.md`.

**Base de estilo e de normas ABNT:** o arquivo [README.md](../../../README.md) deste repositório. Tudo o que está lá vale aqui — estrutura, citações, referências, figuras, tabelas, formatação. Este documento **não repete** as regras da ABNT; ele diz **o que pesquisar e o que escrever** em cada capítulo deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copie estas frases para o TCC. Elas dizem sobre o que é cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você leu.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do TCC será **criado e compartilhado pelo coordenador em uma pasta do Google Drive**. Você não cria arquivo novo nem trabalha em cópia local.

Como trabalhar nele:

- **Escreva sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico do Drive é o que permite ao orientador ver o que mudou de uma semana para outra.
- **Não crie cópias** ("TCC v2", "TCC final", "TCC final revisado"). É a forma mais rápida de perder trabalho. O Drive já guarda tudo em **Arquivo → Histórico de versões**.
- **Marque cada entrega no histórico.** Ao terminar um capítulo, use **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 29/09`.
- **Avise por mensagem quando entregar.** O orientador não fica olhando o documento; ele precisa saber que há algo novo para ler.
- **Comentário se responde, não se apaga.** Responda a cada comentário e só então marque como resolvido.
- **Figuras e tabelas** vão dentro do documento, no lugar certo, com identificação em cima e fonte embaixo. Não mande imagem em anexo separado.
- **Crie a seção "Referências" no primeiro dia** e acrescente cada obra assim que ler. Deixar para o fim garante referência faltando e citação sem fonte.
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
| 22/09 a 28/09 | Sprint 1 – repositório e primeiro áudio | Introdução e Objetivo Geral (29/09) |
| 29/09 a 12/10 | Sprints 2 e 3 – corpus e as três ferramentas | Referencial Teórico (13/10) |
| 13/10 a 19/10 | Sprint 4 – tempo, tamanho, offline | Metodologia (20/10) |
| 20/10 a 26/10 | Sprint 5 – inteligibilidade (WER) | Materiais e Métodos (27/10) |
| 27/10 a 09/11 | Sprints 6 e 7 – pronúncia, questionário, gráficos | Resultados (10/11) |
| 10/11 a 16/11 | Sprint 8 – recomendação e documentação | Conclusão (17/11) |
| 17/11 a 23/11 | — | Resumo, Objetivos e Título (24/11) |

**Um aviso sobre o cronograma.** A Metodologia vence em 20/10, quando você ainda não terá medido tudo. E os Resultados vencem em 10/11, logo depois da sprint mais pesada. Isso é normal e tem solução:

- escreva a Metodologia falando do **plano** ("serão comparadas três ferramentas...") e depois passe tudo para o passado;
- **vá preenchendo as tabelas de Resultados a cada sprint**, e não tudo na última semana. Quem deixa os Resultados para o fim não entrega.

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Texto pela metade dá para comentar; texto que não chega, não.
- Cada entrega é: capítulo escrito + versão nomeada no histórico + aviso ao orientador.
- Resolva **todos** os comentários da entrega anterior antes de avisar sobre a próxima.

---

## Que tipo de trabalho é este

Um **TCC** com a estrutura completa das [orientações gerais](../../../README.md), escrito de modo que, ao final, possa ser reduzido a um **artigo de 8 a 12 páginas** para um congresso ou uma revista. **Confirme com o orientador qual é o destino** — dele vêm o modelo e o limite de páginas.

Quatro coisas fazem a diferença entre um TCC comum e um trabalho publicável:

1. **O objeto do trabalho não é o programa que você escreveu.** É a **comparação medida** entre ferramentas de síntese de voz. A plataforma Narrativas é o contexto que justifica a pergunta. Se o texto virar um manual dos seus scripts, o trabalho perde o valor.
2. **O leitor quer saber quanto, não o quê.** Não interessa que você gerou áudios; interessa que a ferramenta A errou 8% das palavras e a ferramenta B errou 23%, e o que isso significa.
3. **O método tem de dar para repetir.** Máquina, versões, corpus, quantas repetições, qual voz de cada ferramenta.
4. **Declare as limitações.** Este trabalho tem várias (corpus pequeno, avaliação feita por você mesmo, reconhecimento de fala como medida indireta). Reconhecê-las aumenta a confiança no trabalho; escondê-las é o caminho mais rápido para a recusa.

Estrutura dos capítulos:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Narrativas populares e tradição oral
2.2 Patrimônio cultural imaterial e acervos digitais
2.3 Síntese de voz
2.4 Acessibilidade digital
2.5 Avaliação da qualidade de voz sintetizada
2.6 Trabalhos relacionados
3 METODOLOGIA
3.1 Classificação da pesquisa
3.2 Etapas do trabalho
3.3 Protocolo de medição
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
6 CONCLUSÃO
REFERÊNCIAS
APÊNDICES (o questionário, se houver; a lista de termos regionais)
```

---

# 1. Introdução
**Prazo: 29/09/2026**

Cinco blocos de parágrafos, nesta ordem (é a sequência fixa do `README.md`). Duas a três páginas.

## 1.1 Contextualização (2 a 3 parágrafos)

**Pesquise sobre:**

- **narrativas populares e tradição oral**: o que são, como se transmitem, que papel cumprem na formação da identidade de uma comunidade. Aqui o projeto já lhe dá um ponto de partida pronto: as referências citadas em `projeto.md` (Bezerra, 2026; Dos Santos Fernandes e Martins, 2026). Vá além delas e procure também autores clássicos da área, como **Luís da Câmara Cascudo** (a referência incontornável quando se fala em folclore brasileiro e potiguar), **Paul Zumthor** e **Walter Ong**, que tratam da oralidade como forma de cultura;
- **patrimônio cultural imaterial**: a Convenção da UNESCO para a Salvaguarda do Patrimônio Cultural Imaterial (2003) e o registro de bens imateriais no Brasil (Decreto nº 3.551/2000, IPHAN);
- **acervos digitais culturais e humanidades digitais**: como as tecnologias digitais vêm sendo usadas para preservar e difundir cultura. As referências Soave e Da Silva Lemos (2022) e Reis (2023), já citadas no projeto, servem bem aqui.

**Escreva sobre:** o valor das narrativas populares como patrimônio e como elas se transmitem — pela **voz**, de geração em geração. Depois apresente o projeto Narrativas como a iniciativa que busca preservar digitalmente esse acervo no Rio Grande do Norte.

E então faça a ligação que dá sentido ao seu tema específico, que é a melhor coisa que a sua Introdução tem: **essas narrativas nasceram para serem ouvidas, não lidas.** Um acervo que as transforma apenas em texto na tela preserva o conteúdo, mas perde a forma original. Devolver a voz a esse acervo não é um enfeite — é uma questão de fidelidade ao que está sendo preservado.

Traga pelo menos **um dado concreto** neste bloco (número de bens registrados como patrimônio imaterial no Brasil, dados sobre acervos digitais, algo mensurável), porque dado numérico dá peso imediato ao texto.

## 1.2 Problemática (2 a 3 parágrafos)

**Pesquise sobre:**

- o custo e o esforço de produzir **narração humana**: tempo de estúdio, locução, edição. Procure por "produção de audiolivro", "*audiobook production*", "narração profissional";
- **acessibilidade digital**: quantas pessoas no Brasil têm deficiência visual ou baixa visão (dados do IBGE), e o que a Lei Brasileira de Inclusão (Lei nº 13.146/2015) exige de sítios públicos. Procure também o **eMAG** (Modelo de Acessibilidade em Governo Eletrônico) e as diretrizes **WCAG** do W3C;
- **baixa escolaridade e letramento**: parte do público das narrativas populares é justamente quem tem mais dificuldade com texto escrito. Procure dados do INAF ou do IBGE sobre analfabetismo funcional no Brasil e no Nordeste.

**Escreva sobre:** o problema em três camadas, cada uma reforçando a anterior.

Primeiro, o **problema prático**: o protótipo da plataforma já prevê narração em áudio, mas gravar locução humana para todo um acervo é inviável — exige estúdio, locutor e horas de trabalho por narrativa, e o acervo tende a crescer continuamente por colaboração da comunidade. Se a narração depender de gravação humana, na prática a maior parte do acervo vai ficar sem áudio.

Segundo, o **problema de acesso**: sem áudio, o acervo exclui pessoas com deficiência visual e pessoas com dificuldade de leitura — exatamente parte do público que mais se identifica com esse patrimônio. Aqui você amarra com a Lei Brasileira de Inclusão.

Terceiro, e este é o ponto específico do seu trabalho: a síntese de voz por computador seria a solução óbvia, **mas ninguém sabe se ela funciona neste caso**. As ferramentas de voz são treinadas com linguagem padrão e vocabulário urbano. Narrativas populares do sertão potiguar estão cheias de nomes e termos que provavelmente não estavam nesse treinamento: "Boitatá", "Caipora", "Mossoró", "Seridó", "açude", "jerimum", "xique-xique". Se o sintetizador pronunciar errado justamente as palavras que carregam a identidade cultural da narrativa, a solução vira um problema — e um problema pior do que a ausência de áudio, porque distorce o patrimônio que se quer preservar.

**Feche enunciando a pergunta de pesquisa**, de forma direta: *as ferramentas gratuitas de síntese de voz em português brasileiro dão conta de narrar narrativas populares, incluindo seus nomes e termos regionais?*

**Não escreva** que "a plataforma está sem áudio porque é ruim". O acervo ainda está em construção — esse é o momento certo de responder à pergunta, antes de a equipe decidir no escuro. Esse enquadramento é bem mais forte.

## 1.3 Caminho para a solução (1 a 2 parágrafos)

**Pesquise sobre:**

- as opções existentes para dar áudio a um acervo: locução humana profissional, locução por voluntários da comunidade, síntese de voz gratuita, síntese de voz paga (serviços de nuvem), e o leitor de tela que o próprio usuário já tem instalado;
- o que são as ferramentas que você vai comparar, consultando a documentação oficial de cada uma;
- a diferença entre síntese de voz que funciona **na nuvem** e a que funciona **na própria máquina**, e por que isso importa para uma instituição pública (dependência de serviço externo, custo, continuidade).

**Escreva sobre:** o leque de alternativas, dizendo o que cada uma resolve e o que cada uma custa. Mostre que existe um gradiente:

- **locução humana profissional** — melhor qualidade, custo proibitivo para um acervo grande;
- **voluntários da comunidade** — interessante culturalmente, mas de qualidade irregular e difícil de sustentar no tempo;
- **serviços pagos de síntese na nuvem** — boa qualidade, mas custo por caractere e dependência de contrato;
- **ferramentas gratuitas de síntese** — sem custo, mas com qualidade a verificar. **É este o recorte do trabalho.**

Justifique o recorte: o projeto Narrativas é institucional e público, e uma solução que dependa de orçamento contínuo ou de trabalho voluntário permanente não se sustenta. Por isso a pergunta é sobre as **ferramentas gratuitas**.

Diga também por que o trabalho **não** avalia os serviços pagos: eles são uma alternativa conhecida e de qualidade estabelecida, e o que está em aberto é se a opção gratuita já é suficiente. Recorte declarado é recorte defendido.

## 1.4 Apresentação da solução (2 parágrafos)

**Escreva sobre:** o que foi feito, de forma concreta. Foram comparadas **três ferramentas gratuitas** de síntese de voz em português brasileiro (gTTS, pyttsx3 e edge-tts), gerando o áudio das **mesmas** narrativas populares de domínio público em todas elas.

Descreva **como** foram avaliadas, porque é isso que sustenta o trabalho:

- **inteligibilidade medida de forma automática**: cada áudio gerado foi transcrito de volta para texto por um programa de reconhecimento de fala, e a transcrição foi comparada com o texto original. Quanto mais próximos, mais clara foi a fala. A medida usada é a taxa de erro de palavras;
- **pronúncia de termos regionais**: uma lista de 30 nomes e palavras do vocabulário potiguar e nordestino, verificada de duas formas — automaticamente e por escuta;
- **tempo de geração, tamanho do arquivo, funcionamento sem internet e custo**;
- **avaliação com ouvintes** (se ela tiver sido realizada): questionário anônimo com escala de 1 a 5.

Registre que o corpus é formado por narrativas de **domínio público**, com a origem e a situação de direitos autorais de cada texto documentada, e que **nenhum dado de usuário da plataforma foi utilizado**.

Se houve questionário, diga que ele foi **anônimo**, sem coleta de qualquer dado que identificasse quem respondeu, conforme a LGPD (Lei nº 13.709/2018), e informe como a questão ética foi encaminhada junto ao orientador. Se não houve, este é um dos pontos a declarar nas Limitações — não na Introdução.

## 1.5 Vínculo com o projeto e escopo (1 parágrafo)

**Escreva sobre:** que o trabalho está vinculado ao projeto Narrativas, do IFRN, cuja etapa atual trata de autenticação, área administrativa e gerenciamento do acervo. Explique que este TCC foi desenvolvido **de forma independente**, em repositório próprio, sem alterar o sistema, porque o objetivo é **responder antecipadamente a uma decisão técnica** que a equipe vai precisar tomar: se a plataforma pode oferecer narração automática ou se o áudio terá de ser sempre humano.

Deixe claro que **implementar a narração na plataforma é trabalho futuro**, fora do escopo deste TCC.

Feche a Introdução com um parágrafo curto dizendo como o texto está organizado ("Além desta introdução, o Capítulo 2 apresenta o referencial teórico; o Capítulo 3 descreve a metodologia; [...]").

---

# 2. Objetivo Geral
**Prazo: 29/09/2026 (junto com a Introdução)**

Uma **única frase**, com **uma única ação principal**. Modelo do `README.md`:

> "O objetivo principal do presente trabalho consiste [na ação] de [o quê] para [finalidade]."

**Direcionamentos:**

- o verbo aqui **não** é "desenvolver". Você não está entregando um sistema; está entregando conhecimento medido. Verbos adequados: **avaliar**, **comparar**, **analisar**. O título provisório sugerido na temática já indica o caminho: *"Avaliação de ferramentas de síntese de voz para a narração automatizada de narrativas populares em português brasileiro"*;
- diga **o que** é avaliado: ferramentas gratuitas de síntese de voz em português brasileiro;
- diga **para quê**: a narração automatizada de um acervo digital de narrativas populares;
- diga **em que dimensão** você mede: inteligibilidade, pronúncia de termos regionais e viabilidade técnica. Sem isso, "avaliar ferramentas" fica vago demais;
- **não** empilhe ações. "Avaliar, implementar e integrar" são três objetivos, não um;
- **não** prometa o que você não mediu. Se o questionário não foi aplicado, não coloque "percepção dos usuários" no objetivo geral.

**Confira antes de entregar:** leia o objetivo geral e, logo depois, a primeira frase da sua Conclusão. Se as duas não estiverem falando da mesma coisa, uma delas está errada.

---

# 3. Objetivos Específicos
**Prazo: 24/11/2026 (com o Resumo e o Título)**

Ficam para o fim de propósito: eles descrevem o que foi **realmente alcançado**, e isso só se sabe com o trabalho pronto. Até lá, use uma versão provisória e vá ajustando.

**Direcionamentos:**

- de 4 a 5 itens, verbo no infinitivo, minúscula no início, ponto e vírgula no fim de cada um e ponto no último;
- na **mesma ordem** das etapas da Metodologia e das seções dos Resultados;
- cada um **verificável**: na Conclusão você terá de mostrar, com número, que foi atingido;
- não confunda objetivo com tarefa. "Instalar o edge-tts" não é objetivo específico.

**O que cada item deve cobrir** (redija com as suas palavras depois):

1. revisar a literatura sobre tradição oral, acervos digitais culturais, síntese de voz e acessibilidade digital;
2. constituir um corpus de narrativas populares de domínio público e uma lista de termos regionais para teste;
3. gerar o áudio do corpus em cada uma das ferramentas avaliadas;
4. medir a inteligibilidade, a pronúncia dos termos regionais, o tempo de geração, o tamanho dos arquivos e o funcionamento sem conexão;
5. recomendar, a partir dos resultados, se e como a narração automática pode ser adotada pela plataforma Narrativas.

---

# 4. Referencial Teórico
**Prazo: 13/10/2026**

**Vídeo com a explicação (assista antes de começar):** https://youtu.be/8Qztq1Q5vb0

Comece a procurar referências **na primeira semana**, não na véspera. Este é o capítulo que mais consome tempo.

Uma regra prática resolve metade dos problemas aqui: **tudo o que você vai usar nos Resultados precisa estar explicado antes**. Se você vai apresentar "taxa de erro de palavras" na tabela, tem que ter explicado o que é. Se um conceito não reaparece depois, não precisa estar.

Seu trabalho tem uma vantagem rara: ele é **interdisciplinar**. Junta cultura popular com tecnologia. Aproveite isso — comece pelo lado cultural, que é o que dá sentido ao resto, e só então vá para o técnico.

## 4.1 Narrativas populares e tradição oral

**Pesquise:** "tradição oral", "narrativas populares", "cultura popular", "folclore brasileiro", "memória coletiva". Autores: **Luís da Câmara Cascudo** (*Dicionário do Folclore Brasileiro*, *Contos Tradicionais do Brasil*) — indispensável e ainda mais adequado por ser potiguar; **Paul Zumthor** (*Introdução à poesia oral*, *A letra e a voz*); **Walter Ong** (*Oralidade e cultura escrita*). Some as referências já usadas no projeto (Bezerra, 2026; Dos Santos Fernandes e Martins, 2026).

**Escreva:** o que são narrativas populares e como se transmitem; por que a **voz** é constitutiva delas, e não um acessório — a entonação, o ritmo e a pausa fazem parte do que está sendo transmitido; e por que a passagem da oralidade para o texto escrito preserva o conteúdo mas perde parte da forma.

**Esta subseção é a que dá sentido ao seu trabalho técnico.** Se você explicar bem aqui por que a voz importa, o leitor entende imediatamente por que vale a pena medir a qualidade de uma voz sintética. Não trate como enfeite.

## 4.2 Patrimônio cultural imaterial e acervos digitais

**Pesquise:** Convenção da UNESCO para a Salvaguarda do Patrimônio Cultural Imaterial (2003); Decreto nº 3.551/2000 e o registro de bens imateriais pelo IPHAN; "acervo digital", "curadoria digital", "humanidades digitais", "preservação digital". As referências Soave e Da Silva Lemos (2022), Reis (2023), Binda e Da Silva (2026) e Pires (2025), já no projeto, se encaixam aqui.

**Escreva:** o que é patrimônio cultural imaterial e por que ele é mais frágil que o material — depende de pessoas vivas que o guardem. Retome o argumento que está no próprio documento do projeto: as narrativas estão ameaçadas pelo envelhecimento de seus detentores. Depois apresente os acervos digitais como estratégia de salvaguarda, e o projeto Narrativas como um caso concreto disso.

## 4.3 Síntese de voz

**Pesquise:** "síntese de voz", "conversão texto-fala", "*text-to-speech*", "*speech synthesis*". Para os fundamentos, procure obras de referência da área (por exemplo, *Text-to-Speech Synthesis*, de Paul Taylor) e artigos de revisão sobre síntese de voz neural. Para as ferramentas específicas, use a documentação oficial de cada uma.

**Escreva:** o que é síntese de voz e como ela evoluiu, em três gerações, explicadas de forma simples:

- **concatenativa**: monta a fala colando pedaços de gravações humanas. Soa natural nos trechos, mas emenda mal;
- **paramétrica**: gera o som a partir de um modelo matemático da voz. Mais flexível, mas soa artificial;
- **neural**: usa redes neurais treinadas com muitas horas de fala. É o estado atual e a razão de as vozes terem melhorado tanto nos últimos anos.

Explique também dois pontos que você vai precisar nos Resultados:

- a diferença entre síntese que roda **na nuvem** e síntese que roda **na própria máquina**, com as implicações de cada uma (dependência de internet, custo, privacidade, continuidade do serviço);
- por que a síntese erra em **nomes próprios e palavras raras**: o modelo aprende a pronunciar a partir do que viu no treinamento, e o vocabulário regional do sertão dificilmente estava lá. **Este parágrafo é a fundamentação da hipótese central do seu trabalho** — capriche nele.

Por fim, apresente brevemente cada ferramenta avaliada, dizendo o que é e em qual dessas categorias se encaixa.

## 4.4 Acessibilidade digital

**Pesquise:** Lei Brasileira de Inclusão (Lei nº 13.146/2015); **eMAG** – Modelo de Acessibilidade em Governo Eletrônico; diretrizes **WCAG** do W3C; "leitor de tela", "audiodescrição", "acessibilidade em acervos digitais". Dados do IBGE sobre pessoas com deficiência visual no Brasil.

**Escreva:** o que é acessibilidade digital e o que a legislação brasileira exige de sítios públicos. Explique a diferença entre duas coisas que costumam ser confundidas: o **leitor de tela**, que é um programa que o próprio usuário instala e que lê qualquer texto da tela, e a **narração embutida no acervo**, que é o que a plataforma pretende oferecer. Diga por que a segunda faz sentido mesmo existindo a primeira — a narração embutida serve também a quem não usa leitor de tela, como pessoas com dificuldade de leitura, idosos e quem simplesmente prefere ouvir.

Amarre ao trabalho: a narração automática é, ao mesmo tempo, uma questão de **difusão cultural** e de **acessibilidade**. Essa dupla justificativa fortalece bastante a Introdução, e é por isso que ela merece fundamentação aqui.

## 4.5 Avaliação da qualidade de voz sintetizada

**Pesquise:** "**MOS**" (*Mean Opinion Score*) e a recomendação **ITU-T P.800**, que é a norma internacional onde essa escala de 1 a 5 foi definida; "inteligibilidade" e "naturalidade" como dimensões distintas de qualidade de voz; "**taxa de erro de palavras**" (*Word Error Rate*, WER) e "taxa de erro de caracteres" (CER); avaliação objetiva × subjetiva de voz sintetizada.

**Escreva:** que existem dois caminhos para avaliar uma voz sintética, e que eles medem coisas diferentes:

- **avaliação subjetiva**: pessoas ouvem e dão nota. O método padrão é o MOS, com escala de 1 a 5. Explique que **naturalidade** (soar como gente) e **inteligibilidade** (dar para entender) são coisas distintas — uma voz pode ser perfeitamente compreensível e soar robótica, e o contrário também acontece;
- **avaliação objetiva**: medidas calculadas por programa, sem pessoas. Explique o método que você usou: transcrever o áudio gerado de volta para texto com reconhecimento de fala e comparar com o texto original. Defina **WER** e **CER**, dizendo como se interpretam (quanto menor, melhor).

**E seja honesto desde já sobre o limite do método objetivo:** o programa de reconhecimento de fala tem erros próprios e foi treinado com voz humana, de modo que ele é um **indício** de inteligibilidade, não uma prova. Dizer isso aqui, no Referencial, prepara o leitor — e é muito melhor do que ser cobrado por isso na banca.

## 4.6 Trabalhos relacionados

**Pesquise:** trabalhos que tenham **comparado** ferramentas de síntese de voz, especialmente em português; trabalhos sobre síntese de voz aplicada a acessibilidade; trabalhos sobre digitalização e difusão de acervos culturais com áudio. Busque em: **SBC OpenLib** (procure pelo Simpósio Brasileiro de Tecnologia da Informação e da Linguagem Humana — STIL, e pelo WEI), **BDTD**, repositórios de institutos federais e universidades, SciELO, Google Acadêmico, e também em bases internacionais como ACM e IEEE.

Termos úteis: "comparação de ferramentas TTS", "avaliação síntese de voz português", "*TTS evaluation Portuguese*", "*speech synthesis accessibility*", "acervo digital áudio".

**Escreva:** de 4 a 6 trabalhos, um parágrafo cada, dizendo o que foi avaliado, **como foi medido** (esta é a informação que mais interessa a você) e quais as limitações.

Feche com um **quadro comparativo** entre esses trabalhos e o seu, com colunas como: ferramentas avaliadas, idioma, tipo de texto usado, método de avaliação (subjetivo, objetivo ou os dois), se testou vocabulário regional, se testou funcionamento sem internet, e se o material está disponível publicamente.

**Esse quadro é a justificativa do seu trabalho.** O seu diferencial provavelmente vai aparecer em duas colunas: o **vocabulário regional** como critério de avaliação, e o **domínio das narrativas populares**. Se você encontrar um trabalho que já faz exatamente isso, avise o orientador — em outubro ainda dá tempo de ajustar o recorte.

## Regras para o referencial inteiro

- **Toda afirmação técnica precisa de referência.**
- **Não empilhe citações.** O capítulo não pode ser "Fulano diz X. Beltrano diz Y". Explique com suas palavras, relacione os autores e ligue ao seu trabalho.
- **Documentação oficial** (das ferramentas) serve para descrever a ferramenta, não para fundamentar conceito. Para conceito, use livro ou artigo.
- **Nada de blog, Stack Overflow ou site sem autoria** nas Referências. Você vai usar muito esse material para resolver problema técnico — isso é normal —, mas ele não entra na lista.
- **Nunca cite o que você não leu.** Ferramentas de IA inventam referências com muita naturalidade.
- Meta para este trabalho: **18 a 25 referências**, equilibradas entre o lado cultural e o lado técnico. Como o TCC é interdisciplinar, um referencial só técnico ou só cultural fica desequilibrado.

---

# 5. Metodologia
**Prazo: 20/10/2026**

Como o trabalho foi feito. Verbos no passado e linguagem impessoal ("foi realizado", "realizou-se"). Duas a três páginas.

**Pasta com metodologias prontas para consulta:** https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

## 5.1 Classificação da pesquisa

**Pesquise:** Gil (2017) e Prodanov e Freitas (2013) — referências completas no `README.md`. Leia os capítulos de classificação antes de escrever; não classifique de ouvido.

**Escreva:** a classificação pelos quatro critérios, **justificando cada uma** com uma frase ligada ao seu trabalho (o erro mais comum é só listar os rótulos). O enquadramento mais provável:

- **Natureza:** aplicada — o resultado responde a uma decisão concreta do projeto Narrativas;
- **Objetivos:** exploratória e descritiva — investiga uma questão ainda não respondida neste contexto e descreve o comportamento medido das ferramentas;
- **Abordagem:** quantitativa, ou **quali-quantitativa** se o questionário tiver sido aplicado e você analisar as respostas abertas;
- **Procedimentos:** pesquisa bibliográfica combinada com **pesquisa experimental** — as mesmas narrativas foram submetidas a ferramentas diferentes, sob as mesmas condições, e os resultados foram comparados. Se houve questionário, acrescente **levantamento**.

Discuta o enquadramento com o orientador antes de fechar. É um dos pontos mais cobrados em banca.

## 5.2 Pesquisa bibliográfica

**Escreva:** quais bases foram consultadas, quais palavras-chave foram usadas (liste-as, em português e em inglês), o recorte de tempo e os critérios para escolher os trabalhos. Escreva isso **enquanto** pesquisa, não depois — reconstruir de memória sai impreciso e dá mais trabalho.

## 5.3 Etapas do trabalho

**Escreva:** as etapas em ordem cronológica. Uma **figura com o fluxo** ajuda muito o leitor e é simples de fazer (use o draw.io, que é gratuito). Lembre: identificação em cima, centralizada, fonte embaixo.

As etapas, com base no plano de desenvolvimento:

1. levantamento bibliográfico sobre tradição oral, acervos digitais, síntese de voz e acessibilidade;
2. seleção das ferramentas a comparar, com os critérios da escolha;
3. constituição do corpus de narrativas de domínio público e da lista de termos regionais;
4. geração dos áudios, com a mesma configuração de voz por ferramenta;
5. medição de tempo, tamanho e funcionamento sem conexão;
6. medição da inteligibilidade por transcrição automática;
7. avaliação da pronúncia dos termos regionais;
8. aplicação do questionário com ouvintes (se realizada);
9. consolidação, análise e recomendação.

**Justifique a escolha do corpus**, que é um ponto que a banca vai perguntar: por que narrativas de domínio público (porque não há acervo real disponível ainda e porque isso evita problema de direitos autorais); por que dez; por que textos de 200 a 400 palavras; e por que a lista de 30 termos regionais foi montada daquele jeito.

**Explique o encaminhamento ético**, mesmo que o questionário não tenha sido aplicado. Diga o que foi feito: a questão foi levada ao orientador no início do trabalho; o questionário seria anônimo, sem coleta de dados de identificação; e qual foi a decisão. Se não foi aplicado, diga isso aqui e retome nas Limitações. Tratar o assunto abertamente é sinal de maturidade da pesquisa.

## 5.4 Protocolo de medição

**Escreva**, em prosa, o protocolo que está em `docs/protocolo.md`:

- computador na tomada, sem outros programas pesados abertos;
- a mesma conexão de internet em todas as medições, identificada no texto;
- **três repetições** de cada medição de tempo, com uso da média;
- uma execução inicial descartada, para aquecimento;
- a mesma voz usada em todas as narrativas de cada ferramenta;
- o mesmo modelo de reconhecimento de fala para transcrever todos os áudios;
- o critério de normalização do texto antes da comparação (maiúsculas, pontuação e a decisão sobre acentos).

**Justifique, não apenas declare.** Por que três repetições? Porque uma medição sozinha pode sair distorcida por oscilação da rede ou do sistema. Por que a mesma voz? Porque trocar de voz no meio invalidaria a comparação. Por que normalizar o texto? Porque, sem isso, diferença de maiúscula ou de pontuação contaria como erro de pronúncia, que não é. Cada uma dessas frases mostra que você entendeu o que estava fazendo.

---

# 6. Materiais e Métodos
**Prazo: 27/10/2026**

Vale a analogia da receita de bolo do `README.md`: **lista de ingredientes** mais **modo de preparo**. É esta seção que permite (ou impede) que outra pessoa repita o trabalho.

## 6.1 Materiais

Para **cada** item, escreva três coisas: **o que é** (uma ou duas frases, com referência — a documentação oficial serve), **para que foi usado** e **por que foi escolhido**. Escrever só "foi utilizado Python" não vale nada.

| Item | O que dizer além da versão |
|---|---|
| Python 3.x | Linguagem dos scripts; é a linguagem do projeto Narrativas |
| gTTS | Ferramenta avaliada; depende de internet; qual língua e sotaque foram configurados |
| pyttsx3 | Ferramenta avaliada; usa as vozes do sistema; **qual voz** foi usada e se foi preciso instalá-la |
| edge-tts | Ferramenta avaliada; voz neural; **qual voz** (por exemplo, `pt-BR-FranciscaNeural`) |
| Piper (se foi usado) | Ferramenta avaliada; roda sem internet; qual modelo de voz |
| faster-whisper | Reconhecimento de fala usado para medir inteligibilidade; **qual modelo** |
| jiwer | Cálculo das taxas de erro de palavras e de caracteres |
| mutagen | Leitura da duração dos arquivos de áudio |
| Google Forms | Aplicação do questionário (se houve) |
| Google Sheets / Excel | Organização dos dados e geração dos gráficos |
| Git e GitHub | Versionamento e publicação do material, em repositório público próprio |

**O ambiente de execução — sem isto nada é replicável.** Informe: processador, memória RAM, tipo de disco, sistema operacional e versão, e a velocidade da conexão de internet. A internet importa porque duas das ferramentas dependem dela, e parte do tempo medido é tempo de rede.

**Justifique a escolha das ferramentas.** Por que essas e não outras? Os critérios usados foram: serem gratuitas, terem voz em português brasileiro, e cobrirem situações diferentes (com e sem internet, voz do sistema e voz neural). Escrever os critérios é melhor do que só listar as ferramentas.

**Declare também o que não foi usado e por quê:** não foi usado banco de dados, porque o volume de dados do experimento é pequeno e planilha atende melhor; não foi usado Django, porque o trabalho é composto por scripts de linha de comando. Justificar o que você **não** usou mostra que a escolha foi consciente, e não desconhecimento.

## 6.2 Métodos

**a) O corpus.** Quantas narrativas, de que obra vieram, de que ano, qual a situação de direitos autorais, quantas palavras cada uma. **Apresente a tabela de origem** (a planilha `corpus/origem.csv` vira uma tabela do TCC). Diga também como os textos foram limpos antes do uso — remoção de números de página e de quebras de linha, conferência de acentuação, preservação da pontuação — e por que a pontuação foi preservada (ela determina as pausas da fala sintetizada).

**b) A lista de termos regionais.** Como os 30 termos foram escolhidos, em que categorias foram agrupados e por quê. **A lista completa vai para um apêndice**, e um trecho dela aparece no corpo do texto.

**c) A geração dos áudios.** Qual voz de cada ferramenta, quais configurações (velocidade da fala, sotaque), em que formato cada uma salva e quantos áudios foram gerados ao todo. Se as ferramentas geram em formatos diferentes (WAV e MP3), **diga isso aqui** e explique como você tratou a comparação de tamanho.

**d) A medição da inteligibilidade.** Explique o método passo a passo, porque ele é a contribuição metodológica do seu trabalho: o áudio gerado foi transcrito por um programa de reconhecimento de fala; a transcrição e o texto original foram normalizados (maiúsculas, pontuação, acentos) e comparados; calcularam-se as taxas de erro de palavras e de caracteres. **Diga qual modelo de reconhecimento foi usado e que foi o mesmo para todas as ferramentas.** Registre também a decisão sobre acentos e a justificativa.

**e) A avaliação da pronúncia.** As duas formas usadas: verificação automática e verificação por escuta. Para a escuta, explique o procedimento: os arquivos foram renomeados e embaralhados para que você não soubesse qual ferramenta havia gerado cada áudio, e cada um foi classificado em três níveis (correto, reconhecível com erro, irreconhecível). **Declare que a avaliação foi feita pelo próprio autor** e que isso é uma limitação, atenuada pelo embaralhamento e pela apresentação conjunta da verificação automática.

**f) O questionário** (se houve). Quantos áudios, quantas perguntas, a escala usada, como os áudios foram identificados (letras, sem revelar a ferramenta), como foi divulgado, por quanto tempo ficou aberto, quantas pessoas responderam e como as respostas foram analisadas. Deixe claro que foi **anônimo** e sem coleta de dados de identificação. **O formulário completo vai para um apêndice.**

**g) A análise dos dados.** Como as três repetições foram agregadas (média e desvio padrão), como foram calculadas as médias de taxa de erro por ferramenta, e como as tabelas e os gráficos foram produzidos.

---

# 7. Resultados e Discussão
**Prazo: 10/11/2026**

O capítulo mais importante. Organize na mesma ordem dos objetivos específicos.

> **Regra sem exceção:** toda figura, tabela, quadro ou trecho de código é **anunciado no texto antes** de aparecer e **explicado depois**. Nunca duas figuras seguidas sem texto entre elas.

## 7.1 O corpus e os áudios gerados

Curta e objetiva. Apresente a tabela do corpus (narrativas, origem, número de palavras) e quantos áudios foram gerados ao todo. **Informe o endereço do repositório público** onde os áudios estão disponíveis — isso é um ponto forte do trabalho, porque permite a qualquer pessoa ouvir e conferir o que você mediu.

## 7.2 Viabilidade técnica: tempo, tamanho, conexão e custo

Tabela com uma linha por ferramenta: tempo médio de geração (com desvio padrão), tempo por palavra, tamanho por minuto de áudio, formato de saída, funciona sem internet, custo e limites de uso.

**Discuta:**

- a diferença de tempo entre as ferramentas, **lembrando que parte do tempo das que usam internet é tempo de rede**, e não de processamento. Isso não é um defeito da medição — é uma característica da solução, e é exatamente o que um gestor precisa saber antes de escolher;
- o resultado do teste **sem internet**, que é o mais importante para o projeto. Se apenas uma ferramenta funcionou offline, a conclusão prática já começa a se desenhar aqui;
- os limites de uso e os termos de serviço encontrados. Uma ferramenta gratuita com limite diário pode não servir para gerar o áudio de um acervo inteiro.

## 7.3 Inteligibilidade

Tabela com o WER e o CER médios por ferramenta, com desvio padrão. Um gráfico de barras ajuda — e na legenda diga que **quanto menor, melhor**, porque nem todo leitor sabe.

**Discuta, e discutir é mais do que apresentar:**

- qual ferramenta foi mais compreensível, e a distância entre elas;
- **exemplos concretos de erro.** Mostre trechos: o texto original de um lado, a transcrição do outro, com as palavras erradas destacadas. Um exemplo vale mais que uma coluna de números, e este é o tipo de figura que faz o leitor entender o problema de imediato;
- se a taxa de erro foi maior nas narrativas com mais termos regionais do que nas mais neutras. **Se foi, você acabou de confirmar a hipótese central do trabalho** — apresente essa comparação com destaque;
- se alguma ferramenta teve variação grande entre as narrativas, o que indicaria instabilidade.

## 7.4 Pronúncia dos termos regionais

Esta é a seção mais original do seu trabalho. Duas tabelas:

- acertos por **ferramenta**: quantos dos 30 termos cada uma pronunciou corretamente, pela escuta e pela verificação automática;
- acertos por **categoria**: seres do folclore, cidades do RN, natureza, cultura, comida.

**Discuta:**

- em que categoria as ferramentas erram mais. Se todas erram nos nomes de cidade, ou todas erram nos nomes do folclore, esse padrão é um resultado;
- **os termos que todas erraram.** Se há um conjunto de palavras que nenhuma ferramenta acerta, a conclusão prática muda completamente: não adianta trocar de ferramenta, seria preciso um dicionário de pronúncia. Essa é uma recomendação muito concreta para o projeto Narrativas;
- **que tipo de erro** aconteceu. Sílaba tônica trocada, som aberto virando fechado, palavra lida letra por letra, palavra lida como se fosse inglês. Descrever o tipo de erro é mais útil do que contar quantos foram;
- se a verificação automática e a escuta concordaram. Quando discordam, vale comentar por quê — pode ser limitação do reconhecimento de fala, e isso reforça a necessidade da avaliação humana.

**Inclua exemplos citáveis**, do tipo "a ferramenta X leu 'Seridó' como 'Serido'" ou "'xique-xique' foi soletrado letra por letra". São esses trechos que vão ser lembrados por quem ler.

## 7.5 Avaliação com ouvintes

**Se o questionário foi aplicado:** informe quantas pessoas responderam e apresente a média e o desvio padrão das notas de naturalidade e de inteligibilidade por ferramenta. Gráfico de barras com a barra de erro. Apresente também os comentários da pergunta aberta, agrupados por assunto, com duas ou três citações — **sem qualquer identificação de quem respondeu**.

Discuta se a percepção das pessoas bateu com as medidas automáticas. **Se não bateu, isso é um resultado interessante**, não um problema: significa que os dois métodos medem coisas diferentes, e explicar isso é uma discussão de alto nível. Uma voz pode ser perfeitamente inteligível para um programa de reconhecimento e ainda assim soar desagradável para uma pessoa.

**Se o questionário não foi aplicado:** escreva uma subseção curta explicando que a avaliação subjetiva não foi realizada, por qual razão, e que ela fica como trabalho futuro. Depois siga em frente. **Não invente dados, em nenhuma hipótese**, e não deixe o assunto sem explicação — o leitor vai estranhar a ausência se ela não for justificada.

## 7.6 Quadro comparativo e recomendação

Um quadro com uma linha por ferramenta e colunas de pontos fortes, pontos fracos, quando usar e quando não usar. **Este quadro é a contribuição prática do seu TCC** — é o que a equipe do Narrativas vai olhar.

E então responda, de forma direta, à pergunta do trabalho: a narração automática é viável para o acervo? Qual ferramenta é recomendada? O que precisaria ser resolvido antes de usar em produção? Ou a conclusão é que, para este acervo, a narração precisa continuar sendo humana?

**Qualquer uma dessas respostas é um bom resultado, inclusive a última.** Um trabalho que conclui "não dá, e aqui está a medição que mostra por quê" é tão útil quanto o contrário. Não force um resultado positivo.

## 7.7 Limitações do trabalho

Subseção curta e honesta. Reconhecer limite aumenta a confiança no trabalho:

- o corpus tem **dez narrativas**, de duas obras, e pode não representar toda a variedade das narrativas populares potiguares;
- a inteligibilidade foi medida por **reconhecimento automático de fala**, que é um indício e não uma prova, já que o próprio reconhecedor comete erros e foi treinado com voz humana;
- a avaliação de pronúncia foi feita **pelo próprio autor**, ainda que com os áudios embaralhados;
- foram avaliadas **ferramentas gratuitas**, em uma configuração de voz por ferramenta; outras vozes poderiam dar resultados diferentes;
- as medições foram feitas em **uma única máquina** e com uma única conexão de internet;
- (se for o caso) a **avaliação com ouvintes não foi realizada**, pela razão X.

Depois de listar, acrescente o argumento que sustenta o trabalho: como o estudo é **comparativo**, essas limitações valem igualmente para todas as ferramentas. O que se compara é uma ferramenta contra a outra, nas mesmas condições.

---

# 8. Conclusão
**Prazo: 17/11/2026**

Duas a três páginas no máximo. Nada de resultado, conceito ou citação que não tenha aparecido antes.

**Escreva, nesta ordem:**

1. **Retomada do problema e do objetivo geral**, afirmando que ele foi alcançado **e dizendo por quê, com número**: "[...] foi alcançado, uma vez que a comparação das três ferramentas mostrou taxas de erro de palavras entre X% e Y% e acertos de pronúncia entre Z e W dos 30 termos regionais avaliados."

2. **Um comentário por objetivo específico**, na mesma ordem em que foram apresentados, cada um apontando o resultado que o comprova.

3. **A resposta à pergunta de pesquisa**, em um parágrafo direto: a síntese de voz gratuita dá conta de narrar narrativas populares potiguares? Em que condições? Com qual ferramenta?

4. **Contribuições:** um corpus de narrativas populares preparado e com origem documentada; um método de avaliação de síntese de voz que não depende de aprovação ética e pode ser repetido por outros trabalhos; a medição inédita do comportamento dessas ferramentas diante do vocabulário regional nordestino; e uma recomendação técnica concreta para o projeto Narrativas, com o material todo disponível em repositório público.

5. **Limitações e dificuldades:** retome brevemente as limitações do capítulo anterior e acrescente as dificuldades reais que você enfrentou — a ausência de voz em português no sistema, o tempo de transcrição, a decisão sobre como normalizar os acentos, a questão ética do questionário. É aqui que o `docs/diario.md` das sprints se paga.

6. **Trabalhos futuros**, concretos e ligados ao que você encontrou:
   - implementar a narração automática na plataforma Narrativas, com a ferramenta recomendada (esta é a principal);
   - construir um **dicionário de pronúncia** dos termos regionais que todas as ferramentas erraram, e medir o ganho que ele traz — se você fez o teste extra de "ensinar" a pronúncia, cite o indício que encontrou;
   - aplicar a avaliação com ouvintes, com o devido encaminhamento ético, incluindo pessoas com deficiência visual e moradores das regiões de origem das narrativas;
   - ampliar o corpus e incluir ferramentas pagas na comparação;
   - avaliar a possibilidade de narração por voluntários da comunidade como alternativa culturalmente mais próxima.

**Não escreva** que "a ferramenta X é a melhor" sem dizer em qual critério e sobre qual corpus. E não generalize para "síntese de voz em português" o que você mediu em dez narrativas, três ferramentas e uma máquina.

---

# 9. Resumo, Título e revisão final
**Prazo: 24/11/2026**

## 9.1 Resumo

Escrito **por último**, depois de o texto todo estar aprovado pelo orientador. Parágrafo único, 150 a 500 palavras, linguagem impessoal, sem citações, sem siglas pouco conhecidas e sem menção a figuras ou tabelas (NBR 6028:2021).

Uma ou duas frases para cada item:

1. **contexto e problema:** as narrativas populares nasceram para ser ouvidas, e gravar narração humana para um acervo inteiro é inviável;
2. **objetivo:** o que o trabalho se propôs a avaliar;
3. **método:** três ferramentas gratuitas de síntese de voz, dez narrativas de domínio público, medição de inteligibilidade por transcrição automática e avaliação da pronúncia de 30 termos regionais;
4. **resultados:** os números principais — taxas de erro, acertos de pronúncia, tempo, funcionamento sem internet;
5. **conclusão:** a recomendação e o encaminhamento para o projeto.

**Coloque números no resumo.** Em um trabalho que mede coisas, resumo sem número é resumo fraco — e é o resumo que faz alguém decidir se lê o resto.

O **Abstract** é a versão em inglês. Os termos da área têm forma consagrada em inglês (*text-to-speech*, *speech synthesis*, *word error rate*, *oral tradition*, *intangible cultural heritage*); use-as, e não a tradução literal. Não entregue tradução automática sem revisar.

**Palavras-chave** (3 a 5), separadas por ponto e vírgula. Campo de ideias: síntese de voz; narrativas populares; acessibilidade digital; patrimônio cultural imaterial; acervo digital. Escolha os termos pelos quais alguém **procuraria** o seu trabalho — e procure equilibrar o lado técnico e o lado cultural, porque as duas comunidades podem se interessar.

## 9.2 Título

**Última coisa a ser definida**, em acordo com o orientador. Deve indicar **o que foi feito** e **em que contexto**, e combinar com o objetivo geral.

A temática já sugere um título provisório: *"Avaliação de ferramentas de síntese de voz para a narração automatizada de narrativas populares em português brasileiro"*. Ele funciona, e você pode refiná-lo. Pontos a cobrir: a ação (avaliação ou comparação), o objeto (ferramentas de síntese de voz), a aplicação (narração de narrativas populares) e, se couber, o recorte regional. Se houver subtítulo, separe com dois-pontos. Evite título genérico demais e não prometa no título mais do que o trabalho mediu.

## 9.3 Revisão final — checklist

Além do checklist do `README.md`:

- [ ] O objetivo geral, os objetivos específicos, as seções dos Resultados e os parágrafos da Conclusão estão na mesma ordem e falando das mesmas coisas?
- [ ] Todos os números citados no Resumo, nos Resultados e na Conclusão são **exatamente** os mesmos?
- [ ] Toda métrica que aparece nos Resultados foi explicada no Referencial?
- [ ] A origem e a situação de direitos autorais de cada texto do corpus estão declaradas?
- [ ] Está dito que nenhum texto de autor ainda protegido foi reproduzido?
- [ ] O encaminhamento da questão ética do questionário está descrito na Metodologia?
- [ ] Se houve questionário, está declarado que foi anônimo, e nenhuma resposta permite identificar quem respondeu?
- [ ] Toda tabela e figura é citada no texto antes de aparecer e explicada depois?
- [ ] Todas as tabelas e figuras têm identificação em cima, centralizada, e fonte embaixo?
- [ ] Os gráficos têm unidade no eixo, e a legenda diz se "menor é melhor"?
- [ ] O ambiente de execução está descrito (máquina, sistema, versões, internet)?
- [ ] Está dito quantas repetições foram feitas de cada medição?
- [ ] A seção de limitações está presente e honesta?
- [ ] As siglas (TTS, WER, CER, MOS, LGPD, CEP, IPHAN, UNESCO) foram escritas por extenso na primeira ocorrência?
- [ ] A numeração das seções está sem ponto após o número ("2.1 Narrativas populares e tradição oral")?
- [ ] O texto está impessoal e no passado?
- [ ] O endereço do repositório público está no texto e o repositório está acessível?
- [ ] Os apêndices (lista de termos, questionário) estão incluídos?
- [ ] Todos os comentários do orientador no documento do Drive foram respondidos?
- [ ] A versão final foi nomeada no histórico de versões do Drive?

---

## Referências mínimas a garantir

Como o trabalho é interdisciplinar, o referencial precisa ser equilibrado:

**Lado cultural:**

- **2 a 3 obras sobre tradição oral e narrativas populares** (Seção 4.1) — Cascudo é praticamente obrigatório aqui, ainda mais sendo um trabalho potiguar;
- **2 a 3 obras ou documentos sobre patrimônio imaterial e acervos digitais** (Seção 4.2), incluindo a Convenção da UNESCO;

**Lado técnico:**

- **3 a 4 obras sobre síntese de voz** (Seção 4.3), com pelo menos uma obra de referência da área;
- **2 a 3 fontes sobre acessibilidade digital** (Seção 4.4), incluindo a Lei nº 13.146/2015 e o eMAG ou as WCAG;
- **2 a 3 fontes sobre avaliação de qualidade de voz** (Seção 4.5), incluindo a recomendação ITU-T P.800 para o MOS;
- **4 a 6 trabalhos relacionados** (Seção 4.6);

**Obrigatórias:**

- **2 obras de metodologia científica** — Gil (2017) e Prodanov e Freitas (2013), já no `README.md`;
- **a legislação citada** — Lei nº 13.146/2015, Lei nº 13.709/2018 (LGPD) e Lei nº 9.610/1998 (direitos autorais, que você vai citar ao justificar o corpus de domínio público);
- **a documentação oficial das ferramentas** avaliadas.

Anote a referência completa de **tudo** o que ler, na seção de Referências do documento do Drive, desde o primeiro dia. Zotero e Mendeley ajudam a montar, mas confira cada entrada contra a NBR 6023:2018 antes de entregar: esses gerenciadores erram com frequência.
