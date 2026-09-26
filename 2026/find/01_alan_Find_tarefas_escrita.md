# Plano de escrita do TCC – Alan Bezerra (Projeto FIND)

**Projeto pai:** FIND – Plataforma e Aplicativo Móvel para Gestão de Objetos Perdidos e Encontrados (ver [projeto.md](../projeto.md)).

**Temática:** acessibilidade e design inclusivo - avaliação e correção da acessibilidade da plataforma web do FIND segundo a **WCAG 2.2**, com base no marco brasileiro (**eMAG** e **Lei Brasileira de Inclusão**, Lei nº 13.146/2015).

**Repositório:** https://github.com/gabryellgs/projeto-find (plataforma web). O aplicativo móvel (https://github.com/gabryellgs/find-app) não faz parte da avaliação deste trabalho.

**Documento complementar:** [01_alan_Find_tarefas_desenvolvimento.md](01_alan_Find_tarefas_desenvolvimento.md) - as *sprints* de desenvolvimento. Tudo o que você medir e corrigir lá vira texto aqui.

**Base de estilo e de normas ABNT:** o arquivo [README.md](../../../README.md) deste repositório. Tudo o que está lá vale aqui - estrutura, citações, referências, figuras, tabelas, formatação. Este documento **não repete** as regras da ABNT; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copie estas frases para o TCC. Elas dizem sobre o que é cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você leu.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do TCC **já foi criado e compartilhado pelo coordenador em uma pasta do Google Drive**. Você não cria arquivo novo nem trabalha em cópia local.

Como trabalhar nele:

- **Escreva sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico do Drive é o que permite ao orientador ver o que mudou de uma semana para outra.
- **Não crie cópias** ("TCC v2", "TCC final", "TCC final revisado"). O Drive já guarda tudo em **Arquivo → Histórico de versões**.
- **Marque cada entrega no histórico.** Ao terminar uma seção, use **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 02/10`.
- **Avise por mensagem quando entregar.** O orientador não fica olhando o documento; ele precisa saber que há algo novo.
- **Comentário se responde, não se apaga - e quem resolve é o orientador.** Ao atender um comentário, responda na própria conversa dizendo o que foi feito (por exemplo, "Reescrevi o segundo parágrafo e incluí a referência pedida"). **Não clique em "Resolver":** o orientador confere a alteração e, se o comentário tiver sido atendido, ele mesmo marca como resolvido; se não tiver, ele deixa um novo comentário na mesma conversa.
- **Figuras:** cole a imagem no documento e guarde o arquivo original (PNG em boa resolução) em uma subpasta `figuras/` da mesma pasta do Drive. Os gráficos gerados pelo `comparar.py` já saem em 200 dpi.

---

## Cronograma de entregas

Data de referência: **25/09/2026**. Cada prazo conta a partir da conclusão da etapa anterior; as datas abaixo consideram que cada etapa é concluída no prazo. Entregar antes é bem-vindo.

| # | Entrega | Duração | Prazo |
|---|---|---|---|
| 1 | Introdução e Objetivo Geral | 1 semana a partir de hoje | **02/10/2026** (sexta-feira) |
| 2 | Referencial Teórico | 2 semanas após a Introdução | **16/10/2026** (sexta-feira) |
| 3 | Metodologia | 1 semana após o Referencial | **23/10/2026** (sexta-feira) |
| 4 | Materiais e Métodos | 1 semana após a Metodologia | **30/10/2026** (sexta-feira) |
| 5 | Resultados e Discussão | 2 semanas após Materiais e Métodos | **13/11/2026** (sexta-feira) |
| 6 | Conclusão | 1 semana após os Resultados | **20/11/2026** (sexta-feira) |
| 7 | Resumo, Objetivos Específicos e Título | 1 semana após a Conclusão | **27/11/2026** (sexta-feira) |

**Escrita e desenvolvimento andam juntos.** Veja como uma coisa alimenta a outra:

| Semana | Desenvolvimento (*sprint*) | O que isso dá para a escrita |
|---|---|---|
| 28/09 a 02/10 | Sprint 1 - normas e ferramentas | Leitura da WCAG 2.2 e do eMAG: base da Introdução e do Referencial |
| 05/10 a 16/10 | Sprints 2 e 3 - protocolo e avaliação "antes" | O protocolo é a Metodologia quase pronta; o diagnóstico é a primeira parte dos Resultados |
| 19/10 a 06/11 | Sprints 4 a 6 - correções | O quadro de correções dos Resultados |
| 09/11 a 13/11 | Sprint 7 - avaliação "depois" | A comparação antes/depois |

**Não deixe os Resultados para as duas últimas semanas.** Escreva o diagnóstico inicial (seção 7.1) e a comparação entre ferramentas (seção 7.2) **logo depois da Sprint 3**, e o quadro de correções (seção 7.3) **à medida que corrigir**. Na semana de 09/11, só a comparação antes/depois (seção 7.4) e a discussão devem faltar. Cole as tabelas e os gráficos no documento assim que ficarem prontos, mesmo sem o texto de análise.

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Texto pela metade dá para comentar; texto que não chega, não.
- Cada entrega é: seção escrita + revisão feita com o [checklist das orientações gerais](../../../README.md#checklist-antes-de-enviar-uma-versão-ao-orientador) + versão nomeada no histórico + aviso ao orientador.
- Responda a **todos** os comentários da entrega anterior, dizendo o que foi feito, antes de avisar sobre a próxima.

---

## Que tipo de trabalho é este

Um **TCC no modelo ABNT**, escrito de forma **completa e sem limite de páginas**, do tipo **estudo de avaliação de conformidade**: aplica-se um protocolo de avaliação de acessibilidade a um sistema real, corrigem-se as barreiras encontradas e aplica-se o mesmo protocolo de novo. Escreva pensando no TCC. Depois que ele estiver pronto, **extrairemos dele um artigo**, com formato e tamanho definidos pelo veículo escolhido (ver seção 10).

**Onde o artigo poderá ser publicado** (para você conhecer desde já e usar como fonte de leitura):

- **IHC** - Simpósio Brasileiro sobre Fatores Humanos em Sistemas Computacionais (SBC). É o evento brasileiro mais próximo do tema; tem trilhas de artigos completos, curtos e de relatos;
- **JIS** - *Journal on Interactive Systems* (SBC), periódico da comunidade de IHC;
- **WebMedia** - Simpósio Brasileiro de Sistemas Multimídia e Web (SBC);
- **SBSI** - Simpósio Brasileiro de Sistemas de Informação, e a revista **iSys** (SBC);
- eventos regionais e institucionais (escolas regionais da SBC e eventos de pesquisa do IFRN), como primeira publicação.

Os artigos dos veículos da SBC estão na SBC OpenLib (SOL): https://sol.sbc.org.br. **Antes de começar a escrever, leia pelo menos três avaliações de acessibilidade publicadas no IHC ou no WebMedia** para entender o formato, o nível de detalhe do método e o tipo de tabela esperados.

Cinco coisas fazem a diferença entre um relatório de correções e um trabalho de pesquisa:

1. **O objeto do trabalho não é o sistema de achados e perdidos.** É a **acessibilidade de uma aplicação web real** e o que acontece quando ela é avaliada e corrigida com método. O FIND é o **caso**.
2. **O método tem de dar para repetir.** Amostra de páginas definida antes, ferramentas com versão, configurações, dados fictícios fixos, *checklist* escrito, *scripts* versionados. Um leitor tem de conseguir refazer a sua avaliação.
3. **Toda barreira precisa de evidência e de classificação.** Qual critério WCAG, qual recomendação eMAG, em qual página, qual ferramenta encontrou, com print. "O site tinha problemas de contraste" não é resultado; "12 ocorrências de contraste insuficiente (critério 1.4.3) em 7 das 12 páginas, com razão mínima de 2,1:1" é.
4. **As ferramentas também são objeto de análise.** Mostrar o que cada ferramenta encontrou, o que nenhuma encontrou e o que só a inspeção por teclado revelou é uma contribuição por si só (QP2).
5. **O que não foi corrigido também é resultado.** Barreira remanescente, com justificativa, mostra honestidade e indica trabalho futuro.

Estrutura sugerida:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Acessibilidade digital e pessoas com deficiência
2.2 Marco legal e normativo da acessibilidade digital no Brasil
2.3 Diretrizes de Acessibilidade para o Conteúdo Web (WCAG 2.2)
2.4 Avaliação de acessibilidade na web
2.5 Trabalhos relacionados
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

# 1. Introdução
**Prazo: 02/10/2026**

**Texto corrido, sem subtítulos.** Não crie itens como "Contextualização" ou "Problemática" dentro da Introdução: os blocos abaixo indicam **a ordem dos parágrafos** (é a sequência fixa do [README.md](../../../README.md#introdução)), e a passagem de um bloco para o outro deve ser feita com frases de transição. A Introdução fecha com as perguntas de pesquisa. Duas a três páginas.

**Primeiro bloco - contexto (2 a 3 parágrafos)**

*Pesquise sobre:*

- o número de pessoas com deficiência no Brasil - a **PNAD Contínua 2022 (IBGE)**, módulo Pessoas com Deficiência, é a fonte oficial mais recente; use o dado exato e a data da publicação;
- a dependência crescente de serviços digitais para estudar, trabalhar e acessar serviços públicos - a pesquisa **TIC Domicílios** (Cetic.br) traz dados de uso de internet;
- o conceito de **acessibilidade digital** e a ideia de que ela beneficia também idosos, pessoas com limitações temporárias (um braço quebrado) ou situacionais (sol forte na tela, celular com uma mão só).

*Fale sobre:*

- por que, quando um serviço passa a ser digital, a falta de acessibilidade **exclui** pessoas que antes eram atendidas no balcão;
- que acessibilidade na web é um **direito** garantido por lei no Brasil, e não uma cortesia (antecipe a LBI em uma frase; o detalhe fica no Referencial);
- o cenário do trabalho em uma frase ou duas: sistemas institucionais, como os de instituições de ensino, que atendem estudantes e servidores com e sem deficiência.

**Segundo bloco - o problema (2 a 3 parágrafos)**

O problema do trabalho é a **distância entre a norma e a prática** no desenvolvimento web, e não "as pessoas perdem objetos".

*Pesquise sobre:*

- o relatório **WebAIM Million** (edição mais recente): o percentual de páginas iniciais com falhas WCAG detectáveis e os tipos de erro mais comuns (baixo contraste, imagens sem texto alternativo, campos sem rótulo, links vazios);
- levantamentos sobre sites brasileiros - procure os estudos do **Movimento Web para Todos** em parceria com a BigDataCorp;
- as causas apontadas pela literatura: falta de conhecimento dos desenvolvedores, acessibilidade tratada só no fim do projeto, uso de componentes prontos sem verificação.

*Fale sobre:*

- a persistência das barreiras mesmo com diretrizes existentes há mais de 20 anos;
- que equipes pequenas, como as de projetos acadêmicos, desenvolvem com foco em funcionalidade e raramente avaliam a acessibilidade de forma sistemática;
- o problema de **como avaliar**: as ferramentas automáticas são fáceis de usar, mas detectam só uma parte das barreiras e discordam entre si - o que dificulta saber se um sistema está acessível confiando apenas nelas;
- os **critérios novos da WCAG 2.2** (2023), ainda pouco investigados em avaliações publicadas no Brasil.

**Terceiro bloco - caminhos possíveis (1 a 2 parágrafos)**

*Pesquise sobre:* métodos de avaliação de acessibilidade (ferramentas automáticas, inspeção por especialista, testes com usuários); a metodologia **WCAG-EM** da W3C; o **ASES**, avaliador do governo brasileiro.

*Fale sobre:*

- as formas de avaliar a acessibilidade e o que cada uma custa (as automáticas são rápidas e baratas; a inspeção manual exige conhecimento; os testes com usuários são os mais completos e os mais caros);
- a combinação de várias ferramentas automáticas com uma inspeção manual simples (por teclado) como um caminho **viável para equipes pequenas**;
- o que a literatura já tem (avaliações de sites de governo, de universidades, de institutos federais) e **o que falta**: avaliações que vão além do diagnóstico - que corrigem, medem de novo e comparam - e que considerem a WCAG 2.2 junto com o eMAG.

**Quarto bloco - o que este trabalho faz (2 parágrafos)**

*Fale sobre:*

- o FIND em uma visão geral: plataforma web desenvolvida em Django no IFRN para o gerenciamento de achados e perdidos, em uso por estudantes e servidores;
- o que **este trabalho** faz: avalia 12 páginas da plataforma com quatro ferramentas automáticas (axe, WAVE, Lighthouse e ASES) e uma inspeção por teclado, classifica as barreiras segundo a WCAG 2.2 e o eMAG, corrige-as e repete a avaliação com o mesmo protocolo;
- o que se espera obter: o retrato da conformidade antes e depois, a comparação entre as ferramentas e um procedimento de avaliação que outras equipes podem reaproveitar.

**Quinto bloco - vínculo com o projeto e escopo (1 parágrafo)**

*Fale sobre:*

- o histórico do FIND (desde novembro de 2025, inicialmente para o IFRN Campus Canguaretama), a equipe e o projeto institucional a que ele pertence;
- **a sua participação**: você já contribuiu com o FIND antes deste trabalho (telas de itens encontrados e perdidos, ajustes de cores e validação de funcionalidades, entre janeiro e julho de 2026). Diga isso e deixe claro que a avaliação e as correções de acessibilidade são a contribuição deste TCC;
- o que **não** é escopo: o aplicativo móvel, os painéis de bolsista, de administrador e de IoT, e a avaliação com usuários com deficiência.

**Fechamento - perguntas de pesquisa (1 parágrafo)**

Feche a Introdução apresentando, em texto corrido, as três perguntas que organizam os Resultados:

- **QP1:** qual é o nível de conformidade da plataforma web do FIND com os critérios A e AA da WCAG 2.2 e com as recomendações do eMAG, e quais são as barreiras mais frequentes?
- **QP2:** quais barreiras cada ferramenta automática detecta, e quais só aparecem na inspeção por teclado?
- **QP3:** qual foi o efeito das correções aplicadas sobre os indicadores de acessibilidade?

---

# 2. Objetivo Geral
**Prazo: 02/10/2026** (junto com a Introdução)

- Uma frase, com **um único verbo principal**, coerente com as perguntas de pesquisa (regras em [README.md](../../../README.md#objetivo-geral));
- o objeto do objetivo é a **acessibilidade da plataforma web do FIND**, e não "desenvolver um sistema de achados e perdidos";
- estrutura para você completar:

> "O objetivo principal do presente trabalho consiste em avaliar [...] da plataforma web FIND em relação às [...] e ao [...], comparando [...] antes e depois da correção das barreiras identificadas."

Verbos que combinam: **avaliar** (o melhor para este trabalho), **analisar**, **aprimorar**. Evite "desenvolver" e "criar": o trabalho avalia e corrige um sistema que já existe.

---

# 3. Objetivos Específicos

**Não escreva agora.** Eles serão entregues no final (27/11/2026), junto com o Resumo e o Título, para refletirem o que foi **realmente feito**. Siga as regras das orientações gerais: 3 a 5 itens, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Verbos e temas que combinam com este trabalho:

- **definir** um protocolo de avaliação ... com base na WCAG-EM ...;
- **identificar** as barreiras de acessibilidade ... por meio de ferramentas automáticas e de inspeção por teclado ...;
- **comparar** as barreiras detectadas por cada ...;
- **corrigir** as barreiras ... priorizando ...;
- **mensurar** o efeito das correções ... comparando ...

Não transforme correções em objetivos (por exemplo, "adicionar um link para pular ao conteúdo").

---

# 4. Referencial Teórico
**Prazo: 16/10/2026**

Antes de começar, assista ao vídeo sobre Referencial Teórico: https://youtu.be/8Qztq1Q5vb0.

Explique **somente os conceitos que aparecem depois nos Resultados**. Pense assim: se o termo "nome acessível" vai aparecer na análise dos botões com ícone, o leitor do TCC precisa ter aprendido o que é nome acessível aqui. Detalhes de instalação e uso das ferramentas vão para Materiais e Métodos.

## 4.1 Acessibilidade digital e pessoas com deficiência

**Pesquise sobre:** o conceito de deficiência na LBI e na Convenção sobre os Direitos das Pessoas com Deficiência (ONU, promulgada no Brasil pelo Decreto nº 6.949/2009) - o **modelo social**, em que a deficiência resulta da interação entre a pessoa e as barreiras do ambiente; definição de acessibilidade digital; tecnologias assistivas (leitor de tela, navegação por teclado, ampliador de tela, *software* de reconhecimento de voz); desenho universal.

**Fale sobre:** a ideia central do modelo social aplicada à web - **a barreira está no sistema, e não na pessoa**. Um botão sem nome acessível impede que um usuário de leitor de tela conclua a tarefa; o problema é do botão. Apresente brevemente as tecnologias assistivas e **como cada uma depende do código** (o leitor de tela lê a estrutura do HTML; quem navega por teclado depende do foco visível e da ordem do foco). Essa ligação entre tecnologia assistiva e código é o que dá sentido às correções dos Resultados.

## 4.2 Marco legal e normativo da acessibilidade digital no Brasil

**Pesquise sobre:**

- **Lei nº 13.146/2015** (Lei Brasileira de Inclusão), em especial o art. 63;
- **Decreto nº 5.296/2004** (art. 47) e **Lei nº 10.098/2000**;
- **eMAG 3.1** - Modelo de Acessibilidade em Governo Eletrônico: origem, estrutura (45 recomendações em seis seções) e relação com a WCAG;
- a **ABNT NBR 17225:2025**, norma brasileira de requisitos de acessibilidade para conteúdo e aplicações web - confira o título exato e a data de publicação;
- o **ASES**, avaliador do governo brasileiro, baseado no eMAG.

**Fale sobre:** a obrigação legal da acessibilidade digital no Brasil e **por que ela alcança o FIND** (um sistema nascido em uma instituição federal de ensino); o eMAG como referência nacional e sua relação com a WCAG (o eMAG 3.1 se baseia na WCAG 2.0; a WCAG 2.2 é mais recente e traz critérios que ele não cobre); e como a nova norma da ABNT se posiciona em relação aos dois. Termine com um **quadro de correspondência** entre as seções do eMAG e os princípios da WCAG - ele justifica, na Metodologia, por que o trabalho usa os dois.

## 4.3 Diretrizes de Acessibilidade para o Conteúdo Web (WCAG 2.2)

**Pesquise sobre:** a W3C e a WAI; a evolução da WCAG (1.0, 2.0, 2.1, 2.2); os **quatro princípios** (perceptível, operável, compreensível e robusto); as diretrizes, os critérios de sucesso e os **níveis de conformidade** (A, AA e AAA); os **critérios novos da versão 2.2**; a remoção do critério 4.1.1; a especificação **WAI-ARIA** (papéis, estados e propriedades) e o conceito de **nome acessível**.

**Fale sobre:**

- a organização da WCAG em princípios → diretrizes → critérios de sucesso, com um exemplo de cada princípio **tirado do tipo de barreira que você encontrou no FIND** (contraste para "perceptível", foco visível para "operável", rótulos de formulário para "compreensível", nome acessível para "robusto");
- por que o nível **AA** é a meta usual (é o exigido pela maioria das legislações e pela própria recomendação da W3C para conformidade de sites);
- os seis critérios novos da 2.2 nos níveis A e AA (2.4.11, 2.5.7, 2.5.8, 3.2.6, 3.3.7 e 3.3.8), explicando cada um em uma ou duas frases - pelo menos três deles aparecem na sua avaliação;
- o papel do WAI-ARIA e a regra de ouro "use HTML nativo antes de ARIA": ela justifica várias correções que você fez (trocar `<div>` por `<button>`, `<label>` em vez de `aria-label` sempre que possível).

Inclua como quadro a tabela de critérios A e AA que você montou na Sprint 1 (Tarefa 1.2), com a correspondência eMAG. Se ficar longa, vá para o Apêndice e cite no texto.

## 4.4 Avaliação de acessibilidade na web

**Pesquise sobre:**

- os três tipos de avaliação: **automática**, **inspeção manual/por especialista** e **com usuários**;
- a **WCAG-EM** (*Website Accessibility Conformance Evaluation Methodology*, W3C): as cinco etapas (definir o escopo, explorar o site, selecionar uma amostra representativa, avaliar a amostra e relatar os resultados);
- as **limitações das ferramentas automáticas**: o que elas conseguem verificar (atributos presentes, contraste calculável) e o que não conseguem (se o texto alternativo faz sentido, se a ordem do foco é lógica); estudos que compararam ferramentas e mostraram cobertura parcial e divergência entre elas;
- as ferramentas usadas: axe-core, WAVE, Lighthouse e ASES - o que cada uma avalia e como relata.

**Fale sobre:** por que nenhuma ferramenta sozinha garante conformidade, e por que combinar ferramentas com inspeção manual é a prática recomendada; a WCAG-EM como a base do seu protocolo; os conceitos de **falso positivo** (a ferramenta aponta um problema que não existe) e **falso negativo** (a ferramenta não detecta um problema real). Esses dois conceitos são essenciais para a QP2.

## 4.5 Trabalhos relacionados

**Busque** avaliações de acessibilidade de sistemas web, preferencialmente brasileiros e preferencialmente com correção e reavaliação. Bases: SBC OpenLib (SOL) - anais do IHC e do WebMedia -, ACM Digital Library (anais da W4A e da ASSETS), IEEE Xplore, Google Acadêmico e o Portal de Periódicos da CAPES. Termos de busca (em português e em inglês):

- `"avaliação de acessibilidade" AND ("WCAG" OR "eMAG")`;
- `"acessibilidade" AND ("instituto federal" OR "universidade") AND "site"`;
- `"web accessibility evaluation" AND "automated tools" AND "comparison"`;
- `"WCAG 2.2"`;
- `"accessibility" AND "before and after" AND "web"`;
- `"ASES" AND "eMAG"`.

Termine a seção com um **quadro comparativo** (5 a 8 trabalhos), com critérios como: sistema avaliado, diretriz usada (WCAG 2.0/2.1/2.2, eMAG), ferramentas usadas, inspeção manual (sim/não), avaliação com usuários (sim/não), houve correção (sim/não), houve reavaliação (sim/não). A última linha é o seu trabalho - o quadro deve deixar visível a lacuna que ele ocupa (provavelmente: WCAG 2.2 + eMAG + comparação entre ferramentas + antes/depois).

## Leituras de partida

Localize a fonte original, confira os dados e só depois inclua nas Referências:

- W3C. *Web Content Accessibility Guidelines (WCAG) 2.2* (Recomendação W3C, 2023) e o documento *Understanding WCAG 2.2*;
- W3C. *Website Accessibility Conformance Evaluation Methodology (WCAG-EM) 1.0* (2014);
- W3C. *WAI-ARIA 1.2* e *ARIA Authoring Practices Guide*;
- BRASIL. *eMAG - Modelo de Acessibilidade em Governo Eletrônico*, versão 3.1 (2014);
- BRASIL. Lei nº 13.146, de 6 de julho de 2015 (Lei Brasileira de Inclusão);
- BRASIL. Decreto nº 5.296, de 2 de dezembro de 2004;
- ABNT NBR 17225:2025;
- IBGE. PNAD Contínua 2022 - Pessoas com Deficiência;
- WEBAIM. *The WebAIM Million* (edição mais recente);
- VIGO, M.; BROWN, J.; CONWAY, V. *Benchmarking web accessibility evaluation tools: measuring the harm of sole reliance on automated tests* (W4A, 2013);
- documentação oficial do axe-core (Deque), do WAVE (WebAIM), do Lighthouse (Google) e do ASES.

Regras de citação e de referência: [README.md](../../../README.md#como-citar-nbr-105202023) e [README.md](../../../README.md#referências).

---

# 5. Metodologia
**Prazo: 23/10/2026**

Antes de escrever, consulte as metodologias prontas na pasta de orientações anteriores: https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing.

**Texto corrido, sem subtítulos**, como na Introdução. Os blocos abaixo indicam a ordem dos parágrafos. A esta altura, o protocolo (`acessibilidade/PROTOCOLO.md`, Sprint 2) já está pronto: a Metodologia é, em grande parte, esse protocolo escrito em linguagem acadêmica.

**Primeiro bloco - classificação da pesquisa (1 a 2 parágrafos)**

*Fale sobre:* natureza **aplicada** (resolve um problema de um sistema real); objetivos **exploratórios e descritivos**; abordagem **quali-quantitativa** - quantitativa nas contagens de violações e nas pontuações, qualitativa na classificação das barreiras e na análise das correções. Nos procedimentos: pesquisa bibliográfica e **estudo de caso único** com **avaliação de conformidade antes e depois** das correções, baseada na WCAG-EM. Justifique a ausência de participantes: a avaliação é feita por inspeção e por ferramentas, sem usuários, o que dispensa a submissão ao Comitê de Ética em Pesquisa.

**Segundo bloco - o caso e o escopo da avaliação (1 parágrafo)**

*Fale sobre:* a plataforma web do FIND (tecnologias em uma frase), o escopo da avaliação (páginas públicas e páginas do usuário comum), a **meta de conformidade** (WCAG 2.2, níveis A e AA, e eMAG 3.1) e o que ficou fora (aplicativo móvel e painéis administrativos). Isso corresponde à etapa 1 da WCAG-EM.

**Terceiro bloco - a amostra (1 parágrafo e um quadro)**

*Fale sobre:* como as 12 páginas foram escolhidas (etapas 2 e 3 da WCAG-EM: páginas mais usadas + pelo menos uma de cada tipo - formulário, lista, detalhe, conversa, *upload*); apresente o **quadro da amostra** (ID, página, tipo, exige login). Explique que as páginas foram avaliadas com **dados fictícios fixos**, gerados por um comando, para garantir o mesmo conteúdo nas duas rodadas e para não expor dados reais (LGPD).

**Quarto bloco - as etapas do trabalho (2 a 3 parágrafos e uma figura)**

Descreva as etapas em ordem, com uma **figura do fluxo** (as cinco etapas da WCAG-EM adaptadas ao seu trabalho, mostrando o ciclo avaliar → corrigir → reavaliar):

1. estudo das diretrizes e montagem do quadro de critérios WCAG 2.2 × eMAG;
2. definição do protocolo e da amostra;
3. avaliação inicial (versão marcada com a *tag* `a11y-antes`);
4. consolidação das barreiras e priorização;
5. correção;
6. reavaliação com o mesmo protocolo (*tag* `a11y-depois`);
7. comparação dos resultados.

A ordem dessas etapas é a ordem que os Objetivos Específicos vão seguir.

**Quinto bloco - critérios de análise (1 a 2 parágrafos)**

*Fale sobre:*

- **o que conta como barreira** e a **regra de unificação** (um mesmo problema, em um mesmo componente e critério, é uma barreira, mesmo que várias ferramentas o apontem ou que ele apareça em várias páginas por vir do *template* base);
- as **unidades de medida** (regras violadas e ocorrências, no axe; erros e erros de contraste, no WAVE; pontuação de 0 a 100, no Lighthouse; percentual, no ASES; itens atendidos, no *checklist*) - e por que elas **não são comparáveis entre si**, só dentro de cada ferramenta, entre o antes e o depois;
- o **critério de priorização** das correções (barreiras que impedem o uso → globais → número de páginas afetadas → impacto).

---

# 6. Materiais e Métodos
**Prazo: 30/10/2026**

Relembre a analogia da receita de bolo do [README.md](../../../README.md#materiais-e-métodos): outra pessoa precisa conseguir repetir a avaliação.

## 6.1 Materiais

Monte um **quadro-resumo** com as versões **efetivamente usadas** (anotadas na Sprint 1 e confirmadas no dia de cada rodada):

| Ferramenta | Versão | Finalidade no trabalho |
|---|---|---|
| FIND (plataforma web) | *tags* `a11y-antes` e `a11y-depois` | Sistema avaliado |
| Python / Django | 3.12 / 6.0.3 | Execução local do FIND |
| Navegador (Edge ou Chrome) | versão do dia | Execução das ferramentas |
| axe-core (via `axe-playwright-python`) | impressa pelo script | Avaliação automática de todas as páginas |
| Playwright para Python | `pip show playwright` | Automação do navegador |
| axe DevTools (extensão, versão gratuita) | versão da extensão | Investigação dos elementos com problema |
| WAVE (extensão) | versão da extensão | Avaliação automática e estrutura da página |
| Lighthouse | rodapé do relatório | Pontuação de acessibilidade |
| ASES Web | versão informada no site | Avaliação segundo o eMAG |
| WebAIM Contrast Checker | – | Cálculo das razões de contraste |
| Faker, pandas, matplotlib | `pip show` | Dados fictícios, análise e gráficos |
| Git e GitHub | – | Versionamento e *tags* das rodadas |

Informe também a **resolução** usada (1366 × 768) e o sistema operacional.

## 6.2 Métodos

Para cada item, explique **o que é, para que foi usado e por que foi escolhido**:

- **dados fictícios:** o comando `popular_dados_avaliacao` - o que ele cria (2 usuários, 12 itens, dois terços com foto, uma conversa com mensagens) e por que os dados são fixos;
- **avaliação automática com o axe-core:** o *script* `avaliar_axe.py` - como ele autentica, que conjunto de regras usa (*tags* WCAG 2.0, 2.1 e 2.2, níveis A e AA), o que grava e por que automatizar (evitar erro de transcrição e garantir a mesma execução nas duas rodadas). Mostre um **trecho curto** do *script* como quadro;
- **WAVE, Lighthouse e ASES:** como cada um foi executado (modo anônimo e categoria única no Lighthouse; código-fonte no ASES para páginas com login) e o que foi registrado de cada um;
- **inspeção por teclado:** o *checklist* K1 a K11, com o critério WCAG de cada item e como ele é verificado;
- **consolidação das barreiras:** a planilha - colunas, regra de unificação, códigos B01, B02...;
- **correções:** como foram feitas e rastreadas (commits com o código da barreira), e como foi verificado que nada quebrou (testes automatizados existentes e conferência manual);
- **comparação:** o *script* `comparar.py` e o que ele gera.

> **Dica:** os revisores de IHC valorizam o "por que esta ferramenta e não outra". Explique a escolha de cada uma: o axe por ser o motor mais usado e aberto, o WAVE por mostrar a estrutura da página, o Lighthouse por estar embutido no navegador e ser muito usado por desenvolvedores, e o ASES por ser a referência do governo brasileiro e avaliar segundo o eMAG.

---

# 7. Resultados e Discussão
**Prazo: 13/11/2026**

Organize o capítulo pelas **questões de pesquisa**. Cada tabela e cada gráfico tem de ser citado e comentado no texto antes de aparecer: o que ele mostra, qual é o número mais importante e o que isso significa.

## 7.1 Diagnóstico inicial (QP1)

**Apresente:**

- uma **tabela por página** com os indicadores da rodada "antes": regras violadas e ocorrências (axe), erros e erros de contraste (WAVE), pontuação (Lighthouse), percentual (ASES) e itens atendidos no *checklist* de teclado;
- os **critérios WCAG mais violados** (tabela ou gráfico de barras horizontais, ordenado), com o nível (A/AA) e a recomendação eMAG correspondente;
- a distribuição das barreiras pelos **quatro princípios** da WCAG e pelo **impacto** (crítico, sério, moderado, menor);
- a separação entre **barreiras globais** (vindas do `base.html` e do CSS comum) e **locais** (de uma página só) - e quantas páginas cada barreira global afeta;
- o que **já atendia** aos critérios (idioma declarado, textos alternativos presentes, abas com ARIA) - avaliação equilibrada mostra os dois lados.

**Discuta:** quais tipos de barreira predominam e se isso coincide com o que o WebAIM Million e os trabalhos relacionados relatam; qual o efeito de o *template* base concentrar parte dos problemas; como se saíram os **critérios novos da WCAG 2.2** (2.4.11, 2.5.7, 2.5.8, 3.3.8).

## 7.2 Comparação entre as ferramentas e a inspeção por teclado (QP2)

**Apresente:**

- uma **tabela "barreira × quem detectou"** (colunas axe, WAVE, Lighthouse, ASES, Teclado) - é a coluna "Detectada por" da planilha de barreiras;
- um resumo: quantas barreiras cada ferramenta detectou, quantas foram detectadas por **todas**, quantas por **uma só**, e quantas **só pelo teclado**. Um diagrama de Venn ou um gráfico de barras empilhadas funciona bem;
- **exemplos concretos** (com print) de: uma barreira que só o teclado revelou (por exemplo, foco invisível ou foco encoberto pela barra fixa); um possível **falso positivo** de alguma ferramenta; uma divergência entre ferramentas sobre o mesmo elemento.

**Discuta:** por que as ferramentas diferem (motores diferentes, regras diferentes, o ASES avalia o HTML sem executar o JavaScript, o Lighthouse usa um subconjunto do axe); o que isso significa para uma equipe pequena que confia em uma ferramenta só; e se os seus números confirmam a literatura sobre a cobertura parcial das ferramentas automáticas (VIGO; BROWN; CONWAY, 2013).

## 7.3 Correções aplicadas

**Apresente:**

- um **quadro de correções**: barreira (código), critério WCAG, o que foi alterado, arquivo(s) e páginas beneficiadas;
- **dois ou três exemplos** em detalhe, com trecho de código **antes e depois** (poucas linhas, numeradas como quadro) e print da tela - escolha os mais representativos: o link "Pular para o conteúdo", o foco visível e um rótulo de formulário, por exemplo;
- o **quadro de cores** alteradas: cor antiga, cor nova e as duas razões de contraste;
- as **barreiras não corrigidas**, com a justificativa de cada uma.

**Discuta:** quais correções foram simples (um atributo) e quais exigiram mudar a estrutura da página; o **efeito multiplicador** das correções no *template* base; e as correções que usaram HTML nativo em vez de ARIA, relacionando com o Referencial.

## 7.4 Comparação antes e depois (QP3)

**Apresente:**

- a tabela por página com **antes, depois e diferença** para cada indicador;
- o **gráfico de ocorrências por página** (antes × depois) e o de violações por critério WCAG, gerados pelo `comparar.py`;
- a evolução das pontuações do Lighthouse e do ASES e dos itens atendidos no *checklist*.

**Discuta:**

- quanto cada indicador melhorou, e se todas as ferramentas "concordam" sobre a melhora;
- casos em que a pontuação quase não mudou apesar das correções (ou mudou muito com pouca correção) - e por quê. Isso mostra que **pontuação não é o mesmo que conformidade**;
- se o FIND passou a atender aos níveis A e AA **nas páginas avaliadas**. Cuidado com a afirmação: conformidade total exige avaliação manual de todos os critérios e, idealmente, testes com usuários. Diga exatamente o que os seus dados permitem afirmar.

## 7.5 Discussão e limitações

Esta seção dá um passo atrás: em vez de descrever os números, ela os **interpreta**. Duas a três páginas, em texto corrido, nesta ordem:

1. **Síntese (1 parágrafo).** O que o trabalho mostrou, em poucas frases, respondendo às três QPs.
2. **Relação com o Referencial e com os trabalhos relacionados (2 parágrafos).** O FIND tem as mesmas barreiras que os sites avaliados na literatura? A comparação entre ferramentas confirma os estudos anteriores? O que o seu trabalho acrescenta ao quadro comparativo da seção 4.5 (WCAG 2.2, eMAG, antes/depois)?
3. **Implicações para quem desenvolve (1 parágrafo).** O que uma equipe pequena, como a do FIND, pode aprender: quais barreiras são evitadas desde o início com pouco esforço, a importância do *template* base, a combinação mínima de ferramentas que valeu a pena, e como o *script* do axe pode ser usado para impedir que novas barreiras entrem no código.
4. **Limitações (1 a 2 parágrafos).** Para cada uma, diga o que foi feito para reduzi-la:
   - **amostra de 12 páginas**, e não o sistema inteiro;
   - **ausência de avaliação com usuários** com deficiência e de teste com leitor de tela;
   - a **mesma pessoa avaliou e corrigiu** - reduzido pelo protocolo escrito antes da primeira rodada e pela execução automatizada;
   - as **ferramentas mudam de versão** e os resultados dependem delas - por isso as versões estão registradas;
   - os critérios que dependem de julgamento (qualidade do texto alternativo, clareza das instruções) foram avaliados de forma limitada.

**Cuidados gerais nos Resultados:**

- **não exponha dados reais de usuários** em prints: use sempre o ambiente local com os dados fictícios;
- trechos de código só quando ilustram uma correção, com poucas linhas e numerados como quadro;
- figuras e tabelas seguem o [README.md](../../../README.md#como-incluir-imagens): título acima, fonte abaixo, citadas no texto antes de aparecerem. Nos prints das ferramentas, a fonte é "Elaborado pelo autor (2026), com a ferramenta X".

---

# 8. Conclusão
**Prazo: 20/11/2026**

**Fale sobre:**

- a resposta **direta** a cada QP, em poucas frases cada, com o número principal de cada uma;
- se o objetivo geral foi atingido;
- as contribuições do trabalho: o diagnóstico e as correções no FIND, a comparação entre as ferramentas e o procedimento reprodutível (protocolo, dados fictícios e *scripts*) que outras equipes podem reaproveitar;
- as limitações, com honestidade (amostra, ausência de usuários, uma única pessoa avaliando);
- trabalhos futuros **coerentes com os resultados**: avaliação com leitor de tela e com usuários que usam tecnologia assistiva; extensão aos painéis administrativos e ao aplicativo móvel; o *script* do axe em integração contínua.

Não traga informação nova nem citações na Conclusão (regras em [README.md](../../../README.md#conclusão)).

---

# 9. Resumo, Título e Objetivos Específicos
**Prazo: 27/11/2026**

## 9.1 Resumo e *Abstract*

- **Tamanho:** no TCC, parágrafo único com 150 a 500 palavras (NBR 6028:2021). Os veículos da SBC exigem resumo em português e em inglês.
- **Sequência:** contexto (acessibilidade como direito), problema (barreiras persistentes e limitações das ferramentas), objetivo, método (estudo de caso com avaliação antes e depois, 12 páginas, quatro ferramentas e inspeção por teclado, WCAG 2.2 e eMAG), principais resultados **com números** (barreiras encontradas, corrigidas e a variação dos indicadores; o que só o teclado revelou) e a principal conclusão.
- **Palavras-chave possíveis:** acessibilidade na web; WCAG 2.2; eMAG; avaliação de conformidade; ferramentas de avaliação automática; inclusão digital.

## 9.2 Título

Definido por último, depois da aprovação do texto. Deve deixar claro que o trabalho **avalia e corrige** a acessibilidade e citar as referências normativas. Título provisório para referência:

> *Avaliação e correção da acessibilidade de uma plataforma web segundo a WCAG 2.2 e o eMAG: um estudo de caso da plataforma FIND*

## 9.3 Objetivos Específicos

Escreva agora, olhando para as etapas da Metodologia e para o que foi realmente feito (ver seção 3 deste documento).

---

# 10. Do TCC ao artigo

Esta etapa começa **depois** que o TCC estiver aprovado.

- **Estrutura típica de um artigo de avaliação de acessibilidade:** Introdução; Fundamentação (WCAG 2.2, eMAG e avaliação) e trabalhos relacionados; Método (escopo, amostra, ferramentas, protocolo); Resultados (diagnóstico, comparação entre ferramentas, correções, antes e depois); Discussão e limitações; Conclusão.
- **Modelo:** o exigido pela chamada (em geral, o modelo da SBC, também disponível no Overleaf).
- **Enxugar:** no artigo, o Referencial vira uma seção curta, o quadro de critérios vai para material suplementar, e o foco fica nas tabelas da QP2 (quem detectou o quê) e da QP3 (antes e depois).
- **Material suplementar:** a pasta `acessibilidade/` do repositório (protocolo, *scripts*, resultados) pode ser citada como artefato do artigo - os eventos da SBC valorizam artefatos disponíveis para reprodução.
- **Revisão às cegas:** se for o caso, retire da versão submetida os nomes, a instituição e o *link* do repositório. Uma opção para o *link* é o Anonymous GitHub.
- **Autoria:** aluno, orientador e, se for o caso, demais integrantes da equipe do FIND.
- **Submissão:** nenhum artigo deve ser submetido sem a revisão final do orientador.
