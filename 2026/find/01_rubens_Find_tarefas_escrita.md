# Plano de escrita do TCC – Rubens (Tecnologia em Sistemas para Internet)

**Projeto pai:** FIND – Desenvolvimento da Plataforma e Aplicativo Móvel para Gestão de Objetos Perdidos e Encontrados (ver `.llm/Find/projeto.md`).

**Temática:** Banco de dados do FIND: modelagem, criação e utilização como base comum das três aplicações (web, *mobile* e IoT).

**Repositórios que serão descritos no trabalho:**

- Projeto Web (back-end, API, painel web e endpoint IoT): https://github.com/gabryellgs/projeto-find
- Projeto Mobile: https://github.com/gabryellgs/find-app

**Base de estilo e de normas ABNT:** o arquivo `README.md` deste repositório. Tudo o que está lá vale aqui. Este documento **não repete** as regras da ABNT; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copie estas frases para o TCC. Elas dizem sobre o que é cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você leu.

> **Este trabalho descreve o que foi feito.** Não é preciso alterar nada no FIND. O seu papel é explicar, com fundamentação, **como** o banco de dados foi modelado, criado e usado, **por que** cada decisão foi tomada e **o que** cada decisão custou. Onde houver algo que você faria diferente hoje, isso entra na discussão e nos trabalhos futuros, não em uma mudança no código.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do TCC será **criado e compartilhado pelo coordenador em uma pasta do Google Drive**. Você não cria arquivo novo nem trabalha em cópia local.

Como trabalhar nele:

- **Escreva sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico do Drive é o que permite ao orientador ver o que mudou de uma semana para outra.
- **Não crie cópias** ("TCC v2", "TCC final", "TCC final revisado"). O Drive já guarda tudo em **Arquivo → Histórico de versões**.
- **Marque cada entrega no histórico.** Ao terminar uma seção, use **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 02/10`.
- **Avise por mensagem quando entregar.** O orientador não fica olhando o documento; ele precisa saber que há algo novo.
- **Comentário se responde, não se apaga nem se resolve.** Responda a cada comentário dizendo o que você fez. **Quem marca como resolvido é o orientador**, não você. Enquanto ele não marcar, o comentário continua aberto e a conversa segue ali mesmo: o orientador pode responder de novo, pedir outro ajuste, e você responde outra vez no mesmo fio.
- **Figuras e tabelas** vão dentro do documento, no lugar certo, com identificação em cima e fonte embaixo. Não mande imagem em anexo separado.
- **Crie a seção "Referências" no primeiro dia** e acrescente cada obra assim que ler.
- **Não dê acesso a terceiros** sem falar com o coordenador.

---

## Cronograma de entregas

Início da escrita: **25/09/2026**.

| # | Entrega | Prazo |
|---|---|---|
| 1 | Introdução e Objetivo Geral | **02/10/2026** |
| 2 | Referencial Teórico | **16/10/2026** |
| 3 | Metodologia | **23/10/2026** |
| 4 | Materiais e Métodos | **30/10/2026** |
| 5 | Resultados e Discussão | **13/11/2026** |
| 6 | Conclusão | **20/11/2026** |
| 7 | Resumo, Objetivos Específicos e Título | **27/11/2026** |

### O que fazer em paralelo com a escrita

Como o sistema já existe, o seu "desenvolvimento" é **levantar e organizar as evidências** que vão aparecer nos Resultados. Distribua assim:

| Semana | Levantamento no repositório | Entrega de escrita |
|---|---|---|
| 25/09 a 01/10 | Rodar o FIND localmente (SQLite e, se possível, Docker com MySQL); ler todos os `models.py` | Introdução e Objetivo Geral (02/10) |
| 02/10 a 15/10 | Desenhar o modelo conceitual e o diagrama do banco; montar o dicionário de dados | Referencial Teórico (16/10) |
| 16/10 a 22/10 | Montar a linha do tempo das migrações a partir do histórico do Git | Metodologia (23/10) |
| 23/10 a 29/10 | Mapear quais tabelas cada aplicação (web, *mobile*, IoT) lê e escreve | Materiais e Métodos (30/10) |
| 30/10 a 12/11 | Rodar os testes de modelos; reunir números (tabelas, campos, relacionamentos, índices, migrações) | Resultados (13/11) |
| 13/11 a 19/11 | Revisar figuras e quadros | Conclusão (20/11) |
| 20/11 a 26/11 | — | Resumo, Objetivos e Título (27/11) |

**Guarde tudo o que levantar** (diagramas, planilhas, saídas de comando) em uma pasta sua no Drive. É desse material que saem as figuras e os quadros.

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Texto pela metade dá para comentar; texto que não chega, não.
- Cada entrega é: seção escrita + versão nomeada no histórico + aviso ao orientador.
- Responda a **todos** os comentários da entrega anterior (e faça os ajustes pedidos) antes de avisar sobre a próxima.

---

## Que tipo de trabalho é este

O que você vai escrever é um **Trabalho de Conclusão de Curso (TCC)**, no modelo (*template*) disponibilizado na página do projeto e com as regras do `README.md`. O foco é o TCC: é ele que será avaliado pela banca.

Mas escreva desde já com **teor publicável**. Depois da defesa, você vai tirar trechos deste TCC para montar um **artigo** para evento ou revista — destinos que combinam com o tema são a **ERBD** (Escola Regional de Banco de Dados, da SBC), o **ENCOMPIF**, a **SECITEX** e a revista **HOLOS** do IFRN. Isso só funciona se o texto do TCC já tiver a qualidade de um artigo: cada afirmação com referência, método claro, resultados concretos e discussão. Um TCC bem escrito vira artigo com cortes; um TCC fraco precisa ser reescrito do zero.

"Fizemos um banco de dados" não é publicável. O que torna o seu trabalho publicável são quatro coisas:

1. **Um banco para três clientes muito diferentes.** Um navegador, um celular e um microcontrolador ESP32 leem e escrevem nos mesmos dados. Esse é o ponto que interessa ao leitor.
2. **Um modelo explicado, não só desenhado.** Guardar imagens dentro do banco, apagar em cascata ou manter o registro com `SET_NULL`: diga o que o FIND faz e por quê, com base no Referencial.
3. **A evolução do esquema.** O banco não nasceu pronto: foram 15 migrações entre janeiro e julho de 2026, incluindo uma reorganização em que os modelos mudaram de aplicação sem perder dados. Isso é um resultado.
4. **Números.** Quantas tabelas, relacionamentos, índices, migrações, testes de modelo. Números concretos dão credibilidade a um estudo de caso.

Uma dica prática para facilitar o artigo depois: escreva cada seção de forma que ela **se sustente sozinha** (sem depender de "como dito no capítulo anterior" a cada parágrafo) e mantenha figuras e quadros autoexplicativos. São eles que você vai reaproveitar.

Estrutura sugerida:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Bancos de dados relacionais e SGBD
2.2 Projeto de banco de dados: modelos conceitual, lógico e físico
2.3 Integridade referencial e restrições
2.4 Mapeamento objeto-relacional e migrações de esquema
2.5 Trabalhos relacionados
3 METODOLOGIA
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
6 CONCLUSÃO
REFERÊNCIAS
```

### Fronteira com os outros trabalhos do FIND

- **João Gabriel** escreve sobre a arquitetura e a integração entre as três aplicações (camadas, contrato da API). Você escreve sobre **os dados**: o que é guardado, como está organizado e como cada aplicação chega até ele. Quando falar da API, fale dela como **o caminho até o banco**, sem descrever a arquitetura em detalhe — cite o trabalho dele se já estiver disponível.
- **Gabryell** trata da correspondência automática entre itens. Você menciona os campos `image_hash`, `latitude` e `longitude` como parte do modelo, mas não explica os algoritmos de similaridade.

---

# 1. Introdução
**Prazo: 02/10/2026**

A Introdução é um **texto corrido, sem subcapítulos**. Não crie títulos como "1.1 Contextualização", "1.2 Problemática" etc. no TCC: os blocos abaixo servem só para organizar estas orientações e indicar a **ordem dos parágrafos** (é a sequência do `README.md`). No texto, um bloco deve levar ao seguinte naturalmente, sem títulos entre eles. Uma a duas páginas no total. As únicas subseções da Introdução são o Objetivo geral e os Objetivos específicos.

**Bloco 1 – Contextualização (1 a 2 parágrafos)**

**Pesquise sobre:**

- a perda de objetos em ambientes de grande circulação (escolas, empresas, eventos) e como ela costuma ser tratada: grupos de mensagem, caixas no balcão, cadernos de anotação. O próprio `projeto.md` cita Martins e Reis (2025), um TCC sobre sistema de achados e perdidos: comece por ele e procure outros;
- o papel dos **sistemas de informação** na organização de dados institucionais. Procure em livros de sistemas de informação (por exemplo, Laudon e Laudon) e no Google Acadêmico;
- o crescimento do uso de celulares e de dispositivos IoT. Procure **um número** (TIC Domicílios, do Cetic.br, é uma boa fonte brasileira).

**Fale sobre:** o problema cotidiano dos objetos perdidos e a informação que se perde junto com eles — ninguém sabe o que foi encontrado, onde está e com quem. Depois, estreite para o ponto do seu trabalho: qualquer solução digital para isso depende de **guardar bem essa informação**. O objeto, o local, a data, quem encontrou, quem reclamou, quem devolveu. Isso é um problema de banco de dados antes de ser um problema de tela.

**Bloco 2 – Problemática (1 a 2 parágrafos)**

**Pesquise sobre:**

- problemas de dados dispersos e redundantes: o que acontece quando a mesma informação existe em vários lugares (planilha, grupo de mensagem, caderno). Procure por "redundância de dados", "inconsistência de dados" e "anomalias de atualização" em livros de banco de dados (Elmasri e Navathe; Heuser);
- a dificuldade de manter **um único conjunto de dados** para aplicações com necessidades diferentes (navegador, celular, dispositivo embarcado).

**Fale sobre:** o problema em duas camadas.

- **No mundo real:** a informação sobre os objetos fica espalhada e sem histórico. Não se sabe se um item já foi devolvido, nem quem o entregou.
- **No sistema:** o FIND tem três portas de entrada para os mesmos dados. O painel web é usado pelo público e pelos bolsistas do balcão; o aplicativo móvel é usado por quem está andando pelo campus; e o leitor RFID com ESP32 identifica etiquetas no balcão. As três precisam ver **o mesmo item, no mesmo estado, ao mesmo tempo**. Se cada uma tivesse seus próprios dados, um item devolvido no balcão continuaria aparecendo como "achado" no celular.

**Feche mostrando a lacuna:** há muitos relatos de sistemas de achados e perdidos que descrevem telas e funcionalidades, mas poucos explicam **como os dados foram modelados** e **como um mesmo banco atende clientes web, móveis e IoT**. É esse espaço que o seu trabalho ocupa. Confirme essa lacuna na pesquisa do Referencial; se não se confirmar, ajuste a frase.

**Bloco 3 – Caminho para a solução (1 a 2 parágrafos)**

**Pesquise sobre:**

- as alternativas para guardar os dados de um sistema desse tipo: planilhas, banco de dados relacional, banco de dados não relacional (NoSQL), serviços prontos na nuvem (como o Firebase);
- as vantagens de um banco relacional quando os dados têm muitos relacionamentos (usuário, item, categoria, conversa, mensagem, log).

**Fale sobre:** as alternativas e por que o caminho escolhido foi um **banco de dados relacional centralizado**, acessado por todas as aplicações através de um único *back-end*. Explique a ideia central: nenhuma das três aplicações fala diretamente com o banco. A web usa o Django; o celular e o ESP32 passam pela API do mesmo Django. Assim, as regras sobre os dados ficam em um só lugar.

Mencione também que a escolha de usar o **ORM do Django** (mapeamento objeto-relacional) e suas **migrações** permitiu que o esquema do banco evoluísse junto com o sistema, e que o mesmo código funcionasse em dois bancos diferentes (SQLite no desenvolvimento e MySQL em produção).

**Bloco 4 – Apresentação da solução (1 a 2 parágrafos)**

**Fale sobre:** o que foi feito, de forma concreta:

- um banco de dados relacional com as entidades do domínio — usuário e perfil, item, categoria, conversa e mensagem, notificação, registro de ações dos bolsistas, dispositivo IoT e leitura RFID, além do armazenamento das imagens;
- criado e evoluído por meio de migrações do Django, entre janeiro e julho de 2026;
- em **MySQL 8.4** em produção (e no ambiente Docker) e **SQLite** no desenvolvimento local;
- com o **Redis** usado como apoio para o *chat* em tempo real, e não como banco de dados principal (diga isso claramente, para o leitor não confundir);
- servindo as três aplicações: painel web em Django, aplicativo em React Native/Expo e leitor RFID com ESP32.

Diga também como o trabalho foi feito: análise do código-fonte, dos arquivos de migração e do histórico de versões do repositório, reconstrução dos modelos conceitual e lógico e verificação por meio dos testes automatizados do projeto.

**Bloco 5 – Vínculo com o projeto e escopo (1 parágrafo)**

**Fale sobre:** o vínculo com o projeto de pesquisa FIND, do IFRN, iniciado para o Campus Canguaretama e ampliado para outras instituições, empresas e eventos. Deixe claro o **escopo**: este trabalho trata da camada de dados — modelagem, criação e uso. A arquitetura geral, a interface e os algoritmos de busca por imagem são tratados em outros trabalhos do projeto.

Feche a Introdução com um parágrafo curto dizendo como o texto está organizado.

---

# 2. Objetivo Geral
**Prazo: 02/10/2026 (junto com a Introdução)**

Uma **única frase**, com **uma única ação principal**. Modelo do `README.md`:

> "O objetivo principal do presente trabalho consiste [na ação] de [o quê] para [finalidade]."

**Direcionamentos:**

- a ação principal pode ser **descrever**, **apresentar** ou **analisar** a modelagem e a implementação do banco de dados do FIND. Evite "desenvolver": o TCC não entrega um banco novo, entrega a análise de um banco que já existe. Decida o verbo com o orientador;
- diga **o quê**: o banco de dados da plataforma FIND;
- diga **para quê**: servir de base comum às aplicações web, móvel e IoT de gestão de objetos perdidos e encontrados;
- **não** empilhe ações. "Modelar, criar, implementar e integrar" são quatro objetivos, não um;
- **não** prometa o que o trabalho não mostra (por exemplo, "melhorar o desempenho", se você não mediu desempenho).

**Confira antes de entregar:** leia o objetivo geral e, logo depois, a primeira frase da sua Conclusão. Se as duas não estiverem falando da mesma coisa, uma delas está errada.

---

# 3. Objetivos Específicos
**Prazo: 27/11/2026 (com o Resumo e o Título)**

Ficam para o fim de propósito: eles descrevem o que foi **realmente alcançado**. Até lá, use uma versão provisória.

**Direcionamentos:**

- 4 itens, verbo no infinitivo, minúscula no início, ponto e vírgula no fim de cada um e ponto no último;
- na **mesma ordem** das subseções dos Resultados;
- cada um **verificável**: na Conclusão você terá de apontar o resultado que o comprova;
- não confunda objetivo com tarefa. "Instalar o MySQL" não é objetivo específico.

**O que cada item deve cobrir** (redija com as suas palavras depois):

1. apresentar o modelo conceitual das entidades do domínio de achados e perdidos;
2. descrever o modelo lógico e físico implementado (tabelas, chaves, restrições e índices);
3. analisar a evolução do esquema ao longo das migrações;
4. descrever como as aplicações web, móvel e IoT utilizam o banco de dados.

---

# 4. Referencial Teórico
**Prazo: 16/10/2026**

**Vídeo com a explicação (assista antes de começar):** https://youtu.be/8Qztq1Q5vb0

Comece a procurar referências **na primeira semana**, não na véspera.

Regra prática: **tudo o que você vai usar nos Resultados precisa estar explicado aqui**. Se você vai mostrar um diagrama entidade-relacionamento, tem de ter explicado o que é entidade, atributo, relacionamento e cardinalidade. Se vai falar de `SET_NULL`, tem de ter explicado integridade referencial. Se um conceito não reaparece depois, não precisa estar aqui.

Escreva do assunto mais geral para o mais específico.

## 4.1 Bancos de dados relacionais e SGBD

**Pesquise:** "banco de dados relacional", "sistema gerenciador de banco de dados", "modelo relacional", "transação", "propriedades ACID". Livros básicos: Elmasri e Navathe (*Sistemas de Banco de Dados*), Silberschatz, Korth e Sudarshan (*Sistema de Banco de Dados*) e Heuser (*Projeto de Banco de Dados*). O artigo de Codd (1970) que criou o modelo relacional é uma referência clássica — cite-o se o ler.

**Escreva:** o que é um banco de dados e o que é um SGBD, e por que um SGBD é melhor do que guardar os dados em arquivos soltos ou planilhas (menos redundância, controle de acesso, integridade, acesso simultâneo). Explique o modelo relacional de forma simples: tabelas, linhas, colunas, chave primária e chave estrangeira.

Diferencie, em um parágrafo, o **SQLite** (banco em um único arquivo, sem servidor, ótimo para desenvolvimento) e o **MySQL** (banco cliente-servidor, feito para muitos acessos simultâneos). Você vai precisar dessa diferença para explicar por que o FIND usa os dois.

## 4.2 Projeto de banco de dados: modelos conceitual, lógico e físico

**Pesquise:** "modelagem de dados", "modelo entidade-relacionamento", "Peter Chen 1976", "cardinalidade", "normalização", "formas normais". Heuser é a referência mais didática em português para esta parte.

**Escreva:** as três etapas do projeto de um banco:

- **conceitual:** o que existe no mundo real e como se relaciona (entidades, atributos, relacionamentos), sem pensar em tecnologia;
- **lógico:** como isso vira tabelas, chaves e colunas;
- **físico:** como fica em um SGBD específico (tipos de dados, índices, tamanhos).

Explique **cardinalidade** (1:1, 1:N, N:N) com exemplos do próprio FIND: um usuário tem um perfil (1:1); um usuário cadastra vários itens (1:N). Explique o que é **normalização**, de forma breve, e para que serve (evitar repetição e anomalias).

Use a analogia que achar melhor, como a da planta de uma casa: o modelo conceitual é o esboço dos cômodos, o lógico é a planta com as medidas, e o físico é a obra feita com os materiais escolhidos.

## 4.3 Integridade referencial e restrições

**Pesquise:** "integridade referencial", "chave estrangeira", "*ON DELETE CASCADE*", "*ON DELETE SET NULL*", "restrição de unicidade", "índice".

**Escreva:** o que acontece com os dados relacionados quando um registro é apagado, e as opções que existem: apagar junto (*cascade*), deixar vazio (*set null*) ou impedir a exclusão. Isso é essencial para os Resultados, porque o FIND usa as duas primeiras de propósito, em lugares diferentes.

Explique também o que são **restrições de unicidade** (por exemplo, o *slug* do item e o *token* do dispositivo não podem se repetir) e o que é um **índice**, com a comparação do índice remissivo de um livro. Diga que índice acelera a busca, mas ocupa espaço e deixa as escritas um pouco mais lentas.

## 4.4 Mapeamento objeto-relacional e migrações de esquema

**Pesquise:** "mapeamento objeto-relacional", "ORM", "*object-relational impedance mismatch*", "padrão *Active Record*" (Fowler, *Patterns of Enterprise Application Architecture*), "migração de esquema", "*evolutionary database design*", "refatoração de banco de dados" (Ambler e Sadalage, *Refactoring Databases*). A documentação do Django sobre *models* e *migrations* serve para descrever a ferramenta.

**Escreva:** o que é um ORM e que problema resolve: o programador descreve as tabelas como classes em Python, e o ORM gera o SQL. Explique a vantagem que importa para o FIND: o mesmo código funciona em SQLite e em MySQL.

Depois explique o que são **migrações**: arquivos que registram, passo a passo, cada mudança feita no esquema do banco, para que qualquer cópia do sistema possa ser atualizada até a mesma versão. Diga por que isso é importante em um projeto em que várias pessoas trabalham e o banco muda ao longo dos meses. Mencione que as migrações também podem **inserir dados** (dados iniciais), não só criar tabelas.

## 4.5 Trabalhos relacionados

**Pesquise:** outros sistemas de achados e perdidos (TCCs, artigos, aplicativos acadêmicos) e trabalhos que descrevam a modelagem de dados de sistemas web com aplicativo móvel ou IoT. Busque em: SBC OpenLib (em especial anais da ERBD e do SBBD), BDTD, repositórios de institutos federais e universidades e Google Acadêmico. Termos: "sistema de achados e perdidos", "*lost and found system*", "modelagem de banco de dados estudo de caso", "banco de dados aplicação móvel IoT".

**Escreva:** de 3 a 5 trabalhos, um parágrafo cada, dizendo o que foi feito, **que banco de dados foi usado**, **se o modelo de dados foi apresentado** e quais as limitações.

Feche com um **quadro comparativo** entre esses trabalhos e o seu. Sugestão de colunas: SGBD utilizado, se apresenta o modelo de dados, quais clientes acessam os dados (web, *mobile*, IoT), se registra histórico de ações e se discute a evolução do esquema. **Esse quadro é a justificativa do seu trabalho.** Se encontrar um trabalho que já faz exatamente a mesma coisa, avise o orientador: em outubro ainda dá tempo de ajustar o recorte.

## Regras para o referencial inteiro

- **Toda afirmação técnica precisa de referência.**
- **Não empilhe citações.** O capítulo não pode ser "Fulano diz X. Beltrano diz Y". Explique com as suas palavras e ligue ao FIND.
- **Documentação oficial** (Django, MySQL, SQLite, Redis) serve para descrever a ferramenta, não para fundamentar conceito. Para conceito, use livro ou artigo.
- **Nada de blog, Stack Overflow ou site sem autoria** nas Referências.
- **Nunca cite o que você não leu.** Ferramentas de IA inventam referências com muita naturalidade. Confira cada uma das obras sugeridas aqui antes de usar.
- Meta para este trabalho: **12 a 18 referências**.

---

# 5. Metodologia
**Prazo: 23/10/2026**

Como o trabalho foi feito. Verbos no passado e linguagem impessoal ("foi realizado", "realizou-se"). Uma a duas páginas.

A Metodologia também é um **texto corrido, sem subcapítulos**. Não crie títulos como "3.1 Classificação da pesquisa" ou "3.2 Etapas" no TCC. Os blocos abaixo indicam a **ordem do conteúdo**; no texto, eles viram parágrafos em sequência.

**Pasta com metodologias prontas para consulta:** https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

**Bloco 1 – Classificação da pesquisa (1 a 2 parágrafos)**

**Pesquise:** Gil (2017) e Prodanov e Freitas (2013) — referências completas no `README.md`. Leia os capítulos de classificação antes de escrever.

**Escreva:** a classificação pelos quatro critérios, **justificando cada uma** com uma frase ligada ao seu trabalho, em prosa (não em lista). O enquadramento mais provável:

- **Natureza:** aplicada — o trabalho trata de um sistema real, em uso;
- **Objetivos:** descritiva — descreve como o banco foi modelado, criado e usado;
- **Abordagem:** qualitativa, com apoio de dados quantitativos descritivos (contagem de tabelas, relacionamentos, migrações e testes);
- **Procedimentos:** estudo de caso (o FIND), com pesquisa bibliográfica e **pesquisa documental** — os documentos analisados são o código-fonte, os arquivos de migração e o histórico de versões do Git.

Discuta o enquadramento com o orientador antes de fechar.

**Bloco 2 – Etapas do trabalho (1 a 2 parágrafos)**

Descreva, em ordem e em texto corrido, as etapas realizadas. Uma figura com o fluxo ajuda (use o draw.io, que é gratuito), mas ela **complementa** o texto, não o substitui:

1. pesquisa bibliográfica;
2. levantamento dos requisitos de dados a partir do projeto FIND (o que o sistema precisa guardar);
3. análise dos modelos do Django (`accounts`, `items`, `chats`, `iot`);
4. reconstrução do modelo conceitual e do modelo lógico;
5. análise da evolução do esquema pelas migrações e pelo histórico do Git;
6. mapeamento do uso do banco por cada aplicação (web, *mobile* e IoT);
7. verificação por meio dos testes automatizados dos modelos.

**Não confunda com Materiais e Métodos.** Aqui vai a ideia geral e a ordem; lá vão as ferramentas, as versões e os detalhes.

**Bloco 3 – Cuidados éticos (1 parágrafo curto)**

Feche a Metodologia declarando que **nenhum dado real de usuário** foi usado ou apresentado: os exemplos e as capturas de tela foram feitos em uma cópia local, com dados de teste, em conformidade com a LGPD (Lei nº 13.709/2018), e que **não houve participantes humanos**, o que dispensa submissão ao Comitê de Ética em Pesquisa.

---

# 6. Materiais e Métodos
**Prazo: 30/10/2026**

Vale a analogia do `README.md`: **lista de ingredientes** mais **modo de preparo**. Aqui entram as ferramentas usadas no FIND para o banco de dados e as que você usou para analisá-lo.

## 6.1 Materiais

Para **cada** item, escreva três coisas: **o que é** (uma ou duas frases, com referência), **para que foi usado** e **por que foi escolhido**. Escrever só "foi utilizado MySQL" não vale nada.

**Usados no FIND:**

| Ferramenta | O que dizer além da versão |
|---|---|
| Python 3.12 e Django 6.0 | *Framework* e ORM que definem os modelos e geram o SQL. Registre que as primeiras migrações foram geradas no Django 5.2 e as seguintes no 6.0 |
| MySQL 8.4 | Banco de produção e do ambiente Docker; conjunto de caracteres `utf8mb4` e modo `STRICT_TRANS_TABLES` (explique o que cada um garante) |
| SQLite | Banco do desenvolvimento local; explique por que é conveniente nessa etapa |
| Redis 7 | Camada de mensagens do *chat* em tempo real (Django Channels) em produção; **não** guarda os dados do sistema |
| Docker Compose | Sobe juntos o MySQL, o Redis e a aplicação, com as migrações executadas na inicialização |
| Render | Serviço onde o FIND está publicado; o sistema de arquivos dele é temporário, e isso explica a decisão sobre as imagens |
| Django REST Framework e Simple JWT | A API pela qual o aplicativo acessa os dados, com autenticação por *token* |
| React Native/Expo e AsyncStorage | O aplicativo não tem banco próprio; o AsyncStorage guarda só os *tokens* de acesso e os dados do usuário logado |
| ESP32 com leitor RFID | Envia o UID lido para a API; não guarda dados localmente |
| `pytest` | Testes automatizados, incluindo os testes dos modelos |

**Usados por você na análise:**

| Ferramenta | Uso |
|---|---|
| Git e GitHub | Histórico dos *commits* e das migrações |
| brModelo ou draw.io | Modelo conceitual |
| `django-extensions` (comando `graph_models`) e Graphviz | Diagrama do modelo lógico gerado direto dos modelos do Django |
| MySQL Workbench (engenharia reversa) ou dbdiagram.io | Ajustes e versão final do diagrama lógico/físico, se necessário |
| DB Browser for SQLite | Inspeção das tabelas no banco local |
| Planilha (Google Sheets) | Dicionário de dados e contagens |

**Gere o diagrama lógico com o `graph_models`.** A extensão `django-extensions` desenha o diagrama direto a partir dos modelos do Django, o que garante que a figura corresponde exatamente ao código. Faça tudo **apenas na sua cópia local**, sem enviar nada ao repositório:

1. instale o Graphviz no computador (https://graphviz.org/download/);
2. no ambiente virtual do FIND, instale `pip install django-extensions pydot`;
3. na sua cópia local, acrescente `'django_extensions'` em `INSTALLED_APPS` do `find/settings.py`;
4. gere o diagrama das aplicações que interessam: `python manage.py graph_models accounts items chats iot --pydot -g -o diagrama_find.png`;
5. ao terminar, desfaça a alteração do `settings.py` (`git checkout find/settings.py`) e confira com `git status` que nada ficou modificado.

Se o diagrama ficar poluído, gere um por aplicação ou use a opção `--include-models` para mostrar só as tabelas principais. Cite a ferramenta nos Materiais e informe na fonte da figura que ela foi gerada com o `graph_models`.

Informe também o ambiente onde você rodou o FIND para a análise: sistema operacional, versão do Python, e se usou SQLite ou Docker com MySQL.

## 6.2 Métodos

**a) Levantamento das entidades.** Diga que as entidades foram levantadas a partir dos arquivos `models.py` de cada aplicação do Django (`accounts`, `items`, `chats`, `iot`) e do modelo de usuário do próprio Django. Explique também que o arquivo `mainpage/models.py` apenas reexporta os modelos, por causa de uma reorganização feita em junho de 2026.

**b) Construção dos diagramas.** Como o modelo conceitual foi reconstruído a partir do código e como o diagrama lógico foi gerado a partir dos modelos com o comando `graph_models` da `django-extensions`.

**c) Linha do tempo das migrações.** Como a linha do tempo foi montada: a data que o Django grava no cabeçalho de cada migração ("*Generated by Django ... on ...*") e os *commits* que as introduziram (`git log -- '*/migrations/*'`).

**d) Mapeamento do uso por aplicação.** Como você descobriu o que cada aplicação lê e escreve: para o *mobile*, pelas chamadas em `src/services/api.js` e `src/services/auth.js` do `find-app`; para a IoT, pelo *firmware* em `esp32_firmware/main.ino` e pela view `iot/api/views.py`; para a web, pelas views de `mainpage` e pelos arquivos `urls.py` das APIs.

**e) Verificação.** Que os testes de modelo do projeto (`accounts`, `items`, `chats` e `iot`) foram executados com `pytest` e que o resultado foi registrado.

---

# 7. Resultados e Discussão
**Prazo: 13/11/2026**

A seção mais importante e a mais longa do TCC. Organize na mesma ordem dos objetivos específicos.

> **Regra sem exceção:** toda figura, tabela, quadro ou código é **anunciado no texto antes** de aparecer e **explicado depois**. Nunca duas figuras seguidas sem texto entre elas.

## 7.1 Modelo conceitual

Apresente o **diagrama entidade-relacionamento** (figura) com as entidades do domínio. As que você vai encontrar no código:

- **Usuário** (tabela do próprio Django) e **Perfil** (telefone, cidade, estado, CEP, foto), em relação 1:1;
- **Grupos de acesso**: Bolsistas, Administradores e Usuários (grupos do Django, criados automaticamente);
- **Empresa** (instituição à qual o perfil pertence);
- **Categoria** e **Item**;
- **Conversa** (*chat*) e **Mensagem**;
- **Notificação**;
- **Registro de ação** (`AcaoLog`), que guarda o que cada bolsista fez;
- **Dispositivo** e **Leitura RFID** (`LeituraLog`);
- **Arquivo de mídia**, onde ficam as imagens.

**Discuta** as relações que mostram como o domínio foi entendido. Por exemplo: uma conversa liga **dois usuários** (quem iniciou e o dono do item) e **um item**, e o item pode deixar de existir sem que a conversa seja apagada.

## 7.2 Modelo lógico e físico

Apresente o **diagrama lógico** (figura) e um **dicionário de dados** resumido (quadro) com as tabelas principais: nome da tabela, campos principais, tipo, chave e restrição. Não precisa listar todos os campos de todas as tabelas no corpo do texto; se ficar grande, coloque o dicionário completo em apêndice.

Pontos que merecem um parágrafo cada:

- **O item e seu ciclo de vida.** O campo `status` tem cinco valores (`perdido`, `achado`, `pendente_confirmacao`, `confirmado`, `devolvido`). Mostre o ciclo em uma figura simples, e explique que é esse campo que permite que web, celular e balcão vejam o mesmo estado.
- **Os campos que ligam o item aos outros mundos.** `rfid_uid` liga o item à etiqueta física; `slug` gera o endereço público e o QR Code; `image_hash` guarda a "impressão digital" da imagem para a busca visual; `latitude` e `longitude` guardam onde foi encontrado. Explique cada um em uma frase, sem entrar nos algoritmos.
- **Índices e unicidade.** Quais campos têm índice (`rfid_uid`, `image_hash`, o nome do arquivo de mídia) e quais são únicos (`slug` do item, `token_auth` do dispositivo, nome do arquivo). Ligue cada índice à consulta que ele acelera: a leitura RFID procura o item pelo `rfid_uid`; toda imagem exibida é procurada pelo nome.
- **As escolhas de exclusão.** Aqui está uma das discussões mais ricas do trabalho. Mostre em um quadro onde o FIND usa `CASCADE` e onde usa `SET_NULL`, e a lógica por trás:
  - apagar um usuário apaga os itens, o perfil e as notificações dele (`CASCADE`);
  - apagar uma categoria **não** apaga os itens: eles ficam sem categoria (`SET_NULL`);
  - apagar um item **não** apaga os registros de ação dos bolsistas, as leituras RFID nem as conversas (`SET_NULL`). O histórico é preservado. Explique por que isso é importante para a prestação de contas do balcão.
- **Onde ficam as imagens.** As imagens dos itens e os QR Codes são gravados como dado binário na tabela `arquivos_midia`, por meio de um armazenamento próprio (`find/storage.py`), e servidos pela view `serve_db_media`. Descreva como funciona e o motivo registrado no próprio código: no Render, os arquivos gravados em disco se perdem a cada reinicialização. Registre que o `README.md` do projeto cita o Cloudinary, mas a configuração atual (`settings.py`) usa o armazenamento no banco — descreva o que está em vigor.
- **Nomes de tabela.** Várias tabelas mantêm nomes antigos (`mainpage_item`, `mainpage_chat`, `mainpage_profile`) mesmo estando em outras aplicações. Isso é consequência da reorganização explicada na próxima seção.

## 7.3 Evolução do esquema

Apresente a **linha do tempo das migrações** (figura ou quadro), de janeiro a julho de 2026: o que cada uma acrescentou. Os marcos que você vai encontrar:

- janeiro de 2026: modelos iniciais e o *chat*, incluindo uma restrição de unicidade na conversa que foi criada e depois retirada;
- junho de 2026: separação do `mainpage` em três aplicações (`accounts`, `items`, `chats`), a busca por imagem (`image_hash`), o armazenamento de mídia no banco, o registro de ações dos bolsistas, o campo RFID, as coordenadas, as notificações, as empresas e a aplicação `iot`;
- julho de 2026: ajuste final no modelo de dispositivo.

**Discuta o caso mais interessante:** a reorganização de junho. Os modelos mudaram de aplicação no código, mas **as tabelas continuaram as mesmas no banco**. Isso foi feito com a operação `SeparateDatabaseAndState` na migração `0006_move_models_to_apps` e com o `db_table` fixo em cada modelo. Explique a consequência: o código foi reorganizado sem perder nenhum dado já gravado. Ligue ao conceito de refatoração de banco de dados do Referencial.

Discuta também a restrição de unicidade da conversa que foi criada e depois removida: o que ela impedia e por que deixou de fazer sentido. Se não souber o motivo, pergunte ao Gabryell e registre a resposta.

## 7.4 Como cada aplicação usa o banco

Este é o **coração do trabalho**. Apresente um quadro com as tabelas nas linhas e as aplicações nas colunas, marcando se cada aplicação **lê**, **escreve** ou **não usa** cada tabela. Depois, uma figura mostrando o caminho dos dados de cada cliente até o banco.

Escreva um parágrafo para cada aplicação:

- **Web.** O painel em Django acessa o banco diretamente pelo ORM. É a única que usa todas as tabelas, incluindo os painéis de bolsista, de administrador e de IoT. Os indicadores do painel (itens por mês, por categoria, tempo médio até a devolução) são **calculados pelo próprio banco** com agregações do ORM (`annotate`, `Count`, `Avg`, `TruncMonth`); explique por que isso é melhor do que trazer tudo para o Python e contar lá.
- **Mobile.** O aplicativo **não tem banco de dados próprio**. Tudo o que ele mostra vem da API (itens, categorias, perfil, conversas, notificações, pendências do bolsista), e o que ele guarda no aparelho, com o AsyncStorage, são apenas os *tokens* de acesso e os dados do usuário logado. Explique a consequência: não há dado duplicado para sincronizar, mas o aplicativo depende de conexão.
- **IoT.** O ESP32 lê o UID da etiqueta e envia para a API. O próprio **banco autentica o dispositivo**: o *token* enviado é procurado na tabela de dispositivos, que também guarda se o leitor está ativo e quando se comunicou pela última vez. Toda leitura é registrada em `LeituraLog`, **mesmo quando a etiqueta ainda não está associada a nenhum item**. Explique o uso inteligente disso: quando o bolsista cadastra um item na web, a página consulta a leitura mais recente dos últimos 15 segundos e preenche o campo RFID automaticamente. O banco, aqui, é o ponto de encontro entre o leitor físico e o formulário.

**Feche a seção com a ideia principal do trabalho:** as três aplicações não conversam entre si; elas se encontram nos dados. Um item confirmado no balcão pelo leitor RFID aparece como confirmado no celular do dono porque os dois olham para a mesma linha da mesma tabela.

## 7.5 Verificação por testes

Apresente em uma tabela o número de testes de modelo por aplicação e o resultado da execução. Na análise do repositório feita para este plano, havia 9 testes em `accounts`, 20 em `items`, 16 em `chats` e 18 em `iot` — **rode você mesmo e confirme os números** antes de colocar no texto. Diga o que esses testes verificam (por exemplo, geração automática do *slug* e do *token*, relacionamentos e regras de exclusão).

## 7.6 Limitações

Uma subseção curta e honesta. Reconhecer limite aumenta a confiança no trabalho:

- o trabalho **descreve** o banco; não mediu desempenho nem comparou com outras soluções;
- a análise foi feita no código e em uma cópia local, não no banco de produção.

---

# 8. Conclusão
**Prazo: 20/11/2026**

Curta e direta, de uma a duas páginas. Nada de resultado, conceito ou citação que não tenha aparecido antes.

**Escreva, nesta ordem:**

1. **Retomada do problema e do objetivo geral**, afirmando que ele foi alcançado **e dizendo por quê**, com os números: quantas entidades, quantos relacionamentos, quantas migrações, três aplicações atendidas pelo mesmo banco.

2. **Um comentário por objetivo específico**, na mesma ordem em que foram apresentados, cada um apontando a seção ou a figura dos Resultados que o comprova.

3. **Contribuições:** a documentação do modelo de dados de um sistema real de achados e perdidos (que não existia antes); a descrição de como um único banco atende web, celular e IoT; e a evolução do esquema ao longo do projeto, útil para quem for construir sistema parecido.

4. **Dificuldades e limitações:** retome brevemente a Seção 7.6 e acrescente as dificuldades que você realmente enfrentou — entender as migrações antigas, rodar o MySQL localmente, reconstruir o modelo a partir do código.

5. **Trabalhos futuros**, concretos e sem prometer alterações neste trabalho:
   - medir o impacto de manter as imagens no banco à medida que o número de itens cresce;
   - avaliar o uso das coordenadas geográficas em consultas por proximidade;
   - definir uma política de retenção para itens antigos e para os registros de ação e de leitura;
   - avaliar o uso do mesmo banco por várias instituições (a entidade Empresa aponta nessa direção).

**Não generalize** para "qualquer sistema multiplataforma" o que foi observado em um único sistema.

---

# 9. Resumo, Título e revisão final
**Prazo: 27/11/2026**

## 9.1 Resumo

Escrito **por último**, depois de o texto todo estar aprovado. Parágrafo único, 150 a 500 palavras, linguagem impessoal, sem citações, sem siglas pouco conhecidas e sem menção a figuras ou tabelas (NBR 6028:2021).

Uma ou duas frases para cada item:

1. **contexto e problema:** a dispersão das informações sobre objetos perdidos e a necessidade de um único conjunto de dados para web, celular e IoT;
2. **objetivo:** o que o trabalho se propôs a descrever/analisar;
3. **método:** estudo de caso com análise documental do código, das migrações e do histórico de versões;
4. **resultados:** os números principais (entidades, relacionamentos, migrações, testes) e a forma como cada aplicação usa o banco;
5. **conclusão:** o que o estudo permite afirmar e os trabalhos futuros.

O **Abstract** é a versão em inglês. Use os termos consagrados (*relational database*, *data modeling*, *schema migration*, *ORM*). Não entregue tradução automática sem revisar.

**Palavras-chave** (3 a 5), separadas por ponto e vírgula. Campo de ideias: banco de dados relacional; modelagem de dados; migração de esquema; aplicação multiplataforma; achados e perdidos. Escolha os termos pelos quais alguém **procuraria** o seu trabalho.

## 9.2 Título

**Última coisa a ser definida**, em acordo com o orientador. Deve indicar **o que foi feito** e **em que contexto**, e combinar com o objetivo geral.

Pontos a cobrir: o objeto (o banco de dados / a modelagem de dados), a característica que diferencia (base comum para web, *mobile* e IoT) e o contexto (gestão de objetos perdidos e encontrados / plataforma FIND). Se houver subtítulo, separe com dois-pontos. Evite título genérico ("Banco de dados para sistemas web").

## 9.3 Revisão final — checklist

Além do checklist do `README.md`:

- [ ] O objetivo geral, os objetivos específicos, as subseções de Resultados e os parágrafos da Conclusão estão na mesma ordem e falando das mesmas coisas?
- [ ] Os números (tabelas, relacionamentos, migrações, testes) são **exatamente** os mesmos no Resumo, nos Resultados e na Conclusão?
- [ ] Todo conceito usado nos Resultados (cardinalidade, integridade referencial, índice, migração) foi explicado no Referencial?
- [ ] Os diagramas estão legíveis quando impressos em preto e branco?
- [ ] Toda tabela e figura é citada no texto antes de aparecer e explicada depois?
- [ ] Todas as tabelas e figuras têm identificação em cima, centralizada, e fonte embaixo? Nos diagramas que você fez, a fonte é "Elaborado pelo autor (2026)".
- [ ] Fica claro que o Redis não é o banco principal e que o aplicativo não tem banco próprio?
- [ ] **Nenhuma senha, *token* ou chave aparece no texto ou nas figuras.** O repositório tem credenciais escritas no código (por exemplo, em uma migração e no *firmware* do ESP32): se precisar mostrar esses trechos, mascare os valores (`****`).
- [ ] Nenhum dado real de usuário aparece em capturas de tela?
- [ ] As siglas (FIND, IFRN, SGBD, ORM, API, IoT, RFID, LGPD) foram escritas por extenso na primeira ocorrência?
- [ ] A numeração das seções está sem ponto após o número ("2.1 Bancos de dados relacionais")?
- [ ] O texto está impessoal e no passado?
- [ ] Os endereços dos repositórios estão no texto, e o orientador autorizou divulgá-los?
- [ ] Todos os comentários do orientador no documento do Drive foram respondidos?
- [ ] A versão final foi nomeada no histórico de versões do Drive?

---

## Referências mínimas a garantir

- **2 obras de metodologia científica** — Gil (2017) e Prodanov e Freitas (2013), já no `README.md`;
- **3 a 4 obras de banco de dados** — por exemplo, Elmasri e Navathe, Heuser, Silberschatz, Korth e Sudarshan; e, se ler, Codd (1970) e Chen (1976);
- **1 a 2 obras sobre ORM e evolução de esquema** — Fowler (2002) e Ambler e Sadalage (2006);
- **3 a 5 trabalhos relacionados** (Seção 4.5), incluindo Martins e Reis (2025), já citado no projeto;
- **a legislação citada** — Lei nº 13.709/2018 (LGPD);
- **a documentação oficial das ferramentas** — Django, MySQL, SQLite, Redis.

Anote a referência completa de **tudo** o que ler, na seção de Referências do documento do Drive, desde o primeiro dia. Zotero e Mendeley ajudam a montar, mas confira cada entrada contra a NBR 6023:2018 antes de entregar.
