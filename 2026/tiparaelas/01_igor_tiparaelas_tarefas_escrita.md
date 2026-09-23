# TiParaElas — Orientações de Escrita do TCC — Igor

**Estudante:** Igor — Curso Superior de Tecnologia em Sistemas para Internet
**Orientação:** Prof. Bruno Gomes — NIC
**Data de início:** 23/09/2026
**Documento do TCC:** será compartilhado pelo coordenador via **Google Drive**. Escreva diretamente nele, sem criar cópias paralelas.

**Temática:** Painel público de indicadores de gênero na computação com dados abertos do INEP.

> **Importante:** este documento diz **o que pesquisar e sobre o que escrever** em cada seção. Ele **não contém o texto final** — o texto é seu. As orientações gerais de escrita acadêmica, normas da ABNT, citações, referências, figuras e tabelas estão no `README.md` deste repositório; **leia-o antes de começar** e volte a ele sempre que tiver dúvida de formatação. O plano de desenvolvimento é `01_igor_tiparaelas_tarefas_desenvolvimento.md`.

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
- [5. Do TCC ao artigo](#5-do-tcc-ao-artigo)
- [6. Erros que derrubam um artigo na avaliação](#6-erros-que-derrubam-um-artigo-na-avaliação)
- [7. Checklist antes de cada entrega](#7-checklist-antes-de-cada-entrega)

---

## 1. Antes de começar

Quatro coisas precisam estar claras antes da primeira linha:

**1. O que o seu TCC afirma.** *"Construímos, dentro da plataforma TiParaElas, um painel público que visualiza a participação feminina nos cursos de computação no Brasil a partir dos dados abertos do INEP e do IBGE, e analisamos essa participação quanto à evolução no tempo, à distribuição territorial e às diferenças entre subáreas e entre ingresso e conclusão."*

**2. O que ele NÃO afirma.** Ele **não** afirma que o painel é útil, fácil de usar ou que apoia decisões — isso exigiria avaliação com participantes, que não houve. Frases como "o painel facilita a tomada de decisão" são cortadas pelos revisores. Ele também **não** explica as causas da desigualdade: os seus dados mostram **o quê** e **onde**, não **por quê**. As causas vêm da literatura, no Referencial Teórico, e são retomadas na discussão como hipóteses — nunca como achado seu.

**3. Dois tipos de contribuição, e as duas contam.** Há o **achado sobre os dados** (a série histórica, o mapa, as diferenças entre subáreas) e há as **decisões de visualização** que tornam esses dados legíveis (por que linha e não barra; por que classes numéricas na legenda; por que apresentar também o valor proporcional à população). Um TCC que só mostra gráficos é fraco; um que **justifica cada escolha de representação** com referência é um artigo.

**3b. Duas fontes de dados no mesmo site, e isso precisa ficar claro.** A plataforma passa a ter **duas páginas de transparência**: uma com os dados **da própria plataforma** (ações e perfis cadastrados) e outra com os dados **do cenário nacional** (INEP). São coisas diferentes, e confundi-las seria grave — o visitante poderia achar que as ações cadastradas no TiParaElas explicam as matrículas do país. A separação em submenus, a declaração da fonte no topo de cada página e o link cruzado entre elas são **decisões de arquitetura da informação**, e valem um parágrafo nos Resultados. No caminho, você também **corrigiu os indicadores da página antiga** — porque um número errado ao lado de um número certo contamina os dois.

**4. Todo número precisa de origem.** Ano da sinopse, tabela usada, recorte de cursos, data de acesso. Quando o revisor perguntar "de onde vem esse 15,3%?", você precisa ter a resposta. É por isso que o modelo `FonteDados` existe no plano de desenvolvimento.

**Como trabalhar no documento do Google Drive:**

- escreva direto no documento compartilhado; **não crie cópias** ("versão final 2", "corrigido") — elas se perdem e o orientador revisa a errada;
- marque estados com **Arquivo > Histórico de versões > Nomear versão atual** (ex.: `v1 - Introdução - 30/09`);
- **resolva todos os comentários** do orientador antes de entregar a seção seguinte;
- ao entregar, avise por mensagem **qual seção** está pronta para revisão.

**Regra de ouro:** escreva a partir do seu **diário de bordo**. Toda semana, ao fechar a sprint, passe as decisões do diário para o documento. Neste trabalho, em especial, as decisões sobre os dados (qual tabela, qual recorte, o que fazer com valor ausente) **são** o capítulo de Materiais e Métodos.

**Antes de escrever a primeira linha:** leia **pelo menos três artigos do WIT** na SBC OpenLib (`https://sol.sbc.org.br`) e **dois trabalhos que analisem dados do Censo da Educação Superior**. Você precisa ver o formato esperado antes de tentar produzi-lo — inclusive como esses trabalhos descrevem o recorte de dados.

---

## 2. Cronograma de entregas

| # | Seção | Prazo de entrega | Sprint correspondente |
|---|---|---|---|
| 1 | Introdução e Objetivo Geral | **30/09/2026** (quarta) | Sprint 1 |
| 2 | Referencial Teórico | **14/10/2026** (quarta) | Sprints 2 e 3 |
| 3 | Metodologia | **21/10/2026** (quarta) | Sprint 4 |
| 4 | Materiais e Métodos | **28/10/2026** (quarta) | Sprint 5 |
| 5 | Resultados | **11/11/2026** (quarta) | Sprints 6 e 7 |
| 6 | Conclusão | **18/11/2026** (quarta) | Sprint 8 |
| 7 | Resumo, Objetivos Específicos e Título | **25/11/2026** (quarta) | Sprint 9 |

**Um ajuste que você precisa conhecer desde já:** a entrega dos **Resultados (11/11)** cai no primeiro dia da Sprint 8. Nessa data você já terá o diagnóstico e as correções (Sprints 1, 2 e 6), a navegação reorganizada (Sprint 6), a série histórica, o ranking, o mapa e o indicador proporcional (Sprints 6 e 7) — ou seja, **as QP1 e QP2 completas, mais as subseções 5.1 a 5.6**. O que vem da Sprint 8 — a comparação entre subáreas e o funil ingresso → conclusão, que respondem à **QP3** — entra na **revisão que acompanha a Conclusão, em 18/11**.

Deixe as subseções 5.7 e 5.8 criadas e sinalizadas como pendentes desde 11/11, e **avise o orientador** do que está em aberto. Entregar com aviso claro é profissional; entregar sem avisar parece descuido.

**Uma vantagem do cronograma:** a subseção **5.1 (diagnóstico e correção)** pode ser escrita já em **outubro**, porque o material dela sai das Sprints 1 e 2. Adiante esse trecho enquanto espera os dados do INEP ficarem prontos — é a forma mais fácil de chegar em 11/11 com boa parte dos Resultados escrita.

**Dica de ritmo:** as entregas caem na quarta, mesmo dia em que começa a sprint seguinte. Escreva ao longo da semana — sexta e segunda, quando a sprint já produziu material — e não na terça à noite.

---

## 3. Estrutura prevista do TCC

```
Título
Resumo / Palavras-chave
Abstract / Keywords
1 INTRODUÇÃO
  1.1 Objetivo geral
  1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
  2.1 Mulheres na computação
  2.2 Dados abertos e o Censo da Educação Superior
  2.3 Visualização de dados
  2.4 Painéis (dashboards) e indicadores
  2.5 Trabalhos relacionados
3 METODOLOGIA
  3.1 Classificação da pesquisa
  3.2 Pesquisa bibliográfica
  3.3 Etapas do trabalho
  3.4 Fontes de dados e recorte
  3.5 Procedimento de extração e validação
  3.6 Limitações e ameaças à validade
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
  5.1 Diagnóstico e correção dos indicadores existentes
  5.2 Modelo de dados e procedência
  5.3 O painel desenvolvido e a organização da navegação
  5.4 Evolução da participação feminina (QP1)
  5.5 Distribuição territorial (QP2)
  5.6 Indicador proporcional e o recorte Nordeste/RN (QP2)
  5.7 Diferenças entre subáreas (QP3)
  5.8 Ingresso e conclusão (QP3)
  5.9 Discussão
6 CONCLUSÃO
REFERÊNCIAS
APÊNDICES (dicionário de dados, recorte de cursos, protocolo de extração)
```

---

## 4. Orientações por seção

---

### 4.1 Introdução

**Prazo: 30/09/2026** | Tamanho sugerido: 6 a 8 parágrafos

Siga a sequência de parágrafos do `README.md`.

#### Parágrafo 1 — Contextualização

**Pesquise sobre:** a importância da computação no mercado de trabalho e na economia brasileira (relatórios da Brasscom e do setor de TI servem), e a participação das mulheres na área. Busque os **dados do Censo da Educação Superior (INEP)** e os relatórios da **UNESCO** sobre gênero em STEM.

**Escreva sobre:** o cenário geral — a computação como área estratégica e em expansão, e a desigualdade de gênero dentro dela. Feche o parágrafo com um dado numérico que mostre o tamanho do desequilíbrio.

> **Cuidado:** não abra com "Desde os primórdios da humanidade, a tecnologia...". Comece com o dado que interessa.

#### Parágrafo 2 — Problemática

**Pesquise sobre:** as barreiras apontadas pela literatura (estereótipos, ausência de modelos de referência, falta de pertencimento, ambiente hostil) e o **histórico da queda** da participação feminina na computação a partir dos anos 1980 — há literatura brasileira e internacional sobre isso.

**Escreva sobre:**

- a sub-representação e o fato de ela **não ser recente nem acidental**;
- **e o problema específico do seu trabalho:** os dados oficiais que descrevem essa desigualdade **existem, são públicos e são atualizados anualmente** — mas estão em planilhas de dezenas de abas, com codificação técnica de áreas, sem série pronta e sem visualização. Ou seja: **o dado existe, mas não está acessível a quem precisaria dele** (coordenações de curso, projetos de extensão como o TiParaElas, gestoras públicas, pesquisadoras iniciantes);
- que, por isso, discussões sobre gênero na computação frequentemente se apoiam em impressões, em números soltos repetidos sem fonte ou em dados desatualizados.

> **Este parágrafo é o coração da sua justificativa.** Ele precisa deixar claro que o problema não é a falta de dado, e sim a falta de **acesso e de leitura** do dado.

#### Parágrafo 3 — Caminho para a solução

**Pesquise sobre:** dados abertos e transparência ativa; visualização de dados como forma de tornar informação acessível; painéis (*dashboards*) e observatórios de indicadores educacionais. Procure se **já existem painéis públicos** com esse recorte (gênero + computação + Brasil) — e o que falta neles: atualização, recorte por subárea, abertura dos dados, foco em computação.

**Escreva sobre:** por que um painel construído sobre dados oficiais resolve o problema do parágrafo 2, e cite os trabalhos e painéis existentes, sempre com referência.

#### Parágrafo 4 — Apresentação da solução

**Escreva sobre** o que foi feito, com honestidade quanto ao escopo:

- que foi desenvolvido um **painel público**, dentro da plataforma TiParaElas, alimentado pelas **Sinopses Estatísticas da Educação Superior (INEP)** e pelas **estimativas de população do IBGE**;
- o recorte: cursos de computação, por UF e por ano, cobrindo o período de X a Y (preencha com os anos reais);
- o que o painel mostra: evolução da participação feminina em matrículas, ingressos e conclusões; distribuição por UF e região; indicador proporcional à população; comparação entre subáreas; e o recorte Nordeste/RN;
- que, **antes disso**, os indicadores já existentes na seção de transparência da plataforma foram **diagnosticados e corrigidos**, e que a navegação foi reorganizada para separar claramente **os dados da plataforma** dos **dados do cenário nacional**;
- que os dados agregados podem ser **exportados em CSV**, com dicionário de dados;
- **não mencione avaliações com usuárias — elas não aconteceram.**

> Mencione a correção em **uma frase** aqui, sem detalhar. O detalhe fica nos Resultados. A introdução precisa deixar claro que ela aconteceu — porque ela sustenta a confiabilidade do resto —, mas o trabalho não é *sobre* ela.

#### Parágrafo 5 — Vínculo com o projeto

**Escreva sobre:** o TiParaElas (o repositório começa em junho de 2025), o NIC e a equipe. Confirme com o orientador o nome oficial do projeto, o edital e a instituição. **Ponto obrigatório:** o repositório tem vários autores — **deixe explícito que a sua contribuição é o painel de indicadores** (modelagem, importação, cálculo e visualização), e que o cadastro de ações, os perfis e a validação foram desenvolvidos pela equipe. Delimitar a própria contribuição em trabalho colaborativo é exigência ética, não modéstia.

#### Últimos parágrafos — Perguntas, contribuições e organização

Feche com:

- as **três questões de pesquisa** (QP1 evolução no tempo, QP2 distribuição territorial, QP3 subáreas e ingresso × conclusão);
- as **contribuições**: (a) o painel público e atualizável; (b) a série tratada e exportável, com dicionário de dados; (c) a análise dos três recortes; (d) as decisões de visualização e de navegação documentadas; (e) a correção dos indicadores existentes, com testes que a tornam permanente;
- um parágrafo sobre a **organização do texto**.

---

### 4.2 Objetivo Geral

**Prazo: 30/09/2026** | Tamanho: **uma frase**

Uma frase, com **um único verbo principal**, coerente com as questões de pesquisa e com o que a Conclusão vai afirmar.

Rascunho para adaptar (não copie — ajuste ao recorte final):

> "O objetivo principal do presente trabalho consiste no desenvolvimento de um painel público de indicadores sobre a participação feminina nos cursos de computação no Brasil, a partir dos dados abertos do Censo da Educação Superior, integrado à plataforma TiParaElas."

**Verifique três coisas:**

1. O verbo é concreto (desenvolver, construir, analisar) e não vago (estudar, abordar, compreender)?
2. Ele promete mais do que foi feito? Se a frase disser "avaliar a utilidade do painel" ou "identificar as causas da desigualdade", está errada;
3. Ele cabe na Conclusão? Você terá de escrever "o objetivo foi alcançado porque..." — se não conseguir completar a frase, o objetivo está mal formulado.

> **Uma decisão a tomar com o orientador:** o objetivo enfatiza **o painel** (produto de engenharia) ou **a análise** (produto de pesquisa)? Recomendo que o objetivo geral seja o painel e que a análise apareça nos objetivos específicos — assim o trabalho se sustenta mesmo que algum recorte da análise não renda achado forte.

> Os **objetivos específicos** são escritos por último (25/11). Deixe a seção 1.2 com um rascunho provisório e reescreva no fim. Veja a seção 4.8.

---

### 4.3 Referencial Teórico

**Prazo: 14/10/2026** (2 semanas)

> Assista antes ao vídeo indicado no `README.md`: https://youtu.be/8Qztq1Q5vb0

**Regra que vale para o capítulo inteiro:** explique **somente** os conceitos que reaparecem nos Resultados. Detalhes de Django e de Chart.js **não** vão aqui — vão para Materiais e Métodos, com referência à documentação oficial.

#### 2.1 Mulheres na computação

**Pesquise sobre:** a história da participação feminina na área, incluindo **a queda a partir dos anos 1980**; os dados atuais de matrículas e concluintes; as barreiras apontadas pela literatura; e as iniciativas de incentivo, com destaque para o **Programa Meninas Digitais** da SBC e os trabalhos publicados no **WIT**.

**Escreva sobre:** o panorama e as explicações que a literatura oferece. **Esta subseção é a que fornece as hipóteses interpretativas** que você vai usar na discussão dos Resultados — porque os seus dados mostram o padrão, mas não a causa. Quanto melhor esta subseção, mais rica a sua discussão.

> **Cuidado central deste trabalho:** a queda histórica dos anos 1980 vem da **literatura**, e não dos seus dados. Deixe isso explícito no texto — "segundo [autor], a proporção de mulheres na computação vem declinando desde a década de 1980" — e nunca apresente esse declínio como achado da sua série.

#### 2.2 Dados abertos e o Censo da Educação Superior

**Pesquise sobre:** o conceito de dados abertos e transparência ativa; a **Lei de Acesso à Informação** (Lei nº 12.527/2011); o que é o **Censo da Educação Superior** (quem produz, com que periodicidade, o que coleta, qual a diferença entre **microdados** e **sinopses estatísticas**); e a **classificação de cursos** adotada pelo INEP (CINE Brasil), incluindo **quando ela passou a ser usada** e o que havia antes.

**Escreva sobre:** a fonte que sustenta todo o seu trabalho. O leitor precisa entender, lendo esta subseção, **o que é o Censo, o que é uma sinopse e como os cursos são classificados** — porque as suas decisões de recorte, explicadas na Metodologia, dependem disso.

> Esta subseção costuma ser esquecida por quem trabalha com dados públicos, e é justamente o que separa um trabalho sério de um que "baixou uma planilha". Dedique atenção a ela.

#### 2.3 Visualização de dados

**Pesquise sobre:** tipos de dados e tarefas de visualização; **canais visuais** (posição, comprimento, cor) e sua eficácia relativa; a adequação entre tipo de dado e tipo de gráfico (**série temporal pede linha**; comparação entre categorias pede barra); **mapas coropléticos** e seus cuidados — normalização e definição das classes de cor; escalas de eixo e o efeito de truncar ou não o eixo Y; e paletas seguras para daltonismo.

**Escreva sobre:** os princípios que você **de fato aplicou**. Cada decisão do seu painel precisa ter fundamento aqui: por que a série histórica é linha; por que o ranking é de barras horizontais; por que a legenda do mapa tem classes numéricas; por que existe a versão proporcional à população; e como você escolheu a escala do eixo Y.

> **Esta é a subseção que transforma o seu trabalho em artigo.** Sem ela, os Resultados viram uma galeria de gráficos. Com ela, cada figura é uma decisão justificada.

#### 2.4 Painéis (*dashboards*) e indicadores

**Pesquise sobre:** a definição de *dashboard*, os tipos (estratégico, analítico, operacional), boas práticas de projeto e o mantra de Shneiderman ("visão geral primeiro, *zoom* e filtro, detalhes sob demanda"). Pesquise também o que caracteriza um **indicador** (definição, fórmula, fonte, periodicidade) e por que a definição explícita de cada indicador é requisito de transparência.

**Escreva sobre:** os conceitos e como eles orientaram o painel. **Não afirme que painéis melhoram a decisão** sem citação — e lembre que você não mediu isso.

#### 2.5 Trabalhos relacionados

**Pesquise** com estes termos, em português e em inglês:

- `"mulheres na computação" AND ("Censo da Educação Superior" OR "INEP")`
- `"gender gap" AND "computer science" AND "enrollment"`
- `"women in computing" AND "Brazil"`
- `"Meninas Digitais"`
- `"painel" AND "indicadores" AND "educação superior"`
- `"dashboard" AND "open data" AND "higher education"`
- `"evasão" AND "computação" AND "gênero"`

**Escreva sobre:** os trabalhos que analisaram dados do Censo com recorte de gênero e os painéis/observatórios de indicadores educacionais, sempre apontando **o que falta em cada um**. Feche com um **quadro comparativo** com critérios como: fonte dos dados, período coberto, recorte (nacional/regional), desagregação por subárea, atualização e disponibilidade dos dados. Inclua **a sua proposta como última coluna**.

> Lembrete do `README.md`: é obrigatório apontar as limitações dos trabalhos relacionados. Se um painel existente já resolvesse o problema, o seu trabalho perderia a justificativa.

**Leituras de partida** (localize a fonte original, confira e só então inclua nas Referências): Munzner (*Visualization Analysis and Design*, 2014); Shneiderman (*The Eyes Have It*, 1996); Few (*Information Dashboard Design*); Tufte (*The Visual Display of Quantitative Information*); Sarikaya *et al.* (*What Do We Talk About When We Talk About Dashboards?*, 2019); Lima (*As mulheres na Ciência da Computação*, Revista Estudos Feministas, 2013); UNESCO (*Decifrar o código*); publicações do Programa Meninas Digitais e anais do WIT; INEP (Censo da Educação Superior, sinopses e documento da classificação CINE Brasil); IBGE (estimativas da população); Lei nº 12.527/2011; documentação do Django e do Chart.js.

**Ainda nesta entrega:** organize as referências no Zotero Web e monte a primeira versão da lista de REFERÊNCIAS, **já formatada pela NBR 6023:2018** e conferida manualmente. Documentos oficiais do INEP e do IBGE têm forma específica de referenciar — confira com cuidado, e não confie no botão "Citar".

---

### 4.4 Metodologia

**Prazo: 21/10/2026** (1 semana)

Escreva em terceira pessoa e no passado ("foi realizada", "adotou-se").

#### 3.1 Classificação da pesquisa

**Escreva sobre**, com base em Gil (2017) e Prodanov e Freitas (2013), justificando cada escolha em uma frase:

- **Natureza:** aplicada;
- **Objetivos:** exploratórios e descritivos;
- **Abordagem:** quantitativa;
- **Procedimentos:** pesquisa bibliográfica, **pesquisa documental** (sobre bases de dados oficiais) e **desenvolvimento de artefato** (o painel).

#### 3.2 Pesquisa bibliográfica

**Escreva sobre:** bases consultadas, termos de busca (seção 2.5), período das publicações e critérios de inclusão e exclusão.

#### 3.3 Etapas do trabalho

**Escreva sobre:** as etapas em ordem cronológica, **com uma figura do fluxo** (draw.io):

1. revisão da literatura;
2. **diagnóstico dos indicadores já existentes na plataforma**, com reprodução e registro de cada inconsistência;
3. **correção dos indicadores e unificação das consultas em um módulo único**, com testes automatizados;
4. localização e obtenção das fontes oficiais (INEP e IBGE);
5. análise da estrutura das sinopses e definição do recorte de cursos;
6. modelagem dos dados (dimensões de UF/região, área e fonte);
7. desenvolvimento do procedimento de importação e validação;
8. implementação dos indicadores e dos testes automatizados;
9. projeto e implementação das visualizações e **da organização da navegação entre as duas páginas de transparência**;
10. análise dos resultados.

> As etapas 2 e 3 **precedem** o trabalho com os dados oficiais de propósito: não faria sentido acrescentar indicadores novos a uma seção do site cujos indicadores existentes estavam incorretos. Diga isso no texto, em uma frase — é uma decisão de método, não acaso.

#### 3.4 Fontes de dados e recorte

Subseção central. **Escreva sobre:**

- **Fonte primária:** Sinopses Estatísticas da Educação Superior (INEP). **Diga por que usou as sinopses e não os microdados** — as sinopses já vêm agregadas no recorte necessário e são muito menores, o que torna o procedimento reproduzível em um computador comum. Essa é uma justificativa legítima e deve estar escrita;
- **Período coberto** e por que esse período (disponibilidade e comparabilidade);
- **Recorte de cursos:** quais códigos da classificação entram, quais não entram, e **os casos de fronteira com a decisão tomada** (Engenharia de Computação, por exemplo, costuma ser classificada em Engenharias — diga se entrou ou não, e por quê). **Cite o documento oficial da classificação;**
- **Variáveis utilizadas:** matrículas, ingressantes e concluintes, por sexo, UF e área;
- **Fonte secundária:** estimativas de população do IBGE, com o ano de referência, usadas no indicador proporcional;
- **Data de acesso** de cada fonte.

> **A quebra de comparabilidade da classificação precisa estar aqui, explicitamente.** Se a classificação de cursos mudou em algum ponto da série, diga em qual ano, o que você fez a respeito (restringiu a série ou montou correspondência) e qual a consequência para a interpretação. **Este parágrafo é um dos que mais pesam a favor do seu trabalho** — ele mostra que você entendeu a fonte, e não apenas baixou uma planilha.

#### 3.5 Procedimento de extração e validação

**Escreva sobre:**

- como os dados foram extraídos das planilhas e normalizados;
- o **procedimento de importação automatizado**, com execução prévia em modo de simulação;
- as **validações aplicadas**: soma das UFs conferida com o total nacional publicado; verificação de que o valor feminino nunca excede o total; unicidade por ano/UF/área;
- o **tratamento de valores ausentes ou suprimidos** pelo INEP, e a diferença entre "zero mulheres" e "sem informação" (elas são apresentadas de forma diferente nos gráficos);
- os **testes automatizados** como verificação das regras de cálculo.

#### 3.6 Limitações e ameaças à validade

Subseção **obrigatória**. **Escreva sobre:**

- **o dado é de matrícula, não de pessoa:** o Censo conta vínculos; uma mesma pessoa em dois cursos aparece duas vezes;
- **o recorte de cursos é uma decisão:** incluir ou excluir Engenharia de Computação, cursos tecnológicos ou modalidade a distância altera os números. Por isso o recorte está declarado e os dados exportáveis;
- **quebra de classificação** ao longo da série, se houver;
- **sexo no Censo é uma variável binária declarada**, o que não captura a diversidade de identidades de gênero. Essa é uma limitação da fonte, não sua — **mas precisa ser dita**, e dizê-la com cuidado em um trabalho sobre gênero é sinal de maturidade;
- **os dados descrevem, não explicam:** o painel mostra onde e quanto, não por quê. As causas discutidas vêm da literatura;
- **defasagem:** o Censo mais recente disponível refere-se a um ano anterior ao corrente.

---

### 4.5 Materiais e Métodos

**Prazo: 28/10/2026** (1 semana)

Lembre-se da analogia da receita de bolo, no `README.md`: **materiais** são os ingredientes, **métodos** é o modo de preparo. Para cada item: **o que é** (com referência), **para que foi usado** e **por que foi escolhido**.

**Materiais.** Quadro-resumo com as versões **efetivamente usadas** — confira com `pip freeze` na data da escrita:

| Ferramenta | Versão | Finalidade no trabalho |
|---|---|---|
| Python | (confirme) | Linguagem do *back-end* e do tratamento de dados |
| Django | 5.1.3 | *Framework* web, ORM e agregações dos indicadores |
| MySQL | (confirme) | Armazenamento dos indicadores importados |
| pandas | (confirme) | Leitura das sinopses e normalização |
| openpyxl | (confirme) | Leitura dos arquivos `.xlsx` do INEP |
| matplotlib | (confirme) | Geração das figuras estáticas do trabalho |
| Chart.js | (**fixe e informe** — o projeto usava CDN sem versão) | Gráficos interativos do painel |
| Mapa do Brasil em SVG | — (**registre fonte e licença**) | Mapa coroplético por UF |
| Git e GitHub | — | Versionamento e rastreabilidade da contribuição |
| draw.io | — | Diagramas (fluxo das etapas, modelo de dados) |

**Métodos.** Descreva:

- **modelagem dos dados:** as entidades criadas e por que a estrutura é essa — o indicador como fato, e UF/região, área e fonte como dimensões. Explique por que **sexo foi modelado como colunas** (total e feminino) em vez de virar uma dimensão: simplifica o cálculo dos percentuais e evita registros redundantes;
- **rastreabilidade da procedência:** cada registro aponta para a fonte que o originou (órgão, ano, tabela, URL, data de acesso). Diga por que isso importa;
- **definição de cada indicador:** a fórmula, o numerador, o denominador e o que entra na contagem. Um quadro resolve bem;
- **o indicador proporcional:** a fórmula (matrículas femininas por 100 mil habitantes), a fonte da população e o ano de referência;
- **projeto das visualizações:** para cada uma — qual pergunta responde, qual tipo de gráfico foi escolhido e **por quê**, como a escala foi definida e, no mapa, como as classes da legenda foram construídas;
- **procedimento de diagnóstico dos indicadores existentes:** como cada inconsistência foi reproduzida (cenário montado no banco, comparação entre o valor exibido e o valor correto obtido por consulta direta) e como foi registrada;
- **unificação das consultas:** a decisão de concentrar os indicadores em um módulo único e por que ela evita a divergência entre páginas;
- **testes automatizados:** quantos, o que verificam e a decisão de escrever **um teste por inconsistência corrigida**, para que o erro não retorne;
- **organização da navegação:** o critério de separação entre os dados da plataforma e os dados oficiais, e as salvaguardas adotadas (rótulos, declaração de fonte em cada página, link cruzado);
- **exportação e dicionário de dados.**

> **Dica que os revisores valorizam: o "por que X e não Y".** Por exemplo: por que construir o painel dentro da plataforma, com Django e Chart.js, em vez de usar uma ferramenta de BI pronta (Power BI, Metabase, Looker Studio)? Argumentos legítimos: integração ao site existente, ausência de custo de licença, controle sobre a acessibilidade e sobre a exportação dos dados, e o fato de o painel precisar conviver com o restante da plataforma. **Informe apenas as alternativas que foram de fato consideradas.** Se nenhuma foi avaliada, diga isso e trate como limitação. **Não invente comparações.**

> **Onde a maioria erra aqui:** descrever o que o painel *mostra* em vez de descrever *como foi construído*. A descrição das telas e dos números é Resultado.

---

### 4.6 Resultados

**Prazo: 11/11/2026** (2 semanas) | Capítulo mais longo do trabalho

Organize **pelas questões de pesquisa**, e não por telas.

#### 5.1 Diagnóstico e correção dos indicadores existentes

**Escreva sobre:** os erros encontrados na tela de transparência que já existia e o que foi feito com cada um. Use um **quadro** com quatro colunas: **problema → efeito no número → correção aplicada → teste que o protege**. Os sete erros estão listados na seção 3.1 do documento de desenvolvimento.

Destaque os dois que mais importam para um trabalho sobre dados:

- **contagem que inclui registros que o site não exibe** (perfil reprovado entrava no total e no *ranking*, com link que levava a erro 404);
- **a mesma grandeza calculada de formas diferentes em páginas diferentes**, fazendo o total do painel divergir do total da galeria. A correção foi concentrar as consultas em um **módulo único**, de modo que o mesmo número apareça igual em todo o site.

**Por que esta subseção abre o capítulo, e não fica escondida no fim:** ela estabelece **a condição de confiabilidade** de tudo o que vem depois. Um trabalho que apresenta gráficos sem mostrar que verificou a origem dos números é mais fraco que um que expõe os erros encontrados e como os resolveu. **Mostrar erro corrigido é rigor, não demérito** — e nenhum desses erros foi introduzido por você.

Aproveite para registrar dois pontos de conteúdo próprio:

- a retirada do e-mail da consulta do *ranking* como aplicação concreta do princípio de **minimização de dados** da LGPD;
- o caso do fuso horário no MySQL, em que **a página funcionava em desenvolvimento e quebrava em produção** — um exemplo útil de por que o ambiente de teste precisa espelhar o de produção.

#### 5.2 Modelo de dados e procedência

**Escreva sobre:** o diagrama do modelo (figura), identificando o fato e as dimensões; um quadro com o **dicionário de dados resumido**; e a tabela de **cobertura**: quantos registros foram importados, cobrindo quantos anos, quantas UFs e quantas áreas, e de quais arquivos vieram. Informe também o resultado das **validações** (a soma por UF conferiu com o total publicado?).

> Esta subseção é curta, mas é ela que autoriza o leitor a confiar em todo o resto.

#### 5.3 O painel desenvolvido e a organização da navegação

**Escreva sobre:** as telas, com poucas figuras bem escolhidas. Para cada visualização: **anuncie a figura antes**, mostre, e **explique depois** — qual pergunta ela responde e **qual decisão de projeto foi tomada** (tipo de gráfico, escala, classes, cor). Não faça uma galeria de prints: escolha três ou quatro figuras e explique bem.

**Dedique um parágrafo à organização da navegação.** A plataforma passou a ter duas páginas de transparência alimentadas por fontes distintas — os dados da própria plataforma e os dados oficiais do Censo. Explique:

- por que manter as duas **na mesma seção do site** (são as duas respostas à pergunta "quais são os dados por trás disso?");
- por que **separá-las em submenus**, com rótulos que tornam a diferença evidente, em vez de misturar tudo em uma página só;
- **como os rótulos foram escolhidos** — um rótulo vago como "Dados Gerais" não diz de quem nem sobre o que são os dados, enquanto o par adotado contrasta a plataforma e o cenário nacional;
- as duas salvaguardas contra confusão de fontes: a **declaração da fonte no topo de cada página** e o **link cruzado** entre elas.

> Isso é **arquitetura da informação**, e é uma decisão de projeto legítima — não é "detalhe de menu". O risco real que ela evita é o leitor atribuir aos dados da plataforma uma representatividade que eles não têm. Vale meia página, com uma figura do menu aberto.

Mencione também a exportação em CSV, o dicionário de dados e o bloco "Como os números são calculados" — são elementos de transparência e valem parágrafo.

#### 5.4 Evolução da participação feminina (QP1)

**Escreva sobre:** a série histórica nacional, em matrículas, ingressos e conclusões. Responda com números: qual era o percentual no início e no fim da série; houve crescimento, estabilidade ou queda; e em quantos pontos percentuais. Apresente **a figura e a tabela** — o leitor precisa poder conferir os valores.

**Discuta:** a tendência é a mesma nos três indicadores? Se matrículas crescem mas conclusões não acompanham, isso já antecipa a QP3.

#### 5.5 Distribuição territorial (QP2)

**Escreva sobre:** o mapa por UF e a tabela por região, no ano mais recente. Responda: a desigualdade é homogênea no país? Quais UFs estão acima e abaixo da média nacional? Qual a diferença entre a maior e a menor? Comente se há padrão regional.

#### 5.6 Indicador proporcional e o recorte Nordeste/RN (QP2)

**Escreva sobre:** a comparação entre o mapa de **percentual feminino** e o de **matrículas femininas por 100 mil habitantes**, e **o que muda entre os dois**. Explique a diferença conceitual: o primeiro mede equidade dentro da área; o segundo mede oferta em relação à população. Uma UF pode ter percentual alto e, ainda assim, pouquíssimas mulheres em computação.

Em seguida, o recorte Nordeste/RN: como a região e o estado se comportam em relação ao Brasil, ao longo da série.

#### 5.7 Diferenças entre subáreas (QP3)

> Subseção **completada na revisão de 18/11**. Na entrega de 11/11, deixe-a criada e sinalizada como pendente, e avise o orientador.

**Escreva sobre:** o percentual feminino por subárea da computação e se o padrão se mantém ao longo dos anos. Se houver diferença marcante entre subáreas, **esse é um achado** — e a discussão dele, à luz do que a literatura diz sobre estereótipos associados a diferentes atividades da computação, é dos trechos mais interessantes que o trabalho pode ter.

#### 5.8 Ingresso e conclusão (QP3)

> Também completada na revisão de 18/11.

**Escreva sobre:** a comparação entre o percentual feminino entre ingressantes e entre concluintes.

**Cuidado obrigatório:** ingressantes e concluintes do mesmo ano **não são a mesma coorte** — quem conclui em um ano ingressou anos antes. Diga qual abordagem você adotou (comparação com defasagem aproximada, ou comparação apenas das tendências) e **declare que é uma aproximação**. Tratar como coorte sem ressalva é o erro que derruba o artigo.

Se houver diferença consistente, escreva com o verbo certo: os dados **sugerem** ou são **compatíveis com** evasão diferencial — eles não a **provam**, porque você não acompanhou indivíduos.

#### 5.9 Discussão

**Escreva sobre:** o que os resultados significam à luz do Referencial Teórico; como eles se relacionam com os trabalhos relacionados (confirmam? contradizem? atualizam?); e o que as **decisões de visualização** revelaram — por exemplo, o fato de o mapa absoluto e o proporcional contarem histórias diferentes é, em si, um argumento a favor de apresentar os dois.

Retome as limitações ao interpretar cada resultado.

**Cuidados que valem para o capítulo inteiro:**

- toda figura e tabela informa a fonte: *"Fonte: Elaborado pelo autor (2026), a partir de INEP (ano) e IBGE (ano)."*;
- siga as regras de tabelas do IBGE (ver `README.md`): sem traços verticais nas laterais, **"–"** para zero e **"..."** para dado não disponível;
- **use vírgula como separador decimal** e a mesma quantidade de casas em cada coluna. Percentual com duas casas decimais em um gráfico é excesso: uma casa basta;
- **não converta percentual em afirmação causal.** "O RN tem 18% de mulheres" é resultado; "o RN tem 18% porque há menos incentivo" é especulação, a menos que você cite quem afirma isso;
- toda figura é **anunciada antes** e **explicada depois**. Nunca coloque imagens em sequência sem texto entre elas.

---

### 4.7 Conclusão

**Prazo: 18/11/2026** (1 semana)

**Escreva sobre:**

1. **Resposta direta à pergunta de pesquisa e a cada uma das três QPs.** Não enrole: responda, com números;
2. um **comentário por objetivo específico**, na ordem em que foram apresentados;
3. as **contribuições**: o painel público e atualizável; a série tratada e exportável com dicionário de dados; a análise dos três recortes; as decisões de visualização e de navegação documentadas; e a correção dos indicadores existentes, protegida por testes;
4. as **limitações**, com honestidade: dado de matrícula e não de pessoa; recorte de cursos como decisão; sexo binário na fonte; ausência de avaliação com usuárias; caráter descritivo (não explicativo);
5. os **trabalhos futuros** — use a lista da seção 10 do documento de desenvolvimento: cruzar os dados do INEP com o acervo de iniciativas da plataforma; incluir recorte por raça/cor e por tipo de instituição (pública × privada); atualização automática a cada novo Censo; comparação internacional; avaliação do painel com usuárias; acessibilidade completa; histórico de validação das ações; e painéis restritos para a coordenadora e para a gestão.

**Não faça:** apresentar resultado ou citação que não apareceu antes; copiar a introdução; afirmar que o painel "facilita a tomada de decisão" (você não mediu) ou que o trabalho "explica a desigualdade de gênero na computação" (ele a descreve).

---

### 4.8 Resumo, Objetivos Específicos e Título

**Prazo: 25/11/2026** | Escritos **por último**, depois da aprovação do texto

#### Objetivos específicos (volte à seção 1.2)

De 4 a 6 itens, **verbos no infinitivo**, na **mesma ordem das etapas da Metodologia**, cada um **verificável na Conclusão**. Estrutura para adaptar:

- revisar a literatura sobre participação feminina na computação, dados abertos e visualização de dados;
- diagnosticar e corrigir os indicadores já existentes na seção de transparência da plataforma;
- definir o recorte de cursos e as variáveis a partir da classificação oficial do INEP;
- modelar e importar os dados do Censo da Educação Superior para a plataforma;
- desenvolver o painel público de indicadores, com exportação dos dados agregados;
- analisar a participação feminina quanto à evolução no tempo, à distribuição territorial e às diferenças entre subáreas.

**Confira:** cada objetivo específico tem uma subseção correspondente nos Resultados? Se um não tem, ou não foi cumprido, ou está mal formulado. E **não transforme funcionalidade em objetivo** — "permitir filtrar por estado" não é objetivo específico.

> **São seis itens, e o README recomenda de 3 a 5.** Combine com o orientador: ou o objetivo do diagnóstico/correção fica visível (ele tem subseção própria nos Resultados, então se sustenta), ou ele é incorporado ao objetivo de desenvolvimento do painel. Prefiro mantê-lo visível — é meia página de Resultados que, sem objetivo correspondente, fica órfã.

Formato: item começa em minúscula, termina com ponto e vírgula; o último termina com ponto.

#### Resumo

Parágrafo único, 150 a 500 palavras (NBR 6028:2021), impessoal, sem citações e sem menção a figuras. No artigo, siga o limite da chamada — os veículos da SBC normalmente exigem resumo em português **e** em inglês.

Sequência: contexto (sub-representação feminina na computação) → problema (os dados oficiais existem, mas não estão acessíveis nem visualizados) → objetivo → método (importação das sinopses do INEP, modelagem, cálculo de indicadores e desenvolvimento do painel) → **principais resultados, com números** → principal conclusão.

**Palavras-chave possíveis:** mulheres na computação; dados abertos; visualização de dados; painel de indicadores; educação superior.

**Abstract:** traduza e **revise**. Não confie em tradutor automático — termos como *dashboard*, *choropleth map*, *open data*, *enrollment* e *gender gap* têm forma consagrada, e você já viu essa forma nos artigos que leu.

#### Título

**Última informação a ser preenchida**, em acordo com o orientador. Rascunhos para discutir:

- *Painel público de indicadores de gênero na computação: desenvolvimento e análise a partir dos dados abertos do Censo da Educação Superior*
- *Onde estão as mulheres na computação? Um painel de indicadores a partir dos dados abertos do INEP*
- *Participação feminina nos cursos de computação no Brasil: desenvolvimento de um painel de indicadores sobre dados abertos*

**Confira:** o título é coerente com o objetivo geral e com a conclusão? Ele promete algo que o trabalho não entrega (avaliação com usuárias, explicação das causas)? Se promete, mude o título.

---

## 5. Do TCC ao artigo

**Estrutura típica do artigo:** Introdução; Fundamentação e trabalhos relacionados; Fonte de dados e método; O painel; Resultados; Discussão; Limitações; Conclusão.

**Onde publicar** — confira sempre a chamada vigente (prazos, trilhas, limite de páginas, modelo e se a revisão é às cegas):

| Veículo | Por que serve |
|---|---|
| **WIT — Women in Information Technology** (*workshop* do CSBC/SBC) | **Alvo principal.** Tema, dados e enquadramento coincidem exatamente com o escopo do evento |
| **WEI — Workshop sobre Educação em Computação** (CSBC) | Serve pelo recorte de educação superior em computação |
| **Cadernos de Gênero e Tecnologia** (UTFPR) | Periódico alinhado ao recorte de gênero |
| **SBSI / iSys** | Enquadramento em sistemas de informação, dados abertos e visualização |

Os artigos dos eventos da SBC estão na SBC OpenLib: `https://sol.sbc.org.br`.

**Antes de submeter:**

- baixe o **modelo da chamada** (em geral o modelo da SBC, também disponível no Overleaf) e confira limite de páginas e formato das referências;
- **revisão às cegas:** se for o caso, retire nomes, instituição e o nome da plataforma, substituindo por "[omitido]";
- **dados:** os dados são públicos e agregados, então **não há impedimento de privacidade**. Combine com o orientador a publicação da série tratada no **Zenodo** (gratuito, com DOI). Isso valoriza o artigo — o valor está no tratamento, não no dado bruto;
- **corte com critério:** se o limite de páginas apertar, **preserve** a seção de fonte de dados e recorte (é ela que dá credibilidade) e reduza as capturas de tela do painel. A subseção de diagnóstico e correção dos indicadores, que no TCC ocupa uma página, **no artigo cabe em um parágrafo do método** ("os indicadores preexistentes da plataforma foram diagnosticados e corrigidos antes da construção do painel, e as consultas foram unificadas em um módulo único, coberto por testes") — ela sustenta a confiabilidade, mas não é o assunto do artigo.

---

## 6. Erros que derrubam um artigo na avaliação

1. **Afirmar utilidade sem evidência.** "O painel facilita a tomada de decisão" — você não mediu isso. Corte a frase.
2. **Apresentar causas como achado.** Os dados mostram o padrão; as causas vêm da literatura e são hipóteses.
3. **Atribuir aos seus dados a queda histórica dos anos 1980.** Isso vem da literatura — a sua série não alcança esse período.
4. **Tratar ingressantes e concluintes do mesmo ano como a mesma coorte**, sem ressalva.
5. **Número sem origem.** Todo valor precisa da fonte, do ano e do recorte de cursos.
6. **Não declarar o recorte de cursos.** Se o leitor não sabe se Engenharia de Computação entrou, ele não pode comparar os seus números com nenhum outro.
7. **Omitir a quebra de classificação** na série. Se ela existe e você não disse, o trabalho tem um erro escondido.
8. **Série temporal em gráfico de barras**, ou mapa com legenda sem números. São erros de visualização em um trabalho cujo tema é, em parte, visualização.
9. **Referências inventadas.** Acontece muito com IA generativa. **Só inclua referência que você encontrou, abriu e leu.** A responsabilidade pelo texto é sua.
10. **Não delimitar a própria contribuição.** O repositório tem vários autores; deixe explícito o que é seu.

---

## 7. Checklist antes de cada entrega

- [ ] Todos os comentários da revisão anterior foram resolvidos
- [ ] Toda afirmação técnica tem citação, e toda obra citada está nas Referências
- [ ] Citações conforme a NBR 10520:2023 (`(Silva, 2020)`, com página nas diretas)
- [ ] Figuras e tabelas com identificação em cima, centralizadas, fonte embaixo **com o ano da fonte de dados**, e citadas no texto antes de aparecerem
- [ ] Tabelas seguindo as normas do IBGE; vírgula como separador decimal; casas decimais uniformes
- [ ] Numeração das seções sem ponto após o número ("3.1 Classificação da pesquisa")
- [ ] Texto impessoal e no passado
- [ ] Termos estrangeiros em itálico (*dashboard*, *framework*, *back-end*)
- [ ] Siglas por extenso na primeira ocorrência (INEP, IBGE, SBC, WIT, CINE, LAI)
- [ ] Nenhuma afirmação sobre utilidade percebida ou avaliação com usuárias
- [ ] Nenhuma afirmação causal sustentada apenas pelos seus dados
- [ ] Versão nomeada no histórico do Google Docs (ex.: `v2 - Referencial - 14/10`)
