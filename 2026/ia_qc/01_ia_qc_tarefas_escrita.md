# Quarto Chinês — Orientações de Escrita do TCC (Ciclo 1)

**Estudante:** Curso Técnico Integrado em Informática
**Orientação:** NIC
**Tema:** Bancada de estratégias de casamento sintático e o argumento do Quarto Chinês
**Data de início:** 23/09/2026
**Documento do TCC:** já foi compartilhado pelo coordenador no **Google Drive**. Escreva diretamente nele, sem criar cópias paralelas.

> **Importante:** este documento diz **o que pesquisar e sobre o que escrever** em cada seção. Ele **não contém o texto final** — o texto é seu. As orientações gerais de escrita, as normas da ABNT e as regras de citação, figuras, tabelas e referências estão no `README.md` deste repositório; **leia-o antes de começar**. O que você vai programar a cada semana está em [01_ia_qc_tarefas_desenvolvimento.md](01_ia_qc_tarefas_desenvolvimento.md).

---

## Sumário

- [1. Antes de começar](#1-antes-de-começar)
- [2. Cronograma de entregas](#2-cronograma-de-entregas)
- [3. Estrutura prevista do TCC](#3-estrutura-prevista-do-tcc)
- [4. Orientações por seção](#4-orientações-por-seção)
  - [4.1 Introdução](#41-introdução)
  - [4.2 Objetivo Geral](#42-objetivo-geral)
  - [4.3 Referencial Teórico](#43-referencial-teórico)
  - [4.4 Metodologia](#44-metodologia)
  - [4.5 Materiais e Métodos](#45-materiais-e-métodos)
  - [4.6 Resultados](#46-resultados)
  - [4.7 Conclusão](#47-conclusão)
  - [4.8 Resumo, Objetivos Específicos e Título](#48-resumo-objetivos-específicos-e-título)
- [5. Do TCC ao artigo: onde publicar](#5-do-tcc-ao-artigo-onde-publicar)
- [6. Erros comuns neste tema](#6-erros-comuns-neste-tema)
- [7. Checklist antes de cada entrega](#7-checklist-antes-de-cada-entrega)

---

## 1. Antes de começar

**O que o seu TCC afirma:** *"Implementamos cinco estratégias puramente sintáticas para escolher a resposta de um sistema de regras (igualdade exata, normalização, contém, palavras-chave e similaridade textual), executamos todas sobre a mesma bateria de 100 mensagens, com gabarito definido antes do experimento, e medimos respostas adequadas, inadequadas, ausência de resposta e tempo. Discutimos, à luz do argumento do Quarto Chinês de John Searle, por que o aumento de acertos representa um aumento da aparência de compreensão, e não de compreensão."*

**O que o seu TCC NÃO afirma:**
- **não** diz que o sistema "entende", "compreende" ou "pensa" — e também não diz que prova que as máquinas **nunca** vão entender. O trabalho **ilustra** o argumento de Searle; não o prova nem o refuta;
- **não** diz qual é "a melhor estratégia" de forma geral — os resultados valem para **esta** bateria, **este** livro de 12 regras e **este** limiar;
- **não** traz opinião de usuários — **não houve teste com pessoas** (isso depende do Comitê de Ética e fica como trabalho futuro);
- **não** usa IA dentro do sistema — nenhum modelo de linguagem, nenhum aprendizado de máquina.

**Dois cuidados de linguagem:**
- troque "o sistema entendeu a pergunta" por **"o sistema escolheu a regra adequada"**. No seu TCC, a diferença entre essas duas frases **é o assunto do trabalho**;
- use **"resposta adequada"** e **"resposta inadequada"** (os termos do experimento), e não "certa" e "errada" soltos.

**Como trabalhar no Google Drive:**
- escreva direto no documento compartilhado; **não crie cópias**;
- ao terminar uma seção, use **Arquivo → Histórico de versões → Nomear versão atual** (ex.: `v1 - Introdução - 30/09`);
- **resolva os comentários** do orientador antes de entregar a seção seguinte;
- ao entregar, avise o orientador dizendo **qual seção** está pronta.

**Regra de ouro:** escreva a partir do **diário de bordo** (`docs/diario.md`) e do **protocolo** (`docs/protocolo.md`) do repositório. O texto cresce junto com o experimento, e não no final.

---

## 2. Cronograma de entregas

Hoje é **23/09/2026** (quarta-feira). Cada prazo conta a partir da conclusão da etapa anterior.

| # | Seção | Prazo | Duração | Sprints que alimentam a seção |
|---|---|---|---|---|
| 1 | Introdução e Objetivo Geral | **30/09/2026** (quarta) | 1 semana a partir de hoje | Sprint 1 |
| 2 | Referencial Teórico | **14/10/2026** (quarta) | 2 semanas após a Introdução | Sprints 1, 2 e 3 |
| 3 | Metodologia | **21/10/2026** (quarta) | 1 semana após o Referencial | Sprints 3 e 4 |
| 4 | Materiais e Métodos | **28/10/2026** (quarta) | 1 semana após a Metodologia | Sprints 3, 4 e 5 |
| 5 | Resultados | **11/11/2026** (quarta) | 2 semanas após Materiais e Métodos | Sprints 6 e 7 |
| 6 | Conclusão | **18/11/2026** (quarta) | 1 semana após os Resultados | Sprint 8 |
| 7 | Resumo, Objetivos Específicos e Título | **25/11/2026** (quarta) | 1 semana após a Conclusão | Encerramento |

**Atenção ao prazo dos Resultados.** A execução oficial do experimento acontece na Sprint 7 (até 10/11). Por isso, escreva os Resultados em duas partes: de **29/10 a 04/11**, a parte que já existe (o livro de regras, a bateria, as estratégias com trechos de código e a tela do comando); de **05 a 11/11**, as tabelas, os gráficos e a discussão.

**Dica de ritmo:** escreva um pouco ao longo da semana, e não na véspera. Duas sessões de uma hora rendem mais do que uma madrugada.

---

## 3. Estrutura prevista do TCC

Siga a estrutura do `README.md`. Para este tema:

```
Título
Resumo / Palavras-chave
Abstract / Keywords
1 INTRODUÇÃO
  1.1 Objetivo geral
  1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
  2.1 Inteligência artificial e chatbots
  2.2 Chatbots baseados em regras: do ELIZA aos sistemas de perguntas frequentes
  2.3 Comparação de textos: normalização, busca de trechos e similaridade
  2.4 O argumento do Quarto Chinês: sintaxe e semântica
  2.5 Trabalhos relacionados
3 METODOLOGIA
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
  5.1 A bancada desenvolvida
  5.2 Desempenho das estratégias
  5.3 Onde cada estratégia acerta e erra
  5.4 A aparência de compreensão: discussão à luz do Quarto Chinês
  5.5 Limitações
6 CONCLUSÃO
REFERÊNCIAS
APÊNDICES (A: livro de regras; B: bateria de 100 mensagens com gabarito)
```

---

## 4. Orientações por seção

---

### 4.1 Introdução

**Prazo: 30/09/2026** | Tamanho sugerido: 5 a 7 parágrafos

Siga a sequência de parágrafos do `README.md`: contexto → problema → caminho para a solução → solução proposta → vínculo com o projeto → objetivos e organização. **Leia antes a introdução que já existe em `.llm/ia_qc/projeto.md`** — ela é do projeto pai e tem bons pontos de partida e referências, mas **o seu texto é outro**: o foco do seu TCC é o experimento com as estratégias.

#### Parágrafo 1 — Contextualização

**Pesquise sobre:**
- o crescimento do uso de *chatbots* e assistentes virtuais no dia a dia (atendimento de empresas, serviços públicos, escolas). Procure um dado recente e confiável — por exemplo, no artigo da Harvard Business Review já citado no projeto (ZAO-SANDERS, 2026) ou em pesquisas do Cetic.br (TIC Domicílios);
- o fato de que muitos *chatbots* de atendimento **não usam IA generativa**: funcionam com regras e respostas prontas.

**Escreva sobre:** como conversar com programas se tornou comum e como, muitas vezes, as pessoas não sabem se estão falando com um sistema "inteligente" ou com uma lista de regras.

> **Cuidado:** não comece com "Desde os primórdios da humanidade..." nem com "Nos dias atuais, a tecnologia...". Comece com o fato ou o dado que interessa.

#### Parágrafo 2 — Problemática

**Pesquise sobre:** o chamado **efeito ELIZA** — a tendência das pessoas de atribuir compreensão a programas que apenas manipulam texto (Weizenbaum, 1966, relata as reações ao seu programa); e a pergunta de Searle: *podem os computadores pensar?* (SEARLE, 1980; 1984).

**Escreva sobre:** o problema de que **responder de forma adequada não é o mesmo que entender**. Um sistema pode parecer inteligente só porque encontra a resposta certa com frequência. E, quando erra, pode errar **com confiança**, o que engana mais do que ficar calado. Termine o parágrafo com a pergunta que o seu trabalho investiga (ver 1ª seção do documento de desenvolvimento).

#### Parágrafo 3 — Caminho para a solução

**Pesquise sobre:** o experimento mental do **Quarto Chinês** (SEARLE, 1980) e a distinção entre **sintaxe** (a forma dos símbolos) e **semântica** (o significado); as formas simples de comparar textos usadas em *chatbots* de regras (igualdade, palavras-chave, similaridade). Cite 1 ou 2 trabalhos que discutem o Quarto Chinês hoje (LIMA FILHO, 2010; CANDIOTTO, 2025 — estão nas referências do projeto).

**Escreva sobre:** a ideia de que dá para **construir** um pequeno "quarto chinês" em software e **medir** até onde ele consegue ir apenas manipulando símbolos. Explique por que isso transforma uma discussão filosófica em algo observável.

#### Parágrafo 4 — Apresentação da solução

**Escreva sobre** o que foi feito, sem exagerar:
- uma **bancada de experimentação** desenvolvida em Python e Django;
- **cinco estratégias** sintáticas (cite os nomes);
- uma **bateria fixa de 100 mensagens**, com **gabarito definido antes** dos testes;
- os indicadores medidos: respostas adequadas, inadequadas, ausência de resposta e tempo.

Diga claramente que **não houve teste com pessoas** e que **nenhuma técnica de IA** foi usada dentro do sistema — isso é proposital.

#### Parágrafo 5 — Vínculo com o projeto

**Escreva sobre:** o NIC e o projeto de pesquisa "Podem os computadores pensar?" (consulte `.llm/ia_qc/projeto.md`), que estuda o argumento de Searle e desenvolve uma aplicação que simula o Quarto Chinês. Diga que **este TCC é uma parte** desse projeto: a parte que **mede**, com um experimento, o comportamento de um sistema de regras.

#### Último parágrafo — Objetivos e organização

Apresente o objetivo geral (seção 1.1) e um parágrafo curto dizendo o que cada capítulo traz ("O Capítulo 2 apresenta...").

---

### 4.2 Objetivo Geral

**Prazo: 30/09/2026** (junto com a Introdução) | Tamanho: **uma frase**

Uma frase, com **um verbo principal**, coerente com o que você vai fazer. Siga o modelo do `README.md`.

Estrutura para você completar (não copie; ajuste com o orientador):

> "O objetivo principal do presente trabalho consiste em comparar [...] estratégias de [...] em um sistema de respostas baseado em regras, a fim de analisar [...] à luz do argumento do Quarto Chinês."

**Confira:**
1. O verbo é concreto? ("comparar", "avaliar", "desenvolver e avaliar" — e não "estudar" ou "abordar").
2. Ele promete só o que será feito? Se disser "provar que as máquinas não pensam" ou "validar com usuários", está errado.
3. Na Conclusão, você conseguirá escrever "o objetivo foi alcançado porque..."?

> Os **objetivos específicos** são escritos por último (25/11). Deixe um rascunho na seção 1.2 e reescreva no final.

---

### 4.3 Referencial Teórico

**Prazo: 14/10/2026** (2 semanas) | Assista antes ao vídeo do `README.md`: https://youtu.be/8Qztq1Q5vb0

Lembre-se da analogia do `README.md`: o Referencial explica os conceitos que um leitor de fora da área não conhece. Aqui, o leitor vai tropeçar em: *chatbot*, regra, normalização, similaridade de textos, sintaxe, semântica, Quarto Chinês. **Explique só o que você vai usar nos Resultados.** Como o seu código funciona vai em Materiais e Métodos, não aqui.

#### 2.1 Inteligência artificial e *chatbots*

**Pesquise sobre:** definições de inteligência artificial (RUSSELL; NORVIG — procure a edição em português; e as referências do projeto: GOMES, 2010; TEIXEIRA, 2019); o **Teste de Turing** (TURING, 1950), que avalia a máquina pelo **comportamento** observado de fora; o que é um *chatbot*.

**Escreva sobre:** o que é IA, a ideia do Teste de Turing (julgar pela aparência do comportamento) e o que é um *chatbot*. Seja breve: 3 a 4 parágrafos. O Teste de Turing é importante porque o seu experimento também mede **o comportamento de fora** — e é justamente isso que Searle critica.

#### 2.2 *Chatbots* baseados em regras

**Pesquise sobre:** o **ELIZA** (WEIZENBAUM, 1966) — como funcionava (palavras-chave e modelos de frases) e como as pessoas reagiram; o **A.L.I.C.E.** e a linguagem AIML (WALLACE, 2009); os *chatbots* de perguntas frequentes (FAQ) usados em atendimento; a diferença entre *chatbots* baseados em regras e os baseados em modelos de linguagem.

**Escreva sobre:** como um *chatbot* de regras escolhe uma resposta (livro de regras: gatilho → resposta) e por que ele é um bom objeto para estudar a diferença entre responder e entender. Explique o **efeito ELIZA**.

#### 2.3 Comparação de textos

**Pesquise sobre:**
- **normalização de texto** (minúsculas, remoção de acentos e pontuação) — procure no livro de Jurafsky e Martin, *Speech and Language Processing*, capítulo sobre normalização de texto (versão gratuita no site dos autores);
- **busca de subcadeias** (verificar se um trecho está contido em um texto) e **palavras-chave**;
- **similaridade entre sequências de caracteres**: a ideia de medir o quanto dois textos se parecem; o algoritmo de Ratcliff/Obershelp, que é a base do `SequenceMatcher` do Python (RATCLIFF; METZENER, 1988), e a documentação oficial do módulo `difflib`; cite também a distância de Levenshtein como exemplo de outra medida.

**Escreva sobre:** cada técnica em linguagem simples, com um exemplo de frase. Monte um **quadro** com as cinco técnicas (nome, o que faz, exemplo, o que **não** consegue perceber). Ponto central: **todas operam sobre a forma do texto, nenhuma sobre o significado.**

#### 2.4 O argumento do Quarto Chinês: sintaxe e semântica

É a seção mais importante do Referencial. Dedique a ela o maior tempo de leitura.

**Pesquise sobre:**
- o experimento mental como Searle o descreve (SEARLE, 1980, *Minds, brains, and programs*; e SEARLE, 1984, *Mente, cérebro e ciência*, que está nas referências do projeto);
- a distinção entre **IA fraca** e **IA forte**;
- a frase central de Searle: programas têm **sintaxe**, mas não **semântica**;
- pelo menos **duas réplicas** ao argumento (a Resposta dos Sistemas e a Resposta do Robô) e o que Searle respondeu;
- o debate atual, com a IA generativa (CANDIOTTO, 2025; OLIVEIRA, 2025; LIMA FILHO, 2010 — todos nas referências do projeto).

**Escreva sobre:** o experimento passo a passo (a pessoa, o livro de regras, os símbolos que entram e saem, quem está do lado de fora); o que Searle conclui; as réplicas; e **a correspondência com o seu trabalho**. Monte um quadro:

| No Quarto Chinês | Na bancada desenvolvida |
|---|---|
| Os símbolos em chinês que entram | A mensagem do usuário |
| O livro de regras | A tabela de regras no banco de dados |
| A pessoa que segue as regras | A estratégia de casamento (o código) |
| Os símbolos que saem | A resposta pré-cadastrada |
| Quem está do lado de fora e acha que há compreensão | Quem lê as respostas adequadas |

#### 2.5 Trabalhos relacionados

**Pesquise** no Google Acadêmico, na SBC OpenLib (https://sol.sbc.org.br), no Portal de Periódicos da CAPES e na SciELO:
- `"quarto chinês" searle inteligência artificial`;
- `"chinese room" chatbot`;
- `chatbot "baseado em regras" avaliação`;
- `"string similarity" chatbot "question matching"`;
- `chatbot FAQ "casamento de padrões"`.

**Escreva sobre:** 4 a 6 trabalhos — alguns que **discutem** o Quarto Chinês e outros que **avaliam** *chatbots* de regras ou comparam formas de casar perguntas. Para cada um: o que fez, como avaliou e o que concluiu. Termine com um **quadro comparativo** (colunas: trabalho, discute o Quarto Chinês?, implementa um sistema?, compara estratégias?, bateria com gabarito prévio?). A última linha é o **seu trabalho** — e ela deve mostrar o que ele traz de diferente: **unir a discussão filosófica a uma medição**.

**Leituras de partida** (localize a fonte original antes de colocar nas Referências e **confira todos os dados**):
- SEARLE, J. R. Minds, brains, and programs. *Behavioral and Brain Sciences*, v. 3, n. 3, p. 417-457, 1980;
- SEARLE, J. R. *Mente, cérebro e ciência*. Lisboa: Edições 70, 1984;
- TURING, A. M. Computing machinery and intelligence. *Mind*, v. 59, n. 236, p. 433-460, 1950;
- WEIZENBAUM, J. ELIZA: a computer program for the study of natural language communication between man and machine. *Communications of the ACM*, v. 9, n. 1, p. 36-45, 1966;
- RATCLIFF, J. W.; METZENER, D. E. Pattern matching: the gestalt approach. *Dr. Dobb's Journal*, 1988;
- PYTHON SOFTWARE FOUNDATION. *difflib — Helpers for computing deltas* (documentação oficial);
- JURAFSKY, D.; MARTIN, J. H. *Speech and Language Processing* (3. ed., versão preliminar on-line);
- LIMA FILHO (2010), CANDIOTTO (2025) e OLIVEIRA (2025), já listados no projeto.

---

### 4.4 Metodologia

**Prazo: 21/10/2026** | Veja exemplos de metodologia na pasta do orientador: https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

Aqui você descreve **o caminho** da pesquisa. As ferramentas, as versões e os detalhes de cada estratégia ficam para Materiais e Métodos.

- **Classificação da pesquisa:** quanto à natureza, **aplicada**; quanto aos objetivos, **exploratória**; quanto à abordagem, **quantitativa** (contagens e tempo), com **análise qualitativa** dos exemplos de erro; quanto aos procedimentos, **pesquisa bibliográfica** seguida de **desenvolvimento de software** e **pesquisa experimental** (as mesmas mensagens submetidas a cinco "tratamentos" diferentes). Confirme a classificação com o orientador e **cite um autor de metodologia** para cada termo (ver a seção "Classificação da pesquisa" do `README.md`).
- **Pesquisa bibliográfica:** em que bases pesquisou, com quais palavras-chave (as da seção 2.5) e como escolheu os trabalhos.
- **Etapas** (faça **uma figura do fluxo** no draw.io — `https://app.diagrams.net`, gratuito, no navegador):
  1. estudo do argumento do Quarto Chinês e das técnicas de comparação de textos;
  2. construção do livro de regras (12 regras);
  3. elaboração da bateria de 100 mensagens e do gabarito;
  4. **congelamento** da bateria e do gabarito (com a data e a marcação no Git);
  5. implementação das cinco estratégias, com testes automáticos;
  6. implementação do comando de execução do experimento;
  7. execução oficial e coleta dos resultados;
  8. análise quantitativa e qualitativa e discussão à luz do referencial.
- **O gabarito definido antes:** explique **por que** a bateria e o gabarito foram escritos e congelados **antes** das estratégias — para que os resultados não fossem ajustados depois de conhecidos. Isso dá credibilidade ao trabalho; escreva com destaque.
- **Aspectos éticos:** escreva, em uma frase, que o trabalho **não envolveu seres humanos** — as mensagens foram escritas pelo próprio autor — e que, por isso, não houve submissão ao Comitê de Ética. A avaliação é **instrumental**: incide sobre o comportamento do sistema, não sobre pessoas.
- **Limitações do método:** as mensagens foram escritas por uma só pessoa (o autor), que também conhecia as regras; 12 regras e 100 mensagens; um único limiar de similaridade; um único computador para medir o tempo.

---

### 4.5 Materiais e Métodos

**Prazo: 28/10/2026** | Lembre-se da analogia da **receita de bolo** do `README.md`: outra pessoa deve conseguir repetir o seu experimento só lendo esta seção. Use o `docs/protocolo.md` e o `docs/ambiente.md`.

**Materiais** — quadro com o que foi usado (as versões estão no `docs/ambiente.md`):

| Material | Versão | Para que foi usado |
|---|---|---|
| Computador (processador, memória, Windows) | anotar | Execução do experimento |
| Python | anotar | Linguagem de programação |
| Django | anotar | Banco de dados, painel de administração e comando do experimento |
| SQLite | a do Python | Armazenamento do livro de regras |
| Módulos `unicodedata`, `string` e `difflib` | biblioteca padrão | Normalização e similaridade |
| `time.perf_counter` | biblioteca padrão | Medição de tempo |
| matplotlib | anotar | Gráficos |
| Git e GitHub | anotar | Versionamento e congelamento da bateria |
| Google Planilhas | – | Escrita da bateria e tabelas dinâmicas |

**Métodos** — para cada item, explique **o que é, como foi feito e por que foi escolhido**:
- **o livro de regras:** o tema (dúvidas sobre o campus), as 12 regras, os campos de cada regra e o fato de as respostas serem fictícias. Coloque um exemplo de regra completa em um quadro e todas as regras no **Apêndice A**;
- **a bateria:** as 5 categorias, a quantidade de cada uma, um exemplo de cada, e o critério de escrita. A bateria completa vai no **Apêndice B**;
- **as cinco estratégias:** para cada uma, a regra de decisão **em palavras** e os parâmetros (limiar de 0,75; mínimo de 50% das palavras-chave; critério de desempate). Um trecho de código curto pode entrar aqui ou nos Resultados — combine com o orientador para não repetir;
- **a classificação:** a tabela de adequada / inadequada / sem resposta (ver Sprint 3 do documento de desenvolvimento);
- **a medição de tempo:** 10 repetições da bateria inteira por estratégia, média em milissegundos, sem contar a leitura do banco;
- **a reprodutibilidade:** o repositório público, as *tags* `bateria-congelada` e `execucao-oficial`, e os comandos para repetir o experimento.

---

### 4.6 Resultados

**Prazo: 11/11/2026** (2 semanas) | Esta é a vitrine do trabalho. Siga a seção "Resultados" do `README.md`: toda figura, tabela e código é **anunciado no texto antes** e **comentado depois**.

#### 5.1 A bancada desenvolvida

- uma figura da **estrutura do sistema** (mensagem → estratégia → regra escolhida → resposta), feita no draw.io;
- o *print* do livro de regras no Django Admin;
- **um ou dois trechos de código** curtos e comentados — por exemplo, a função `normalizar` e a `similaridade` (legenda ABNT, como um quadro ou figura);
- o *print* da saída do comando `testar_estrategias`;
- os testes automáticos (quantos, e o que verificam).

#### 5.2 Desempenho das estratégias

- a **tabela comparativa** (adequadas, inadequadas, sem resposta, tempo médio);
- o **gráfico de barras** da classificação e o do tempo;
- descreva o que os números mostram: qual estratégia teve mais adequadas? Qual teve mais inadequadas? As duas coisas andaram juntas? Quanto o tempo variou — e ele **importa**, para este tamanho de livro?

#### 5.3 Onde cada estratégia acerta e erra

- a **tabela por categoria** (identica, forma, parafrase, digitacao, fora);
- mostre **onde** está o ganho: a normalização resolve a categoria `forma`? A similaridade resolve a `digitacao`? Alguma estratégia resolve bem as paráfrases?
- o **quadro de exemplos** da Tarefa 7.4 (mensagem × resposta de cada estratégia), com a explicação de **por que** cada estratégia errou. Os casos da categoria `fora` que receberam resposta são o seu melhor material: o sistema respondeu **com confiança** algo que não foi perguntado;
- se fez a análise do limiar (Tarefa 7.5), apresente-a aqui, como **complementar**.

#### 5.4 A aparência de compreensão: discussão à luz do Quarto Chinês

É a seção que transforma o experimento em um trabalho publicável. Discuta:
- as duas perguntas diferentes: *"o sistema encontrou uma resposta adequada?"* (medida neste trabalho) e *"o sistema compreendeu o que o usuário quis dizer?"* (a questão filosófica);
- por que o ganho de acertos da estratégia 1 para a 5 é ganho de **aparência**: o mecanismo continua o mesmo (entrada → comparação → regra → resposta pronta). Use o quadro da seção 2.4;
- por que as **respostas inadequadas** importam mais do que a ausência de resposta: calar mostra o limite; errar com confiança **esconde** o limite (ligue ao efeito ELIZA);
- o que um observador **de fora** concluiria olhando só a coluna de adequadas — e o que ele não veria;
- a relação com os *chatbots* atuais: sistemas muito mais sofisticados levantam a mesma pergunta (CANDIOTTO, 2025). **Cuidado:** não afirme que os modelos de linguagem funcionam como o seu sistema; diga apenas que o debate sobre aparência e compreensão continua.

#### 5.5 Limitações

As da Metodologia, mais o que você percebeu no experimento (por exemplo: a bateria foi escrita por quem conhecia as regras; palavras no plural não casam com as palavras-chave; a estratégia "contém" depende da ordem das regras).

**Cuidados:**
- os números do texto devem bater **exatamente** com o `resumo.csv` da execução oficial;
- figuras e tabelas numeradas, com título acima, fonte abaixo e citadas no texto antes de aparecerem (regras do `README.md`);
- não coloque o código inteiro — só os trechos que explicam o funcionamento.

---

### 4.7 Conclusão

**Prazo: 18/11/2026**

- responda **diretamente** à pergunta do trabalho, com os números principais;
- diga se cada objetivo específico foi alcançado;
- retome a contribuição: uma bancada reprodutível que **torna observável** a distinção entre sintaxe e semântica;
- apresente as limitações com honestidade;
- **trabalhos futuros:** integrar a bancada à aplicação da Sala Chinesa do projeto; ampliar o livro de regras e a bateria (inclusive com mensagens escritas por outras pessoas, após aprovação no Comitê de Ética); testar outras medidas de similaridade; submeter a mesma bateria a um *chatbot* de IA generativa e comparar os tipos de erro; avaliar o uso da bancada como material didático sobre IA.

Não traga dados nem citações novas na Conclusão.

---

### 4.8 Resumo, Objetivos Específicos e Título

**Prazo: 25/11/2026** — escritos por último, com base no que foi **realmente feito** e depois da aprovação do texto pelo orientador.

#### Objetivos específicos (volte à seção 1.2)
3 a 5 itens, **em lista com marcadores**, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Sugestões de verbos:
- **revisar** a literatura sobre ... e o argumento do Quarto Chinês;
- **elaborar** uma bateria de ... com gabarito definido previamente;
- **implementar** cinco estratégias de ...;
- **comparar** o desempenho das estratégias quanto a ...;
- **discutir** os resultados à luz de ....

#### Resumo
- parágrafo único, de 150 a 500 palavras (NBR 6028:2021);
- sequência: contexto, problema, objetivo, método, **resultados com números** (ex.: "a estratégia X obteve N respostas adequadas e M inadequadas, contra ... da igualdade exata") e conclusão;
- palavras-chave possíveis: Quarto Chinês; *chatbots*; casamento de padrões; similaridade textual; filosofia da inteligência artificial;
- *Abstract* em inglês com o mesmo conteúdo.

#### Título
Curto, informativo e coerente com o objetivo. Evite "Um estudo sobre..." e siglas sem explicação. Alguns modelos para discutir com o orientador (não são definitivos):
- "Acertar não é entender: estratégias sintáticas de resposta e o argumento do Quarto Chinês";
- "Quanto parece entender um sistema de regras? Uma comparação de estratégias de casamento sintático à luz do Quarto Chinês".

---

## 5. Do TCC ao artigo: onde publicar

Com o orientador, o TCC pode virar um **artigo curto** ou um **resumo expandido**. O ponto forte do trabalho para publicação é a combinação de **experimento reprodutível** (bateria congelada, código aberto) com **discussão filosófica**. Opções, a confirmar com o orientador:

| Evento/periódico | Por que combina |
|---|---|
| **SECITEX** — Semana de Ciência, Tecnologia e Extensão do IFRN | Evento da própria instituição, aberto a estudantes do ensino técnico — bom primeiro passo |
| **CONNEPI** — Congresso Norte-Nordeste de Pesquisa e Inovação | Congresso da rede federal com espaço para trabalhos do técnico |
| **FEBRACE** / **MOSTRATEC** | Feiras de ciências para estudantes da educação básica e técnica; valorizam projetos com experimento e dados |
| **Revista HOLOS** (IFRN) | Periódico da instituição, para uma versão mais completa em artigo |
| **ENIAC** — Encontro Nacional de Inteligência Artificial e Computacional (SBC) | Evento de IA; exige um texto mais maduro — ver com o orientador |

Cuidados:
- **leia pelo menos três trabalhos** publicados no evento escolhido antes de adaptar o texto;
- confira a chamada de trabalhos (prazo, número de páginas, modelo e se aceita estudantes do ensino técnico);
- no artigo, o foco é o **experimento e a discussão** — a parte de instalação e telas encolhe bastante;
- defina a autoria com o orientador antes de enviar;
- **nenhum trabalho é enviado sem a revisão final do orientador.**

---

## 6. Erros comuns neste tema

- Escrever que o sistema "entendeu", "compreendeu" ou "pensou".
- Afirmar que o experimento **prova** que as máquinas não pensam (ele **ilustra** o argumento).
- Apresentar a estratégia com mais acertos como "a mais inteligente".
- Olhar só as respostas adequadas e esquecer as **inadequadas**.
- Não deixar claro que a bateria e o gabarito foram definidos **antes** dos testes.
- Explicar o Quarto Chinês a partir de vídeos ou blogs, sem ler Searle e ao menos um comentador.
- Explicar no Referencial conceitos que não aparecem nos Resultados.
- Números do texto diferentes dos da execução oficial.
- Citações sem referência, ou referências fora da NBR 6023:2018.
- Usar IA generativa para escrever o texto — em um TCC sobre programas que parecem entender sem entender, isso se refuta sozinho. Uso para tirar dúvidas deve ser declarado (ver o `README.md`).

---

## 7. Checklist antes de cada entrega

- [ ] A seção responde ao que este documento pede
- [ ] Toda afirmação tem evidência (citação, dado do experimento, print ou trecho de código)
- [ ] Números conferidos com o `resultados/resumo.csv` da execução oficial
- [ ] Nenhuma frase diz que o sistema "entende"
- [ ] Figuras e tabelas numeradas, com título acima, fonte abaixo e citadas no texto
- [ ] Citações na NBR 10520:2023 e referências na NBR 6023:2018
- [ ] Comentários da entrega anterior resolvidos
- [ ] Versão nomeada no histórico do Google Docs
- [ ] Checklist das orientações gerais (`README.md`) conferido
