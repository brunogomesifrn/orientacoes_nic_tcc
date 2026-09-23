# TiParaElas — Plano de Trabalho (Ciclo 1)

**Estudante:** Mariana — Curso Superior de Tecnologia em Sistemas para Internet
**Orientação:** Prof. Bruno Gomes — NIC
**Período do Ciclo 1:** 22/09/2026 a 16/11/2026 (8 sprints de 1 semana, de terça a segunda)
**Projeto base:** TiParaElas (Python/Django), em `../tiparaelas/` — repositório privado `https://github.com/nicifrn/tiparaelas`
**Política de trabalho:** Política de Desenvolvimento de Software do NIC — `https://github.com/nicifrn/nic_projetos_tarefas`

> **Leia este documento inteiro antes de começar a Sprint 1.** Ele diz *o que* fazer, *como* fazer e *o que precisa estar pronto* ao final de cada semana. O documento complementar, com as orientações de escrita do TCC, é `01_mariana_tiparaelas_tarefas_escrita.md`.

---

## Sumário

- [1. Visão geral do ciclo](#1-visão-geral-do-ciclo)
- [2. Recorte do tema para o Ciclo 1](#2-recorte-do-tema-para-o-ciclo-1)
- [3. Ambiente e ferramentas](#3-ambiente-e-ferramentas)
- [4. Onde guardar o seu trabalho](#4-onde-guardar-o-seu-trabalho)
- [5. Rotina de trabalho](#5-rotina-de-trabalho)
- [6. Sprints](#6-sprints)
- [7. Riscos e planos B](#7-riscos-e-planos-b)
- [8. Trabalhos futuros (Ciclo 2)](#8-trabalhos-futuros-ciclo-2)
- [9. Checklist de encerramento do Ciclo 1](#9-checklist-de-encerramento-do-ciclo-1)

---

## 1. Visão geral do ciclo

A temática que você escolheu é **acessibilidade na web segundo a WCAG** (as Diretrizes de Acessibilidade para Conteúdo Web, do W3C), aplicada à plataforma TiParaElas.

A temática completa seria avaliar, corrigir o código, reavaliar e testar com usuárias, mas não será possível devido ao comitê de ética. Por isso, **neste ciclo você faz apenas a primeira parte: o diagnóstico.**

| Ciclo 1 — você, agora (22/09 a 16/11/2026) | Depois — outro(a) estudante ou um próximo ciclo |
|---|---|
| **Analisar** a acessibilidade de 8 páginas do TiParaElas | **Corrigir** o código seguindo o seu plano |
| Registrar as barreiras encontradas em uma planilha | Reavaliar as páginas com o seu roteiro (antes × depois) |
| Comparar o que as ferramentas automáticas encontram com o que você encontra testando manualmente | Testar com usuárias que usam tecnologia assistiva (depende do Comitê de Ética) |
| Escrever um **plano de correção** para outra pessoa executar | |

**Você não vai alterar o código do sistema neste ciclo.** O seu trabalho é observar, testar, registrar e planejar.

**Por que isso já é publicável:** um **estudo de avaliação de acessibilidade** com método claro, barreiras encontradas, comparação entre métodos e recomendações é um formato aceito em eventos como o IHC, o WebMedia e o WIT (Women in Information Technology). E o tema tem um argumento forte: uma plataforma criada para incluir mulheres na tecnologia precisa também incluir mulheres com deficiência.

---

## 2. Recorte do tema para o Ciclo 1

**Título provisório** (o título definitivo é a última coisa a ser definida):

> *Diagnóstico de acessibilidade de uma plataforma de visibilidade de mulheres na tecnologia: avaliação da plataforma TiParaElas segundo a WCAG 2.2*

**Pergunta de pesquisa:**

> Quais barreiras de acessibilidade existem nas principais páginas da plataforma TiParaElas, segundo a WCAG 2.2, e quais delas são encontradas por ferramentas automáticas e quais só aparecem na verificação manual?

Ela se divide em três questões menores (QP), que organizam todo o trabalho:

| QP | Pergunta | Sprints |
|---|---|---|
| QP1 | Quais barreiras existem nas 8 páginas avaliadas? | 3, 4 e 5 |
| QP2 | Quais barreiras as ferramentas automáticas encontram e quais só a verificação manual (teclado e leitor de tela) encontra? | 3 a 6 |
| QP3 | Que correções devem ser feitas, e em que ordem? | 7 |

**O que entra neste ciclo:**

- **8 páginas:** Início, Galeria de ações, Detalhe de uma ação, Inspirações, Detalhe de uma inspiração, Contato, Login e Cadastro;
- **12 critérios da WCAG 2.2** (lista na Tarefa 2.2), escolhidos por serem verificáveis com as ferramentas disponíveis;
- **2 ferramentas automáticas:** Lighthouse e ASES;
- **3 verificações manuais:** navegação só com teclado, zoom e contraste, e leitor de tela (Narrador do Windows).

**O que você vai entregar ao final dos 2 meses:**

1. **Planilha de barreiras** preenchida (o coração do trabalho).
2. **Relatório de diagnóstico**: quadros, gráficos e exemplos com prints.
3. **Plano de correção**: um documento para outra pessoa corrigir o site, com prioridade, local no código e sugestão de solução para cada barreira.
4. **TCC escrito** em paralelo (veja o documento de escrita).

---

## 3. Ambiente e ferramentas

Restrições do laboratório: **Windows**, sem instalação de aplicativos, sem Docker. Em desenvolvimento, o TiParaElas usa **SQLite**, então não é preciso configurar o MySQL.

**Todas as ferramentas deste ciclo já estão no computador ou funcionam no navegador:**

| Ferramenta | Para quê | Onde |
|---|---|---|
| **Lighthouse** | Avaliação automática (dá uma nota de 0 a 100 para a acessibilidade) | Já vem no Chrome/Edge: tecla F12 > aba *Lighthouse* |
| **ASES Web** | Avaliação automática segundo o eMAG (modelo de acessibilidade do governo brasileiro) | `https://asesweb.governoeletronico.gov.br` |
| **WebAIM Contrast Checker** | Verificar se a cor do texto contrasta bem com o fundo | `https://webaim.org/resources/contrastchecker/` |
| **Narrador do Windows** | Leitor de tela (lê a página em voz alta, como uma pessoa cega usaria) | Já vem no Windows: **Ctrl + Windows + Enter** liga e desliga |
| **Google Planilhas** | Planilha de barreiras e gráficos | navegador |
| **Google Docs** | Relatório de diagnóstico e plano de correção | navegador |
| Fone de ouvido | Para usar o Narrador sem atrapalhar o laboratório | traga o seu |

> Você **não precisa** escrever scripts neste ciclo. Os gráficos são feitos no próprio Google Planilhas.

---

## 4. Onde guardar o seu trabalho

Crie no Google Drive uma pasta `Mariana - Acessibilidade TiParaElas` (compartilhada com o orientador), com esta organização:

```
Mariana - Acessibilidade TiParaElas/
├── diario/                    <- um documento por semana (diário de bordo)
├── prints/
│   ├── lighthouse/
│   ├── ases/
│   ├── teclado/
│   ├── contraste/
│   └── leitor_de_tela/
├── Planilha de barreiras      <- Google Planilhas
├── Checklist dos 12 critérios <- Google Docs
├── Relatório de diagnóstico   <- Google Docs
└── Plano de correção          <- Google Docs
```

**Nome dos prints:** `pagina_ferramenta_numero.png` — por exemplo, `P03_teclado_02.png`. Assim você encontra tudo depois.

**Repositório do projeto:** só na Sprint 8, a planilha e o plano de correção serão copiados para o repositório do TiParaElas, em uma branch, seguindo a política do NIC (Tarefa 8.2). Até lá, você **só lê** o código, sem alterá-lo.

---

## 5. Rotina de trabalho

| Quando | O quê |
|---|---|
| **Terça (início da sprint)** | Ler as tarefas da semana e tirar dúvidas com o orientador |
| **Cada dia de trabalho** | Anotar no diário: o que fez, o que encontrou, o que travou |
| **Segunda (fim da sprint)** | Conferir a lista "Pronto quando", avisar o orientador |
| **Reunião semanal** | Mostrar a planilha e os prints e apresentar as dúvidas |

**O diário é importante:** boa parte da Metodologia e dos Resultados do TCC sai dele.

**Regra dos 45 minutos:** travou? Tente por 45 minutos. Se não resolver, mande a dúvida ao orientador contando: o que queria fazer, o que fez, o que apareceu na tela (print) e o que já tentou.

**Três cuidados para toda a avaliação:**
1. Use sempre **o mesmo navegador** (anote qual e a versão).
2. Use sempre **os mesmos dados fictícios** (Tarefa 1.3). **Nunca use dados reais de pessoas.**
3. **Não altere o código.** Se o sistema mudar no meio da avaliação, os resultados deixam de ser comparáveis. Trabalhe sempre na mesma versão (Tarefa 1.1).

---

## 6. Sprints

| Sprint | Período | Tema |
|---|---|---|
| 1 | 22/09 a 28/09 | Ambiente, dados fictícios e primeiras leituras |
| 2 | 29/09 a 05/10 | Amostra, checklist dos 12 critérios e planilha |
| 3 | 06/10 a 12/10 | Avaliação automática (Lighthouse e ASES) |
| 4 | 13/10 a 19/10 | Verificação manual 1: teclado, zoom e contraste |
| 5 | 20/10 a 26/10 | Verificação manual 2: leitor de tela e formulários |
| 6 | 27/10 a 02/11 | Organização dos resultados e gráficos |
| 7 | 03/11 a 09/11 | Plano de correção |
| 8 | 10/11 a 16/11 | Revisão, entrega no repositório e encerramento |

> Feriados: 12/10 (fim da Sprint 3) e 02/11 (fim da Sprint 6). Nessas semanas, feche a sprint na sexta-feira anterior.

---

### Sprint 1 — Ambiente, dados fictícios e primeiras leituras (22/09 a 28/09/2026)

**Objetivo:** ter o TiParaElas rodando com dados de exemplo e entender o que é acessibilidade na web.

#### Tarefa 1.1 — Rodar o TiParaElas no seu computador

*Como fazer a primeira vez* (PowerShell, dentro da pasta `tiparaelas/`):

1. Atualize o código: `git checkout develop` e depois `git pull`.
2. Anote o código da versão que você vai avaliar: `git log -1 --format=%h`. Esse código (ex.: `ff0d958`) vai para o TCC. **Não faça `git pull` de novo até o fim da avaliação**, a menos que o orientador peça.
3. Ative o ambiente virtual: `.\venv\Scripts\Activate`. Se o PowerShell bloquear, rode antes `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`.
4. `pip install -r requirements.txt`, depois `python manage.py migrate` e `python manage.py runserver`.
5. Abra `http://127.0.0.1:8000/` e navegue pelo site.
6. Anote no diário a versão do Chrome (menu ⋮ > Ajuda > Sobre o Google Chrome).

#### Tarefa 1.2 — Criar a pasta no Google Drive

Crie a estrutura da seção 4 e compartilhe com o orientador. Crie o primeiro diário: `2026-09-22 - Sprint 1`.

#### Tarefa 1.3 — Cadastrar dados fictícios

Um site vazio não mostra os problemas. Por exemplo: sem imagens cadastradas, não dá para saber se as imagens têm descrição.

*Como fazer:*

1. Crie quatro administradores (pois cada usuário só pode criar 1 perfil de inspiração): `python manage.py createsuperuser`.
2. Entre no sistema e cadastre, pela área interna, **dados inventados**: 6 ações (com imagem principal e algumas imagens na galeria; coloque um vídeo do YouTube em 2 delas) e 4 perfis de inspiração (com foto e frase), um para cada usuário administrador que você criou. Deixe **pelo menos 1 perfil bem completo** (foto, frase, 3 imagens na galeria, trajetória com 2 ou 3 etapas, links e palavras-chave): ele será a página P05 da avaliação. Use imagens gratuitas (por exemplo, do site Unsplash) e nomes inventados.
3. **Faça uma cópia de segurança** para não perder esses dados: com o servidor parado, copie o arquivo `db.sqlite3` e a pasta `media/` para uma pasta fora do projeto (por exemplo, `Documentos\backup_tiparaelas\`). Se algo der errado, basta copiar de volta.

#### Tarefa 1.4 — Leitura: o que é acessibilidade na web

Leia e faça um resumo de uma página, com as suas palavras, no diário:

1. **"Introdução à Acessibilidade Web"** do W3C/WAI (existe em português): `https://www.w3.org/WAI/fundamentals/accessibility-intro/pt-BR`.
2. **"WCAG Overview"** (visão geral da WCAG; use o tradutor do navegador se preferir): `https://www.w3.org/WAI/standards-guidelines/wcag/`. Entenda os **4 princípios** (perceptível, operável, compreensível e robusto) e os **níveis A, AA e AAA**.
3. Assista a um vídeo curto de uma pessoa cega usando leitor de tela no computador (procure no YouTube "como uma pessoa cega usa o computador"). Anote o que mais chamou a sua atenção.

*Pronto quando:*
- [ ] TiParaElas rodando, com a versão (código do commit) e a versão do Chrome anotadas
- [ ] Dados fictícios cadastrados e cópia de segurança feita
- [ ] Pasta do Drive criada e compartilhada
- [ ] Resumo das leituras no diário

---

### Sprint 2 — Amostra, checklist e planilha (29/09 a 05/10/2026)

**Objetivo:** definir exatamente **o que** será avaliado e **como**, antes de começar.

#### Tarefa 2.1 — Definir as 8 páginas da amostra

No início do Relatório de diagnóstico, monte este quadro com o endereço exato de cada página (abra cada uma no navegador e copie o endereço):

| Código | Página | Endereço |
|---|---|---|
| P01 | Início | `http://127.0.0.1:8000/` |
| P02 | Galeria de ações | `http://127.0.0.1:8000/galeria/` |
| P03 | Detalhe de uma ação (escolha uma com galeria de fotos e vídeo) | `http://127.0.0.1:8000/acoes/...` |
| P04 | Inspirações | `http://127.0.0.1:8000/inspiracoes/` |
| P05 | Detalhe de uma inspiração (use o perfil completo da Tarefa 1.3) | `http://127.0.0.1:8000/inspiracao/...` |
| P06 | Contato | `http://127.0.0.1:8000/contato/` |
| P07 | Login | `http://127.0.0.1:8000/usuarios/login/` |
| P08 | Cadastro | `http://127.0.0.1:8000/usuarios/cadastro/` |

> **Atenção:** para ver as páginas P07 e P08, você precisa estar **deslogada**. Saia do sistema antes de avaliá-las, e depois entre de novo se precisar.

Escreva também **por que** essas páginas foram escolhidas: são as mais visitadas pelo público e incluem os principais tipos de conteúdo (textos, imagens, vídeo, menus e formulários). O detalhe de inspiração é a página que mostra as "mulheres que inspiram", o centro da proposta do TiParaElas. Login e Cadastro são a porta de entrada de quem quer participar da plataforma.

#### Tarefa 2.2 — Montar o checklist dos 12 critérios

Crie o documento `Checklist dos 12 critérios`. Para cada critério, escreva **com as suas palavras**: (a) o que ele exige; (b) um exemplo de erro; (c) como você vai verificar. Consulte a explicação de cada critério no site do W3C (*Understanding WCAG 2.2*) — dá para usar o tradutor do navegador.

| # | Critério WCAG 2.2 | Nível | Em poucas palavras | Como verificar |
|---|---|---|---|---|
| 1 | 1.1.1 Conteúdo não textual | A | Imagens têm descrição (texto alternativo) | Ferramentas + leitor de tela |
| 2 | 1.3.1 Informações e relações | A | Títulos, listas e regiões estão marcados corretamente no HTML | Leitor de tela (lista de títulos) |
| 3 | 1.4.3 Contraste mínimo | AA | O texto contrasta com o fundo (mínimo 4,5:1) | WebAIM Contrast Checker |
| 4 | 1.4.4 Redimensionar texto | AA | Com zoom de 200%, nada se perde nem se sobrepõe | Zoom do navegador |
| 5 | 2.1.1 Teclado | A | Tudo funciona sem mouse | Teclado |
| 6 | 2.4.1 Ignorar blocos | A | Há um jeito de pular o menu e ir direto ao conteúdo | Teclado |
| 7 | 2.4.2 Página com título | A | Cada página tem um título que diz o que ela é | Aba do navegador + leitor de tela |
| 8 | 2.4.4 Finalidade do link | A | Dá para entender para onde o link leva | Leitor de tela (lista de links) |
| 9 | 2.4.7 Foco visível | AA | Ao navegar com Tab, dá para ver onde se está | Teclado |
| 10 | 3.1.1 Idioma da página | A | A página informa que está em português | Ferramentas |
| 11 | 3.3.1 Identificação do erro | A | Erros de formulário são avisados de forma clara | Formulários + leitor de tela |
| 12 | 3.3.2 Rótulos ou instruções | A | Campos de formulário têm nome e instruções | Formulários + leitor de tela |

> **Justificativa para o TCC:** a WCAG 2.2 tem 55 critérios nos níveis A e AA. Estes 12 foram escolhidos porque se aplicam ao conteúdo das páginas da amostra e podem ser verificados com as ferramentas disponíveis no laboratório. Os demais ficam para um próximo ciclo. Anote isso: vai para a Metodologia.

#### Tarefa 2.3 — Criar a planilha de barreiras

**Barreira** é qualquer problema que dificulta ou impede uma pessoa com deficiência de usar a página.

Crie a planilha no Google Planilhas com estas colunas:

| Coluna | O que colocar | Exemplo |
|---|---|---|
| `id` | Número sequencial | 7 |
| `pagina` | Código da página (ou "Todas") | P03 |
| `onde` | Parte da página | Menu superior |
| `descricao` | O problema, com as suas palavras | Ao navegar com Tab, não dá para ver qual link está selecionado |
| `criterio` | Critério do checklist | 2.4.7 Foco visível |
| `lighthouse` | A ferramenta apontou? (S/N) | N |
| `ases` | A ferramenta apontou? (S/N) | N |
| `manual` | Você encontrou testando? (S/N) | S |
| `como_encontrei` | Teclado, zoom, contraste ou leitor de tela | Teclado |
| `gravidade` | Crítica, alta, média ou baixa | Alta |
| `print` | Nome do arquivo do print | P03_teclado_02.png |

**Escala de gravidade** (escreva-a no topo da planilha e use sempre a mesma):

- **Crítica:** impede a pessoa de concluir o que queria (ex.: não consegue enviar o cadastro sem mouse);
- **Alta:** dificulta muito;
- **Média:** confunde, mas dá para contornar;
- **Baixa:** incomoda pouco.

> **Regra importante:** se o mesmo problema aparece em todas as páginas (por exemplo, no menu, que é igual em todas), registre **uma linha só** e escreva "Todas" na coluna `pagina`.

*Pronto quando:*
- [ ] Quadro das 8 páginas com endereços e justificativa
- [ ] Checklist dos 12 critérios explicado com as suas palavras
- [ ] Planilha criada, com as colunas e a escala de gravidade

---

### Sprint 3 — Avaliação automática: Lighthouse e ASES (06/10 a 12/10/2026)

**Objetivo:** ver o que as ferramentas automáticas dizem sobre cada página.

> Feriado em 12/10: feche a sprint na sexta, 09/10.

#### Tarefa 3.1 — Lighthouse

*Como fazer, em cada uma das 8 páginas:*

1. Abra a página no Chrome, com o servidor rodando.
2. Pressione **F12** e abra a aba **Lighthouse** (se não aparecer, clique em `>>`).
3. Marque **somente** *Accessibility*, dispositivo **Desktop**, e clique em *Analyze page load*.
4. Anote a **nota** numa tabela no relatório (página × nota).
5. Tire print do resultado e salve em `prints/lighthouse/`.
6. Para cada item em vermelho ou laranja, clique para abrir, leia a explicação e registre na planilha (coluna `lighthouse = S`). Descubra a qual critério do checklist o problema pertence; se não pertencer a nenhum dos 12, anote na coluna `descricao` "(fora do checklist)".

#### Tarefa 3.2 — ASES

Como o site está rodando só no seu computador, o ASES não consegue acessar o endereço. Por isso, você vai **copiar o código da página**:

1. Abra a página e pressione **Ctrl + U** (abre o código-fonte).
2. **Ctrl + A** e **Ctrl + C** para copiar tudo.
3. No ASES, escolha a opção de avaliar por **código-fonte**, cole e avalie.
4. Anote o **percentual** que o ASES mostra, tire print e salve em `prints/ases/`.
5. Registre na planilha os erros apontados (coluna `ases = S`). Se o mesmo problema já estiver na planilha, vindo do Lighthouse, **não crie linha nova**: só marque `ases = S` na linha existente.

> **Limitação para anotar no diário:** ao colar o código, o ASES não carrega as folhas de estilo (CSS), então ele não consegue avaliar bem as cores. Isso vai para a seção de limitações do TCC.

#### Tarefa 3.3 — Primeira análise

No diário, responda: qual página teve a pior nota? Quais problemas aparecem nas duas ferramentas? Quais aparecem só em uma?

> **Atenção:** uma nota 100 no Lighthouse **não** significa que a página é acessível. As ferramentas automáticas só conseguem verificar parte dos problemas. É exatamente isso que você vai mostrar nas próximas sprints.

*Pronto quando:*
- [ ] Nota do Lighthouse e percentual do ASES das 8 páginas em uma tabela
- [ ] Prints salvos
- [ ] Problemas das ferramentas registrados na planilha, sem linhas repetidas

---

### Sprint 4 — Verificação manual 1: teclado, zoom e contraste (13/10 a 19/10/2026)

**Objetivo:** testar as páginas como uma pessoa que não usa mouse ou que tem baixa visão.

#### Tarefa 4.1 — Navegar só com o teclado

Muitas pessoas com deficiência motora ou visual não usam mouse. **Deixe o mouse de lado** e use só:

| Tecla | O que faz |
|---|---|
| **Tab** | Vai para o próximo link, botão ou campo |
| **Shift + Tab** | Volta |
| **Enter** | Abre o link ou aciona o botão |
| **Espaço** | Marca caixas de seleção e aciona botões |
| **Esc** | Fecha janelas e menus |

Em cada página, responda estas perguntas no diário (**sim** ou **não**, com uma explicação curta):

1. Ao apertar Tab a primeira vez, aparece algum link do tipo "Pular para o conteúdo"? *(critério 2.4.1)*
2. Ao apertar Tab, **sempre dá para ver** onde você está (uma borda, um destaque)? *(2.4.7)*
3. O foco segue uma ordem que faz sentido (de cima para baixo, da esquerda para a direita)?
4. Dá para abrir o submenu "Sobre" pelo teclado? *(2.1.1)*
5. Diminua a janela até aparecer o menu de celular (☰). Dá para abrir e fechar esse menu pelo teclado? *(2.1.1)*
6. Nas páginas P03 e P05: dá para abrir uma foto da galeria e fechá-la com Esc? Depois de fechar, o foco volta para a foto que você abriu? *(2.1.1)*
7. Nas páginas P06, P07 e P08: dá para preencher e enviar o formulário só pelo teclado? No Login, dá para usar o botão de mostrar/esconder a senha? *(2.1.1)*

Cada "não" vira uma linha na planilha (`manual = S`, `como_encontrei = Teclado`), com print.

> **Dica para tirar print do foco:** navegue com Tab até o ponto e use **Windows + Shift + S**.

#### Tarefa 4.2 — Zoom de 200%

Em cada página, pressione **Ctrl + +** até o zoom chegar a **200%** (aparece no canto da barra de endereço). Verifique: o texto continua legível? Algo fica escondido, cortado ou por cima de outra coisa? *(critério 1.4.4)*. Registre os problemas com print. Volte ao zoom normal com **Ctrl + 0**.

#### Tarefa 4.3 — Contraste das cores

1. Escolha, em cada página, os textos que parecem mais "clarinhos" (textos cinza, textos coloridos, textos pequenos sobre fundo colorido).
2. Descubra a cor: clique com o botão direito no texto > **Inspecionar**. Na aba *Styles*, procure `color` (cor do texto) e `background` (cor do fundo). Clique no quadradinho colorido para ver o código da cor (ex.: `#76707E`).
3. Coloque as duas cores no **WebAIM Contrast Checker** e anote o resultado.
4. Monte uma tabela no relatório:

| Página | Onde | Cor do texto | Cor do fundo | Contraste | Mínimo exigido | Passa? |
|---|---|---|---|---|---|---|
| Todas | Subtítulo das páginas | #76707E | #F4F2EE | ? | 4,5:1 | ? |

**Mínimo exigido:** 4,5:1 para texto normal e 3:1 para texto grande (a partir de cerca de 24px, ou 19px em negrito). Os que não passam vão para a planilha (`critério 1.4.3`).

*Pronto quando:*
- [ ] As 7 perguntas de teclado respondidas para cada página
- [ ] Zoom de 200% verificado nas 8 páginas
- [ ] Tabela de contraste com pelo menos 8 pares de cores
- [ ] Problemas registrados na planilha, com prints

---

### Sprint 5 — Verificação manual 2: leitor de tela e formulários (20/10 a 26/10/2026)

**Objetivo:** ouvir o site como uma pessoa cega o ouviria.

#### Tarefa 5.1 — Aprender o básico do Narrador

1. Coloque o fone e ligue o Narrador: **Ctrl + Windows + Enter** (o mesmo atalho desliga).
2. Nas configurações do Narrador, confirme que a voz está em **português**.
3. Treine 30 minutos em uma página qualquer (a Wikipédia é boa para treinar). Comandos úteis (a **tecla Narrador** é o **Caps Lock** ou o **Insert**):

| Comando | O que faz |
|---|---|
| Tab / Shift + Tab | Próximo / anterior link, botão ou campo |
| **H** / Shift + H | Próximo / anterior **título** |
| **K** | Próximo **link** |
| **F** | Próximo **campo de formulário** |
| **D** | Próxima **região** (menu, conteúdo principal, rodapé) |
| Tecla Narrador + **Ctrl** + **R** | Ler a página a partir do ponto atual |
| **Ctrl** | Para a leitura |

Consulte o "Guia completo do Narrador", da Microsoft, se precisar.

#### Tarefa 5.2 — Ouvir as 8 páginas

Em cada página, responda no diário:

1. Ao abrir, o Narrador lê um **título** que diz qual é a página? *(2.4.2)*
2. Navegando com **H**, os títulos fazem sentido e estão em ordem? *(1.3.1)*
3. Navegando com **D**, existe uma região de "conteúdo principal"? *(1.3.1)*
4. As **imagens** são descritas? A descrição ajuda a entender a imagem, ou é algo genérico como "Imagem 1"? *(1.1.1)*
5. Navegando com **K**, dá para entender **para onde cada link leva** só pelo nome lido? *(2.4.4)*
6. Ao chegar no botão "Sobre" do menu, o Narrador diz que ele abre um submenu e se está aberto ou fechado?

**Anote entre aspas o que o Narrador fala** (por exemplo: *"Sobre, botão, recolhido"* ou *"link"* sem nome). Essas falas são ótimos exemplos para os Resultados do TCC.

#### Tarefa 5.3 — Testar os formulários (Contato, Login e Cadastro)

Com o Narrador ligado:

1. Navegue pelos campos com **F**. O nome de cada campo é lido? Dá para saber quais são obrigatórios? *(3.3.2)*
2. Envie o formulário **vazio**. O Narrador avisa que houve erro? Ao voltar para um campo com erro, a mensagem de erro é lida? *(3.3.1)*
3. No Login, digite um e-mail e uma senha **errados** e envie. O Narrador lê a mensagem de erro? Ao chegar no botão de mostrar a senha, o Narrador diz para que ele serve e se a senha está visível ou escondida?
4. No Login, o link "Entrar com SUAP" é lido como **link** ou como **botão**? Ele leva para outra página, então o correto é ser lido como link. *(anote a fala exata)*
5. No Cadastro, escolha um **estado**. O Narrador avisa que as cidades estão carregando ou que foram carregadas?

Registre tudo na planilha (`como_encontrei = Leitor de tela`).

*Pronto quando:*
- [ ] As 6 perguntas respondidas para cada página, com as falas do Narrador anotadas
- [ ] Formulários de Contato, Login e Cadastro testados
- [ ] Problemas registrados na planilha

---

### Sprint 6 — Organização dos resultados e gráficos (27/10 a 02/11/2026)

**Objetivo:** transformar a planilha em números, quadros e gráficos para o TCC.

> Feriado em 02/11: feche a sprint na sexta, 30/10.

#### Tarefa 6.1 — Revisar a planilha

1. Procure **linhas repetidas** (o mesmo problema registrado duas vezes) e junte-as em uma só.
2. Confira se todas as linhas têm critério, gravidade e print.
3. Revise a gravidade de cada barreira usando a escala da Tarefa 2.3.

#### Tarefa 6.2 — Quadro "critério × página"

No relatório, monte um quadro com os 12 critérios nas linhas e as 8 páginas nas colunas. Em cada célula, coloque:

- **✓** — o critério é atendido na página;
- **✗** — há pelo menos uma barreira desse critério na página;
- **—** — o critério não se aplica (ex.: 3.3.1 numa página sem formulário).

Esse quadro mostra de uma vez **onde estão os problemas**.

#### Tarefa 6.3 — Gráficos no Google Planilhas

Use **Tabela dinâmica** (menu *Inserir > Tabela dinâmica*) para contar e depois *Inserir > Gráfico*. Faça:

1. **Barreiras por página** (gráfico de barras).
2. **Barreiras por gravidade** (crítica, alta, média, baixa).
3. **Barreiras por critério**.
4. **Quem encontrou cada barreira** — o gráfico mais importante do trabalho (QP2). Crie uma coluna nova `encontrada_por`, com três valores possíveis:
   - **Só ferramentas** (Lighthouse ou ASES = S e manual = N);
   - **Só manual** (manual = S e Lighthouse e ASES = N);
   - **Ambos**.

   Dica de fórmula (ajuste as letras das colunas):
   ```
   =SE(E(OU(F2="S";G2="S");H2="S");"Ambos";SE(H2="S";"Só manual";"Só ferramentas"))
   ```

Use títulos e legendas em português e cores que contrastem bem (o seu TCC também precisa ser acessível).

#### Tarefa 6.4 — Escolher os exemplos

Escolha **3 barreiras** para mostrar em detalhe no TCC. Prefira: a de maior gravidade; uma que **só** a verificação manual encontrou; e uma que as ferramentas encontraram. Para cada uma, separe: o print, a descrição e (se houver) a fala do Narrador.

*Pronto quando:*
- [ ] Planilha revisada, sem repetições
- [ ] Quadro critério × página pronto
- [ ] 4 gráficos prontos
- [ ] 3 exemplos escolhidos
- [ ] Números principais enviados ao orientador (servem para a entrega dos Resultados, em 10/11)

---

### Sprint 7 — Plano de correção (03/11 a 09/11/2026)

**Objetivo:** escrever um documento para que **outra pessoa** consiga corrigir o site sem precisar refazer a sua avaliação.

Pense assim: daqui a alguns meses, um(a) bolsista que nunca viu a sua planilha vai receber este documento. Ele precisa entender **o que corrigir, onde, em que ordem e como saber que ficou certo**.

#### Tarefa 7.1 — Encontrar onde está cada problema no código

Você não vai alterar nada, só **localizar**. O TiParaElas é organizado assim:

| Parte do site | Arquivo |
|---|---|
| Estrutura comum a todas as páginas públicas | `templates/publico/base.html` |
| Menu superior | `templates/publico/menu.html` |
| Rodapé | `templates/publico/rodape.html` |
| Cores e estilos gerais | `static/assets/css/styles.css` (as cores ficam no início, em variáveis como `--c-muted`) |
| Comportamento do menu e animações | `static/assets/js/script.js` |
| Páginas públicas (Início, Galeria, Detalhe de ação, Inspirações, Contato) | `apps/core/templates/` e `apps/acoes/templates/` |
| Detalhe de inspiração | `apps/core/templates/inspiracao_detalhe.html` |
| Login e Cadastro | `apps/usuarios/templates/login.html` e `apps/usuarios/templates/cadastro.html` |

*Como fazer:* abra a pasta do projeto no VS Code e use **Ctrl + Shift + F** (buscar em todos os arquivos) com um trecho do texto que aparece na tela. Por exemplo, para achar o menu "Sobre", busque `Sobre`. Anote o arquivo e, se possível, a linha.

> Dica: problemas que aparecem em "Todas" as páginas quase sempre estão em `base.html`, `menu.html`, `rodape.html` ou `styles.css`. **Corrigir ali resolve o problema em todas as páginas de uma vez** — por isso essas correções devem vir primeiro no plano.

#### Tarefa 7.2 — Pesquisar uma sugestão de solução

Para cada barreira, procure **como costuma ser resolvida**. Boas fontes:

- a página *Understanding* de cada critério, no site do W3C (tem uma parte chamada *Techniques*, com exemplos);
- os artigos do WebAIM (`https://webaim.org/articles/`);
- a documentação da MDN sobre acessibilidade (`https://developer.mozilla.org/pt-BR/docs/Web/Accessibility`).

Escreva a sugestão em 1 a 3 frases, sem precisar escrever o código. Exemplo: *"Adicionar, como primeiro elemento da página, um link 'Pular para o conteúdo' que leve ao conteúdo principal. Ele pode ficar escondido e aparecer só quando receber o foco do teclado (técnica G1 do W3C)."*

#### Tarefa 7.3 — Escrever o Plano de correção

No documento `Plano de correção`, faça:

1. **Introdução curta:** para que serve o documento, qual versão do sistema foi avaliada (código do commit) e onde está a planilha.
2. **Tabela de correções**, em ordem de prioridade:

| Prioridade | Barreira (id) | Critério | Onde (arquivo) | Sugestão de solução | Esforço | Como verificar se ficou certo |
|---|---|---|---|---|---|---|
| 1 | 3 | 2.4.1 Ignorar blocos | `templates/publico/base.html` | ... | Pequeno | Apertar Tab ao abrir a página: deve aparecer "Pular para o conteúdo" |

   **Como definir a prioridade:** primeiro as barreiras **críticas e altas**; entre elas, primeiro as que aparecem em **todas as páginas**; por último, as médias e baixas.
   **Esforço:** *pequeno* (mudar poucas linhas em um arquivo), *médio* (vários arquivos) ou *grande* (exige mudar o banco de dados ou o funcionamento do sistema). Na dúvida, pergunte ao orientador.

3. **Roteiro de reavaliação:** copie os passos das Sprints 3, 4 e 5 (Lighthouse, ASES, teclado, zoom, contraste e Narrador), para que a pessoa que corrigir possa **repetir a sua avaliação** e comparar antes e depois.
4. **O que não foi avaliado:** os critérios e as páginas que ficaram fora do ciclo.

#### Tarefa 7.4 — Criar as *issues* no GitHub

Para cada linha do plano (ou grupo de linhas no mesmo arquivo), crie uma *issue* no repositório do TiParaElas, como pede a política do NIC (item 12). Use:

- **título:** `[Acessibilidade][WCAG 2.4.1] Falta link para pular ao conteúdo`;
- **etiqueta:** `acessibilidade`;
- **texto:** a descrição, o arquivo, a sugestão, como verificar e o print.

Anote o número da *issue* no plano. Se você não tiver permissão para criar *issues*, peça ao orientador.

*Pronto quando:*
- [ ] Todas as barreiras com arquivo localizado e sugestão de solução
- [ ] Plano de correção completo (introdução, tabela, roteiro e o que não foi avaliado)
- [ ] *Issues* criadas e numeradas no plano

---

### Sprint 8 — Revisão, entrega no repositório e encerramento (10/11 a 16/11/2026)

#### Tarefa 8.1 — Revisão com o orientador

Apresente na reunião a planilha, os gráficos e o plano. Faça os ajustes pedidos.

#### Tarefa 8.2 — Guardar o trabalho no repositório do projeto

Para que o próximo bolsista encontre o seu trabalho junto com o código, siga a política do NIC:

```
git checkout develop
git pull
git checkout -b feature/diagnostico-acessibilidade
```

1. Crie a pasta `docs/acessibilidade/` no projeto.
2. Coloque nela: a planilha exportada em CSV (*Arquivo > Fazer download > .csv*), o Plano de correção exportado em PDF e os prints principais (em uma subpasta `prints/`).
3. Crie um arquivo `docs/acessibilidade/README.md` explicando, em poucas linhas, o que há na pasta.
4. Salve no Git:
   ```
   git add docs/acessibilidade
   git commit -m "docs: adiciona diagnóstico e plano de correção de acessibilidade"
   git push -u origin feature/diagnostico-acessibilidade
   ```
5. No GitHub, abra um *Pull Request* para a `develop` com: o objetivo, o que foi incluído e as *issues* relacionadas. **Você não aprova o próprio PR**: o orientador revisa.

> Confira antes que nenhum print tem dados reais de pessoas.

#### Tarefa 8.3 — Lições aprendidas

No diário, escreva meia página respondendo: o que foi mais difícil? O que mais surpreendeu? O que as ferramentas deixaram passar? O que você faria diferente? Esse texto ajuda a escrever a Discussão e a Conclusão do TCC.

*Pronto quando:*
- [ ] Ajustes do orientador feitos
- [ ] PR aberto com a pasta `docs/acessibilidade/`
- [ ] Lições aprendidas escritas

---

## 7. Riscos e planos B

| Risco | Plano B |
|---|---|
| O sistema não roda no computador do laboratório | Anote o erro completo e fale com o orientador no mesmo dia; enquanto isso, adiante as leituras e o checklist |
| O ASES está fora do ar | Tente em outro dia da mesma semana; se continuar fora, siga só com o Lighthouse e registre isso como limitação |
| Dificuldade com o Narrador | Treine mais um dia na Wikipédia antes de avaliar o TiParaElas; se continuar difícil, avise o orientador |
| Os dados fictícios se perderam | Copie de volta a cópia de segurança da Tarefa 1.3 |
| Atraso em uma sprint | As Sprints 3, 4, 5 e 7 são as mais importantes. Se precisar, reduza a quantidade de pares de cores na tabela de contraste ou de gráficos, e avise o orientador |

---

## 8. Trabalhos futuros (Ciclo 2)

Estes itens aparecem no TCC como trabalhos futuros:

1. **Correção das barreiras** por outro(a) estudante, seguindo o Plano de correção e as *issues*.
2. **Reavaliação** com o seu roteiro, para comparar antes e depois das correções (e gerar um segundo artigo).
3. **Avaliação dos demais critérios** da WCAG 2.2, de outras páginas (Transparência, Sobre, Atividades, recuperação de senha) e da área interna do sistema.
4. **Teste com usuárias** que usam tecnologia assistiva, após aprovação no Comitê de Ética em Pesquisa (CEP).
5. **Avaliação com o NVDA**, o leitor de tela mais usado no Brasil, se a instalação for liberada.

---

## 9. Checklist de encerramento do Ciclo 1

- [ ] Planilha de barreiras completa e revisada
- [ ] Relatório de diagnóstico com as tabelas das ferramentas, a tabela de contraste, o quadro critério × página, os 4 gráficos e os 3 exemplos
- [ ] Plano de correção completo
- [ ] *Issues* criadas no GitHub
- [ ] PR com a pasta `docs/acessibilidade/`
- [ ] Seções do TCC entregues nos prazos do documento de escrita
