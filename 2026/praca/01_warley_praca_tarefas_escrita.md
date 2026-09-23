# Praça da Paz — Orientações de Escrita do TCC (Ciclo 1)

**Estudante:** Warley — Curso Superior de Tecnologia em Sistemas para Internet
**Orientação:** Prof. Bruno Gomes — NIC
**Data de início:** 23/09/2026
**Documento do TCC:** já compartilhado pelo coordenador no **Google Drive**. Escreva diretamente nele, sem criar cópias paralelas.

> **Importante:** este documento diz **o que pesquisar e sobre o que escrever** em cada seção. Ele **não contém o texto final**. O texto é seu. As orientações gerais de escrita, as normas da ABNT e as regras de citação, figuras, tabelas e referências estão no `README.md` deste repositório; **leia-o antes de começar**. O que você vai fazer em cada semana está em `01_warley_praca_tarefas_desenvolvimento.md`.

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
- [5. Referências sugeridas para começar](#5-referências-sugeridas-para-começar)
- [6. Erros comuns em TCCs sobre teste e correção de software](#6-erros-comuns-em-tccs-sobre-teste-e-correção-de-software)
- [7. Checklist antes de cada entrega](#7-checklist-antes-de-cada-entrega)

---

## 1. Antes de começar

**O que o seu TCC afirma (em uma frase):** *"Verificamos de forma sistemática o site da Praça da Paz entre os Povos, identificamos por navegação e análise de código defeitos de visibilidade de registros desativados, de controle de acesso e de robustez, corrigimos esses defeitos seguindo um fluxo de versionamento com* issues, branches *e* pull requests, *e criamos testes automatizados que comprovam as correções e evitam que os defeitos voltem."*

**O que o seu TCC NÃO afirma:**
- **não** diz que o sistema "não tem mais bugs". Você fala só do que foi **verificado** (as páginas e os casos de teste do seu roteiro);
- **não** diz que você criou funcionalidades novas. O trabalho é de **verificação e correção**;
- **não** apresenta o código do sistema inteiro, apenas os **trechos** relacionados aos defeitos.

**Vocabulário técnico (use sempre do mesmo jeito):**
- **erro** (engano): ação humana que produz um resultado incorreto (ex.: o programador esqueceu o filtro);
- **defeito** (*bug*): a imperfeição que ficou no código (ex.: `Planta.objects.all()` em vez de `filter(status=True)`);
- **falha**: o comportamento errado que o usuário vê (ex.: a planta desativada aparece no acervo).

Essas definições estão no glossário do ISTQB e em livros de teste de software. **Defina-as no Referencial e use-as com rigor no texto todo.** "Bug" pode ser usado como sinônimo de defeito, desde que você avise isso na primeira vez.

**Como trabalhar no Google Drive:**
- escreva direto no documento compartilhado; **não crie cópias**;
- ao terminar uma seção, use **Arquivo > Histórico de versões > Nomear versão atual** (ex.: `v1 - Introdução - 30/09`);
- **resolva os comentários** do orientador antes de entregar a seção seguinte;
- ao entregar, avise o orientador dizendo **qual seção** está pronta.

**Regra de ouro:** escreva a partir do **diário de bordo**, da **planilha de bugs** e do **relatório de verificação**. O texto cresce junto com o trabalho, e não no final.

---

## 2. Cronograma de entregas

Hoje é **23/09/2026**. Cada prazo conta a partir da conclusão da etapa anterior.

| # | Seção | Prazo | Duração | Sprints que alimentam a seção |
|---|---|---|---|---|
| 1 | Introdução e Objetivo Geral | **30/09/2026** (quarta) | 1 semana a partir de hoje | Sprint 1 |
| 2 | Referencial Teórico | **14/10/2026** (quarta) | 2 semanas após a Introdução | Sprints 1 a 3 |
| 3 | Metodologia | **21/10/2026** (quarta) | 1 semana após o Referencial | Sprints 2 a 4 |
| 4 | Materiais e Métodos | **28/10/2026** (quarta) | 1 semana após a Metodologia | Sprints 1 a 5 |
| 5 | Resultados | **11/11/2026** (quarta) | 2 semanas após Materiais e Métodos | Sprints 2 a 7 |
| 6 | Conclusão | **18/11/2026** (quarta) | 1 semana após os Resultados | Sprint 8 |
| 7 | Resumo, Objetivos Específicos e Título | **25/11/2026** (quarta) | 1 semana após a Conclusão | Encerramento |

**Atenção ao ritmo dos Resultados:** as correções terminam na Sprint 6 (até 03/11) e o reteste na Sprint 7 (até 10/11). Por isso, escreva os Resultados assim:
- **de 28/10 a 03/11:** a verificação inicial (quantos bugs, de que tipo, como foram encontrados) e os exemplos já corrigidos (Grupos A e B);
- **de 04/11 a 11/11:** os bugs de segurança, o reteste, os números finais e os gráficos.

**Dica de ritmo:** escreva um pouco ao longo da semana (de preferência às quintas e sextas), e não na véspera.

---

## 3. Estrutura prevista do TCC

Siga a estrutura do `README.md`. Para este tema:

```
Título
Resumo / Palavras-chave
Abstract / Keywords
1 INTRODUÇÃO
  1.1 Objetivo geral
  1.2 Objetivos específicos
2 REFERENCIAL TEÓRICO
  2.1 Qualidade de software: erro, defeito e falha
  2.2 Teste de software: níveis, técnicas e teste de regressão
  2.3 Desenvolvimento web com Django
  2.4 Exclusão lógica e visibilidade de dados
  2.5 Segurança em aplicações web: controle de acesso e redirecionamento aberto
  2.6 Controle de versão e fluxo de trabalho colaborativo
  2.7 Trabalhos relacionados
3 METODOLOGIA
4 MATERIAIS E MÉTODOS
  4.1 O sistema verificado
  4.2 Ferramentas e ambiente
  4.3 Roteiro de verificação
  4.4 Procedimento de correção
  4.5 Testes automatizados
5 RESULTADOS E DISCUSSÃO
  5.1 Visão geral dos defeitos encontrados
  5.2 Exemplos detalhados
  5.3 Testes automatizados e reteste
  5.4 Discussão e limitações
6 CONCLUSÃO
REFERÊNCIAS
APÊNDICES (A: roteiro de verificação; B: tabela completa de defeitos; C: relatório de verificação)
```

---

## 4. Orientações por seção

---

### 4.1 Introdução

**Prazo: 30/09/2026** | Tamanho sugerido: 5 a 6 parágrafos

Siga a sequência de parágrafos do `README.md`: **contexto → problema → solução possível → solução proposta → projeto maior e escopo**.

#### Parágrafo 1 — Contextualização

**Pesquise sobre:**
- o Jardim Etnobotânico Praça da Paz entre os Povos do IFRN Campus Canguaretama: o que é e para que serve (fonte: projeto de extensão de Bezerra (2023), citado em `.llm/praca/projeto.md`; peça o documento ao orientador);
- as Leis nº 10.639/2003 e nº 11.645/2008 (ensino de história e cultura afro-brasileira e indígena);
- o site da praça: a primeira etapa (páginas públicas) e a etapa atual (sistema administrativo).

**Escreva sobre:** a importância de divulgar os saberes tradicionais indígenas e afro-brasileiros e o papel do site nessa divulgação. Termine o parágrafo dizendo que o site já está em uso, com um **painel administrativo** em que a equipe cadastra, **ativa e desativa** plantas, espaços e outros conteúdos.

#### Parágrafo 2 — Problemática

**Pesquise sobre:**
- o custo e o impacto de defeitos de software que chegam ao usuário (Pressman; Sommerville; relatórios como o do NIST sobre o custo de testes inadequados — **confira o dado na fonte original**);
- por que sistemas desenvolvidos por várias pessoas, em várias etapas, tendem a acumular inconsistências.

**Escreva sobre:** o problema concreto que você encontrou: **desativar um registro no painel nem sempre tem efeito no site público**. Dê o exemplo da planta desativada que continua aparecendo no acervo. Diga que isso é mais do que um detalhe: o administrador perde o controle do que é publicado, e alguns defeitos do mesmo tipo afetam a **segurança** (um usuário desativado que continua entrando no sistema). **Não entre em detalhes técnicos nem cite números ainda.** Eles ficam para os Resultados.

#### Parágrafo 3 — Solução possível

**Pesquise sobre:** atividades de **verificação e validação** de software e **teste de software** como forma de encontrar defeitos antes (ou depois) de chegarem ao usuário; testes automatizados de regressão.

**Escreva sobre:** de forma geral, como se costuma resolver esse tipo de problema: verificação sistemática (roteiros de teste), correção controlada e testes automatizados que impedem o defeito de voltar.

#### Parágrafo 4 — Solução proposta

**Escreva sobre:** o que **você** fez: uma verificação sistemática do site da Praça da Paz, por navegação guiada por um roteiro de casos de teste e por análise do código; o registro de cada defeito; a correção em *branches* próprias, com *issues* e *pull requests*; e a criação de testes automatizados com o *framework* de testes do Django.

#### Parágrafo 5 — Projeto maior e escopo

**Escreva sobre:** o projeto "Desenvolvimento do Sistema Administrativo e Colaborativo do Site da Praça da Paz entre os Povos", desenvolvido no Núcleo de Inovação em Computação (NIC) do IFRN Campus Canguaretama. Diga qual parte é sua: a verificação e a correção de defeitos. Diga também o que ficou **fora** do escopo (novas funcionalidades, mudanças visuais).

> Dica: se ficar longo, o parágrafo 5 pode ser dividido. Não use subtítulos dentro da Introdução.

---

### 4.2 Objetivo Geral

**Prazo: 30/09/2026** (junto com a Introdução) | Tamanho: 1 frase

Uma única frase, começando com verbo no infinitivo, que responda **o quê**, **em quê** e **para quê**. Estrutura sugerida:

> *Verbo (Identificar e corrigir / Verificar e corrigir) + o quê (defeitos de...) + em quê (no site da Praça da Paz entre os Povos do IFRN Campus Canguaretama) + para quê (de forma a garantir que... / contribuindo para...).*

**Cuidados:**
- o objetivo deve ser **alcançável** e **verificável** ao final das 8 semanas;
- não use "desenvolver um sistema": você não desenvolveu um sistema, você verificou e corrigiu um sistema existente;
- os objetivos **específicos** só serão escritos no final (seção 4.8), como pede o `README.md`.

---

### 4.3 Referencial Teórico

**Prazo: 14/10/2026** | Tamanho sugerido: 6 a 10 páginas

Relembre a função do Referencial com o vídeo do orientador: https://youtu.be/8Qztq1Q5vb0 e com a analogia do `README.md`. **Regra:** tudo o que aparecer no Referencial deve ser **usado** depois, na Metodologia, em Materiais e Métodos ou nos Resultados. Se um conceito não for usado, retire.

#### 2.1 Qualidade de software: erro, defeito e falha

**Pesquise sobre:**
- o conceito de qualidade de software (Pressman; Sommerville) e o modelo de qualidade de produto da ISO/IEC 25010 (características como **adequação funcional**, **confiabilidade** e **segurança**);
- as definições de erro, defeito e falha (glossário do ISTQB/BSTQB; Delamaro, Maldonado e Jino).

**Escreva sobre:** as definições, com um exemplo seu (a planta desativada). Relacione os seus grupos de defeitos às características da ISO/IEC 25010: a visibilidade de registros desativados afeta a **adequação funcional**; o login de usuário desativado afeta a **segurança**; o erro 500 afeta a **confiabilidade**.

#### 2.2 Teste de software: níveis, técnicas e teste de regressão

**Pesquise sobre:**
- teste **caixa-preta** (funcional) e **caixa-branca** (estrutural);
- **teste exploratório** e teste baseado em **casos de teste** (roteiros);
- **teste de unidade**, **teste de integração** e **teste de sistema**;
- **teste de regressão**: o que é e por que automatizar;
- o princípio de que "testes mostram a presença de defeitos, não a sua ausência" (Dijkstra, citado no *syllabus* do ISTQB).

**Escreva sobre:** cada conceito de forma curta, sempre dizendo **como ele aparece no seu trabalho**: a navegação guiada pelo roteiro é teste caixa-preta de sistema; a leitura do código para achar a causa é análise caixa-branca; os testes do Django que você escreveu são testes automatizados de regressão.

#### 2.3 Desenvolvimento web com Django

**Pesquise sobre** (use a documentação oficial do Django como fonte principal):
- a arquitetura MTV (*Model–Template–View*);
- o ORM: *models*, *QuerySets*, `all()`, `filter()` e `get_object_or_404`;
- o *framework* de testes do Django (`TestCase`, *test client*, `assertContains`).

**Escreva sobre:** o suficiente para o leitor entender os seus trechos de código nos Resultados. Uma figura simples do fluxo MTV (requisição → *view* → *model*/banco → *template* → resposta) ajuda muito. **Faça a figura você mesmo** (Google Desenhos, por exemplo) e siga as regras de figuras do `README.md` (legenda acima, fonte abaixo).

#### 2.4 Exclusão lógica e visibilidade de dados

**Pesquise sobre:** **exclusão lógica** (*soft delete*) × **exclusão física**: por que sistemas preferem "desativar" a "apagar" (histórico, auditoria, possibilidade de reativar, integridade das relações entre tabelas) e qual é o risco dessa escolha: **toda consulta precisa lembrar do filtro**.

**Escreva sobre:** esse é o conceito central do seu Grupo A. Explique que o campo `status` implementa a exclusão lógica e que o defeito acontece quando uma consulta "esquece" o filtro. Esta seção prepara o leitor para entender por que o mesmo defeito apareceu em tantos lugares.

> Fontes: há pouco material acadêmico com o termo *soft delete*. Procure em livros de banco de dados e de padrões de projeto (ex.: Fowler, *Patterns of Enterprise Application Architecture*) e na documentação do Django sobre *Managers*. Peça ajuda ao orientador se não encontrar.

#### 2.5 Segurança em aplicações web: controle de acesso e redirecionamento aberto

**Pesquise sobre:**
- o OWASP Top 10 (versão 2021 ou a mais recente publicada), em especial **A01 – Quebra de Controle de Acesso**;
- **redirecionamento aberto** (*open redirect*, CWE-601) e o seu uso em *phishing*;
- autenticação no Django (`is_active`, *authentication backends*) e a função `url_has_allowed_host_and_scheme`;
- a LGPD (Lei nº 13.709/2018), art. 46, sobre medidas de segurança para proteger dados pessoais. O projeto já cita a LGPD e o Marco Civil da Internet.

**Escreva sobre:** os dois problemas de segurança do seu trabalho, em linguagem acessível, e por que um usuário desativado que continua entrando no sistema é um risco para os dados pessoais cadastrados.

> **Cuidado ético:** descreva os defeitos de segurança de forma conceitual. **Não publique** passo a passo de ataque contra o site em produção. Nos Resultados, deixe claro que os testes foram feitos no **ambiente local** e que os defeitos já estavam **corrigidos** quando o texto foi publicado.

#### 2.6 Controle de versão e fluxo de trabalho colaborativo

**Pesquise sobre:** Git, *branches*, *issues*, *pull requests*, revisão de código e *Conventional Commits* (documentação do Git, do GitHub e da especificação *Conventional Commits*). Cite também a norma de desenvolvimento do NIC (`nic_projetos_tarefas`).

**Escreva sobre:** como esse fluxo garante **rastreabilidade**: é possível ligar cada defeito (planilha) → *issue* → *commit* → *pull request* → teste. Essa rastreabilidade é um dos pontos fortes do seu trabalho.

#### 2.7 Trabalhos relacionados

**Pesquise** no Google Acadêmico, na SBC OpenLib (SOL) e no Portal de Periódicos da CAPES (links no `README.md`), com termos como:
- "teste de software" "aplicação web" "estudo de caso";
- "teste de regressão" "Django" ou "Python";
- "teste exploratório" "defeitos";
- "OWASP" "vulnerabilidades" "aplicações web" "instituição de ensino";
- TCCs de outros *campi* do IFRN e de outros IFs sobre testes em sistemas web (BDTD e repositório institucional do IFRN).

**Escreva sobre:** de 3 a 5 trabalhos. Para cada um: o que fizeram, como fizeram, o que encontraram e **em que o seu trabalho se parece ou se diferencia**. Uma tabela comparativa no final ajuda (ex.: colunas "Trabalho", "Sistema avaliado", "Técnica de teste", "Correção dos defeitos?", "Testes automatizados?").

Consulte também os TCCs anteriores orientados no NIC: https://drive.google.com/drive/folders/1OwAjk47aQWuRKLf-ktesizSax9csEtXO?usp=sharing

---

### 4.4 Metodologia

**Prazo: 21/10/2026** | Tamanho sugerido: 1,5 a 2 páginas

Siga o `README.md` (Classificação da pesquisa, Pesquisa bibliográfica, Etapas do desenvolvimento). Veja exemplos de metodologia na pasta do Drive indicada acima.

**Classificação da pesquisa — pesquise e escreva sobre:**
- **natureza:** aplicada (resolve um problema real de um sistema em uso);
- **abordagem:** qualitativa e quantitativa. É qualitativa porque descreve e interpreta os defeitos, e quantitativa porque conta os defeitos por grupo, por gravidade e os testes;
- **objetivos:** exploratória e descritiva. Justifique cada uma;
- **procedimento:** **estudo de caso** (um único sistema, em seu contexto real) somado a pesquisa bibliográfica.

Use autores de metodologia científica (ex.: Gil, *Como elaborar projetos de pesquisa*; Wazlawick, *Metodologia de pesquisa para ciência da computação*) e **cite a edição que você consultou**.

**Pesquisa bibliográfica:** onde pesquisou, com quais termos, em que período. Anote isso no diário **enquanto** pesquisa o Referencial.

**Etapas — descreva em ordem (uma figura com o fluxo ajuda):**
1. Estudo do sistema e preparação do ambiente e dos dados de teste;
2. Elaboração do roteiro de verificação (casos de teste);
3. Execução do roteiro e registro dos defeitos (inclua a varredura prévia do orientador como **ponto de partida**, e diga isso com transparência);
4. Localização da causa no código;
5. Correção, em ciclos semanais (*sprints* do Scrum), com *issue* → *branch* → *commit* → teste automatizado → *pull request*;
6. Reteste completo (regressão) e consolidação dos resultados.

**Não entre em detalhes técnicos aqui** (comandos, nomes de arquivos, colunas da planilha). Isso vai para Materiais e Métodos.

---

### 4.5 Materiais e Métodos

**Prazo: 28/10/2026** | Tamanho sugerido: 3 a 5 páginas

Lembre-se da analogia da **receita de bolo** do `README.md`: outra pessoa deve conseguir **repetir** a sua verificação lendo esta seção.

#### 4.1 O sistema verificado

**Escreva sobre:** o site da Praça da Paz: tecnologias (Python, Django, SQLite no desenvolvimento, Bootstrap), organização em apps (`core` para as páginas públicas; `plantas`, `espacos`, `usuarios` e `acontecimentos` para o painel), os cadastros que possuem status e a **versão verificada** (commit inicial `7b489f0`, de 23/09/2026). Um quadro com "Página – URL – Pública ou painel – Dados exibidos" (Tarefa 2.1) cabe muito bem aqui.

#### 4.2 Ferramentas e ambiente

**Escreva sobre:** um quadro com ferramenta, versão e finalidade: Python, Django, Git/GitHub, navegador (nome e versão), ferramentas do desenvolvedor do navegador, Google Planilhas, editor de código, sistema operacional. Explique a escolha por ferramentas **gratuitas** e sem instalação de programas (apenas `pip`), pela restrição dos computadores do laboratório.

Descreva também os **dados fictícios de teste**: quantos registros de cada tipo, quantos desativados e por que não foram usados dados reais (LGPD).

#### 4.3 Roteiro de verificação

**Escreva sobre:** como o roteiro foi construído (um caso de teste por cadastro com status, mais os casos de login, de `next` e de parâmetros inválidos). Mostre **um caso de teste completo como exemplo** (quadro) e remeta o roteiro inteiro para o **Apêndice A**. Explique a classificação de gravidade (Alta, Média, Baixa) e os critérios usados. Explique as fontes de evidência: prints, código de status HTTP (aba Rede do navegador) e a página de Erros do painel.

#### 4.4 Procedimento de correção

**Escreva sobre:** o fluxo de trabalho da norma do NIC: uma *issue* por defeito, *branches* `fix/...`, um *commit* por defeito no padrão *Conventional Commits*, *pull request* por *sprint* com prints antes/depois e revisão do orientador. Uma figura com esse fluxo, ligando planilha → *issue* → *branch* → *commit* → PR, deixa claro o conceito de rastreabilidade.

#### 4.5 Testes automatizados

**Escreva sobre:** como os testes foram escritos (`django.test.TestCase`, banco de dados temporário criado no `setUp`, *test client* simulando o navegador, `assertContains`, `assertNotContains` e verificação de código de status). Mostre **um** teste curto como exemplo (figura ou quadro com o código) e explique o experimento de validação: **rodar o teste sem a correção (deve falhar) e com a correção (deve passar)**.

---

### 4.6 Resultados

**Prazo: 11/11/2026** | Tamanho sugerido: 6 a 10 páginas

Veja no `README.md` o que pode ser apresentado e os cuidados. **Todo resultado precisa de evidência** (print, tabela, trecho de código, número da planilha).

#### 5.1 Visão geral dos defeitos encontrados

**Escreva sobre:**
- uma tabela-resumo: ID, defeito, grupo, gravidade, como foi identificado, situação. Se ficar grande, coloque aqui uma versão resumida e a completa no **Apêndice B**;
- os números: total de defeitos, por grupo, por gravidade, por forma de identificação (varredura prévia, navegação, página de Erros, código);
- dois gráficos (bugs por grupo; bugs por gravidade), feitos no Google Planilhas, seguindo as regras de figura do `README.md`;
- **quantos defeitos você encontrou além da varredura prévia do orientador.** Esse número mostra a sua contribuição e deve ser dito com clareza.

**Discuta:** por que o mesmo tipo de defeito (esquecer o filtro de status) se repetiu tanto? Relacione com o conceito de exclusão lógica (seção 2.4) e com o fato de o sistema ter sido desenvolvido por várias pessoas em etapas diferentes. Aponte o contraexemplo: a página de Acontecimentos **já filtrava** corretamente.

#### 5.2 Exemplos detalhados

Para cada um dos **3 exemplos** escolhidos na Tarefa 7.4, use sempre a mesma estrutura:
1. **Como foi identificado:** o caso de teste do roteiro e o print "antes";
2. **Causa:** o trecho de código com o defeito (figura com poucas linhas, destacando a linha do problema);
3. **Correção:** o trecho corrigido;
4. **Comprovação:** o print "depois" e o teste automatizado (falhando antes, passando depois).

Sugestão de exemplos: B01 (o mais simples e didático), B05 → B08 (uma correção que revelou outro defeito: o link para espaço desativado) e B11 (segurança: usuário desativado entrando no sistema).

#### 5.3 Testes automatizados e reteste

**Escreva sobre:** quantos testes foram criados, por grupo de defeito; o print da execução final (`python manage.py test` com "OK"); o resultado do reteste completo do roteiro (Sprint 7); e se alguma correção quebrou algo que os testes detectaram (se aconteceu, **conte**: é um resultado positivo, porque mostra os testes funcionando).

#### 5.4 Discussão e limitações

**Escreva sobre:**
- o que a navegação encontrou e a leitura do código não encontraria, e vice-versa (use as suas lições aprendidas);
- **limitações:** verificação feita em ambiente local, com dados fictícios, com um único navegador; roteiro que cobre as páginas mapeadas, não todos os caminhos possíveis; parte dos defeitos partiu de uma varredura prévia; não houve teste com usuários reais;
- as decisões tomadas com o orientador (ex.: planta ativa em espaço desativado) e por quê.

---

### 4.7 Conclusão

**Prazo: 18/11/2026** | Tamanho sugerido: 1 a 1,5 página

Siga o `README.md`. **Não traga informação nova** e não cite autores aqui.

**Escreva sobre:**
- retome o problema e o objetivo geral, e diga **se foi alcançado**, com base nos números dos Resultados;
- os principais achados: a predominância de defeitos de exclusão lógica e a gravidade dos defeitos de segurança;
- a contribuição prática: um site mais confiável para a divulgação dos saberes da Praça da Paz, testes automatizados que ficam no projeto e uma regra documentada para os próximos desenvolvedores (Tarefa 8.2);
- a contribuição para a sua formação;
- **trabalhos futuros:** *Manager* para centralizar o filtro de status, testes para todas as páginas, execução automática dos testes a cada PR (GitHub Actions), unificação dos campos `status` e `is_active`, defeitos pendentes.

---

### 4.8 Resumo, Objetivos Específicos e Título

**Prazo: 25/11/2026** | Só depois de o orientador aprovar o texto completo, como pede o `README.md`.

#### Objetivos específicos

Em tópicos, com verbos no infinitivo, **um para cada etapa** que você realmente fez e que aparece nos Resultados. Pense em verbos como: *elaborar* (o roteiro), *identificar e classificar* (os defeitos), *corrigir* (os defeitos, seguindo o fluxo), *implementar* (os testes automatizados), *avaliar* (as correções por meio de reteste). Cada objetivo específico deve ter um "resultado correspondente" no capítulo 5. Se não tiver, retire o objetivo.

#### Resumo

Um parágrafo único, de 150 a 500 palavras (NBR 6028:2021), com: contexto (1 a 2 frases), problema, objetivo, método (roteiro, correção com fluxo de versionamento, testes automatizados), **principais resultados com números** (quantos defeitos, de que tipos, quantos corrigidos, quantos testes) e conclusão. De 3 a 5 palavras-chave (ex.: teste de software; Django; qualidade de software; segurança web; Praça da Paz entre os Povos). Faça também o *Abstract*.

#### Título

Claro, específico e com o sistema no título. Deve deixar claro que se trata de **verificação e correção**, e não de desenvolvimento. Estruturas possíveis (**não copie; crie o seu**):
- "Verificação e correção de defeitos em [tipo de sistema]: o caso de [sistema]"
- "[Ação] de [o quê] no [sistema] do IFRN Campus Canguaretama"

---

## 5. Referências sugeridas para começar

Pontos de partida. **Consulte a obra, confira a edição e o ano que você usou** e formate conforme a NBR 6023:2018 (exemplos no `README.md`).

- PRESSMAN, Roger S.; MAXIM, Bruce R. *Engenharia de software: uma abordagem profissional*. Porto Alegre: AMGH;
- SOMMERVILLE, Ian. *Engenharia de software*. São Paulo: Pearson;
- DELAMARO, Márcio; MALDONADO, José Carlos; JINO, Mario. *Introdução ao teste de software*. Rio de Janeiro: Elsevier;
- MYERS, Glenford J.; BADGETT, Tom; SANDLER, Corey. *The art of software testing*. Hoboken: Wiley;
- ISTQB / BSTQB. *Syllabus Certified Tester Foundation Level* (versão 4.0) e glossário em português;
- ISO/IEC 25010 (modelo de qualidade de produto de software);
- OWASP. *OWASP Top 10* (versão 2021 ou mais recente);
- MITRE. *CWE-601: URL Redirection to Untrusted Site ('Open Redirect')*;
- DJANGO. Documentação oficial: *Making queries*, *Testing in Django*, *User authentication*;
- BRASIL. Lei nº 13.709/2018 (LGPD), além das Leis nº 10.639/2003 e nº 11.645/2008 já citadas no projeto;
- GIL, Antonio Carlos. *Como elaborar projetos de pesquisa*. São Paulo: Atlas;
- WAZLAWICK, Raul Sidnei. *Metodologia de pesquisa para ciência da computação*. Rio de Janeiro: Elsevier.

---

## 6. Erros comuns em TCCs sobre teste e correção de software

| Erro | Como evitar |
|---|---|
| Transformar o TCC em "diário de programação" ("depois abri o arquivo X, depois...") | Descreva o **método** e os **resultados**. O passo a passo detalhado fica no apêndice |
| Colar arquivos inteiros de código | Mostre só as linhas relevantes (antes/depois), como figura, com legenda e fonte ("Fonte: elaborado pelo autor (2026)") |
| Dizer "o sistema agora não tem erros" | Diga "os defeitos verificados foram corrigidos e os casos de teste do roteiro passaram" |
| Confundir erro, defeito e falha | Defina no Referencial e use sempre igual |
| Esconder que partiu de uma lista prévia do orientador | Seja transparente e destaque o que **você** encontrou a mais |
| Prints sem contexto | Todo print com legenda explicativa, citado no texto **antes** de aparecer |
| Expor detalhes de ataque contra o site em produção | Descreva a vulnerabilidade de forma conceitual e informe que já foi corrigida |
| Números diferentes entre Resumo, Resultados e Conclusão | Use sempre a aba "Resumo" da planilha como fonte única |

---

## 7. Checklist antes de cada entrega

- [ ] Li de novo as orientações desta seção e a parte correspondente do `README.md`
- [ ] Toda afirmação tem citação ou evidência (planilha, print, código)
- [ ] Citações no formato da NBR 10520:2023; referências na NBR 6023:2018
- [ ] Figuras e tabelas com legenda acima, fonte abaixo e citadas no texto
- [ ] Termos técnicos em inglês em itálico (*bug*, *branch*, *pull request*...)
- [ ] Resolvi os comentários do orientador na seção anterior
- [ ] Nomeei a versão no histórico do Google Docs
- [ ] Avisei o orientador de que a seção está pronta
