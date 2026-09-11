# Orientações de Escrita e Prazos – Gabryell Gonçalves (Projeto FIND)

Este documento reúne as orientações individuais do trabalho acadêmico do Gabryell Gonçalves. Ele complementa as [orientações gerais](../../README.md), que continuam valendo para a estrutura do trabalho, a formatação ABNT, as citações, as referências, as figuras e as tabelas.

> **Importante:** a análise dos repositórios foi feita em 11/09/2026 (web: commit `e2f364a`; mobile: commit `7c99848`). A análise da arquitetura geral da plataforma está nas [orientações do João Gabriel](joao_gabriel.md), que trabalha no mesmo projeto. Aqui aparece apenas o que interessa à correspondência automática. Sempre prevalecem os acordos feitos com o orientador.

## Sumário

- [1. Temática do trabalho](#1-temática-do-trabalho)
- [2. O que falta implementar](#2-o-que-falta-implementar)
- [3. Orientações de escrita](#3-orientações-de-escrita)
- [4. Prazos](#4-prazos)

---

## 1. Temática do trabalho

### 1.1 Tema e recorte

**Tema:** correspondência automática entre itens perdidos e encontrados.

**Recorte:** recuperação de informação e inteligência artificial aplicada. É o recorte mais técnico e algorítmico entre os temas do FIND e o de maior potencial de novidade. O trabalho **não** é um manual do sistema FIND nem uma descrição de telas. Ele transforma uma evolução já prevista no projeto (a correspondência automática e a geolocalização) na contribuição central: um mecanismo que, a partir de um objeto cadastrado como **perdido**, sugere os objetos cadastrados como **encontrados** com maior chance de serem o mesmo objeto (e vice-versa). Para isso, combina três fontes de evidência:

- **similaridade textual** entre título, descrição e local, com técnicas léxicas e *embeddings* (processamento de linguagem natural);
- **similaridade visual** entre as imagens enviadas (visão computacional);
- **proximidade geográfica e temporal**, a partir das coordenadas e das datas dos cadastros.

**Título provisório** (o título definitivo é a última informação a ser definida): *Correspondência multimodal entre itens perdidos e encontrados: avaliação de similaridade textual, visual e geográfica na plataforma FIND*.

> O trabalho do João Gabriel trata da **arquitetura** da plataforma; o seu trata do **algoritmo** e da sua avaliação. No seu artigo, a plataforma aparece apenas como cenário e como local de integração do protótipo.

### 1.2 Ponto de partida: o que o FIND já tem

A correspondência automática é tratada como evolução futura, mas o código já tem as primeiras peças. Isso **é uma vantagem**: a heurística existente vira a **linha de base** (*baseline*) que as técnicas propostas precisam superar.

| O que existe | Onde está | Como funciona | Limitações para a pesquisa |
|---|---|---|---|
| Dados do item | `items/models.py` (modelo `Item`) | `titulo` (até 45 caracteres), `descricao` (até 200), `categoria` (6 categorias padrão, criadas pelo comando `criar_categorias`), `local` (texto livre, até 45), `data`, uma `imagem`, `latitude` e `longitude` (opcionais) e `status` | Textos curtos; uma única imagem por item; local em texto livre |
| "Smart Match" (criado em 25/06/2026, commit `a4fb324`) | Função `_calcular_match_score`, em `mainpage/views.py`, usada pela view `busca_visual` | Para cada item `perdido` do usuário, pontua os itens `achado`, `pendente_confirmacao` e `confirmado` de outros usuários: categoria igual (35 pontos) + proporção de palavras do título em comum (até 40) + proporção de palavras da descrição em comum (até 25). Mostra até 6 sugestões com pontuação ≥ 30 | Existe só na web, sem API; não usa imagem, localização nem data; não trata acentos, radicais nem sinônimos ("celular" e "smartphone" não combinam); é recalculada a cada acesso à página, comparando todos os perdidos com todos os achados; pesos definidos sem avaliação; sem testes |
| Busca visual por imagem (criada em 03/06/2026, commit `8bc9db3`) | Método `Item.buscar_por_imagem`, em `items/models.py`; rotas `/itens/busca-visual/` (web) e `/api/items/busca-visual/` (app) | Com a chave `GEMINI_API_KEY`, o Gemini 2.5 Flash descreve a foto em poucas palavras e o sistema procura itens que contenham **todas** essas palavras no título, na descrição ou no local. Sem a chave, ou sem resultados, usa o pHash (50%) combinado com a interseção de histogramas de cor HSV (50%), com pontuação mínima de 30 | É uma busca manual, não uma comparação entre perdidos e achados; não filtra por status (devolve também itens devolvidos); exigir todas as palavras torna a busca restritiva e, como o filtro já exige todas, praticamente todos os resultados recebem 100% e a ordenação não diferencia os itens; a resposta do Gemini varia entre execuções, o que prejudica a reprodutibilidade; o caminho alternativo reabre todas as imagens do banco a cada consulta |
| Hash perceptual do item | Campo `image_hash` (pHash 16×16, 256 bits), gerado ao salvar a imagem; comando `gerar_hashes` | Distância de Hamming entre os hashes | O pHash foi projetado para detectar **quase-duplicatas** (a mesma foto redimensionada ou comprimida), e não o mesmo objeto fotografado em outro ângulo, fundo ou iluminação, que é o caso real |
| Coordenadas | Web: mapa Leaflet no cadastro (`register_item.html`). App: botão "Marcar minha localização atual" (`CadastrarItem.jsx`) | O usuário marca um ponto no mapa (web) ou anexa a posição do aparelho (app) | A API descarta as coordenadas enviadas pelo app (ver itens 1 e 20 da seção 2) |
| Promessas na página inicial do app | `src/components/landing/BenefitsSection.jsx` | Anuncia um "algoritmo que cruza descrições e fotos para sugerir matches" e "notificações instantâneas quando alguém registrar um item que combina com o seu" | Nada disso existe hoje. **Não descreva essas funções no artigo como se já existissem** |

### 1.3 Pergunta de pesquisa

**Pergunta principal:** que técnicas — similaridade textual (NLP/*embeddings*) sobre as descrições, similaridade visual (visão computacional) sobre as imagens enviadas e proximidade por geolocalização — oferecem melhor precisão e revocação (*recall*) na sugestão de correspondências entre itens perdidos e encontrados?

Para que a pergunta possa ser respondida com evidências em um artigo, desdobre-a em questões de pesquisa (QP) menores (confirme com o orientador):

- **QP1:** qual o desempenho de cada fonte de evidência isolada (textual léxica, textual semântica, visual e geográfica) em comparação com a heurística atual do FIND?
- **QP2:** a combinação (fusão) das fontes supera a melhor fonte isolada? Qual estratégia de fusão funciona melhor?
- **QP3:** como o desempenho se comporta quando falta informação (item sem foto, sem coordenadas ou com descrição curta) e quando a comparação é entre modalidades diferentes (descrição do item perdido × foto do item achado)?
- **QP4:** qual o custo computacional (tempo de resposta, memória e custo de API) de cada configuração, e qual delas é viável na infraestrutura atual do FIND?

**Hipóteses** a confirmar ou refutar com os experimentos:

- **H1:** *embeddings* semânticos superam a contagem de palavras em comum, porque tratam sinônimos e paráfrases;
- **H2:** a fusão das fontes supera a melhor fonte isolada;
- **H3:** representações visuais aprendidas (por exemplo, CLIP) superam o pHash com histograma de cor quando o mesmo objeto é fotografado em condições diferentes.

> **Ponto de maior novidade:** na prática, quem perde um objeto raramente tem uma foto dele, enquanto quem acha costuma fotografá-lo. A comparação **cruzada** entre a descrição do item perdido e a foto do item achado (QP3) é pouco explorada em sistemas de achados e perdidos e merece destaque no artigo.

### 1.4 Formato e onde publicar

**Formato:** proposta e avaliação experimental de um protótipo do módulo de correspondência, contendo:

- um conjunto de dados de teste com gabarito, controlado (e, se possível, complementado por dados reais anonimizados);
- a heurística atual como linha de base e as estratégias comparadas;
- métricas de recuperação de informação (Recall@k, MRR e nDCG@k) e precisão/revocação/F1 no limiar de notificação;
- testes estatísticos de significância;
- estudo de ablação (retirar uma fonte de evidência por vez) e análise de robustez;
- medição do custo computacional;
- integração do protótipo à plataforma (web e app) como prova de viabilidade.

**Onde publicar.** Confira sempre a chamada vigente: prazos, trilhas, limite de páginas, modelo e se a revisão é às cegas.

- **ENIAC** – Encontro Nacional de Inteligência Artificial e Computacional (SBC, realizado junto com a BRACIS). O prazo de submissão costuma ficar no primeiro semestre; é provável que a edição de 2026 já esteja encerrada, então mire a edição de 2027 ou um periódico;
- **WebMedia** – Simpósio Brasileiro de Sistemas Multimídia e Web, adequado à recuperação multimodal;
- **SBBD** – Simpósio Brasileiro de Banco de Dados, e **KDMiLe** – *Symposium on Knowledge Discovery, Mining and Learning*;
- **STIL** – Simpósio Brasileiro de Tecnologia da Informação e da Linguagem Humana, se o foco pender para o texto em português;
- periódicos: **JIDM** (*Journal of Information and Data Management*, SBC), **RITA** (Revista de Informática Teórica e Aplicada), **JBCS** (*Journal of the Brazilian Computer Society*) e **RBCA** (Revista Brasileira de Computação Aplicada).

Os artigos dos eventos e periódicos da SBC estão na SBC OpenLib (SOL): https://sol.sbc.org.br. **Antes de começar a escrever, leia pelo menos três artigos experimentais publicados no ENIAC ou no WebMedia** para entender o formato esperado.

---

## 2. O que falta implementar

**Mantenha a arquitetura atual:** monólito Django com os apps `accounts`, `items`, `chats` e `iot`; API REST com JWT; app React Native/Expo; MySQL em produção; imagens no banco (`DatabaseStorage`); implantação no Render. **Não** crie microsserviços, banco vetorial ou nova infraestrutura. Na escala esperada do FIND (centenas a poucos milhares de itens), comparar vetores em memória com NumPy é suficiente, e essa escolha deve ser justificada no artigo.

### 2.1 Coordenação com o trabalho do João Gabriel

O mesmo repositório será refatorado pelo João Gabriel (camada de serviços, *serializers*, versionamento da API e integração contínua; itens 16, 17, 18 e 23 das [orientações dele](joao_gabriel.md#2-o-que-falta-implementar)). Para evitar conflitos:

- implemente a correspondência como um **serviço** dentro do app `items` (por exemplo, o pacote `items/matching/`), chamado pelas views web e pelas views da API, que é o mesmo padrão que ele vai adotar;
- trabalhe com *branches* e *pull requests* e combinem quem altera `mainpage/views.py` (view `busca_visual`) e `items/api/views.py`;
- os itens de segurança 1 a 4 das orientações dele (credenciais no histórico do Git, inclusive a chave do Gemini) precisam estar resolvidos antes de o repositório ser citado no artigo.

### 2.2 Visão geral do módulo proposto

```
Item cadastrado ou editado (perdido ou achado)
        │
        ▼
1. Representações ─────── texto normalizado, vetor do texto, vetor da imagem, pHash, coordenadas, data
        │
        ▼
2. Candidatos ─────────── status complementar, outro usuário, data compatível, exclui devolvidos
        │
        ▼
3. Pontuação por fonte ── s_texto, s_imagem, s_cruzada, s_geo, s_categoria (de 0 a 1)
        │
        ▼
4. Fusão ──────────────── soma ponderada (com fontes ausentes) ou Reciprocal Rank Fusion
        │
        ▼
5. Ranking e limiar ───── k melhores sugestões; notificação acima do limiar
        │
        ▼
6. Registro e retorno ─── sugestão guardada; usuário confirma ou rejeita
```

### 2.3 Lista de pendências

- **Prioridade 1:** base do experimento. Sem ela não há Resultados.
- **Prioridade 2:** técnicas comparadas. É o núcleo do artigo.
- **Prioridade 3:** integração do protótipo à plataforma. Se o tempo apertar, garanta a API e uma tela no app e deixe as notificações como desejáveis.

Crie uma *issue* no GitHub para cada item.

#### Prioridade 1 – Dados, gabarito e avaliação

| # | Situação encontrada | O que fazer |
|---|---|---|
| 1 | `api_create_item` e `api_edit_item` (`items/api/views.py`) **ignoram** `latitude` e `longitude`, embora o app as envie (`CadastrarItem.jsx`). Todo item cadastrado pelo app fica sem coordenadas. Além disso, `_item_to_dict` não devolve esses campos, então o mapa de `DetalheItem.jsx` nunca aparece. A edição web (`edit_item`) também não atualiza as coordenadas | Gravar as coordenadas na criação e na edição (validando as faixas de −90 a 90 e de −180 a 180), devolvê-las na API e permitir alterá-las na edição web |
| 2 | Não há conjunto de dados nem gabarito (quais pares perdido–achado são o mesmo objeto) | Montar o conjunto de avaliação seguindo o protocolo da seção 2.4 e guardá-lo em `avaliacao/`, na raiz do repositório web. As imagens podem ficar fora do Git (por exemplo, Git LFS ou Zenodo), com um script de download |
| 3 | Não há script de avaliação nem métricas | Criar um comando, por exemplo `python manage.py avaliar_correspondencia --estrategia <nome> --dados <pasta>`, que ordene os candidatos de cada item consulta e calcule as métricas da seção 2.5 e o tempo por consulta. Grave os resultados em CSV, com a data, o *hash* do commit, as versões dos modelos e a semente aleatória |
| 4 | A heurística atual (`_calcular_match_score`) está dentro da view, misturada à renderização da página, e não tem testes | Extraí-la **sem mudar o comportamento** para `items/matching/`, como estratégia **B0** (linha de base), com testes unitários. Ela aparece em todas as tabelas do artigo |
| 5 | Não existe um contrato comum entre estratégias | Definir uma interface única: cada estratégia recebe um item consulta e uma lista de candidatos e devolve uma pontuação entre 0 e 1 para cada candidato, além do seu nome e versão. Assim, o script do item 3 avalia qualquer estratégia da mesma forma |

#### Prioridade 2 – Técnicas a comparar

Rode os experimentos localmente ou no Google Colab. A decisão sobre o que vai para produção sai dos resultados da QP4 (ver "Cuidados", abaixo).

| # | Estratégia | O que implementar |
|---|---|---|
| 6 | **T1 – Textual léxica** | Normalização do texto (minúsculas, remoção de acentos, *stopwords* do português e radicalização com o RSLP, disponível no NLTK) e TF-IDF com similaridade do cosseno (scikit-learn) ou BM25 (por exemplo, `rank-bm25`) sobre título, descrição e local. A comparação com a B0 mostra o ganho obtido só com o tratamento do texto |
| 7 | **T2 – Textual semântica** | *Embeddings* de sentenças multilíngues (por exemplo, `paraphrase-multilingual-MiniLM-L12-v2` ou `multilingual-e5-small`, via `sentence-transformers`) e similaridade do cosseno. Trata sinônimos e paráfrases ("celular" × "smartphone", "garrafa" × "squeeze"). Opcional: comparar com um *embedding* obtido por API externa, discutindo custo e reprodutibilidade |
| 8 | **V0 – Visual atual** | Reaproveitar o pHash e o histograma HSV já existentes como estratégia, comparando a imagem do item perdido com a do item achado |
| 9 | **V1 – Visual com *embeddings*** | Vetores de imagem de um modelo pré-treinado, como o CLIP (por exemplo, `clip-ViT-B-32`, via `sentence-transformers`) ou o DINOv2 (via `transformers`), com similaridade do cosseno |
| 10 | **X1 – Cruzada (texto × imagem)** | Com um CLIP multilíngue (por exemplo, `clip-ViT-B-32-multilingual-v1`), comparar a **descrição** do item perdido com a **foto** do item achado. É o caso mais comum na prática e o ponto de maior potencial de novidade |
| 11 | **G1 – Geográfica e temporal** | Distância de Haversine entre as coordenadas, convertida em pontuação com decaimento (por exemplo, `exp(−d/σ)`, com σ calibrado). Sem coordenadas, usar a similaridade textual do campo `local` ou uma pontuação neutra. Filtro temporal: descartar ou penalizar itens achados com data muito anterior à da perda (tolerância a definir) |
| 12 | **F1 e F2 – Fusão** | **F1:** soma ponderada das pontuações, **redistribuindo os pesos quando uma fonte está ausente** (item sem foto ou sem coordenadas), com os pesos ajustados por busca em grade no conjunto de validação. **F2:** *Reciprocal Rank Fusion* (RRF), que combina as posições nos rankings e dispensa calibrar as escalas das pontuações. Teste a categoria de duas formas: como filtro e como mais uma pontuação |
| 13 | Ablação e robustez | Rodar a melhor fusão retirando uma fonte por vez e avaliá-la em subconjuntos: sem foto, sem coordenadas, descrição curta (até 5 palavras) e objetos muito parecidos entre si |

#### Prioridade 3 – Integração do protótipo à plataforma

| # | Situação encontrada | O que fazer |
|---|---|---|
| 14 | As sugestões são recalculadas a cada acesso e não ficam guardadas; não há como saber se uma sugestão estava certa | Criar o modelo `SugestaoCorrespondencia` no app `items`, com item perdido, item achado, pontuação final, pontuações por fonte (JSON), estratégia e versão, situação (sugerida, vista, confirmada ou rejeitada) e data. O par perdido–achado deve ser único |
| 15 | Os vetores teriam de ser recalculados a cada comparação | Guardar as representações em um modelo `RepresentacaoItem` (item, tipo texto ou imagem, modelo e versão, vetor em `BinaryField` e data) no MySQL atual, recalculadas só quando título, descrição ou imagem mudarem. O `Item.save` já detecta a troca de imagem para gerar o pHash; reaproveite essa lógica |
| 16 | Não há gatilho para gerar sugestões | Gerar as sugestões fora do ciclo da requisição, para não deixar o cadastro lento: um comando `recalcular_correspondencias` executado periodicamente ou uma tarefa disparada após o `commit` da transação |
| 17 | Não há API de correspondências, e o app exibe dados que não existem: o selo "match" de `Busca.jsx` depende de `item.matches`, que a API nunca envia, e o card "Matches" do `Dashboard.jsx` mostra, na verdade, a quantidade de itens **devolvidos** | Criar `GET /api/items/<id>/correspondencias/` (apenas para o dono do item) e `POST /api/correspondencias/<id>/avaliar/` (confirmar ou rejeitar). No app, criar a seção "Possíveis correspondências" no detalhe do item perdido e corrigir o selo e o card |
| 18 | A web usa a função própria da view `busca_visual` | Fazer a view chamar o serviço de `items/matching/` com a estratégia escolhida no experimento |
| 19 | As notificações anunciadas na página inicial do app não existem | Criar uma `Notificacao` (modelo já existente) para o dono do item perdido quando surgir uma sugestão acima do limiar escolhido pela curva de precisão × revocação |
| 20 | No app, a coordenada é a posição do aparelho **no momento do cadastro**, que pode não ser o lugar onde o objeto foi perdido ou achado. O campo `local` do app sugere "Bairro ou cidade", pouco útil dentro de um campus. Na web, o ponto é escolhido no mapa | Permitir marcar o ponto no mapa também no app (o `react-native-maps` já é usado em `ItemLocationMap`) e trocar o texto de ajuda do `local` por algo como "Bloco, sala ou setor". Registre no artigo essa diferença entre web e app como ameaça à validade |
| 21 | `buscar_por_imagem` não filtra status, exige todas as palavras devolvidas pelo Gemini e envia sempre o tipo `image/jpeg` | Desejável: filtrar pelos status complementares e excluir os devolvidos, substituir a exigência de todas as palavras por uma pontuação e enviar o tipo MIME real da imagem |
| 22 | Não há testes da busca nem da correspondência | Testes unitários de cada estratégia (casos pequenos com resposta conhecida), da fusão com fonte ausente e dos endpoints do item 17. Nos testes, os modelos pesados podem ser substituídos por *mocks* |

#### Cuidados

- **Custo em produção:** o `sentence-transformers` depende do PyTorch, que ocupa centenas de megabytes e pode não caber na memória do plano atual do Render. Decida a integração com os números da QP4: modelo menor, cálculo em lote ou API externa. Essa decisão é um resultado do trabalho, e não um problema.
- **Reprodutibilidade:** fixe as versões das bibliotecas e dos modelos, as sementes aleatórias e o *hash* do commit. Não use uma API de IA generativa como única referência, porque o modelo muda sem aviso.
- **Privacidade (LGPD):** use dados reais somente com autorização e anonimizados (sem nomes, matrículas, documentos, rostos ou placas nas fotos). Itens da categoria "Documentos" não devem entrar em um conjunto público. Enviar imagens a uma API externa é tratamento de dados por terceiros e deve ser informado no artigo.
- **Exposição das sugestões:** mostre as sugestões apenas ao dono do item perdido, sem revelar dados pessoais de quem achou além do que o chat já revela.

### 2.4 Protocolo sugerido para o conjunto de dados

Esta é a decisão mais importante do trabalho, porque todos os resultados dependem dela. Proposta (confirme as quantidades com o orientador):

1. **Objetos:** reúna de 40 a 60 objetos reais, comuns em um campus e distribuídos pelas 6 categorias, incluindo **grupos de objetos parecidos** (várias garrafas, mochilas pretas, carregadores e chaves). Esses objetos parecidos tornam o teste honesto.
2. **Item achado:** uma pessoa fotografa o objeto como um achador faria (celular, fundo e iluminação do próprio local), escreve título e descrição curtos e marca o local no mapa.
3. **Item perdido:** **outra pessoa**, que conhece o objeto mas não vê a foto do achado, escreve título e descrição de memória e marca onde acredita tê-lo perdido. Em parte dos casos, anexe uma foto diferente do mesmo objeto; nos demais, não anexe foto (para a QP3).
4. **Variações controladas:** registre, para cada par, se há foto nos dois lados, em um só ou em nenhum; se há coordenadas; a distância entre os pontos; e a diferença entre as datas.
5. **Distratores:** acrescente itens achados sem par (por exemplo, de 2 a 3 vezes o número de pares) para simular um mural real.
6. **Gabarito por construção:** cada par recebe um identificador comum no momento da criação, então nada precisa ser rotulado depois.
7. **Divisão:** separe o conjunto de validação (cerca de 30%, para ajustar pesos, σ e limiar) e o de teste (cerca de 70%, para os resultados finais) **antes** de rodar qualquer estratégia. Nunca ajuste nada olhando o conjunto de teste.
8. **Dados reais (opcional):** os itens devolvidos em produção podem formar um segundo conjunto, pequeno e anonimizado. Se forem usados, deixe claro que o gabarito veio do registro de devolução.
9. **Sem descrições geradas por IA:** não gere as descrições com IA generativa. Se usar IA para ampliar os dados, mantenha esses exemplos separados e trate-os como ameaça à validade.
10. **Ficha do conjunto:** documente tudo em `avaliacao/README.md` (quantidades, categorias, quem produziu, como, quando, aparelhos usados e licença).

Como o protocolo envolve pessoas escrevendo descrições e tirando fotos, leia a seção [Pesquisas com pessoas](../../README.md#pesquisas-com-pessoas) das orientações gerais e verifique com o orientador se é necessário submeter o estudo a um Comitê de Ética em Pesquisa.

### 2.5 Métricas sugeridas

A correspondência é avaliada como um **problema de ranqueamento**: cada item perdido é uma consulta, e os itens achados são os candidatos a ordenar.

| Métrica | O que responde |
|---|---|
| Recall@k (k = 1, 5 e 10) | O item correto aparece entre as k primeiras sugestões? É a mais importante para o usuário, que só olha poucas sugestões |
| MRR (*Mean Reciprocal Rank*) | Em que posição, em média, o item correto aparece |
| nDCG@10 | Qualidade da ordenação, valorizando acertos nas primeiras posições |
| Precisão, revocação e F1 no limiar | Quando vale a pena notificar o usuário (equilíbrio entre excesso de alertas e correspondências perdidas) |
| Tempo por consulta (média e percentil 95) e memória | Viabilidade na infraestrutura atual (QP4) |
| Teste de Wilcoxon pareado por consulta e intervalos de confiança por *bootstrap* | Se a diferença entre duas estratégias é estatisticamente significativa |

> Como normalmente só há **um** item correto por consulta, a Precision@k diz pouco (no máximo 1/k). Priorize Recall@k e MRR.

---

## 3. Orientações de escrita

Escreva o TCC no modelo ABNT, seguindo as [orientações gerais](../../README.md), mas pense no **artigo** desde o início. Toda afirmação sobre o desempenho do mecanismo precisa de um número vindo do experimento, e toda afirmação sobre técnicas precisa de uma referência. Frases como "a IA identifica os objetos com precisão" ou "o sistema inteligente encontra o item", sem métricas, são cortadas pelos revisores.

### 3.1 Introdução

- **Contextualização:**
  - pesquise sobre a perda de objetos em locais de grande circulação (instituições de ensino, transporte público, aeroportos e eventos) e sobre o destino dos objetos não devolvidos. Procure números em fontes confiáveis (relatórios de instituições e de empresas de transporte, pesquisas publicadas) e não use números sem fonte;
  - fale sobre como o processo tradicional (balcão, cadernos de registro, murais e grupos de mensagens) depende de alguém procurar manualmente;
  - fale sobre as plataformas digitais de achados e perdidos e sobre como a maioria delas funciona apenas como mural com busca manual.
- **Problemática:**
  - fale sobre por que encontrar a correspondência é difícil: quem perdeu e quem achou descrevem o mesmo objeto com palavras diferentes, as fotos são tiradas em condições diferentes, quem perdeu geralmente não tem foto e a localização é imprecisa;
  - fale sobre como, com o crescimento do mural, a busca manual fica cansativa e objetos deixam de ser devolvidos;
  - mostre que a comparação por palavras em comum, como a heurística atual do FIND, falha nesses casos. Use um exemplo curto só como ilustração; os detalhes ficam para os Resultados;
  - aponte a falta de avaliação: soluções que anunciam "correspondência inteligente" raramente medem precisão e revocação.
- **Caminho para a solução:**
  - pesquise sobre recuperação de informação (a correspondência como problema de ranqueamento), *embeddings* de texto, visão computacional com modelos pré-treinados (CLIP), recuperação multimodal, fusão de evidências e recuperação de informação geográfica;
  - cite trabalhos que aplicam essas técnicas a problemas parecidos, como a correspondência de produtos no comércio eletrônico (*product matching*), a busca de animais perdidos por imagem e os próprios sistemas de achados e perdidos;
  - mostre a lacuna: faltam comparações controladas entre fontes de evidência, com métricas de recuperação de informação, com textos em português e com dados faltantes. **Confirme a lacuna na revisão da literatura**; se encontrar um trabalho que já faça isso, ajuste a contribuição.
- **Apresentação da solução:**
  - fale sobre o módulo de correspondência proposto para o FIND: o que ele recebe, o que devolve e quais fontes de evidência usa;
  - diga o que este trabalho faz: constrói um conjunto de avaliação com gabarito, compara estratégias isoladas e combinadas com a heurística existente, mede o custo e integra o protótipo à plataforma;
  - não antecipe resultados que ainda não existem.
- **Vínculo com projetos:** fale sobre o histórico do FIND (desde novembro de 2025), a equipe e o projeto institucional a que ele pertence (confirme com o orientador). Os repositórios têm vários autores, então **deixe explícito o que já existia antes do TCC** (busca visual e heurística, de junho de 2026) **e o que é contribuição deste trabalho** (módulo, conjunto de dados e avaliação). Cite também o trabalho paralelo do João Gabriel sobre a arquitetura.
- **Pergunta de pesquisa e contribuições:** feche a Introdução com a pergunta de pesquisa e as QPs (seção 1.3) e com uma lista curta de contribuições, como é comum em artigos de computação. Por exemplo:
  - um conjunto de avaliação com gabarito para correspondência de itens perdidos e encontrados, com textos em português;
  - a comparação experimental entre fontes textuais, visuais, cruzadas e geográficas, tendo a heurística atual como linha de base;
  - a análise da robustez a dados ausentes e do custo computacional;
  - um protótipo integrado a uma plataforma em uso.

### 3.2 Objetivo geral

- Escreva uma frase, com um único verbo principal, coerente com a pergunta de pesquisa;
- o objeto do objetivo é o **mecanismo de correspondência e a sua avaliação**, e não "desenvolver um sistema de achados e perdidos";
- estrutura para você completar:

> "O objetivo principal do presente trabalho consiste em propor e avaliar [...] para a sugestão automática de correspondências entre itens perdidos e encontrados na plataforma FIND, comparando [...] por meio de [...]."

### 3.3 Referencial Teórico

Explique somente os conceitos que aparecem depois nos Resultados. Detalhes de instalação e uso das bibliotecas vão para Materiais e Métodos, com referência à documentação oficial. Estrutura sugerida:

```
2 REFERENCIAL TEÓRICO
2.1 Recuperação de informação e sua avaliação
2.2 Representação e similaridade de textos
2.3 Representação e similaridade de imagens
2.4 Recuperação multimodal e fusão de evidências
2.5 Recuperação de informação geográfica e temporal
2.6 Trabalhos relacionados
```

- **2.1 Recuperação de informação e sua avaliação:** pesquise sobre consulta, documento e relevância; o modelo vetorial, o TF-IDF e o BM25; e a avaliação com coleções de teste e gabarito (paradigma de Cranfield). Explique Recall@k, MRR, nDCG, curva de precisão × revocação e testes de significância.
- **2.2 Representação e similaridade de textos:** pesquise sobre o pré-processamento em português (tokenização, *stopwords* e radicalização com o RSLP), as limitações da representação por "saco de palavras" (sinônimos e paráfrases), os *embeddings* de sentenças (BERT, Sentence-BERT, modelos multilíngues e o BERTimbau) e a similaridade do cosseno. Fale sobre as dificuldades dos textos curtos, como os do FIND.
- **2.3 Representação e similaridade de imagens:** pesquise sobre o hash perceptual e os histogramas de cor (o que o FIND já usa) e as representações aprendidas por redes neurais pré-treinadas (CNN, *Vision Transformer*, CLIP e DINOv2). Fale sobre a invariância a ângulo, iluminação e fundo e sobre o uso de modelos sem treino adicional (*zero-shot*).
- **2.4 Recuperação multimodal e fusão de evidências:** pesquise sobre o espaço compartilhado entre texto e imagem do CLIP, a busca cruzada entre modalidades, a fusão precoce e a tardia, a normalização de pontuações (min-max e z-score), o RRF e o tratamento de modalidades ausentes.
- **2.5 Recuperação de informação geográfica e temporal:** pesquise sobre a distância de Haversine, funções de decaimento pela distância, a imprecisão do GPS em ambientes internos e o uso de janelas temporais.
- **2.6 Trabalhos relacionados:** busque sistemas de achados e perdidos e trabalhos de correspondência em domínios parecidos. Termos de busca (use em português e em inglês):
  - `"lost and found" AND (matching OR retrieval OR recommendation)`;
  - `"lost item" AND ("image retrieval" OR "computer vision")`;
  - `"product matching" AND multimodal`;
  - `"lost pet" AND (image OR recognition)`;
  - `"cross-modal retrieval" AND CLIP`;
  - `"multimodal fusion" AND "information retrieval"`;
  - `"achados e perdidos" AND (sistema OR aplicativo)`.

  Bases: SOL, IEEE Xplore, ACM Digital Library, Portal de Periódicos da CAPES, Google Acadêmico e arXiv (neste, verifique se o trabalho foi publicado depois em evento ou periódico). Muitos trabalhos sobre achados e perdidos descrevem o sistema sem avaliá-lo; isso reforça a lacuna, mas cite-os com cuidado. Termine a seção com um quadro comparativo usando critérios como: domínio, fontes de evidência usadas (texto, imagem, local e tempo), técnica, conjunto de dados (tamanho e se é público), métricas, tratamento de dados ausentes e idioma.

**Leituras de partida.** Localize a fonte original, confira os dados e só depois inclua nas Referências:

- MANNING, C. D.; RAGHAVAN, P.; SCHÜTZE, H. *Introduction to Information Retrieval* (Cambridge University Press, 2008; disponível gratuitamente on-line);
- BAEZA-YATES, R.; RIBEIRO-NETO, B. *Recuperação de informação: conceitos e tecnologia das máquinas de busca* (2. ed., Bookman, 2013);
- ROBERTSON, S.; ZARAGOZA, H. *The Probabilistic Relevance Framework: BM25 and Beyond* (Foundations and Trends in Information Retrieval, 2009);
- JÄRVELIN, K.; KEKÄLÄINEN, J. *Cumulated gain-based evaluation of IR techniques* (ACM Transactions on Information Systems, 2002);
- SMUCKER, M. D.; ALLAN, J.; CARTERETTE, B. *A comparison of statistical significance tests for information retrieval evaluation* (CIKM, 2007);
- ORENGO, V. M.; HUYCK, C. *A stemming algorithm for the Portuguese language* (SPIRE, 2001);
- DEVLIN, J. et al. *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding* (NAACL, 2019);
- REIMERS, N.; GUREVYCH, I. *Sentence-BERT* (EMNLP-IJCNLP, 2019) e *Making Monolingual Sentence Embeddings Multilingual using Knowledge Distillation* (EMNLP, 2020);
- SOUZA, F.; NOGUEIRA, R.; LOTUFO, R. *BERTimbau: Pretrained BERT Models for Brazilian Portuguese* (BRACIS, 2020);
- ZAUNER, C. *Implementation and Benchmarking of Perceptual Image Hash Functions* (dissertação, 2010);
- SWAIN, M. J.; BALLARD, D. H. *Color indexing* (International Journal of Computer Vision, 1991);
- RADFORD, A. et al. *Learning Transferable Visual Models From Natural Language Supervision* (ICML, 2021), o artigo do CLIP;
- OQUAB, M. et al. *DINOv2: Learning Robust Visual Features without Supervision* (Transactions on Machine Learning Research, 2024);
- BALTRUŠAITIS, T.; AHUJA, C.; MORENCY, L.-P. *Multimodal Machine Learning: A Survey and Taxonomy* (IEEE TPAMI, 2019);
- ATREY, P. K. et al. *Multimodal fusion for multimedia analysis: a survey* (Multimedia Systems, 2010);
- CORMACK, G. V.; CLARKE, C. L. A.; BÜTTCHER, S. *Reciprocal rank fusion outperforms Condorcet and individual rank learning methods* (SIGIR, 2009);
- JONES, C. B.; PURVES, R. S. *Geographical information retrieval* (International Journal of Geographical Information Science, 2008);
- BRASIL. Lei nº 13.709, de 14 de agosto de 2018 (Lei Geral de Proteção de Dados Pessoais);
- documentação oficial do scikit-learn, do Sentence Transformers, do ImageHash, do NumPy e do Django.

### 3.4 Metodologia

- **Classificação da pesquisa:** fale sobre a natureza aplicada, o objetivo explicativo, a abordagem quantitativa (com análise qualitativa dos erros) e os procedimentos: pesquisa bibliográfica e **pesquisa experimental**. Deixe claras as variáveis do experimento: independentes (estratégia e fontes disponíveis), dependentes (as métricas) e controladas (mesmo conjunto de dados, mesma divisão e mesmas versões).
- **Pesquisa bibliográfica:** informe as bases consultadas, os termos de busca (seção 3.3), o período das publicações e os critérios de inclusão e exclusão.
- **Etapas:** descreva em ordem cronológica, com uma figura do fluxo:
  1. revisão da literatura;
  2. análise do que já existe no FIND e definição da linha de base;
  3. construção do conjunto de avaliação e do gabarito;
  4. implementação das estratégias e do script de avaliação;
  5. experimentos: estratégias isoladas, ajuste da fusão na validação, avaliação no teste, ablação e robustez;
  6. análise estatística e análise de erros;
  7. integração do protótipo à plataforma e medição do custo.
- **Planejamento do experimento:** apresente um quadro que ligue cada QP às estratégias comparadas, às métricas e à análise estatística usada.
- **Aspectos éticos:** descreva quem produziu as fotos e as descrições, como os dados foram anonimizados e se houve submissão a Comitê de Ética (seção 2.4).
- **Ameaças à validade:** o artigo precisa de uma subseção sobre isso, que pode ficar na Metodologia ou nos Resultados. Fale sobre:
  - o conjunto controlado e de tamanho limitado, que não reproduz todo o uso real;
  - os objetos escolhidos pelo pesquisador e as descrições escritas por pessoas que sabiam do estudo;
  - a diferença de significado das coordenadas na web e no app (item 20);
  - a possibilidade de os modelos pré-treinados já terem visto imagens parecidas;
  - a generalização para outras instituições;
  - a mudança dos modelos disponíveis apenas por API.

### 3.5 Materiais e Métodos

**Materiais.** Monte o quadro-resumo com as versões **efetivamente usadas**: confira `requirements.txt` e `package.json` na data da escrita. Versões encontradas em 11/09/2026:

| Ferramenta | Versão | Finalidade no trabalho |
|---|---|---|
| Python | 3.12 | Linguagem do back-end e dos experimentos |
| Django / Django REST Framework | 6.0.3 / 3.15.2 | Integração do módulo à plataforma e à API |
| ImageHash / Pillow | 4.3.2 / 12.1.1 | pHash e manipulação de imagens (estratégia V0) |
| NumPy / SciPy | 2.2.6 / 1.17.1 | Histogramas, vetores e similaridades |
| MySQL / SQLite | 8.4 / – | Banco de dados em produção / em desenvolvimento |
| React Native / Expo | 0.81.5 / SDK 54 | Exibição das sugestões no app |
| expo-location / expo-image-picker | 19.0 / 17.0 | Coordenadas e fotos no app |
| Leaflet | 1.9.4 | Marcação do local no mapa (web) |
| Gemini | 2.5 Flash | Busca visual existente (comparação opcional) |
| pytest | 9.1.0 | Testes automatizados |
| scikit-learn, NLTK, rank-bm25 | a definir | Estratégia T1 |
| Sentence Transformers / PyTorch | a definir | Estratégias T2, V1 e X1 |
| Modelos pré-treinados | nome exato e revisão | Informe o identificador do modelo e a revisão usada |
| Máquina dos experimentos | CPU, GPU e memória | Necessário para interpretar os tempos medidos |

**Métodos.** Para cada item, explique o que é, para que foi usado e por que foi escolhido:

- **conjunto de dados:** protocolo seguido, quantidades, aparelhos usados nas fotos, anonimização e divisão entre validação e teste;
- **pré-processamento:** tratamento do texto (normalização e radicalização) e das imagens (redimensionamento e orientação);
- **estratégias:** apresente a fórmula de pontuação de cada uma (cosseno, Haversine, decaimento pela distância, soma ponderada com redistribuição de pesos e RRF, que soma `1 / (k + posição)` em cada ranking, com k = 60 no trabalho de Cormack, Clarke e Büttcher);
- **ajuste de parâmetros:** busca em grade no conjunto de validação (pesos, σ, tolerância de datas e limiar);
- **métricas e testes estatísticos:** fórmulas das métricas da seção 2.5 e o teste usado;
- **medição de custo:** máquina, número de repetições e aquecimento dos modelos antes da medição;
- **integração:** modelos de dados, endpoints e gatilho de geração das sugestões.

> **Dica para o artigo:** os revisores valorizam o "por que X e não Y". Justifique a escolha dos modelos pelo tamanho, pelo suporte ao português e pela licença. Informe apenas as alternativas que foram de fato testadas; não invente comparações.

### 3.6 Resultados (e Discussão)

Organize o capítulo pelas questões de pesquisa, e não por telas. Estrutura sugerida:

- **Caracterização do conjunto de dados:** tabela com o total de itens, pares e distratores, a distribuição por categoria, a porcentagem de itens com foto e com coordenadas e o tamanho médio das descrições. Uma figura com exemplos de pares, sem dados pessoais.
- **Fontes isoladas (QP1):** tabela com as estratégias B0, T1, T2, V0, V1, X1 e G1 nas linhas e Recall@1, Recall@5, Recall@10, MRR e nDCG@10 nas colunas, calculadas no conjunto de teste e com intervalos de confiança. Comente o que cada fonte captura e onde falha.
- **Fusão (QP2):** F1 e F2 comparadas com a melhor fonte isolada e com a B0, com os resultados do teste estatístico. Informe os pesos encontrados e apresente a tabela de ablação.
- **Robustez e busca cruzada (QP3):** gráfico com o desempenho por subconjunto (sem foto, sem coordenadas, descrição curta e objetos parecidos) e os resultados da estratégia X1.
- **Custo (QP4):** tabela com o tempo de cálculo das representações por item, o tempo por consulta (média e percentil 95), a memória, o tamanho do modelo e o custo por mil consultas quando houver API. Discuta o que é viável no Render.
- **Limiar de notificação:** curva de precisão × revocação, o limiar escolhido e os valores de precisão e revocação nesse ponto.
- **Análise de erros:** de 3 a 5 exemplos comentados de falhas, como duas mochilas pretas com descrições quase iguais ou uma foto escura do item achado.
- **Integração:** uma figura da web e uma do app com as sugestões e um diagrama de sequência do fluxo. Não é um catálogo de telas.
- **Discussão:** relacione os resultados com o Referencial Teórico e com os trabalhos relacionados (com cautela, porque os conjuntos de dados são diferentes) e aponte as limitações.

Cuidados:

- apresente **todas** as estratégias testadas, inclusive as que foram mal, e não arredonde números a seu favor;
- nunca ajuste parâmetros no conjunto de teste;
- não exponha nomes, documentos, rostos, e-mails ou outros dados pessoais em figuras e tabelas;
- siga as regras de [imagens](../../README.md#como-incluir-imagens) e de [tabelas](../../README.md#como-incluir-tabelas) das orientações gerais.

### 3.7 Conclusão

- Responda **diretamente** à pergunta de pesquisa e a cada QP, com os números principais;
- comente cada objetivo específico;
- retome as principais contribuições;
- apresente as limitações com honestidade: conjunto controlado e limitado, e pendências não concluídas;
- sugira trabalhos futuros, por exemplo: avaliação em produção com usuários reais (taxa de devolução e confirmações das sugestões), aprendizado a partir das confirmações e rejeições (*learning to rank*), ajuste fino dos modelos com dados da instituição, uso das leituras RFID e QR Code como evidência adicional, várias fotos por item e aplicação em outras instituições.

### 3.8 Objetivos específicos

Serão entregues no final, junto com o Resumo, para refletirem o que foi **realmente feito**. Siga as regras das orientações gerais: 3 a 5 itens, verbos no infinitivo, na mesma ordem das etapas da Metodologia. Verbos e temas que combinam com este trabalho:

- **revisar** a literatura sobre ...;
- **construir** um conjunto de avaliação ...;
- **implementar** estratégias de similaridade ...;
- **comparar** ... por meio de métricas de recuperação de informação;
- **analisar** a robustez ... e o custo computacional ...;
- **integrar** o módulo ... à plataforma FIND.

Não transforme funcionalidades do sistema em objetivos (por exemplo, "permitir que o usuário receba notificações").

### 3.9 Resumo e *Abstract*

- **Tamanho:** no TCC, parágrafo único com 150 a 500 palavras (NBR 6028:2021). No artigo, siga o limite da chamada. Os veículos da seção 1.4 exigem resumo em português e em inglês.
- **Sequência:** contexto, problema, objetivo, método (conjunto de dados, estratégias e métricas), principais resultados **com números** (por exemplo, "a fusão ... alcançou Recall@5 de ..., contra ... da heurística atual") e principal conclusão.
- **Palavras-chave possíveis:** recuperação de informação; recuperação multimodal; *embeddings*; visão computacional; achados e perdidos.

### 3.10 Do TCC ao artigo

- **Estrutura típica de um artigo experimental:** Introdução; Trabalhos relacionados; Fundamentação (curta); Módulo proposto; Metodologia experimental (conjunto de dados, estratégias, métricas e protocolo); Resultados; Discussão e ameaças à validade; Conclusão.
- **Modelo:** use o exigido pela chamada (em geral, o modelo da SBC, também disponível no Overleaf).
- **Revisão às cegas:** se for o caso, retire da versão submetida os nomes, a instituição (o código cita o domínio `find.ifrn.edu.br`) e os links dos repositórios. Uma opção para os links é o Anonymous GitHub.
- **Artefatos:** se as autorizações permitirem, publique o conjunto de dados e os scripts de avaliação (por exemplo, no Zenodo, que gera um DOI). Isso aumenta a reprodutibilidade e é bem visto pelos revisores.
- **Licença e autoria:** o README do projeto declara "Licença Proprietária". Antes de publicar código ou dados, confirme com a equipe e com o orientador o que pode ser divulgado. Defina a autoria do artigo (aluno, orientador e, se for o caso, demais integrantes) antes da submissão.
- **Uso de IA generativa na escrita:** siga a seção [Uso de inteligência artificial generativa](../../README.md#uso-de-inteligência-artificial-generativa) das orientações gerais e as regras do veículo escolhido.
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

**Alinhamento sugerido das implementações.** É uma recomendação; os prazos oficiais são os da tabela acima. Os Resultados dependem do conjunto de dados e dos experimentos, que precisam começar já:

| Até | O que deve estar pronto | Por quê |
|---|---|---|
| 18/09/2026 | Recorte e QPs aprovados pelo orientador; *issues* criadas; itens 1 e 4 (coordenadas na API e extração da linha de base); protocolo do conjunto de dados definido (seção 2.4) e autorizações encaminhadas; organização do trabalho no repositório combinada com o João Gabriel | A Introdução e o objetivo geral dependem do recorte, e o protocolo é a base de todo o experimento |
| 05/10/2026 | Item 2 (conjunto de dados construído e dividido); itens 3 e 5 (script de avaliação e interface comum) funcionando com as estratégias B0, T1 e V0 (itens 6 e 8) | A Metodologia descreve o protocolo e o planejamento do experimento |
| 12/10/2026 | Itens 7, 9, 10 e 11 (T2, V1, X1 e G1) avaliados no conjunto de validação | Materiais e Métodos descreve as estratégias e as ferramentas |
| 19/10/2026 | Itens 12 e 13 (fusão, ablação e robustez) executados no conjunto de teste; medição de custo; protótipo integrado (itens 14 a 19, ao menos a API e uma tela no app) e item 22 (testes) | Sobra uma semana para escrever os Resultados com os dados fechados |

Antes de cada envio, use o [checklist das orientações gerais](../../README.md#checklist-antes-de-enviar-uma-versão-ao-orientador).
