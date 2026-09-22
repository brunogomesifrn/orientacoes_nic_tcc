# Plano de escrita do artigo – Bruno (Técnico Integrado em Informática)

**Projeto pai:** Narrativas – plataforma digital para registro, organização e difusão das narrativas populares do Rio Grande do Norte (ver [projeto.md](../projeto.md)).

**Temática:** 4.1 – Exportação de narrativas para folder em PDF (ver [tematicas.md](../tematicas.md)).

**Plano de desenvolvimento correspondente:** `01_bruno_narrativas_tarefas_desenvolvimento.md`.

**Base de estilo e de normas ABNT:** o arquivo [README.md](../../../README.md) deste repositório. Tudo o que está lá vale aqui — estrutura, citações, referências, figuras, tabelas, formatação. Este documento **não repete** as regras da ABNT; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copie estas frases para o artigo. Elas dizem sobre o que é cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você leu.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do artigo será **criado e compartilhado pelo coordenador em uma pasta do Google Drive**. Você não cria arquivo novo nem trabalha em cópia local.

- **Escreva sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico do Drive é o que permite ao orientador ver o que mudou de uma semana para outra.
- **Não crie cópias** ("Artigo v2", "Artigo final", "Artigo final revisado"). É a forma mais rápida de perder trabalho. O Drive já guarda tudo em **Arquivo → Histórico de versões**.
- **Marque cada entrega no histórico.** Ao terminar uma seção, use **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 29/09`.
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
| 22/09 a 28/09 | Sprint 1 – ambiente e primeiro PDF | Introdução e Objetivo Geral (29/09) |
| 29/09 a 12/10 | Sprints 2 e 3 – acervo, modelo do folder e FPDF2 | Referencial Teórico (13/10) |
| 13/10 a 19/10 | Sprint 4 – ReportLab | Metodologia (20/10) |
| 20/10 a 26/10 | Sprint 5 – xhtml2pdf e WeasyPrint | Materiais e Métodos (27/10) |
| 27/10 a 09/11 | Sprints 6 e 7 – medições, fidelidade e gráficos | Resultados (10/11) |
| 10/11 a 16/11 | Sprint 8 – quadro e recomendação | Conclusão (17/11) |
| 17/11 a 23/11 | — | Resumo, Objetivos e Título (24/11) |

**Dois avisos sobre o cronograma:**

1. **A Metodologia vence em 20/10**, quando você ainda terá feito só duas bibliotecas. Isso é normal: escreva falando do **plano** ("serão comparadas três bibliotecas...") e passe tudo para o passado na revisão final;
2. **Os Resultados vencem em 10/11**, logo depois da semana mais pesada. A solução é **ir preenchendo as tabelas a cada sprint que fecha**, e não tudo na última semana. Quem deixa os Resultados para o fim não entrega.

**Uma vantagem que o seu cronograma tem, aproveite:** o Referencial vence logo depois da Sprint 3, quando você acabou de brigar com fontes e acentuação na FPDF2. Escreva a parte do referencial que fala de PDF e codificação de caracteres **na mesma semana** em que você estiver vivendo esse problema. Sai muito mais fácil, e o texto fica muito melhor.

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Texto pela metade dá para comentar; texto que não chega, não.
- Cada entrega é: seção escrita + versão nomeada no histórico + aviso ao orientador.
- Resolva **todos** os comentários da entrega anterior antes de avisar sobre a próxima.

---

## Que tipo de trabalho é este

Escreva no formato de **artigo científico**, de 8 a 12 páginas, no modelo do evento ou da revista de destino. **Confirme com o orientador qual é o destino antes de começar** — dele vêm o modelo, o limite de páginas e o idioma.

**A coisa mais importante que você precisa entender antes de escrever a primeira linha:**

> O seu trabalho **não é** "fiz um programa que gera PDF". O seu trabalho é **"descobri qual biblioteca Python é a mais adequada para gerar o folder do projeto Narrativas, e provei com medições"**.

A diferença entre as duas frases é a diferença entre um relatório técnico e um artigo. Guarde isso: toda vez que você estiver em dúvida sobre o que escrever, pergunte-se se aquilo ajuda a responder a pergunta do trabalho.

O seu trabalho tem três coisas a favor, e você deve explorar as três:

1. **Ele produz números.** Fidelidade, tempo, tamanho, acentuação — tudo medido, com tabelas e gráficos;
2. **Ele responde a uma pergunta real e em aberto.** A equipe do Narrativas **ainda não escolheu** biblioteca nenhuma. A sua recomendação vai decidir a implementação futura. Diga isso na Introdução;
3. **Ele tem um resultado que quase ninguém publica:** uma das bibliotecas **não pôde ser instalada** no ambiente disponível. Isso é informação valiosa para quem vai decidir, e é o tipo de coisa que só se descobre tentando.

Estrutura sugerida das seções:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Narrativas populares e patrimônio cultural imaterial
2.2 Material didático impresso e difusão cultural
2.3 O formato PDF e a geração programática de documentos
2.4 Bibliotecas Python para geração de PDF
2.5 Acessibilidade de documentos digitais
2.6 Trabalhos relacionados
3 METODOLOGIA
3.1 Classificação da pesquisa
3.2 Pergunta de pesquisa
3.3 Desenho da comparação
3.4 O acervo de teste e o modelo do folder
3.5 Protocolo de medição
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
6 CONCLUSÃO
REFERÊNCIAS
```

---

# 1. Introdução
**Prazo: 29/09/2026**

Cinco blocos de parágrafos, nesta ordem (é a sequência definida no `README.md`). Uma a duas páginas no total.

## 1.1 Contextualização (2 parágrafos)

**Pesquise sobre:**

- **narrativas populares, tradição oral e patrimônio cultural imaterial.** Comece pelas referências que já estão no [projeto.md](../projeto.md) — Bezerra (2026), Binda e Da Silva (2026), Pires (2025) — e procure a **Convenção da UNESCO para a Salvaguarda do Patrimônio Cultural Imaterial (2003)** e o **Decreto nº 3.551/2000**, que criou o registro de bens culturais de natureza imaterial no Brasil;
- **o risco concreto de perda desse patrimônio**: as narrativas vivem na memória de pessoas idosas, e desaparecem quando elas morrem. Esse é o argumento mais forte da sua Introdução, e ele já está escrito no documento do projeto;
- **as Humanidades Digitais** e o papel das plataformas digitais na preservação e difusão de acervos culturais (Reis, 2023; Soave e Da Silva Lemos, 2022, ambos já no projeto).

**Escreva sobre:** a importância das narrativas populares como forma de transmitir conhecimento, valores e identidade, e a ameaça real de que elas se percam. Em seguida apresente o projeto Narrativas como uma resposta a isso: uma plataforma digital que registra e organiza esse acervo.

**E então estreite para o seu assunto**, que é o ponto onde a maioria dos trabalhos erra: **preservar não basta, é preciso difundir**. Uma narrativa guardada em um banco de dados que ninguém lê está tão perdida quanto a que não foi registrada. É aí que entra o **material impresso**: o folder que um professor imprime e leva para a sala de aula alcança um público que talvez nunca entre no site.

## 1.2 Problemática (2 parágrafos)

**Pesquise sobre:**

- **o papel do material impresso na educação**, especialmente em escolas públicas e em regiões com acesso limitado à internet. Procure dados de conectividade em escolas brasileiras (pesquisa **TIC Educação**, do Cetic.br) — eles sustentam o argumento de que o PDF impresso ainda é necessário;
- **a geração automática de documentos**: por que gerar mil folders à mão é inviável e por que isso costuma ser feito por programa;
- **as diferenças entre bibliotecas de geração de PDF** e os problemas mais comuns — acentuação, fontes, imagens e dependências do sistema operacional.

**Escreva sobre:** o problema concreto. Os protótipos de tela do portal Narrativas já preveem os botões "Baixar PDF" e "Material Didático". Mas **a plataforma não tem nenhuma biblioteca de PDF escolhida**, e essa escolha não é trivial:

- há várias bibliotecas Python para isso, com formas de trabalhar **muito diferentes** entre si;
- elas se comportam de maneira diferente em coisas que importam muito em português — **acentuação** e **fontes**;
- algumas exigem **programas do sistema operacional** que nem sempre podem ser instalados;
- e o PDF gerado pode ou não ter **texto pesquisável**, o que decide se ele é acessível a quem usa leitor de tela.

Explique a consequência de escolher errado: a equipe descobre o problema **depois** de ter implementado, e refazer custa caro. E uma consequência mais grave: se o PDF sair com o texto quebrado ou sem texto selecionável, o material didático fica inutilizável para parte do público — justamente o oposto do que o projeto quer.

**Faça a ponte para o que ainda não se sabe:** não existe uma resposta pronta sobre qual biblioteca usar, porque a resposta depende do documento que se quer gerar. Um folder cultural, com imagem, texto longo em português, caixa com borda e rodapé repetido, exercita justamente os pontos em que essas bibliotecas se diferenciam. **É essa comparação, feita sobre um documento real do projeto, que o seu trabalho entrega.**

## 1.3 Caminho para a solução (1 a 2 parágrafos)

**Pesquise sobre:**

- **o formato PDF**: o que é, por que virou o padrão para documentos que precisam ser impressos igual em qualquer computador, e o fato de ser uma norma aberta (**ISO 32000**);
- **as bibliotecas Python que geram PDF**, e principalmente as **duas formas diferentes de fazer isso**:
  - **desenhar por coordenadas** — o programa diz onde cada elemento fica na página (é assim na FPDF2);
  - **descrever o documento** e deixar a biblioteca encaixar — com blocos (ReportLab) ou com HTML e CSS (xhtml2pdf, WeasyPrint).

**Escreva sobre:** as alternativas existentes e essa diferença de abordagem, que é o eixo conceitual do seu artigo. Mostre que não é só "uma biblioteca ou outra": são **maneiras diferentes de pensar o documento**, com vantagens diferentes — controle milimétrico de um lado, facilidade de mudar o leiaute do outro.

Justifique o recorte: comparar **três bibliotecas** (mais uma quarta, cuja instalação foi testada), gerando **o mesmo folder**, a partir do **mesmo acervo**, na **mesma máquina**, e medindo fidelidade, tempo, tamanho, acentuação, imagens, acessibilidade e esforço de implementação.

Diga também o que o trabalho **não** faz: não trata de edição de PDF, de assinatura digital, de PDF/A para arquivamento de longo prazo nem de geração a partir de banco de dados. Isso vira trabalho futuro. **Recorte declarado é recorte defendido.**

## 1.4 Apresentação da solução (2 parágrafos)

**Escreva sobre:** o que foi feito. Concretamente: foi desenhado um **modelo de folder** em A4 com dez elementos definidos (faixa de identificação, título, dados da narrativa, imagem com legenda, texto justificado, caixa de palavras-chave, rodapé com a fonte bibliográfica e numeração de páginas); montado um **acervo de teste com dez narrativas populares em domínio público**, de tamanhos variados; e esse mesmo folder foi implementado em **três bibliotecas Python**.

Explique **por que o mesmo folder nas três**: porque assim a única coisa que muda entre elas é a biblioteca. Se cada uma gerasse um folder diferente, não daria para saber se a diferença veio da ferramenta ou do programador. **Essa é a decisão de método mais importante do trabalho** e merece uma frase de destaque já aqui.

Diga como foi avaliado: uma **lista de conferência de dez itens**, escrita **antes** de gerar qualquer folder e pontuada de 0 a 2 por item, com uma **segunda avaliação independente** feita pelo orientador; e medições automáticas de tempo (com repetições e mediana), tamanho do arquivo, número de páginas, extração de texto e verificação de palavras acentuadas.

Registre que **todas as narrativas são de domínio público** e que **as imagens têm licença livre**, com a origem de cada uma documentada — e que **não há dados de pessoas envolvidos**, nem participantes de pesquisa, o que dispensa submissão ao Comitê de Ética em Pesquisa.

## 1.5 Vínculo com o projeto e escopo (1 parágrafo)

**Escreva sobre:** o vínculo com o projeto Narrativas, do IFRN, que é um projeto institucional com equipe própria. Explique que:

- o seu trabalho foi feito **em separado da plataforma**, sem alterar o código dela — o que era necessário porque o cadastro de narrativas ainda não existe no sistema;
- o seu escopo é **apenas a comparação das bibliotecas e a recomendação**;
- a **implementação do botão "Baixar PDF" na plataforma é trabalho futuro**, a cargo da equipe de desenvolvimento, que usará a sua recomendação como insumo.

Feche a Introdução com um parágrafo curto dizendo como o texto está organizado.

---

# 2. Objetivo Geral
**Prazo: 29/09/2026 (junto com a Introdução)**

Uma **única frase**, com **uma única ação principal**, coerente com o título e com a conclusão. Modelo do `README.md`:

> "O objetivo principal do presente trabalho consiste no [ação] de [o quê] para [finalidade]."

**Direcionamentos:**

- **o verbo principal não é "desenvolver".** Este é o erro mais provável no seu caso, porque você vai passar seis semanas programando. Mas os programas são o **meio**; o que o trabalho entrega é a **resposta medida**. Verbos adequados: **comparar**, **avaliar**, **analisar**;
- nomeie **o que** é comparado (bibliotecas Python de geração de PDF), **para que** (gerar folders de narrativas populares) e **em que dimensão** (fidelidade ao leiaute, desempenho e acessibilidade). Sem a terceira parte, o objetivo fica vago demais;
- **não** empilhe ações. "Desenvolver, comparar, avaliar e implantar" são quatro objetivos, não um;
- **não** prometa o que não vai medir. Se você não vai testar impressão em papel de verdade, não fale em "qualidade de impressão".

**Teste antes de enviar:** leia o objetivo geral e, em seguida, a primeira frase da sua Conclusão. Se as duas não estiverem falando exatamente da mesma coisa, uma das duas está errada.

---

# 3. Objetivos Específicos
**Prazo: 24/11/2026 (com o Resumo e o Título)**

Ficam para o final de propósito: precisam descrever o que foi **realmente alcançado**. Até lá, trabalhe com uma versão provisória e vá ajustando.

**Direcionamentos:**

- de 4 a 5 itens, verbo no infinitivo, minúscula no início, ponto e vírgula no fim de cada um e ponto no último;
- na **mesma ordem** das etapas da Metodologia e das subseções dos Resultados;
- cada um **verificável**: na Conclusão você terá de mostrar, com número, que foi atingido;
- "instalar a biblioteca X" não é objetivo específico — é tarefa.

**Esqueleto do que cada item deve cobrir** (redija com as suas palavras ao fechar o texto):

1. revisar a literatura sobre patrimônio cultural imaterial, material didático impresso e geração programática de documentos;
2. definir um modelo de folder para as narrativas do projeto e uma lista de critérios para avaliá-lo;
3. implementar o mesmo folder em três bibliotecas Python, sobre um acervo comum de narrativas de domínio público;
4. medir e comparar fidelidade ao leiaute, tempo de geração, tamanho do arquivo, tratamento de acentuação e imagens, e acessibilidade do PDF;
5. recomendar, com base nos resultados, a biblioteca mais adequada à plataforma Narrativas.

---

# 4. Referencial Teórico
**Prazo: 13/10/2026**

**Explicação em vídeo (assista antes de começar):** https://youtu.be/8Qztq1Q5vb0

Comece a procurar referências **na primeira semana**. E entenda uma coisa sobre o seu referencial: ele tem **duas metades**, e as duas são necessárias:

- a metade **cultural** (narrativas, patrimônio, material didático), que justifica *por que* o trabalho importa;
- a metade **técnica** (PDF, bibliotecas, acessibilidade), que sustenta *o que* você mediu.

Muitos trabalhos técnicos esquecem a primeira, e ficam parecendo manual. Muitos trabalhos culturais esquecem a segunda, e ficam sem base para os resultados. **O seu precisa das duas.**

Vá do geral para o específico e escreva **apenas sobre o que reaparece** na Metodologia ou nos Resultados.

## 4.1 Narrativas populares e patrimônio cultural imaterial

**Pesquise:** as referências do [projeto.md](../projeto.md) (Bezerra, 2026; Binda e Da Silva, 2026; Dos Santos Fernandes e Martins, 2026; Pires, 2025); a **Convenção da UNESCO de 2003** sobre patrimônio imaterial; o **Decreto nº 3.551/2000**; e trabalhos sobre folclore e cultura popular brasileira. Para o Rio Grande do Norte especificamente, procure no repositório do IFRN e da UFRN.

**Escreva:** o que é patrimônio cultural imaterial e por que narrativas orais fazem parte dele; por que esse patrimônio é frágil; e o que se entende por salvaguarda. **Seja breve e vá direto ao ponto** — uma página é suficiente. O erro comum aqui é escrever cinco páginas sobre cultura popular e esquecer que o trabalho é sobre geração de PDF.

Termine amarrando ao seu tema: **registrar não é suficiente, é preciso difundir**, e o material impresso é uma das formas de difusão.

## 4.2 Material didático impresso e difusão cultural

**Pesquise:** o papel do material impresso na educação básica; o uso de temas da cultura local em sala de aula (procure pela **BNCC** e pelos temas de cultura e diversidade); e dados sobre acesso à internet nas escolas brasileiras (**TIC Educação**, do Cetic.br).

**Escreva:** por que, mesmo com tudo disponível na internet, o material impresso continua tendo função — principalmente onde a conexão é ruim ou os equipamentos são poucos. Esse é o argumento que justifica o seu trabalho existir, e ele precisa estar fundamentado com dado, não com opinião.

Explique também o que é um **folder** enquanto peça de comunicação: documento curto, visual, feito para circular e ser lido rapidamente. Isso justifica as escolhas do seu modelo (imagem grande, texto justificado, palavras-chave em destaque).

## 4.3 O formato PDF e a geração programática de documentos

**Pesquise:** o que é o **PDF** (*Portable Document Format*), a norma **ISO 32000**, e por que ele se tornou o padrão para documentos que precisam ser impressos igual em qualquer lugar. Procure também por **codificação de caracteres** — **UTF-8**, **Latin-1** (ISO-8859-1) e **Unicode** —, e por **fontes embutidas** em PDF.

**Escreva:** o que é o PDF e qual problema ele resolve (o documento sai igual em qualquer computador e impressora). Depois, dois conceitos que você vai usar o artigo inteiro:

- **fontes e codificação de caracteres.** Um PDF guarda texto, e o texto precisa de uma fonte que contenha os caracteres usados. Fontes antigas cobrem só um conjunto limitado de caracteres (Latin-1), que **inclui** os acentos do português mas **não inclui** coisas como travessão e reticências tipográficas. É por isso que uma biblioteca pode "engolir" um caractere. **Você viveu esse problema na Sprint 3 — descreva o conceito aqui e o caso concreto nos Resultados**;
- **texto real × imagem de texto.** Um PDF pode conter o texto de verdade (dá para selecionar, copiar e pesquisar) ou apenas o desenho dele. Isso decide se o documento é acessível.

Depois, a **geração programática**: por que gerar documentos por programa, em vez de fazer à mão, quando o conteúdo vem de um acervo que cresce.

## 4.4 Bibliotecas Python para geração de PDF

**Pesquise:** a documentação oficial da **FPDF2**, da **ReportLab**, da **xhtml2pdf** e da **WeasyPrint**. Procure também por comparações já publicadas entre elas.

**Escreva:** apresente cada uma em um parágrafo — o que é, como funciona, de onde veio — e, principalmente, **organize-as pelas duas formas de trabalhar**:

- **por coordenadas:** o programa diz a posição de cada elemento (FPDF2);
- **por descrição:** o programa descreve o conteúdo e a biblioteca encaixa na página, seja com blocos (ReportLab) ou com HTML e CSS (xhtml2pdf, WeasyPrint).

**Essa classificação é o eixo do seu artigo.** Ela explica quase todos os resultados que você vai apresentar: por que uma exige mais linhas de código, por que outra lida melhor com texto longo, por que outra é mais fácil de mudar.

Mencione também a questão das **dependências**: algumas bibliotecas são Python puro e instalam com um comando; outras precisam de programas do sistema operacional. **Fundamente isso aqui**, porque é o que explica o caso da WeasyPrint nos seus Resultados.

> **Atenção:** a documentação oficial serve para **descrever a ferramenta**. Para **fundamentar conceito** (o que é PDF, o que é Unicode, o que é acessibilidade), use livro ou artigo, não a documentação.

## 4.5 Acessibilidade de documentos digitais

**Pesquise:** **acessibilidade digital**, leitores de tela, e o que torna um PDF acessível. Procure pela **Lei Brasileira de Inclusão (Lei nº 13.146/2015)**, pelas **WCAG** e pelo modelo **eMAG**, do governo brasileiro. Procure também por **PDF/UA**, que é a norma de acessibilidade específica para PDF.

**Escreva:** por que um PDF pode ser inacessível, e o que é o mínimo para ele não ser: o texto precisa existir como texto (e não como desenho), para que o leitor de tela consiga ler.

**Amarre ao seu trabalho:** o projeto Narrativas quer democratizar o acesso ao patrimônio cultural. Um material didático que uma pessoa cega não consegue ler contraria esse objetivo. **É por isso que "texto pesquisável" é um dos seus critérios de comparação**, e não um detalhe técnico.

Seja honesto sobre o alcance: você verificou apenas se o texto é extraível, que é o requisito mais básico. Acessibilidade completa em PDF envolve muito mais (estrutura de marcação, ordem de leitura, texto alternativo das imagens). **Diga isso** — e coloque a verificação completa como trabalho futuro.

## 4.6 Trabalhos relacionados

**Pesquise:** trabalhos que **comparem bibliotecas ou ferramentas** de geração de documentos; trabalhos sobre **geração automática de material didático**; e trabalhos sobre **acervos digitais de cultura popular** que produzam material para download. Onde procurar: **SBC OpenLib** (`sol.sbc.org.br`), **BDTD**, repositórios de institutos federais, **Google Acadêmico** e **SciELO**.

**Escreva:** de **3 a 4 trabalhos**, um parágrafo cada, dizendo: o que foi comparado, **como foi avaliado** (esta é a informação que mais importa para você) e qual a limitação. Feche com um **quadro comparativo** entre eles e o seu trabalho, com colunas como: o que foi comparado, quantas ferramentas, critérios usados, havia critério definido antes?, houve segundo avaliador?, o domínio de aplicação.

**Esse quadro é o argumento de originalidade do seu artigo.** Preste atenção a um ponto provável: comparações de bibliotecas de PDF costumam aparecer em blogs e tutoriais, com opinião e sem medição. Se for esse o caso do que você encontrar, **diga isso explicitamente** — a sua contribuição passa a ser justamente fazer a comparação **com método**: critério escrito antes, segundo avaliador, medições repetidas e um documento real de um projeto real.

**E se você não achar quase nada?** Não invente. Escreva que a literatura acadêmica sobre o assunto é escassa, que o material disponível é majoritariamente técnico e não avaliado, e **aumente o alcance da busca** — trabalhos sobre comparação de bibliotecas em geral, ou sobre geração de relatórios. Conversar com o orientador nessa hora é o caminho.

## Regras que valem para o referencial inteiro

- **Toda afirmação técnica precisa de referência.**
- **Não empilhe citações.** Explique com as suas palavras, relacione os autores e amarre ao seu trabalho.
- **Nada de blog, Stack Overflow ou site sem autoria** nas Referências. Você vai usar muito esse tipo de material para resolver problema de programação — isso é normal e esperado —, mas ele não entra na lista de referências.
- **Nunca cite uma referência que você não leu.** Ferramentas de inteligência artificial inventam referências com naturalidade; se você não abriu o texto, ele não entra.
- Meta para este trabalho: **14 a 20 referências**, bem divididas entre a parte cultural e a parte técnica.

---

# 5. Metodologia
**Prazo: 20/10/2026**

Como o trabalho foi conduzido. Verbos no passado e linguagem impessoal. Duas páginas.

**Pasta com metodologias prontas para consulta:** https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

## 5.1 Classificação da pesquisa

**Pesquise:** Gil (2017) e Prodanov e Freitas (2013) — referências completas no `README.md`. Leia os capítulos de classificação antes de escrever.

**Escreva:** a classificação pelos quatro critérios, **justificando cada uma** com uma frase que ligue o critério ao seu trabalho. Enquadramento mais provável:

- **Natureza:** aplicada — gera conhecimento para uma decisão concreta da equipe do projeto Narrativas;
- **Objetivos:** exploratória e descritiva — descreve e compara o comportamento das bibliotecas em uma situação ainda não estudada nesse contexto;
- **Abordagem:** quantitativa, com apoio qualitativo — as notas, os tempos e os tamanhos são números, e a análise das dificuldades de implementação é qualitativa;
- **Procedimentos:** **experimental**, combinada com pesquisa bibliográfica. Você muda uma coisa (a biblioteca), mantém tudo o mais igual (o mesmo folder, o mesmo acervo, a mesma máquina) e observa o efeito.

Aproveite para **dizer o que variou e o que foi mantido fixo**: variou a biblioteca; foram mantidos o modelo do folder, o acervo, a máquina, a lista de conferência e o protocolo de medição.

## 5.2 Pergunta de pesquisa

Enuncie a pergunta principal em uma frase e, abaixo dela, **três perguntas menores** que os Resultados vão responder uma a uma. Sugestões (reescreva com as suas palavras):

- qual biblioteca reproduz com mais fidelidade o modelo de folder definido?
- como as bibliotecas se comportam em relação a desempenho e tamanho do arquivo, e isso muda conforme o tamanho da narrativa?
- todas geram um PDF com texto pesquisável e com a acentuação correta?
- e a pergunta prática, que fecha o trabalho: **qual delas o projeto Narrativas deve adotar, e em que condição essa resposta mudaria?**

Responda todas na Conclusão, **com recomendação explícita**. Trabalho aplicado que não recomenda nada desperdiça o próprio resultado.

## 5.3 Desenho da comparação

**Escreva** — e este é o coração da sua Metodologia:

- **o mesmo folder nas três bibliotecas**, com a justificativa: assim a única variável é a biblioteca. Se os folders fossem diferentes, não daria para saber se a diferença veio da ferramenta ou de quem programou. Dedique um parágrafo inteiro a isso;
- **o mesmo acervo** nas três, e as mesmas dez narrativas;
- **a mesma máquina, na mesma sessão de medição**;
- **a lista de conferência foi escrita ANTES** de qualquer folder ser gerado. Explique por quê: se o critério fosse escrito depois, ele acabaria favorecendo a biblioteca de que o autor mais gostou. Isso é uma proteção contra viés, e declarar que você a tomou vale muito;
- **a segunda avaliação pelo orientador**, feita de forma independente, e o que ela mostrou (em quantos dos 30 itens houve concordância).

**Justifique também a ausência de banco de dados.** O objeto do trabalho é a geração do PDF; as narrativas foram armazenadas em arquivos de texto porque um banco acrescentaria complexidade sem alterar nenhum resultado — as bibliotecas receberiam os mesmos dados de qualquer forma. **Escreva isso com essas palavras**: é uma decisão de método consciente, não uma limitação por desconhecimento.

Uma **figura** com o desenho do experimento (o acervo → o programa de cada biblioteca → os PDFs → as medições e a avaliação) ajuda muito o leitor. Use o `app.diagrams.net`, que funciona no navegador.

## 5.4 O acervo de teste e o modelo do folder

**Escreva:**

- **de onde vieram as narrativas**: as obras, os autores, os anos, e **por que estão em domínio público** (Lei nº 9.610/1998). Informe quantas são e a variação de tamanho entre elas, e **explique por que a variação importa**: as narrativas longas são as que fazem o folder passar de página, que é onde as bibliotecas mais se diferenciam;
- **de onde vieram as imagens** e qual a licença de cada uma;
- **o modelo do folder**: apresente a figura do modelo desenhado e descreva os dez elementos. Justifique as escolhas — por que A4, por que imagem grande, por que caixa de palavras-chave. Cada elemento foi escolhido porque exercita algo diferente nas bibliotecas; diga isso;
- **a lista de conferência e a escala de 0 a 2**, com o significado de cada nota.

## 5.5 Protocolo de medição

Transcreva o protocolo, **justificando cada escolha, não apenas declarando**:

- cada folder foi gerado **6 vezes**, e a primeira execução foi descartada — porque a primeira é sempre a mais lenta, já que o programa ainda está carregando coisas na memória (**aquecimento**);
- foi usada a **mediana**, e não a média, porque a mediana não é distorcida por uma medição atípica;
- a máquina estava **sem outros programas abertos**;
- o texto do PDF foi extraído com uma biblioteca específica (`pypdf`), e a acentuação foi verificada procurando palavras acentuadas conhecidas no texto extraído;
- o esforço de implementação foi medido pelo **número de linhas de código** de cada gerador, contadas sem linhas vazias e sem comentários — e, no caso da biblioteca que usa HTML, **somando também as linhas do arquivo HTML**, para a comparação ser justa.

**Cada justificativa dessas é uma frase que mostra domínio do método**, e é o que separa um artigo de um relato.

---

# 6. Materiais e Métodos
**Prazo: 27/10/2026**

Vale a analogia do `README.md`: **lista de ingredientes** mais **modo de preparo**. Esta seção é o que permite (ou impede) outra pessoa repetir o seu trabalho.

## 6.1 Materiais

Para **cada** item: **o que é** (uma ou duas frases), **para que foi usado** e **qual a versão**.

| Ferramenta | O que dizer além da versão |
|---|---|
| Python 3.x | Linguagem usada nos três geradores |
| **FPDF2** | Biblioteca de geração de PDF por coordenadas |
| **ReportLab** | Biblioteca de geração de PDF por blocos |
| **xhtml2pdf** | Biblioteca que converte HTML e CSS em PDF |
| **WeasyPrint** | Quarta biblioteca; **a instalação foi tentada e não foi concluída** (ver Resultados) |
| `pypdf` | Extração do texto dos PDFs gerados, para verificar acessibilidade e acentuação |
| `matplotlib` | Geração dos gráficos |
| Módulos `csv`, `os`, `time`, `statistics` | Já vêm com o Python: planilhas, arquivos e cronometragem |
| Git | Versionamento, em subpasta própria do repositório do projeto |

**Duas justificativas são obrigatórias:**

1. **Por que essas bibliotecas, e não outras.** O critério foi: serem gratuitas, serem usadas em projetos reais, e **poderem ser instaladas apenas com `pip`** — porque o ambiente disponível não permite instalar programas. Declare esse critério: ele é legítimo, é realista, e explica por que ferramentas que dependem de um programa externo (como as que usam o `wkhtmltopdf` ou um navegador) ficaram de fora;

2. **Por que arquivos de texto e não banco de dados**, conforme já explicado na Metodologia.

**Ambiente de execução — sem isto o artigo não é reproduzível.** Informe processador, memória RAM, sistema operacional e versão, versão do Python e a versão exata de cada biblioteca (o comando `pip list` mostra todas). Informe também a **data das medições**.

## 6.2 Métodos

**a) O acervo.** Quantas narrativas, de onde vieram, como foram organizadas nos arquivos. **Mostre a estrutura de um arquivo** como figura — ajuda muito o leitor a entender o que entra no gerador.

**b) O modelo do folder.** Apresente a figura do modelo e a tabela dos dez elementos.

**c) Os três geradores.** Um parágrafo curto por biblioteca, dizendo **como o folder foi construído nela**, com um trecho curto de código quando ele esclarecer. Seja preciso:

- **FPDF2:** o cabeçalho e o rodapé foram feitos sobrescrevendo os métodos próprios da biblioteca; o texto foi posicionado com `multi_cell`; **a fonte precisou ser trocada por uma fonte TrueType externa** — diga qual, e por quê;
- **ReportLab:** os elementos foram montados como uma lista de blocos e entregues ao documento, que cuidou da paginação; o cabeçalho e o rodapé foram desenhados por uma função chamada a cada página; **a caixa com borda precisou ser feita com uma tabela de uma célula**, porque não existe um elemento próprio para isso;
- **xhtml2pdf:** o folder foi descrito em um arquivo HTML com CSS, e os dados da narrativa foram substituídos no modelo antes da conversão; **o caminho das imagens precisou ser absoluto**, e parte do CSS moderno não é suportada — diga o que você tentou e não funcionou.

"Foi utilizado `multi_cell` com alinhamento justificado" é informação reproduzível; "o texto foi formatado adequadamente" não é.

**d) As medições automáticas.** O programa que gera cada folder repetidamente, cronometra, mede o tamanho do arquivo, conta as páginas, extrai o texto e verifica as palavras acentuadas, gravando uma linha por combinação de narrativa e biblioteca.

**e) A avaliação da fidelidade.** Como foi feita: os PDFs da mesma narrativa abertos lado a lado com o modelo; a avaliação item por item (e não biblioteca por biblioteca, para manter a consistência); a justificativa escrita para toda nota diferente de 2; e a segunda avaliação independente.

---

# 7. Resultados e Discussão
**Prazo: 10/11/2026**

A seção mais importante. Três a quatro páginas. Organize respondendo às **perguntas de pesquisa**, na mesma ordem.

> **Regra sem exceção:** toda figura, tabela ou quadro é **anunciado no texto antes** de aparecer e **explicado depois**. Nada de duas figuras seguidas sem texto entre elas.

## 7.1 Os folders gerados

Comece mostrando o produto. A melhor figura do seu artigo provavelmente é esta: **o mesmo folder, gerado pelas três bibliotecas, lado a lado**. Deixe que o leitor veja a diferença antes de você explicá-la.

Apresente também os números do acervo (dez narrativas, tamanhos, origem) e o modelo desenhado, se ainda não apareceu.

## 7.2 Fidelidade ao leiaute

Tabela com os dez itens nas linhas e as três bibliotecas nas colunas, com as notas e o total de cada uma. Acompanhe do gráfico de barras.

**Discuta item por item, mas com foco no que foi diferente.** Onde as três tiraram 2, uma frase resolve. Onde alguma tirou 0 ou 1, **explique o mecanismo**: não basta dizer "a caixa de palavras-chave ficou diferente"; diga *por que* — porque a biblioteca não tem um elemento pronto para isso, ou porque o CSS usado não é suportado.

**Apresente também a concordância com o segundo avaliador.** É um dado curto e ele dá credibilidade a toda a tabela. Se houve divergência em algum item, diga qual e por quê — divergência não é problema, é informação sobre quão subjetivo aquele item é.

## 7.3 Desempenho e tamanho do arquivo

Tabela com o tempo mediano, o desvio, o tamanho do arquivo e o número de páginas, por biblioteca. Acompanhe dos gráficos de barras (tempo e tamanho) e do gráfico de linhas (tempo por tamanho da narrativa).

**Discuta:**

- **qual é a mais rápida, e se a diferença tem importância prática.** Este é o ponto mais fácil de errar. Se todas gerarem o folder em menos de um segundo, **diga com todas as letras que o tempo não é critério de decisão neste caso** — o usuário não percebe a diferença. Essa é uma conclusão honesta e valiosa, e muito melhor do que fingir que 80 ms contra 200 ms muda alguma coisa para quem clica no botão;
- **o comportamento com narrativas maiores.** O gráfico de linhas responde a isso: alguma biblioteca fica desproporcionalmente lenta com texto longo? Se sim, aí o tempo volta a importar, porque o acervo vai crescer;
- **o tamanho do arquivo**, que importa para quem tem internet ruim — e o seu Referencial já explicou por que isso é relevante no público do projeto. Se uma biblioteca gerar arquivos muito maiores, investigue por quê (normalmente é o modo como a imagem é embutida) e diga.

## 7.4 Acentuação, imagens e acessibilidade

Estes três andam juntos, porque são os critérios de "o folder funciona de verdade?".

- **Acentuação:** apresente o resultado da verificação automática. **E apresente o caso concreto que você viveu**: a fonte padrão de uma das bibliotecas não cobria certos caracteres, o que exigiu registrar uma fonte externa. **Explique o mecanismo** usando o conceito de codificação de caracteres do seu Referencial — é a melhor amarração entre teoria e resultado que o seu artigo tem;
- **Imagens:** se alguma biblioteca deformou a imagem, mostre a figura. Uma imagem esticada é o tipo de erro que o leitor entende na hora;
- **Acessibilidade:** informe, para cada biblioteca, se o texto do PDF é extraível, e quantos caracteres foram extraídos em comparação com o original. Retome o argumento do Referencial: um material didático que o leitor de tela não lê contraria o objetivo de democratizar o acesso.

## 7.5 Facilidade de instalação e esforço de implementação

Tabela com: número de passos e de pacotes instalados, linhas de código do gerador (e do HTML, quando houver) e o tempo que você levou para escrever cada um.

**E aqui vai o resultado que dá caráter ao seu artigo: o caso da WeasyPrint.** Apresente-o com destaque, em parágrafo próprio:

- o que você tentou fazer, na ordem;
- a mensagem de erro exata (vale como figura);
- o motivo: a biblioteca depende de programas do sistema operacional que não vêm pelo `pip` e exigem instalador;
- **a consequência prática para o projeto**: em um ambiente Windows sem privilégios de administração — que é exatamente o caso dos laboratórios do instituto —, essa biblioteca não é uma opção viável, **por mais bem avaliada que seja tecnicamente em outros contextos**.

Seja preciso e justo na formulação: você **não** está dizendo que a WeasyPrint é ruim. Está dizendo que, **neste ambiente**, ela não pôde ser usada. A diferença entre as duas afirmações é grande, e escrever a segunda mostra maturidade.

**Sobre o tempo que você levou para programar cada uma:** apresente o número, mas **declare a limitação junto** — a ordem em que você implementou influencia o resultado, porque na terceira biblioteca você já sabia exatamente o que fazer. Reconhecer isso vale mais do que esconder.

## 7.6 Quadro comparativo e recomendação

O quadro final, com uma linha por critério e uma coluna por biblioteca, incluindo a WeasyPrint com "não avaliado" e o motivo.

**Este quadro é a contribuição prática do seu trabalho** — é o que a equipe do Narrativas vai olhar para decidir. Se o artigo tiver uma única figura memorável, que seja esta.

Depois dele, **a recomendação**, em um parágrafo, com três partes:

1. **qual biblioteca**, com o número que sustenta a escolha;
2. **em que condição a resposta mudaria** — por exemplo, se a equipe precisar mudar o leiaute com frequência e tiver quem saiba CSS;
3. **o que ainda precisa ser verificado** antes da implementação definitiva.

Não fuja da recomendação. Um trabalho aplicado que termina em "cada uma tem suas vantagens" desperdiça tudo o que mediu.

## 7.7 Limitações do trabalho

Subseção curta e honesta. Quatro pontos bastam:

- **um único modelo de folder foi testado.** Outro leiaute — com duas colunas, ou com muitas imagens — poderia mudar a ordem das bibliotecas;
- **a avaliação de fidelidade envolve julgamento**, ainda que com critério escrito antes e com um segundo avaliador;
- **o acervo é pequeno** (dez narrativas) e as medições foram feitas em uma única máquina;
- **o tempo de implementação sofre efeito da ordem** em que as bibliotecas foram programadas.

Note que várias dessas limitações são atenuadas pelo fato de o estudo ser **comparativo**: a mesma limitação incide sobre as três. Diga isso — é um bom argumento, desde que você não o use para varrer tudo para baixo do tapete.

---

# 8. Conclusão
**Prazo: 17/11/2026**

Curta e direta. Nada de resultado, conceito ou citação que não tenha aparecido antes.

**Escreva, nesta ordem:**

1. **Retomada do problema e do objetivo geral**, afirmando que foi alcançado **com o motivo e com número**: "[...] uma vez que a comparação das três bibliotecas, sobre um mesmo modelo de folder e um acervo de dez narrativas, resultou em X, Y e Z pontos de fidelidade ao leiaute."

2. **Um comentário por objetivo específico**, na mesma ordem, cada um apontando o resultado que o comprova.

3. **Resposta direta a cada pergunta de pesquisa** da Seção 5.2. Uma ou duas frases cada. E responda mesmo à última: **recomende uma biblioteca** para o projeto Narrativas.

4. **Contribuições:** um modelo de folder para as narrativas do projeto, com critérios de avaliação documentados; a comparação medida de três bibliotecas sobre um documento real, com método declarado; a constatação de que uma quarta biblioteca é inviável no ambiente dos laboratórios do instituto; e três programas geradores com código disponível, que a equipe pode reaproveitar.

5. **Limitações e dificuldades:** retome brevemente as limitações e acrescente as dificuldades reais do desenvolvimento — a questão das fontes e da acentuação, o caminho das imagens, as diferenças de CSS suportado, a tentativa frustrada de instalação. **É aqui que o `docs/diario.md` se paga**: se você escreveu as três linhas toda semana, este parágrafo se escreve sozinho.

6. **Trabalhos futuros**, concretos e ligados ao que você encontrou:
   - implementar o botão "Baixar PDF" na plataforma Narrativas com a biblioteca recomendada (principal);
   - gerar o folder a partir do banco de dados da plataforma, quando o cadastro de narrativas existir;
   - avaliar a acessibilidade completa do PDF, conforme a norma PDF/UA, e não apenas a extração do texto;
   - testar leiautes mais complexos, com duas colunas e múltiplas imagens;
   - avaliar a impressão física dos folders, com papel e cores reais;
   - produzir uma versão "Material Didático", com atividades pedagógicas, como já previsto nos protótipos da plataforma.

**Não escreva:** que "a biblioteca X é a melhor" sem dizer em qual critério, sobre qual documento e em que ambiente. E não generalize para "geração de PDF em Python" o que você mediu com um folder, dez narrativas e uma máquina.

---

# 9. Resumo, Título e revisão final
**Prazo: 24/11/2026**

## 9.1 Resumo

Escrito **por último**, depois do texto aprovado. Parágrafo único, 150 a 500 palavras, impessoal, sem citações, sem siglas pouco conhecidas e sem menção a figuras ou tabelas (NBR 6028:2021).

Uma ou duas frases para cada item:

1. **contexto e problema:** a difusão de narrativas populares em material impresso e a ausência de uma escolha técnica para gerar esse material;
2. **objetivo:** o que o trabalho se propôs a comparar;
3. **método:** um modelo de folder, três bibliotecas Python, um acervo de dez narrativas de domínio público, lista de critérios definida previamente e medições repetidas;
4. **resultados:** os números principais — a nota de fidelidade de cada biblioteca, a diferença de tempo e o caso da biblioteca que não pôde ser instalada;
5. **conclusão:** a recomendação e o encaminhamento (a implementação na plataforma como trabalho futuro).

**Coloque números no resumo.** Resumo sem número é resumo fraco — é ele que faz o avaliador decidir se lê o resto.

O **Abstract** é a versão em inglês. Termos técnicos têm forma consagrada em inglês (*layout fidelity*, *rendering*, *accessibility*, *open source*); use-as, e não a tradução literal. Não entregue tradução automática sem revisão.

**Palavras-chave** (3 a 5), separadas por ponto e vírgula. Campo semântico: geração de documentos; PDF; bibliotecas Python; patrimônio cultural imaterial; material didático. Escolha termos pelos quais alguém **procuraria** o seu trabalho.

## 9.2 Título

**Última coisa a ser definida**, em acordo com o orientador. Deve indicar **o que foi feito** e **em que contexto**, e ser coerente com o objetivo geral.

A sugestão que está em `tematicas.md` é um bom ponto de partida:

> *Geração automatizada de folders em PDF a partir de narrativas culturais: um comparativo entre bibliotecas Python.*

Repare que ela tem as três partes de um bom título: a ação (geração automatizada), o contexto (narrativas culturais) e o recorte (comparativo entre bibliotecas). **Ajuste-a com o orientador** para refletir o que o trabalho realmente entregou — se a fidelidade ao leiaute foi o critério decisivo, por exemplo, isso pode aparecer no título. Evite títulos genéricos ("Gerador de PDF em Python") e evite prometer mais do que o artigo mede.

## 9.3 Revisão final — checklist

Além do checklist do `README.md`:

- [ ] O objetivo geral, os objetivos específicos, as perguntas de pesquisa, as subseções de Resultados e os parágrafos da Conclusão estão na mesma ordem e falando das mesmas coisas?
- [ ] Todos os números citados no Resumo, nos Resultados e na Conclusão são **exatamente** os mesmos? (Erro mais comum: refazer a medição e esquecer de atualizar o resumo.)
- [ ] Está escrito que a lista de conferência foi definida **antes** de gerar os folders?
- [ ] A segunda avaliação, feita pelo orientador, está descrita e o resultado apresentado?
- [ ] Está declarado por que não foi usado banco de dados?
- [ ] O caso da biblioteca que não pôde ser instalada está apresentado **como resultado**, e formulado de modo justo (não é "a biblioteca é ruim", é "neste ambiente não foi possível")?
- [ ] Toda tabela e figura é citada no texto antes de aparecer e explicada depois?
- [ ] Todas as tabelas e figuras têm identificação em cima, centralizada, e fonte embaixo?
- [ ] Os gráficos informam unidade e, se o eixo não começa em zero, o aviso na legenda?
- [ ] A origem das narrativas está informada, com a justificativa do domínio público?
- [ ] A licença das imagens está informada?
- [ ] O ambiente de execução está completo (processador, memória, sistema operacional, versões, data da medição)?
- [ ] Há pelo menos um resultado contra a sua própria expectativa, ou uma dificuldade sua, relatados honestamente?
- [ ] As limitações estão declaradas?
- [ ] As siglas (PDF, CSS, HTML, UTF-8, LGPD, BNCC) foram escritas por extenso na primeira vez que aparecem?
- [ ] A numeração das seções está sem ponto após o número?
- [ ] O texto está impessoal e no passado?
- [ ] O link do repositório está no texto, e o orientador autorizou divulgar esse endereço?
- [ ] Todos os comentários do orientador foram respondidos e resolvidos?
- [ ] A versão final foi nomeada no histórico do Drive?

---

## Referências mínimas a garantir

- **2 obras de metodologia científica** — Gil (2017) e Prodanov e Freitas (2013), já no `README.md`;
- **3 a 4 obras sobre patrimônio cultural imaterial e narrativas populares** (Seção 4.1) — várias já estão no [projeto.md](../projeto.md), aproveite-as;
- **2 obras sobre material didático impresso e difusão cultural** (Seção 4.2), com pelo menos uma fonte de dados sobre conectividade nas escolas;
- **2 a 3 fontes sobre o formato PDF e codificação de caracteres** (Seção 4.3);
- **a documentação oficial das quatro bibliotecas** (Seção 4.4) — serve para descrever a ferramenta, não para fundamentar conceito;
- **2 fontes sobre acessibilidade digital** (Seção 4.5), incluindo a Lei nº 13.146/2015;
- **3 a 4 trabalhos relacionados** (Seção 4.6);
- **a legislação citada** — Lei nº 9.610/1998 (direitos autorais, que justifica o uso das narrativas) e Lei nº 13.146/2015.

Registre a referência completa de **tudo** o que ler, na seção de Referências do documento do Drive, desde o primeiro dia. O Zotero e o Mendeley (ambos gratuitos) ajudam a montar, mas confira cada entrada contra a NBR 6023:2018 antes de entregar: esses programas erram com frequência.
