# Orientações de Escrita e Prazos – Alan Bezerra (Projeto FIND)

Este documento reúne as orientações individuais do trabalho acadêmico do Alan Bezerra. Ele complementa as [orientações gerais](../../README.md), que continuam valendo para a estrutura do trabalho, a formatação ABNT, as citações, as referências, as figuras e as tabelas.

> **Importante:** a análise dos repositórios foi feita em 11/09/2026 (web: commit `e2f364a`; mobile: commit `7c99848`). Os números apresentados na seção 2 foram medidos no código nessa data e servem como **ponto de partida**: eles vão mudar assim que você começar a corrigir, e quem coleta os números oficiais do trabalho é você. Sempre prevalecem os acordos feitos com o orientador.

## Sumário

- [1. Temática do trabalho](#1-temática-do-trabalho)
- [2. O que falta implementar](#2-o-que-falta-implementar)
- [3. Orientações de escrita](#3-orientações-de-escrita)
- [4. Prazos](#4-prazos)

---

## 1. Temática do trabalho

### 1.1 Tema e recorte

**Tema:** acessibilidade digital e desenho inclusivo.

**Recorte:** desenvolvimento web (e móvel) com foco em padrões de acessibilidade. É uma competência central do curso de Tecnologia em Sistemas para Internet (TSI) e muito valorizada no mercado.

O trabalho **não** é um manual do sistema FIND e **não** é sobre a arquitetura da plataforma. O FIND é o **objeto avaliado**: você vai medir a acessibilidade da plataforma (web e aplicativo), corrigir as barreiras encontradas e medir de novo, comparando o antes e o depois.

O que você vai fazer, em uma frase: **avaliar e adequar a acessibilidade da plataforma FIND segundo as diretrizes WCAG 2.2**, usando ferramentas automáticas (axe, WAVE, Lighthouse e o ASES, do governo brasileiro) somadas a inspeção manual e a teste com tecnologias assistivas (leitor de tela e navegação por teclado), ancorando tudo no marco brasileiro (Lei Brasileira de Inclusão, eMAG e as normas ABNT de acessibilidade digital).

**Título provisório** (o título definitivo é a última informação a ser definida): *Avaliação e adequação da acessibilidade de uma plataforma web e móvel de achados e perdidos segundo a WCAG 2.2: um estudo antes e depois*.

### 1.2 O caso avaliado: a plataforma FIND

O FIND é uma plataforma de gestão de achados e perdidos em ambiente institucional, com três perfis de usuário: usuário comum, bolsista (confirma e devolve itens no balcão) e administrador.

| Componente | Repositório | Tecnologias da interface | O que você avalia |
|---|---|---|---|
| Cliente web (páginas renderizadas no servidor) | [projeto-find](https://github.com/gabryellgs/projeto-find) | Django 6.0 com *templates*, Bootstrap 5.3, Bootstrap Icons, Swiper | 30 arquivos HTML e 23 arquivos CSS: estrutura semântica, formulários, foco, contraste, conteúdo dinâmico |
| Aplicativo móvel | [find-app](https://github.com/gabryellgs/find-app) | React Native 0.81, Expo SDK 54, React Navigation 7 | 14 telas e 17 componentes: rótulos acessíveis, papéis, alvos de toque, escala de fonte, contraste |
| Ambiente de produção | – | Render | É onde você roda as ferramentas automáticas (`https://projeto-find.onrender.com`) |

> O back-end, a API, o IoT (RFID) e a busca visual com IA **não são o foco** do seu trabalho. Eles aparecem só como contexto, quando a barreira estiver na interface que expõe esses recursos (por exemplo, o resultado da busca por imagem precisa de alternativa textual).

### 1.3 Marco legal e normativo (o diferencial brasileiro do seu trabalho)

Este é o ponto que dá identidade ao trabalho e que os revisores brasileiros valorizam. Estude e cite, sempre na fonte original:

| Instrumento | O que é | Por que entra no seu trabalho |
|---|---|---|
| **Lei nº 13.146/2015** (Lei Brasileira de Inclusão – LBI), art. 63 | Torna obrigatória a acessibilidade dos sítios mantidos por empresas com sede ou representação comercial no país e por órgãos do governo, segundo as melhores práticas e diretrizes de acessibilidade adotadas internacionalmente. Prevê também o símbolo de acessibilidade em destaque | É a base legal da obrigatoriedade. O FIND é um sistema institucional: a exigência se aplica |
| **Decreto nº 5.296/2004**, art. 47 | Primeiro dispositivo a exigir acessibilidade nos portais e sítios eletrônicos da administração pública | Mostra a evolução da exigência. Comente suas limitações: restringia-se à deficiência visual e à administração pública |
| **eMAG 3.1** (Modelo de Acessibilidade em Governo Eletrônico, 2014) | Recomendações para padronizar a acessibilidade dos sítios do governo brasileiro; base do avaliador ASES | É o modelo nacional. Use-o para justificar o uso do ASES e para traduzir recomendações ao contexto brasileiro |
| **ABNT NBR 17060:2022** | Primeira norma brasileira de acessibilidade digital: acessibilidade em aplicativos de dispositivos móveis – requisitos (54 requisitos, sendo 36 obrigatórios, alinhados à WCAG) | É a norma certa para a parte **mobile** do seu trabalho. Quase nenhum TCC usa: é diferencial |
| **ABNT NBR 17225:2025** | Acessibilidade em conteúdo e aplicações web – requisitos, desenvolvida a partir da WCAG 2.2, com lista de itens críticos | É a norma mais recente para a parte **web**. Verifique a edição vigente e o acesso pela biblioteca da instituição |
| **WCAG 2.2** (W3C, recomendação de 05/10/2023) | Diretrizes internacionais, organizadas em 4 princípios, com critérios de sucesso nos níveis A, AA e AAA | É o instrumento de medida do trabalho. Adote o **nível AA** como meta, como fazem a legislação e as normas |

**Atenção a um detalhe que vale pontos:** a WCAG 2.2 acrescentou nove critérios de sucesso em relação à 2.1 — 2.4.11 Foco não obscurecido (mínimo), 2.4.12 Foco não obscurecido (melhorado), 2.4.13 Aparência do foco, 2.5.7 Movimentos de arrastar, 2.5.8 Tamanho do alvo (mínimo), 3.2.6 Ajuda consistente, 3.3.7 Entrada redundante, 3.3.8 e 3.3.9 Autenticação acessível. **As ferramentas automáticas praticamente não testam esses critérios novos.** Se a sua inspeção manual cobrir justamente eles, o trabalho ganha originalidade. Confirme a lista e a redação oficial na tradução autorizada do W3C.

### 1.4 Pergunta de pesquisa

**Pergunta principal:** quais barreiras de acessibilidade estão presentes em uma plataforma web e móvel desenvolvida sem requisitos de acessibilidade e em que medida correções guiadas pela WCAG 2.2 reduzem essas barreiras?

Desdobre em questões de pesquisa (QP) menores (confirme com o orientador):

- **QP1:** quais barreiras de acessibilidade existem hoje na plataforma, como elas se distribuem por critério de sucesso, por princípio e por severidade, e quais telas concentram os problemas?
- **QP2:** qual é a **concordância entre os métodos de avaliação** — axe, WAVE, Lighthouse, ASES, inspeção manual e teste com tecnologia assistiva? Quantas barreiras cada método detecta, quantas só aparecem na inspeção manual e quantos falsos positivos as ferramentas produzem?
- **QP3:** qual o efeito das correções aplicadas, comparando a avaliação antes e depois por critério de sucesso, e quais barreiras permanecem?

> A **QP2 é o seu melhor trecho de pesquisa**. Já existe literatura mostrando que ferramentas automáticas detectam apenas parte das barreiras reais, e comparar quatro ferramentas (incluindo o ASES, pouco estudado fora do Brasil) em um sistema real é uma contribuição concreta. Sem ela, o trabalho corre o risco de parecer apenas um relatório técnico.

### 1.5 Formato e onde publicar

**Formato:** estudo de avaliação de conformidade com correção e reavaliação, contendo:

- protocolo de avaliação explícito (ver a WCAG-EM na seção 3.4);
- inventário de barreiras, com critério de sucesso, severidade, localização e evidência;
- quadro comparativo entre os métodos de avaliação (QP2);
- comparação antes/depois por critério;
- se possível, teste de tarefas com usuárias e usuários que usam tecnologia assistiva.

**Onde publicar.** Confira sempre a chamada vigente: prazos, trilhas, limite de páginas, modelo e se a revisão é às cegas.

- **IHC – Simpósio Brasileiro sobre Fatores Humanos em Sistemas Computacionais** (SBC): é o veículo mais adequado ao tema no Brasil;
- **Journal on Interactive Systems (JIS)**, revista da SBC ligada à comunidade de IHC;
- **WAIHCWS** (Workshop sobre Aspectos da Interação Humano-Computador na Web Social) e trilhas de acessibilidade do **SBSI** e do **SBQS** (Simpósio Brasileiro de Qualidade de Software), onde há trabalhos de avaliação de acessibilidade com métricas;
- eventos de governo digital da SBC, para o recorte legal/eMAG/ASES;
- internacionais, se a escrita em inglês avançar: **W4A** (ACM Web for All) e **ASSETS** (ACM), além da revista *Universal Access in the Information Society* (Springer).

Os artigos dos veículos brasileiros estão na SBC OpenLib (SOL): https://sol.sbc.org.br. **Antes de começar a escrever, leia pelo menos três artigos de avaliação de acessibilidade publicados no IHC ou no SOL** e repare em como eles descrevem o protocolo, apresentam os resultados por critério e discutem as limitações. Esse é o formato que se espera de você.

> **Combinação com os colegas.** Os repositórios são compartilhados com outros trabalhos do projeto (arquitetura e correspondência automática de itens). O seu escopo é a **interface**: *templates*, CSS, componentes do aplicativo e os textos apresentados ao usuário. Não refatore a camada de serviços nem a API: isso é escopo de outro trabalho. Combine com a equipe o uso de *branches* e *pull requests* para evitar conflitos nos mesmos arquivos, e marque as suas *issues* com uma etiqueta própria (por exemplo, `acessibilidade`), porque essa etiqueta vai virar dado do seu trabalho.

---

## 2. O que falta implementar

Mantenha a arquitetura já existente. O que entra aqui é o que precisa ser **acrescentado ou corrigido na interface** para que a temática se sustente, mais a infraestrutura de avaliação que vai gerar os dados do artigo.

### 2.1 Diagnóstico preliminar (medido em 11/09/2026)

Este é um levantamento **estático** do código, feito com scripts, para você não começar do zero. Ele **não substitui** a sua avaliação: refaça a medição com as ferramentas e com inspeção manual, na data da sua coleta, e use os seus números no trabalho.

**Comece reconhecendo o que já está certo** — um artigo que diz "não havia nada" perde credibilidade quando o revisor abre o código:

- 47 das 48 imagens nos *templates* têm atributo `alt`;
- os formulários de login, cadastro e recuperação de senha já usam `role="alert"` e `aria-live="assertive"` nas mensagens de erro (`login.html:63`, `register.html:63`, `password_reset.html:50-52`);
- os painéis do bolsista e do administrador usam o padrão de abas do Bootstrap com `role="tablist"`, `role="tab"`, `aria-selected` e `aria-controls` (`admin_dashboard.html:49-80`);
- as mensagens do Django aparecem em `div` com `role="alert"` nos painéis;
- o mapa do aplicativo foi configurado com `pointerEvents="none"` e `scrollEnabled={false}` (`ItemLocationMap.native.js`), o que evita o problema de movimento de arrastar (critério 2.5.7);
- a navbar usa a combinação `#0B3A4A` sobre `#90dbf4`, com relação de contraste de 7,93:1 — aprovada com folga no nível AA.

**Barreiras encontradas no cliente web** (30 arquivos HTML, dos quais 19 estendem o `base.html` e 7 têm estrutura própria):

| # | Situação medida | Critério WCAG 2.2 provavelmente envolvido |
|---|---|---|
| a | **Nenhum link de "pular para o conteúdo"** em nenhuma página (0 ocorrências), e nenhuma classe utilitária própria para texto visível apenas a leitores de tela | 2.4.1 Ignorar blocos |
| b | **12 das 19 páginas** que estendem o `base.html` **não têm `<h1>`**. Entre elas, `item_detail.html`, `chats_list.html`, `bolsista_dashboard.html` e `admin_dashboard.html` | 1.3.1 Informações e relações; 2.4.6 Cabeçalhos e rótulos |
| c | **68 dos 90 `<label>` não têm atributo `for`**, e **75 dos 97 campos** de formulário (`input`, `select`, `textarea`) não têm rótulo programático (sem `for`, sem `aria-label`, sem `aria-labelledby`). A identificação do campo depende do `placeholder` | 1.3.1; 3.3.2 Rótulos ou instruções; 4.1.2 Nome, função, valor |
| d | **604 ícones** `<i class="bi ...">` e **nenhum** com `aria-hidden="true"`: ícones decorativos são anunciados pelo leitor de tela | 1.1.1 Conteúdo não textual |
| e | **9 controles cujo conteúdo é apenas um ícone, sem nome acessível:** enviar mensagem (`chat_detail.html:83`, `chats_list.html:178`, `item_detail.html:304`), fechar o chat (`item_detail.html:292`), voltar (`chat_detail.html:14`), filtros (`menu.html:119`), busca visual (`menu.html:125`), novo item (`base.html:499`) e leitura RFID (`bolsista_dashboard.html:911`) | 1.1.1; 2.4.4 Finalidade do link; 4.1.2 |
| f | **43 células de cabeçalho `<th>` e nenhuma com `scope`**; as tabelas dos painéis também não têm legenda (`caption`) | 1.3.1 |
| g | **12 diálogos modais** (`modal fade`) no código estático, dos quais apenas 2 têm nome acessível e **nenhum** tem `role="dialog"`/`aria-modal`. Como vários ficam dentro de laços `{% for %}`, em tempo de execução o número é bem maior | 4.1.2; 2.4.3 Ordem do foco |
| h | **`outline: none` em 11 dos 23 arquivos CSS**, com `:focus-visible` definido em **apenas 1** (`new_password.css`): em boa parte da interface não se vê onde está o foco do teclado | 2.4.7 Foco visível; 2.4.11 Foco não obscurecido; 2.4.13 Aparência do foco |
| i | **Nenhum `@media (prefers-reduced-motion)`**, com animações e transições declaradas em vários arquivos | 2.3.3 Animação a partir de interações (AAA) |
| j | **Contraste insuficiente em cores de uso frequente.** Valores calculados pela fórmula da WCAG: `#0ea5e9` sobre branco e branco sobre `#0ea5e9` = **2,77:1**; `#1eaed4` sobre branco = **2,61:1**; `#94A3B8` sobre branco = **2,56:1**; texto do rodapé `rgba(11,58,74,.38)` = **2,10:1**; `#0284c7` sobre `#e0f2fe` = **3,57:1**. O mínimo AA é 4,5:1 para texto normal e 3:1 para texto grande e componentes | 1.4.3 Contraste (mínimo); 1.4.11 Contraste de elementos não textuais |
| k | **Atributo `lang` ausente** em `password_reset_complete.html`, `password_reset_confirm.html`, `password_reset_done.html` e na janela de impressão gerada em `bolsista_dashboard.html:1137`. O `aria-label="Close"` dos alertas está em inglês em página declarada como `pt-br` | 3.1.1 Idioma da página; 3.1.2 Idioma de partes |
| l | **As mensagens novas do chat são inseridas via `innerHTML`/`appendChild`** (`chats.js:173-183`) **sem região `aria-live`**: quem usa leitor de tela não é avisado de que chegou mensagem | 4.1.3 Mensagens de status |
| m | **42 declarações de `font-size` em px** e ausência de verificação de redimensionamento: é preciso testar zoom de 200% e 400% e largura de 320px | 1.4.4 Redimensionar texto; 1.4.10 Refluxo |
| n | Na busca visual, textos alternativos pouco informativos: `alt="Padrão"`, `alt="Preview"`, `alt="Escaneando..."` (`visual_search.html:547`, `591`, `614`) e 1 imagem sem `alt` (`edit_profile.html:36`) | 1.1.1 |
| o | **Não há declaração de acessibilidade nem símbolo de acessibilidade** na interface (0 ocorrências de recursos desse tipo) | Exigência do art. 63 da LBI |

**Barreiras encontradas no aplicativo móvel** (13 telas, 17 componentes):

| # | Situação medida | Critério / norma |
|---|---|---|
| p | **Nenhuma propriedade de acessibilidade em todo o aplicativo:** 0 ocorrências de `accessibilityLabel`, `accessibilityRole`, `accessibilityHint` e `accessible` em 213 `TouchableOpacity` e 18 `Pressable`. Para o TalkBack e o VoiceOver, a maioria dos controles não tem nome nem função | NBR 17060 (controle e interação); 4.1.2 |
| q | **30 controles contêm apenas um ícone** (`Ionicons`) e nenhum tem rótulo: notificações e avatar (`HomeHeader.jsx:29,38`), filtro (`SearchBar.jsx:108`), câmera da busca visual (`Busca.jsx:341`), voltar (`CadastrarItem.jsx:186`), remover foto (`CadastrarItem.jsx:218`), atualizar (`Chat.jsx:113`) | 1.1.1; 4.1.2 |
| r | **O `placeholder` é usado como rótulo** nos campos (`Login.jsx`: `placeholder={label}`), nos 19 campos de texto do aplicativo. O rótulo desaparece quando a pessoa digita | 3.3.2; 2.4.6 |
| s | **11 componentes `<Image>` sem rótulo acessível**, incluindo fotos de itens (`Busca.jsx:96,498`) e avatar (`HomeHeader.jsx:44`) | 1.1.1 |
| t | **207 valores de `fontSize` fixos** e alturas fixas em vários contêineres: é preciso testar o aplicativo com a fonte do sistema ampliada e verificar se o texto é cortado | 1.4.4; NBR 17060 |
| u | **78 medidas de largura/altura abaixo de 44** em componentes tocáveis: indício de alvos pequenos. Verifique manualmente contra o mínimo de 24×24 px CSS do critério 2.5.8 (AA) e, como boa prática, os 44×44 do critério 2.5.5 (AAA) e das recomendações das plataformas | 2.5.8 Tamanho do alvo (mínimo) |
| v | **48 chamadas de `Alert.alert`** como único retorno de erro e `userInterfaceStyle: "automatic"` no `app.json` **sem nenhum uso de `useColorScheme`**: o tema anunciado não é realmente aplicado | 4.1.3; 1.4.3 |

### 2.2 Lista de pendências

- **Prioridade 1:** infraestrutura de avaliação. Sem isso você não tem dados, e **nada pode ser corrigido antes da primeira medição**.
- **Prioridade 2:** correções da web.
- **Prioridade 3:** correções do aplicativo e avaliação com usuários.

Crie uma *issue* por item, com a etiqueta `acessibilidade`, citando o critério de sucesso envolvido. Assim a própria lista vira dado do processo e o seu histórico de *commits* mostra a relação entre barreira e correção.

#### Prioridade 1 – Infraestrutura de avaliação (antes de corrigir qualquer coisa)

| # | O que fazer | Por quê |
|---|---|---|
| 1 | **Definir e escrever o protocolo de avaliação** antes de medir: páginas da amostra, perfis de usuário cobertos (comum, bolsista, administrador), estados da tela (vazio, com erro, carregando), navegadores, leitores de tela e versões, nível-alvo (AA) e critérios de severidade | É o que separa um trabalho publicável de um relatório de ferramenta. Siga a WCAG-EM (seção 3.4) |
| 2 | **Coletar a avaliação "antes"** com axe, WAVE, Lighthouse e ASES em todas as páginas da amostra, salvando os relatórios brutos (JSON/HTML) no repositório, com data e *hash* do commit | São os dados da sua QP1 e da comparação antes/depois. Depois de corrigir, não há como voltar atrás |
| 3 | **Fazer a inspeção manual "antes"**: navegação só por teclado em cada fluxo, teste com leitor de tela (NVDA no Windows, TalkBack no Android), zoom de 200% e 400%, largura de 320px, verificação de contraste e os critérios novos da WCAG 2.2 | Ferramentas automáticas não detectam ordem de foco, qualidade do texto alternativo, nem a maioria dos critérios novos |
| 4 | **Guardar os scripts e planilhas de coleta** no repositório (por exemplo, em `docs/acessibilidade/`), com inventário de barreiras em formato tabular (ID, página, critério, severidade, método que detectou, evidência, status) | Permite reproduzir os números do artigo e é a base de todas as tabelas dos Resultados |
| 5 | **Automatizar a verificação no CI**: o repositório web não tem nenhum *workflow* ativo hoje. Crie um no GitHub Actions rodando testes automatizados de acessibilidade (por exemplo, axe-core via Playwright ou Selenium, e/ou Lighthouse CI) nas páginas principais, a cada *push* | Transforma acessibilidade em requisito contínuo e rende um resultado próprio: "as regressões passaram a ser detectadas automaticamente" |
| 6 | **Criar a amostra de páginas e de telas** de forma justificada: as páginas mais acessadas, mais os fluxos completos (cadastrar item, buscar, conversar no chat, confirmar devolução) | A WCAG-EM exige amostragem explícita; sem isso o revisor não sabe o que foi avaliado |

#### Prioridade 2 – Correções no cliente web

| # | O que fazer |
|---|---|
| 7 | Adicionar link "pular para o conteúdo principal" no `base.html`, visível ao receber foco, e uma classe utilitária para conteúdo exclusivo de leitores de tela (item **a**) |
| 8 | Garantir um `<h1>` por página e revisar a hierarquia de cabeçalhos sem saltos de nível (item **b**) |
| 9 | Associar todos os rótulos aos campos (`for`/`id`), mantendo o `placeholder` apenas como exemplo, nunca como rótulo; revisar `autocomplete` nos campos de identificação (itens **c** e critério 1.3.5) |
| 10 | Marcar todos os ícones decorativos com `aria-hidden="true"` e dar nome acessível aos 9 controles que são só ícone (itens **d** e **e**) |
| 11 | Corrigir as tabelas dos painéis: `scope` nos `<th>`, `caption` descritiva e revisão de tabelas usadas para leiaute, se houver (item **f**) |
| 12 | Dar nome acessível aos diálogos (`aria-labelledby` apontando para o título), garantir retorno do foco ao fechar e fechamento por `Esc`, testando o comportamento real do Bootstrap 5.3 (item **g**) |
| 13 | Refazer o estilo de foco: remover os `outline: none` sem substituto e definir um indicador de foco visível e consistente com `:focus-visible` em toda a interface (item **h**) |
| 14 | Revisar a paleta para atingir 4,5:1 em texto e 3:1 em componentes, **mantendo a identidade visual** do projeto: proponha os novos valores de cor em um quadro antes/depois com as relações de contraste calculadas (item **j**). Esse quadro é um ótimo resultado para o artigo |
| 15 | Corrigir `lang` nas páginas que não declaram idioma, traduzir os rótulos em inglês e marcar termos estrangeiros com `lang` quando fizer sentido (item **k**) |
| 16 | Anunciar as mensagens novas do chat e os demais retornos dinâmicos por região `aria-live` adequada (item **l**) |
| 17 | Adicionar `@media (prefers-reduced-motion: reduce)` desativando animações e transições (item **i**) |
| 18 | Revisar textos alternativos: descritivos para imagens informativas, `alt=""` para decorativas, e alternativa textual para os resultados da busca por imagem (item **n**) |
| 19 | Criar uma **página de declaração de acessibilidade** (o que foi implementado, o nível alcançado, as limitações conhecidas e um canal de contato) e incluir o símbolo de acessibilidade em destaque, como pede o art. 63 da LBI (item **o**) |
| 20 | Validar o HTML gerado (validador do W3C) nas páginas da amostra e corrigir erros que afetem a semântica, como `id` duplicado dentro dos laços de modais |

#### Prioridade 3 – Correções no aplicativo e avaliação com usuários

| # | O que fazer |
|---|---|
| 21 | Adicionar `accessibilityLabel`, `accessibilityRole` e, quando necessário, `accessibilityHint` e `accessibilityState` a todos os controles, começando pelos 30 que são só ícone (itens **p** e **q**) |
| 22 | Substituir o `placeholder` por rótulo visível associado em todos os campos, e associar a mensagem de erro ao campo correspondente (item **r**) |
| 23 | Dar rótulo às imagens informativas e marcar as decorativas como ocultas à acessibilidade (item **s**) |
| 24 | Testar o aplicativo com a fonte do sistema ampliada e corrigir cortes de texto, trocando alturas fixas por dimensionamento flexível (item **t**) |
| 25 | Ajustar os alvos de toque pequenos, usando `hitSlop` onde não for possível aumentar o componente (item **u**) |
| 26 | Revisar o contraste das cores do aplicativo: branco sobre `#90dbf4` está em **1,54:1** e branco sobre `#6dcef0` em **1,79:1**, muito abaixo do mínimo; o placeholder do login está em **2,05:1** (item **v**) |
| 27 | Garantir que erros e estados de carregamento sejam anunciados pela tecnologia assistiva, e não apenas exibidos; implementar de fato o tema claro/escuro anunciado no `app.json` ou remover a configuração |
| 28 | Rodar o **Accessibility Scanner** (Android) e o **Accessibility Inspector** (Xcode, se houver acesso a iOS) em cada tela, e adotar um *linter* de acessibilidade para React Native no projeto |
| 29 | **Teste com usuários de tecnologia assistiva** (ver a seção 3.4 antes de começar): de 3 a 6 participantes, tarefas reais, antes e depois das correções, com taxa de conclusão, tempo, barreiras observadas e percepção. **Verifique com o orientador a necessidade de Comitê de Ética em Pesquisa (CEP) e de Termo de Consentimento Livre e Esclarecido (TCLE), com antecedência** |
| 30 | **Coletar a avaliação "depois"** repetindo exatamente o protocolo do item 1, com a mesma amostra, as mesmas ferramentas e as mesmas versões |

**Métricas sugeridas** (colete antes e depois, com data e *hash* do commit):

| Métrica | Como obter |
|---|---|
| Número de violações por página, por ferramenta | Relatórios do axe, WAVE, Lighthouse e ASES |
| Violações por critério de sucesso e por princípio (perceptível, operável, compreensível, robusto) | Inventário de barreiras |
| Violações por severidade e por tela | Inventário de barreiras |
| Nota de acessibilidade do Lighthouse e percentual do ASES | Relatórios das ferramentas |
| Barreiras detectadas por cada método e por mais de um método (sobreposição), além de falsos positivos confirmados manualmente | Comparação dos relatórios com a inspeção manual — **dados da QP2** |
| Critérios de sucesso em conformidade, não conformes e não aplicáveis, no nível AA | Avaliação segundo o protocolo |
| Relações de contraste das cores da paleta, antes e depois | Cálculo pela fórmula da WCAG ou ferramenta de contraste |
| Elementos com rótulo acessível / total de elementos interativos (web e aplicativo) | Script próprio sobre o código |
| Taxa de conclusão de tarefas e tempo por tarefa, com tecnologia assistiva | Teste com usuários |
| Violações impedidas pelo CI após a adoção | Histórico das execuções do *workflow* |

---

## 3. Orientações de escrita

Escreva o TCC no modelo ABNT, seguindo as [orientações gerais](../../README.md), mas pense no **artigo** desde o início. A regra de ouro do seu tema: **toda afirmação sobre acessibilidade precisa de evidência** — critério de sucesso citado, relatório de ferramenta, captura de tela, número medido ou referência. Frases como "o sistema ficou acessível" ou "a interface agora é inclusiva", sem conformidade medida e sem o nível declarado, são cortadas pelos revisores.

Cuidado com dois erros comuns neste tema: tratar "acessibilidade" como sinônimo de usabilidade e falar de pessoas com deficiência de forma capacitista. Use a linguagem dos documentos oficiais ("pessoa com deficiência"), evite "portador" e "deficiente", e não trate a acessibilidade como favor ou caridade: é direito, previsto em lei.

### 3.1 Introdução

- **Contextualização:**
  - pesquise dados sobre a população com deficiência no Brasil (Censo Demográfico do IBGE e Pesquisa Nacional de Saúde) e sobre acesso à internet e uso de dispositivos móveis (pesquisa TIC Domicílios, do Cetic.br/NIC.br) e fale sobre o tamanho do público afetado;
  - fale sobre a digitalização de serviços institucionais: quando um serviço só existe em um sistema web ou aplicativo, a barreira digital vira exclusão do serviço;
  - apresente o domínio (achados e perdidos em instituição de ensino) apenas como **cenário** do caso avaliado.
- **Problemática:** o problema do trabalho é a **barreira de acesso**.
  - Fale sobre a baixa conformidade de sítios brasileiros com as diretrizes de acessibilidade, trazendo dados de estudos publicados (há vários no SOL, com universidades federais e portais de governo);
  - fale sobre a causa recorrente: acessibilidade tratada como ajuste posterior, e não como requisito, em equipes sem formação específica. O FIND é exatamente esse caso, e você tem os números da seção 2 para mostrar isso;
  - fale sobre a existência de obrigação legal descumprida (art. 63 da LBI) e sobre o risco de que soluções novas nasçam inacessíveis;
  - use os exemplos do FIND só como ilustração. Os detalhes ficam para os Resultados.
- **Caminho para a solução:**
  - pesquise sobre as diretrizes WCAG, o eMAG e as normas ABNT de acessibilidade digital, e sobre os métodos de avaliação: automática, inspeção manual por especialista e teste com usuários;
  - fale sobre as **limitações das ferramentas automáticas**, com referência: elas cobrem apenas parte dos critérios e produzem falsos positivos, o que justifica a combinação de métodos que você adotou;
  - fale sobre desenho inclusivo e desenho universal como abordagem preventiva, e não corretiva;
  - cite estudos semelhantes de avaliação de conformidade e mostre a lacuna: a maioria avalia sítios de terceiros com ferramentas automáticas, **sem corrigir nada e sem reavaliar**. O seu diferencial é fechar o ciclo avaliação → correção → reavaliação em um sistema real, com acesso ao código, e incluir o aplicativo móvel.
- **Apresentação da solução:**
  - fale sobre o FIND (web em Django e aplicativo em React Native/Expo) e diga o que este trabalho faz: avalia a acessibilidade segundo a WCAG 2.2 no nível AA, combinando quatro ferramentas automáticas com inspeção manual e tecnologias assistivas; corrige as barreiras encontradas na interface; e reavalia, comparando o antes e o depois;
  - informe onde a plataforma está implantada (Render) e, se o teste com usuários acontecer, cite-o aqui, com o público e a forma de aplicação. **Não mencione avaliações que não aconteceram** — se o teste com usuários não for viável, diga isso nas limitações e não prometa no texto.
- **Vínculo com projetos:** fale sobre o histórico do FIND (desde novembro de 2025), a equipe e o projeto institucional a que ele pertence (confirme com o orientador). Como os repositórios têm vários autores e há outros TCCs no mesmo projeto, **deixe explícito qual é a sua contribuição** (a camada de interface e a avaliação de acessibilidade) e o que é escopo dos colegas.
- **Pergunta de pesquisa e contribuições:** feche a Introdução com a pergunta e as QPs (seção 1.4) e com uma lista curta de contribuições. Por exemplo: o inventário de barreiras de uma plataforma web e móvel real; a comparação entre quatro ferramentas automáticas (incluindo o ASES) e a inspeção manual; o conjunto de correções aplicadas com a medição antes e depois; e as lições aprendidas para equipes pequenas.

### 3.2 Objetivo geral

- Escreva uma frase, com um único verbo principal, coerente com a pergunta de pesquisa;
- o objeto do objetivo é a **acessibilidade da plataforma**, e não "desenvolver um sistema de achados e perdidos". Também não escreva "tornar o sistema acessível a todos": você não consegue comprovar isso;
- estrutura para você completar:

> "O objetivo principal do presente trabalho consiste em avaliar e adequar a acessibilidade [...] da plataforma FIND, em suas interfaces web e móvel, segundo [...], por meio de [...], comparando [...]."

### 3.3 Referencial Teórico

Explique somente os conceitos que aparecem depois nos Resultados. Detalhes de instalação e uso das ferramentas vão para Materiais e Métodos. Estrutura sugerida:

```
2 REFERENCIAL TEÓRICO
2.1 Acessibilidade digital e desenho inclusivo
2.2 Tecnologias assistivas
2.3 Marco legal e normativo brasileiro
2.4 Diretrizes WCAG 2.2
2.5 Avaliação de acessibilidade
2.6 Acessibilidade em aplicações móveis
2.7 Trabalhos relacionados
```

- **2.1 Acessibilidade digital e desenho inclusivo:** pesquise sobre os conceitos de acessibilidade e de deficiência (modelo médico *versus* modelo social, e a definição da Convenção sobre os Direitos das Pessoas com Deficiência), sobre desenho universal e desenho inclusivo, e sobre os tipos de deficiência e limitações (visual, auditiva, motora, cognitiva, além de limitações temporárias e situacionais). Relacione com a diferença entre acessibilidade e usabilidade.
- **2.2 Tecnologias assistivas:** pesquise e **explique como funcionam** os leitores de tela (NVDA, JAWS, TalkBack, VoiceOver), a navegação só por teclado, os ampliadores de tela, o reconhecimento de voz e os recursos de alto contraste e ampliação de fonte dos sistemas operacionais. É aqui que o leitor entende por que um botão sem nome acessível simplesmente não existe para quem usa leitor de tela. Use a analogia a seu favor: descreva o que o leitor de tela anuncia em um botão sem rótulo ("botão", e nada mais).
- **2.3 Marco legal e normativo brasileiro:** desenvolva o quadro da seção 1.3, com as fontes originais: LBI (art. 63), Decreto nº 5.296/2004, eMAG 3.1, ABNT NBR 17060:2022 e ABNT NBR 17225:2025. Explique a relação entre elas e a WCAG, e diga explicitamente qual instrumento você adotou como referência de conformidade e por quê.
- **2.4 Diretrizes WCAG 2.2:** pesquise sobre a estrutura das diretrizes (os quatro princípios — perceptível, operável, compreensível e robusto —, as diretrizes, os critérios de sucesso e os níveis A, AA e AAA), sobre o que significa conformidade e sobre os nove critérios novos da versão 2.2. Explique também o WAI-ARIA e os papéis, estados e propriedades, porque as suas correções usam isso. Cuidado: não reproduza a lista inteira de 86 critérios; detalhe apenas os que aparecem nos seus resultados.
- **2.5 Avaliação de acessibilidade:** pesquise sobre os métodos (avaliação automática, inspeção/avaliação por especialistas, percurso de barreiras, teste com usuários), sobre a **WCAG-EM** como metodologia de avaliação de conformidade, sobre as limitações e a cobertura das ferramentas automáticas e sobre métricas de acessibilidade. Esta seção é a base teórica da sua QP2.
- **2.6 Acessibilidade em aplicações móveis:** pesquise sobre as diferenças entre web e móvel (gestos, alvos de toque, orientação de tela, escala de fonte do sistema), sobre os requisitos da NBR 17060 e sobre as APIs de acessibilidade das plataformas e do React Native.
- **2.7 Trabalhos relacionados:** busque estudos de avaliação de acessibilidade, preferencialmente brasileiros e com método explícito. Termos de busca (use em português e em inglês):
  - `avaliação de acessibilidade AND WCAG`;
  - `acessibilidade web AND eMAG`;
  - `"automated accessibility evaluation" AND tools`;
  - `"accessibility barriers" AND "screen reader" AND "user study"`;
  - `"mobile accessibility" AND "React Native"`;
  - `"accessibility" AND "before and after" AND remediation`;
  - `WCAG 2.2 AND "success criteria" AND evaluation`.

  Termine a seção com um quadro comparativo usando critérios como: objeto avaliado (sítios de terceiros ou sistema próprio), diretrizes e versão adotadas, métodos empregados (automático, manual, com usuários), se houve correção e reavaliação, se incluiu aplicativo móvel e se usou o marco normativo brasileiro. O seu trabalho deve aparecer na última coluna, e a lacuna tem de ficar visível.

**Leituras de partida.** Localize a fonte original, confira os dados e só depois inclua nas Referências:

- W3C. *Web Content Accessibility Guidelines (WCAG) 2.2* (recomendação de 05/10/2023) e a tradução autorizada para o português;
- W3C. *Website Accessibility Conformance Evaluation Methodology (WCAG-EM) 1.0*;
- W3C. *Accessible Rich Internet Applications (WAI-ARIA)* e o *ARIA Authoring Practices Guide*;
- BRASIL. Lei nº 13.146, de 6 de julho de 2015 (LBI), e Decreto nº 5.296, de 2 de dezembro de 2004;
- BRASIL. *eMAG – Modelo de Acessibilidade em Governo Eletrônico*, versão 3.1. Brasília: MP/SLTI, 2014;
- ABNT. NBR 17060:2022 – *Acessibilidade em aplicativos de dispositivos móveis: requisitos*;
- ABNT. NBR 17225:2025 – *Acessibilidade em conteúdo e aplicações web: requisitos*;
- IBGE. dados do Censo Demográfico e da Pesquisa Nacional de Saúde sobre pessoas com deficiência;
- CETIC.br/NIC.br. *TIC Domicílios*, edição mais recente;
- estudos sobre a cobertura e a confiabilidade de ferramentas automáticas de avaliação (procure por Vigo, Brown e Conway; e por Brajnik, no tema de métodos e métricas de avaliação);
- HENRY, S. L. *Just Ask: Integrating Accessibility Throughout Design*, para o planejamento de testes com pessoas com deficiência;
- LAZAR, J.; GOLDSTEIN, D.; TAYLOR, A. *Ensuring Digital Accessibility through Process and Policy*;
- artigos brasileiros de avaliação de acessibilidade publicados no IHC, no SBSI e no SBQS (SBC OpenLib);
- documentação oficial: WebAIM (WAVE), Deque (axe-core), Google (Lighthouse), Governo Digital (ASES), React Native (*Accessibility*), Bootstrap (*Accessibility*) e Django.

### 3.4 Metodologia

- **Classificação da pesquisa:** fale sobre a natureza aplicada, os objetivos exploratórios e descritivos e a abordagem quali-quantitativa (contagens de violações e relações de contraste, de um lado; análise das barreiras e da experiência de uso, de outro). Nos procedimentos, fale sobre a pesquisa bibliográfica, a pesquisa documental (normas e diretrizes) e o **estudo de caso único** com intervenção (avaliação, correção e reavaliação). Combine com o orientador a terminologia: se preferir, "pesquisa-ação" descreve bem o ciclo diagnosticar–intervir–avaliar. Seja consistente do início ao fim do texto.
- **Protocolo de avaliação (o coração da sua Metodologia).** Descreva, de forma que outra pessoa consiga repetir:
  - **escopo:** quais URLs e quais telas do aplicativo, por perfil de usuário, e por que essa amostra representa a plataforma;
  - **base de conformidade:** WCAG 2.2, nível AA (declare o nível!), e como o eMAG e as normas ABNT entram;
  - **ferramentas e versões**, com a data de cada execução;
  - **procedimento manual:** roteiro de navegação por teclado, leitor de tela usado e versão, zoom e largura testados, e a lista de critérios verificados manualmente;
  - **classificação das barreiras:** como você definiu severidade (por exemplo, impede a tarefa / dificulta / incomoda) e como resolveu divergências entre ferramentas;
  - **tratamento de falsos positivos:** toda violação automática foi confirmada manualmente? Diga como.
- **Pesquisa bibliográfica:** informe as bases consultadas, os termos de busca (seção 3.3), o período das publicações e os critérios de inclusão e exclusão.
- **Etapas:** descreva em ordem cronológica, com uma figura do fluxo:
  1. revisão da literatura e estudo das diretrizes e normas;
  2. definição do protocolo e da amostra;
  3. avaliação inicial automática (axe, WAVE, Lighthouse e ASES);
  4. inspeção manual e teste com tecnologias assistivas;
  5. consolidação do inventário de barreiras, com classificação por critério e severidade;
  6. implementação incremental das correções na web e no aplicativo;
  7. automatização da verificação no CI;
  8. reavaliação com o mesmo protocolo e comparação antes/depois;
  9. se houver, teste de tarefas com usuários de tecnologia assistiva;
  10. análise dos resultados e das lições aprendidas.
- **Teste com usuários (se houver).** Planeje com cuidado e com antecedência:
  - **ética primeiro:** verifique com o orientador a necessidade de submissão ao CEP e use TCLE. Nunca divulgue dados que identifiquem os participantes (LGPD);
  - recrutamento: de 3 a 6 participantes que **usem tecnologia assistiva no dia a dia**, e não colegas simulando deficiência. Se você precisar simular (por exemplo, navegar com a tela desligada), diga claramente que foi simulação e trate como limitação;
  - tarefas reais e curtas (cadastrar um item perdido, buscar um item, iniciar uma conversa), com medidas de taxa de conclusão, tempo, barreiras observadas e comentários em voz alta;
  - instrumento de percepção, se couber (por exemplo, o System Usability Scale, com a ressalva de que ele mede usabilidade percebida, não conformidade).
- **Ameaças à validade:** o artigo precisa dessa subseção. Fale sobre:
  - a amostra de páginas, que pode não cobrir todas as barreiras;
  - a participação do autor como avaliador e como implementador das correções, o que gera viés: descreva como mitigou (protocolo escrito antes, relatórios brutos guardados, revisão do orientador);
  - a avaliação de acessibilidade depender de julgamento humano, especialmente nos critérios manuais, e você ser um avaliador iniciante — há literatura sobre inspeções feitas por avaliadores novatos: cite-a;
  - o número pequeno de participantes, se houver teste com usuários;
  - versões de ferramentas, navegadores e leitores de tela, que mudam resultados ao longo do tempo;
  - conformidade técnica não garantir uma boa experiência de uso.

### 3.5 Materiais e Métodos

**Materiais.** Monte o quadro-resumo com as versões **efetivamente usadas**, conferidas na data da escrita. Um modelo para você completar:

| Ferramenta | Versão | Finalidade no trabalho |
|---|---|---|
| axe DevTools / axe-core | a conferir | Avaliação automática no navegador e no CI |
| WAVE (WebAIM) | a conferir | Avaliação automática com apoio visual na página |
| Lighthouse | a conferir | Auditoria automática e nota de acessibilidade |
| ASES (Governo Digital) | a conferir | Avaliação segundo o eMAG; **verifique a disponibilidade e o funcionamento da ferramenta na data da coleta e registre isso no texto** |
| NVDA | a conferir | Leitor de tela (Windows) na inspeção manual |
| TalkBack / VoiceOver | a conferir | Leitor de tela no aplicativo (Android / iOS) |
| Accessibility Scanner / Accessibility Inspector | a conferir | Verificação de acessibilidade no aplicativo |
| Validador de HTML do W3C | – | Conformidade do código gerado |
| Ferramenta de contraste (por exemplo, TPGi Colour Contrast Analyser) | a conferir | Cálculo das relações de contraste |
| Navegadores usados nos testes | a conferir | Ambiente de avaliação |
| Django / Bootstrap | 6.0.3 / 5.3 | Tecnologias da interface web corrigida |
| React Native / Expo | 0.81.5 / SDK 54 | Tecnologias do aplicativo corrigido |
| Playwright ou Selenium + axe-core | a conferir | Testes automatizados de acessibilidade no CI |
| GitHub Actions | – | Execução contínua das verificações |
| Git e GitHub | – | Versionamento e registro das *issues* e dos *pull requests* |

**Métodos.** Para cada item, explique o que é, para que foi usado e por que foi escolhido. Em especial:

- **por que quatro ferramentas automáticas, e não uma:** explique que elas usam conjuntos de regras diferentes e que a comparação é objeto da QP2;
- **como a inspeção manual foi conduzida:** roteiro, critérios verificados, quantas passagens;
- **como as correções foram implementadas:** em incrementos pequenos, uma *issue* por barreira, com *pull request* referenciando o critério de sucesso;
- **como a reavaliação garantiu comparabilidade:** mesma amostra, mesmas ferramentas, mesmas versões, mesmo procedimento;
- **como os dados foram analisados:** contagens, distribuição por critério e princípio, sobreposição entre métodos.

> **Dica para o artigo:** aqui vale a analogia da receita de bolo das orientações gerais. Dizer "foi usado o axe" é como dizer "usei farinha". O revisor precisa saber a versão, em que páginas, em que data, com qual navegador, com que configuração e como os resultados foram tratados — senão ninguém reproduz o seu estudo.

### 3.6 Resultados (e Discussão)

Organize o capítulo pelas questões de pesquisa, e não por telas. Estrutura sugerida:

- **Caracterização da avaliação (contexto):** a amostra de páginas e telas, o protocolo aplicado e as datas das coletas. Uma figura com o fluxo ajuda.
- **Barreiras encontradas (QP1):**
  - quadro com o inventário de barreiras: identificador, página/tela, critério de sucesso, princípio, severidade, método que detectou e evidência;
  - gráficos de distribuição: violações por princípio, por critério, por severidade e por tela;
  - destaque as barreiras **bloqueantes**, as que impedem a tarefa (por exemplo, enviar uma mensagem no chat com um botão sem nome acessível, ou operar o aplicativo inteiro sem rótulos);
  - use capturas com o leitor de tela para mostrar o que é anunciado. Isso comunica o problema muito melhor do que uma lista de códigos de erro.
- **Comparação entre os métodos de avaliação (QP2):**
  - tabela com o número de barreiras detectadas por axe, WAVE, Lighthouse, ASES, inspeção manual e teste com usuários;
  - diagrama ou tabela de sobreposição: quantas foram detectadas por todas, quantas por apenas uma, quantas **somente** pela inspeção manual;
  - falsos positivos confirmados;
  - discussão: quais tipos de barreira cada método encontra bem e quais escapam (especialmente os critérios novos da WCAG 2.2). **Esta é a seção mais publicável do seu trabalho.**
- **Correções aplicadas e efeito medido (QP3):**
  - quadro de correções: barreira, critério, o que foi alterado (arquivo/componente) e resultado;
  - tabela antes/depois por critério e por ferramenta, com a variação;
  - quadro da paleta de cores antes e depois, com as relações de contraste calculadas;
  - mostre um exemplo curto de código antes e depois (por exemplo, um campo de formulário sem rótulo associado e o mesmo campo corrigido), seguindo as regras de apresentação de código das orientações gerais;
  - resultado do CI: o que passou a ser detectado automaticamente.
- **Resultados do teste com usuários (se houver):** taxa de conclusão e tempo por tarefa, antes e depois; barreiras relatadas; citações curtas e anonimizadas das falas.
- **Barreiras remanescentes:** seja honesto e liste o que não foi corrigido e por quê (dependência de terceiros, limitação de tempo, decisão de projeto). Declare o nível de conformidade alcançado **com precisão**: "conformidade com o nível AA nas páginas da amostra, exceto nos critérios X e Y" é uma afirmação defensável; "o sistema é acessível" não é.
- **Lições aprendidas:** numere (L1, L2...) e associe cada uma a uma evidência. Temas possíveis: o custo de corrigir depois *versus* projetar desde o início; barreiras que nenhuma ferramenta automática apontou; o efeito de colocar a verificação no CI; o que um componente de terceiros (Bootstrap, biblioteca de ícones) resolve e o que ele não resolve.
- **Discussão:** relacione os resultados com o Referencial Teórico e com os trabalhos relacionados (os seus números de conformidade são comparáveis aos dos estudos brasileiros que você leu?) e aponte as limitações.

Cuidados:

- use poucas telas, e sempre com propósito: a mesma tela antes e depois, ou a tela com o foco visível, ou o que o leitor de tela anuncia. O artigo não é um catálogo de telas;
- não exponha dados reais de usuários, e-mails, senhas ou tokens em figuras, relatórios de ferramentas ou trechos de código;
- ao mostrar relatórios das ferramentas, recorte a área relevante e mantenha o texto legível;
- não transforme o capítulo em uma lista de saídas de ferramenta. Interprete: o que cada número significa para quem usa o sistema.

### 3.7 Conclusão

- Responda **diretamente** à pergunta de pesquisa e a cada QP;
- comente cada objetivo específico, na mesma ordem;
- retome as principais contribuições e as lições aprendidas;
- apresente as limitações com honestidade: amostra de páginas, papel duplo do autor como avaliador e desenvolvedor, número de participantes, barreiras remanescentes e o fato de a conformidade técnica não garantir uma boa experiência;
- sugira trabalhos futuros, por exemplo: avaliação com um número maior de participantes e mais perfis de deficiência; acessibilidade dos documentos e dos conteúdos gerados pelos usuários; inclusão de acessibilidade no processo de desenvolvimento da equipe desde o requisito; avaliação do impacto das correções sobre o uso real da plataforma.

### 3.8 Objetivos específicos

Serão entregues no final, junto com o Resumo, para refletirem o que foi **realmente feito**. Siga as regras das orientações gerais: 3 a 5 itens, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Verbos e temas que combinam com este trabalho:

- **revisar** a literatura sobre acessibilidade digital, diretrizes e métodos de avaliação;
- **definir** o protocolo de avaliação e a amostra ...;
- **avaliar** a acessibilidade da plataforma ... por meio de ferramentas automáticas e inspeção manual;
- **comparar** os resultados obtidos pelos diferentes métodos de avaliação;
- **corrigir** / **adequar** as barreiras identificadas conforme ...;
- **reavaliar** a plataforma e **comparar** os resultados antes e depois;
- **avaliar** o uso com usuários de tecnologia assistiva (somente se acontecer).

Não transforme funcionalidades do sistema em objetivos (por exemplo, "permitir a navegação por teclado" não é objetivo específico: é resultado de uma correção).

### 3.9 Resumo e *Abstract*

- **Tamanho:** no TCC, parágrafo único com 150 a 500 palavras (NBR 6028:2021). No artigo, siga o limite da chamada. Os veículos da seção 1.5 exigem resumo em português e em inglês;
- **Sequência:** contexto (acessibilidade como direito e obrigação legal), problema, objetivo, método (ferramentas, inspeção manual, nível de conformidade adotado), principais resultados **com números** (quantas barreiras, quais critérios, variação antes/depois) e principal conclusão;
- **Palavras-chave possíveis:** acessibilidade digital; WCAG 2.2; avaliação de acessibilidade; tecnologia assistiva; desenvolvimento web; aplicativos móveis.

### 3.10 Do TCC ao artigo

- **Estrutura típica deste tipo de artigo:** Introdução; Fundamentação e trabalhos relacionados; Método de avaliação; Resultados (barreiras, comparação entre métodos, antes e depois); Discussão e lições aprendidas; Ameaças à validade; Conclusão;
- **Modelo:** use o exigido pela chamada (em geral, o modelo da SBC, também disponível no Overleaf);
- **Acessibilidade do próprio artigo:** é uma marca de coerência no seu tema. Garanta texto alternativo nas figuras, não use cor como única forma de distinguir séries nos gráficos, verifique o contraste das figuras e gere um PDF com texto selecionável e estruturado;
- **Revisão às cegas:** se for o caso, retire da versão submetida os nomes, a instituição e os links dos repositórios;
- **Licença, autoria e divulgação:** o README do projeto declara licença proprietária. Antes de publicar trechos de código ou capturas de tela, confirme com a equipe e com o orientador o que pode ser divulgado. Divulgar barreiras de acessibilidade é legítimo e é o objeto do trabalho, mas **não divulgue falhas de segurança** que você encontrar de passagem: avise a equipe e o orientador em privado. Defina a autoria do artigo antes da submissão;
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

**Alinhamento sugerido das implementações.** É uma recomendação; os prazos oficiais são os da tabela acima. No seu trabalho essa ordem é especialmente importante, porque **a avaliação inicial precisa estar pronta antes de qualquer correção** — se você corrigir primeiro, perde o "antes" e o trabalho perde o eixo.

| Até | O que deve estar pronto | Por quê |
|---|---|---|
| 18/09/2026 | Protocolo de avaliação escrito e amostra definida (itens 1 e 6); *issues* de acessibilidade criadas | O protocolo orienta a Introdução e garante que a medição inicial seja válida |
| 28/09/2026 | **Avaliação "antes" concluída**: relatórios automáticos das quatro ferramentas e inspeção manual, com o inventário de barreiras consolidado e guardado no repositório (itens 2 a 4) | Depois de corrigir não há como recuperar esses dados. É também o insumo da Metodologia |
| 12/10/2026 | Correções da web (itens 7 a 20) e CI de acessibilidade funcionando (item 5) | Materiais e Métodos descreve as ferramentas e o procedimento já executados |
| 26/10/2026 | Correções do aplicativo (itens 21 a 28), **reavaliação concluída** (item 30) e, se houver, teste com usuários (item 29) | Os Resultados só podem ser escritos com os números do "depois" fechados |

Se o teste com usuários depender de Comitê de Ética, **inicie o processo na primeira semana**: o prazo de tramitação pode ser maior que o do seu cronograma. Se não for viável no tempo do TCC, combine com o orientador para tratá-lo como trabalho futuro, e não como promessa no texto.

Antes de cada envio, use o [checklist das orientações gerais](../../README.md#checklist-antes-de-enviar-uma-versão-ao-orientador).
