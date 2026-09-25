# Praça da Paz — Plano de Trabalho: Verificação e Correção de Bugs (Ciclo 1)

**Estudante:** Warley — Curso Superior de Tecnologia em Sistemas para Internet
**Orientação:** Prof. Bruno Gomes — NIC
**Período do Ciclo 1:** 23/09/2026 a 17/11/2026 (8 sprints de 1 semana, de quarta a terça)
**Projeto base:** Site da Praça da Paz entre os Povos (Python/Django), em `../pppraca/` — repositório `https://github.com/nicifrn/pppraca`
**Fluxo de trabalho no repositório:** `https://github.com/nicifrn/nic_projetos_tarefas` — **leia antes de criar a primeira *branch***. Ele é a norma e prevalece sobre o resumo da seção 4.

> **Leia este documento inteiro antes de começar a Sprint 1.** Ele diz *o que* fazer, *como* fazer e *o que precisa estar pronto* ao final de cada semana. O documento complementar, com as orientações de escrita do TCC, é `01_warley_praca_tarefas_escrita.md`.

---

## Sumário

- [1. Visão geral do ciclo](#1-visão-geral-do-ciclo)
- [2. O que já sabemos: catálogo inicial de bugs](#2-o-que-já-sabemos-catálogo-inicial-de-bugs)
- [3. Ambiente e ferramentas](#3-ambiente-e-ferramentas)
- [4. Fluxo de trabalho no repositório](#4-fluxo-de-trabalho-no-repositório)
- [5. Onde guardar o seu trabalho e rotina](#5-onde-guardar-o-seu-trabalho-e-rotina)
- [6. Sprints](#6-sprints)
- [7. Riscos e planos B](#7-riscos-e-planos-b)
- [8. Trabalhos futuros](#8-trabalhos-futuros)
- [9. Checklist de encerramento do Ciclo 1](#9-checklist-de-encerramento-do-ciclo-1)

---

## 1. Visão geral do ciclo

O site da Praça da Paz já tem as páginas públicas (acervo, espaços, acontecimentos, contato) e o painel administrativo (cadastro de plantas, espaços, famílias, tipos, culturas, parceiros, usuários e perfis). Quase todos os cadastros têm um campo **status** (ativo/inativo), e o painel tem botões para **ativar/desativar** cada registro.

O problema: **desativar um registro nem sempre tem efeito**. Por exemplo, uma planta desativada no painel **continua aparecendo no acervo público**. Esse tipo de defeito se repete em vários pontos do sistema.

A sua tarefa neste ciclo é:

1. **Verificar** o sistema de forma organizada, navegando pelas páginas como um visitante e como um administrador;
2. **Registrar** cada bug encontrado: onde, como reproduzir, o que era esperado e o que aconteceu (com print);
3. **Localizar a causa** no código;
4. **Corrigir**, em *branches* próprias, seguindo o fluxo do NIC;
5. **Criar um teste automático** para cada correção, para garantir que o bug não volte;
6. **Retestar** tudo ao final e produzir um **relatório de verificação** (antes × depois), que vira a base dos Resultados do seu TCC.

**Por que isso é um bom TCC:** você vai aplicar, em um sistema real e em uso, conceitos de **teste de software** (teste exploratório, teste de regressão, testes automatizados), **qualidade de software** e **segurança web**. O resultado é mensurável: quantos bugs, de que tipo, de que gravidade, quantos corrigidos e quantos cobertos por testes.

**O que você NÃO vai fazer neste ciclo:** criar funcionalidades novas, mudar o layout ou reorganizar o código. **Só corrija bugs.** Se achar algo que é uma melhoria (e não um bug), registre na planilha como "sugestão" e siga em frente.

---

## 2. O que já sabemos: catálogo inicial de bugs

O orientador fez uma varredura prévia no código (versão de 23/09/2026, commit `7b489f0`) e encontrou os problemas abaixo. **Esta lista é o seu ponto de partida, não a resposta final:**

- você deve **confirmar cada um navegando pelo sistema** (é isso que vai para o TCC: *como foi identificado*);
- se algum não se confirmar, registre como "não reproduzido";
- **procure outros**. Todo bug novo que você encontrar sozinho vale muito no TCC.

### 2.1 Grupo A — Registros desativados aparecendo nas páginas públicas

A app `core` (`apps/core/views.py`) monta as páginas públicas e **não filtra pelo campo `status`** na maioria das consultas.

| ID | Bug | Onde (página) | Causa provável (código) |
|---|---|---|---|
| **B01** | Plantas desativadas aparecem no acervo | `/acervo/` | `acervo_view` usa `Planta.objects...all()` |
| **B02** | Filtros do acervo oferecem famílias e espaços desativados | `/acervo/` (caixas "Família" e "Espaço") | `acervo_view`: `FamiliaPlanta.objects.all()` e `Espaco.objects.all()` |
| **B03** | Espaços desativados aparecem na galeria de espaços | `/espacos/` | `espacos_view`: `Espaco.objects.all()` |
| **B04** | Espaços e parceiros desativados aparecem na página inicial | `/` | `index`: `Espaco.objects.all()` e `Parceiro.objects.all()` |
| **B05** | Espaço desativado continua abrindo pela URL direta | `/espacos/<número>/` | `espaco_detalhe_view`: `get_object_or_404(Espaco, pk=pk)` sem `status=True` |
| **B06** | Plantas desativadas aparecem na lista de plantas do espaço | `/espacos/<número>/` | `espaco_detalhe_view`: `Planta.objects.filter(espaco=espaco)` |
| **B07** | Planta desativada continua abrindo pela URL direta | `/plantas/<slug>/` | `planta_detalhe_view`: `get_object_or_404(Planta, slug=slug)` |
| **B08** | Detalhe da planta mostra família, tipos e culturas desativados, e um link para espaço desativado (que, depois de corrigir o B05, vira um link quebrado) | `/plantas/<slug>/` | `apps/core/templates/planta_detalhe.html` usa `planta.tipos.all`, `planta.culturas.all`, `planta.familia` e `planta.espaco` sem verificar status |

> **Modelo de como deveria ser:** a página de **Acontecimentos** já faz certo. Abra `acontecimentos_view` e `acontecimento_detalhe_view` em `apps/core/views.py` e veja o `filter(is_ativo=True)` e o `get_object_or_404(..., is_ativo=True)`. Use esse código como referência. **Atenção:** em Acontecimentos o campo se chama `is_ativo`; nos outros models ele se chama `status`.

### 2.2 Grupo B — Registros desativados oferecidos nos formulários do painel

| ID | Bug | Onde | Causa provável |
|---|---|---|---|
| **B09** | O formulário de planta oferece famílias e espaços desativados | Painel > Plantas > Cadastrar/Editar | `apps/plantas/forms.py`: `FamiliaPlanta.objects.all()` e `Espaco.objects.all()`. Compare com as linhas logo abaixo, de `tipos` e `culturas`, que **já filtram** `status=True` |
| **B10** | Os formulários de usuário oferecem ocupações e perfis desativados | Painel > Usuários > Cadastrar/Editar; Meus dados; Cadastro público | `apps/usuarios/forms.py`: `Ocupacao.objects.all()` (três formulários) e `Perfil.objects.all()` |

### 2.3 Grupo C — Segurança e controle de acesso

| ID | Bug | Onde | Causa provável |
|---|---|---|---|
| **B11** | **Usuário desativado continua conseguindo fazer login** e usar o painel | `/auth/login/` | O botão "desativar" muda o campo `status`, mas o Django só bloqueia login pelo campo `is_active`. São dois campos diferentes e um não atualiza o outro (`admin_usuarios_toggle` em `apps/usuarios/views.py`) |
| **B12** | **Redirecionamento aberto** no login: um link como `/auth/login/?next=https://site-qualquer.com` manda o usuário, depois de logar, para um site externo | `/auth/login/` e callback do SUAP | `login_view` e `suap_callback` usam o `next` sem validar |
| **B14** | (preventivo) Os *decorators* de perfil não verificam se o perfil está ativo. Hoje eles não estão em uso, mas, se forem usados, um perfil "coordenador" desativado continuará dando acesso | `apps/*/decorators.py` | `perfis.filter(nome='coordenador')` sem `status=True` |

> O B11 e o B12 são os bugs **mais graves** da lista. O B11 é **controle de acesso quebrado** (categoria A01 do OWASP Top 10) e o B12 é **redirecionamento aberto** (CWE-601), muito usado em golpes de *phishing*.

### 2.4 Grupo D — Robustez (erros 500)

| ID | Bug | Onde | Causa provável |
|---|---|---|---|
| **B13** | Parâmetros inválidos na URL derrubam a página com **erro 500** | `/acervo/?familia=abc`, `/acervo/?espaco=x`, `/acontecimentos/?tipo=x`, `/acontecimentos/?de=abc` | `acervo_view` e `acontecimentos_view` passam o texto da URL direto para o `filter()` sem validar se é número ou data |

> Esses erros ficam registrados automaticamente no painel, em **Erros** (`/usuarios/admin/erros/`). Essa página é uma ótima **fonte de evidência** para o TCC.

### 2.5 Grupo E — Baixa prioridade (registrar e decidir com o orientador)

| ID | Situação | Observação |
|---|---|---|
| **B15** | O painel (`perfil_view`) conta plantas e espaços **incluindo os desativados** | Decidir: mostrar "total" ou "ativos"? Talvez os dois |
| **B16** | As rotas da app `usuarios` estão incluídas **duas vezes** em `pppraca/urls.py` (`auth/` e `usuarios/`), então `/auth/login/` e `/usuarios/login/` funcionam | **Não corrija sem autorização**: outras partes do sistema podem depender das duas |
| **D1** | Planta **ativa** em espaço **desativado**: deve aparecer no acervo? | Sugestão: a planta aparece, mas sem o nome/link do espaço. **Confirme com o orientador** |
| **D2** | Acontecimento ativo cujo **tipo** está desativado: deve aparecer? | Decidir com o orientador |

---

## 3. Ambiente e ferramentas

Tudo gratuito, instalado via `pip` ou já disponível no laboratório.

| Ferramenta | Para quê | Observação |
|---|---|---|
| Python 3 + `venv` | Rodar o projeto | Já usado no NIC |
| Django e dependências | `pip install -r requirements.txt` | Se o `mysqlclient` falhar ao instalar, veja a seção 7 |
| Git | Versionamento | Confirme com o orientador se o Git está instalado no seu computador do laboratório |
| Editor de código | Ler e alterar o código | Use o disponível no laboratório (ex.: VS Code). Se não houver, avise |
| Navegador (Chrome ou Firefox) | Navegar e testar | Use **sempre o mesmo navegador** e anote a versão |
| Ferramentas do desenvolvedor do navegador (F12) | Ver erros e códigos HTTP | Aba **Rede (Network)** mostra o código de status (200, 404, 500) |
| Google Planilhas / Google Docs | Planilha de bugs, relatório, diário | Na sua conta institucional |
| Ferramenta de captura de tela do Windows (`Win + Shift + S`) | Prints de evidência | Já vem no Windows |
| `django.test` | Testes automáticos | Já vem com o Django, nada a instalar |

**Não use Docker.** O projeto roda com SQLite no modo de desenvolvimento, sem instalar banco de dados.

---

## 4. Fluxo de trabalho no repositório

Você trabalha **no repositório principal do projeto** (`nicifrn/pppraca`), sempre em ***branches* de correção**. **Nunca faça commit direto na `main`.**

**Antes de criar a primeira *branch*, leia `https://github.com/nicifrn/nic_projetos_tarefas`.** Se houver divergência com o resumo abaixo, **a norma do NIC prevalece**. Avise o orientador para corrigir este documento.

**Resumo do fluxo:**

1. **Uma *issue* por bug** no GitHub do `pppraca`, com o ID da planilha no título. Exemplo: `[B01] Plantas desativadas aparecem no acervo público`. No corpo, cole os passos para reproduzir, o esperado, o obtido e o print.
2. **Uma *branch* por grupo de correções** (uma por sprint de correção), criada a partir da `main` atualizada:
   ```
   git checkout main
   git pull
   git checkout -b fix/status-listagens-publicas
   ```
   > O `README.md` do projeto usa *branches* com o nome da app (`core`, `plantas`...). Para este trabalho de correção, use *branches* `fix/...`, conforme a norma do NIC. **Confirme o nome com o orientador na Sprint 1.**
3. **Um commit por bug**, no padrão *Conventional Commits* e citando a *issue*:
   ```
   fix: oculta plantas desativadas no acervo publico (#12)
   fix: oculta familias e espacos desativados nos filtros do acervo (#13)
   test: adiciona testes de status para o acervo (#12 #13)
   ```
4. ***Pull request* ao final da sprint**, com "Closes #12, Closes #13" na descrição, e prints de **antes e depois**. **Não junte duas sprints no mesmo PR.**
5. **Antes de abrir o PR:** `python manage.py test` passando, `python manage.py check` sem problemas, sem `print()` esquecido.
6. **Nunca faça commit** do `.env`, do `db.sqlite3` nem da pasta `media/` com seus dados de teste. Confira com `git status` antes de cada commit.

**Configure o seu nome no Git uma vez** (você vai precisar identificar os seus commits no TCC):
```
git config --global user.name "Warley Seu Sobrenome"
git config --global user.email "seu-email-institucional"
```

---

## 5. Onde guardar o seu trabalho e rotina

### 5.1 Pasta no Google Drive

Crie a pasta `Warley - Bugs Praça da Paz`, compartilhada com o orientador:

```
Warley - Bugs Praça da Paz/
├── diario/                       <- um documento por semana (diário de bordo)
├── prints/
│   ├── antes/                    <- bug acontecendo
│   └── depois/                   <- bug corrigido
├── Planilha de bugs              <- Google Planilhas (o coração do trabalho)
├── Roteiro de verificação        <- Google Docs (Sprint 2)
└── Relatório de verificação      <- Google Docs (vai crescendo; versão final na Sprint 8)
```

**Nome dos prints:** `ID_antes_numero.png` e `ID_depois_numero.png`. Exemplo: `B01_antes_01.png`, `B01_depois_01.png`.

### 5.2 Planilha de bugs

Crie na Sprint 1 com estas colunas:

| Coluna | Exemplo |
|---|---|
| ID | B01 |
| Título | Plantas desativadas aparecem no acervo |
| Grupo | A — status nas páginas públicas |
| Como foi encontrado | Navegação (roteiro, passo 3) / Varredura prévia do orientador / Análise do código / Página de Erros |
| Página / URL | `/acervo/` |
| Perfil usado | Visitante (sem login) |
| Passos para reproduzir | 1. No painel, desativar a planta "Arruda". 2. Sair. 3. Abrir `/acervo/` |
| Resultado esperado | "Arruda" não aparece |
| Resultado obtido | "Arruda" aparece na listagem |
| Evidência | `B01_antes_01.png` |
| Gravidade | Alta / Média / Baixa (veja abaixo) |
| Causa (arquivo e função) | `apps/core/views.py`, `acervo_view` |
| Correção aplicada | Adicionado `.filter(status=True)` |
| Issue / Branch / PR | #12 / `fix/status-listagens-publicas` / PR #20 |
| Teste automático | `apps/core/tests.py`, `test_acervo_nao_mostra_planta_inativa` |
| Reteste (data e resultado) | 04/11/2026 — OK |
| Situação | Aberto / Corrigido / Não reproduzido / Decidir com orientador |

**Gravidade (use sempre o mesmo critério):**
- **Alta:** falha de segurança ou de acesso, ou exposição de conteúdo que o administrador quis esconder;
- **Média:** página quebra (erro 500) ou mostra informação inconsistente;
- **Baixa:** detalhe visual, texto, contagem ou organização.

### 5.3 Rotina semanal

| Quando | O quê |
|---|---|
| **Quarta (início da sprint)** | Ler as tarefas da semana, abrir as *issues*, criar a *branch*, tirar dúvidas |
| **Cada dia de trabalho** | Anotar no diário: o que fez, o que encontrou, o que travou, **o que decidiu e por quê** |
| **Terça (fim da sprint)** | Rodar os testes, abrir o PR, conferir "Pronto quando", avisar o orientador |
| **Reunião semanal** | Mostrar a planilha, os prints e o PR |

**Regra dos 45 minutos:** travou? Tente por 45 minutos. Se não resolver, mande a dúvida ao orientador contando: o que queria fazer, o que fez, o que apareceu na tela (print) e o que já tentou.

**O diário é importante:** a Metodologia, os Materiais e Métodos e os Resultados do TCC saem dele.

---

## 6. Sprints

| Sprint | Período | Foco | Bugs |
|---|---|---|---|
| 1 | 23/09 a 29/09 | Ambiente, dados de teste e primeiro bug reproduzido | B01 (só reproduzir) |
| 2 | 30/09 a 06/10 | Roteiro de verificação e varredura por navegação | Todos (reproduzir e registrar) |
| 3 | 07/10 a 13/10 | 1ª correção: listagens públicas + primeiros testes | B01, B02, B03, B04 |
| 4 | 14/10 a 20/10 | 2ª correção: páginas de detalhe | B05, B06, B07, B08 |
| 5 | 21/10 a 27/10 | 3ª correção: formulários do painel e erros 500 | B09, B10, B13 |
| 6 | 28/10 a 03/11 | 4ª correção: segurança | B11, B12, B14 |
| 7 | 04/11 a 10/11 | Reteste completo (regressão) e números finais | Todos |
| 8 | 11/11 a 17/11 | Relatório de verificação, documentação e encerramento | — |

---

### Sprint 1 — Ambiente, dados de teste e primeiro bug (23/09 a 29/09/2026)

**Objetivo:** projeto rodando no seu computador, dados fictícios cadastrados e o bug B01 reproduzido e documentado.

#### Tarefa 1.1 — Rodar o projeto no seu computador

*Ajuda/direcionamento:*

1. Clone o repositório (no Prompt de Comando ou PowerShell, dentro da sua pasta de projetos):
   ```
   git clone https://github.com/nicifrn/pppraca
   cd pppraca
   ```
2. Crie e ative o ambiente virtual:
   ```
   python -m venv venv
   venv\Scripts\activate
   ```
   O nome `(venv)` deve aparecer no início da linha.
3. Instale as dependências: `pip install -r requirements.txt`
4. Copie o arquivo de configuração: `copy .env.example .env`. Deixe `DB_ENGINE=sqlite3` (ou vazio). **Não preencha** as chaves do Google e do SUAP, pois você não vai precisar delas.
5. Crie o banco e o seu administrador:
   ```
   python manage.py migrate
   python manage.py createsuperuser
   ```
6. Rode: `python manage.py runserver` e abra `http://localhost:8000`.
7. Entre no painel em `http://localhost:8000/auth/login/` com o e-mail e a senha que você criou.

Anote no diário cada passo e **cada erro** que aparecer, com a solução. Isso vai para Materiais e Métodos.

#### Tarefa 1.2 — Ler a documentação e a norma do NIC

1. Leia o `README.md` e o `CLAUDE.md` do `pppraca`. Foque em: estrutura das apps, separação público × privado e o campo `status`;
2. Leia `https://github.com/nicifrn/nic_projetos_tarefas`;
3. Escreva no diário, em até 10 linhas, **o fluxo que você entendeu** (issue → branch → commit → PR). Mostre ao orientador na reunião e **confirme o nome das *branches*** (seção 4).
4. Configure o seu nome no Git (seção 4).

#### Tarefa 1.3 — Cadastrar os dados fictícios de teste

Os testes só funcionam se existirem registros **ativos e desativados** de cada tipo. Pelo painel, cadastre:

| O quê | Quantidade | Desativar |
|---|---|---|
| Espaços | 3 (ex.: "Espaço Teste A", "B", "C") | "Espaço Teste C" |
| Famílias | 3 | 1 |
| Tipos | 3 | 1 |
| Culturas | 3 | 1 |
| Plantas | 8, distribuídas nos 3 espaços, usando famílias, tipos e culturas ativos **e** desativados | 2 plantas |
| Parceiros | 2 | 1 |
| Ocupações | 2 | 1 |
| Perfis | use os existentes (crie "teste" se precisar) | 1 |
| Usuários | 1 usuário comum de teste, **com dados fictícios** | ainda não (Sprint 2) |

**Regras:**
- use nomes que deixem claro o que é teste e o que está desativado. Ex.: planta "Arruda (INATIVA)". Assim o print fica autoexplicativo;
- **nunca use dados reais de pessoas** (nome, CPF, e-mail). Use CPFs de teste gerados por ferramentas on-line de "gerador de CPF para testes";
- anote na planilha (aba "Dados de teste") tudo o que cadastrou e o que desativou.

#### Tarefa 1.4 — Reproduzir o primeiro bug (B01)

1. No painel, confira que a planta "Arruda (INATIVA)" está desativada;
2. **Saia do sistema** (ou abra uma janela anônima: `Ctrl + Shift + N`). Você deve testar como **visitante**;
3. Abra `http://localhost:8000/acervo/`;
4. Se a planta aparecer, **o bug está confirmado**. Tire o print `B01_antes_01.png`;
5. Preencha a primeira linha da planilha de bugs com todas as colunas que já conseguir.

#### Tarefa 1.5 — Criar a estrutura no Google Drive

Crie a pasta da seção 5.1, a planilha de bugs (seção 5.2) e o primeiro diário. Compartilhe com o orientador.

**Pronto quando:**
- [ ] O projeto roda no seu computador e você entra no painel
- [ ] Fluxo do NIC lido e nome das *branches* confirmado com o orientador
- [ ] Dados fictícios cadastrados (ativos e desativados) e anotados
- [ ] B01 reproduzido, com print e linha na planilha
- [ ] Pasta no Drive compartilhada

---

### Sprint 2 — Roteiro de verificação e varredura por navegação (30/09 a 06/10/2026)

**Objetivo:** ter um **roteiro de verificação** escrito e usá-lo para reproduzir e registrar todos os bugs da seção 2, e procurar outros.

> Esta sprint é a base do seu TCC: é aqui que você responde **"como os bugs foram identificados?"**. Trabalhe com calma e documente tudo.

#### Tarefa 2.1 — Mapear as páginas do sistema

Abra `apps/core/urls.py` (páginas públicas) e os `urls.py` de cada app (painel). Monte, no documento "Roteiro de verificação", uma tabela com **todas as páginas**:

| Página | URL | Pública ou painel? | Mostra dados de quais cadastros? |
|---|---|---|---|
| Início | `/` | Pública | Espaços, parceiros, dados do site |
| Acervo | `/acervo/` | Pública | Plantas, famílias, espaços |
| ... | ... | ... | ... |

*Ajuda:* para descobrir que dados cada página mostra, abra a *view* correspondente em `apps/core/views.py` e veja o que ela manda para o template (o dicionário no final do `render`).

#### Tarefa 2.2 — Escrever o roteiro de verificação

Para cada cadastro que tem status (Planta, Espaço, Família, Tipo, Cultura, Parceiro, Ocupação, Perfil, Usuário, Acontecimento, Tipo de acontecimento), escreva um **caso de teste**:

```
CT-03 — Espaço desativado
Pré-condição: "Espaço Teste C" desativado no painel; usuário deslogado.
Passos:
  1. Abrir a página inicial (/) e procurar "Espaço Teste C".
  2. Abrir /espacos/ e procurar "Espaço Teste C".
  3. Abrir /acervo/ e abrir a caixa de filtro "Espaço".
  4. Digitar na barra de endereço /espacos/<número do Espaço C>/.
  5. Abrir uma planta ativa do Espaço C e clicar no link do espaço.
Resultado esperado: o Espaço C não aparece em nenhum lugar; a URL direta mostra a página 404.
```

*Ajuda:* o número (pk) do espaço aparece na URL quando você clica em "Editar" no painel (`/espacos/admin/editar/3/` → o número é 3).

Inclua também casos de teste para:
- **CT-login-desativado:** desativar o usuário de teste no painel, sair e tentar entrar com ele (B11);
- **CT-next:** sair e abrir `http://localhost:8000/auth/login/?next=https://www.google.com`, fazer login e ver para onde vai (B12). **Teste só com o seu próprio sistema local.** Nunca faça esse tipo de teste em sites de terceiros;
- **CT-parametros:** mudar à mão os valores na barra de endereço dos filtros, por exemplo `/acervo/?familia=abc`, `/acervo/?page=9999`, `/acontecimentos/?de=ontem` (B13);
- **CT-formularios:** no painel, abrir "Cadastrar planta" e "Cadastrar usuário" e ver se as listas mostram itens desativados (B09, B10).

#### Tarefa 2.3 — Executar o roteiro

Execute todos os casos de teste. Para **cada** resultado diferente do esperado:
1. tire o print (`Bxx_antes_01.png`);
2. registre na planilha;
3. para erros 500: abra o painel > **Erros** e tire um print do registro do erro. Abra o registro e veja o *traceback*. A última linha diz qual foi o erro, e as linhas com `apps/...` dizem **em que arquivo e função** ele aconteceu.

*Dica para o F12:* com a aba **Rede (Network)** aberta, recarregue a página. A primeira linha mostra o código de status: **200** (ok), **302** (redirecionou), **404** (não encontrado), **500** (erro do servidor). Tire print disso também, porque é uma ótima evidência.

**Se achar um bug que não está na seção 2**, dê a ele o próximo ID livre (B17, B18...) e marque "Como foi encontrado: navegação (CT-xx)".

#### Tarefa 2.4 — Localizar a causa no código

Para cada bug confirmado, abra o arquivo indicado na seção 2 e **encontre a linha** responsável. Preencha a coluna "Causa". Você ainda **não vai alterar nada**, só entender.

*Dica:* no editor, use `Ctrl + Shift + F` (buscar em todos os arquivos) com o nome da view ou do template.

#### Tarefa 2.5 — Criar as issues

Crie no GitHub **uma *issue* por bug confirmado** (título com o ID; corpo com passos, esperado, obtido e print). Anote o número da *issue* na planilha. Para B15, B16, D1 e D2, **leve à reunião para decidir** antes de abrir *issue*.

**Pronto quando:**
- [ ] Roteiro de verificação escrito (mapa das páginas + casos de teste)
- [ ] Todos os casos executados; planilha preenchida até a coluna "Causa"
- [ ] Prints "antes" de todos os bugs confirmados
- [ ] *Issues* criadas
- [ ] Decisões de B15, B16, D1 e D2 registradas no diário

---

### Sprint 3 — 1ª correção: listagens públicas + primeiros testes (07/10 a 13/10/2026)

**Bugs:** B01, B02, B03, B04 — *Branch sugerida:* `fix/status-listagens-publicas`

**Objetivo:** esconder dos visitantes os registros desativados nas listagens, e criar os primeiros testes automáticos.

#### Tarefa 3.1 — Entender o que é um *QuerySet* e o `filter()`

Leia na documentação do Django a página "Making queries" (seções *Retrieving objects* e *Retrieving specific objects with filters*). Em resumo:

```python
Planta.objects.all()                 # todas as plantas, ativas e desativadas
Planta.objects.filter(status=True)   # só as ativas
```

Experimente no *shell* do Django (`python manage.py shell`):
```python
from apps.plantas.models import Planta
Planta.objects.count()
Planta.objects.filter(status=True).count()
```
A diferença entre os dois números são as plantas que você desativou.

#### Tarefa 3.2 — Corrigir B01 e B02 (acervo)

Em `apps/core/views.py`, na função `acervo_view`:

1. Na linha que monta `plantas_qs`, troque `.all()` por `.filter(status=True)`;
2. Nas linhas de `familias` e `espacos` (usadas nos filtros), faça o mesmo;
3. Salve, recarregue `/acervo/` e confira: a planta "Arruda (INATIVA)" sumiu? As famílias e espaços desativados sumiram das caixas de filtro?
4. Tire os prints `B01_depois_01.png` e `B02_depois_01.png`;
5. Faça **um commit para cada bug**.

#### Tarefa 3.3 — Corrigir B03 e B04 (espaços e página inicial)

Mesmo raciocínio:
- `espacos_view`: espaços ativos;
- `index`: espaços ativos **e** parceiros ativos.

Confira no navegador, tire os prints "depois" e faça os commits.

#### Tarefa 3.4 — Escrever os primeiros testes automáticos

Um teste automático é um pequeno programa que **simula o navegador** e verifica se a página mostra o que deveria. Ele é importante porque, se no futuro alguém desfizer a sua correção sem querer, o teste avisa.

Abra `apps/core/tests.py` (hoje está quase vazio) e escreva:

```python
from django.test import TestCase
from django.urls import reverse

from apps.espacos.models import Espaco
from apps.plantas.models import Planta


class AcervoStatusTest(TestCase):
    def setUp(self):
        # setUp roda antes de cada teste, em um banco de dados vazio e temporário
        self.espaco = Espaco.objects.create(nome='Espaço Teste')
        Planta.objects.create(nome_popular='Babosa', nome_cientifico='Aloe vera',
                              espaco=self.espaco)
        Planta.objects.create(nome_popular='Arruda', nome_cientifico='Ruta graveolens',
                              espaco=self.espaco, status=False)

    def test_acervo_mostra_planta_ativa(self):
        resposta = self.client.get(reverse('acervo'))
        self.assertContains(resposta, 'Babosa')

    def test_acervo_nao_mostra_planta_inativa(self):
        resposta = self.client.get(reverse('acervo'))
        self.assertNotContains(resposta, 'Arruda')
```

Rode com: `python manage.py test apps.core`

**Experimento importante para o TCC:** desfaça temporariamente a correção do B01 (volte o `.all()`), rode o teste e **tire print do teste falhando**. Depois refaça a correção e tire print do teste passando. Isso mostra que o teste realmente detecta o bug.

> O orientador já rodou esse teste na versão atual do sistema (sem correção): `test_acervo_nao_mostra_planta_inativa` **falha**, confirmando o B01.

Escreva testes parecidos para B02, B03 e B04 (um espaço desativado não pode aparecer em `/espacos/` nem em `/`; um parceiro desativado não pode aparecer em `/`).

*Dica:* use nomes bem diferentes nos dados de teste (ex.: "Espaço Oculto") para o `assertNotContains` não confundir com outro texto da página.

#### Tarefa 3.5 — Abrir o PR

Siga o item 5 da seção 4. No PR, coloque uma tabela com os prints antes/depois. Atualize a planilha (colunas "Correção", "Issue/Branch/PR" e "Teste").

**Pronto quando:**
- [ ] B01 a B04 corrigidos, um commit por bug
- [ ] Pelo menos 5 testes em `apps/core/tests.py`, todos passando
- [ ] Print do teste falhando (sem correção) e passando (com correção)
- [ ] PR aberto; planilha atualizada

---

### Sprint 4 — 2ª correção: páginas de detalhe (14/10 a 20/10/2026)

**Bugs:** B05, B06, B07, B08 — *Branch sugerida:* `fix/status-paginas-detalhe`

**Objetivo:** um registro desativado não pode abrir pela URL direta, e a página de uma planta não pode mostrar informações desativadas.

#### Tarefa 4.1 — Corrigir B05 e B07 (URL direta deve dar 404)

O `get_object_or_404` aceita mais de um critério. Veja como está em `acontecimento_detalhe_view` (`is_ativo=True`) e faça o mesmo:

- `espaco_detalhe_view`: acrescente `status=True`;
- `planta_detalhe_view`: acrescente `status=True`.

Teste no navegador: a URL da planta e do espaço desativados deve mostrar a **página 404** do site.

**Por que 404 e não uma mensagem "planta desativada"?** Porque, para o visitante, um registro desativado **não existe**. Mostrar que ele existe já seria vazar informação.

#### Tarefa 4.2 — Corrigir B06 (plantas do espaço)

Em `espaco_detalhe_view`, a linha `Planta.objects.filter(espaco=espaco)` deve filtrar também `status=True`. Dica: o `filter` aceita vários critérios separados por vírgula.

#### Tarefa 4.3 — Corrigir B08 (informações desativadas no detalhe da planta)

Este é um pouco diferente, porque o problema está no **template** `apps/core/templates/planta_detalhe.html`:

1. **Tipos e culturas:** o template usa `{% with tipos=planta.tipos.all %}`. Templates do Django não aceitam `filter(status=True)`. A solução é **mandar a lista já filtrada pela view**:
   ```python
   def planta_detalhe_view(request, slug):
       planta = get_object_or_404(Planta, slug=slug, status=True)
       return render(request, 'planta_detalhe.html', {
           'planta': planta,
           'tipos': planta.tipos.filter(status=True),
           'culturas': planta.culturas.filter(status=True),
       })
   ```
   No template, **remova** os `{% with ... %}` e `{% endwith %}` de tipos e culturas e use direto `{% if tipos %}` e `{% for tipo in tipos %}`.
2. **Família:** troque `{% if planta.familia %}` por `{% if planta.familia and planta.familia.status %}`.
3. **Espaço:** o link para o espaço aparece em **dois lugares** (no topo, "← Nome do espaço", e no bloco "Espaço"). Nos dois, só mostre o link se `planta.espaco.status` for verdadeiro. No topo, se o espaço estiver desativado, use o link "← Espaços", que já existe no `{% else %}`.

Depois do B05, um link para espaço desativado leva à página 404. Este é um bom exemplo, para o TCC, de **uma correção que revela outro problema**. Registre isso no diário.

Confirme com o orientador a decisão D1 (planta ativa em espaço desativado) antes de fechar esta tarefa.

#### Tarefa 4.4 — Testes

Em `apps/core/tests.py`, crie testes para:
- planta desativada → `self.assertEqual(resposta.status_code, 404)`;
- espaço desativado → 404;
- espaço ativo **não** lista planta desativada;
- detalhe da planta **não** mostra um tipo, uma cultura e uma família desativados (crie-os no `setUp` com nomes únicos e associe à planta: `planta.tipos.add(tipo)`).

Rode **todos** os testes (`python manage.py test`). Os da Sprint 3 também têm que continuar passando.

**Pronto quando:**
- [ ] B05 a B08 corrigidos e com prints "depois"
- [ ] Novos testes escritos; todos os testes do projeto passando
- [ ] PR aberto; planilha atualizada

---

### Sprint 5 — 3ª correção: formulários do painel e erros 500 (21/10 a 27/10/2026)

**Bugs:** B09, B10, B13 — *Branch sugerida:* `fix/formularios-e-filtros`

#### Tarefa 5.1 — Corrigir B09 (formulário de planta)

Em `apps/plantas/forms.py`, no `__init__` do formulário de planta, as linhas de `tipos` e `culturas` **já estão certas** (`filter(status=True)`). Faça o mesmo nas linhas de `familia` e `espaco`.

**Cuidado com um caso especial:** e se uma planta **já cadastrada** estiver ligada a uma família que depois foi desativada? Ao abrir "Editar" dessa planta, a família não estará na lista e o Django vai reclamar ao salvar. Teste esse cenário! Se acontecer, a solução é incluir a família atual da planta na lista:

```python
from django.db.models import Q

familia_atual = self.instance.familia_id if self.instance.pk else None
self.fields['familia'].queryset = FamiliaPlanta.objects.filter(
    Q(status=True) | Q(pk=familia_atual)
).order_by('nome')
```

Faça o mesmo para `espaco`. Registre no diário se esse caso aconteceu e como resolveu: é outro ótimo exemplo para o TCC.

#### Tarefa 5.2 — Corrigir B10 (formulários de usuário)

Em `apps/usuarios/forms.py`, procure (`Ctrl + F`) por `Ocupacao.objects.all()` (aparece **três vezes**, uma em cada formulário) e por `Perfil.objects.all()`. Aplique o mesmo raciocínio da Tarefa 5.1, inclusive o cuidado com o registro já salvo.

#### Tarefa 5.3 — Corrigir B13 (erro 500 com parâmetros inválidos)

O problema: `/acervo/?familia=abc` manda o texto `"abc"` para `filter(familia_id="abc")`, e o banco espera um número.

**Para os filtros numéricos** (`familia`, `espaco`, `tipo`), só filtre se o valor for número:

```python
if familia_id.isdigit():
    plantas_qs = plantas_qs.filter(familia_id=familia_id)
```

**Para as datas** (`de` e `ate` em `acontecimentos_view`), use a função do Django que converte texto em data:

```python
from django.utils.dateparse import parse_date

def _data_valida(texto):
    try:
        return parse_date(texto)   # devolve None se o formato estiver errado
    except ValueError:             # formato certo, mas data impossível (ex.: 2026-13-45)
        return None
```

E no lugar de `if de:` use `data_de = _data_valida(de)` e `if data_de:`.

Teste no navegador todas as URLs do caso CT-parametros. Nenhuma pode dar erro 500. Confira também se a página **Erros** do painel parou de receber novos registros para essas URLs.

#### Tarefa 5.4 — Testes

- Para B13: `self.client.get(reverse('acervo') + '?familia=abc')` deve ter `status_code == 200`. Faça o mesmo para cada parâmetro.
- Para B09 e B10: teste o **formulário** diretamente:
  ```python
  from apps.plantas.forms import PlantaForm

  form = PlantaForm()
  self.assertNotIn(self.familia_inativa, form.fields['familia'].queryset)
  ```

> Observação: sem a correção, o teste do B13 aparece como **ERROR** (e não FAIL), porque o erro 500 "estoura" dentro do teste. Isso é normal. Anote a diferença entre FAIL e ERROR no diário.

**Pronto quando:**
- [ ] B09, B10 e B13 corrigidos, incluindo o caso "registro já salvo com item desativado"
- [ ] Testes escritos; todos passando
- [ ] PR aberto; planilha atualizada

---

### Sprint 6 — 4ª correção: segurança (28/10 a 03/11/2026)

**Bugs:** B11, B12, B14 — *Branch sugerida:* `fix/seguranca-login`

> Esta sprint mexe em **login**. Faça tudo com calma, teste muito e peça revisão do orientador **antes** de abrir o PR.

#### Tarefa 6.1 — Entender o B11

O model `Usuario` tem **dois** campos parecidos:
- `is_active`: campo do próprio Django. **O Django bloqueia o login quando ele é `False`**;
- `status`: campo criado no projeto. É **ele** que o botão "desativar" do painel altera.

Como o botão não mexe no `is_active`, o Django nunca fica sabendo que o usuário foi desativado.

#### Tarefa 6.2 — Corrigir B11

1. Em `apps/usuarios/views.py`, na função `admin_usuarios_toggle`, faça o `is_active` acompanhar o `status`:
   ```python
   usuario.status = not usuario.status
   usuario.is_active = usuario.status
   usuario.save(update_fields=['status', 'is_active'])
   ```
   Com isso, **todas** as formas de login (e-mail/CPF, Google, SUAP) passam a bloquear o usuário, e quem já estava logado é desconectado na próxima página que abrir.
2. **Proteja o seu próprio acesso:** o que acontece se o administrador desativar a si mesmo? Teste isso **com um segundo superusuário de teste**, nunca com o seu. Se o sistema deixar, acrescente uma verificação que impeça (`if usuario == request.user:` → mensagem de erro e `redirect`).
3. **Dados antigos:** usuários desativados **antes** da correção continuam com `is_active=True`. Combine com o orientador e rode uma vez no *shell*:
   ```python
   from apps.usuarios.models import Usuario
   Usuario.objects.filter(status=False).update(is_active=False)
   ```
   **No servidor de produção, isso só pode ser feito pelo orientador.** Documente o comando no PR.

#### Tarefa 6.3 — Corrigir B12 (redirecionamento aberto)

O Django tem uma função pronta para verificar se o endereço do `next` é do próprio site:

```python
from django.utils.http import url_has_allowed_host_and_scheme

next_url = request.GET.get('next', '')
if not url_has_allowed_host_and_scheme(next_url, allowed_hosts={request.get_host()},
                                       require_https=request.is_secure()):
    next_url = 'perfil'
return redirect(next_url)
```

Aplique em `login_view` **e** em `suap_callback`. Teste:
- `/auth/login/?next=https://www.google.com` → depois do login, deve ir para o painel;
- `/auth/login/?next=/acervo/` → depois do login, deve ir para o acervo (o `next` legítimo continua funcionando).

#### Tarefa 6.4 — Corrigir B14 (preventivo)

Nos três arquivos `decorators.py` que verificam perfil (`apps/espacos`, `apps/plantas` e `apps/usuarios`; este último tem **duas** ocorrências), acrescente `status=True` nos `perfis.filter(...)`. Exemplo: `perfis.filter(nome='coordenador', status=True)`. Use `Ctrl + Shift + F` com `perfis.filter` para não esquecer nenhum.

#### Tarefa 6.5 — Testes

```python
from apps.usuarios.models import Usuario


class LoginSegurancaTest(TestCase):
    def setUp(self):
        self.usuario = Usuario.objects.create_user(
            username='teste', email='teste@exemplo.com', cpf='12345678901',
            celular='84999999999', password='SenhaForte123')

    def test_usuario_desativado_nao_acessa_painel(self):
        # desativa pelo botão do painel (use um superuser de teste para chamar a URL do toggle)
        ...
        self.client.post(reverse('login'), {'identificador': 'teste@exemplo.com',
                                            'senha': 'SenhaForte123'})
        resposta = self.client.get(reverse('perfil'))
        self.assertEqual(resposta.status_code, 302)   # 302 = mandou de volta para o login
```

> O orientador já rodou uma versão deste teste na versão atual (desativando só o `status`): o usuário desativado **entra** e a página do painel responde 200, confirmando o B11.

Complete o `...` criando um superusuário de teste, fazendo login com ele (`self.client.force_login(admin)`), chamando `self.client.post(reverse('admin_usuarios_toggle', args=[self.usuario.pk]))` e depois `self.client.logout()`.

Para o B12, teste que `self.client.post(reverse('login') + '?next=https://www.google.com', {...})` **não** redireciona para o Google: `self.assertNotIn('google', resposta.url)`.

**Pronto quando:**
- [ ] B11, B12 e B14 corrigidos; revisão do orientador feita antes do PR
- [ ] Testes de segurança escritos; todos passando
- [ ] PR aberto; planilha atualizada

---

### Sprint 7 — Reteste completo e números finais (04/11 a 10/11/2026)

**Objetivo:** provar que tudo foi corrigido e que nada quebrou. **Não corrija bugs novos nesta sprint**, apenas registre-os (a não ser que o orientador autorize).

#### Tarefa 7.1 — Atualizar o ambiente

Depois que os PRs forem aceitos, atualize a sua `main` (`git checkout main` e `git pull`) e rode `python manage.py test`. Todos os testes devem passar. Tire print do resultado (quantidade de testes e "OK").

#### Tarefa 7.2 — Executar de novo o roteiro de verificação

Execute **todo** o roteiro da Sprint 2, com os mesmos dados fictícios e o mesmo navegador. Para cada caso, registre na planilha a coluna "Reteste". Tire os prints "depois" que ainda faltarem.

Isso se chama **teste de regressão**: verificar que as correções funcionaram e que não criaram problemas em outros lugares. Navegue também pelas páginas que você **não** alterou, para confirmar que continuam funcionando.

#### Tarefa 7.3 — Consolidar os números

Em uma aba "Resumo" da planilha, monte:
- total de bugs: encontrados, corrigidos, não reproduzidos, pendentes de decisão;
- bugs por **grupo** (A, B, C, D, E) e por **gravidade**;
- bugs por **forma de identificação** (varredura prévia, navegação, página de Erros, análise do código);
- total de testes automáticos criados e quantos arquivos foram alterados (use `git log --author="Warley" --stat` para contar);
- dois gráficos no Google Planilhas: "Bugs por grupo" e "Bugs por gravidade".

#### Tarefa 7.4 — Escolher 3 exemplos para o TCC

Escolha **3 bugs** para descrever em detalhe nos Resultados. Sugestão: um do Grupo A (B01, o mais simples), um "encadeado" (B05 → B08, uma correção que revelou outra) e um de segurança (B11). Para cada um, junte: print antes, trecho de código antes, trecho de código depois, print depois e o teste.

**Pronto quando:**
- [ ] Todos os testes passando na `main` atualizada
- [ ] Roteiro reexecutado; coluna "Reteste" preenchida
- [ ] Aba "Resumo" com números e gráficos
- [ ] 3 exemplos escolhidos e com material reunido

---

### Sprint 8 — Relatório de verificação e encerramento (11/11 a 17/11/2026)

#### Tarefa 8.1 — Relatório de verificação (documento para o TCC)

No Google Docs "Relatório de verificação", organize:

1. **Escopo:** versão do sistema (commit inicial `7b489f0` e commit final), navegador, período;
2. **Método:** o roteiro de verificação (resumo dos casos de teste) e o fluxo issue → branch → correção → teste → PR → reteste;
3. **Tabela geral de bugs:** ID, título, grupo, gravidade, como foi identificado, causa, correção, teste, situação;
4. **Os 3 exemplos detalhados** (Tarefa 7.4);
5. **Números e gráficos** (Tarefa 7.3);
6. **Pendências:** bugs não corrigidos e decisões em aberto, com recomendação.

Esse relatório é a base direta da seção de Resultados do TCC e vai como **apêndice**.

#### Tarefa 8.2 — Documentação no repositório

Com autorização do orientador, em uma *branch* `docs/regra-status`, acrescente ao `CLAUDE.md` e/ou ao `README.md` do `pppraca` uma regra curta como: *"Toda consulta em página pública deve filtrar `status=True` (ou `is_ativo=True`). Todo `get_object_or_404` público deve incluir o filtro de status."* Isso evita que o mesmo tipo de bug volte em funcionalidades futuras.

#### Tarefa 8.3 — Lições aprendidas

No diário, responda: quais bugs foram mais difíceis de achar? Algum bug só apareceu navegando (e não lendo o código)? Algum só apareceu lendo o código? O que você faria diferente? Essas respostas vão para a Discussão e a Conclusão do TCC.

**Pronto quando:**
- [ ] Relatório de verificação completo e revisado pelo orientador
- [ ] PR de documentação aberto (se autorizado)
- [ ] Lições aprendidas registradas

---

## 7. Riscos e planos B

| Risco | Sinal | O que fazer |
|---|---|---|
| `pip install` falha no `mysqlclient` | Erro de compilação ao instalar | Instale o resto sem ele: abra o `requirements.txt`, e rode `pip install` de cada pacote, pulando o `mysqlclient`. Você usa SQLite e não precisa dele. **Não altere o `requirements.txt` no repositório** |
| `migrate` falha | Erro de migração | Apague o seu `db.sqlite3` **local** e rode de novo. Se persistir, mande o erro ao orientador |
| Conflito de *merge* com outras pessoas | Git avisa "CONFLICT" | Não resolva sozinho na primeira vez. Chame o orientador. `apps/core/views.py` e `apps/usuarios/views.py` são os arquivos mais prováveis de conflito |
| Atraso | Terminou a sprint com tarefas abertas | Prioridade: B11 e B12 (segurança) > Grupo A > B13 > Grupo B > B14. Se precisar cortar, corte B14 e o Grupo E |
| A correção quebrou outra coisa | Teste antigo falhando | Ótimo, o teste funcionou! Registre no diário, corrija e conte isso no TCC |
| Achou muitos bugs novos | Planilha crescendo | Registre todos, mas só corrija os novos com autorização. Os que não couberem vão para "Trabalhos futuros" |

---

## 8. Trabalhos futuros

Coisas que **não** entram neste ciclo, mas devem aparecer no TCC como continuidade:
- um *Manager* personalizado (ex.: `Planta.ativos.all()`) para centralizar o filtro de status e evitar repetição;
- testes automáticos para **todas** as páginas (hoje só as corrigidas têm teste);
- executar os testes automaticamente a cada PR (GitHub Actions, gratuito para repositórios públicos);
- unificar os campos `status` e `is_active` do usuário;
- resolver as rotas duplicadas (B16).

---

## 9. Checklist de encerramento do Ciclo 1

- [ ] Planilha de bugs completa (todas as colunas e reteste)
- [ ] Prints antes/depois de todos os bugs corrigidos
- [ ] Todos os PRs abertos e revisados; *issues* fechadas
- [ ] `python manage.py test` passando na `main`
- [ ] Relatório de verificação no Drive
- [ ] Diário de bordo das 8 semanas
- [ ] Material dos 3 exemplos reunido para o TCC
- [ ] Seções do TCC entregues nos prazos de `01_warley_praca_tarefas_escrita.md`
