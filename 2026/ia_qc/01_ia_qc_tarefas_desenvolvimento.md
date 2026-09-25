# Plano de tarefas de desenvolvimento — Bancada de Estratégias de Casamento Sintático

**Projeto pai:** "Podem os computadores pensar?" — o Quarto Chinês de John Searle (ver [projeto.md](../projeto.md)).

**Temática:** Sugestão B das [sugestões de implementação (v2)](../sugestoes_implementacao_v2.md) — **Bancada de estratégias de casamento sintático**, simplificada para este ciclo.

**Duração:** 8 sprints de 1 semana (**23/09/2026 a 17/11/2026**).

**Escrita do TCC:** acontece **em paralelo**, com prazos próprios. Veja [01_ia_qc_tarefas_escrita.md](01_ia_qc_tarefas_escrita.md). Cada sprint deste documento indica qual seção do TCC ela alimenta.

---

## Sumário

- [A ideia do trabalho, em uma página](#a-ideia-do-trabalho-em-uma-página)
- [Decisões técnicas já fechadas](#decisões-técnicas-já-fechadas)
- [Combinados gerais](#combinados-gerais)
- [Visão geral das sprints](#visão-geral-das-sprints)
- [Sprint 1 — Repositório, ambiente e projeto Django](#sprint-1--2309-a-2909-repositório-ambiente-e-projeto-django)
- [Sprint 2 — O livro de regras](#sprint-2--3009-a-0610-o-livro-de-regras)
- [Sprint 3 — A bateria de 100 mensagens e o gabarito](#sprint-3--0710-a-1310-a-bateria-de-100-mensagens-e-o-gabarito)
- [Sprint 4 — Estratégias 1 e 2: igualdade exata e normalização](#sprint-4--1410-a-2010-estratégias-1-e-2-igualdade-exata-e-normalização)
- [Sprint 5 — Estratégias 3 e 4: contém e palavras-chave](#sprint-5--2110-a-2710-estratégias-3-e-4-contém-e-palavras-chave)
- [Sprint 6 — Estratégia 5 e o comando `testar_estrategias`](#sprint-6--2810-a-0311-estratégia-5-e-o-comando-testar_estrategias)
- [Sprint 7 — Gráficos, tabelas e análise dos erros](#sprint-7--0411-a-1011-gráficos-tabelas-e-análise-dos-erros)
- [Sprint 8 — Reprodutibilidade, documentação e apresentação](#sprint-8--1111-a-1711-reprodutibilidade-documentação-e-apresentação)
- [Riscos e o que fazer](#riscos-e-o-que-fazer)
- [Checklist final de entregas](#checklist-final-de-entregas)

---

## A ideia do trabalho, em uma página

Um *chatbot* simples funciona assim: ele tem um **livro de regras** (pergunta → resposta) e, quando chega uma mensagem, precisa decidir **qual regra usar**. Por exemplo:

> **Regra R01 — Pergunta:** "Qual é o horário de funcionamento?"
> **Resposta:** "O campus funciona das 7h às 22h."

A questão é: como o programa decide que a mensagem "qual o horário do campus?" corresponde à regra R01? Existem várias formas de fazer isso **sem entender nada** do que foi escrito — só comparando letras e palavras. Você vai programar **cinco** dessas formas (estratégias) e compará-las:

| # | Estratégia | Como decide | Exemplo |
|---|---|---|---|
| 1 | **Igualdade exata** | A mensagem tem de ser idêntica à pergunta da regra | "Qual é o horário de funcionamento?" ✔ / "qual é o horário de funcionamento?" ✘ |
| 2 | **Normalização** | Tira maiúsculas, acentos, pontuação e espaços extras, e depois compara | "QUAL E O HORARIO DE FUNCIONAMENTO" ✔ |
| 3 | **Contém** | A regra dispara se um trecho curto (ex.: "horário") aparecer na mensagem | "Vocês podem informar o horário?" ✔ |
| 4 | **Palavras-chave** | A regra dispara se uma parte mínima das palavras-chave aparecer, em qualquer ordem | "Queria saber o funcionamento e o horário do campus" ✔ |
| 5 | **Similaridade** | Calcula o quanto os textos se parecem (de 0 a 1) com o `SequenceMatcher` do Python | "Quais são os horários de funcionamento?" → 0,87 ✔ |

Depois, você passa **as mesmas 100 mensagens** por cada estratégia (100 × 5 = 500 execuções) e conta:

- **respostas adequadas** — escolheu a regra certa;
- **respostas inadequadas** — respondeu, mas com a regra errada (a pior situação: o sistema erra **com confiança**);
- **ausência de resposta** — nenhuma regra foi escolhida;
- **tempo de processamento**.

### A pergunta do trabalho

> **Quanto uma estratégia mais sofisticada de manipulação de texto melhora a *aparência* de compreensão de um sistema que continua funcionando só por regras sintáticas?**

A ligação com o **Quarto Chinês**, de John Searle: a pessoa trancada na sala não sabe chinês, mas devolve respostas corretas porque segue um livro de regras. Quem está do lado de fora acha que ela entende chinês. O seu programa é essa sala. A estratégia 5 provavelmente vai acertar mais do que a 1 — e **nenhuma das duas entende uma palavra**. É isso que o seu TCC vai mostrar com números.

### O que este trabalho **não** é

- **Não** é um *chatbot* com inteligência artificial. Não use ChatGPT, Gemini, APIs de IA, aprendizado de máquina nem bibliotecas de processamento de linguagem natural (NLTK, spaCy etc.). Só Python puro e Django.
- **Não** tem teste com pessoas. Nenhum colega vai responder formulário (isso exigiria o Comitê de Ética). Quem gera os dados é o próprio programa.
- **Não** é para descobrir "a melhor estratégia". É para medir **o que muda** de uma para outra e discutir **o que isso significa**.

---

## Decisões técnicas já fechadas

| Item | Decisão |
|---|---|
| Linguagem | **Python 3** (a versão instalada no laboratório) |
| Framework | **Django** — usado para o banco de dados, o painel de administração (Django Admin) e o comando de gerenciamento |
| Banco de dados | **SQLite** (já vem com o Python e o Django; não precisa instalar nada) |
| Comparação de textos | Somente a **biblioteca padrão** do Python: `unicodedata`, `string`, `difflib` |
| Medição de tempo | `time.perf_counter()` |
| Bateria de mensagens | Um arquivo **CSV** (`dados/bateria.csv`), guardado no Git |
| Gráficos | `matplotlib` |
| Editor | **VS Code** |
| Versionamento | **Git + GitHub** (gratuito) |
| O que **não** entra | Docker, APIs de IA, aprendizado de máquina, bibliotecas de linguagem natural, *front-end* elaborado |

**Tudo é instalado com `pip`**, porque os computadores do laboratório não permitem instalar programas. As únicas bibliotecas externas são `django` e `matplotlib`.

> **Pressupostos a confirmar com o orientador na primeira reunião:** o **Python**, o **Git** e o **VS Code** já estão instalados nas máquinas do laboratório. Se o Git não estiver, veja a seção [Riscos e o que fazer](#riscos-e-o-que-fazer).

### Por que o Django, se o experimento poderia ser só um *script*?

Porque o livro de regras fica em um **banco de dados** administrado pelo **Django Admin** (você cadastra as regras por uma tela pronta, sem programar formulários), e o experimento vira um **comando** do projeto (`python manage.py testar_estrategias`). Isso deixa a bancada pronta para, no futuro, ser ligada à aplicação da Sala Chinesa do projeto — e rende bom conteúdo técnico para o TCC.

---

## Combinados gerais

- **Reunião semanal:** no início de cada sprint você mostra ao orientador o que fez, **rodando no computador**. Não vale só contar.
- **Commits:** pelo menos **3 por sprint**, com mensagem em português dizendo o que foi feito (ex.: `Cria o modelo Regra`, e não `ajustes`).
- **`git push` no fim de todo dia de trabalho.** Se o computador do laboratório for formatado, o seu trabalho está no GitHub.
- **Travou mais de 40 minutos no mesmo erro? Peça ajuda.** Leve o **texto do erro** copiado (não uma foto da tela) e diga o que já tentou.
- **Diário de bordo:** `docs/diario.md`. No fim de cada sprint, escreva três linhas: **o que funcionou, o que deu errado, o que aprendi**. Esse diário vira a Metodologia e a Conclusão do TCC.
- **Evidências:** todo *print* importante vai para `docs/evidencias/`, com nome que diga o que é (ex.: `s2_admin_regras.png`). Eles vão para o capítulo de Resultados.
- **Nunca use IA generativa para escrever o código ou o texto por você.** Pode usar para **tirar dúvida** sobre um erro, desde que você entenda a resposta — e isso deve ser declarado no TCC (ver seção "Uso de inteligência artificial generativa" do `README.md`). Lembre-se da ironia: é um trabalho sobre programas que parecem entender sem entender.

### A regra de ouro do experimento

> **A bateria de 100 mensagens, o gabarito e o livro de regras são definidos ANTES de programar as estratégias — e depois disso não mudam mais.**

Se você mudar uma mensagem depois de ver o resultado, para uma estratégia "se sair melhor", o experimento perde o valor. Isso será conferido: você vai criar uma **marcação (tag) no Git** no dia em que a bateria for congelada (Sprint 3), e qualquer pessoa poderá verificar que ela não mudou.

---

## Visão geral das sprints

| Sprint | Período | Entrega principal | Alimenta a seção do TCC |
|---|---|---|---|
| 1 | 23/09 a 29/09 | Repositório no GitHub + projeto Django rodando | Introdução e Objetivo Geral |
| 2 | 30/09 a 06/10 | Livro de regras (12 regras) cadastrado no Admin | Referencial Teórico |
| 3 | 07/10 a 13/10 | Bateria de 100 mensagens + gabarito **congelados** | Referencial Teórico e Metodologia |
| 4 | 14/10 a 20/10 | Estratégias 1 e 2 + testes | Metodologia |
| 5 | 21/10 a 27/10 | Estratégias 3 e 4 + testes | Materiais e Métodos |
| 6 | 28/10 a 03/11 | Estratégia 5 + comando `testar_estrategias` + primeira execução | Materiais e Métodos e Resultados |
| 7 | 04/11 a 10/11 | Tabela, gráficos e análise dos erros | Resultados |
| 8 | 11/11 a 17/11 | Reprodutibilidade, README e apresentação | Conclusão |

---

# Sprint 1 — 23/09 a 29/09: repositório, ambiente e projeto Django

**Objetivo da semana:** ter um repositório no GitHub com um projeto Django que abre no navegador, e entender, em linhas gerais, o que é o Quarto Chinês.

### Tarefa 1.1 — Criar a conta e o repositório no GitHub

1. Acesse `https://github.com` e crie uma conta gratuita (se ainda não tiver). Use um nome de usuário profissional (ex.: `joaosilva-dev`, e não `xXjoaoXx`). **Anote o e-mail usado** — vai precisar dele no passo 1.2.
2. Já logado, clique no **+** (canto superior direito) → **New repository**.
3. Preencha:
   - **Repository name:** `bancada-quarto-chines`
   - **Description:** `Bancada de estratégias de casamento sintático — TCC (NIC)`
   - **Public** (repositórios públicos contam como portfólio; se o orientador preferir, use Private)
   - Marque **Add a README file**
   - Em **Add .gitignore**, escolha o modelo **Python**
4. Clique em **Create repository**.
5. Adicione o orientador como colaborador: **Settings → Collaborators → Add people** → digite o usuário do GitHub do orientador (peça a ele).

### Tarefa 1.2 — Configurar o Git e clonar o repositório

Abra o **PowerShell** (ou o terminal do VS Code: menu **Terminal → New Terminal**).

1. Confira se o Git está instalado:

   ```powershell
   git --version
   ```

   Se aparecer algo como `git version 2.x`, está tudo certo. Se der erro, avise o orientador (ver [Riscos](#riscos-e-o-que-fazer)).

2. Diga ao Git quem você é (uma vez por computador; use o **mesmo e-mail da conta do GitHub**):

   ```powershell
   git config --global user.name "Seu Nome Completo"
   git config --global user.email "seu-email@exemplo.com"
   ```

3. Escolha uma pasta de trabalho e clone o repositório. No GitHub, na página do repositório, clique no botão verde **Code** e copie o endereço HTTPS:

   ```powershell
   cd $HOME\Documents
   git clone https://github.com/SEU-USUARIO/bancada-quarto-chines.git
   cd bancada-quarto-chines
   code .
   ```

   O último comando abre a pasta no VS Code.

4. No **primeiro `git push`**, vai abrir uma janela do navegador pedindo para você entrar no GitHub. Faça o login e autorize. Nos computadores compartilhados do laboratório, **faça logout do GitHub no navegador** ao terminar o dia.

### Tarefa 1.3 — Ambiente virtual e Django

Um **ambiente virtual** é uma pasta (`.venv`) com um Python só deste projeto. Assim as bibliotecas que você instala não se misturam com as de outros projetos e não precisam de permissão de administrador.

No terminal, **dentro da pasta do repositório**:

```powershell
python -m venv .venv
.venv\Scripts\activate
```

Se aparecer `(.venv)` no começo da linha, deu certo.

> **Deu erro de "execução de scripts foi desabilitada"?** Rode uma vez `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` e tente de novo. Se ainda assim for bloqueado, use o Prompt de Comando (`cmd`) e rode `.venv\Scripts\activate.bat`.

**Toda vez que abrir o terminal para trabalhar, ative o ambiente de novo.**

Instale as bibliotecas e registre as versões:

```powershell
python -m pip install --upgrade pip
pip install django matplotlib
pip freeze > requirements.txt
```

O `requirements.txt` é a "lista de compras" do projeto: qualquer pessoa pode recriar o ambiente com `pip install -r requirements.txt`.

### Tarefa 1.4 — Criar o projeto e o app Django

```powershell
django-admin startproject config .
python manage.py startapp bancada
```

Atenção ao **ponto** no final do primeiro comando: ele cria o projeto na pasta atual.

- `config` é o **projeto** (as configurações gerais);
- `bancada` é o **app** (onde fica o seu código: o livro de regras, as estratégias e o comando do experimento).

Abra `config/settings.py` e faça três alterações:

```python
INSTALLED_APPS = [
    "django.contrib.admin",
    # ... (deixe os que já existem)
    "bancada",                 # <- acrescente esta linha
]

LANGUAGE_CODE = "pt-br"        # painel em português
TIME_ZONE = "America/Fortaleza"
```

Crie o banco e rode o servidor:

```powershell
python manage.py migrate
python manage.py runserver
```

Abra `http://127.0.0.1:8000/` no navegador. Se aparecer o foguete do Django, funcionou. Tire um *print* e salve em `docs/evidencias/s1_django_rodando.png`. Para parar o servidor: **Ctrl + C** no terminal.

### Tarefa 1.5 — Organizar as pastas e o `.gitignore`

Crie esta estrutura (as pastas vazias você preenche nas próximas sprints):

```
bancada-quarto-chines/
├── bancada/                ← o app (código do experimento)
├── config/                 ← configurações do Django
├── dados/                  ← livro de regras (regras.json) e bateria (bateria.csv)
├── resultados/             ← CSVs gerados pelo experimento
├── graficos/               ← script e imagens dos gráficos
├── docs/
│   ├── diario.md           ← diário de bordo
│   ├── ambiente.md         ← descrição do computador e das versões
│   ├── protocolo.md        ← as regras do experimento (Sprint 3)
│   └── evidencias/         ← prints
├── manage.py
├── requirements.txt
├── README.md
└── .gitignore
```

O `.gitignore` do modelo Python já ignora a pasta `.venv`. Abra-o e confira se, **no final do arquivo**, estão estas linhas (se não estiverem, acrescente):

```
.venv/
db.sqlite3
__pycache__/
```

> **Por que não guardar o `db.sqlite3` no Git?** Porque o banco é **gerado** a partir dos arquivos em `dados/`. Quem clonar o repositório recria tudo com dois comandos (você verá isso na Sprint 2). É isso que torna o experimento **reprodutível**.

### Tarefa 1.6 — Registrar o ambiente

Em `docs/ambiente.md`, anote (vai para Materiais e Métodos):

- processador e memória RAM (Configurações → Sistema → Sobre);
- versão do Windows;
- versão do Python (`python --version`);
- versão do Django (`python -m django --version`);
- versão do matplotlib (está no `requirements.txt`).

**Rode o experimento final sempre no mesmo computador**, senão os tempos não são comparáveis. Anote qual é (ex.: "Laboratório 3, máquina 12").

### Tarefa 1.7 — Primeiro commit

```powershell
git status
git add .
git commit -m "Cria o projeto Django e o app bancada"
git push
```

Antes do `git add .`, confira no `git status` que a pasta `.venv` e o `db.sqlite3` **não** aparecem na lista. Se aparecerem, o `.gitignore` está errado — corrija antes de comitar.

### Tarefa 1.8 — Leitura: o Quarto Chinês

Leia um texto curto em português sobre o experimento do Quarto Chinês (comece por LIMA FILHO, 2010, que está nas referências do projeto) e escreva, com as suas palavras, **um parágrafo** em `docs/diario.md` respondendo: *"O que acontece dentro do quarto, e por que Searle diz que a pessoa não entende chinês?"*. Isso ajuda na Introdução do TCC, que vence em **30/09**.

### Entregas da Sprint 1

- [ ] Repositório `bancada-quarto-chines` no GitHub, com o orientador como colaborador
- [ ] Projeto Django rodando (print em `docs/evidencias/`)
- [ ] `requirements.txt`, `.gitignore` e `docs/ambiente.md`
- [ ] Parágrafo sobre o Quarto Chinês no diário

---

# Sprint 2 — 30/09 a 06/10: o livro de regras

**Objetivo da semana:** criar a tabela de regras no banco, cadastrar **12 regras** pelo Django Admin e salvá-las em um arquivo que vai para o Git.

### Tarefa 2.1 — Escolher o tema das regras

O livro de regras simula o **atendimento de dúvidas de estudantes sobre o campus**. O tema é conhecido por você, o que facilita inventar perguntas realistas. Sugestão de 12 regras (combine com o orientador):

| Nome | Assunto |
|---|---|
| R01 | Horário de funcionamento do campus |
| R02 | Horário da biblioteca |
| R03 | Empréstimo de livros |
| R04 | Matrícula / renovação de matrícula |
| R05 | Refeitório / merenda |
| R06 | Senha do Wi-Fi |
| R07 | Transporte / horário do ônibus |
| R08 | Estágio |
| R09 | Calendário acadêmico / férias |
| R10 | Emissão de declaração na secretaria |
| R11 | Carteira estudantil |
| R12 | Auxílios e bolsas estudantis |

**As respostas podem ser fictícias** (ex.: "A biblioteca funciona das 8h às 21h."). O que importa no experimento é **qual regra foi escolhida**, não se a informação é verdadeira. Diga isso no TCC.

Repare que várias regras **se parecem de propósito** (R01, R02 e R07 falam de "horário"; R02 e R03 falam de "biblioteca/livros"). É assim que aparecem as respostas inadequadas — e é isso que torna o experimento interessante.

### Tarefa 2.2 — Criar o modelo `Regra`

Um **modelo** (*model*) no Django é uma classe Python que vira uma tabela no banco. Cada atributo vira uma coluna.

Em `bancada/models.py`:

```python
from django.db import models


class Regra(models.Model):
    # Identificação curta, usada no gabarito (ex.: R01)
    nome = models.CharField(max_length=10, unique=True)
    # Assunto, só para você se localizar (ex.: "Horário do campus")
    assunto = models.CharField(max_length=100)
    # Pergunta cadastrada: usada pelas estratégias 1, 2 e 5
    pergunta = models.CharField(max_length=200)
    # Trecho curto: usado pela estratégia 3 (contém)
    trecho = models.CharField(max_length=50)
    # Palavras-chave separadas por vírgula: usadas pela estratégia 4
    palavras_chave = models.CharField(max_length=200)
    # Resposta que o sistema devolve quando a regra é escolhida
    resposta = models.TextField()

    class Meta:
        ordering = ["nome"]

    def __str__(self):
        return f"{self.nome} - {self.assunto}"
```

Por que cada estratégia usa um campo diferente? Porque cada uma precisa de uma "pista" diferente: a igualdade exata precisa da pergunta inteira; a estratégia "contém" precisa de um trecho curto; a de palavras-chave, de uma lista de palavras. **Todos os campos de todas as regras são preenchidos agora**, antes de existir qualquer estratégia.

Crie a tabela no banco:

```powershell
python manage.py makemigrations
python manage.py migrate
```

### Tarefa 2.3 — Registrar no Django Admin

Em `bancada/admin.py`:

```python
from django.contrib import admin

from .models import Regra


@admin.register(Regra)
class RegraAdmin(admin.ModelAdmin):
    list_display = ["nome", "assunto", "pergunta", "trecho", "palavras_chave"]
    search_fields = ["nome", "assunto", "pergunta"]
```

Crie o seu usuário administrador e abra o painel:

```powershell
python manage.py createsuperuser
python manage.py runserver
```

Acesse `http://127.0.0.1:8000/admin/`, entre com o usuário criado e cadastre as 12 regras. Exemplo de uma regra completa:

| Campo | Valor |
|---|---|
| nome | `R01` |
| assunto | `Horário do campus` |
| pergunta | `Qual é o horário de funcionamento do campus?` |
| trecho | `funcionamento` |
| palavras_chave | `horario, funcionamento, campus, abre, fecha` |
| resposta | `O campus funciona de segunda a sexta, das 7h às 22h.` |

Cuidados ao preencher:

- **pergunta:** escreva como um estudante escreveria, com acento e ponto de interrogação;
- **trecho:** uma palavra ou expressão curta que **identifique bem** a regra. Evite trechos que aparecem em várias regras (se R01 e R02 tiverem o trecho "horário", as duas vão disputar a mesma mensagem);
- **palavras_chave:** de 3 a 5 palavras, **sem acento e em minúsculas**, separadas por vírgula.

Tire um *print* da lista de regras no Admin: `docs/evidencias/s2_admin_regras.png`.

### Tarefa 2.4 — Salvar as regras em arquivo (*fixture*)

O banco não vai para o Git, então as regras precisam ser salvas em um arquivo:

```powershell
python manage.py dumpdata bancada.Regra --indent 2 -o dados/regras.json
```

Abra o `dados/regras.json` e veja: são as suas 12 regras em formato texto. Para recriar o banco em outro computador:

```powershell
python manage.py migrate
python manage.py loaddata dados/regras.json
```

**Teste isso agora:** apague o `db.sqlite3`, rode os dois comandos acima e confira no Admin se as regras voltaram (vai precisar criar o superusuário de novo). Se voltaram, o seu livro de regras é reprodutível.

> **Sempre que alterar uma regra no Admin, rode o `dumpdata` de novo e comite o `regras.json`.** Depois da Sprint 3, as regras ficam congeladas e não mudam mais.

### Tarefa 2.5 — Leitura: *chatbots* baseados em regras

Pesquise sobre o **ELIZA** (Weizenbaum, 1966), o primeiro *chatbot* conhecido, que funcionava só com regras de padrões de texto — e mesmo assim algumas pessoas acreditavam que ele as entendia. Anote no diário: como o ELIZA funcionava e por que isso tem a ver com o seu trabalho. Vai para o Referencial Teórico (prazo: **14/10**).

### Entregas da Sprint 2

- [ ] Modelo `Regra` criado e registrado no Admin
- [ ] 12 regras cadastradas, com **todos** os campos preenchidos
- [ ] `dados/regras.json` no Git, testado com `loaddata`
- [ ] Print do Admin e anotações sobre o ELIZA no diário

---

# Sprint 3 — 07/10 a 13/10: a bateria de 100 mensagens e o gabarito

**Objetivo da semana:** escrever as 100 mensagens de teste, o gabarito de cada uma e as regras do experimento — e **congelar** tudo antes de programar qualquer estratégia.

Esta é **a sprint mais importante do trabalho**. A bateria é o seu instrumento de medida: se ela for mal feita, todos os resultados ficam comprometidos.

### Tarefa 3.1 — Entender o que é o gabarito

Para cada mensagem, você decide **antes** qual regra **deveria** ser escolhida. Com isso, cada resultado das estratégias será classificado automaticamente assim:

| O que a estratégia fez | O gabarito dizia | Classificação |
|---|---|---|
| Escolheu a regra R02 | R02 | **Adequada** |
| Escolheu a regra R07 | R02 | **Inadequada** (qualquer regra diferente da esperada é inadequada) |
| Escolheu uma regra qualquer | *vazio* (fora do escopo) | **Inadequada** — respondeu o que não devia |
| Não escolheu nenhuma | R02 | **Sem resposta** (indevida) |
| Não escolheu nenhuma | *vazio* (fora do escopo) | **Sem resposta** (correta: ficar calado era o certo) |

### Tarefa 3.2 — Escrever as 100 mensagens

Use o **Google Planilhas** (gratuito, no navegador) com exatamente estas quatro colunas:

| numero | mensagem | categoria | regra_esperada |
|---|---|---|---|
| 1 | Qual é o horário de funcionamento do campus? | identica | R01 |
| 2 | QUAL E O HORARIO DE FUNCIONAMENTO DO CAMPUS | forma | R01 |
| 3 | Até que horas o campus fica aberto? | parafrase | R01 |
| 4 | qual o horaro de funcionamnto do campus | digitacao | R01 |
| 5 | Quem ganhou o jogo de ontem? | fora | |

Distribua as 100 mensagens em **cinco categorias**:

| Categoria | Quantidade | O que é | Para que serve |
|---|---|---|---|
| `identica` | 12 | Igual à pergunta cadastrada (uma por regra) | Garante que toda estratégia acerta o caso mais fácil |
| `forma` | 20 | Mesmo texto, mas com maiúsculas, sem acento, sem pontuação ou com espaços a mais | Mostra o efeito da normalização |
| `parafrase` | 36 | Mesmo pedido com **outras palavras** ("Até que horas o campus fica aberto?") | É onde a diferença entre as estratégias aparece |
| `digitacao` | 12 | Com erros de digitação ("horaro", "bibliotca") | Mostra onde a similaridade ajuda |
| `fora` | 20 | Perguntas que **nenhuma** regra responde ("Qual a capital da França?") e perguntas **parecidas** com as regras, mas diferentes ("Qual o horário do jogo?") | Mede as respostas inadequadas — o sistema deveria ficar calado |

Regras para escrever:

1. **Escreva como um estudante de verdade escreveria** — inclusive com gírias e abreviações ("vcs", "q horas"). Não escreva pensando em qual estratégia vai acertar.
2. **Distribua as mensagens entre as 12 regras** de forma parecida (cerca de 6 a 7 por regra, fora a categoria `fora`).
3. **Inclua casos difíceis de propósito** na categoria `fora`: mensagens que têm as mesmas palavras das regras, mas pedem outra coisa ("Qual o horário do ônibus da excursão de sábado?", "A biblioteca da cidade abre domingo?"). São elas que revelam o "erro com confiança".
4. **Mensagens com duas perguntas ao mesmo tempo, não.** Cada mensagem deve ter uma única resposta certa (ou nenhuma).
5. **Não use ponto e vírgula nem quebra de linha dentro das mensagens.**

Quando terminar: **Arquivo → Fazer download → Valores separados por vírgula (.csv)** e salve como `dados/bateria.csv`. Abra o arquivo no VS Code e confira se a primeira linha é `numero,mensagem,categoria,regra_esperada` e se os acentos aparecem corretamente.

### Tarefa 3.3 — Escrever o protocolo do experimento

Crie `docs/protocolo.md` com as decisões que **não podem mudar depois**. Este arquivo vai quase direto para a seção de Materiais e Métodos:

```markdown
# Protocolo do experimento

Data de congelamento: __/10/2026

## Livro de regras
- 12 regras, em dados/regras.json.
- Ordem de consulta: pelo nome (R01, R02, ...). Em caso de empate, vence a primeira.

## Bateria
- 100 mensagens, em dados/bateria.csv (categorias: identica 12, forma 20,
  parafrase 36, digitacao 12, fora 20).

## Classificação
- Adequada: regra escolhida = regra esperada.
- Inadequada: escolheu uma regra diferente da esperada, ou escolheu uma regra
  quando a esperada era nenhuma.
- Sem resposta: nenhuma regra escolhida.

## Parâmetros das estratégias (fixos)
- Normalização: minúsculas; remoção de acentos; pontuação trocada por espaço;
  espaços repetidos reduzidos a um.
- Contém: o trecho da regra aparece na mensagem, ignorando maiúsculas e minúsculas.
- Palavras-chave: a regra dispara quando pelo menos 50% das suas palavras-chave
  aparecem na mensagem normalizada; vence a regra com o maior percentual.
- Similaridade: SequenceMatcher sobre os textos normalizados; limiar = 0,75;
  vence a regra com a maior similaridade.

## Medição de tempo
- Bateria inteira executada 10 vezes por estratégia; registra-se a média.
- O tempo não inclui a leitura do banco nem do CSV.
- Computador: (ver docs/ambiente.md).
```

> **Por que o limiar é 0,75 e não outro valor?** Um valor tem de ser escolhido **antes** de ver os resultados, e 0,75 é um ponto de partida razoável. Veja um exemplo que você pode calcular: "Qual é o horário de funcionamento?" e "Qual é o horário do ônibus?" têm similaridade **0,71** — pedem coisas diferentes, e o limiar de 0,75 evita que uma dispare a outra. Se quiser, **depois** do experimento principal, você pode rodar outros limiares como análise extra — mas o resultado principal é sempre o de 0,75.

### Tarefa 3.4 — Revisão do orientador e congelamento

1. Envie a planilha e o protocolo ao orientador. **Só congele depois da aprovação.**
2. Faça os ajustes pedidos.
3. Congele com um commit e uma *tag* (uma "etiqueta" que marca aquele momento no histórico):

```powershell
git add dados/ docs/protocolo.md
git commit -m "Congela a bateria, o gabarito e o livro de regras"
git tag bateria-congelada
git push
git push --tags
```

A partir de agora, **`dados/bateria.csv` e `dados/regras.json` não mudam mais.** Se você achar um erro grave em uma mensagem, **não corrija sozinho**: fale com o orientador e registre a decisão no diário e no TCC.

### Entregas da Sprint 3

- [ ] `dados/bateria.csv` com 100 mensagens, categoria e regra esperada
- [ ] `docs/protocolo.md` preenchido
- [ ] Aprovação do orientador
- [ ] Tag `bateria-congelada` no GitHub

---

# Sprint 4 — 14/10 a 20/10: estratégias 1 e 2 (igualdade exata e normalização)

**Objetivo da semana:** programar as duas primeiras estratégias e testá-las.

Todas as estratégias ficam em um único arquivo, `bancada/estrategias.py`, e **seguem o mesmo formato**: recebem a mensagem e a lista de regras, e devolvem a regra escolhida — ou `None`, se nenhuma servir. Esse formato comum é o que permite, depois, rodar a mesma bateria em todas elas.

### Tarefa 4.1 — Estratégia 1: igualdade exata

Crie `bancada/estrategias.py`:

```python
"""Estratégias de casamento sintático.

Todas recebem a mensagem do usuário e a lista de regras, e devolvem
a regra escolhida ou None (quando nenhuma regra se aplica).
"""
import string
import unicodedata
from difflib import SequenceMatcher


def igualdade_exata(mensagem, regras):
    """Estratégia 1: a mensagem precisa ser idêntica à pergunta da regra."""
    for regra in regras:
        if mensagem == regra.pergunta:
            return regra
    return None
```

### Tarefa 4.2 — A função `normalizar` e a estratégia 2

Acrescente ao mesmo arquivo:

```python
def normalizar(texto):
    """Minúsculas, sem acentos, sem pontuação e sem espaços repetidos."""
    texto = texto.lower()
    # Separa as letras dos acentos ("á" vira "a" + acento) e descarta os acentos
    texto = unicodedata.normalize("NFD", texto)
    texto = "".join(c for c in texto if unicodedata.category(c) != "Mn")
    # Troca cada sinal de pontuação por um espaço
    for sinal in string.punctuation:
        texto = texto.replace(sinal, " ")
    # split() quebra nos espaços (quantos forem); join() junta com um só
    return " ".join(texto.split())


def normalizacao(mensagem, regras):
    """Estratégia 2: igualdade exata, mas entre os textos normalizados."""
    mensagem_normalizada = normalizar(mensagem)
    for regra in regras:
        if mensagem_normalizada == normalizar(regra.pergunta):
            return regra
    return None
```

Entenda linha por linha antes de seguir. Teste no *shell* do Django:

```powershell
python manage.py shell
```

```python
>>> from bancada.estrategias import normalizar
>>> normalizar("Qual É   o HORÁRIO de funcionamento?!")
'qual e o horario de funcionamento'
```

Teste com pelo menos 5 frases suas. Para sair do *shell*: `exit()`.

### Tarefa 4.3 — Testes automáticos

Um **teste automático** é um código que confere se outro código faz o que deveria. Em `bancada/tests.py`:

```python
from types import SimpleNamespace

from django.test import SimpleTestCase

from .estrategias import igualdade_exata, normalizacao, normalizar

# Regras "de mentira", só para os testes (não usam o banco)
R01 = SimpleNamespace(nome="R01", pergunta="Qual é o horário de funcionamento?")
R02 = SimpleNamespace(nome="R02", pergunta="Qual o horário da biblioteca?")
REGRAS = [R01, R02]


class NormalizarTeste(SimpleTestCase):
    def test_remove_maiusculas_acentos_e_pontuacao(self):
        self.assertEqual(normalizar("Qual É o HORÁRIO?"), "qual e o horario")

    def test_reduz_espacos(self):
        self.assertEqual(normalizar("  qual   o  horario "), "qual o horario")


class IgualdadeExataTeste(SimpleTestCase):
    def test_texto_identico(self):
        self.assertEqual(igualdade_exata("Qual é o horário de funcionamento?", REGRAS), R01)

    def test_minusculas_nao_casam(self):
        self.assertIsNone(igualdade_exata("qual é o horário de funcionamento?", REGRAS))


class NormalizacaoTeste(SimpleTestCase):
    def test_forma_diferente_casa(self):
        self.assertEqual(normalizacao("QUAL E O HORARIO DE FUNCIONAMENTO", REGRAS), R01)

    def test_palavras_diferentes_nao_casam(self):
        self.assertIsNone(normalizacao("Qual o horário de funcionamento?", REGRAS))
```

Rode:

```powershell
python manage.py test bancada
```

Deve aparecer `OK`. Acrescente **pelo menos mais 2 testes** seus para cada estratégia. Tire um *print* do resultado: `docs/evidencias/s4_testes.png`.

> **Os testes usam regras de mentira, e não a bateria.** A bateria é para o experimento, não para testar o código — assim você não fica tentado a ajustar o código "olhando" para ela.

### Entregas da Sprint 4

- [ ] `bancada/estrategias.py` com `igualdade_exata`, `normalizar` e `normalizacao`
- [ ] `bancada/tests.py` passando, com testes seus além dos exemplos
- [ ] Diário atualizado

---

# Sprint 5 — 21/10 a 27/10: estratégias 3 e 4 (contém e palavras-chave)

**Objetivo da semana:** programar as estratégias 3 e 4, seguindo exatamente as regras do `docs/protocolo.md`.

### Tarefa 5.1 — Estratégia 3: contém

A ideia é a mesma do `icontains` do Django: "contém, ignorando maiúsculas e minúsculas". A diferença é que aqui queremos saber se o **trecho da regra** está **dentro da mensagem**, então fazemos em Python:

```python
def contem(mensagem, regras):
    """Estratégia 3: o trecho da regra aparece na mensagem (ignora maiúsculas)."""
    mensagem_minuscula = mensagem.lower()
    for regra in regras:
        if regra.trecho.lower() in mensagem_minuscula:
            return regra
    return None
```

Observe duas características que **você vai discutir nos Resultados**:

- a estratégia **não remove acentos** — "horario" não contém "horário";
- ela devolve a **primeira** regra cujo trecho aparece, mesmo que outras também apareçam. A ordem das regras (R01, R02...) passa a influenciar o resultado.

### Tarefa 5.2 — Estratégia 4: palavras-chave

```python
PROPORCAO_MINIMA_PALAVRAS_CHAVE = 0.5


def palavras_chave(mensagem, regras):
    """Estratégia 4: pelo menos 50% das palavras-chave aparecem na mensagem.

    Vence a regra com o maior percentual; em caso de empate, a primeira.
    """
    palavras_da_mensagem = set(normalizar(mensagem).split())
    melhor_regra = None
    maior_proporcao = 0.0
    for regra in regras:
        chaves = [normalizar(p) for p in regra.palavras_chave.split(",") if p.strip()]
        if not chaves:
            continue
        encontradas = sum(1 for chave in chaves if chave in palavras_da_mensagem)
        proporcao = encontradas / len(chaves)
        if proporcao > maior_proporcao:
            melhor_regra = regra
            maior_proporcao = proporcao
    if maior_proporcao >= PROPORCAO_MINIMA_PALAVRAS_CHAVE:
        return melhor_regra
    return None
```

Entenda os pontos principais:

- `set(...)` guarda as palavras da mensagem **sem repetição e sem ordem** — é por isso que a ordem das palavras não importa;
- a comparação é **palavra por palavra**: "horarios" (plural) **não** é igual a "horario". Anote isso no diário — é uma limitação que aparece nos Resultados;
- o `>` (e não `>=`) na comparação garante que, em caso de empate, fica a **primeira** regra, como diz o protocolo.

### Tarefa 5.3 — Testes

Acrescente ao `bancada/tests.py` regras de mentira com `trecho` e `palavras_chave`:

```python
R03 = SimpleNamespace(
    nome="R03",
    pergunta="Qual é o horário de funcionamento do campus?",
    trecho="funcionamento",
    palavras_chave="horario, funcionamento, campus",
)
```

E escreva testes para:

- `contem` encontrando o trecho no meio da frase;
- `contem` **não** encontrando quando a mensagem vem sem acento e o trecho tem acento;
- `palavras_chave` com as palavras em outra ordem ("Queria saber o funcionamento e o horário do campus");
- `palavras_chave` abaixo do mínimo (só 1 de 3 palavras → `None`).

```powershell
python manage.py test bancada
```

### Tarefa 5.4 — Diário e leitura

No diário, responda: *"A estratégia de palavras-chave 'entende' a pergunta? O que exatamente ela está fazendo?"*. Essa resposta, com as suas palavras, é o começo da discussão do TCC.

### Entregas da Sprint 5

- [ ] Funções `contem` e `palavras_chave` em `bancada/estrategias.py`
- [ ] Testes novos passando
- [ ] Diário atualizado

---

# Sprint 6 — 28/10 a 03/11: estratégia 5 e o comando `testar_estrategias`

**Objetivo da semana:** terminar as estratégias e criar o comando que roda o experimento inteiro e grava os resultados.

### Tarefa 6.1 — Estratégia 5: similaridade

O `SequenceMatcher`, da biblioteca `difflib`, compara dois textos e devolve um número entre **0** (nada parecido) e **1** (idênticos). Experimente no *shell* antes de programar:

```python
>>> from difflib import SequenceMatcher
>>> SequenceMatcher(None, "qual e o horario", "quais sao os horarios").ratio()
```

Acrescente ao `bancada/estrategias.py`:

```python
LIMIAR_SIMILARIDADE = 0.75


def similaridade(mensagem, regras):
    """Estratégia 5: a regra com a pergunta mais parecida, se passar do limiar."""
    mensagem_normalizada = normalizar(mensagem)
    melhor_regra = None
    maior_valor = 0.0
    for regra in regras:
        valor = SequenceMatcher(None, mensagem_normalizada, normalizar(regra.pergunta)).ratio()
        if valor > maior_valor:
            melhor_regra = regra
            maior_valor = valor
    if maior_valor >= LIMIAR_SIMILARIDADE:
        return melhor_regra
    return None


# Todas as estratégias, na ordem em que aparecem no TCC
ESTRATEGIAS = {
    "Igualdade exata": igualdade_exata,
    "Normalização": normalizacao,
    "Contém": contem,
    "Palavras-chave": palavras_chave,
    "Similaridade": similaridade,
}
```

O dicionário `ESTRATEGIAS` junta as cinco funções. Como todas recebem os mesmos parâmetros, o comando do experimento pode chamá-las uma depois da outra, em um único laço `for`.

Escreva também testes para `similaridade` (um caso acima do limiar e um abaixo) e rode `python manage.py test bancada`.

### Tarefa 6.2 — O comando `testar_estrategias`

Um **comando de gerenciamento** é um programa que roda com `python manage.py nome_do_comando`. Crie as pastas e arquivos (os `__init__.py` ficam **vazios**):

```
bancada/
└── management/
    ├── __init__.py
    └── commands/
        ├── __init__.py
        └── testar_estrategias.py
```

Em `bancada/management/commands/testar_estrategias.py`:

```python
import csv
import time
from pathlib import Path

from django.core.management.base import BaseCommand

from bancada.estrategias import ESTRATEGIAS
from bancada.models import Regra

ARQUIVO_BATERIA = Path("dados/bateria.csv")
PASTA_RESULTADOS = Path("resultados")
REPETICOES_TEMPO = 10


def classificar(regra_esperada, regra_obtida):
    """Compara o que a estratégia escolheu com o gabarito."""
    if regra_obtida == "":
        return "sem resposta"
    if regra_obtida == regra_esperada:
        return "adequada"
    return "inadequada"


class Command(BaseCommand):
    help = "Executa a bateria de mensagens em todas as estratégias e grava os resultados."

    def handle(self, *args, **options):
        # Lê o livro de regras e a bateria UMA vez, fora da medição de tempo
        regras = list(Regra.objects.order_by("nome"))
        with open(ARQUIVO_BATERIA, encoding="utf-8-sig", newline="") as arquivo:
            bateria = list(csv.DictReader(arquivo))
        self.stdout.write(f"{len(regras)} regras e {len(bateria)} mensagens carregadas.")

        PASTA_RESULTADOS.mkdir(exist_ok=True)
        detalhes = []
        resumo = []

        for nome_estrategia, estrategia in ESTRATEGIAS.items():
            contagem = {"adequada": 0, "inadequada": 0, "sem resposta": 0}
            silencio_correto = 0

            # 1) Classificação: cada mensagem passa uma vez pela estratégia
            for item in bateria:
                esperada = item["regra_esperada"].strip()
                regra = estrategia(item["mensagem"], regras)
                obtida = regra.nome if regra else ""
                classificacao = classificar(esperada, obtida)
                contagem[classificacao] += 1
                if classificacao == "sem resposta" and esperada == "":
                    silencio_correto += 1
                detalhes.append({
                    "estrategia": nome_estrategia,
                    "numero": item["numero"],
                    "mensagem": item["mensagem"],
                    "categoria": item["categoria"],
                    "regra_esperada": esperada,
                    "regra_obtida": obtida,
                    "classificacao": classificacao,
                })

            # 2) Tempo: a bateria inteira, repetida várias vezes
            tempos = []
            for _ in range(REPETICOES_TEMPO):
                inicio = time.perf_counter()
                for item in bateria:
                    estrategia(item["mensagem"], regras)
                tempos.append(time.perf_counter() - inicio)
            tempo_medio_ms = sum(tempos) / len(tempos) * 1000

            resumo.append({
                "estrategia": nome_estrategia,
                "adequadas": contagem["adequada"],
                "inadequadas": contagem["inadequada"],
                "sem_resposta": contagem["sem resposta"],
                "sem_resposta_correta": silencio_correto,
                "tempo_medio_ms": f"{tempo_medio_ms:.3f}",
            })
            self.stdout.write(
                f"{nome_estrategia:<16} adequadas={contagem['adequada']:>3} "
                f"inadequadas={contagem['inadequada']:>3} "
                f"sem resposta={contagem['sem resposta']:>3} "
                f"tempo={tempo_medio_ms:.3f} ms"
            )

        self.gravar_csv(PASTA_RESULTADOS / "detalhado.csv", detalhes)
        self.gravar_csv(PASTA_RESULTADOS / "resumo.csv", resumo)
        self.stdout.write(self.style.SUCCESS("Resultados gravados na pasta resultados/."))

    def gravar_csv(self, caminho, linhas):
        with open(caminho, "w", encoding="utf-8-sig", newline="") as arquivo:
            escritor = csv.DictWriter(arquivo, fieldnames=linhas[0].keys())
            escritor.writeheader()
            escritor.writerows(linhas)
```

Leia com calma e identifique no código:

1. onde a bateria é lida;
2. onde cada mensagem é classificada (adequada / inadequada / sem resposta);
3. por que o tempo é medido em um **segundo laço**, separado da classificação;
4. por que a leitura do banco fica **fora** da medição de tempo.

Rode:

```powershell
python manage.py testar_estrategias
```

A saída deve ter cinco linhas, uma por estratégia, e a pasta `resultados/` deve ter dois arquivos: `resumo.csv` (5 linhas) e `detalhado.csv` (500 linhas — 100 mensagens × 5 estratégias).

### Tarefa 6.3 — Conferência manual

Antes de confiar nos números, **confira à mão**:

- a soma adequadas + inadequadas + sem resposta dá **100** em cada estratégia?
- a estratégia 1 acertou **todas** as mensagens da categoria `identica`? (Deveria.)
- escolha 5 linhas do `detalhado.csv` e confira, lendo a mensagem, se a classificação está certa.

Se encontrar um **erro no código**, corrija o código e rode de novo — isso é permitido. O que **não** é permitido é mudar a bateria ou as regras. Anote no diário qualquer correção.

Comite os resultados:

```powershell
git add bancada/ resultados/
git commit -m "Cria o comando testar_estrategias e gera a primeira execução"
git push
```

### Entregas da Sprint 6

- [ ] Estratégia 5 e dicionário `ESTRATEGIAS`
- [ ] Comando `testar_estrategias` funcionando
- [ ] `resultados/resumo.csv` e `resultados/detalhado.csv`
- [ ] Conferência manual registrada no diário
- [ ] Print da saída do comando: `docs/evidencias/s6_comando.png`

---

# Sprint 7 — 04/11 a 10/11: gráficos, tabelas e análise dos erros

**Objetivo da semana:** transformar os CSVs em tabelas e gráficos para o TCC e selecionar os exemplos que vão para a discussão.

### Tarefa 7.1 — Execução oficial

Feche os outros programas do computador (navegador, jogos, etc.), para não atrapalhar a medição de tempo, e rode o experimento **uma última vez**, no computador anotado em `docs/ambiente.md`:

```powershell
python manage.py testar_estrategias
git add resultados/
git commit -m "Execução oficial do experimento"
git tag execucao-oficial
git push --tags
git push
```

### Tarefa 7.2 — Tabela comparativa

Com o `resultados/resumo.csv`, monte a tabela principal do TCC:

| Estratégia | Adequadas | Inadequadas | Sem resposta | Tempo médio (ms) |
|---|---:|---:|---:|---:|
| Igualdade exata | — | — | — | — |
| Normalização | — | — | — | — |
| Contém | — | — | — | — |
| Palavras-chave | — | — | — | — |
| Similaridade | — | — | — | — |

Monte também uma **segunda tabela, por categoria**: quantas mensagens adequadas cada estratégia teve em cada categoria (`identica`, `forma`, `parafrase`, `digitacao`, `fora`). Você pode fazer isso no Google Planilhas: importe o `detalhado.csv` e use **Inserir → Tabela dinâmica** (linhas: estratégia; colunas: categoria; valores: contagem de classificação, com filtro "adequada"). É essa tabela que mostra **onde** cada estratégia ganha e perde.

### Tarefa 7.3 — Gráficos com `matplotlib`

Crie `graficos/gerar_graficos.py`:

```python
"""Gera os gráficos do TCC a partir de resultados/resumo.csv."""
import csv
from pathlib import Path

import matplotlib.pyplot as plt

PASTA = Path(__file__).resolve().parent
with open(PASTA.parent / "resultados" / "resumo.csv", encoding="utf-8-sig") as arquivo:
    resumo = list(csv.DictReader(arquivo))

estrategias = [linha["estrategia"] for linha in resumo]
series = [
    ("Adequadas", "adequadas", "#2a78b5", ""),
    ("Inadequadas", "inadequadas", "#d4722c", "//"),
    ("Sem resposta", "sem_resposta", "#9a9a9a", ".."),
]

# Gráfico 1: barras agrupadas (adequadas, inadequadas, sem resposta)
fig, ax = plt.subplots(figsize=(9, 5))
largura = 0.26
for i, (rotulo, coluna, cor, hachura) in enumerate(series):
    valores = [int(linha[coluna]) for linha in resumo]
    posicoes = [x + (i - 1) * largura for x in range(len(estrategias))]
    barras = ax.bar(posicoes, valores, largura, label=rotulo, color=cor,
                    hatch=hachura, edgecolor="white")
    ax.bar_label(barras, fontsize=8)
ax.set_xticks(range(len(estrategias)))
ax.set_xticklabels(estrategias)
ax.set_ylabel("Número de mensagens (de 100)")
ax.set_ylim(0, 100)
ax.legend(frameon=False)
ax.spines[["top", "right"]].set_visible(False)
fig.tight_layout()
fig.savefig(PASTA / "grafico_classificacao.png", dpi=200)

# Gráfico 2: tempo médio por estratégia
fig, ax = plt.subplots(figsize=(9, 4))
tempos = [float(linha["tempo_medio_ms"]) for linha in resumo]
barras = ax.bar(estrategias, tempos, color="#2a78b5")
ax.bar_label(barras, fmt="%.2f", fontsize=8)
ax.set_ylabel("Tempo médio da bateria (ms)")
ax.spines[["top", "right"]].set_visible(False)
fig.tight_layout()
fig.savefig(PASTA / "grafico_tempo.png", dpi=200)

print("Gráficos salvos na pasta graficos/.")
```

Rode com o ambiente ativado:

```powershell
python graficos/gerar_graficos.py
```

Por que as **hachuras** (listras e pontos)? Porque o TCC pode ser impresso em preto e branco, e porque nem todo leitor distingue bem as cores. Com as hachuras, as barras continuam diferentes.

**Olhe os gráficos** antes de colocar no TCC: os rótulos estão legíveis? Os números batem com a tabela? No TCC, o **título vai acima** da figura e a **fonte abaixo** ("Fonte: elaborado pelo autor (2026)") — ver a seção "Como incluir imagens" do `README.md`. **Não coloque título dentro da imagem.**

### Tarefa 7.4 — Análise dos erros

No `detalhado.csv` (filtre no Google Planilhas), escolha e anote no diário:

- **3 exemplos de resposta inadequada** — de preferência de estratégias diferentes. Para cada um: a mensagem, a regra escolhida, a regra certa e **por que** a estratégia errou (ex.: "a similaridade escolheu R01 porque 'horário do ônibus' é parecido com 'horário de funcionamento' letra por letra");
- **2 exemplos em que a similaridade acertou e a igualdade exata não respondeu** — mostram o ganho de "aparência de inteligência";
- **1 exemplo em que todas as estratégias falharam** — mostra o limite da manipulação sintática.

Esses exemplos são o material mais valioso da discussão do TCC. Monte com eles um **quadro** (mensagem × o que cada estratégia respondeu).

### Tarefa 7.5 (opcional) — Análise de sensibilidade do limiar

Só se as tarefas anteriores estiverem prontas. Rode a estratégia 5 com outros limiares (0,5; 0,6; 0,7; 0,8; 0,9) e veja como mudam as adequadas e as inadequadas. Para isso, mude **temporariamente** o `LIMIAR_SIMILARIDADE`, rode o comando, copie o resultado e **volte ao 0,75**. Esse resultado entra no TCC como **análise complementar**, deixando claro que o resultado principal é o de 0,75, definido antes.

### Entregas da Sprint 7

- [ ] Tag `execucao-oficial`
- [ ] Tabela comparativa e tabela por categoria
- [ ] `graficos/grafico_classificacao.png` e `graficos/grafico_tempo.png`
- [ ] Quadro de exemplos de erros e acertos no diário

---

# Sprint 8 — 11/11 a 17/11: reprodutibilidade, documentação e apresentação

**Objetivo da semana:** garantir que qualquer pessoa consiga repetir o experimento e preparar a apresentação.

### Tarefa 8.1 — Teste de reprodutibilidade

Simule um colega que nunca viu o projeto. Em **outra pasta**:

```powershell
cd $HOME\Desktop
git clone https://github.com/SEU-USUARIO/bancada-quarto-chines.git teste-reproducao
cd teste-reproducao
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
python manage.py migrate
python manage.py loaddata dados/regras.json
python manage.py test bancada
python manage.py testar_estrategias
```

As contagens (adequadas, inadequadas, sem resposta) devem ser **idênticas** às da execução oficial. O tempo pode variar um pouco — é normal, e isso vale uma frase no TCC. Se algo falhar, corrija no repositório original e repita. Depois, apague a pasta `teste-reproducao`.

### Tarefa 8.2 — README do repositório

Reescreva o `README.md` com:

1. **O que é** o projeto (2 a 3 frases, citando o Quarto Chinês);
2. **As cinco estratégias** (uma linha cada);
3. **Como instalar e rodar** (os comandos da Tarefa 8.1);
4. **Onde estão** os dados, os resultados e os gráficos;
5. **A tabela de resultados** e o gráfico principal (imagem);
6. **Autoria:** seu nome, orientador, NIC, 2026.

### Tarefa 8.3 (opcional) — Uma tela para demonstração

Só se sobrar tempo. Uma página simples em que se digita uma mensagem e se vê, lado a lado, o que **cada estratégia** responderia. Não entra nos resultados, mas deixa a apresentação muito mais interessante — a banca pode testar ao vivo e ver o sistema "acertar sem entender". Peça orientação antes de começar: é uma *view*, um *template* com um formulário e uma rota.

### Tarefa 8.4 — Apresentação e encerramento

- Prepare de 8 a 10 slides (Google Apresentações): o Quarto Chinês; o problema; as cinco estratégias com um exemplo cada; a bateria; a tabela; o gráfico; os exemplos de erro; a conclusão ("acertar mais não é entender mais").
- Complete o diário com a reflexão final: *"O que mudou na minha forma de ver os chatbots?"*.
- Marque a versão final:

```powershell
git tag v1.0
git push --tags
```

### Entregas da Sprint 8

- [ ] Reprodução em pasta limpa com os mesmos resultados
- [ ] `README.md` completo
- [ ] Slides da apresentação
- [ ] Tag `v1.0`

---

## Riscos e o que fazer

| Risco | O que fazer |
|---|---|
| **O Git não está instalado no laboratório** | Avise o orientador. Alternativa sem instalação: o **PortableGit** (versão portátil oficial do Git para Windows, baixada em `git-scm.com`, que roda de uma pasta, sem permissão de administrador). Último recurso: enviar os arquivos pela página do GitHub (**Add file → Upload files**) — funciona, mas é trabalhoso |
| **O PowerShell bloqueia a ativação do `.venv`** | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`; ou usar o `cmd` com `.venv\Scripts\activate.bat` |
| **O `pip install` é bloqueado pela rede** | Avise o orientador na **primeira semana**. Sem o `matplotlib`, os gráficos podem ser feitos no Google Planilhas; o Django é indispensável |
| **Atraso na bateria (Sprint 3)** | É o maior risco. As Sprints 4 e 5 podem começar com testes de regras de mentira, mas o experimento (Sprint 6) **não roda** sem a bateria congelada |
| **Vontade de "melhorar" a bateria depois de ver os resultados** | Não pode. Resultados ruins para uma estratégia **são resultados** — e rendem boa discussão |
| **Uma estratégia acerta tudo ou erra tudo** | Provável erro de código. Faça a conferência manual (Tarefa 6.3) e peça ajuda |
| **Tempos muito pequenos (frações de milissegundo)** | É esperado com 100 mensagens e 12 regras. Registre com 3 casas decimais e discuta: para este tamanho de livro, o tempo não é um problema — o que diferencia as estratégias é a qualidade das escolhas |
| **Computador do laboratório formatado** | Por isso o `git push` diário. Tudo se recupera com a Tarefa 8.1 |

---

## Checklist final de entregas

| # | Entrega (conforme a proposta do projeto) | Onde está |
|---|---|---|
| 1 | As cinco estratégias implementadas | `bancada/estrategias.py` |
| 2 | A bateria fixa com 100 mensagens | `dados/bateria.csv` (tag `bateria-congelada`) |
| 3 | O gabarito definido previamente | coluna `regra_esperada` + `docs/protocolo.md` |
| 4 | O mecanismo automatizado de execução | `python manage.py testar_estrategias` |
| 5 | O registro dos resultados de cada estratégia | `resultados/detalhado.csv` (tag `execucao-oficial`) |
| 6 | Tabela comparativa | `resultados/resumo.csv` + TCC |
| 7 | Gráfico(s) | `graficos/*.png` |
| 8 | Análise dos resultados | Diário (Tarefa 7.4) + capítulo de Resultados |
| 9 | Discussão relacionada ao Quarto Chinês | Capítulo de Resultados e Conclusão do TCC |
| 10 | Documentação da implementação e da metodologia | `README.md`, `docs/protocolo.md`, `docs/ambiente.md`, testes e TCC |
