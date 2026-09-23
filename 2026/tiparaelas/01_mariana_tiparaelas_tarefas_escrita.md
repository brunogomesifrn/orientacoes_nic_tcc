# TiParaElas — Orientações de Escrita do TCC (Ciclo 1)

**Estudante:** Mariana — Curso Superior de Tecnologia em Sistemas para Internet
**Orientação:** Prof. Bruno Gomes — NIC
**Data de início:** 22/09/2026
**Documento do TCC:** será compartilhado pelo coordenador via **Google Drive**. Escreva diretamente nele, sem criar cópias paralelas.

> **Importante:** este documento diz **o que pesquisar e sobre o que escrever** em cada seção. Ele **não contém o texto final** — o texto é seu. As orientações gerais de escrita, as normas da ABNT e as regras de citação, figuras, tabelas e referências estão no `README.md` deste repositório; **leia-o antes de começar**. O que você vai fazer em cada semana está em `01_mariana_tiparaelas_tarefas_desenvolvimento.md`.

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
- [6. Erros comuns em trabalhos de acessibilidade](#6-erros-comuns-em-trabalhos-de-acessibilidade)
- [7. Checklist antes de cada entrega](#7-checklist-antes-de-cada-entrega)

---

## 1. Antes de começar

**O que o seu TCC afirma:** *"Avaliamos a acessibilidade de oito páginas da plataforma TiParaElas segundo 12 critérios da WCAG 2.2, usando duas ferramentas automáticas (Lighthouse e ASES) e verificação manual (teclado, zoom, contraste e leitor de tela); identificamos e classificamos as barreiras; comparamos o que cada forma de avaliação encontrou; e propusemos um plano de correção priorizado."*

**O que o seu TCC NÃO afirma:**
- **não** diz que o site foi corrigido — neste ciclo **não houve alteração no código**; as correções ficam para outra pessoa, seguindo o seu plano;
- **não** diz que a plataforma "é acessível" ou "não é acessível" como um todo — você fala só das **8 páginas** e dos **12 critérios** avaliados;
- **não** traz opiniões de usuárias com deficiência — **não houve teste com pessoas** (isso depende do Comitê de Ética e fica como trabalho futuro).

**Dois cuidados de linguagem:**
- use **"pessoa com deficiência"**, termo da Lei Brasileira de Inclusão. Evite "portador de deficiência", "pessoa especial" e "deficiente";
- toda afirmação sobre acessibilidade precisa de **evidência**: um critério, um print, um dado da planilha ou uma referência.

**Como trabalhar no Google Drive:**
- escreva direto no documento compartilhado; **não crie cópias**;
- ao terminar uma seção, use **Arquivo > Histórico de versões > Nomear versão atual** (ex.: `v1 - Introdução - 29/09`);
- **resolva os comentários** do orientador antes de entregar a seção seguinte;
- ao entregar, avise o orientador dizendo **qual seção** está pronta.

**Regra de ouro:** escreva a partir do **diário de bordo** e da **planilha de barreiras**. O texto cresce junto com a avaliação, e não no final.

---

## 2. Cronograma de entregas

Hoje é **22/09/2026**. Cada prazo conta a partir da conclusão da etapa anterior.

| # | Seção | Prazo | Duração | Sprints que alimentam a seção |
|---|---|---|---|---|
| 1 | Introdução e Objetivo Geral | **29/09/2026** (terça) | 1 semana a partir de hoje | Sprint 1 |
| 2 | Referencial Teórico | **13/10/2026** (terça) | 2 semanas após a Introdução | Sprints 1 e 2 |
| 3 | Metodologia | **20/10/2026** (terça) | 1 semana após o Referencial | Sprints 2 e 3 |
| 4 | Materiais e Métodos | **27/10/2026** (terça) | 1 semana após a Metodologia | Sprints 3, 4 e 5 |
| 5 | Resultados | **10/11/2026** (terça) | 2 semanas após Materiais e Métodos | Sprints 3 a 7 |
| 6 | Conclusão | **17/11/2026** (terça) | 1 semana após os Resultados | Sprint 8 |
| 7 | Resumo, Objetivos Específicos e Título | **24/11/2026** (terça) | 1 semana após a Conclusão | Encerramento |

Os números da avaliação ficam prontos na Sprint 6 (até 30/10), e o plano de correção na Sprint 7 (até 09/11). Por isso, escreva os Resultados assim: de 28/10 a 04/11, a situação encontrada e a comparação entre métodos; de 05 a 10/11, o plano de correção.

**Dica de ritmo:** escreva um pouco ao longo da semana (de preferência às quintas e sextas), e não na véspera.

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
  2.1 Pessoas com deficiência e acessibilidade digital
  2.2 Tecnologias assistivas
  2.3 WCAG 2.2, eMAG e legislação brasileira
  2.4 Formas de avaliar a acessibilidade
  2.5 Trabalhos relacionados
3 METODOLOGIA
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
  5.1 Páginas avaliadas
  5.2 Barreiras encontradas
  5.3 Ferramentas automáticas × verificação manual
  5.4 Plano de correção
  5.5 Discussão e limitações
6 CONCLUSÃO
REFERÊNCIAS
APÊNDICES (checklist dos 12 critérios, planilha de barreiras resumida, plano de correção completo)
```

---

## 4. Orientações por seção

---

### 4.1 Introdução

**Prazo: 29/09/2026** | Tamanho sugerido: 5 a 6 parágrafos

Siga a sequência de parágrafos do `README.md`.

#### Parágrafo 1 — Contextualização

**Pesquise sobre:**
- quantas pessoas com deficiência existem no Brasil (IBGE, PNAD Contínua 2022 ou Censo 2022 — **confira o número na fonte original**);
- a internet como meio de acesso a informação, estudo e trabalho;
- a baixa participação de mulheres na computação (Censo da Educação Superior do INEP; Programa Meninas Digitais, da SBC).

**Escreva sobre:** a importância de uma web acessível e a desigualdade de gênero na computação, e **ligue os dois temas**: uma plataforma criada para incluir mulheres na tecnologia precisa ser acessível, senão exclui justamente as mulheres com deficiência.

> **Cuidado:** não comece com "Desde os primórdios...". Comece com o dado que interessa.

#### Parágrafo 2 — Problemática

**Pesquise sobre:** o relatório mais recente do *WebAIM Million* (levantamento anual de acessibilidade de 1 milhão de sites) e pesquisas do Movimento Web para Todos sobre sites brasileiros. Anote as falhas mais comuns (baixo contraste, imagens sem descrição, campos sem nome, links vazios).

**Escreva sobre:** a maioria dos sites ainda tem barreiras; muitas equipes confiam apenas em ferramentas automáticas, que não encontram todos os problemas; projetos pequenos, feitos por bolsistas, raramente passam por uma avaliação de acessibilidade. Use dados e citações.

#### Parágrafo 3 — Caminho para a solução

**Pesquise sobre:** o que é a WCAG 2.2 e o eMAG; as formas de avaliar a acessibilidade (ferramentas automáticas e verificação manual); 2 ou 3 trabalhos brasileiros que avaliaram a acessibilidade de sites (procure na SBC OpenLib: https://sol.sbc.org.br).

**Escreva sobre:** que existem diretrizes e formas de avaliação reconhecidas, que a literatura recomenda **combinar** ferramentas automáticas com verificação manual e que um diagnóstico é o primeiro passo para corrigir um site.

#### Parágrafo 4 — Apresentação da solução

**Escreva sobre** o que foi feito, sem exagerar:
- a avaliação de **8 páginas** do TiParaElas segundo **12 critérios** da WCAG 2.2;
- com **Lighthouse e ASES** (automáticas) e **teclado, zoom, contraste e o leitor de tela Narrador** (manuais);
- a comparação entre o que as ferramentas encontraram e o que só a verificação manual encontrou;
- a elaboração de um **plano de correção** priorizado, para ser executado em uma etapa seguinte.

Diga claramente que **o código não foi alterado neste trabalho** e que não houve teste com usuárias.

#### Parágrafo 5 — Vínculo com o projeto

**Escreva sobre:** o NIC e o projeto TiParaElas (consulte `.llm/tiparaelas/projeto.md`): plataforma que divulga ações, oportunidades e mulheres que inspiram na tecnologia, ligada aos Objetivos de Desenvolvimento Sustentável 4, 5 e 10 da ONU. Conte a sua participação anterior no projeto (por exemplo, o gerenciamento de tipos de evento) e diga que o foco deste TCC é a acessibilidade.

#### Último parágrafo — Objetivos e organização

Apresente a pergunta de pesquisa (seção 2 do documento de desenvolvimento), o objetivo geral e os específicos, e um parágrafo curto dizendo o que cada capítulo traz.

---

### 4.2 Objetivo Geral

**Prazo: 29/09/2026** (junto com a Introdução) | Tamanho: **uma frase**

Uma frase, com **um verbo principal**, coerente com o que você vai fazer. Siga o modelo do `README.md`.

Estrutura para você completar (não copie; ajuste com o orientador):

> "O objetivo principal do presente trabalho consiste em avaliar a acessibilidade de [...] da plataforma web TiParaElas segundo [...], de modo a identificar [...] e propor [...]."

**Confira:**
1. O verbo é concreto? ("avaliar", "diagnosticar" — e não "estudar" ou "abordar").
2. Ele promete só o que será feito? Se disser "corrigir" ou "tornar acessível", está errado para este ciclo.
3. Na Conclusão, você conseguirá escrever "o objetivo foi alcançado porque..."?

> Os **objetivos específicos** são escritos por último (24/11). Deixe um rascunho na seção 1.2 e reescreva no final.

---

### 4.3 Referencial Teórico

**Prazo: 13/10/2026** (2 semanas) | Assista antes ao vídeo do `README.md`: https://youtu.be/8Qztq1Q5vb0

Explique **só os conceitos que você vai usar nos Resultados**. Como usar as ferramentas vai em Materiais e Métodos, não aqui.

#### 2.1 Pessoas com deficiência e acessibilidade digital

**Pesquise sobre:** o conceito de pessoa com deficiência e de barreira na Lei Brasileira de Inclusão (Lei nº 13.146/2015, arts. 2º e 3º); o que é acessibilidade na web (W3C/WAI); a relação entre equidade de gênero e acessibilidade (a ideia de que as exclusões se somam — pesquise **interseccionalidade**).

**Escreva sobre:** o que é acessibilidade digital e por que ela é um direito. Seja breve.

#### 2.2 Tecnologias assistivas

**Pesquise sobre:** o que são tecnologias assistivas; como funcionam os leitores de tela (NVDA, Narrador, VoiceOver, TalkBack); a navegação só com teclado; ampliadores de tela; o VLibras.

**Escreva sobre:** como uma pessoa cega ou com baixa visão usa um site (ouve os títulos, pula entre links e campos, usa o teclado). Isso ajuda o leitor a entender, nos Resultados, por que um foco invisível ou uma imagem sem descrição é um problema real.

#### 2.3 WCAG 2.2, eMAG e legislação brasileira

**Pesquise sobre:** a WCAG 2.2 — 4 princípios (perceptível, operável, compreensível, robusto), diretrizes, critérios de sucesso e níveis A, AA e AAA; o eMAG 3.1 (modelo do governo federal); a Lei Brasileira de Inclusão (art. 63, sobre sites) e a norma ABNT NBR 17225 (confira a edição vigente).

**Escreva sobre:** como a WCAG está organizada e o que diz a lei brasileira. Monte um **quadro com os 12 critérios avaliados** (número, nome, nível e o que exige, em uma linha) — você vai usá-lo nos Resultados.

#### 2.4 Formas de avaliar a acessibilidade

**Pesquise sobre:** ferramentas automáticas (o que conseguem e o que **não** conseguem verificar — Vigo, Brown e Conway, 2013); verificação manual e testes com tecnologias assistivas; a metodologia de avaliação do W3C, chamada WCAG-EM (leia a página de visão geral, com o tradutor do navegador se preferir).

**Escreva sobre:** as vantagens e limitações de cada forma de avaliação e por que se recomenda combiná-las. Essa seção sustenta a sua QP2.

#### 2.5 Trabalhos relacionados

**Pesquise** na SBC OpenLib (https://sol.sbc.org.br) e no Google Acadêmico:
- `"avaliação de acessibilidade" eMAG`;
- `"acessibilidade web" ASES`;
- `"acessibilidade" "leitor de tela" avaliação site`;
- `"web accessibility evaluation" "automated tools"`.

**Escreva sobre:** 4 a 6 trabalhos que avaliaram a acessibilidade de sites, principalmente brasileiros (portais de governo, de universidades, de institutos federais). Para cada um: que site avaliou, que ferramentas usou, se fez verificação manual e o que encontrou. Termine com um **quadro comparativo** (colunas: site avaliado, diretriz, ferramentas, verificação manual, leitor de tela, plano de correção). A última linha é o **seu trabalho**.

**Leituras de partida** (localize a fonte original antes de colocar nas Referências):
- W3C. *Web Content Accessibility Guidelines (WCAG) 2.2* e *Understanding WCAG 2.2*;
- W3C. *Introdução à Acessibilidade Web* (em português) e *WCAG Overview*;
- W3C. *Website Accessibility Conformance Evaluation Methodology (WCAG-EM) 1.0*;
- BRASIL. *eMAG — Modelo de Acessibilidade em Governo Eletrônico*, versão 3.1;
- BRASIL. Lei nº 13.146, de 6 de julho de 2015 (Lei Brasileira de Inclusão);
- VIGO, M.; BROWN, J.; CONWAY, V. *Benchmarking web accessibility evaluation tools: measuring the harm of sole reliance on automated tests*, 2013;
- WebAIM. *The WebAIM Million* (relatório mais recente).

---

### 4.4 Metodologia

**Prazo: 20/10/2026** | Veja exemplos de metodologia na pasta do orientador: https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

Aqui você descreve **o caminho** da pesquisa. As ferramentas e versões ficam para Materiais e Métodos.

- **Classificação da pesquisa:** aplicada; exploratória e descritiva; quali-quantitativa (conta as barreiras e também as descreve); procedimentos: pesquisa bibliográfica e **estudo de caso** (a plataforma TiParaElas). Confirme a classificação com o orientador.
- **Pesquisa bibliográfica:** onde pesquisou, com quais palavras e como escolheu os trabalhos.
- **Etapas** (faça **uma figura do fluxo** no draw.io — `https://app.diagrams.net`):
  1. estudo da WCAG 2.2 e da literatura;
  2. escolha das 8 páginas e dos 12 critérios (com a justificativa — Tarefas 2.1 e 2.2);
  3. avaliação automática (Lighthouse e ASES);
  4. verificação manual (teclado, zoom, contraste e leitor de tela);
  5. registro e classificação das barreiras (planilha, escala de gravidade);
  6. comparação entre as formas de avaliação;
  7. elaboração do plano de correção.
- **Escala de gravidade:** apresente a escala (crítica, alta, média, baixa) e diga que ela foi definida **antes** da avaliação.
- **Aspectos éticos:** não houve participação de pessoas; só foram usados dados fictícios.
- **Limitações do método:** uma só avaliadora; 8 páginas e 12 critérios; uso do Narrador (e não do NVDA); o ASES avaliado pelo código-fonte, sem as folhas de estilo; site rodando no computador local, com dados fictícios.

---

### 4.5 Materiais e Métodos

**Prazo: 27/10/2026** | Lembre-se da analogia da **receita de bolo** do `README.md`: outra pessoa deve conseguir repetir a sua avaliação.

**Materiais** — quadro com o que foi usado (as versões estão no seu diário):

| Ferramenta | Versão | Para que foi usada |
|---|---|---|
| TiParaElas (Python/Django) | commit anotado na Tarefa 1.1 | Sistema avaliado |
| Google Chrome | anotar | Navegador da avaliação |
| Lighthouse | versão do Chrome | Avaliação automática |
| ASES Web | – | Avaliação automática segundo o eMAG |
| WebAIM Contrast Checker | – | Medição de contraste |
| Narrador do Windows | versão do Windows | Leitor de tela |
| Google Planilhas | – | Registro das barreiras e gráficos |

**Métodos** — para cada item, explique **o que é, como foi usado e por que foi escolhido**:
- **dados fictícios:** o que foi cadastrado e por quê;
- **Lighthouse:** as opções escolhidas (só *Accessibility*, modo *Desktop*);
- **ASES:** a avaliação por código-fonte e a limitação disso;
- **teclado:** as teclas usadas e as 7 perguntas da Tarefa 4.1;
- **zoom e contraste:** o procedimento e os valores mínimos exigidos;
- **leitor de tela:** os comandos usados e as perguntas das Tarefas 5.2 e 5.3;
- **planilha:** as colunas e a regra de uma linha por barreira;
- **plano de correção:** como foram definidas a prioridade e o esforço.

---

### 4.6 Resultados

**Prazo: 10/11/2026** (2 semanas) | Organize pelas **questões de pesquisa**.

#### 5.1 Páginas avaliadas
Quadro das 8 páginas, com o endereço e o tipo de conteúdo de cada uma.

#### 5.2 Barreiras encontradas (QP1)
- tabela com a nota do Lighthouse e o percentual do ASES de cada página;
- total de barreiras e gráficos por página, por gravidade e por critério;
- o **quadro critério × página** (✓, ✗, —);
- a tabela de contraste;
- 2 ou 3 **exemplos** detalhados, com print e, quando houver, a fala do Narrador entre aspas.

#### 5.3 Ferramentas automáticas × verificação manual (QP2)
- o gráfico **"quem encontrou cada barreira"** (só ferramentas, só manual, ambos) — é o resultado mais importante do trabalho;
- exemplos de barreiras que **só** a verificação manual encontrou;
- comente se alguma página teve nota alta no Lighthouse e, mesmo assim, barreiras graves;
- compare com o que diz a literatura (Vigo, Brown e Conway, 2013).

#### 5.4 Plano de correção (QP3)
- tabela resumida do plano (prioridade, barreira, critério, arquivo, esforço);
- explique a lógica da prioridade: por que corrigir primeiro o que está no layout comum a todas as páginas;
- quantas correções são de esforço pequeno, médio e grande;
- o plano completo vai para o apêndice.

#### 5.5 Discussão e limitações
Discuta: o que os resultados mostram sobre a acessibilidade da plataforma; o que as barreiras da página de detalhe de inspiração significam para a proposta do projeto (se uma mulher com deficiência não consegue conhecer as histórias das "mulheres que inspiram", a plataforma falha justamente no seu objetivo); se as barreiras de Login e Cadastro impedem alguém de **participar** da plataforma; o papel de quem cadastra o conteúdo (descrição das imagens); por que confiar só em ferramentas automáticas é arriscado; a relação com a inclusão de mulheres com deficiência; e as limitações do trabalho.

**Cuidados:**
- fale **das 8 páginas e dos 12 critérios**, e não do site inteiro;
- figuras e tabelas numeradas, com título acima, fonte abaixo e citadas no texto antes de aparecerem (regras do `README.md`);
- prints só com dados fictícios.

---

### 4.7 Conclusão

**Prazo: 17/11/2026**

- responda **diretamente** à pergunta de pesquisa e às três QPs, com os números principais;
- diga se cada objetivo específico foi alcançado;
- retome as principais contribuições (o diagnóstico, a comparação entre métodos e o plano de correção) e as lições aprendidas (Tarefa 8.3);
- apresente as limitações com honestidade;
- trabalhos futuros: execução do plano de correção por outro(a) estudante, reavaliação antes × depois, avaliação de mais páginas e critérios, e teste com usuárias após aprovação no Comitê de Ética.

Não traga dados nem citações novas na Conclusão.

---

### 4.8 Resumo, Objetivos Específicos e Título

**Prazo: 24/11/2026** — escritos por último, com base no que foi **realmente feito**.

#### Objetivos específicos (volte à seção 1.2)
3 a 5 itens, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Sugestões de verbos:
- **identificar**, na literatura, ...;
- **avaliar** ... por meio de ferramentas automáticas ...;
- **verificar** manualmente ... com teclado e leitor de tela ...;
- **comparar** ...;
- **propor** um plano de correção ....

#### Resumo
- parágrafo único, de 150 a 500 palavras (NBR 6028:2021);
- sequência: contexto, problema, objetivo, método, **resultados com números** (quantas barreiras, quantas só a verificação manual encontrou) e conclusão;
- palavras-chave possíveis: acessibilidade web; WCAG 2.2; avaliação de acessibilidade; tecnologias assistivas; mulheres na computação;
- *Abstract* em inglês com o mesmo conteúdo.

#### Título
Curto, informativo e coerente com o objetivo. Parta do título provisório (seção 2 do documento de desenvolvimento). Evite "Um estudo sobre..." e siglas sem explicação.

---

## 5. Do TCC ao artigo: onde publicar

Com o orientador, o TCC pode virar um artigo curto. **Antes de escrever, leia pelo menos três artigos de avaliação de acessibilidade** publicados nestes eventos, na SBC OpenLib:

| Evento | Por que combina |
|---|---|
| **IHC** — Simpósio Brasileiro sobre Fatores Humanos em Sistemas Computacionais | Principal comunidade brasileira sobre acessibilidade |
| **WebMedia** — Simpósio Brasileiro de Sistemas Multimídia e Web | Trabalhos sobre sistemas web |
| **WIT** — *Women in Information Technology* (CSBC) | O tema de mulheres e acessibilidade combina muito com o evento |

Cuidados:
- confira a chamada de trabalhos (prazo, número de páginas e modelo — em geral, o modelo da SBC);
- o artigo também precisa ser acessível: tabelas de verdade (não imagens), bom contraste e descrição nas figuras;
- defina a autoria com o orientador antes de enviar;
- **nenhum artigo é enviado sem a revisão final do orientador.**

---

## 6. Erros comuns em trabalhos de acessibilidade

- Escrever que o site "é acessível" ou "não é acessível" como um todo.
- Usar a nota do Lighthouse como prova de que a página é acessível.
- Dizer que o site foi corrigido (neste ciclo, ele não foi).
- Relatar só o que as ferramentas encontraram, sem a verificação manual.
- Não informar a versão do sistema, o navegador e as páginas avaliadas.
- Explicar no Referencial conceitos que não aparecem nos Resultados.
- Citações sem referência, ou referências fora da NBR 6023:2018.

---

## 7. Checklist antes de cada entrega

- [ ] A seção responde ao que este documento pede
- [ ] Toda afirmação tem evidência (citação, critério, print ou dado da planilha)
- [ ] Números conferidos com a planilha
- [ ] Figuras e tabelas numeradas, com título acima, fonte abaixo e citadas no texto
- [ ] Citações na NBR 10520:2023 e referências na NBR 6023:2018
- [ ] Comentários da entrega anterior resolvidos
- [ ] Versão nomeada no histórico do Google Docs
- [ ] Checklist das orientações gerais (`README.md`) conferido
