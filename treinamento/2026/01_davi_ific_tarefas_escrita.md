# Plano de escrita do artigo – Davi (Tecnologia em Sistemas para Internet)

**Projeto pai:** iFIC – Desenvolvimento de Funcionalidades de Autenticação, Administração e Gerenciamento de Cursos de Formação Inicial e Continuada (ver `.llm/ific/projeto.md`).

**Temática:** S5 – Otimização de desempenho: consultas no ORM do Django e cache com Redis (ver `.llm/ific/tematicas.md`).

**Plano de desenvolvimento correspondente:** `01_davi_ific_tarefas_desenvolvimento.md`.

**Base de estilo e de normas ABNT:** o arquivo `README.md` deste repositório. Tudo o que está lá vale aqui. Este documento **não repete** as regras da ABNT; ele diz **o que pesquisar e o que escrever** em cada seção deste trabalho específico.

> **Importante:** o que segue são **orientações**, não o texto pronto. Não copie estas frases para o artigo. Elas dizem sobre o que é cada parágrafo; o texto tem de ser escrito por você, com as suas palavras e com as referências que você leu.

---

## Onde escrever: documento compartilhado no Google Drive

O documento do artigo será **criado e compartilhado pelo coordenador em uma pasta do Google Drive**. Você não cria arquivo novo nem trabalha em cópia local.

Como trabalhar nele:

- **Escreva sempre no documento compartilhado.** Nada de escrever no Word e colar depois: o histórico do Drive é o que permite ao orientador ver o que mudou de uma semana para outra.
- **Não crie cópias** ("Artigo v2", "Artigo final", "Artigo final revisado"). É a forma mais rápida de perder trabalho. O Drive já guarda tudo em **Arquivo → Histórico de versões**.
- **Marque cada entrega no histórico.** Ao terminar uma seção, use **Arquivo → Histórico de versões → Nomear versão atual**, com um rótulo como `Entrega 1 – Introdução – 29/09`.
- **Avise por mensagem quando entregar.** O orientador não fica olhando o documento; ele precisa saber que há algo novo.
- **Comentário se responde, não se apaga.** Responda a cada comentário e só então marque como resolvido.
- **Figuras e tabelas** vão dentro do documento, no lugar certo, com identificação em cima e fonte embaixo. Não mande imagem em anexo separado.
- **Crie a seção "Referências" no primeiro dia** e acrescente cada obra assim que ler. Deixar para o fim garante referência faltando.
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
| 22/09 a 28/09 | Sprint 1 – ambiente, Django e modelos | Introdução e Objetivo Geral (29/09) |
| 29/09 a 12/10 | Sprints 2 e 3 – base de dados, V0 e medição | Referencial Teórico (13/10) |
| 13/10 a 19/10 | Sprint 4 – V1 (`select_related`) | Metodologia (20/10) |
| 20/10 a 26/10 | Sprint 5 – V2 (índices) | Materiais e Métodos (27/10) |
| 27/10 a 09/11 | Sprints 6 e 7 – V3 (`annotate`) e V4 (cache) | Resultados (10/11) |
| 10/11 a 16/11 | Sprint 8 – bateria final | Conclusão (17/11) |
| 17/11 a 23/11 | — | Resumo, Objetivos e Título (24/11) |

**Um aviso sobre o cronograma.** A Metodologia vence em 20/10, quando você só terá medido V0 e V1. E os Resultados vencem em 10/11, com a V4 recém-pronta. Isso é normal e tem solução:

- escreva a Metodologia falando do **plano** ("serão medidas cinco versões...") e depois passe para o passado;
- **vá preenchendo as tabelas de Resultados a cada sprint**, e não tudo na última semana. Quem deixa os Resultados para o fim não entrega.

### Regras de entrega

- Entregue **no prazo, mesmo incompleto**. Texto pela metade dá para comentar; texto que não chega, não.
- Cada entrega é: seção escrita + versão nomeada no histórico + aviso ao orientador.
- Resolva **todos** os comentários da entrega anterior antes de avisar sobre a próxima.

---

## Que tipo de artigo é este

Escreva um **artigo científico** de 8 a 12 páginas, para um congresso ou uma revista. **Confirme com o orientador qual é o destino antes de começar**, porque dele vêm o modelo de formatação e o limite de páginas.

O seu trabalho tem uma vantagem: ele produz **números**. Isso é o que diferencia um artigo de um relato de "fiz um sistema". Quatro coisas fazem a diferença:

1. **O leitor quer saber quanto, não o quê.** Não interessa que você fez uma página em Django; interessa que a versão otimizada respondeu em X ms contra Y ms da original.
2. **O método tem de dar para repetir.** Diga a máquina, as versões, quantas vezes repetiu, quanto tempo durou cada rodada.
3. **Mostre o custo, não só o ganho.** Índice ocupa espaço; cache pode mostrar dado velho. Trabalho que só mostra o lado bom perde credibilidade.
4. **Declare as limitações.** Reconhecer limite aumenta a confiança no trabalho; esconder é o caminho mais rápido para a recusa.

Estrutura sugerida:

```
1 INTRODUÇÃO
1.1 Objetivo geral
1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
2.1 Desempenho em aplicações web
2.2 ORM e o problema das N+1 consultas
2.3 Índices em banco de dados
2.4 Cache em aplicações web
2.5 Trabalhos relacionados
3 METODOLOGIA
3.1 Classificação da pesquisa
3.2 Como o experimento foi montado
3.3 Protocolo de medição
4 MATERIAIS E MÉTODOS
5 RESULTADOS E DISCUSSÃO
6 CONCLUSÃO
REFERÊNCIAS
```

---

# 1. Introdução
**Prazo: 29/09/2026**

Cinco blocos de parágrafos, nesta ordem (é a sequência do `README.md`). Uma a duas páginas no total.

## 1.1 Contextualização (1 a 2 parágrafos)

**Pesquise sobre:**

- o que são os **Cursos de Formação Inicial e Continuada (FIC)** e o papel da Rede Federal na oferta de qualificação profissional. Fontes: Lei nº 11.892/2008, Guia Pronatec de Cursos FIC, Plataforma Nilo Peçanha e o portal do IFRN. Procure **um número** (quantos cursos, quantas vagas, quantos concluintes) para usar no texto;
- a relação entre **lentidão de uma página e desistência do usuário**. Procure por "*web performance*", "*page load time*", "tempo de resposta e abandono". Um bom ponto de partida são os estudos de Jakob Nielsen sobre limites de tempo de resposta. Se usar relatório de empresa, diga que é relatório de empresa.

**Escreva sobre:** a oferta de cursos FIC pelo IFRN e o iFIC como a plataforma que centraliza essas informações. Depois estreite para o ponto do seu trabalho: a **página pública de listagem de cursos** é a mais acessada de um sistema assim, e o acesso a ela **não é constante** — concentra-se quase todo na abertura das inscrições.

Feche fazendo a ligação que dá sentido ao trabalho: nesse cenário, desempenho não é detalhe técnico, é **acesso**. Uma página lenta ou fora do ar no dia da inscrição deixa candidato de fora, o que vai contra o objetivo do próprio projeto. Use essa ligação — ela é o que torna o trabalho mais do que um exercício de programação.

## 1.2 Problemática (1 a 2 parágrafos)

**Pesquise sobre:**

- o **problema das N+1 consultas** em ORM. Procure por "*N+1 select problem*", "problema N+1 ORM", "*lazy loading*";
- o que acontece quando uma consulta não tem índice: o banco lê a tabela inteira;
- por que esses problemas **não aparecem durante o desenvolvimento**.

**Escreva sobre:** o problema concreto. O ORM do Django facilita muito o trabalho porque esconde o SQL — mas, ao esconder o SQL, ele também esconde o **custo**. Escrever `turma.curso.nome` dentro de um laço parece só acessar um atributo, e na verdade é uma ida ao banco. Com 500 turmas na tela, são centenas de consultas para montar uma página só.

Explique a consequência em cadeia, que é o coração da sua problemática: mais consultas → cada requisição demora mais → o servidor atende menos gente por segundo → forma-se fila → quem chega depois espera muito mais → alguns acessos dão erro por tempo esgotado.

E explique por que isso passa despercebido: com 20 registros de teste na máquina do desenvolvedor, 200 consultas levam milissegundos e ninguém nota. Com 50.000 inscrições e 50 pessoas acessando ao mesmo tempo, a mesma página trava. O problema só aparece exatamente quando não se pode mais errar.

**Feche mostrando a lacuna, que é o que justifica pesquisar:** existem várias técnicas conhecidas para resolver isso, mas cada uma tem um ganho e um custo diferentes, e é difícil achar medições que as comparem **uma de cada vez, sobre a mesma aplicação e os mesmos dados**. É esse espaço que o seu trabalho ocupa.

**Não escreva** que "o iFIC está lento". Você não mediu o iFIC — o seu objeto é um protótipo. Fale do problema como fenômeno conhecido, aplicado a um cenário representativo.

## 1.3 Caminho para a solução (1 a 2 parágrafos)

**Pesquise sobre:**

- as formas de deixar uma página web mais rápida: escrever consultas melhores, criar índices, deixar o banco fazer os cálculos, usar cache, e ainda as soluções de infraestrutura (servidor maior, mais servidores);
- no Django: `select_related`, `prefetch_related`, `annotate`, e o sistema de cache;
- o que é o **Redis** e por que ele é a escolha mais comum para cache.

**Escreva sobre:** as alternativas que existem e o que cada uma custa. Mostre que há uma ordem natural, do mais barato para o mais arriscado:

1. escrever a consulta do jeito certo — não custa nada além de saber fazer;
2. criar índices — custa espaço em disco e deixa as escritas um pouco mais lentas;
3. deixar o banco calcular — não custa nada, mas exige cuidado para não errar a conta;
4. usar cache — é o mais rápido de todos, mas cria um problema novo: o dado guardado pode ficar desatualizado.

Justifique então o recorte do trabalho: avaliar essas **quatro técnicas**, aplicadas **uma de cada vez**, sobre a mesma página e os mesmos dados, medindo número de consultas, tempo de resposta e quantas requisições o servidor atende por segundo.

Diga também por que o trabalho **não** trata de servidor maior nem de vários servidores: são soluções de infraestrutura, e o foco aqui é o que o desenvolvedor controla no código e no banco.

## 1.4 Apresentação da solução (1 a 2 parágrafos)

**Escreva sobre:** o que foi feito, de forma concreta. Um protótipo em Django da página pública de listagem de cursos e turmas FIC, escrito em **cinco versões que ficam no ar ao mesmo tempo**, cada uma em um endereço: a versão sem nenhuma otimização (V0) e quatro versões que acrescentam, uma por vez, o carregamento dos relacionamentos de uma só vez, os índices no banco, a contagem feita pelo banco e o cache no Redis.

**Explique por que as cinco ficam no ar juntas:** porque assim todas são medidas no mesmo dia, na mesma máquina, com os mesmos dados. Se cada versão fosse medida em um dia diferente, qualquer variação do computador entraria no resultado. É uma decisão simples e é o que faz a comparação valer — mereça uma frase de destaque já aqui.

Diga como foi avaliado: base de dados fictícia com 1.000 turmas e 50.000 inscrições, gerada por script; contagem das consultas SQL por meio de teste automatizado; testes de carga com o Locust, com 10 e 50 usuários simultâneos, três repetições cada; e testes automatizados verificando se o cache mostra o dado atualizado depois de uma alteração.

Registre que **todos os dados são fictícios**, gerados com a biblioteca `Faker`, sem qualquer dado pessoal real — em conformidade com a LGPD (Lei nº 13.709/2018) — e que **não houve participantes humanos**, o que dispensa submissão ao Comitê de Ética em Pesquisa.

## 1.5 Vínculo com o projeto e escopo (1 parágrafo)

**Escreva sobre:** o vínculo com o projeto de pesquisa iFIC, do IFRN, cuja etapa atual trata de autenticação, painel administrativo e gerenciamento de cursos FIC. Explique que o protótipo foi construído **separadamente**, para testar as técnicas antes de levá-las à plataforma, e que **aplicá-las ao iFIC é trabalho futuro**, fora do escopo deste artigo.

Feche a Introdução com um parágrafo curto dizendo como o texto está organizado.

---

# 2. Objetivo Geral
**Prazo: 29/09/2026 (junto com a Introdução)**

Uma **única frase**, com **uma única ação principal**. Modelo do `README.md`:

> "O objetivo principal do presente trabalho consiste [na ação] de [o quê] para [finalidade]."

**Direcionamentos:**

- o verbo aqui provavelmente **não** é "desenvolver". O protótipo é o meio, não o fim — o que o trabalho entrega são os números. Verbos que cabem: **avaliar**, **comparar**, **medir**, **analisar**. Decida com o orientador;
- diga **o que** é avaliado: quatro técnicas de otimização (carregar os relacionamentos de uma vez, índices, cálculo no banco e cache);
- diga **sobre o quê**: a listagem pública de cursos FIC, em um protótipo Django;
- diga **em que dimensão** você mede: número de consultas, tempo de resposta e requisições por segundo. Sem isso, "otimizar o desempenho" fica vago demais;
- **não** empilhe ações. "Desenvolver, avaliar, comparar e integrar" são quatro objetivos, não um;
- **não** prometa o que não vai medir.

**Confira antes de entregar:** leia o objetivo geral e, logo depois, a primeira frase da sua Conclusão. Se as duas não estiverem falando da mesma coisa, uma delas está errada.

---

# 3. Objetivos Específicos
**Prazo: 24/11/2026 (com o Resumo e o Título)**

Ficam para o fim de propósito: eles descrevem o que foi **realmente alcançado**, e isso só se sabe com o trabalho pronto. Até lá, use uma versão provisória.

**Direcionamentos:**

- de 4 a 5 itens, verbo no infinitivo, minúscula no início, ponto e vírgula no fim de cada um e ponto no último;
- na **mesma ordem** das etapas da Metodologia e das subseções dos Resultados;
- cada um **verificável**: na Conclusão você terá de mostrar, com número, que foi atingido;
- não confunda objetivo com tarefa. "Instalar o Redis" não é objetivo específico.

**O que cada item deve cobrir** (redija com as suas palavras depois):

1. revisar a literatura sobre desempenho em aplicações web, consultas em ORM, índices e cache;
2. construir um protótipo da listagem pública de cursos FIC, com base de dados fictícia de grande volume;
3. definir um procedimento de medição que possa ser repetido;
4. implementar as quatro técnicas de otimização, uma de cada vez;
5. medir e comparar o ganho e o custo de cada técnica, com diferentes quantidades de usuários simultâneos.

---

# 4. Referencial Teórico
**Prazo: 13/10/2026**

**Vídeo com a explicação (assista antes de começar):** https://youtu.be/8Qztq1Q5vb0

Comece a procurar referências **na primeira semana**, não na véspera.

Aqui vale uma regra prática que resolve metade dos problemas desta seção: **tudo o que você vai usar nos Resultados precisa estar explicado aqui**. Se você vai apresentar "p95" na tabela, tem que ter explicado percentil aqui. Se não reaparece depois, não precisa estar.

Escreva do assunto mais geral para o mais específico.

## 4.1 Desempenho em aplicações web

**Pesquise:** "desempenho de aplicações web", "*web application performance*", "tempo de resposta", "*throughput*", "teste de carga", "*load testing*", "percentil". Para conceitos de medição de desempenho, procure livros da área de sistemas e artigos em português na SBC OpenLib e no Google Acadêmico.

**Escreva:** as três definições que você vai usar o artigo inteiro:

- **tempo de resposta (latência):** quanto uma requisição demora;
- **vazão:** quantas requisições o servidor atende por segundo;
- **usuários simultâneos:** quantas pessoas estão acessando ao mesmo tempo.

Explique também **por que a média não basta** e o que é o **percentil 95**: é o tempo abaixo do qual ficaram 95% dos acessos. A média pode parecer boa mesmo quando algumas pessoas esperaram muito; o p95 mostra o que aconteceu com quem se deu pior. Como você vai apresentar p95 na tabela, precisa definir aqui.

Por fim, explique o que é um **teste de carga**: simular várias pessoas acessando ao mesmo tempo para ver como o sistema se comporta.

## 4.2 ORM e o problema das N+1 consultas

**Pesquise:** "ORM", "mapeamento objeto-relacional", "*N+1 select problem*", "*lazy loading*", "*eager loading*". A documentação oficial do Django serve para explicar o `select_related`, mas o **conceito** de N+1 deve vir de livro ou artigo.

**Escreva:** o que é um ORM e que problema ele resolve (escrever código em objetos em vez de SQL). Depois explique o mecanismo que causa o problema: o ORM só busca os dados relacionados **no momento em que você os usa** — o chamado carregamento preguiçoso. Dentro de um laço, isso vira uma consulta por volta.

Defina o **problema N+1** com um exemplo pequeno: 1 consulta para trazer a lista, mais N consultas (uma por item) para completar os dados. Explique então a solução: pedir ao ORM que traga tudo de uma vez, o que no Django se faz com `select_related` (que junta as tabelas em uma consulta só) e com `prefetch_related` (que faz uma segunda consulta e junta os resultados na memória). Diga quando cada um se aplica.

## 4.3 Índices em banco de dados

**Pesquise:** "índice em banco de dados", "*database index*", "plano de execução", "*query execution plan*", "EXPLAIN MySQL". Livros de banco de dados (como os de Elmasri e Navathe, ou de Silberschatz e colegas) servem para os fundamentos, e a documentação do MySQL serve para a parte prática.

**Escreva:** o que é um índice, usando uma comparação simples — é como o índice remissivo no fim de um livro: sem ele, para achar um assunto você leria o livro inteiro. Explique o que é **varredura completa de tabela** e por que ela fica cada vez mais cara conforme a tabela cresce.

Explique também o que é o **plano de execução** e para que serve o comando `EXPLAIN`: ele mostra como o banco decidiu buscar os dados, e é assim que você sabe se o índice está sendo usado ou não.

E, importante, explique o **custo do índice**: ele ocupa espaço em disco e precisa ser atualizado toda vez que um registro é inserido, alterado ou apagado. Como você vai medir esse custo nos Resultados, ele precisa estar explicado aqui.

## 4.4 Cache em aplicações web

**Pesquise:** "cache em aplicações web", "*caching*", "*cache invalidation*", "TTL", "*cache hit*", e a documentação do Redis e do sistema de cache do Django.

**Escreva:** o que é cache — guardar o resultado já pronto para não ter que calcular de novo — e por que ele é, ao mesmo tempo, a técnica de maior ganho e a de maior risco. Explique o que é o **Redis**: um armazenamento que guarda pares chave-valor na memória, o que o torna muito mais rápido que um banco em disco. Deixe claro que o Redis **não substitui** o banco de dados: os dados continuam no MySQL, e o Redis guarda só uma cópia pronta.

Explique os **níveis de cache** possíveis em uma aplicação Django: a página HTML inteira, um pedaço do template, ou o resultado de uma consulta.

E, com destaque, explique o **problema da atualização do cache**: como o cache guarda uma cópia, ela pode ficar velha. As duas formas de resolver são o **tempo de expiração** (o dado se apaga sozinho depois de X minutos) e o **apagamento por evento** (quando alguém altera um registro, o cache é limpo).

Amarre ao seu domínio, que é o que dá sentido à escolha: mostrar "10 vagas restantes" em uma turma que já lotou não é um detalhe de desempenho, é informação errada para um candidato. É por isso que o seu trabalho testa a atualização do cache, e não só mede a velocidade.

## 4.5 Trabalhos relacionados

**Pesquise:** trabalhos que **tenham medido** desempenho de aplicações web ou de acesso a banco de dados — comparações entre ORM e SQL, avaliações de cache, comparações entre bancos. Busque em: SBC OpenLib, BDTD, repositórios de institutos federais e universidades, e Google Acadêmico. Termos: "otimização de consultas Django", "desempenho ORM", "avaliação de cache Redis", "*ORM performance*".

**Escreva:** de 3 a 5 trabalhos, um parágrafo cada, dizendo o que foi avaliado, **como foi medido** (esta é a informação que mais importa para você) e quais as limitações.

Feche com um **quadro comparativo** entre esses trabalhos e o seu, com colunas como: técnicas avaliadas, se foram aplicadas uma de cada vez ou todas juntas, banco de dados usado, tamanho da base, quantidade de usuários simultâneos testada, métricas apresentadas e se houve conferência de que o resultado continuou correto.

**Esse quadro é a justificativa do seu trabalho.** O seu diferencial provavelmente vai aparecer em duas colunas: aplicar as técnicas **uma de cada vez** e **conferir se o resultado continuou correto** depois de otimizar — coisa que boa parte dos trabalhos de desempenho não faz. Se você encontrar um trabalho que já faz exatamente isso no mesmo contexto, avise o orientador: em outubro ainda dá tempo de ajustar o recorte.

## Regras para o referencial inteiro

- **Toda afirmação técnica precisa de referência.**
- **Não empilhe citações.** O capítulo não pode ser "Fulano diz X. Beltrano diz Y". Explique com suas palavras e ligue ao seu trabalho.
- **Documentação oficial** (Django, MySQL, Redis) serve para descrever a ferramenta, não para fundamentar conceito. Para conceito, use livro ou artigo.
- **Nada de blog, Stack Overflow ou site sem autoria** nas Referências. Você vai usar muito esse material para resolver problema técnico — isso é normal e não tem problema —, mas ele não entra na lista.
- **Nunca cite o que você não leu.** Ferramentas de IA inventam referências com muita naturalidade.
- Meta para este trabalho: **12 a 18 referências**.

---

# 5. Metodologia
**Prazo: 20/10/2026**

Como o trabalho foi feito. Verbos no passado e linguagem impessoal ("foi realizado", "realizou-se"). Uma a duas páginas.

**Pasta com metodologias prontas para consulta:** https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

## 5.1 Classificação da pesquisa

**Pesquise:** Gil (2017) e Prodanov e Freitas (2013) — referências completas no `README.md`. Leia os capítulos de classificação antes de escrever; não classifique de ouvido.

**Escreva:** a classificação pelos quatro critérios, **justificando cada uma** com uma frase ligada ao seu trabalho (o erro mais comum é só listar os rótulos). O enquadramento mais provável:

- **Natureza:** aplicada — o resultado serve para decisões concretas no iFIC;
- **Objetivos:** explicativa — o trabalho investiga a relação entre uma causa (a técnica aplicada) e um efeito (o tempo de resposta);
- **Abordagem:** quantitativa — todos os resultados são números;
- **Procedimentos:** **experimental**, junto com pesquisa bibliográfica. Você muda **uma coisa de cada vez** e observa o que acontece, mantendo o resto igual.

Discuta o enquadramento com o orientador antes de fechar.

## 5.2 Como o experimento foi montado

**Escreva:** a ideia das **cinco versões da mesma página**, cada uma em um endereço, todas no ar ao mesmo tempo. E a justificativa: medir todas no mesmo dia, na mesma máquina e com os mesmos dados evita que variações do computador entrem no resultado. Dedique um parágrafo inteiro a isso — é a sua principal decisão de método.

Diga o que cada versão acrescenta em relação à anterior (uma frase por versão).

**Seja honesto sobre os índices.** Índice fica no banco e acelera **todas** as versões, não só aquela em que você o criou. Explique o que você fez: mediu V0 e V1 antes de criar os índices, criou os índices e mediu V0, V1 e V2 de novo, e apresenta as duas situações. Quem avalia o artigo vai procurar exatamente por isso — encontrar a ressalva já escrita conta muito a seu favor.

Diga também que você **conferiu se as cinco versões mostram a mesma coisa**, por teste automatizado. Otimização que muda o resultado não é otimização, é defeito. Poucos trabalhos fazem essa conferência; diga que você fez.

Uma **figura** simples com as cinco versões e o que cada uma acrescenta ajuda muito o leitor. Use o draw.io, que é gratuito.

## 5.3 Protocolo de medição

Passe para o texto, em prosa, o protocolo que você escreveu em `docs/protocolo.md` na Sprint 3:

- base de dados grande carregada;
- `DEBUG` desligado e ferramenta de depuração desativada;
- servidor Waitress (ou Gunicorn), e não o `runserver` do Django;
- um minuto de aquecimento descartado antes de cada medição;
- três minutos de medição;
- três repetições de cada cenário;
- dois cenários: 10 e 50 usuários simultâneos;
- métricas anotadas: consultas por requisição, tempo médio, mediana, p95, requisições por segundo e erros.

**Justifique as escolhas, não só declare.** Por que três repetições? Porque uma medição sozinha pode sair distorcida. Por que descartar o aquecimento? Porque a primeira execução é sempre mais lenta, já que o banco ainda não tem nada em memória. Por que não usar o `runserver`? Porque ele atende um pedido por vez e é de desenvolvimento — medir carga nele mediria o `runserver`, não a aplicação. Cada uma dessas frases mostra que você entendeu o que estava fazendo.

## 5.4 Etapas do desenvolvimento

Liste as etapas em ordem, da pesquisa bibliográfica até a bateria final de medições, mencionando que o desenvolvimento foi feito em sprints semanais com acompanhamento do orientador. Uma figura do fluxo ajuda.

**Não confunda com Materiais e Métodos.** Aqui vai a ideia geral e a ordem; lá vão as ferramentas, as versões e os detalhes.

---

# 6. Materiais e Métodos
**Prazo: 27/10/2026**

Vale a analogia do `README.md`: **lista de ingredientes** mais **modo de preparo**. Em trabalho de desempenho, é esta seção que permite (ou impede) que outra pessoa repita o experimento.

## 6.1 Materiais

Para **cada** item, escreva três coisas: **o que é** (uma ou duas frases, com referência — a documentação oficial serve), **para que foi usado** e **por que foi escolhido**. Escrever só "foi utilizado Django" não vale nada.

| Ferramenta | O que dizer além da versão |
|---|---|
| Python 3.12 | Linguagem do protótipo; é a do projeto iFIC |
| Django 5 | *Framework* e ORM avaliados; é o do projeto iFIC |
| MySQL 8 | Banco de dados; **justifique a escolha** (ver abaixo) |
| Redis | Guarda o cache na memória; diga como foi instalado (WSL2, Memurai ou Linux) |
| `django-redis` | Liga o Redis ao sistema de cache do Django |
| `mysqlclient` ou `PyMySQL` | Driver de acesso ao banco; diga qual dos dois você usou |
| Waitress ou Gunicorn | Servidor usado nas medições, no lugar do `runserver` |
| Locust | Ferramenta de teste de carga |
| `django-debug-toolbar` | Usada para **ver** as consultas durante o desenvolvimento; **desligada nas medições** |
| `Faker` | Geração dos dados fictícios |
| Testes do Django | Contagem de consultas, comparação entre versões e teste do cache |
| Google Sheets / Excel | Organização das medições e geração dos gráficos |
| Git | Versionamento, em subpasta dentro do repositório compartilhado do projeto |

**A justificativa do MySQL é obrigatória**, porque a temática original previa outro banco. O argumento é técnico: o trabalho mede o que acontece **com várias pessoas acessando ao mesmo tempo**, e o SQLite guarda tudo em um arquivo único que ele trava a cada escrita — o que seria medido é a trava do arquivo, não as consultas. Por isso o experimento exige um banco cliente-servidor.

Deixe claro também, para não confundir o leitor, que **o Redis não substitui o MySQL**: os dados continuam no banco, e o Redis guarda apenas uma cópia pronta do resultado.

**O ambiente de execução — sem isto nada é replicável.** Informe: processador (modelo e número de núcleos), memória RAM, tipo de disco (SSD ou HD), sistema operacional e versão. Diga também que o banco, o cache, a aplicação e o Locust rodaram **todos na mesma máquina** — isso é uma limitação e precisa aparecer.

## 6.2 Métodos

**a) O protótipo.** Descreva o modelo de dados (com uma figura do diagrama) e o que a listagem mostra. Diga por que essa página foi escolhida: é a mais acessada de um sistema desse tipo e concentra o acesso no período de inscrições.

**b) A base de dados fictícia.** Quantos cursos, turmas, candidatos e inscrições foram gerados; que foi usada a biblioteca `Faker` em português, com **semente fixa** (o que faz o script gerar sempre os mesmos dados, permitindo que outra pessoa reproduza exatamente a sua base); e as regras de coerência que foram garantidas. Declare que não há dado real de pessoas (LGPD) e que não houve participantes humanos.

**c) As cinco versões.** Um parágrafo curto por versão, dizendo **exatamente** o que mudou. Seja preciso: "aplicou-se `select_related` sobre curso, eixo e campus" é informação que dá para repetir; "otimizaram-se as consultas" não é. Um trecho de código curto ajuda, quando esclarecer.

**d) Como cada número foi obtido.** O número de consultas veio de teste automatizado do Django; o tempo de resposta e as requisições por segundo vieram dos relatórios do Locust; o espaço ocupado pelos índices veio de uma consulta ao `information_schema` do MySQL.

**e) Os testes de conferência.** O teste que compara a saída das cinco versões, e os testes que verificam se o cache mostra o dado atualizado depois de uma alteração. Diga quais situações foram testadas (alterar turma, alterar curso, criar inscrição, apagar turma).

**f) Como os dados foram analisados.** Que cada cenário foi repetido três vezes e que os valores apresentados são a média dessas repetições, com o desvio padrão informado. Diga como calculou a melhora percentual em relação à V0.

---

# 7. Resultados e Discussão
**Prazo: 10/11/2026**

A seção mais importante. Três a quatro páginas. Organize na mesma ordem dos objetivos específicos.

> **Regra sem exceção:** toda figura, tabela, quadro ou código é **anunciado no texto antes** de aparecer e **explicado depois**. Nunca duas figuras seguidas sem texto entre elas.

## 7.1 O protótipo construído

Curta e direta — o protótipo é o meio, não o fim. Apresente o diagrama do modelo de dados, uma captura da página funcionando e os números da base gerada (quantas turmas, quantas inscrições). Não gaste mais de meia página aqui.

## 7.2 Número de consultas por requisição

Comece por este resultado, porque ele é o mais limpo (não varia de uma execução para outra) e porque explica todos os outros.

Tabela com uma linha por versão e o número de consultas. Mostre também o SQL gerado pela V0 e pela V1 — o contraste entre uma página que faz centenas de consultas e outra que faz duas é a figura mais didática que o seu artigo pode ter.

**Discuta:** que a queda de V0 para V1 é a prova direta de que o problema N+1 foi eliminado. E comente algo importante sobre a V3: o número de consultas dela **não cresce** quando há mais turmas na listagem. Não é só ser um número menor — é ser um número que para de crescer com o tamanho da base. Essa é a propriedade que realmente importa.

## 7.3 Tempo de resposta e requisições por segundo

A tabela principal do artigo, uma para cada cenário (10 e 50 usuários):

| Versão | Consultas | Tempo médio (ms) | p95 (ms) | Req/s | Melhora sobre a V0 |
|---|---|---|---|---|---|

Use vírgula como separador decimal, o mesmo número de casas decimais em toda a coluna, e informe o desvio padrão das três repetições.

Faça dois ou três gráficos de barras (tempo médio por versão, p95 por versão, consultas por versão). Coloque a unidade no eixo e, se o eixo vertical não começar em zero, avise na legenda.

**Discuta — e discutir é mais do que apresentar:**

- **qual técnica rendeu mais.** É provável que o cache ganhe em número bruto e que o `select_related` ganhe em "resultado por esforço". Diga isso com os números na mão;
- **o que acontece quando a concorrência aumenta.** Este costuma ser o resultado mais interessante: a diferença entre as versões tende a **crescer** com mais usuários, porque a versão ingênua satura antes. Se a V0 começou a dar erro com 50 usuários enquanto a V4 continuou respondendo, isso é um resultado forte — mostre, inclusive com o número de erros;
- **a diferença entre média e p95.** Se a média melhorou pouco mas o p95 caiu muito, o ganho real para as pessoas foi maior do que a média sugere. Explique — é para isso que você definiu percentil no Referencial;
- **qualquer resultado que tenha te surpreendido.** Se alguma otimização rendeu menos do que você esperava, ou até piorou, **esse é o seu melhor resultado**. Resultado inesperado é o que um artigo tem de mais valioso. Não esconda nem suavize: explique o motivo.

## 7.4 Efeito e custo dos índices

Tabela "sem índices × com índices", para V0, V1 e V2, deixando claro que o índice beneficiou **todas** as versões.

Mostre as saídas do `EXPLAIN` antes e depois, comentando o que mudou: antes o banco lia a tabela inteira (`type: ALL`, `key: NULL`), depois passou a usar o índice.

**Apresente o custo**, que é o que diferencia o seu trabalho: quanto espaço os índices ocuparam e quanto tempo a mais a carga da base passou a levar. A maioria dos trabalhos só mostra o ganho.

## 7.5 Cache: ganho e atualização

Apresente os tempos com **cache vazio** e com **cache cheio**, separadamente. Mostrar só o número do cache cheio seria enganoso, porque a primeira pessoa a acessar paga o custo inteiro.

Depois apresente a parte que quase nenhum trabalho faz: uma tabela com as situações de atualização testadas e o resultado de cada uma:

| Situação testada | O cache atualizou? |
|---|---|
| Alterar as vagas de uma turma | |
| Alterar o nome de um curso | |
| Criar uma inscrição nova | |
| Apagar uma turma | |

**Se alguma falhou, relate.** Explique por que falhou e o que seria preciso para corrigir. Um artigo que mostra onde o cache falha é mais útil do que um que apresenta o cache como solução perfeita.

Discuta o compromisso central: o cache é a técnica que mais acelera e a única que cria um risco novo — o de mostrar informação errada. Ligue ao domínio: vagas desatualizadas afetam um candidato de verdade.

## 7.6 Comparação final

Um quadro com uma linha por técnica e colunas: ganho em tempo, ganho em requisições por segundo, redução de consultas, custo e risco. **Este quadro é a contribuição prática do seu trabalho** — é o que alguém do projeto iFIC vai olhar para decidir o que aplicar primeiro. Se o artigo tiver uma figura memorável, que seja esta.

## 7.7 Limitações do trabalho

Uma subseção curta e honesta. Reconhecer limite aumenta a confiança no trabalho:

- os dados são **fictícios**, gerados por script, e podem se distribuir de forma diferente dos dados reais;
- **tudo rodou na mesma máquina** — aplicação, banco, cache e a ferramenta de teste de carga disputaram o mesmo processador. Os tempos absolutos seriam melhores em um servidor de verdade;
- foi avaliada **uma única página**, em **um único banco de dados**, em **uma única máquina**;
- a versão "ingênua" foi escrita pelo próprio autor e pode não representar exatamente o código de um sistema real.

Depois de listar, acrescente o argumento que salva o trabalho: como o estudo é **comparativo**, essas limitações valem igualmente para as cinco versões. O que se compara é V1 contra V0, não o número absoluto. Diga isso — mas não use esse argumento para varrer tudo para baixo do tapete.

---

# 8. Conclusão
**Prazo: 17/11/2026**

Curta e direta, geralmente menos de uma página em artigo. Nada de resultado, conceito ou citação que não tenha aparecido antes.

**Escreva, nesta ordem:**

1. **Retomada do problema e do objetivo geral**, afirmando que ele foi alcançado **e dizendo por quê, com número**: "[...] foi alcançado, uma vez que a aplicação das quatro técnicas reduziu o tempo médio de resposta de X ms para Y ms e aumentou de Z para W as requisições atendidas por segundo, com 50 usuários simultâneos."

2. **Um comentário por objetivo específico**, na mesma ordem em que foram apresentados, cada um apontando o resultado que o comprova.

3. **Contribuições:** um procedimento de medição que outras pessoas podem repetir; a medição separada do ganho e do custo de quatro técnicas sobre o mesmo cenário; o quadro comparativo com recomendações práticas; e um protótipo com o código disponível, reaproveitável pelos outros trabalhos do projeto iFIC.

4. **Limitações e dificuldades:** retome brevemente as limitações da Seção 7.7 e acrescente as dificuldades que você realmente enfrentou — instalar o banco, variação entre as medições, o tempo de carga da base, algum caso de cache que não atualizava. É aqui que o `docs/diario.md` das sprints se paga.

5. **Trabalhos futuros**, concretos:
   - aplicar as técnicas às páginas públicas e às listagens administrativas do iFIC (esta é a principal);
   - avaliar o comportamento com dados e acessos reais, depois de implantado;
   - avaliar outras páginas, além da listagem;
   - medir com mais usuários simultâneos e com a aplicação em um servidor separado da ferramenta de teste;
   - testar outras formas de atualizar o cache.

**Não escreva** que "o sistema ficou N vezes mais rápido" sem dizer em qual métrica, com quantos usuários e sobre qual base. E não generalize para "aplicações Django" o que você mediu em uma página, uma máquina e um banco.

---

# 9. Resumo, Título e revisão final
**Prazo: 24/11/2026**

## 9.1 Resumo

Escrito **por último**, depois de o texto todo estar aprovado. Parágrafo único, 150 a 500 palavras, linguagem impessoal, sem citações, sem siglas pouco conhecidas e sem menção a figuras ou tabelas (NBR 6028:2021).

Uma ou duas frases para cada item:

1. **contexto e problema:** a listagem pública de cursos FIC no pico das inscrições e o custo de consultas mal escritas em ORM;
2. **objetivo:** o que o trabalho se propôs a avaliar;
3. **método:** protótipo Django com cinco versões, base fictícia de 50.000 inscrições, testes de carga com 10 e 50 usuários, três repetições;
4. **resultados:** os números principais — queda no número de consultas, ganho no tempo médio e no p95, ganho em requisições por segundo;
5. **conclusão:** o que os números permitem afirmar e o encaminhamento (aplicação ao iFIC como trabalho futuro).

**Coloque números no resumo.** Em um trabalho que mede coisas, resumo sem número é resumo fraco — e é o resumo que faz alguém decidir se lê o resto.

O **Abstract** é a versão em inglês. Os termos da área têm forma consagrada em inglês (*latency*, *throughput*, *cache*); use-as, e não a tradução literal. Não entregue tradução automática sem revisar.

**Palavras-chave** (3 a 5), separadas por ponto e vírgula. Campo de ideias: desempenho de aplicações web; mapeamento objeto-relacional; otimização de consultas; cache; Django. Escolha os termos pelos quais alguém **procuraria** o seu trabalho.

## 9.2 Título

**Última coisa a ser definida**, em acordo com o orientador. Deve indicar **o que foi feito** e **em que contexto**, e combinar com o objetivo geral.

Pontos a cobrir: a ação (avaliação ou comparação), o objeto (técnicas de otimização de consultas e cache), a tecnologia (Django e Redis, se couber) e o contexto (catálogo público de cursos FIC / iFIC). Se houver subtítulo, separe com dois-pontos. Evite título genérico demais ("Otimização de sistemas web") e não prometa no título mais do que o artigo mediu.

## 9.3 Revisão final — checklist

Além do checklist do `README.md`:

- [ ] O objetivo geral, os objetivos específicos, as subseções de Resultados e os parágrafos da Conclusão estão na mesma ordem e falando das mesmas coisas?
- [ ] Todos os números citados no Resumo, nos Resultados e na Conclusão são **exatamente** os mesmos? (Erro mais comum: refazer uma medição e esquecer de atualizar o resumo.)
- [ ] Toda métrica que aparece nos Resultados foi explicada no Referencial?
- [ ] Toda tabela e figura é citada no texto antes de aparecer e explicada depois?
- [ ] Todas as tabelas e figuras têm identificação em cima, centralizada, e fonte embaixo?
- [ ] Os gráficos têm unidade no eixo, e o aviso na legenda caso o eixo não comece em zero?
- [ ] O ambiente de execução está descrito (processador, memória, disco, sistema, versões)?
- [ ] Está dito que cada cenário foi repetido três vezes, com o desvio padrão informado?
- [ ] A seção de limitações está presente e honesta?
- [ ] As siglas (FIC, IFRN, ORM, SGBD, LGPD, CEP) foram escritas por extenso na primeira ocorrência?
- [ ] A numeração das seções está sem ponto após o número ("2.1 Desempenho em aplicações web")?
- [ ] O texto está impessoal e no passado?
- [ ] Está declarado que os dados são fictícios e que não houve participantes humanos?
- [ ] O endereço do repositório e o caminho da sua subpasta estão no texto, e o orientador autorizou divulgá-los?
- [ ] Todos os comentários do orientador no documento do Drive foram respondidos?
- [ ] A versão final foi nomeada no histórico de versões do Drive?

---

## Referências mínimas a garantir

- **2 obras de metodologia científica** — Gil (2017) e Prodanov e Freitas (2013), já no `README.md`;
- **2 a 3 obras sobre desempenho de aplicações web e medição** (Seção 4.1);
- **2 a 3 obras sobre ORM e o problema N+1** (Seção 4.2);
- **2 obras sobre índices e banco de dados** (Seção 4.3);
- **2 a 3 obras sobre cache** (Seção 4.4);
- **3 a 5 trabalhos relacionados** (Seção 4.5);
- **a legislação citada** — Lei nº 13.709/2018 (LGPD) e Lei nº 11.892/2008;
- **a documentação oficial das ferramentas** — Django, MySQL, Redis, Locust.

Anote a referência completa de **tudo** o que ler, na seção de Referências do documento do Drive, desde o primeiro dia. Zotero e Mendeley ajudam a montar, mas confira cada entrada contra a NBR 6023:2018 antes de entregar: esses gerenciadores erram com frequência.
