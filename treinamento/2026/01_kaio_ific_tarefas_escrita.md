# Plano de escrita do artigo – Kaio (Técnico Integrado em Informática)

**Projeto pai:** iFIC – Desenvolvimento de Funcionalidades de Autenticação, Administração e Gerenciamento de Cursos de Formação Inicial e Continuada (ver `.llm/ific/projeto.md`).

**Temática:** T1 – Validador e importador de planilhas de cursos FIC (ver `.llm/ific/tematicas.md`).

**Plano de desenvolvimento correspondente:** `01_kaio_ific_tarefas_desenvolvimento.md`.

**Base normativa e de estilo:** o arquivo `README.md` deste repositório. Tudo o que está lá vale aqui. Este documento **não repete** as regras da ABNT já descritas no `README.md`; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Em nenhuma hipótese copie estas frases para o artigo. Elas indicam o assunto de cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você encontrou e leu.

---

## Cronograma de entregas

Data de referência: **22/09/2026**.

| # | Entrega | Prazo | Observação |
|---|---|---|---|
| 1 | Introdução e Objetivo Geral | **29/09/2026** | 1 semana a partir de hoje |
| 2 | Referencial Teórico | **13/10/2026** | 2 semanas após a conclusão da Introdução |
| 3 | Metodologia | **20/10/2026** | 1 semana após a conclusão do Referencial |
| 4 | Materiais e Métodos | **27/10/2026** | 1 semana após a conclusão da Metodologia |
| 5 | Resultados | **10/11/2026** | 2 semanas após a conclusão de Materiais e Métodos |
| 6 | Conclusão | **17/11/2026** | 1 semana após a conclusão dos Resultados |
| 7 | Resumo, Objetivos Específicos e Título | **24/11/2026** | 1 semana após a conclusão da Conclusão |

### Como o cronograma de escrita conversa com o de desenvolvimento

| Semana | Sprint de desenvolvimento | Entrega de escrita |
|---|---|---|
| 22/09 a 28/09 | Sprint 1 – ambiente e leitura de CSV | Introdução e Objetivo Geral (29/09) |
| 29/09 a 12/10 | Sprints 2 e 3 – módulos e primeiras regras | Referencial Teórico (13/10) |
| 13/10 a 19/10 | Sprint 4 – demais regras | Metodologia (20/10) |
| 20/10 a 26/10 | Sprint 5 – `.xlsx` e relatórios | Materiais e Métodos (27/10) |
| 27/10 a 09/11 | Sprints 6 e 7 – gabarito e medições | Resultados (10/11) |
| 10/11 a 16/11 | Sprint 8 – CLI, testes e documentação | Conclusão (17/11) |
| 17/11 a 23/11 | — | Resumo, Objetivos Específicos e Título (24/11) |

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Um texto pela metade dá para comentar; um texto que não chega, não.
- Nome do arquivo: `Artigo_Kaio_v<N>_AAAA-MM-DD.docx` (por exemplo, `Artigo_Kaio_v1_2026-09-29.docx`).
- Envie em formato editável (Word ou Google Docs com permissão de comentário), nunca em PDF.
- Resolva **todos** os comentários da versão anterior antes de enviar a próxima.
- A cada entrega, anexe também a lista de referências acumulada até ali.

---

## Formato-alvo: artigo publicável

O trabalho deve ser escrito no formato de **artigo científico**, com 8 a 12 páginas, adequado a um congresso ou a uma revista de divulgação científica de nível inicial (por exemplo, eventos de iniciação científica de institutos federais, escolas regionais de computação da Sociedade Brasileira de Computação, ou revistas institucionais). **Confirme com o orientador qual será o evento ou periódico de destino antes de começar a escrever**, porque o modelo de formatação e o limite de páginas vêm dele.

O que faz a diferença entre um relato de projeto e um artigo publicável:

1. **Um problema claro**, não apenas "eu fiz um programa".
2. **Trabalhos relacionados**, mostrando que você conhece o que já existe e sabe dizer por que a sua proposta se justifica.
3. **Método descrito com detalhe suficiente para ser repetido** por outra pessoa.
4. **Resultados medidos, com números**, não impressões. Esta é a parte mais importante e é o que diferencia o seu trabalho.
5. **Limitações declaradas com honestidade.** Reconhecer limites aumenta a credibilidade do trabalho; escondê-los é o caminho mais rápido para a recusa.

Estrutura sugerida das seções:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Qualidade de dados
2.2 Validação e importação de dados
2.3 Cursos de Formação Inicial e Continuada (FIC)
2.4 Trabalhos relacionados
3 METODOLOGIA
3.1 Classificação da pesquisa
3.2 Etapas do desenvolvimento
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
6 CONCLUSÃO
REFERÊNCIAS
```

---

# 1. Introdução
**Prazo: 29/09/2026**

Escreva 5 blocos de parágrafos, exatamente nesta ordem (é a sequência definida no `README.md`). Uma a duas páginas no total.

## 1.1 Contextualização (1 a 2 parágrafos)

**Pesquise sobre:**

- o que são os **Cursos de Formação Inicial e Continuada (FIC)**, qual é a base legal deles e qual o papel da Rede Federal de Educação Profissional, Científica e Tecnológica na oferta desses cursos. Comece pelo **Guia Pronatec de Cursos FIC** e pelo **Catálogo Nacional de Cursos Técnicos**, ambos públicos, e pela **Lei nº 11.892/2008**, que criou os Institutos Federais;
- números da oferta de cursos FIC no Brasil ou no Rio Grande do Norte: quantos cursos, quantas vagas, quantos concluintes. Procure nas plataformas oficiais (Plataforma Nilo Peçanha, INEP, portal do IFRN);
- o papel dos **sistemas de informação** na gestão educacional. Aqui cabe uma citação a Laudon e Laudon (2022), que já é usada no projeto pai.

**Escreva sobre:** o cenário em que o seu trabalho está inserido — a oferta de cursos FIC pelo IFRN como política de qualificação profissional e inclusão, e a necessidade de sistemas que deem conta de gerenciar essa oferta. Feche o bloco apresentando o iFIC como a plataforma que o IFRN está construindo para isso. Traga pelo menos **um dado numérico** neste bloco; ele dá peso imediato ao texto.

## 1.2 Problemática (1 a 2 parágrafos)

**Pesquise sobre:**

- **qualidade de dados** e o custo de dados ruins nas organizações. Procure pelos termos "qualidade de dados", "*data quality*", "*dirty data*" e "*garbage in, garbage out*". As dimensões clássicas de qualidade (completude, consistência, exatidão, validade e unicidade) vão servir tanto aqui quanto no Referencial;
- **erros típicos em planilhas**. Há uma literatura consolidada sobre a taxa de erros em planilhas construídas manualmente — procure por "*spreadsheet errors*" e pelos trabalhos de Raymond Panko, que são a referência mais citada da área. Um número desses no texto vale mais do que um parágrafo de adjetivos;
- o conceito de **ETL** (*Extract, Transform, Load*) e, dentro dele, a etapa de validação antes da carga.

**Escreva sobre:** o problema concreto. As informações de cursos FIC (nome, carga horária, turno, vagas, datas) ainda circulam em planilhas preenchidas manualmente por diferentes pessoas e diferentes campi. Isso gera campos vazios, carga horária escrita como texto, turnos escritos de formas diferentes, códigos repetidos e datas inconsistentes (fim antes do início, ou datas que não existem, como 31/02). Deixe claro **qual é a consequência**: importar essas planilhas para o iFIC sem verificação leva os erros para dentro do sistema, onde eles são muito mais caros de corrigir — e afetam o candidato, que vê uma informação errada sobre o curso. Diga também por que a conferência manual não resolve: ela é lenta, cansativa e, ela própria, sujeita a erro.

**Evite:** afirmar que "os erros são muito frequentes" sem citar fonte. Ou você cita a literatura, ou você apresenta um dado. Como este trabalho não coleta dados de planilhas reais (ver Limitações), a saída é citar a literatura.

## 1.3 Caminho para a solução (1 a 2 parágrafos)

**Pesquise sobre:**

- abordagens existentes para validação de dados tabulares: validação embutida na própria planilha (a "validação de dados" do Excel), validação no formulário de entrada, validação por script e validação no banco de dados (restrições `NOT NULL`, `CHECK`, `PRIMARY KEY`);
- bibliotecas e ferramentas de validação de dados em Python: `Pandera`, `Great Expectations`, `Cerberus`, `Pydantic`, e o próprio módulo `csv` com `openpyxl`;
- padrões abertos de descrição de dados tabulares, como o **Frictionless Data / Table Schema**.

**Escreva sobre:** as alternativas possíveis, com as vantagens e as limitações de cada uma. Mostre que existe mais de um caminho e que você conhece esses caminhos. Depois, justifique a sua escolha: uma ferramenta própria, em Python puro com bibliotecas nativas e `openpyxl`, escrita sob medida para as regras de negócio dos cursos FIC do IFRN e pensada para ser incorporada depois ao iFIC. Argumentos legítimos para essa escolha: poucas dependências externas, facilidade de manutenção por alunos do projeto, regras específicas do domínio que ferramentas genéricas não conhecem, e compatibilidade com a pilha tecnológica do iFIC.

**Cuidado:** não desqualifique as outras ferramentas sem base. A justificativa é "esta se ajusta melhor ao nosso contexto", e não "as outras são ruins".

## 1.4 Apresentação da solução (1 parágrafo)

**Escreva sobre:** o que foi desenvolvido, em termos concretos. Uma ferramenta de linha de comando em Python que lê planilhas `.csv` e `.xlsx` de cursos FIC, aplica dez regras de validação, gera um relatório de erros com a localização exata de cada problema (linha, coluna, regra violada), produz uma planilha limpa com as linhas válidas e importa esses registros para um banco SQLite.

Diga também **como a ferramenta foi avaliada**, porque é isso que o leitor de um artigo quer saber: com planilhas sintéticas de 100, 1.000 e 10.000 linhas, geradas por um script próprio que insere erros controlados e registra um gabarito; a saída do validador foi comparada ao gabarito para calcular precisão e revocação; e o tempo de processamento foi medido para cada tamanho.

Deixe explícito que **todos os dados utilizados são fictícios**, gerados por script, sem qualquer dado pessoal real — o que atende à LGPD (Lei nº 13.709/2018) e dispensa submissão ao Comitê de Ética em Pesquisa, já que não há participantes humanos.

## 1.5 Vínculo com o projeto e escopo (1 parágrafo)

**Escreva sobre:** que este trabalho está vinculado ao projeto de pesquisa iFIC, do IFRN, cuja etapa atual trata de autenticação, área administrativa e gerenciamento de cursos FIC. Explique que o validador foi desenvolvido **como protótipo independente**, para validar a abordagem antes de ser levado à plataforma, e que a **integração ao iFIC é trabalho futuro**, fora do escopo deste artigo. Ser explícito sobre o escopo protege o trabalho: o leitor não vai cobrar de você algo que você declarou que não faria.

Feche a Introdução com um parágrafo curto de organização do texto ("A Seção 2 apresenta o referencial teórico; a Seção 3 descreve a metodologia; [...]").

---

# 2. Objetivo Geral
**Prazo: 29/09/2026 (junto com a Introdução)**

Uma **única frase**, com **uma única ação principal**, coerente com o título e com a conclusão. Siga o modelo do `README.md`:

> "O objetivo principal do presente trabalho consiste no desenvolvimento de [o quê], chamado de [nome], para [finalidade]."

**Direcionamentos:**

- o verbo principal é **desenvolver** (a ação central do trabalho é construir a ferramenta);
- o objeto precisa nomear as duas funções da ferramenta: **validação** e **importação**;
- a finalidade precisa aparecer: garantir a qualidade dos dados de cursos FIC antes da carga no sistema;
- dê um nome à ferramenta. Um nome curto torna o texto inteiro mais fácil de escrever e é o que vai virar o título depois;
- **não** use verbos vagos ("conhecer", "estudar", "compreender");
- **não** empilhe ações ("desenvolver, avaliar, comparar e integrar"). As demais ações são objetivos **específicos**;
- confira a coerência: tudo o que estiver no objetivo geral precisa aparecer nos Resultados e ser retomado na Conclusão. Se você não mediu, não prometa.

**Teste rápido antes de enviar:** leia o objetivo geral e, em seguida, a primeira frase da sua Conclusão. Se as duas não estiverem falando exatamente da mesma coisa, uma das duas está errada.

---

# 3. Objetivos Específicos
**Prazo: 24/11/2026 (com o Resumo e o Título)**

Ficam para o final de propósito: os objetivos específicos precisam descrever o que foi **realmente alcançado**, e isso só se sabe com o trabalho pronto. Até lá, trabalhe com uma versão provisória.

**Direcionamentos:**

- de 4 a 5 itens, com verbo no infinitivo, letra minúscula no início, ponto e vírgula no fim de cada um e ponto no último;
- na **mesma ordem** das etapas da Metodologia e das subseções dos Resultados;
- cada um precisa ser **verificável**: na Conclusão você vai ter de mostrar que cada um foi atingido;
- não confunda objetivo com funcionalidade. "Validar a carga horária" é uma regra do sistema, não um objetivo de pesquisa.

**Esqueleto do que cada item deve cobrir** (escreva com as suas palavras, na hora de fechar o texto):

1. revisão da literatura sobre qualidade de dados, validação de dados tabulares e cursos FIC;
2. levantamento e especificação das regras de validação aplicáveis às planilhas de cursos FIC;
3. implementação da ferramenta de validação e importação;
4. construção de uma base sintética com gabarito de erros para avaliação;
5. avaliação da ferramenta quanto à detecção de erros (precisão e revocação) e ao tempo de processamento.

---

# 4. Referencial Teórico
**Prazo: 13/10/2026**

**Explicação em vídeo (assista antes de começar):** https://youtu.be/8Qztq1Q5vb0

Esta é a seção que exige mais pesquisa e onde os alunos costumam perder mais tempo. Comece a procurar referências **na primeira semana**, não no dia da entrega.

Vá do mais geral para o mais específico e escreva **apenas sobre conceitos que aparecem no resto do artigo**. Se um conceito não reaparece na Metodologia ou nos Resultados, ele não deve estar aqui.

## 4.1 Qualidade de dados

**Pesquise:** "qualidade de dados", "*data quality*", "dimensões da qualidade de dados", "*data cleaning*", "*data profiling*". Autores e obras que costumam aparecer: Wang e Strong (dimensões da qualidade de dados), Redman (custo organizacional de dados ruins) e Rahm e Do (limpeza de dados). Procure no Google Acadêmico, na SciELO, na SBC OpenLib e no Portal de Periódicos da CAPES, em português e em inglês.

**Escreva:** o que é qualidade de dados; quais são as dimensões relevantes para o seu trabalho — **completude** (R01), **validade** (R03 a R06, R08, R09), **consistência** (R07) e **unicidade** (R02); e por que os problemas de qualidade se agravam quando os dados são digitados manualmente em planilhas. Faça a ligação explícita: cada dimensão que você explicar aqui vira uma ou mais regras da sua ferramenta. Essa amarração é o que transforma o referencial em algo útil, e não em enfeite.

## 4.2 Validação e importação de dados

**Pesquise:** ETL (*Extract, Transform, Load*), validação de esquema (*schema validation*), o formato CSV (RFC 4180) e o formato XLSX (padrão Office Open XML, ISO/IEC 29500), bibliotecas de validação em Python e restrições de integridade em bancos de dados relacionais.

**Escreva:** o que é o processo de validação antes da carga e em que ponto do ETL ele acontece; a diferença entre validação **sintática** (o valor está no formato certo?) e validação **semântica** (o valor faz sentido no contexto?) — `31/02/2026` está no formato certo e mesmo assim é inválido, e esse é o seu melhor exemplo; e as camadas em que a validação pode acontecer (planilha, formulário, script, banco), justificando por que a ferramenta valida **antes** da carga, e o banco ainda protege com `PRIMARY KEY`. Explique também, brevemente, o que são CSV e XLSX e por que os dois formatos foram suportados.

## 4.3 Cursos de Formação Inicial e Continuada

**Pesquise:** Lei nº 11.892/2008 (criação dos Institutos Federais), Decreto nº 5.154/2004, Guia Pronatec de Cursos FIC, documentos da Secretaria de Educação Profissional e Tecnológica (SETEC/MEC) e a Organização Didática do IFRN. Procure também artigos sobre a oferta de cursos FIC no Brasil.

**Escreva:** o que são os cursos FIC, sua carga horária mínima, seu público e seu papel na qualificação profissional e na inclusão. Atenção: esta subseção existe para **justificar as regras de negócio** da sua ferramenta. Se a carga horária mínima de um curso FIC é definida em norma, isso explica por que a regra R03 existe e por que ela pode ser mais rígida do que "maior que zero". Escreva pensando nisso.

## 4.4 Trabalhos relacionados

**Pesquise:** outros trabalhos (TCCs, artigos, dissertações) que tenham desenvolvido validadores de planilhas, importadores em lote ou rotinas de limpeza de dados no contexto educacional ou de gestão pública. Busque em: repositórios institucionais de institutos federais e universidades, BDTD, SBC OpenLib e Google Acadêmico. Termos úteis: "validação de planilhas", "importação em lote", "qualidade de dados educacionais", "*bulk import*", "*spreadsheet validation*". Inclua também as ferramentas prontas que você levantou (Pandera, Great Expectations, Frictionless Data).

**Escreva:** de 3 a 5 trabalhos ou ferramentas, com um parágrafo cada: o que fazem, como foram validados e **quais são suas limitações diante do seu problema**. Feche com um **quadro comparativo** (é quadro, não tabela — conteúdo textual), comparando os trabalhos encontrados e a sua proposta em critérios como: formatos de entrada aceitos, regras específicas do domínio FIC, relatório com localização do erro, geração de planilha limpa, importação para banco, avaliação com gabarito de erros e licença/custo.

**Atenção:** este quadro é o argumento central da sua justificativa. Se, ao montá-lo, você concluir que uma ferramenta existente resolve tudo o que a sua resolve, converse com o orientador imediatamente — é sinal de que o recorte precisa ser ajustado, e é muito melhor descobrir isso em outubro.

## Regras que valem para o referencial inteiro

- **Toda afirmação técnica precisa de referência.** Se você escreveu uma frase de definição e não há uma citação, faltou fonte.
- **Não empilhe citações.** O capítulo não pode ser uma sequência de "Fulano (2020) diz X. Beltrano (2021) diz Y". Explique com suas palavras, relacione os autores e amarre ao seu trabalho.
- **Nada de Wikipédia, blog ou site sem autoria** como fonte principal. Documentação oficial de biblioteca é aceitável para descrever a biblioteca.
- **Nunca cite uma referência que você não leu.** Ferramentas de IA inventam referências com muita naturalidade; se você não abriu o texto, ele não entra.
- Meta razoável para este trabalho: **12 a 20 referências**, sendo a maioria artigos, livros, dissertações ou documentos oficiais.

---

# 5. Metodologia
**Prazo: 20/10/2026**

Visão geral de **como o trabalho foi conduzido**. Verbos no passado e linguagem impessoal ("foi realizada", "realizou-se"). Uma a duas páginas.

**Pasta com metodologias prontas para consulta:** https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

## 5.1 Classificação da pesquisa

**Pesquise:** Gil (2017) e Prodanov e Freitas (2013) — as referências completas estão no `README.md`. Leia os capítulos sobre classificação de pesquisa antes de escrever; não classifique "de ouvido".

**Escreva:** a classificação segundo os quatro critérios, **sempre justificando** cada escolha com uma frase que ligue o critério ao seu trabalho (o erro mais comum é apenas listar os rótulos). Para este trabalho, o enquadramento mais provável é:

- **Natureza:** aplicada — gera conhecimento para resolver um problema prático do iFIC;
- **Objetivos:** exploratória e descritiva — explora uma solução ainda não existente no contexto e descreve seu comportamento medido;
- **Abordagem:** quantitativa — os resultados são números (erros detectados, precisão, revocação, tempo de execução);
- **Procedimentos:** pesquisa bibliográfica (levantamento dos conceitos e trabalhos relacionados) combinada com pesquisa **experimental** (avaliação da ferramenta sobre bases sintéticas controladas).

Discuta o enquadramento com o orientador antes de fechar; classificação de pesquisa é um dos pontos mais cobrados na banca.

## 5.2 Pesquisa bibliográfica

**Escreva:** quais bases foram consultadas (Google Acadêmico, SciELO, SBC OpenLib, CAPES, BDTD), quais palavras-chave foram usadas (liste-as, em português e em inglês), qual o recorte temporal e quais os critérios de inclusão e exclusão dos trabalhos. Escreva isso **enquanto** pesquisa, não depois — reconstruir de memória é trabalhoso e costuma sair impreciso.

## 5.3 Etapas do desenvolvimento

**Escreva:** as etapas em ordem cronológica, do início ao fim. Uma **figura com o fluxo das etapas** ajuda muito o leitor e é fácil de fazer (use o draw.io, gratuito). Lembre-se: identificação em cima, centralizada, fonte embaixo.

As etapas a descrever, com base no plano de desenvolvimento:

1. levantamento das regras de validação, a partir das normas dos cursos FIC e da estrutura de dados do iFIC;
2. definição do formato da planilha de entrada (as nove colunas);
3. implementação incremental do validador, em sprints de uma semana, com versionamento em Git, em subpasta própria dentro do repositório compartilhado do projeto;
4. implementação da leitura de `.csv` e `.xlsx` e da geração do relatório de erros e da planilha limpa;
5. construção do gerador de massa sintética com gabarito de erros;
6. execução dos experimentos de detecção (comparação com o gabarito) e de desempenho (tempo de processamento);
7. implementação da importação para o banco SQLite;
8. implementação dos testes automatizados e documentação.

**Descreva também o método de trabalho:** desenvolvimento incremental em sprints de uma semana, com reunião de acompanhamento e revisão de código pelo orientador ao final de cada sprint. Isso é método, e um artigo ganha ao explicitá-lo.

**Não confunda com Materiais e Métodos.** Aqui vai a visão geral: o *quê* e em que ordem. Na próxima seção vão as ferramentas, versões e procedimentos detalhados: o *com o quê* e o *como*.

---

# 6. Materiais e Métodos
**Prazo: 27/10/2026**

Vale a analogia do `README.md`: é a **lista de ingredientes** mais o **modo de preparo**. Escreva com detalhe suficiente para que outra pessoa reproduza o trabalho sem falar com você.

## 6.1 Materiais

Para **cada** item, escreva três coisas: **o que é** (uma ou duas frases, com referência — a documentação oficial serve), **para que foi usado neste trabalho** e **por que foi escolhido**. Escrever só "foi utilizado Python" não vale nada.

Itens a descrever:

| Ferramenta | O que dizer além da versão |
|---|---|
| Python 3.12 | Por que Python, e a relação com a pilha do iFIC (Django) |
| Módulo `csv` | Biblioteca padrão; leitura do formato CSV sem dependência externa |
| `openpyxl` | Leitura de arquivos `.xlsx`; por que foi necessária uma biblioteca externa |
| Módulo `datetime` | Conversão e comparação de datas; validação de datas inexistentes |
| Módulo `sqlite3` e SQLite | Banco embutido, sem servidor; por que SQLite e não MySQL neste protótipo |
| `random` | Geração da massa sintética; uso de semente fixa para reprodutibilidade |
| `pytest` | Testes automatizados das funções de validação |
| `argparse` | Interface de linha de comando |
| Git e GitHub | Versionamento do código, em subpasta própria dentro do repositório compartilhado do projeto |
| VS Code | Ambiente de desenvolvimento |

Informe também o **ambiente de execução** dos experimentos (processador, memória, sistema operacional, versão do Python). Sem isso, os tempos que você vai apresentar não significam nada. Um quadro-resumo com ferramenta, versão e finalidade organiza bem esta seção.

## 6.2 Métodos

Descreva os procedimentos em detalhe suficiente para reprodução:

**a) Especificação das regras.** Apresente o quadro das dez regras (R01 a R10), com código, descrição e a dimensão de qualidade de dados correspondente (o vínculo com a Seção 4.1). Diga de onde veio cada regra: norma dos cursos FIC, estrutura de dados do iFIC ou requisito levantado com a coordenação.

**b) Arquitetura da ferramenta.** Explique a separação em módulos (`config`, `leitor`, `validadores`, `relatorio`, `banco`, `main`) e por quê. Uma figura simples com o fluxo — planilha → leitor → validador → relatório de erros + planilha limpa → banco — comunica isso melhor do que qualquer parágrafo.

**c) Construção da base sintética.** Este é o ponto mais importante da seção, porque é o que sustenta os seus resultados. Descreva: o número de linhas de cada base (100, 1.000 e 10.000); a proporção de linhas com erro (cerca de 20%); como os erros foram distribuídos entre as dez regras; como o gabarito foi registrado; e o uso de **semente fixa** (`random.seed`) para tornar a geração reprodutível. Deixe claro que **nenhum dado real de pessoas foi utilizado**, em conformidade com a LGPD, e mencione a origem dos nomes de cursos (Guia Pronatec, documento público).

**d) Procedimento de avaliação da detecção.** Defina formalmente **verdadeiro positivo**, **falso positivo** e **falso negativo** no contexto do seu trabalho, e apresente as fórmulas de **precisão** e **revocação**. Explique o critério de correspondência entre um erro do relatório e um erro do gabarito — o par (linha, regra) ou a trinca (linha, coluna, regra)? Essa definição muda os números, e por isso precisa estar escrita.

**e) Procedimento de medição de desempenho.** Ferramenta de medição (`time.perf_counter`), o que exatamente foi cronometrado (leitura? validação? leitura mais validação mais escrita?), número de repetições (5), estatísticas apresentadas (média e desvio padrão) e cuidados tomados (fechamento de outros programas, execução consecutiva).

**f) Testes automatizados.** Quantos testes, o que cada grupo cobre e o critério de escolha dos casos (válido, inválido e caso-limite para cada regra).

---

# 7. Resultados e Discussão
**Prazo: 10/11/2026**

A seção mais importante do artigo. Duas a quatro páginas. Organize-a **na mesma ordem dos objetivos específicos**.

> **Regra que não tem exceção:** toda figura, quadro, tabela ou código é **anunciado no texto antes** de aparecer e **explicado depois**. Nada de duas imagens seguidas sem texto entre elas.

## 7.1 Regras de validação especificadas

Apresente o quadro final das dez regras implementadas e comente as decisões de projeto que exigiram escolha, por exemplo: aceitar ou não turno escrito com maiúsculas e espaços extras; o que fazer quando um campo vazio viola R01 e R03 ao mesmo tempo; e o tratamento das datas que o `openpyxl` devolve como `datetime`. Esses são achados reais do desenvolvimento, e são exatamente o tipo de detalhe que dá substância a um artigo técnico. Não os esconda.

## 7.2 A ferramenta desenvolvida

Apresente o que foi construído:

- a figura da arquitetura em módulos;
- o comando de execução e uma captura de tela do terminal com o resumo da validação;
- um trecho do relatório de erros, mostrando o formato com linha, coluna, regra, mensagem e valor;
- uma captura da tabela do SQLite já populada;
- **no máximo dois** trechos de código, curtos e realmente relevantes (por exemplo, a função de conversão de data que rejeita `31/02/2026`, e o `upsert` que evita duplicação na reimportação). Cada trecho vem acompanhado de uma explicação. Código extenso vai para o repositório, com o link citado no texto.

Informe o endereço do repositório e o **caminho da subpasta** em que o código está (por exemplo, `<endereço-do-repositório>/tree/main/kaio`). Código disponível é um ponto forte do trabalho — mas confirme antes com o orientador se o repositório pode ser citado publicamente no artigo, já que ele é compartilhado com outros alunos do projeto.

## 7.3 Avaliação da detecção de erros

Apresente uma **tabela** com uma linha por base (100, 1.000 e 10.000 linhas) e colunas: erros no gabarito, verdadeiros positivos, falsos negativos, falsos positivos, precisão e revocação. Use vírgula como separador decimal e o mesmo número de casas decimais em toda a coluna.

Apresente também a distribuição dos erros **por regra**, para mostrar que todas as dez regras foram exercitadas e nenhuma ficou sem teste.

**Discuta os números, não apenas os apresente:**

- se houve falsos negativos, quais regras falharam e por quê;
- se houve falsos positivos, qual foi a causa (lembre-se do caso do campo vazio que dispara duas regras, e da decisão que você tomou na Sprint 3);
- se a precisão e a revocação deram 100%, **não comemore sem ressalvas**: explique que esse resultado é esperado, porque os erros foram inseridos pelo mesmo script e pelo mesmo autor que escreveu as regras. Isso é uma **limitação metodológica** e precisa estar escrita no texto. Um avaliador de congresso vai notar isso de qualquer forma; é muito melhor que você o diga primeiro.

## 7.4 Desempenho

Apresente uma **tabela** com o tamanho da base, o tempo médio, o desvio padrão e o tempo médio por linha. Um **gráfico** de tempo em função do número de linhas ajuda a visualizar o comportamento.

**Discuta:** o crescimento do tempo é proporcional ao número de linhas? Se sim, comente que o custo é aproximadamente linear e diga o que isso significa na prática. Compare também o tempo de leitura de `.csv` com o de `.xlsx`, se você tiver medido os dois — costuma haver diferença expressiva, e explicá-la (o `.xlsx` é um formato compactado e estruturado em XML) é uma boa discussão técnica.

Traduza os números para o problema real: quanto tempo uma pessoa levaria para conferir 10.000 linhas manualmente, e quanto tempo a ferramenta leva? Esse contraste é o argumento mais forte do seu trabalho — mas apresente a estimativa manual como estimativa, deixando claro o critério que você usou (por exemplo, alguns segundos por linha), já que você não mediu a conferência manual.

## 7.5 Testes automatizados

Informe o número de testes, quantos passaram e o que foi coberto. Se você tiver medido cobertura de código com `pytest-cov`, apresente o percentual — é um indicador objetivo e bem-visto.

## 7.6 Limitações

Uma subseção curta e honesta, com os limites do trabalho:

- a avaliação usou **dados sintéticos**, gerados pelo próprio autor. Erros reais de digitação podem ter padrões diferentes dos simulados;
- as regras foram derivadas do formato de planilha definido para este trabalho; planilhas com outra estrutura exigiriam ajustes;
- não houve avaliação com usuários (servidores que preenchem as planilhas), o que exigiria aprovação do Comitê de Ética em Pesquisa e não cabia no prazo;
- a ferramenta ainda não está integrada ao iFIC.

Declarar limitações **fortalece** o artigo. Esconder limitações é o erro mais comum em trabalhos de iniciação — e o mais fácil de perceber na avaliação.

---

# 8. Conclusão
**Prazo: 17/11/2026**

Duas ou três páginas no máximo — geralmente menos de uma, em artigo. Nada de resultado novo, conceito novo ou citação nova aqui.

**Escreva, nesta ordem:**

1. **Retomada do problema e do objetivo geral.** Uma ou duas frases lembrando o problema (dados de cursos FIC em planilhas manuais, sujeitos a erro) e afirmando que o objetivo geral foi alcançado, **com o motivo**: "[...] foi alcançado, uma vez que a ferramenta desenvolvida detectou X% dos erros presentes na base de avaliação e processou 10.000 linhas em Y segundos."

2. **Um comentário por objetivo específico**, na mesma ordem em que foram apresentados, cada um apontando o resultado que o comprova. Aqui é onde se paga a dívida de ter escrito objetivos verificáveis.

3. **Contribuições.** O que fica para quem vier depois: uma ferramenta funcional, com o código disponível no repositório do projeto; um conjunto documentado de regras de validação para o domínio dos cursos FIC; e um método de avaliação com base sintética e gabarito, que pode ser reaproveitado por outros trabalhos do projeto iFIC.

4. **Limitações e dificuldades.** Retome brevemente as limitações da Seção 7.6 e acrescente as dificuldades do processo de desenvolvimento — codificação de caracteres, datas devolvidas pelo Excel como `datetime`, construção do gabarito. É aqui que o `docs/diario.md` da Sprint 1 vale o investimento. Dificuldades técnicas relatadas com clareza são conteúdo legítimo de artigo, não confissão de fraqueza.

5. **Trabalhos futuros.** Sugestões concretas, ligadas ao que você mesmo encontrou:
   - integrar o validador ao painel administrativo do iFIC, como funcionalidade de importação em lote (esta é a principal);
   - permitir a configuração das regras em arquivo externo, sem alterar o código;
   - avaliar a ferramenta com planilhas reais da coordenação de cursos FIC, devidamente anonimizadas;
   - sugerir correções automáticas para erros comuns de digitação;
   - avaliar a usabilidade do relatório de erros com os servidores que preenchem as planilhas (o que exigiria aprovação do CEP).

**Não escreva:** que "o sistema resolve completamente o problema" nem que "a ferramenta elimina os erros". Ela detecta erros das categorias previstas, em uma base sintética. Diga exatamente isso.

---

# 9. Resumo, Título e revisão final
**Prazo: 24/11/2026**

## 9.1 Resumo

Escrito **por último**, depois de todo o texto aprovado pelo orientador. Parágrafo único, 150 a 500 palavras, linguagem impessoal, sem citações, sem siglas pouco conhecidas e sem menção a figuras ou tabelas (NBR 6028:2021).

Estrutura — uma ou duas frases para cada item:

1. **contexto e problema:** planilhas manuais de cursos FIC e o risco de importar dados inconsistentes;
2. **objetivo:** o que o trabalho se propôs a desenvolver;
3. **método:** validação por regras em Python, avaliação com bases sintéticas de 100, 1.000 e 10.000 linhas com gabarito de erros;
4. **resultados:** os números principais — precisão, revocação e tempo de processamento;
5. **conclusão:** o que os resultados permitem afirmar e o encaminhamento (integração ao iFIC como trabalho futuro).

O **Abstract** é a versão em inglês. Não entregue tradução automática sem revisão.

**Palavras-chave** (3 a 5), separadas por ponto e vírgula. Sugestões de campo semântico: qualidade de dados; validação de dados; cursos FIC; Python; sistemas de informação. Escolha termos que alguém usaria para **encontrar** o seu trabalho.

## 9.2 Título

**Última coisa a ser definida**, em acordo com o orientador. Deve indicar **o que foi feito** e **para quem/para qual contexto**, e ser coerente com o objetivo geral. Se houver subtítulo, separe-o com dois-pontos.

Pontos a cobrir na formulação: a ação (validação e importação), o objeto (planilhas de cursos FIC) e o contexto (IFRN / plataforma iFIC). Se a ferramenta tiver um nome, ele pode abrir o título, no formato "Nome: descrição do que faz". Evite títulos genéricos ("Um sistema em Python") e siglas desconhecidas.

## 9.3 Revisão final — checklist

Antes de enviar a versão final, percorra o checklist do `README.md` e mais estes pontos específicos deste trabalho:

- [ ] O objetivo geral, os objetivos específicos, os títulos das subseções de Resultados e os parágrafos da Conclusão estão na mesma ordem e falando das mesmas coisas?
- [ ] Todos os números citados no Resumo, nos Resultados e na Conclusão são **exatamente** os mesmos? (É o erro mais comum: mudar um experimento e esquecer de atualizar o resumo.)
- [ ] Toda tabela e figura é citada no texto antes de aparecer e explicada depois?
- [ ] Todas as tabelas e figuras têm identificação em cima, centralizada, e fonte embaixo?
- [ ] As referências estão todas citadas no texto, e todas as citações estão na lista?
- [ ] Nenhuma referência foi incluída sem ter sido lida?
- [ ] As siglas (FIC, IFRN, LGPD, CSV, ETL, CEP) foram escritas por extenso na primeira ocorrência?
- [ ] A numeração das seções está sem ponto após o número ("2.1 Qualidade de dados")?
- [ ] O texto está impessoal e no passado?
- [ ] Está declarado que os dados são sintéticos e que não houve participantes humanos?
- [ ] O link do repositório e o caminho da subpasta estão no texto, e o orientador autorizou a divulgação desse endereço?
- [ ] Todos os comentários da versão anterior foram resolvidos?

---

## Referências mínimas a garantir

Ao longo da escrita, garanta que o trabalho tenha pelo menos:

- **2 obras de metodologia científica** — Gil (2017) e Prodanov e Freitas (2013) já estão no `README.md`;
- **3 a 4 obras sobre qualidade de dados** (Seção 4.1);
- **2 a 3 obras sobre validação, ETL ou formatos de dados** (Seção 4.2);
- **2 a 3 documentos oficiais sobre cursos FIC e a Rede Federal** (Seção 4.3);
- **3 a 5 trabalhos relacionados** (Seção 4.4);
- **a legislação citada** — Lei nº 13.709/2018 (LGPD) e Lei nº 11.892/2008;
- **a documentação oficial das ferramentas** — Python, openpyxl, SQLite, pytest.

Anote a referência completa de **tudo** o que ler, desde o primeiro dia. Zotero e Mendeley ajudam, mas confira cada referência contra a NBR 6023:2018 antes de entregar: esses gerenciadores erram com frequência.
