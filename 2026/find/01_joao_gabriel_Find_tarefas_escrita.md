# Plano de escrita do TCC – João Gabriel (Projeto FIND)

**Projeto pai:** FIND – Plataforma e Aplicativo Móvel para Gestão de Objetos Perdidos e Encontrados (ver [projeto.md](../projeto.md)).

**Temática:** arquitetura e integração de uma solução *full-stack* multiplataforma — como ocorreu a integração entre as três aplicações do FIND: **web**, **mobile** e **IoT**.

**Repositórios analisados** (em 22/09/2026):

- Projeto Web (back-end, cliente web e firmware IoT): https://github.com/gabryellgs/projeto-find — último commit `e2f364a` (11/09/2026);
- Projeto Mobile: https://github.com/gabryellgs/find-app — último commit `7c99848` (13/07/2026).

**Base de estilo e de normas ABNT:** o arquivo [README.md](../../../README.md) deste repositório. Tudo o que está lá vale aqui — estrutura, citações, referências, figuras, tabelas, formatação. Este documento **não repete** as regras da ABNT; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copie estas frases para o TCC. Elas dizem sobre o que é cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você leu.

> **Sobre o sistema:** o TCC descreve e analisa a plataforma **como ela foi desenvolvida**. Você não precisa alterar nada nos repositórios para escrever. O que a análise encontrar — inclusive limitações — entra no texto como **resultado** ou como **discussão**, com evidência, e não como tarefa.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do TCC será **criado e compartilhado pelo coordenador em uma pasta do Google Drive**. Você não cria arquivo novo nem trabalha em cópia local.

Como trabalhar nele:

- **Escreva sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico do Drive é o que permite ao orientador ver o que mudou de uma semana para outra.
- **Não crie cópias** ("TCC v2", "TCC final", "TCC final revisado"). O Drive já guarda tudo em **Arquivo → Histórico de versões**.
- **Marque cada entrega no histórico.** Ao terminar uma seção, use **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 02/10`.
- **Avise por mensagem quando entregar.** O orientador não fica olhando o documento; ele precisa saber que há algo novo.
- **Comentário se responde, não se apaga — e quem resolve é o orientador.** Ao atender um comentário, responda na própria conversa dizendo o que foi feito (por exemplo, "Reescrevi o segundo parágrafo e incluí a referência pedida"). **Não clique em "Resolver":** o orientador confere a alteração e, se o comentário tiver sido atendido, ele mesmo marca como resolvido; se não tiver, ele deixa um novo comentário na mesma conversa.
- **Figuras:** cole a imagem no documento e guarde o arquivo original (PNG ou SVG em boa resolução) em uma subpasta `figuras/` da mesma pasta do Drive. Diagramas feitos em draw.io ou PlantUML: guarde também o arquivo-fonte, para poder editar depois.

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

**Um aviso sobre o cronograma.** Os Resultados dependem de diagramas e tabelas que dão trabalho para produzir (diagramas C4 e de sequência, matriz endpoint × cliente, linha do tempo). Não deixe isso para as duas semanas dos Resultados:

- **durante o Referencial (até 16/10):** monte a linha do tempo do projeto (seção 7.3) e faça o levantamento de endpoints e clientes (seção 7.1). Isso ajuda a saber quais conceitos o Referencial precisa explicar;
- **durante a Metodologia e Materiais e Métodos (até 30/10):** desenhe os diagramas C4 e de sequência;
- **cole as figuras e as tabelas no documento assim que ficarem prontas**, mesmo sem o texto de análise. Tabela no lugar é meia seção escrita.

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Texto pela metade dá para comentar; texto que não chega, não.
- Cada entrega é: seção escrita + revisão feita com o [checklist das orientações gerais](../../../README.md#checklist-antes-de-enviar-uma-versão-ao-orientador) + versão nomeada no histórico + aviso ao orientador.
- Responda a **todos** os comentários da entrega anterior, dizendo o que foi feito, antes de avisar sobre a próxima.

---

## Que tipo de trabalho é este

Um **TCC no modelo ABNT**, escrito de forma **completa e sem limite de páginas**, com o método de **estudo de caso único**. Escreva pensando no TCC. Depois que ele estiver pronto, vamos **extrair dele um artigo**, e o formato e o tamanho do artigo serão definidos pelo veículo escolhido (ver seção 10).

**Onde o artigo poderá ser publicado** (para você conhecer desde já; a escolha fica para depois do TCC):

- **iSys – Revista Brasileira de Sistemas de Informação** (SBC) e o **SBSI** (Simpósio Brasileiro de Sistemas de Informação);
- eventos do **CBSoft**: **SBES** (Engenharia de Software) e **SBCARS** (Componentes, Arquiteturas e Reutilização de Software). Procure trilhas de relato de experiência, de indústria ou de ideias emergentes;
- **WebMedia** (Simpósio Brasileiro de Sistemas Multimídia e Web), que aceita trabalhos sobre sistemas web e móveis;
- **SBESC** (Simpósio Brasileiro de Engenharia de Sistemas Computacionais), se o recorte puxar mais para o lado IoT;
- eventos regionais e institucionais (escolas regionais da SBC e eventos de pesquisa do IFRN), como primeira publicação.

Os artigos dos veículos da SBC estão na SBC OpenLib (SOL): https://sol.sbc.org.br. **Antes de começar a escrever, leia pelo menos três estudos de caso ou relatos de arquitetura publicados nesses veículos**: eles mostram o nível de detalhe e o tipo de evidência esperados.

Quatro coisas fazem a diferença entre um relatório de sistema e um trabalho de pesquisa:

1. **O objeto do trabalho não é o sistema de achados e perdidos.** É a **integração**: como três clientes muito diferentes — um navegador, um aplicativo React Native e um microcontrolador ESP32 com leitor RFID — conversam com um único back-end e compartilham dados, contas e regras. O FIND é o **caso real** que permite responder a isso.
2. **Toda afirmação precisa de evidência.** Arquivo do código, diagrama ou referência. Frases como "a arquitetura é escalável, segura e flexível", sem evidência, não se sustentam.
3. **O leitor quer saber o porquê, não só o quê.** Não interessa apenas que o ESP32 envia um `POST`; interessa por que HTTP e não MQTT, por que um token por dispositivo e não o JWT dos usuários, por que a página web consulta a última leitura a cada meio segundo em vez de receber um aviso do servidor. Cada escolha tem **vantagens** e um **custo** — é isso que se chama *trade-off*.
4. **O método tem de dar para repetir.** Informe a data da análise, os repositórios e a versão analisada, e as ferramentas usadas para produzir os diagramas.

Estrutura sugerida:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Arquitetura de software e sua documentação
2.2 Integração de aplicações e estilos para múltiplos clientes
2.3 APIs REST e autenticação em aplicações multiplataforma
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

## O caso em números (levantamento de 22/09/2026)

Use esta seção como ponto de partida. **Confira cada informação nos repositórios na data em que for escrever** e informe no texto a data da análise.

| Aplicação | Repositório | Tecnologias principais | Como se comunica com o back-end |
|---|---|---|---|
| Back-end + cliente web | `projeto-find` | Python 3.12, Django 6.0, Django REST Framework, Simple JWT, Django Channels, django-allauth, MySQL (produção) / SQLite (desenvolvimento), Redis, Bootstrap 5 | O cliente web é renderizado no próprio servidor (templates Django) e autenticado por **sessão**; algumas páginas também chamam endpoints `/api/` por JavaScript |
| Aplicativo móvel | `find-app` | React Native 0.81, Expo SDK 54, React Navigation 7 | **API REST** com **JWT** (`Authorization: Bearer`) e **WebSocket** no chat |
| Leitor IoT | pasta `esp32_firmware/` do `projeto-find` | ESP32, leitor PN532 (RFID/NFC) por I²C, LEDs verde e vermelho | **HTTPS** `POST /api/iot/scan/` com cabeçalho próprio `Authorization: Hardware-Token <token>` |
| Serviços externos | – | Google OAuth, API Gemini, Render | Login social, busca visual e hospedagem |

| Indicador | Back-end e web | App móvel |
|---|---|---|
| Rotas | 44 rotas web (HTML) e 37 endpoints da API REST | – |
| Tamanho aproximado | 6,6 mil linhas de Python (sem migrações) e 11,2 mil linhas de templates | 11,4 mil linhas de JavaScript/JSX |
| Testes automatizados | 190 funções de teste (pytest), 38 delas no módulo `iot` | nenhum |

Esses números servem para **caracterizar o caso** na Metodologia (dar ao leitor uma ideia do porte do sistema). Eles não são o foco da análise.

**Como a integração IoT funciona hoje** (resumo para você conferir no código):

1. o ESP32 lê o UID da etiqueta com o PN532, converte para hexadecimal maiúsculo e envia `{"rfid_uid": "..."}` para `/api/iot/scan/` (`esp32_firmware/main.ino`);
2. o back-end autentica o **dispositivo** pelo token cadastrado no modelo `Dispositivo`, atualiza a `ultima_comunicacao`, procura um `Item` com aquele `rfid_uid` e grava a leitura em `LeituraLog` — com ou sem item associado (`iot/api/views.py`);
3. a resposta HTTP comanda o *feedback* físico: **200** acende o LED verde (item identificado), **404** acende o vermelho (etiqueta sem item), outros códigos fazem o vermelho piscar;
4. no cadastro de item e no painel do bolsista, a **página web** consulta `/api/iot/latest-scan/` a cada **500 ms**, por até **60 tentativas (30 s)**, e preenche o campo RFID com a leitura mais recente dos últimos **15 segundos** (`register_item.html` e `bolsista_dashboard.html`);
5. o administrador gerencia os leitores e consulta as leituras pelo **Painel IoT** da web (`/painel/iot/`);
6. o **aplicativo móvel não fala com o leitor**: ele enxerga o resultado da integração IoT de forma **indireta**, pelos dados dos itens que vêm da API. A integração entre os três acontece **no back-end e no banco de dados**.

Esse último ponto é central para o seu trabalho: o back-end funciona como **ponto único de integração** (*hub*), e cada cliente usa um protocolo e um mecanismo de autenticação diferente para chegar até ele.

---

# 1. Introdução
**Prazo: 02/10/2026**

**Texto corrido, sem subtítulos.** Não crie itens como "Contextualização" ou "Problemática" dentro da Introdução: os blocos abaixo indicam **a ordem dos parágrafos** (é a sequência fixa do [README.md](../../../README.md#introdução)), e a passagem de um bloco para o outro deve ser feita com frases de transição. A Introdução fecha com a pergunta de pesquisa. Duas a três páginas.

**Primeiro bloco — contexto (2 a 3 parágrafos)**

*Pesquise sobre:*

- dados sobre o uso de celular e de internet no Brasil — a pesquisa **TIC Domicílios** (Cetic.br) é a fonte mais citada;
- a presença crescente de dispositivos IoT em ambientes institucionais (controle de acesso, patrimônio, bibliotecas com RFID);
- a ideia de sistemas que precisam atender **vários tipos de cliente ao mesmo tempo**: navegador, celular e dispositivos físicos.

*Fale sobre:*

- por que os sistemas atuais raramente têm um único cliente: o usuário começa no computador, continua no celular, e parte dos dados nasce de sensores e leitores, sem digitação humana;
- a necessidade de **coerência** entre esses clientes: os mesmos dados, as mesmas regras e a mesma conta de usuário, qualquer que seja a porta de entrada;
- o domínio de achados e perdidos em instituições de ensino **apenas como cenário** — um parágrafo curto, no máximo. O trabalho não é sobre achados e perdidos.

**Segundo bloco — o problema (2 a 3 parágrafos)**

O problema do trabalho é **de integração e de arquitetura**, e não "as pessoas perdem objetos".

*Pesquise sobre:* heterogeneidade de clientes, integração de aplicações, dívida técnica e erosão arquitetural (para dar nome e referência aos problemas).

*Fale sobre:*

- a **heterogeneidade** dos clientes: um navegador tem *cookies* e sessão; um aplicativo móvel guarda tokens; um microcontrolador tem pouca memória, não tem usuário humano digitando senha e precisa de uma resposta simples para acender um LED;
- os riscos de ter várias interfaces sobre os mesmos dados: regras de negócio implementadas mais de uma vez, **contratos** (o "combinado" entre cliente e servidor: rotas, campos e códigos de resposta) que divergem quando os clientes evoluem em repositórios separados, e mecanismos de autenticação diferentes para a mesma conta;
- o desafio de integrar um evento **físico** (alguém aproxima uma etiqueta do leitor) com uma tela aberta no navegador, em tempo quase real;
- que essas dificuldades são comuns em projetos pequenos, feitos por equipes acadêmicas, e são pouco relatadas com dados reais.

Use os exemplos do FIND só como ilustração, em uma ou duas frases. Os detalhes ficam para os Resultados.

**Terceiro bloco — caminhos possíveis (1 a 2 parágrafos)**

*Pesquise sobre:* APIs REST como forma de expor um back-end a vários clientes; monólito modular *versus* microsserviços; o padrão *Backend for Frontend* (BFF); formas de integrar dispositivos IoT a sistemas web (HTTP e MQTT).

*Fale sobre:*

- as formas conhecidas de atender clientes diferentes a partir de um mesmo back-end — todos consumindo a mesma API, uma API por tipo de cliente (BFF), ou interfaces diferentes sobre um núcleo comum;
- as opções para integrar dispositivos IoT a sistemas web (requisições HTTP diretas ao servidor ou um intermediário de mensagens como o MQTT);
- o que a literatura já tem (estudos e relatos parecidos) e **o que falta**: trabalhos que mostrem, a partir de um projeto real, a integração de web, mobile e IoT **no mesmo back-end**, com as decisões e os *trade-offs*.

**Quarto bloco — a solução estudada (2 parágrafos)**

*Fale sobre:*

- o FIND e sua arquitetura em uma visão geral: um back-end Django que atende o navegador com páginas renderizadas no servidor (sessão), o aplicativo React Native/Expo pela API REST (JWT) e pelo WebSocket do chat, e o leitor ESP32 + PN532 por um endpoint próprio (token de dispositivo) — todos sobre o mesmo banco de dados;
- o que **este trabalho** faz: descreve a arquitetura de integração, detalha os fluxos entre as três aplicações, mostra como a arquitetura evoluiu a cada novo cliente e discute as decisões tomadas, com suas vantagens e seus custos;
- onde a plataforma foi implantada (Render) e como foi validada. O projeto registra uma etapa de "validação de funcionalidades" em julho de 2026: descreva **como ela foi feita** e se foi formal. Não mencione avaliações que não aconteceram.

**Quinto bloco — vínculo com o projeto e escopo (1 parágrafo)**

*Fale sobre:*

- o histórico do FIND (desde novembro de 2025, inicialmente para o IFRN Campus Canguaretama), a equipe e o projeto institucional a que ele pertence (confirme o nome e o edital com o orientador);
- **qual foi a sua contribuição**. Os repositórios têm vários autores; deixe explícito o que você desenvolveu e qual é o escopo do seu trabalho diante do projeto como um todo;
- o que **não** é escopo: a busca visual com IA (Gemini) e os detalhes de interface. Eles aparecem só como componentes na visão geral.

**Fechamento — pergunta de pesquisa e contribuições (1 parágrafo)**

Feche a Introdução com a pergunta de pesquisa e as contribuições do trabalho, ainda em texto corrido.

**Pergunta principal (proposta — ajuste com o orientador):** como foi estruturada a integração entre uma aplicação web, um aplicativo móvel e um dispositivo IoT a partir de um único back-end, e quais *trade-offs* essa estrutura trouxe?

Desdobre em questões de pesquisa (QP) menores, que vão organizar os Resultados:

- **QP1:** como a arquitetura do FIND está organizada para atender o cliente web, o aplicativo móvel e o leitor IoT?
- **QP2:** quais mecanismos de integração (protocolos, formatos de dados, autenticação e forma de comunicação) cada aplicação usa, e por quê?
- **QP3:** como a arquitetura evoluiu à medida que cada novo tipo de cliente foi acrescentado?
- **QP4:** quais decisões arquiteturais foram tomadas, e que vantagens e custos cada uma trouxe?

**Contribuições** (exemplo): a descrição da arquitetura de integração em diagramas C4 e de sequência; a matriz endpoint × cliente; a descrição da evolução da arquitetura; e o quadro de decisões e *trade-offs*.

---

# 2. Objetivo Geral
**Prazo: 02/10/2026** (junto com a Introdução)

- Uma frase, com **um único verbo principal**, coerente com a pergunta de pesquisa (regras em [README.md](../../../README.md#objetivo-geral));
- o objeto do objetivo é a **arquitetura de integração**, e não "desenvolver um sistema de achados e perdidos";
- estrutura para você completar:

> "O objetivo principal do presente trabalho consiste em descrever e analisar a arquitetura de integração [...] da plataforma FIND, na qual um único back-end atende [...], identificando [...]."

Verbos que combinam: **descrever e analisar** (aceitável como par, por ser um único movimento), **analisar**, **caracterizar**. Evite "desenvolver" e "implementar": o trabalho descreve e analisa o que foi desenvolvido.

---

# 3. Objetivos Específicos

**Não escreva agora.** Eles serão entregues no final (27/11/2026), junto com o Resumo e o Título, para refletirem o que foi **realmente feito**. Siga as regras das orientações gerais: 3 a 5 itens, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Verbos e temas que combinam com este trabalho:

- **revisar** a literatura sobre ...;
- **descrever** a evolução da arquitetura ... a cada novo tipo de cliente ...;
- **documentar** a arquitetura ... utilizando ...;
- **caracterizar** os mecanismos de integração e autenticação de cada ...;
- **analisar** as decisões arquiteturais ... e seus *trade-offs* ...

Não transforme funcionalidades do sistema em objetivos (por exemplo, "permitir a leitura de etiquetas RFID").

---

# 4. Referencial Teórico
**Prazo: 16/10/2026**

Antes de começar, assista ao vídeo sobre Referencial Teórico: https://youtu.be/8Qztq1Q5vb0.

Explique **somente os conceitos que aparecem depois nos Resultados**. Pense assim: se o termo "contrato de API" vai aparecer na análise dos fluxos, o leitor do TCC precisa ter aprendido o que é um contrato de API aqui. Tecnologias específicas (Django, React Native, ESP32, leitor RFID, WebSocket) não ganham seção própria: elas são apresentadas de forma breve em Materiais e Métodos, com referência à documentação oficial.

## 4.1 Arquitetura de software e sua documentação

**Pesquise sobre:** definição de arquitetura de software; atributos de qualidade (manutenibilidade, interoperabilidade e segurança, segundo a ISO/IEC 25010); decisões arquiteturais e *trade-offs*; modelo C4; registros de decisão arquitetural (ADR).

**Fale sobre:** o que é uma decisão arquitetural e por que toda decisão tem vantagens e um custo; como o modelo C4 organiza os diagramas em níveis (contexto, contêineres, componentes); como um ADR registra contexto, decisão, alternativas e consequências. Você vai usar esse formato no quadro de decisões dos Resultados.

## 4.2 Integração de aplicações e estilos para múltiplos clientes

**Pesquise sobre:** estilos de integração (banco de dados compartilhado, chamada remota, troca de mensagens — Hohpe e Woolf); cliente-servidor; arquitetura em camadas; monólito modular *versus* microsserviços; *Backend for Frontend*; páginas renderizadas no servidor *versus* clientes que consomem uma API.

**Fale sobre:** as formas de fazer aplicações diferentes trabalharem juntas e o que cada uma custa; por que um back-end único pode funcionar como ponto central de integração; a diferença entre o navegador receber HTML pronto e o aplicativo receber JSON. Essa seção dá a base teórica para descrever o FIND como um *hub* com três tipos de cliente.

## 4.3 APIs REST e autenticação em aplicações multiplataforma

**Pesquise sobre:** as restrições do estilo REST (Fielding); recursos, métodos e códigos de status HTTP; contrato de API e documentação com OpenAPI; sessão com *cookies*; JSON Web Token (JWT) e *refresh token*; OAuth 2.0 e OpenID Connect (login com Google); autenticação de dispositivos (chave de API ou token por dispositivo); controle de acesso baseado em papéis (RBAC); OWASP API Security Top 10.

**Fale sobre:** por que o navegador usa sessão, o aplicativo usa JWT e o microcontrolador usa um token próprio — **mesma plataforma, três mecanismos**; o que é um contrato de API e por que ele precisa ser mantido quando clientes e servidor evoluem separados; como os códigos HTTP (200, 401, 403, 404) podem servir de linguagem entre servidor e dispositivo — no FIND, eles decidem qual LED acende.

## 4.4 Trabalhos relacionados

**Busque** estudos de caso, relatos de experiência e artigos de arquitetura que integrem web, mobile e/ou IoT em um back-end comum. Bases: SBC OpenLib (SOL), IEEE Xplore, ACM Digital Library, Google Acadêmico e o Portal de Periódicos da CAPES. Termos de busca (use em português e em inglês):

- `"REST API" AND "mobile" AND "web" AND "IoT" AND "architecture"`;
- `"RFID" AND "ESP32" AND "web application"`;
- `"lost and found" AND ("system" OR "application")`;
- `"backend for frontend"`;
- `"case study" AND "software architecture"`;
- `"estudo de caso" AND "arquitetura de software"`;
- `"MQTT" AND "HTTP" AND "comparison"`.

Termine a seção com um **quadro comparativo** (5 a 8 trabalhos), com critérios como: clientes atendidos (web, mobile, IoT), estilo arquitetural, protocolo de integração com o dispositivo, estratégia de autenticação e documentação das decisões. A última linha é o seu trabalho — o quadro deve deixar visível a lacuna que ele ocupa.

## Leituras de partida

Localize a fonte original, confira os dados e só depois inclua nas Referências:

- FIELDING, R. T. *Architectural Styles and the Design of Network-based Software Architectures* (tese de doutorado, 2000);
- BASS, L.; CLEMENTS, P.; KAZMAN, R. *Software Architecture in Practice*;
- HOHPE, G.; WOOLF, B. *Enterprise Integration Patterns*;
- BROWN, S. *The C4 model for visualising software architecture* (c4model.com);
- NYGARD, M. *Documenting Architecture Decisions* (2011);
- NEWMAN, S. *Building Microservices* e o texto do autor sobre o padrão *Backends For Frontends*;
- NAIK, N. *Choice of effective messaging protocols for IoT systems: MQTT, CoAP, AMQP and HTTP* (IEEE ISSE, 2017) — útil para discutir a escolha do HTTP no leitor;
- RFC 9110 (semântica do HTTP), RFC 6749 (OAuth 2.0) e RFC 7519 (JWT);
- ISO/IEC 25010 (modelo de qualidade de produto de software);
- OWASP *API Security Top 10*;
- RUNESON, P.; HÖST, M. *Guidelines for conducting and reporting case study research in software engineering* (Empirical Software Engineering, 2009);
- documentação oficial do Django, do Django REST Framework, do Django Channels, do React Native, do Expo e do ESP32 (Espressif).

Regras de citação e de referência: [README.md](../../../README.md#como-citar-nbr-105202023) e [README.md](../../../README.md#referências).

---

# 5. Metodologia
**Prazo: 23/10/2026**

Antes de escrever, consulte as metodologias prontas na pasta de orientações anteriores: https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing.

**Texto corrido, sem subtítulos**, como na Introdução. Os blocos abaixo indicam a ordem dos parágrafos.

**Primeiro bloco — classificação da pesquisa (1 a 2 parágrafos)**

*Fale sobre:* natureza **aplicada**; objetivos **exploratórios e descritivos**; abordagem **qualitativa** (análise da arquitetura, dos fluxos de integração e das decisões). Nos procedimentos: pesquisa bibliográfica, **pesquisa documental** (código-fonte, arquivos de configuração e documentação dos repositórios) e **estudo de caso único**, conduzido segundo as orientações de Runeson e Höst (2009). Explique, com base nesses autores, por que o estudo de caso é adequado: o objetivo é entender em profundidade um fenômeno (a integração) no seu contexto real (o FIND).

**Segundo bloco — o caso estudado (1 parágrafo)**

*Fale sobre:* a plataforma FIND, seus três perfis de usuário (usuário comum, bolsista e administrador), as três aplicações e o período coberto (novembro de 2025 a setembro de 2026). Use os indicadores de "O caso em números" para dar uma ideia do porte do sistema. Informe os repositórios e a data da versão analisada. Se a revisão do artigo for às cegas, os links saem da versão submetida (ver seção 10).

**Terceiro bloco — etapas do trabalho (1 a 2 parágrafos e uma figura)**

Descreva as etapas em ordem cronológica, com uma **figura do fluxo das etapas**:

1. revisão da literatura;
2. reconstrução da evolução do projeto (em que ordem e em que período cada cliente foi acrescentado);
3. levantamento dos pontos de integração: rotas web, endpoints da API, endpoints usados pelo app (`src/services/api.js` e `auth.js`), endpoints usados pelo firmware e pelas páginas web;
4. documentação da arquitetura (C4, diagramas de sequência e DER) a partir do código;
5. análise dos mecanismos de integração e autenticação de cada cliente e registro das decisões e *trade-offs*.

A ordem dessas etapas é a ordem que os Objetivos Específicos vão seguir.

---

# 6. Materiais e Métodos
**Prazo: 30/10/2026**

Relembre a analogia da receita de bolo do [README.md](../../../README.md#materiais-e-métodos): outra pessoa precisa conseguir repetir a análise.

## 6.1 Materiais

Monte um **quadro-resumo** com as versões **efetivamente usadas** — confira `requirements.txt`, `package.json` e o firmware na data da escrita. Versões encontradas em 22/09/2026:

| Ferramenta | Versão | Finalidade no trabalho |
|---|---|---|
| Python | 3.12 | Linguagem do back-end |
| Django | 6.0.3 | *Framework* do back-end e das páginas web |
| Django REST Framework | 3.15.2 | API REST |
| Simple JWT | 5.5.0 | Autenticação por token no app |
| django-allauth | 65.18.0 | Login com Google na web |
| Django Channels / Daphne | 4.1.0 / 4.2.2 | WebSocket do chat (ASGI) |
| MySQL / SQLite | 8.4 / – | Banco de dados em produção / em desenvolvimento |
| Redis | 7 | *Channel layer* do WebSocket |
| Bootstrap | 5 | Interface web |
| React Native / React | 0.81.5 / 19.1.0 | Aplicativo móvel |
| Expo | SDK 54 | Execução e *build* do app |
| React Navigation | 7 | Navegação do app |
| ESP32 + PN532 | – | Leitor RFID/NFC (cliente IoT) |
| Arduino IDE e biblioteca Adafruit PN532 | – | Desenvolvimento do firmware |
| pytest / pytest-django | 9.1.0 / 4.12.0 | Testes automatizados |
| Render | – | Implantação |
| Git e GitHub | – | Versionamento |

Acrescente as ferramentas usadas **na análise** (por exemplo, draw.io ou PlantUML para os diagramas) e a placa e o leitor usados no protótipo (modelo, e não preço). Ao apresentar tecnologias que não têm seção no Referencial — React Native e Expo, ESP32, RFID, WebSocket —, dê uma explicação curta (uma ou duas frases) e cite a documentação oficial.

## 6.2 Métodos

Para cada item, explique **o que é, para que foi usado e por que foi escolhido**:

- **processo de desenvolvimento:** descreva o que foi realmente feito (incrementos e validações). Não afirme que usou Scrum se não houve *sprints*, papéis e cerimônias;
- **organização do back-end:** como o monólito foi dividido em apps (`accounts`, `items`, `chats`, `iot`) e onde fica cada interface (views web em `mainpage`, API em `*/api/`);
- **integração com o app:** padrão das rotas, formato das respostas JSON, JWT (tempo de expiração, *refresh*), WebSocket do chat;
- **integração com o IoT:** cadastro de dispositivos e geração do token, formato da requisição do ESP32, códigos de resposta e o *feedback* dos LEDs, registro de leituras em `LeituraLog`, limite de requisições (`iot-scan`), o *polling* da página web e a liberação da etiqueta quando o item é devolvido;
- **modelagem:** ferramentas usadas nos diagramas C4, de sequência e no DER;
- **levantamento dos pontos de integração:** como a matriz endpoint × cliente foi montada — a partir dos `urls.py` do back-end, dos arquivos `src/services/*.js` do app, dos templates que chamam a API por JavaScript e do firmware.

**Opcional, se o leitor estiver disponível:** medir o tempo entre aproximar a etiqueta e o campo ser preenchido na página web (por exemplo, 20 leituras cronometradas), registrando a média e o desvio. É uma medição simples que dá ao trabalho um número concreto sobre a integração IoT.

> **Dica:** os leitores valorizam o "por que X e não Y". Informe só as alternativas **que foram de fato consideradas** na época (por exemplo, React Native/Expo *versus* Flutter). Se nenhuma alternativa foi avaliada, diga isso e trate a comparação como discussão à luz da literatura. Não invente comparações.

---

# 7. Resultados e Discussão
**Prazo: 13/11/2026**

Organize o capítulo pelas **questões de pesquisa**, e não por telas. O trabalho não é um catálogo de telas: use capturas apenas para mostrar a **mesma informação chegando por caminhos diferentes** (por exemplo, a leitura de uma etiqueta vista no painel web e o item correspondente no app).

## 7.1 Visão geral da arquitetura de integração (QP1)

**Apresente:**

- diagrama **C4 de contexto** (usuários, bolsista, administrador, leitor físico, Google, Gemini) e de **contêineres** (navegador, app, ESP32, back-end Django, MySQL, Redis);
- diagrama **C4 de componentes** do back-end, mostrando os apps Django e as duas interfaces (views web e API);
- a **matriz endpoint × cliente**: quais rotas o navegador usa, quais o app usa e qual o ESP32 usa. Destaque os casos que cruzam a fronteira — por exemplo, páginas web que chamam `/api/iot/latest-scan/` e endpoints de QR Code por JavaScript;
- o **DER** com destaque para as entidades de integração (`Item.rfid_uid`, `Dispositivo`, `LeituraLog`) e o diagrama de estados do `Item` (`perdido`, `achado`, `pendente_confirmacao`, `confirmado`, `devolvido`).

**Discuta:** o back-end como *hub* e o banco de dados como ponto de encontro entre as aplicações — o app e o leitor RFID nunca se falam, mas compartilham os mesmos itens.

## 7.2 Mecanismos de integração de cada aplicação (QP2)

Uma subseção por fluxo, cada uma com **diagrama de sequência** e explicação:

- **Web ↔ back-end:** sessão, páginas renderizadas no servidor, login com Google pelo allauth;
- **App ↔ back-end:** login com JWT, uso do token nas chamadas, formato das respostas, chat por WebSocket;
- **ESP32 → back-end:** leitura da etiqueta, `POST` com `Hardware-Token`, busca do item, registro em `LeituraLog`, resposta e LED;
- **ESP32 → back-end → navegador:** o fluxo completo de "aproximar a etiqueta e ver o campo preenchido", com o *polling* de 500 ms e a janela de 15 s. Este é o diagrama mais interessante do trabalho: ele junta um evento físico, um endpoint de dispositivo e uma página web.

Feche com um **quadro-síntese** dos três clientes: protocolo, formato, autenticação, forma de comunicação (requisição-resposta, *polling*, WebSocket) e quem inicia a comunicação.

## 7.3 Evolução da arquitetura (QP3)

**Linha do tempo preliminar** (confirme e corrija com a equipe antes de usar):

| Período | O que aconteceu |
|---|---|
| nov. 2025 a jan. 2026 | Aplicação web monolítica em Django com templates: login, cadastro de itens, listagens e chat |
| mar. 2026 | Primeira configuração de integração contínua e de testes |
| abr. 2026 | Início do aplicativo React Native/Expo |
| maio 2026 | API REST para o app, migração para MySQL e implantação no Render |
| jun. 2026 | Modularização do back-end em `accounts`, `items` e `chats`; busca visual por imagem; integração do app com o back-end; suíte de testes automatizados, papéis e permissões, log de ações, QR Code e login com Google na web |
| jun. a jul. 2026 | Integração IoT: modelos `Dispositivo` e `LeituraLog`, endpoint de leitura, "scan ao vivo" na web, liberação da etiqueta ao devolver o item, validação de funcionalidades e firmware do ESP32 |

**Apresente:** a linha do tempo em forma de figura e um diagrama simplificado da arquitetura em cada fase (só web; web + API para o app; web + API + endpoint de dispositivo). Três "fotografias" lado a lado mostram a evolução melhor do que qualquer tabela.

**Discuta:**

- a integração aconteceu **em ondas** (web → mobile → IoT), cada uma acrescentando um novo tipo de cliente a um back-end que já existia. Essas ondas acompanharam a **sequência das disciplinas do curso**: primeiro Back-end, depois Corporativos e, por fim, Dispositivos Móveis e IoT. Cada parte do sistema foi construída à medida que você aprendia as tecnologias correspondentes. Explique isso no texto: é o contexto que justifica por que a arquitetura não foi planejada inteira no início, e sim cresceu por acréscimos;
- o que mudou no back-end a cada novo cliente: a criação da API REST e do JWT para o app, a modularização em apps Django, o endpoint e o token de dispositivo para o ESP32;
- se a arquitetura de cada fase **facilitou ou dificultou** o acréscimo seguinte. Por exemplo: o fato de o back-end já concentrar os dados e as regras permitiu que o app e o leitor fossem "plugados" sem refazer o que existia?

## 7.4 Quadro de decisões e *trade-offs* (QP4)

Esta é a seção em que você mostra **por que a arquitetura ficou como ficou** e **o que se ganhou com isso**. Ela usa o formato de registro de decisões (ADR) apresentado no Referencial (seção 4.1).

**Como montar.** Um quadro com as colunas *Decisão*, *Alternativa*, *Vantagens*, *Custo ou risco* e *Evidência no projeto*. Depois do quadro, escreva **um parágrafo por decisão** explicando o contexto (qual problema a decisão resolvia naquele momento), por que ela foi tomada e o que ela trouxe. Escolha de **5 a 7 decisões**; as quatro primeiras abaixo são obrigatórias, porque tratam diretamente da integração.

**Decisões e o que você pode explicar em cada uma:**

1. **Back-end único como *hub* *versus* serviços separados por cliente.**
   *Vantagens:* dados e regras de negócio em um só lugar; um único banco garante que o item cadastrado na web, lido pelo ESP32 e consultado no app seja o mesmo; a conta do usuário vale em todos os clientes; uma equipe pequena mantém um só projeto, uma só implantação (Render) e uma só suíte de testes; cada novo cliente foi acrescentado sem refazer o que existia (ligue com a seção 7.3).
   *Custos:* ponto único de falha; o sistema escala por inteiro, e não por partes; mudanças no back-end podem afetar os três clientes ao mesmo tempo.
2. **Web renderizada no servidor *versus* web consumindo a mesma API do app.**
   *Vantagens:* a web ficou pronta antes de existir qualquer API; aproveitou o que foi aprendido na disciplina de Back-end; menos código no navegador; autenticação por sessão, simples e segura para o navegador.
   *Custos:* duas "portas" sobre os mesmos dados (views web e views da API), o que pode levar a regras implementadas duas vezes.
3. **Três mecanismos de autenticação (sessão, JWT e token de dispositivo) *versus* um mecanismo único.**
   *Vantagens:* cada cliente usa o mecanismo que combina com ele — o navegador já lida com *cookies*; o app guarda um token; o ESP32 não tem um usuário humano para digitar senha, então recebe um token próprio, que pode ser revogado sem afetar nenhuma conta de pessoa.
   *Custos:* três caminhos de autenticação para manter e testar.
4. **HTTP direto do ESP32 *versus* MQTT com um *broker*.**
   *Vantagens:* reaproveita a infraestrutura que já existia (o mesmo servidor, o mesmo HTTPS, a mesma hospedagem), sem um serviço extra para instalar e manter; o código de resposta HTTP vira o próprio comando do LED (200 = verde, 404 = vermelho), sem precisar de um protocolo próprio; fácil de testar com as mesmas ferramentas da API.
   *Custos:* cada leitura é uma requisição completa; o servidor não consegue "empurrar" mensagens para o leitor; com muitos leitores ou rede instável, o MQTT seria mais adequado (use Naik, 2017).
5. ***Polling* na página web para a leitura RFID *versus* WebSocket** (que o projeto já usa no chat).
   *Vantagens:* simples de implementar e de depurar; funciona sem manter conexão aberta.
   *Custos:* uma requisição a cada 500 ms enquanto a tela está aberta; a janela de 15 s pega a leitura mais recente de qualquer leitor, o que funciona bem com um leitor e pode ficar ambíguo com vários.
6. **Opcionais** (escolha uma ou duas, se houver o que dizer): WebSocket com Channels/Redis no chat *versus* *polling*; conexão TLS do ESP32 sem verificação de certificado (`setInsecure`) *versus* certificado embarcado — simplicidade *versus* segurança; mídia gravada no banco *versus* armazenamento de objetos; SQLite em desenvolvimento e MySQL em produção.

**Exemplo de linha do quadro:**

| Decisão | Alternativa | Vantagens | Custo ou risco | Evidência no projeto |
|---|---|---|---|---|
| Leitor ESP32 envia leituras por HTTPS `POST` ao back-end | MQTT com *broker* | Nenhum serviço extra; reaproveita servidor e hospedagem; código HTTP comanda o LED | Sem *push* para o leitor; menos adequado para muitos leitores | `esp32_firmware/main.ino`; `iot/api/views.py` |

**Feche a seção com um parágrafo-síntese:** por que, **no contexto deste projeto** — equipe pequena, sistema construído em etapas ao longo do curso, um leitor RFID, hospedagem única —, o conjunto dessas decisões foi adequado. Não é preciso provar que a arquitetura é "a melhor"; é preciso mostrar que ela foi **coerente com o contexto** e deixar claro em que condições ela deixaria de ser.

## 7.5 Discussão e limitações

Esta seção dá um passo atrás: em vez de descrever o FIND, ela **interpreta** o que as seções anteriores mostraram. Duas a quatro páginas, em texto corrido, nesta ordem:

1. **Resposta à pergunta principal (1 parágrafo).** Em poucas frases, como a integração foi estruturada e qual foi o principal *trade-off*. Quem ler só este parágrafo tem de entender o resultado do trabalho.
2. **Relação com o Referencial Teórico (2 a 3 parágrafos).** Use os conceitos do capítulo 2 para dar nome ao que foi encontrado. Perguntas que ajudam:
   - o FIND se encaixa em qual estilo de integração de Hohpe e Woolf (banco compartilhado, chamada remota)? Ou combina mais de um?
   - o FIND não usa um BFF, mas a web e o app têm "portas" diferentes sobre o mesmo núcleo. O que isso tem em comum com a ideia do BFF de Newman, e em que é diferente?
   - a API do app segue as restrições REST de Fielding? Em quais pontos sim, em quais não?
   - a escolha do HTTP no leitor confirma ou contradiz o que Naik (2017) recomenda para o porte do FIND?
3. **Relação com os trabalhos relacionados (1 a 2 parágrafos).** Volte ao quadro comparativo da seção 4.4: o que o FIND tem em comum com esses trabalhos, o que ele **confirma** e o que ele **acrescenta** (por exemplo, três tipos de cliente no mesmo back-end, com as decisões documentadas).
4. **Quando esta arquitetura é recomendável (1 parágrafo).** A partir do quadro de decisões, diga para que tipo de projeto a solução do FIND serve bem (equipes pequenas, sistemas acadêmicos ou institucionais, poucos leitores, crescimento por etapas) e o que precisaria mudar em outro cenário (muitos leitores, muitos usuários simultâneos, necessidade de tempo real → MQTT, WebSocket para as leituras, separação de serviços). É essa generalização cuidadosa que torna um estudo de caso útil para outras pessoas.
5. **Limitações (1 a 2 parágrafos).** Seja honesto e, para cada limitação, diga o que foi feito para reduzi-la:
   - **caso único**, que limita a generalização — por isso o item 4 fala em "contexto" e não em regra geral;
   - **participação do autor** no projeto, que pode gerar viés — reduzido ao apoiar cada afirmação em arquivos do código;
   - **análise de uma versão específica** dos repositórios (informe a data);
   - testes automatizados executados com SQLite, enquanto a produção usa MySQL;
   - ausência de avaliação formal com usuários (se for o caso).

**Cuidados gerais nos Resultados:**

- **não exponha senhas, tokens, SSIDs, e-mails ou dados reais de usuários** em figuras, trechos de código ou tabelas. O código do firmware contém credenciais: ao mostrar código, recorte ou substitua por `***`;
- trechos de código só quando ilustram uma decisão, com poucas linhas e numerados como figura ou quadro;
- figuras e tabelas seguem o [README.md](../../../README.md#como-incluir-imagens): título acima, fonte abaixo, citadas no texto antes de aparecerem.

---

# 8. Conclusão
**Prazo: 20/11/2026**

**Fale sobre:**

- a resposta **direta** à pergunta de pesquisa e a cada QP, em poucas frases cada;
- se o objetivo geral foi atingido;
- as principais contribuições;
- as limitações, com honestidade (caso único, participação do autor, análise de uma versão específica);
- trabalhos futuros **coerentes com os resultados**, por exemplo: documentação do contrato da API (OpenAPI), uso de MQTT ou WebSocket para os leitores, suporte a múltiplos leitores simultâneos, avaliação com usuários e testes de carga.

Não traga informação nova nem citações na Conclusão (regras em [README.md](../../../README.md#conclusão)).

---

# 9. Resumo, Título e Objetivos Específicos
**Prazo: 27/11/2026**

## 9.1 Resumo e *Abstract*

- **Tamanho:** no TCC, parágrafo único com 150 a 500 palavras (NBR 6028:2021). No artigo, siga o limite da chamada. Os veículos da SBC exigem resumo em português e em inglês.
- **Sequência:** contexto (sistemas com múltiplos clientes), problema de integração, objetivo, método (estudo de caso único e artefatos produzidos), principais resultados (como a arquitetura atende os três clientes e as principais decisões) e a principal conclusão.
- **Palavras-chave possíveis:** arquitetura de software; integração de sistemas; API REST; Internet das Coisas; RFID; desenvolvimento multiplataforma; estudo de caso.

## 9.2 Título

Definido por último, depois da aprovação do texto. Deve deixar claro que o trabalho é sobre **integração** e citar os três tipos de cliente. Título provisório para referência:

> *Integração de aplicações web, móvel e IoT a partir de um back-end único: um estudo de caso da plataforma FIND*

## 9.3 Objetivos Específicos

Escreva agora, olhando para as etapas da Metodologia e para o que foi realmente feito (ver seção 3 deste documento).

---

# 10. Do TCC ao artigo

Esta etapa começa **depois** que o TCC estiver aprovado. O destino será escolhido com o orientador, e é ele que define o modelo e o limite de páginas.

- **Estrutura típica de um artigo de estudo de caso:** Introdução; Fundamentação e trabalhos relacionados; Método; Contexto do caso; Arquitetura e integração; Evolução; Decisões e *trade-offs*; Discussão e ameaças à validade; Conclusão.
- **Modelo:** use o exigido pela chamada (em geral, o modelo da SBC, também disponível no Overleaf).
- **Enxugar:** o TCC terá mais páginas que o artigo. No artigo, o Referencial vira uma seção curta de fundamentação, e o foco fica nos fluxos de integração, na evolução da arquitetura e no quadro de decisões e *trade-offs*.
- **Revisão às cegas:** se for o caso, retire da versão submetida os nomes, a instituição e os links dos repositórios. Uma opção para os links é o Anonymous GitHub.
- **Licença e autoria:** o README do projeto declara "Licença Proprietária". Antes de publicar trechos de código, confirme com a equipe e com o orientador o que pode ser divulgado. Defina a autoria do artigo (aluno, orientador e, se for o caso, demais integrantes) antes da submissão.
- **Submissão:** nenhum artigo deve ser submetido sem a revisão final do orientador.
