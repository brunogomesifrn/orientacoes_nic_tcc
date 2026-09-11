# Orientações de Escrita e Prazos – João Gabriel (Projeto FIND) – v2

Este documento reúne as orientações individuais do trabalho acadêmico do João Gabriel. Ele complementa as [orientações gerais](../../README.md), que continuam valendo para a estrutura do trabalho, a formatação ABNT, as citações, as referências, as figuras e as tabelas.

> **Importante:** esta versão já considera a arquitetura definida com o orientador: **o cliente web fica fora da API** e as regras de negócio passam a ser compartilhadas por uma camada de serviços (seção 2.1). A análise dos repositórios foi feita em 11/09/2026 (web: commit `e2f364a`; mobile: commit `7c99848`). Sempre prevalecem os acordos feitos com o orientador.

## Sumário

- [1. Temática do trabalho](#1-temática-do-trabalho)
- [2. O que falta implementar](#2-o-que-falta-implementar)
- [3. Orientações de escrita](#3-orientações-de-escrita)
- [4. Prazos](#4-prazos)

---

## 1. Temática do trabalho

### 1.1 Tema e recorte

**Tema:** arquitetura e integração de uma solução *full-stack* multiplataforma.

**Recorte:** engenharia de software e arquitetura de software. O trabalho **não** é um manual do sistema FIND. Ele usa o FIND como **caso real** para descrever e discutir as decisões de projeto de uma plataforma em que **um único back-end e um único núcleo de regras de negócio atendem web e mobile**:

- back-end em Django com duas interfaces sobre as mesmas regras de negócio: páginas web renderizadas no servidor (Bootstrap) e API REST consumida pelo aplicativo móvel (React Native) e pelo leitor IoT;
- modelagem de dados;
- autenticação compartilhada entre os clientes (mesma conta e mesmos papéis, com mecanismos adequados a cada cliente);
- versionamento com Git/GitHub;
- abordagem de desenvolvimento incremental e iterativa.

**Título provisório** (o título definitivo é a última informação a ser definida): *Arquitetura de uma plataforma web e móvel com back-end e regras de negócio compartilhados: relato de experiência do projeto FIND*.

### 1.2 O caso estudado: a plataforma FIND

O FIND é uma plataforma de gestão de achados e perdidos em ambiente institucional, com três perfis de usuário: usuário comum, bolsista (confirma e devolve itens no balcão) e administrador. Componentes existentes hoje:

| Componente | Repositório | Tecnologias principais | Papel na arquitetura |
|---|---|---|---|
| Back-end e cliente web | [projeto-find](https://github.com/gabryellgs/projeto-find) | Python 3.12, Django 6.0, Django REST Framework, Simple JWT, Django Channels, django-allauth, MySQL/SQLite, Redis, Bootstrap 5 | Regras de negócio, persistência, páginas web renderizadas no servidor, API REST e WebSocket do chat |
| Aplicativo móvel | [find-app](https://github.com/gabryellgs/find-app) | React Native 0.81, Expo SDK 54, React Navigation 7 | Cliente móvel que consome a API REST com JWT |
| Leitor IoT | pasta `esp32_firmware/` do projeto-find | ESP32 com leitor PN532 (RFID/NFC) | Cliente da API (leitura de etiquetas) |
| Serviços externos | – | Google OAuth, API Gemini, Render | Login social, busca visual por imagem e hospedagem |

Números levantados em 11/09/2026:

| Indicador | Back-end e web | App móvel |
|---|---|---|
| Commits | 87 (de 05/11/2025 a 11/09/2026) | 11 (de 19/04/2026 a 13/07/2026) |
| Rotas | 44 rotas web (HTML) e 37 endpoints da API REST | – |
| Tamanho aproximado | 6,6 mil linhas de Python (sem migrações, com testes) e 11,2 mil linhas de templates HTML | 11,4 mil linhas de JavaScript/JSX |
| Testes automatizados | 190 funções de teste (pytest) | nenhum |

> O **IoT (RFID)** e a **busca visual com IA** fazem parte da plataforma, mas **não são o foco** do trabalho. Eles aparecem apenas como clientes e integrações na visão arquitetural. Não gaste páginas explicando RFID ou visão computacional.

### 1.3 Pergunta de pesquisa

**Pergunta principal:** como estruturar uma arquitetura desacoplada e manutenível que atenda web e mobile a partir de um único back-end, e quais os *trade-offs* enfrentados?

Para que a pergunta possa ser respondida com evidências em um artigo, desdobre-a em questões de pesquisa (QP) menores (confirme com o orientador):

- **QP1:** como a arquitetura do FIND está organizada para atender o cliente web, o aplicativo móvel e o leitor IoT a partir do mesmo back-end?
- **QP2:** quais decisões de projeto (separação entre páginas web e API, camada de serviços, dados, autenticação, tempo real e implantação) foram tomadas, e quais *trade-offs* cada uma trouxe?
- **QP3:** como a arquitetura evoluiu ao longo do desenvolvimento incremental, e o que as métricas mostram antes e depois da centralização das regras de negócio?

### 1.4 Formato e onde publicar

**Formato:** relato de experiência de desenvolvimento ou artigo de arquitetura, contendo:

- diagramas C4 (contexto, contêineres e componentes);
- diagrama entidade-relacionamento (DER);
- diagramas de sequência dos fluxos principais;
- métricas do processo e do código, extraídas do Git e de ferramentas de análise;
- quadro de decisões arquiteturais e *trade-offs*, com as lições aprendidas.

**Onde publicar.** Confira sempre a chamada vigente: prazos, trilhas, limite de páginas, modelo e se a revisão é às cegas.

- **iSys – Revista Brasileira de Sistemas de Informação** (SBC);
- eventos do **CBSoft** (Congresso Brasileiro de Software), como o **SBES** (Simpósio Brasileiro de Engenharia de Software) e o **SBCARS** (Simpósio Brasileiro de Componentes, Arquiteturas e Reutilização de Software). Procure trilhas voltadas a relatos de experiência, à indústria ou a ideias emergentes;
- **SBSI** (Simpósio Brasileiro de Sistemas de Informação), com perfil próximo ao da iSys;
- periódicos de engenharia de software aplicada.

Os artigos desses veículos estão na SBC OpenLib (SOL): https://sol.sbc.org.br. **Antes de começar a escrever, leia pelo menos três relatos de experiência publicados neles** para entender o formato esperado.

---

## 2. O que falta implementar

### 2.1 Arquitetura adotada: web fora da API, regras de negócio compartilhadas

O back-end tem duas interfaces sobre os mesmos modelos, e **essa separação será mantida**:

| Interface | Onde está | Quem usa | Autenticação |
|---|---|---|---|
| Páginas web renderizadas no servidor | `mainpage/views.py` (1.479 linhas, 44 rotas) | Navegador | Sessão (*cookie*) |
| API REST | `accounts/api`, `items/api`, `chats/api` e `iot/api` (37 endpoints) | App móvel e ESP32 | JWT e token de dispositivo |

A decisão é: **o cliente web continua fora da API**. As páginas web não precisam chamar os endpoints REST. A API existe para o aplicativo móvel e para o leitor IoT. O que muda é **onde ficam as regras de negócio**: hoje elas estão escritas duas vezes (nas views web e nas views da API) e já começaram a divergir. Exemplos concretos:

- o indicador "encontrados" soma `achado` e `confirmado` na web (`_system_counts`, em `mainpage/views.py`), mas conta só `achado` na API (`api_stats`, em `items/api/views.py`). A mesma informação aparece com números diferentes na web e no app;
- fechar um chat é possível na web (`/chats/<id>/fechar/`), mas não pela API;
- a senha mínima é de 6 caracteres na validação do app e de 8 caracteres na API;
- a mudança de status de itens, com registro em `AcaoLog` e criação de notificações, está implementada nos dois lugares.

A solução é extrair uma **camada de serviços** com as regras de negócio. As views web e as views da API passam a ser apenas "adaptadores": recebem a requisição, chamam o serviço e devolvem HTML ou JSON.

```
Navegador ──(sessão)──► views web (HTML) ──┐
                                           ├──► camada de serviços ──► modelos / banco
App e ESP32 ──(JWT/token)──► API REST ─────┘
```

Essa decisão é o eixo do artigo: ela explica por que a web não consome a API, quais problemas a duplicação causou e o que mudou depois da centralização (métricas antes e depois).

### 2.2 Lista de pendências

- **Prioridade 1:** fazer imediatamente.
- **Prioridade 2:** necessário para sustentar, no texto, a "integração" e a "autenticação compartilhada".
- **Prioridade 3:** necessário para discutir manutenibilidade e processo com evidências.

Crie uma *issue* no GitHub para cada item. Assim, a própria lista vira dado do processo (ver item 27).

#### Prioridade 1 – Segurança (os repositórios são públicos e serão citados no artigo)

| # | Situação encontrada | O que fazer |
|---|---|---|
| 1 | `mainpage/migrations/0007_create_superuser.py` cria ou força um superusuário com **senha fixa e fraca** escrita no código | Remover a senha do código (criar o administrador com `createsuperuser` ou por variáveis de ambiente) e **trocar a senha em produção** |
| 2 | `esp32_firmware/main.ino` contém a **senha do Wi-Fi e o token do dispositivo** em texto claro | Revogar o token no painel IoT e gerar outro, trocar a senha da rede e mover os segredos para um `secrets.h` ignorado pelo Git, com um arquivo de exemplo versionado |
| 3 | O `.env` com credenciais foi apagado por um commit comum em 29/05/2026, mas **continua acessível no histórico** | Considerar comprometidas todas as credenciais daquele arquivo e trocá-las (banco, e-mail, Google, Gemini, `SECRET_KEY`) |
| 4 | `SECRET_KEY` tem valor padrão inseguro, e `DEFAULT_PERMISSION_CLASSES` é `AllowAny` | Impedir que a aplicação suba em produção sem `SECRET_KEY` e usar `IsAuthenticated` como padrão, liberando explicitamente só os endpoints públicos |

#### Prioridade 2 – Contrato entre o app e a API

| # | Situação encontrada | O que fazer |
|---|---|---|
| 5 | O app chama `POST /api/google-login/` (`src/services/auth.js`), mas **esse endpoint não existe** no back-end. O login com Google no app não funciona | Criar o endpoint validando o `id_token` do Google e devolvendo JWT, vinculado à mesma conta social criada pelo allauth na web. É o exemplo central de "autenticação compartilhada": mecanismos diferentes, mesma conta |
| 6 | `GET /api/profile/` não devolve `is_admin` nem `is_bolsista`, mas o app usa esses campos para exibir o Painel Bolsista e o Painel Admin (`Dashboard.jsx`). **Os painéis nunca aparecem no app** | Incluir os papéis na resposta, reaproveitando `accounts/permissoes.py` |
| 7 | A função `closeChat` do app aponta para `/api/chats/<id>/fechar/`, rota que só existe na web | Criar o endpoint na API, chamando o mesmo serviço usado pela web |
| 8 | O app envia os status `confirmado` e `pendente_confirmacao` para `/api/items/`, mas a API só filtra `perdido`, `achado` e `devolvido`. Os outros valores são **ignorados sem aviso** e a busca devolve todos os itens | Aceitar todos os status do modelo ou responder com erro 400 |
| 9 | O indicador "encontrados" segue regras diferentes na web e na API | Unificar a regra (resolvido pela camada de serviços do item 16) |
| 10 | O app nunca usa `/api/token/refresh/`. O *access token* expira em 60 minutos e, a partir daí, as chamadas autenticadas falham. Além disso, o `App.js` deixa todas as rotas liberadas, sem verificar o login | Renovar o token automaticamente ao receber 401 e, se a renovação falhar, sair e voltar ao login. Restaurar a navegação condicionada à autenticação |
| 11 | `API_BASE_URL` está fixo na URL de produção | Configurar por ambiente (por exemplo, com a variável `EXPO_PUBLIC_API_URL`) |
| 12 | Os tokens ficam no `AsyncStorage` | Desejável: usar o `expo-secure-store` |

#### Prioridade 2 – Tempo real (chat por WebSocket)

O WebSocket do chat é compartilhado pelos dois clientes e não faz parte da API REST, por isso continua valendo para a web.

| # | Situação encontrada | O que fazer |
|---|---|---|
| 13 | O WebSocket usa `AuthMiddlewareStack` (`find/asgi.py`), que só reconhece **sessão por *cookie***. Como o app autentica com JWT, a conexão é recusada e o app passa a enviar mensagens via REST, **sem tempo real** | Criar um *middleware* de autenticação JWT para o Channels (token enviado na abertura da conexão), mantendo a sessão para a web |
| 14 | O `start.sh`, usado em produção, inicia `gunicorn find.wsgi:application`, um servidor **WSGI**, que não atende conexões WebSocket. Em desenvolvimento o problema não aparece, porque o `daphne` em `INSTALLED_APPS` faz o `runserver` operar em ASGI. O chat da web (`chats.js`) só envia mensagens pelo WebSocket, sem alternativa | Iniciar a aplicação com um servidor ASGI em produção (o Daphne já está nas dependências), confirmar o Redis como *channel layer* no Render e testar o chat nos dois clientes, em produção |
| 15 | O app envia o evento `{"type": "typing"}` ("digitando..."), mas o *consumer* o ignora | Desejável: tratar o evento no back-end ou remover o recurso do app |

#### Prioridade 3 – Arquitetura e manutenibilidade (núcleo do artigo)

| # | Situação encontrada | O que fazer |
|---|---|---|
| 16 | Regras de negócio duplicadas em `mainpage/views.py` e em `*/api/views.py` | Criar a **camada de serviços** (por exemplo, `accounts/services.py`, `items/services.py` e `chats/services.py`) com cadastro de usuário, mudança de status com `AcaoLog` e notificações, confirmação e devolução, estatísticas, chat e gestão de bolsistas. As views web e as da API passam apenas a chamar os serviços. **Colete as métricas do item 28 antes de começar**, para comparar o antes e o depois |
| 17 | Para manter a web fora da API, a fronteira precisa ficar clara, mas alguns templates web ainda chamam endpoints `/api/` por JavaScript: `/api/iot/latest-scan/` (`register_item.html` e `bolsista_dashboard.html`), `/api/items/qr/<slug>/scan/` e `/api/items/qr/<slug>/imagem/` (`bolsista_dashboard.html`) | Criar rotas web equivalentes em `mainpage` chamando os mesmos serviços, para que a web não dependa da API. Se preferir manter alguma dessas chamadas, registre-a como exceção justificada no ADR do item 22 |
| 18 | A API monta as respostas com dicionários manuais (`_item_to_dict`), não usa *serializers* e tem envelopes diferentes (`data`, `results` e `item`) | Usar *serializers* do DRF, um formato único de resposta e de erro e a paginação do próprio DRF |
| 19 | A API não tem documentação nem versionamento, e usa verbos nas URLs (`criar/`, `editar/`, `deletar/`) | Gerar a especificação OpenAPI (por exemplo, com `drf-spectacular`), prefixar as rotas com `/api/v1/` e rever a orientação a recursos. As rotas antigas podem ser mantidas temporariamente para não quebrar o app |
| 20 | `mainpage/views.py` tem 1.479 linhas. Há scripts soltos (`refactor.py` e `mainpage/update_carousels.py`, este com caminho absoluto de uma máquina pessoal), e `mainpage/models.py` apenas reexporta modelos de outros apps | Dividir as views web por domínio, remover os scripts e eliminar a reexportação quando possível |
| 21 | O README diz que as mídias ficam no Cloudinary, mas o código usa `DatabaseStorage` (imagens gravadas como binário no banco) | Corrigir o README e registrar a decisão e o motivo (sistema de arquivos efêmero do Render) |
| 22 | As decisões arquiteturais não estão documentadas | Criar `docs/adr/` com registros de decisão arquitetural (ADR). O primeiro deve ser a decisão desta seção: web renderizada no servidor e fora da API, API para app e IoT, regras de negócio na camada de serviços, com a alternativa considerada (web consumindo a API) e o motivo da escolha. Registre também: monólito modular, sessão + JWT, mídia no banco, Channels/Redis, MySQL em produção e SQLite em desenvolvimento, Expo. ADRs escritos agora sobre decisões passadas devem ser identificados como retroativos |
| 23 | Não há diagramas nos repositórios | Produzir e versionar em `docs/`: C4 (contexto, contêineres e componentes, mostrando a camada de serviços), DER, diagrama de estados do `Item` e diagramas de sequência (login web com sessão e com Google, login no app com JWT, envio de mensagem no chat e leitura RFID) |

#### Prioridade 3 – Qualidade, processo e métricas

| # | Situação encontrada | O que fazer |
|---|---|---|
| 24 | Um *workflow* de integração contínua (CI) foi criado em 26/03/2026 e removido em 29/05/2026, então hoje nenhum teste roda automaticamente. Há 6 *pull requests* do Dependabot abertos, sem revisão | Recriar o *workflow* no GitHub Actions rodando `pytest --cov` a cada *push* e *pull request*, e avaliar (aceitar ou fechar) os PRs do Dependabot |
| 25 | Os 190 testes rodam com SQLite e armazenamento em disco (`conftest.py`), enquanto a produção usa MySQL e `DatabaseStorage`. Não há testes dos serviços, porque a camada ainda não existe | Rodar a suíte e registrar a cobertura. Escrever testes para cada serviço criado no item 16: eles valem para a web e para a API ao mesmo tempo. Citar a diferença de banco como ameaça à validade no artigo. Desejável: um *job* de CI com MySQL |
| 26 | O app não tem testes nem README | Criar o README (como executar, variáveis de ambiente, arquitetura) e, no mínimo, testes da camada `src/services`. Um **teste de contrato** que verifique se cada função de `api.js` corresponde a um endpoint existente teria detectado os itens 5 a 7 |
| 27 | Processo no Git: tudo direto na `main`, nenhuma *issue*, nenhum *pull request* feito pela equipe e nenhuma *tag*. Desde 29/05/2026, 12 dos 66 commits não indicam o tipo de alteração, e há tipos inconsistentes (`refact`/`refactor`, `UI`/`design`/`style`). A mesma pessoa aparece com nomes diferentes nos commits. O commit `5c7a5ce` versionou a pasta `.venv` (5.573 arquivos), removida depois | Adotar, a partir de agora: *issues* para cada pendência, *branches* com *pull requests* (mesmo trabalhando sozinho), Conventional Commits de forma consistente, *tags* por incremento (`v1.0.0`, `v1.1.0` etc.) e um arquivo `.mailmap` para unificar os autores. **Exclua o commit da `.venv` das métricas de linhas alteradas** |
| 28 | Não há métricas coletadas | Coletar e guardar, com a data e o *hash* do commit analisado, as métricas da tabela abaixo, **antes e depois** da camada de serviços |

**Métricas sugeridas:**

| Métrica | Como obter |
|---|---|
| Commits por mês, por autor e por tipo | `git log` e `git shortlog -sn` (com `.mailmap`) |
| Linhas alteradas por módulo ao longo do tempo | `git log --numstat` |
| Tamanho do código por componente (views web, views da API e serviços) | `cloc` |
| Complexidade ciclomática e índice de manutenibilidade (Python) | `radon` |
| Código duplicado entre views web e views da API | `jscpd` |
| Regras de negócio implementadas em mais de um lugar | Levantamento manual (quadro regra × local), antes e depois |
| Cobertura de testes | `pytest --cov` |
| Matriz endpoint × cliente (quais endpoints o app e o ESP32 usam) e rota web × serviço | Levantamento a partir dos `urls.py`, de `src/services/api.js` e do firmware |
| Divergências de contrato encontradas e corrigidas | Itens 5 a 9 desta lista |

Guarde os scripts de coleta no repositório (por exemplo, em `docs/metricas/`), para que os números do artigo possam ser reproduzidos.

---

## 3. Orientações de escrita

Escreva o TCC no modelo ABNT, seguindo as [orientações gerais](../../README.md), mas pense no **artigo** desde o início. Toda afirmação sobre a arquitetura precisa de uma evidência: arquivo, commit, diagrama, métrica ou referência. Frases como "a arquitetura é escalável e segura", sem evidência, são cortadas pelos revisores.

### 3.1 Introdução

- **Contextualização:**
  - pesquise dados sobre o uso de dispositivos móveis e da internet no Brasil (por exemplo, a pesquisa TIC Domicílios, do Cetic.br) e fale sobre por que os sistemas atuais precisam atender navegador e celular ao mesmo tempo;
  - fale sobre a necessidade de manter coerência entre os clientes: mesmos dados, mesmas regras e mesma conta de usuário;
  - apresente o domínio de aplicação (achados e perdidos em instituições de ensino) apenas como **cenário** do caso. O trabalho não é sobre achados e perdidos.
- **Problemática:** o problema do trabalho é **arquitetural**.
  - Fale sobre duplicação de regras de negócio entre interfaces, divergência de contratos entre back-end e clientes, mecanismos de autenticação diferentes em cada cliente, comunicação em tempo real e evolução independente dos clientes.
  - Pesquise sobre dívida técnica e erosão arquitetural para dar nome e referência a esses problemas.
  - Use exemplos do FIND (seção 2.1) só como ilustração. Os detalhes ficam para os Resultados.
- **Caminho para a solução:**
  - pesquise sobre APIs REST, monólito modular *versus* microsserviços, o padrão *Backend for Frontend* (BFF), a camada de serviços (*Service Layer*) e o desenvolvimento móvel multiplataforma;
  - fale sobre as formas de atender clientes diferentes a partir de um mesmo back-end (todos consumindo uma API, ou interfaces distintas sobre um núcleo comum de regras);
  - cite relatos de experiência e artigos de arquitetura parecidos (SOL, IEEE Xplore, ACM Digital Library) e mostre que ainda faltam relatos que exponham decisões e *trade-offs* com dados de um projeto real.
- **Apresentação da solução:**
  - fale sobre o FIND e sua arquitetura: um back-end Django com páginas web renderizadas no servidor para o navegador, API REST para o app React Native/Expo e para o leitor IoT, WebSocket para o chat e uma camada de serviços que concentra as regras de negócio usadas pelas duas interfaces;
  - diga o que este trabalho faz: descreve a arquitetura, registra as decisões, analisa os *trade-offs* e apresenta métricas da evolução do projeto, incluindo o antes e o depois da centralização das regras;
  - informe onde a plataforma foi implantada (Render). Os commits de julho de 2026 mencionam "validação de funcionalidades": descreva como ela foi feita e se foi formal. Não mencione avaliações que não aconteceram.
- **Vínculo com projetos:** fale sobre o histórico do FIND (desde novembro de 2025), a equipe e o projeto institucional a que ele pertence (confirme com o orientador). O repositório tem vários autores, então **deixe explícito qual é a sua contribuição** e qual é o escopo do seu trabalho diante do projeto como um todo.
- **Pergunta de pesquisa e contribuições:** feche a Introdução com a pergunta de pesquisa e as QPs (seção 1.3) e com uma lista curta de contribuições, como é comum em artigos de engenharia de software. Por exemplo: a descrição da arquitetura em C4, o catálogo de decisões e *trade-offs*, as métricas antes e depois da camada de serviços e as lições aprendidas.

### 3.2 Objetivo geral

- Escreva uma frase, com um único verbo principal, coerente com a pergunta de pesquisa;
- o objeto do objetivo é a **arquitetura**, e não "desenvolver um sistema de achados e perdidos";
- estrutura para você completar:

> "O objetivo principal do presente trabalho consiste em descrever e analisar a arquitetura [...] da plataforma FIND, na qual um único back-end, com regras de negócio compartilhadas, atende [...], identificando [...]."

### 3.3 Referencial Teórico

Explique somente os conceitos que aparecem depois nos Resultados. Detalhes de instalação e uso de Django e React Native vão para Materiais e Métodos, com referência à documentação oficial. Estrutura sugerida:

```
2 REFERENCIAL TEÓRICO
2.1 Arquitetura de software
2.2 Estilos e padrões para múltiplos clientes
2.3 APIs REST
2.4 Autenticação e autorização em aplicações multiplataforma
2.5 Comunicação em tempo real
2.6 Desenvolvimento móvel multiplataforma
2.7 Desenvolvimento incremental e controle de versão
2.8 Trabalhos relacionados
```

- **2.1 Arquitetura de software:** pesquise sobre a definição de arquitetura, os atributos de qualidade (principalmente a manutenibilidade, segundo a ISO/IEC 25010), as decisões arquiteturais e os *trade-offs*. Fale sobre documentação de arquitetura: modelo C4, visões arquiteturais e ADR.
- **2.2 Estilos e padrões para múltiplos clientes:** pesquise sobre cliente-servidor, arquitetura em camadas, monólito modular, microsserviços, *Backend for Frontend* e camada de serviços. Fale sobre a diferença entre páginas renderizadas no servidor e clientes que consomem uma API, e sobre como uma camada de serviços permite que as duas formas convivam sem duplicar regras. Essa seção dá a base teórica para a decisão do FIND.
- **2.3 APIs REST:** pesquise sobre as restrições do estilo REST (Fielding), recursos, métodos e códigos HTTP, o modelo de maturidade de Richardson, o versionamento e a documentação com OpenAPI.
- **2.4 Autenticação e autorização:** pesquise sobre sessão com *cookies*, JSON Web Token (JWT), OAuth 2.0 e OpenID Connect (login com Google) e controle de acesso baseado em papéis (RBAC). Fale sobre por que o navegador usa sessão e o app móvel usa token, mesmo com a mesma conta. Consulte também o OWASP API Security Top 10.
- **2.5 Comunicação em tempo real:** pesquise sobre o protocolo WebSocket e a diferença entre WSGI e ASGI. Fale sobre as alternativas (*polling* e *long polling*).
- **2.6 Desenvolvimento móvel multiplataforma:** pesquise sobre as abordagens nativa, híbrida e multiplataforma, e fale sobre onde o React Native e o Expo se encaixam.
- **2.7 Desenvolvimento incremental e controle de versão:** pesquise sobre desenvolvimento iterativo e incremental, refatoração, Git e GitHub, fluxo com *branches* e *pull requests*, Conventional Commits, versionamento semântico e mineração de repositórios de software, que é a base das métricas.
- **2.8 Trabalhos relacionados:** busque relatos de experiência e artigos de arquitetura com back-end compartilhado entre web e mobile. Termos de busca (use em português e em inglês):
  - `"REST API" AND "mobile" AND "web" AND "architecture"`;
  - `"service layer" AND "web application"`;
  - `"backend for frontend"`;
  - `"experience report" AND "software architecture"`;
  - `"cross-platform" AND "React Native"`;
  - `"relato de experiência" AND "arquitetura de software"`.

  Termine a seção com um quadro comparativo usando critérios como: clientes atendidos, estilo arquitetural, forma de compartilhar as regras de negócio, estratégia de autenticação, comunicação em tempo real, documentação das decisões e presença de métricas.

**Leituras de partida.** Localize a fonte original, confira os dados e só depois inclua nas Referências:

- FIELDING, R. T. *Architectural Styles and the Design of Network-based Software Architectures* (tese de doutorado, 2000);
- BASS, L.; CLEMENTS, P.; KAZMAN, R. *Software Architecture in Practice*;
- KRUCHTEN, P. *The 4+1 View Model of Architecture* (IEEE Software, 1995);
- BROWN, S. *The C4 model for visualising software architecture* (c4model.com);
- NYGARD, M. *Documenting Architecture Decisions* (2011);
- FOWLER, M. *Patterns of Enterprise Application Architecture* (padrão *Service Layer*);
- FOWLER, M. *Refactoring: Improving the Design of Existing Code*;
- NEWMAN, S. *Building Microservices* e o texto do autor sobre o padrão *Backends For Frontends*;
- LARMAN, C.; BASILI, V. R. *Iterative and Incremental Development: A Brief History* (IEEE Computer, 2003);
- RFC 6455 (WebSocket), RFC 6749 (OAuth 2.0) e RFC 7519 (JWT);
- ISO/IEC 25010 (modelo de qualidade de produto de software);
- OWASP *API Security Top 10*;
- BIØRN-HANSEN, A.; GRØNLI, T.-M.; GHINEA, G. *A Survey and Taxonomy of Core Concepts and Research Challenges in Cross-Platform Mobile Development* (ACM Computing Surveys);
- RUNESON, P.; HÖST, M. *Guidelines for conducting and reporting case study research in software engineering* (Empirical Software Engineering, 2009);
- documentação oficial do Django, do Django REST Framework, do Django Channels, do React Native e do Expo.

### 3.4 Metodologia

- **Classificação da pesquisa:** fale sobre a natureza aplicada, os objetivos exploratórios e descritivos e a abordagem quali-quantitativa (análise qualitativa das decisões e métricas quantitativas). Nos procedimentos, fale sobre a pesquisa bibliográfica, a pesquisa documental (repositórios, commits e *issues*) e o **relato de experiência** ou **estudo de caso único**. Combine com o orientador qual dos dois termos usar. Se for estudo de caso, siga Runeson e Höst (2009).
- **Pesquisa bibliográfica:** informe as bases consultadas, os termos de busca (seção 3.3), o período das publicações e os critérios de inclusão e exclusão.
- **Etapas:** descreva em ordem cronológica, com uma figura do fluxo:
  1. revisão da literatura;
  2. reconstrução da linha do tempo do projeto a partir do histórico do Git;
  3. documentação da arquitetura (C4, DER e sequência) e registro das decisões (ADR);
  4. diagnóstico dos problemas de integração entre os clientes e da duplicação de regras (seção 2);
  5. coleta das métricas antes da refatoração;
  6. implementação incremental das melhorias (correções de contrato, camada de serviços e fronteira entre web e API);
  7. coleta das métricas depois da refatoração;
  8. análise dos *trade-offs* e extração das lições aprendidas.
- **Linha do tempo preliminar.** Foi extraída dos commits; confirme e corrija com a equipe:

| Período | O que aconteceu |
|---|---|
| nov. 2025 a jan. 2026 | Aplicação web monolítica em Django com templates: login, cadastro de itens, listagens e chat |
| mar. 2026 | Primeira configuração de CI e de testes (o *workflow* foi removido depois) |
| abr. a maio 2026 | Início do aplicativo React Native/Expo (19/04/2026) |
| 29/05/2026 | API REST para o app, migração para MySQL e implantação no Render |
| 03/06/2026 | Modularização: o app `mainpage` foi dividido em `accounts`, `items` e `chats`; busca visual por imagem |
| 11/06/2026 | Integração do app com o back-end |
| 18/06/2026 | Suíte de testes automatizados, papéis e permissões, log de ações, QR Code e login com Google na web |
| jun. 2026 | Pico de atividade: 47 dos 87 commits do repositório web, a maioria de ajustes de interface |
| 04/07/2026 a 13/07/2026 | Integração IoT (ESP32 e RFID), validação de funcionalidades e ajustes nos dois repositórios |
| a partir de set. 2026 | Correções de segurança e de contrato, camada de serviços e documentação da arquitetura (este trabalho) |

- **Ameaças à validade:** o artigo precisa de uma subseção sobre isso, que pode ficar na Metodologia ou nos Resultados. Fale sobre:
  - o caso único, que limita a generalização;
  - a participação do autor no projeto, que pode gerar viés;
  - as métricas retroativas, extraídas de um histórico sem padrão;
  - os testes executados em um ambiente diferente do de produção.

### 3.5 Materiais e Métodos

**Materiais.** Monte o quadro-resumo com as versões **efetivamente usadas**: confira `requirements.txt` e `package.json` na data da escrita, porque as versões mudam se os PRs do Dependabot forem aceitos. Versões encontradas em 11/09/2026:

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
| pytest / pytest-django / pytest-cov | 9.1.0 / 4.12.0 / 7.1.0 | Testes automatizados e cobertura |
| Docker e Docker Compose | – | Ambiente local |
| Render | – | Implantação |
| Git e GitHub | – | Versionamento |
| ESP32 e PN532 | – | Leitor RFID (cliente IoT) |

**Métodos.** Para cada item, explique o que é, para que foi usado e por que foi escolhido:

- **processo de desenvolvimento:** descreva o que foi realmente feito (incrementos e validações). Não afirme que usou Scrum se não houve *sprints*, papéis e cerimônias;
- **modelagem:** ferramentas usadas nos diagramas C4 (por exemplo, Structurizr, PlantUML ou draw.io) e no DER;
- **organização do back-end:** como as responsabilidades foram divididas entre views web, views da API e camada de serviços, e como a refatoração foi feita em passos pequenos, com os testes rodando a cada passo;
- **API e autenticação:** padrões da API e estratégia de autenticação (sessão na web, JWT no app, token de dispositivo no ESP32 e papéis por grupos);
- **testes automatizados e CI;**
- **coleta de métricas:** ferramentas, comandos, data da coleta e *hash* do commit analisado, para permitir a reprodução.

> **Dica para o artigo:** os revisores valorizam o "por que X e não Y". A escolha de manter a web fora da API tem uma alternativa clara (web consumindo a API): explique por que ela não foi adotada. Para as demais escolhas, informe só as alternativas **que foram de fato consideradas**, como React Native/Expo *versus* Flutter, ou mídia no banco *versus* armazenamento de objetos. Se nenhuma alternativa foi avaliada na época, diga isso e trate como limitação. Não invente comparações.

### 3.6 Resultados (e Discussão)

Organize o capítulo pelas questões de pesquisa, e não por telas. Estrutura sugerida:

- **Visão geral da arquitetura (QP1):** diagramas C4 de contexto, de contêineres e de componentes do back-end, mostrando as views web, a API e a camada de serviços. Inclua a matriz endpoint × cliente (app e ESP32) e o quadro rota web × serviço, e mostre o que é compartilhado e o que é exclusivo de cada cliente.
- **Modelagem de dados:**
  - apresente o DER e o diagrama de estados do `Item` (`perdido`, `achado`, `pendente_confirmacao`, `confirmado` e `devolvido`);
  - fale sobre as decisões de modelagem: auditoria com `AcaoLog`, mídia no banco (`ArquivoMidia`) e dispositivos e leituras IoT;
  - comente os nomes de tabela `mainpage_*`, mantidos após a modularização. Eles mostram uma evolução feita sem perda de dados.
- **Separação entre web e API e centralização das regras (QP2):**
  - apresente a situação inicial: regras duplicadas e as divergências encontradas (seção 2.1 e itens 7 a 9);
  - explique a decisão de manter a web fora da API e a camada de serviços, com o ADR correspondente;
  - mostre um exemplo curto de uma regra (por exemplo, a devolução de item) antes, espalhada nas duas views, e depois, no serviço.
- **Autenticação e autorização compartilhadas (QP2):** diagramas de sequência dos logins (sessão e Google na web, JWT no app e token no ESP32) e dos papéis. Mostre os problemas encontrados (itens 5, 6, 10 e 13) e como foram resolvidos.
- **Comunicação em tempo real (QP2):** o chat por WebSocket, a diferença entre WSGI e ASGI na implantação, a autenticação do WebSocket para os dois clientes e a alternativa via REST no app.
- **Evolução incremental e processo (QP3):** figura com a linha do tempo, gráfico de commits por mês, tipos de commit, crescimento dos testes, histórico do CI e o que mudou no processo depois da adoção de *issues* e *pull requests*.
- **Manutenibilidade antes e depois (QP3):** tabela com as métricas antes e depois da camada de serviços e das correções (tamanho das views, duplicação, regras implementadas em mais de um lugar, complexidade, cobertura e divergências de contrato).
- **Quadro de decisões e *trade-offs*:** use as colunas *Decisão*, *Alternativa*, *Benefício*, *Custo ou risco* e *Evidência no projeto*. Decisões candidatas:
  - web renderizada no servidor e fora da API, com camada de serviços compartilhada *versus* web consumindo a API;
  - monólito modular *versus* microsserviços;
  - sessão + JWT *versus* um mecanismo único de autenticação;
  - mídia no banco *versus* armazenamento de objetos;
  - WebSocket com Channels/Redis *versus* *polling*;
  - SQLite em desenvolvimento e MySQL em produção;
  - IA externa (Gemini) com alternativa local.
- **Lições aprendidas:** numere (L1, L2...) e associe cada uma a uma evidência. Exemplos de tema: "duas interfaces sobre os mesmos modelos, sem camada de serviços, fizeram as regras divergirem"; "clientes evoluindo em repositórios separados, sem testes de contrato, geraram chamadas a endpoints inexistentes".
- **Discussão:** relacione os resultados com o Referencial Teórico e com os trabalhos relacionados e aponte as limitações.

Cuidados:

- use poucas telas. Capturas servem para mostrar a **mesma funcionalidade na web e no app**, atendida pelo mesmo serviço no back-end. O artigo não é um catálogo de telas;
- não exponha senhas, tokens, e-mails ou dados reais de usuários em figuras, trechos de código ou tabelas.

### 3.7 Conclusão

- Responda **diretamente** à pergunta de pesquisa e a cada QP;
- comente cada objetivo específico;
- retome as principais contribuições e lições aprendidas;
- apresente as limitações com honestidade: caso único, métricas retroativas e pendências não concluídas;
- sugira trabalhos futuros, por exemplo: testes de desempenho e de carga, observabilidade (logs e monitoramento), avaliação com usuários e extração de serviços independentes, somente se houver necessidade comprovada.

### 3.8 Objetivos específicos

Serão entregues no final, junto com o Resumo, para refletirem o que foi **realmente feito**. Siga as regras das orientações gerais: 3 a 5 itens, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Verbos e temas que combinam com este trabalho:

- **revisar** a literatura sobre ...;
- **reconstruir** a evolução ... a partir do histórico ...;
- **documentar** a arquitetura ... utilizando ...;
- **identificar** e **corrigir** ... de integração ...;
- **centralizar** / **refatorar** as regras de negócio ... em ...;
- **mensurar** e **comparar** ... antes e depois ...;
- **analisar** os *trade-offs* ...

Não transforme funcionalidades do sistema em objetivos (por exemplo, "permitir o login com Google").

### 3.9 Resumo e *Abstract*

- **Tamanho:** no TCC, parágrafo único com 150 a 500 palavras (NBR 6028:2021). No artigo, siga o limite da chamada. Os veículos da seção 1.4 exigem resumo em português e em inglês.
- **Sequência:** contexto, problema arquitetural, objetivo, método (relato de experiência ou estudo de caso, artefatos e métricas), principais resultados **com números** e principal lição ou conclusão.
- **Palavras-chave possíveis:** arquitetura de software; API REST; camada de serviços; desenvolvimento multiplataforma; relato de experiência; Django; React Native.

### 3.10 Do TCC ao artigo

- **Estrutura típica de um relato de experiência:** Introdução; Fundamentação e trabalhos relacionados; Contexto do projeto; Método; Arquitetura e decisões; Resultados e métricas; Discussão e lições aprendidas; Ameaças à validade; Conclusão.
- **Modelo:** use o exigido pela chamada (em geral, o modelo da SBC, também disponível no Overleaf).
- **Revisão às cegas:** se for o caso, retire da versão submetida os nomes, a instituição e os links dos repositórios. Uma opção para os links é o Anonymous GitHub.
- **Licença e autoria:** o README do projeto declara "Licença Proprietária". Antes de publicar trechos de código, confirme com a equipe e com o orientador o que pode ser divulgado. Defina a autoria do artigo (aluno, orientador e, se for o caso, demais integrantes) antes da submissão.
- **Submissão:** nenhum artigo deve ser submetido sem a revisão final do orientador.

---

## 4. Prazos

Hoje é **11/09/2026**. Cada prazo conta a partir da conclusão da etapa anterior, e as datas abaixo consideram que cada etapa é concluída no prazo. Entregar antes é bem-vindo. Envie cada parte ao orientador até a data indicada.

| Etapa de escrita | Duração | Data-limite |
|---|---|---|
| Introdução e Objetivo geral | 1 semana a partir de hoje | **18/09/2026** (sexta-feira) |
| Referencial Teórico | 1 semana e meia após a Introdução | **28/09/2026** (segunda-feira) |
| Metodologia | 1 semana após o Referencial Teórico | **05/10/2026** (segunda-feira) |
| Materiais e Métodos | 1 semana após a Metodologia | **12/10/2026** (segunda-feira) |
| Resultados | 2 semanas após Materiais e Métodos | **26/10/2026** (segunda-feira) |
| Conclusão | 1 semana após os Resultados | **02/11/2026** (segunda-feira) |
| Resumo e Objetivos específicos | 1 semana após a Conclusão | **09/11/2026** (segunda-feira) |

> **Atenção:** 12/10/2026 e 02/11/2026 são feriados nacionais. Combine com o orientador se a entrega deve ser antecipada para o dia útil anterior.

**Alinhamento sugerido das implementações.** É uma recomendação; os prazos oficiais são os da tabela acima. Os Resultados dependem das implementações e das métricas:

| Até | O que deve estar pronto | Por quê |
|---|---|---|
| 18/09/2026 | Itens 1 a 4 (segurança); *issues* criadas para as pendências; métricas "antes" coletadas (item 28); ADR da decisão da seção 2.1 (item 22) | As métricas "antes" precisam ser coletadas antes de qualquer refatoração, e o ADR apoia a escrita da Introdução |
| 05/10/2026 | Itens 5 a 15 (contrato entre o app e a API e tempo real); CI funcionando e trabalho via *pull requests* (itens 24 e 27) | A Metodologia descreve esse processo |
| 19/10/2026 | Itens 16 a 21, 23, 25 e 26 (camada de serviços, fronteira entre web e API, API, documentação, diagramas e testes) e métricas "depois" | Sobra uma semana para escrever os Resultados com os dados fechados |

Antes de cada envio, use o [checklist das orientações gerais](../../README.md#checklist-antes-de-enviar-uma-versão-ao-orientador).
