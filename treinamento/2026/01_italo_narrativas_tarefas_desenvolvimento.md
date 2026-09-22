# Plano de tarefas de desenvolvimento – Ítalo e equipe (Técnico Integrado em Informática)

**Projeto pai:** Narrativas – plataforma digital para registro, organização e difusão das narrativas populares do Rio Grande do Norte (ver [projeto.md](../projeto.md)).

**Temática escolhida:** 4.2 – Busca textual no acervo de narrativas (ver [tematicas.md](../tematicas.md)).

**Equipe:** 3 alunos do curso Técnico Integrado em Informática, com conhecimentos básicos em Python, em treinamento.

| Papel | Quem | O que faz |
|---|---|---|
| **Aluno A** | **Ítalo** | É o autor do TCC. Em toda sprint recebe a tarefa mais elaborada, e é quem escreve o texto |
| **Aluno B** | *(preencher)* | Apoio: corpus, carga dos dados, medições, gabarito |
| **Aluno C** | *(preencher)* | Apoio: banco, planos de execução, tabelas e gráficos |

**Duração:** 8 sprints de 1 semana (22/09/2026 a 16/11/2026).

**Onde o trabalho acontece:** o **repositório de treinamento do projeto já existe** e é compartilhado com os outros alunos. Vocês **não vão criar repositório nenhum**. Todo o trabalho dos três fica dentro de **uma única subpasta**:

```
<repositorio-de-treinamento>/
├── ...              ← pastas de outros alunos (não mexam)
└── italo/           ← a subpasta de vocês três: tudo fica aqui dentro
```

A subpasta leva o nome do Ítalo porque é ele quem usa o trabalho como TCC, mas **os três trabalham dentro dela**. Confirmem com o orientador o endereço do repositório antes de começar. Todos os caminhos deste documento são relativos a essa subpasta.

---

## A ideia do trabalho, em uma página

A tela de listagem do portal Narrativas prevê uma **busca por palavra-chave**. Ninguém ainda decidiu como essa busca vai ser feita. Quando alguém começa a programar, a saída natural é escrever algo como `WHERE texto LIKE '%boitatá%'` — e funciona bem com 20 narrativas de teste. O problema aparece depois, quando o acervo cresce: a busca fica lenta e traz resultados ruins.

A pergunta que este trabalho responde é:

> **Qual estratégia de busca textual atende melhor a um acervo de narrativas populares em português, considerando o tempo de resposta e a qualidade dos resultados?**

Para responder, vocês vão comparar **quatro estratégias**, sobre a **mesma base**, com as **mesmas buscas**, no **mesmo computador**:

| Código | Estratégia | Como funciona |
|---|---|---|
| **E1** | `LIKE` sem índice | `SELECT ... WHERE texto LIKE '%termo%'` — é exatamente o que o Django gera quando se usa `icontains` |
| **E2** | `LIKE` com índice | O mesmo, depois de criar um índice na coluna |
| **E3** | **FTS5 do SQLite** | Busca em texto completo, que já vem embutida no Python |
| **E4** | **FULLTEXT do MySQL** | Busca em texto completo do banco que o projeto usa de verdade |

**Use sempre esses códigos** — E1, E2, E3, E4 — no código, nas planilhas, nos gráficos e no texto do TCC. Isso evita confusão e deixa tudo mais fácil de ler.

### Um aviso que já adianta um resultado

O E2 provavelmente **não vai melhorar nada** em relação ao E1. O motivo é que um índice comum de banco de dados não funciona para `LIKE '%termo%'`: como a busca começa com `%`, o banco não tem por onde "entrar" no índice e acaba lendo a tabela inteira de qualquer jeito.

**Isso não é um erro de vocês.** É um dos achados mais interessantes do trabalho, e é justamente o que explica por que existem tecnologias de busca em texto completo. Não tentem "consertar": **meçam, provem com o plano de execução da consulta e expliquem no TCC.**

### O que este trabalho **não** é

Não é "fazer a busca do site Narrativas". A plataforma é o **contexto** que justifica a pergunta. O objeto do TCC é o **experimento comparativo**. Escrevam isso na Introdução — é o que separa um TCC de um manual de programa.

---

## Decisões técnicas já fechadas

Para não perder tempo discutindo ferramenta:

| Item | Decisão |
|---|---|
| Linguagem | **Python 3** |
| Bancos | **SQLite** (módulo `sqlite3`, já vem com o Python) e **MySQL** (já instalado no laboratório) |
| Biblioteca do MySQL | `mysql-connector-python`, instalada com `pip` |
| Gráficos | `matplotlib`, instalada com `pip` |
| Planilhas | módulo `csv`, que já vem com o Python |
| Editor | VS Code |
| Versionamento | Git, na subpasta de vocês dentro do repositório compartilhado |
| O que **não** entra | Docker, Django, API REST, front-end elaborado, Elasticsearch, inteligência artificial, busca semântica — tudo isso vira "trabalho futuro" no TCC |

**Tudo o que precisa ser instalado vem pelo `pip`**, porque as máquinas do laboratório não permitem instalar programas. O SQLite não precisa de instalação (vem com o Python) e o MySQL já está na máquina.

**Uma simplificação honesta, que precisa estar escrita no TCC.** O portal Narrativas usa Django, e o `icontains` do Django gera exatamente a consulta `LIKE` da E1. Por isso o experimento pode ser feito em SQL puro, sem montar um projeto Django inteiro — o que economiza semanas de trabalho sem mudar o resultado. **Registrem essa decisão na Metodologia**, com a justificativa.

---

## Combinados gerais

- **Reunião semanal:** no começo de cada sprint, cada aluno mostra o que fez, **rodando na máquina**. A partir da Sprint 3, é preciso mostrar número.
- **Commits:** cada aluno faz pelo menos 2 por sprint, com mensagem em português dizendo o que foi feito.
- **Travou mais de 40 minutos no mesmo erro? Peça ajuda.**
- **Planilhas de medição:** a partir da Sprint 3, toda medição vai para `resultados/`. **Nunca apaguem uma medição.** Se uma rodada saiu estranha, registrem e anotem o motivo ao lado.
- **Diário:** `docs/diario.md`, três linhas no fim de cada sprint — o que funcionou, o que deu errado, o que aprendemos. Isso vira a Conclusão do TCC.
- **Prints:** capturas de tela em `docs/evidencias/`. Vão para o capítulo de Resultados.

### Convivência em repositório compartilhado

O repositório é usado por outros alunos, e vocês três mexem na **mesma subpasta**. Então:

1. **Só alterem arquivos dentro de `italo/`.** Nunca editem, movam ou apaguem arquivo de outro aluno.
2. **Comecem sempre com `git pull`.** Como vocês três mexem nos mesmos arquivos, isso é ainda mais importante.
3. **Combinem quem mexe em qual arquivo.** A divisão de tarefas deste plano já separa os arquivos por aluno justamente para evitar que dois editem o mesmo ao mesmo tempo.
4. **Comitem só o que é de vocês:** usem `git add italo/`, nunca `git add .`. Confiram com `git status` antes.
5. **Não comitem** os bancos de dados gerados (`.db`), a pasta `.venv/` nem `__pycache__/`.
6. **Deu `CONFLICT`? Parem e chamem o orientador.**
7. **`git push` no fim de cada dia.**

---

# Sprint 1 — 22/09 a 28/09/2026
## Preparar tudo: ambiente, corpus e banco

**Objetivo:** ao final da semana, ter o ambiente funcionando, textos de verdade em mãos e as tabelas criadas nos dois bancos. **Nada de medir ainda.**

### Estrutura de pastas a criar (Ítalo faz isso no primeiro dia)

```
italo/
├── corpus/              ← os textos das narrativas e a planilha de origem
├── scripts/             ← os programas Python, numerados na ordem de execução
├── bancos/              ← os arquivos .db gerados (não vão para o Git)
├── resultados/          ← as planilhas com as medições
│   └── planos/          ← as saídas de EXPLAIN
├── graficos/
├── docs/
│   ├── protocolo.md
│   ├── diario.md
│   ├── ambiente.md
│   └── evidencias/
├── .gitignore
├── requirements.txt
└── README.md
```

### Tarefas da sprint

| Aluno | Tarefa |
|---|---|
| **Ítalo (A)** | Criar a estrutura, preparar o ambiente e **escrever o protocolo do experimento** |
| **B** | Coletar o corpus: 50 a 100 narrativas reais em português |
| **C** | Criar as tabelas nos dois bancos (SQLite e MySQL) |

---

### Passo a passo do Ítalo

**1. Clonar o repositório e criar a subpasta.**

```
git clone <endereço-do-repositório-de-treinamento>
cd <pasta-do-repositório>
mkdir italo
cd italo
```

**2. Ambiente virtual e bibliotecas.**

```
python -m venv .venv
.venv\Scripts\activate
pip install mysql-connector-python matplotlib
pip freeze > requirements.txt
```

**3. O arquivo `italo/.gitignore`:**

```
.venv/
__pycache__/
*.pyc
bancos/
*.db
```

**4. Conferir se o FTS5 existe no Python da máquina.** O FTS5 é a estratégia E3, e ele precisa estar compilado no SQLite que vem com o Python. Normalmente está, mas confiram agora — descobrir isso na Sprint 5 seria péssimo. Crie `scripts/00_verificar_ambiente.py`:

```python
import sqlite3

conexao = sqlite3.connect(":memory:")
print("Versao do SQLite:", sqlite3.sqlite_version)

try:
    conexao.execute("CREATE VIRTUAL TABLE teste USING fts5(conteudo)")
    print("FTS5: DISPONIVEL")
except sqlite3.OperationalError as erro:
    print("FTS5: NAO DISPONIVEL ->", erro)
```

Se aparecer "NÃO DISPONÍVEL", avisem o orientador **nesta semana**.

**5. Testar a conexão com o MySQL.** Peçam ao orientador o usuário e a senha do MySQL do laboratório. Depois criem o banco pelo MySQL Workbench:

```sql
CREATE DATABASE narrativas_tcc CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
```

E testem pelo Python:

```python
import mysql.connector

conexao = mysql.connector.connect(
    host="localhost", user="root", password="SENHA",
    database="narrativas_tcc",
)
print("Conectou:", conexao.is_connected())
```

> **Sobre a senha:** ela **não pode ir para o Git**, porque o repositório é compartilhado. Criem um arquivo `config_local.py` com o usuário e a senha, e acrescentem `config_local.py` ao `.gitignore`. Criem também um `config_local_exemplo.py`, sem a senha de verdade, e comitem esse.

**6. Escrever o protocolo do experimento** (`docs/protocolo.md`). Esta é a tarefa mais importante do Ítalo nesta sprint. O protocolo responde, em uma página, o seguinte:

1. quais são as 4 estratégias (E1 a E4);
2. quais são os 3 volumes de base (100, 1.000 e 10.000 narrativas);
3. quais são as consultas de teste (vocês fecham a lista na Sprint 5, mas já deixem 5 definidas);
4. **quantas medições por consulta**: 3 execuções de aquecimento, que são descartadas, e depois **10 medições válidas**;
5. o que é registrado em cada medição;
6. qual máquina é usada, com processador, memória, tipo de disco e sistema operacional.

**Por que aquecimento e repetições?** Porque a primeira execução de uma consulta é sempre mais lenta (o banco ainda não carregou nada na memória), e porque uma medição sozinha pode sair distorcida se o antivírus resolver rodar naquele instante. Descartar as primeiras e usar a mediana de dez é o mínimo para o número ser confiável.

**Por que mediana e não média?** Porque uma única execução muito lenta puxa a média inteira para cima e dá uma impressão errada. A mediana ignora esse tipo de distorção. **Relatem as duas**, mas usem a mediana nas comparações.

**7. Começar o `docs/ambiente.md`** com a configuração da máquina do laboratório e as versões de Python, SQLite e MySQL.

---

### Passo a passo do Aluno B

**1. Coletar 50 a 100 narrativas reais, em português.** Só textos em **domínio público**. Fontes:

- **Sílvio Romero, *Contos Populares do Brasil* (1883)** — o autor faleceu em 1914, e a obra está em domínio público;
- **Lindolfo Gomes, *Contos Populares Brasileiros* (1918)** — autor falecido em 1953, também em domínio público;
- **Portal Domínio Público** (`dominiopublico.gov.br`), **Projeto Gutenberg** e **Wikisource**.

> **Cuidado importante:** as obras de **Luís da Câmara Cascudo** ainda **não** estão em domínio público — ele faleceu em 1986, e pela Lei nº 9.610/1998 a proteção dura 70 anos após a morte do autor. Não copiem textos dele para o corpus. Citá-lo como autor no Referencial Teórico é não só permitido como recomendável.

**2. Salvar cada narrativa** em `corpus/narrativa_001.txt`, `narrativa_002.txt`, e assim por diante, sempre em **UTF-8**.

Limpem antes de salvar: tirem números de página, notas de rodapé e cabeçalhos que vieram na cópia; juntem as quebras de linha no meio das frases (texto copiado de PDF vem cheio delas); confiram a acentuação, porque textos digitalizados antigos costumam trazer erros.

**3. Preencher `corpus/origem.csv`**, com uma linha por narrativa:

```
arquivo,titulo,obra,autor,ano,endereco,licenca,data_coleta,caracteres
narrativa_001.txt,...,Contos Populares do Brasil,Silvio Romero,1883,...,dominio publico,2026-09-25,3120
```

**Essa planilha é o que sustenta a Metodologia do TCC.** Sem ela, não há como provar que vocês usaram material que podiam usar.

---

### Passo a passo do Aluno C

**1. Desenhar o modelo de dados.** Quatro tabelas, espelhando o que a plataforma já tem:

```
narrativa       (id, titulo, texto, tipo_id, publico_id, cidade_id, data_cadastro)
narrativa_tipo  (id, nome)
narrativa_publico (id, nome)
cidade          (id, nome, uf)
```

Façam um diagrama simples (pode ser no draw.io, que é gratuito e roda no navegador). Ele vai para o capítulo de Resultados do TCC.

**2. Criar `scripts/01_criar_tabelas_sqlite.py`:**

```python
import sqlite3

SQL = """
CREATE TABLE IF NOT EXISTS narrativa (
    id INTEGER PRIMARY KEY,
    titulo TEXT NOT NULL,
    texto TEXT NOT NULL,
    tipo_id INTEGER,
    publico_id INTEGER,
    cidade_id INTEGER,
    data_cadastro TEXT
);
"""

conexao = sqlite3.connect("bancos/narrativas_100.db")
conexao.executescript(SQL)
conexao.commit()
print("Tabelas criadas.")
```

**3. Criar `scripts/01_criar_tabelas_mysql.py`**, com **exatamente o mesmo modelo**. No MySQL, o tipo da coluna de texto precisa ser `LONGTEXT` (um `VARCHAR` não comporta uma narrativa inteira):

```sql
CREATE TABLE IF NOT EXISTS narrativa (
    id INT PRIMARY KEY,
    titulo VARCHAR(255) NOT NULL,
    texto LONGTEXT NOT NULL,
    tipo_id INT,
    publico_id INT,
    cidade_id INT,
    data_cadastro DATE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

> **Atenção:** os dois bancos precisam ter **o mesmo modelo**. Se as tabelas forem diferentes, a comparação entre SQLite e MySQL perde o sentido. Confiram um ao lado do outro antes de fechar a sprint.

**4. Anotar a collation usada no MySQL.** A collation é o que decide se o banco considera "boitatá" igual a "boitata" e se "SERTÃO" é igual a "sertão". A `utf8mb4_0900_ai_ci` ignora acento e maiúscula; a `utf8mb4_0900_as_cs` não ignora. **Escolham uma, anotem em `docs/ambiente.md` e não mudem mais** — isso afeta diretamente os resultados da Sprint 6.

### Como saber que a Sprint 1 deu certo

- [ ] Subpasta `italo/` criada, com a estrutura de pastas.
- [ ] `python scripts/00_verificar_ambiente.py` mostra que o FTS5 está disponível.
- [ ] Conexão com o MySQL funcionando pelo Python.
- [ ] `docs/protocolo.md` escrito.
- [ ] 50 a 100 arquivos `.txt` em `corpus/`, em UTF-8, com `origem.csv` preenchido.
- [ ] Tabelas criadas nos dois bancos, com o mesmo modelo.
- [ ] `config_local.py` **fora** do Git.

### Erros comuns

- **Acentos quebrados (`Mossor├│`):** o arquivo não foi salvo em UTF-8. No VS Code, clique na codificação no canto inferior direito e escolha "Salvar com codificação → UTF-8".
- **`Access denied` no MySQL:** usuário ou senha errados. Confirmem com o orientador.
- **`ModuleNotFoundError: mysql`:** o ambiente virtual não está ativo. Olhem se aparece `(.venv)` no início da linha do terminal.

---

# Sprint 2 — 29/09 a 05/10/2026
## Gerar as três bases de teste e carregar nos dois bancos

**Objetivo:** ter seis bancos prontos — 100, 1.000 e 10.000 narrativas, em SQLite e em MySQL.

### Tarefas da sprint

| Aluno | Tarefa |
|---|---|
| **Ítalo (A)** | Escrever o gerador das bases (`scripts/02_gerar_base.py`) |
| **B** | Carregar os dados nos dois bancos (`scripts/03_carregar.py`) |
| **C** | Caracterizar a base: tabela e gráfico com o perfil dos textos |

---

### Passo a passo do Ítalo

**1. O problema a resolver.** Vocês têm 50 a 100 narrativas reais, mas precisam de bases de 100, 1.000 e 10.000. Copiar o mesmo texto mil vezes **invalidaria a medição**: o banco e o índice se comportam de forma completamente diferente quando todos os textos são iguais.

**A solução:** gerar narrativas novas **recombinando parágrafos** das narrativas reais. Cada narrativa gerada pega parágrafos sorteados de textos diferentes. O resultado é um texto que tem vocabulário, tamanho e estrutura de português real, mas que não se repete.

**2. Como fazer:**

```python
import random
import hashlib

random.seed(42)      # faz o sorteio sair sempre igual

def carregar_paragrafos(pasta_corpus):
    """Le todos os .txt e devolve uma lista com todos os paragrafos."""
    paragrafos = []
    # para cada arquivo: abrir com encoding="utf-8", separar por "\n\n",
    # e guardar so os paragrafos com mais de 200 caracteres
    return paragrafos


def gerar_narrativa(paragrafos):
    """Monta uma narrativa nova sorteando de 4 a 10 paragrafos."""
    quantidade = random.randint(4, 10)
    escolhidos = random.sample(paragrafos, quantidade)
    return "\n\n".join(escolhidos)
```

**3. A semente aleatória (`random.seed(42)`) é obrigatória.** Ela faz o programa gerar **sempre as mesmas bases**. Sem isso, o colega que rodar o script vai obter outra base, e os números do TCC não poderão ser conferidos por ninguém. Escrevam sobre isso na Metodologia.

**4. Controlem o tamanho.** Cada narrativa gerada deve ter entre **2.000 e 8.000 caracteres**, que é o tamanho de uma narrativa real. Textos curtos demais não estressam a busca; longos demais deixam a carga lenta sem necessidade.

**5. Provem que não há textos repetidos.** Isso é uma exigência metodológica, e é fácil de fazer: calculem o código SHA-256 de cada texto gerado e contem quantos são distintos.

```python
def assinatura(texto):
    return hashlib.sha256(texto.encode("utf-8")).hexdigest()

# ao final:
print(f"Narrativas geradas: {len(textos)}")
print(f"Textos distintos:   {len(set(assinatura(t) for t in textos))}")
```

Os dois números têm de ser iguais. **Guardem essa saída** — ela vira uma frase no capítulo de Resultados.

**6. Variem também os outros campos.** Sorteiem o tipo, o público e a cidade de cada narrativa. Para as cidades, usem uma lista de municípios do Rio Grande do Norte (ou do Brasil, se quiserem mais variedade). Título: monte combinando palavras dos próprios textos, ou use o padrão "A lenda de ..." com um substantivo sorteado.

**7. O script deve aceitar o volume como parâmetro:**

```
python scripts/02_gerar_base.py --volume 100
python scripts/02_gerar_base.py --volume 1000
python scripts/02_gerar_base.py --volume 10000
```

Pesquisem sobre o módulo `argparse`, que já vem com o Python e resolve isso em cinco linhas.

---

### Passo a passo do Aluno B

**1. Escrever `scripts/03_carregar.py`**, que lê as narrativas geradas e grava nos dois bancos.

**2. Cuidado com a codificação — este é o erro mais comum do trabalho.** Abram os arquivos sempre com `encoding="utf-8"`. No MySQL, o `utf8mb4` precisa estar em três lugares: na conexão, na tabela e na coluna. Se um deles estiver errado, os acentos viram lixo e vocês só vão descobrir na hora de medir.

```python
conexao = mysql.connector.connect(
    host="localhost", user="root", password=SENHA,
    database="narrativas_tcc", charset="utf8mb4",
)
```

**3. Carreguem em lote, não um por um.** Inserir 10.000 registros com um `INSERT` por vez demora muito. Usem `executemany` e uma transação só:

```python
sql = "INSERT INTO narrativa (id, titulo, texto, tipo_id, publico_id, cidade_id, data_cadastro) VALUES (?, ?, ?, ?, ?, ?, ?)"
cursor.executemany(sql, lista_de_tuplas)
conexao.commit()
```

> No MySQL, o marcador de parâmetro é `%s` em vez de `?`. É a única diferença relevante entre os dois nesta parte.

**4. Cronometrem a carga** e anotem o tempo de cada volume em cada banco. É um dado a mais para os Resultados, e custa uma linha de código:

```python
import time
inicio = time.perf_counter()
# ... carga ...
print(f"Carga levou {time.perf_counter() - inicio:.2f} segundos")
```

**5. Confiram depois de carregar.** Rodem `SELECT COUNT(*) FROM narrativa;` nos dois bancos e vejam se bate com o volume esperado. Abram o MySQL Workbench e olhem uma narrativa: os acentos estão certos?

---

### Passo a passo do Aluno C

**1. Caracterizar a base.** Monte uma tabela com:

| Volume | Narrativas | Total de palavras | Média de caracteres | Mediana de caracteres | Cidades distintas |
|---|---|---|---|---|---|

**2. Um gráfico da distribuição do tamanho dos textos** (histograma), com `matplotlib`. Isso mostra que a base não é artificial demais — todos os textos com exatamente o mesmo tamanho seria sinal de base mal gerada.

**3. A lista das 30 palavras mais frequentes**, depois de remover as palavras vazias ("de", "a", "o", "que", "e", "um", "para"...). Use `collections.Counter`, que resolve isso em poucas linhas. Essa lista ajuda a escolher as consultas de teste da Sprint 5: não adianta buscar por uma palavra que não existe na base.

### Como saber que a Sprint 2 deu certo

- [ ] Seis bancos carregados (3 volumes × 2 bancos).
- [ ] Nenhum texto repetido — comprovado pela contagem de SHA-256.
- [ ] Acentos corretos nos dois bancos (confiram olhando um registro).
- [ ] Tempo de carga anotado.
- [ ] Tabela de caracterização e histograma prontos.

### Erros comuns

- **`random.sample` dá erro:** a lista de parágrafos tem menos itens do que a quantidade pedida. Confiram quantos parágrafos foram carregados.
- **A carga do volume 10.000 demora muito:** vocês estão inserindo um por um. Usem `executemany`.
- **Acentos virando `?` no MySQL:** faltou `charset="utf8mb4"` na conexão.

---

# Sprint 3 — 06/10 a 12/10/2026
## Medir as estratégias E1 e E2

**Objetivo:** os primeiros números na mão.

> **Atenção:** 12/10 é feriado e cai no último dia desta sprint. Planejem-se.

### Tarefas da sprint

| Aluno | Tarefa |
|---|---|
| **Ítalo (A)** | Escrever o programa de medição (`scripts/04_medir.py`) — o coração do trabalho |
| **B** | Implementar e medir a E1 (`LIKE` sem índice) |
| **C** | Implementar e medir a E2 (`LIKE` com índice) e capturar os planos de execução |

---

### Passo a passo do Ítalo

**1. O programa de medição** é o que vai ser usado até o fim do trabalho. Ele percorre, em laços encaixados:

```
para cada volume (100, 1.000, 10.000):
    para cada estratégia (E1, E2, E3, E4):
        para cada consulta da lista:
            3 execuções de aquecimento (descartadas)
            10 medições válidas, gravando uma linha por medição
```

**2. Grave uma linha por medição**, não só a média. A análise vem depois, e dados detalhados permitem conferir e refazer. O arquivo `resultados/tempos.csv` tem estas colunas:

```
data,maquina,banco,volume,estrategia,consulta,repeticao,tempo_ms,qtd_resultados
```

**3. Como cronometrar:**

```python
import time

inicio = time.perf_counter()
resultados = buscar(conexao, termo)
tempo_ms = (time.perf_counter() - inicio) * 1000
```

Usem `time.perf_counter()`, nunca `time.time()` — o primeiro é bem mais preciso para medir durações curtas.

**4. Uma armadilha que arruinaria o trabalho inteiro.** Em Python, executar uma consulta **não** significa que o banco fez o trabalho. Se vocês só chamarem `cursor.execute(...)` e não lerem o resultado, alguns bancos entregam as linhas aos poucos, e o tempo medido fica falso — pequeno demais.

**Sempre percorram o resultado até o fim:**

```python
def buscar(conexao, termo):
    cursor = conexao.cursor()
    cursor.execute(SQL, (f"%{termo}%", f"%{termo}%"))
    linhas = cursor.fetchall()          # <- isto e obrigatorio
    return [linha[0] for linha in linhas]
```

**5. Organizem com uma função por estratégia, todas com a mesma "cara":**

```python
def buscar_e1(conexao, termo): ...
def buscar_e2(conexao, termo): ...
def buscar_e3(conexao, termo): ...
def buscar_e4(conexao, termo): ...
```

Todas recebem os mesmos parâmetros e devolvem a mesma coisa: uma lista de `id` de narrativas. Assim o programa de medição trata as quatro do mesmo jeito, e acrescentar a E3 e a E4 nas próximas sprints vira uma linha de código.

---

### Passo a passo do Aluno B

**1. A estratégia E1** é a busca mais simples que existe:

```python
SQL_E1 = "SELECT id FROM narrativa WHERE titulo LIKE ? OR texto LIKE ?"

def buscar_e1(conexao, termo):
    cursor = conexao.cursor()
    padrao = f"%{termo}%"
    cursor.execute(SQL_E1, (padrao, padrao))
    return [linha[0] for linha in cursor.fetchall()]
```

**2. Sempre com consulta parametrizada.** Reparem que o termo entra como parâmetro (`?`), e não colado dentro do texto do SQL. **Nunca** escrevam algo como:

```python
# NAO FACAM ISSO
cursor.execute(f"SELECT id FROM narrativa WHERE texto LIKE '%{termo}%'")
```

Isso se chama vulnerabilidade de **injeção de SQL**, e é uma das falhas de segurança mais conhecidas que existem. Pesquisem sobre o assunto: rende um parágrafo no Referencial Teórico e mostra cuidado técnico.

**3. Meçam nos três volumes** e observem como o tempo cresce. Anotem a impressão no diário — vocês vão ver o tempo crescer de forma proporcional ao tamanho da base, porque o banco lê tudo.

---

### Passo a passo do Aluno C

**1. A estratégia E2** é a E1 depois de criar um índice:

```sql
CREATE INDEX idx_narrativa_texto ON narrativa(texto);
```

No MySQL, indexar uma coluna `LONGTEXT` exige informar um tamanho de prefixo:

```sql
CREATE INDEX idx_narrativa_texto ON narrativa(texto(255));
```

**2. Meçam de novo, nos três volumes.** O tempo provavelmente não vai melhorar — e está tudo certo. Não mexam em nada para "consertar".

**3. Capturem a prova.** Esta é a parte mais importante da sua tarefa: mostrar **por que** o índice não ajudou.

No SQLite:

```sql
EXPLAIN QUERY PLAN SELECT id FROM narrativa WHERE texto LIKE '%boitata%';
```

No MySQL (ou pelo Workbench, que mostra o plano em forma de diagrama):

```sql
EXPLAIN SELECT id FROM narrativa WHERE texto LIKE '%boitata%';
```

Procurem na saída por `SCAN` (SQLite) ou por `type: ALL` (MySQL): significa que o banco leu a tabela inteira, sem usar índice.

**4. Agora faça o contraste, que é o que fecha o argumento.** Rodem o mesmo `EXPLAIN` com a busca por **prefixo**, sem o `%` no começo:

```sql
EXPLAIN QUERY PLAN SELECT id FROM narrativa WHERE texto LIKE 'boitata%';
```

Aqui o índice **é** usado. Comparar os dois planos lado a lado prova o argumento: o problema não é o índice, é o `%` no começo da busca, que impede o banco de usar o índice.

**5. Salvem todas as saídas** em `resultados/planos/`, com nomes claros (`e1_sqlite_10000.txt`, `e2_prefixo_mysql_10000.txt`). Tirem print também — vão para o TCC.

**6. Anotem o tamanho do banco em disco** antes e depois de criar o índice. Índice ocupa espaço, e mostrar isso é um resultado.

### Como saber que a Sprint 3 deu certo

- [ ] `resultados/tempos.csv` com as medições de E1 e E2, nos três volumes, nos dois bancos.
- [ ] Planos de execução salvos, com e sem índice, e com busca por prefixo para contraste.
- [ ] Tamanho do banco anotado antes e depois do índice.
- [ ] Os três conseguem explicar, em voz alta, por que o índice não ajudou.

### Erros comuns

- **Tempos absurdamente baixos (menos de 1 ms em 10.000 narrativas):** faltou o `fetchall()`. A consulta não chegou a ser executada de verdade.
- **Tempos muito diferentes entre repetições:** tem outro programa pesado aberto. Fechem tudo e refaçam.

---

# Sprint 4 — 13/10 a 19/10/2026
## Estratégia E3: busca em texto completo do SQLite (FTS5)

**Objetivo:** ver a diferença que uma tecnologia de busca de verdade faz.

### Tarefas da sprint

| Aluno | Tarefa |
|---|---|
| **Ítalo (A)** | Implementar a E3 com FTS5 e medir |
| **B** | Medir o custo do índice FTS (tempo de construção e espaço em disco) |
| **C** | Montar a matriz de acentos, maiúsculas e plurais |

---

### Passo a passo do Ítalo

**1. O que é o FTS5.** É um recurso do próprio SQLite para busca em texto completo. Em vez de ler todos os textos procurando o termo, ele monta antes um **índice invertido**: uma lista que diz, para cada palavra, em quais narrativas ela aparece. Buscar vira consultar essa lista — muito mais rápido.

**2. Criar a tabela de busca:**

```python
SQL_FTS = """
CREATE VIRTUAL TABLE narrativa_fts USING fts5(
    titulo,
    texto,
    tokenize = "unicode61 remove_diacritics 2"
);
"""
```

O `remove_diacritics 2` é o que faz a busca por "boitata" encontrar "boitatá". **É o parâmetro mais importante desta sprint.**

**3. Preencher a tabela**, usando o `id` da narrativa como identificador:

```python
conexao.execute(
    "INSERT INTO narrativa_fts(rowid, titulo, texto) "
    "SELECT id, titulo, texto FROM narrativa"
)
conexao.commit()
```

**4. A busca:**

```python
SQL_E3 = """
SELECT rowid
FROM narrativa_fts
WHERE narrativa_fts MATCH ?
ORDER BY bm25(narrativa_fts)
"""
```

O `bm25()` é uma fórmula que ordena os resultados por **relevância**: uma narrativa em que o termo aparece cinco vezes vem antes de outra em que aparece uma vez. Nenhuma das outras três estratégias faz isso — no `LIKE`, os resultados saem em qualquer ordem. **Esse é um ponto forte da E3 e precisa estar no TCC.**

**5. Testem com e sem o `remove_diacritics 2`.** Criem as duas versões da tabela e vejam o que acontece ao buscar "boitata" (sem acento) em textos que escrevem "boitatá" (com acento). **A diferença entre as duas é um resultado do trabalho**, não um detalhe de configuração.

**6. Uma simplificação que vocês precisam declarar no TCC.** Do jeito que está acima, a tabela FTS guarda uma **cópia** do texto — o banco fica com o texto duas vezes. Existe uma forma de evitar isso (a opção `content=`, com gatilhos que mantêm a cópia sincronizada), mas ela é mais complicada e não muda o tempo de busca, que é o que vocês estão medindo.

A decisão: **usem a forma simples**, meçam o espaço em disco que ela custa (tarefa do Aluno B) e escrevam no TCC que a versão sem duplicação existe e fica como trabalho futuro. Limitação declarada não tira valor do trabalho — esconder, sim.

---

### Passo a passo do Aluno B

**1. Quanto custa essa velocidade?** É a pergunta que o orientador e a banca vão fazer. Meçam três coisas:

- **tempo para construir a tabela FTS** em cada volume;
- **tamanho do banco em disco** com e sem a tabela FTS, em MB e em porcentagem de crescimento;
- **tempo para inserir uma narrativa nova** com a tabela FTS existindo, comparado com o tempo sem ela.

**2. Por que a última medida importa:** um índice de busca acelera a leitura e atrasa a escrita. No portal Narrativas, quem cadastra uma narrativa vai sentir esse atraso. Saber o tamanho dele é informação útil de verdade para a equipe.

**3. Montem a tabela:**

| Volume | Banco sem FTS (MB) | Banco com FTS (MB) | Crescimento (%) | Tempo de construção (s) |
|---|---|---|---|---|

---

### Passo a passo do Aluno C

**1. A matriz de robustez do português.** Esta é uma das tabelas mais interessantes do TCC. A pergunta é: cada estratégia encontra a narrativa quando a pessoa digita de um jeito diferente do que está escrito no texto?

Monte uma tabela com os casos de teste nas linhas e as estratégias nas colunas, marcando ✓ ou ✗:

| Busca digitada | E1 | E2 | E3 |
|---|---|---|---|
| `boitatá` (igual ao texto) | | | |
| `boitata` (sem acento) | | | |
| `BOITATÁ` (maiúsculas) | | | |
| `Boitatá` (inicial maiúscula) | | | |
| `boitatás` (plural) | | | |

Repitam com outros termos: `sertão`/`sertao`, `lobisomem`/`lobisomens`, `assombração`/`assombracao`.

**2. Duas descobertas esperadas — registrem as duas:**

- o `LIKE` do **SQLite** só ignora maiúsculas e minúsculas em letras do alfabeto inglês. Ou seja, ele acha `BOITATA` buscando `boitata`, mas **não** acha `SERTÃO` buscando `sertão`, porque o `Ã` não está no alfabeto inglês. No **MySQL**, isso depende da collation escolhida na Sprint 1 — por isso ela tinha de ser anotada;
- **nenhuma das estratégias trata plural em português.** O FTS5 tem um tratamento de plural chamado `porter`, mas ele foi feito para o inglês e não funciona para o português. Testem e comprovem.

**3. Essas duas limitações não são falhas do trabalho — são o resultado dele.** Elas mostram exatamente onde cada tecnologia para, e é isso que a equipe do Narrativas precisa saber antes de escolher.

### Como saber que a Sprint 4 deu certo

- [ ] E3 funcionando e medida nos três volumes.
- [ ] Comparação entre FTS5 com e sem `remove_diacritics` feita.
- [ ] Tabela de custo do índice FTS pronta.
- [ ] Matriz de acentos, maiúsculas e plurais preenchida.

### Erros comuns

- **`no such table: narrativa_fts`:** a tabela virtual foi criada em um banco e a busca está rodando em outro. Confiram o caminho do arquivo `.db`.
- **`MATCH` dando erro de sintaxe:** o FTS5 tem uma linguagem própria de consulta, e caracteres como `-` e `"` têm significado especial. Para buscar um termo literal, coloquem entre aspas duplas dentro da consulta.

---

# Sprint 5 — 20/10 a 26/10/2026
## Estratégia E4 (MySQL) e o gabarito de relevância

**Objetivo:** fechar as quatro estratégias e definir como medir a **qualidade** dos resultados, e não só a velocidade.

### Tarefas da sprint

| Aluno | Tarefa |
|---|---|
| **Ítalo (A)** | Implementar a E4 com FULLTEXT do MySQL e medir |
| **B** | Fechar a lista de consultas de teste e montar o gabarito |
| **C** | Julgar os resultados junto com o B e anotar a concordância |

---

### Passo a passo do Ítalo

**1. Criar o índice FULLTEXT:**

```sql
ALTER TABLE narrativa ADD FULLTEXT KEY ft_narrativa (titulo, texto);
```

**2. A busca:**

```python
SQL_E4 = """
SELECT id, MATCH(titulo, texto) AGAINST (%s IN NATURAL LANGUAGE MODE) AS relevancia
FROM narrativa
WHERE MATCH(titulo, texto) AGAINST (%s IN NATURAL LANGUAGE MODE)
ORDER BY relevancia DESC
"""
```

Assim como a E3, a E4 ordena por relevância — o que a E1 e a E2 não fazem.

**3. Três armadilhas do MySQL que precisam ser documentadas no TCC.** Descobrir e explicar cada uma vale um parágrafo nos Resultados:

- **palavras curtas são ignoradas.** O MySQL, por padrão, não indexa palavras com menos de 4 caracteres (`innodb_ft_min_token_size` = 3, e o mínimo é maior que isso). Testem buscar por "sol" ou "céu" e vejam o que acontece. Mudar essa configuração exige reconstruir o índice;
- **a lista de palavras ignoradas é em inglês.** O MySQL vem com uma lista de palavras vazias ("the", "and", "of"...) que não são indexadas — mas é em inglês. Então "de", "que" e "para" **entram** no índice em português, ocupando espaço sem servir para nada. Dá para trocar a lista, e vale mencionar isso como possibilidade;
- **acento e maiúscula dependem da collation**, que vocês anotaram na Sprint 1. Testem e confirmem o comportamento real, em vez de supor.

**4. Meçam nos três volumes**, com o mesmo programa e na mesma máquina.

**5. Um cuidado que pode invalidar a comparação:** o MySQL precisa estar rodando **na mesma máquina** onde vocês rodam o script. Se ele estiver em um servidor da rede, o tempo medido inclui o tempo de rede, e comparar com o SQLite (que é um arquivo local) deixa de fazer sentido. Confirmem isso com o orientador e **anotem no TCC**.

**6. Acrescentem a E4 à matriz de robustez** da Sprint 4, completando a tabela com a quarta coluna.

---

### Passo a passo do Aluno B

**1. Fechar a lista de consultas de teste.** Entre **10 e 12 consultas**, misturando situações diferentes:

| Tipo | Exemplo |
|---|---|
| Termo simples | `lobisomem` |
| Termo com acento | `boitatá` |
| O mesmo sem acento | `boitata` |
| Plural | `assombrações` |
| Termo comum na base | (use a lista de palavras frequentes da Sprint 2) |
| Termo genérico | `festa` |
| Termo que não existe na base | `helicóptero` |

O último caso é importante: serve para testar o que cada estratégia faz quando não há resultado nenhum.

**Salvem em `docs/consultas.csv`** e não mudem mais a lista depois de começar a medir.

**2. O que é o gabarito de relevância.** Medir velocidade é fácil. Medir **qualidade** exige saber, de antemão, quais narrativas *deveriam* aparecer em cada busca. Esse "deveria" é o gabarito, e são vocês que o constroem, olhando os textos.

**3. Como montar, de um jeito viável.** Julgar 10.000 narrativas à mão é impossível. Façam assim (é a técnica padrão da área, chamada de *pooling*):

1. rodem as 4 estratégias para cada consulta e peguem os **20 primeiros resultados** de cada uma;
2. juntem tudo em uma lista única, **sem repetir** e **sem dizer de qual estratégia veio cada item**;
3. **embaralhem** a lista;
4. B e C leem cada narrativa da lista, **separadamente**, e marcam 1 (é relevante para a busca) ou 0 (não é);
5. onde os dois discordarem, o Ítalo desempata.

**4. Por que embaralhar e não identificar a origem:** para que quem julga não seja influenciado por saber qual tecnologia trouxe aquele resultado. Isso se chama avaliação cega, e declarar que vocês fizeram assim aumenta a credibilidade do trabalho.

**5. Salvem em `docs/gabarito.csv`:**

```
consulta,narrativa_id,relevante_b,relevante_c,relevante_final
```

---

### Passo a passo do Aluno C

**1. Julgar a lista**, em paralelo com o B e **sem consultar o colega**. Combinem antes o critério do que conta como relevante, e anotem esse critério — por exemplo: "a narrativa é relevante se o tema da busca aparece na história, e não apenas se a palavra aparece uma vez de passagem".

**2. Calculem a taxa de concordância:** em quantos por cento dos casos vocês dois deram a mesma nota. Esse número vai para o TCC — é um indicador de qualidade do gabarito. Concordância baixa significa que o critério estava mal definido, e vale refazer.

**3. Anotem quantos itens precisaram de desempate** e em que tipo de consulta a discordância se concentrou. Costuma ser nas consultas genéricas, e isso é interessante de comentar.

### Como saber que a Sprint 5 deu certo

- [ ] E4 funcionando e medida nos três volumes.
- [ ] As três armadilhas do MySQL testadas e documentadas.
- [ ] `docs/consultas.csv` fechado, com 10 a 12 consultas.
- [ ] `docs/gabarito.csv` preenchido, julgado por duas pessoas separadamente.
- [ ] Taxa de concordância calculada.
- [ ] Matriz de robustez completa, com as quatro estratégias.

---

# Sprint 6 — 27/10 a 02/11/2026
## Calcular a qualidade e montar tabelas e gráficos

**Objetivo:** transformar as planilhas em resultados apresentáveis.

> **Atenção:** 02/11 é feriado e cai no último dia desta sprint.

### Tarefas da sprint

| Aluno | Tarefa |
|---|---|
| **Ítalo (A)** | Calcular as métricas de qualidade |
| **B** | Consolidar as tabelas de tempo |
| **C** | Produzir os gráficos |

---

### Passo a passo do Ítalo

**1. As três métricas de qualidade.** Cruzando o que cada estratégia devolveu com o gabarito:

| Métrica | O que responde | Como calcular |
|---|---|---|
| **Precisão** | Do que a busca trouxe, quanto prestava? | relevantes trazidos ÷ total trazido |
| **Revocação** | Do que prestava, quanto a busca trouxe? | relevantes trazidos ÷ total de relevantes |
| **P@10** | Dos 10 primeiros resultados, quantos prestavam? | relevantes entre os 10 primeiros ÷ 10 |

**2. Por que o P@10 importa mais do que parece:** ninguém olha a página 5 de uma busca. O que decide se a busca é boa, na prática, é o que aparece nos primeiros resultados. E essa métrica só faz sentido para a E3 e a E4, que ordenam por relevância — a E1 e a E2 devolvem em ordem qualquer. **Comentem isso no TCC**, porque é uma diferença importante entre as estratégias.

**3. Uma ressalva obrigatória sobre a revocação.** Como o gabarito foi montado só com os resultados que as estratégias trouxeram (o *pooling* da Sprint 5), pode haver narrativas relevantes que nenhuma estratégia encontrou e que, por isso, não estão no gabarito. Então a revocação é **relativa ao conjunto julgado**, e não absoluta.

Isso é padrão na área e não é problema — **desde que seja declarado**. Escrevam essa frase na Metodologia.

**4. Gerem `resultados/qualidade.csv`** e a tabela consolidada com a média por estratégia.

---

### Passo a passo do Aluno B

**1. Consolidar os tempos.** Para cada estratégia e cada volume, a partir de `resultados/tempos.csv`:

| Estratégia | Volume | Mediana (ms) | Média (ms) | Desvio padrão | Mínimo | Máximo | Nº de medições |
|---|---|---|---|---|---|---|---|

Usem o módulo `statistics`, que já vem com o Python: `statistics.median`, `statistics.mean`, `statistics.stdev`.

**2. Calculem o fator de crescimento**, que é o número mais importante desta tabela: quantas vezes o tempo aumentou de 100 para 1.000 narrativas, e de 1.000 para 10.000.

É esse número que mostra se a estratégia **escala**. Se o tempo multiplica por 10 quando a base multiplica por 10, a estratégia cresce junto com a base — ruim. Se o tempo quase não muda, a estratégia aguenta o crescimento do acervo — bom.

**3. Formatem as tabelas já no padrão ABNT** das [orientações gerais](../../../README.md#como-incluir-tabelas): identificação em cima, centralizada, fonte embaixo, vírgula como separador decimal e o mesmo número de casas decimais na coluna inteira.

---

### Passo a passo do Aluno C

**1. Quatro gráficos, com `matplotlib`:**

1. **tempo mediano × volume**, uma linha por estratégia. **Usem escala logarítmica no eixo vertical** (`plt.yscale("log")`) — sem isso, a E1 fica tão alta que esmaga as outras três no gráfico e ele não comunica nada. Avisem na legenda que a escala é logarítmica;
2. **barras com a precisão e a revocação** de cada estratégia;
3. **barras com o tamanho do banco em disco** por estratégia, mostrando o custo de cada índice;
4. **histograma ou boxplot das 10 medições** de uma consulta, para mostrar a dispersão.

**2. Regras para todos os gráficos:**

- eixos com nome e **unidade** (ms, MB, %);
- legenda identificando as estratégias, sempre com a mesma cor para a mesma estratégia em todos os gráficos;
- **sem título dentro da imagem** — na ABNT, o título vai na identificação acima da figura;
- salvem em `graficos/`, em PNG, com boa resolução (`plt.savefig(caminho, dpi=150)`).

### Como saber que a Sprint 6 deu certo

- [ ] `resultados/qualidade.csv` com precisão, revocação e P@10.
- [ ] Tabela de tempos consolidada, com mediana e fator de crescimento.
- [ ] Quatro gráficos prontos, no padrão combinado.
- [ ] Todas as tabelas já formatadas no padrão ABNT.

---

# Sprint 7 — 03/11 a 09/11/2026
## Protótipo, README e repetição em outra máquina

**Objetivo:** mostrar a estratégia vencedora funcionando e provar que o experimento se repete.

### Tarefas da sprint

| Aluno | Tarefa |
|---|---|
| **Ítalo (A)** | Construir o protótipo de busca |
| **B** | Escrever o README de reprodução |
| **C** | Repetir o experimento em outro computador do laboratório |

---

### Passo a passo do Ítalo

**1. Um protótipo simples, de linha de comando** (`scripts/09_prototipo.py`), usando a estratégia que venceu. Ele recebe um termo, faz a busca e mostra:

- quantos resultados encontrou;
- o tempo que a consulta levou;
- os 10 primeiros, ordenados por relevância, com o título e um **trecho do texto em volta do termo encontrado**.

```
> boitata

Encontrados 37 resultados em 4,2 ms

 1. A lenda da cobra de fogo
    "...contam que a boitata aparece nas noites escuras do sertao..."
 2. ...
```

**2. Para o trecho destacado**, o FTS5 tem uma função pronta chamada `snippet()`. Pesquisem na documentação: ela devolve o pedaço do texto em volta do termo, com marcadores em volta da palavra encontrada. É um detalhe pequeno que deixa o protótipo muito mais convincente na apresentação.

**3. O protótipo é ilustração, não é o trabalho.** Uma tela e meia página no TCC bastam. Não gastem tempo com interface bonita nem com Flask — o valor do trabalho está nas medições.

---

### Passo a passo do Aluno B

**1. O `README.md` da subpasta** precisa permitir que outra pessoa repita tudo. Deve conter:

- o que é o trabalho e a que projeto pertence;
- pré-requisitos: Python (com a versão), MySQL (com a versão), e `pip install -r requirements.txt`;
- como configurar o `config_local.py` a partir do arquivo de exemplo;
- **a ordem dos scripts**, numerada, com uma linha explicando o que cada um faz e quanto tempo demora;
- quanto espaço em disco é preciso;
- de onde veio o corpus e qual a situação de direitos autorais;
- a configuração da máquina onde as medições foram feitas: processador, memória, tipo de disco, sistema operacional.

**Sem essa última informação, os tempos medidos não significam nada.** É a primeira coisa que um avaliador procura em trabalho de desempenho.

---

### Passo a passo do Aluno C

**1. Rodem o experimento completo em outro computador do laboratório**, com o mesmo procedimento. Isso é mais simples do que parece: é clonar o repositório, instalar as bibliotecas, gerar as bases e rodar o script de medição.

**2. Comparem os dois computadores:**

- as estratégias mantiveram a **mesma ordem** de desempenho?
- de quanto foi a diferença percentual dos tempos?

**3. Por que isso vale a pena:** se a ordem se manteve, vocês podem afirmar no TCC que a conclusão **não depende do computador usado**. É um tipo de verificação raro em trabalho de conclusão de curso e que impressiona positivamente a banca. Se a ordem mudou, é ainda mais importante investigar e relatar.

### Como saber que a Sprint 7 deu certo

- [ ] Protótipo funcionando, com trecho destacado e tempo na tela.
- [ ] `README.md` permite que outra pessoa repita o trabalho.
- [ ] Experimento repetido em outra máquina, com a comparação anotada.
- [ ] Print do protótipo em `docs/evidencias/`.

---

# Sprint 8 — 10/11 a 16/11/2026
## Recomendação final e fechamento

**Objetivo:** transformar os números em uma resposta para a equipe do Narrativas.

> **Atenção:** 15/11 é feriado e cai nesta sprint.

### Tarefas da sprint

| Aluno | Tarefa |
|---|---|
| **Ítalo (A)** | Escrever a recomendação técnica e revisar o código dos três |
| **B** | Revisar figuras, tabelas e referências do TCC |
| **C** | Organizar o repositório e montar a apresentação |

---

### Passo a passo do Ítalo

**1. A recomendação técnica** (`docs/recomendacao.md`), em uma página, escrita **para a equipe de desenvolvimento do Narrativas**:

- qual estratégia adotar e por quê;
- com quais configurações (tratamento de acento, quais campos indexar);
- **a partir de qual tamanho de acervo ela compensa** — se com 100 narrativas todas são igualmente rápidas, dizer isso é honesto e útil;
- quanto ela custa em espaço em disco e em tempo de cadastro;
- o que fazer quando o acervo passar de 10.000 narrativas, que foi o maior volume testado;
- **as limitações** do que foi medido.

**2. Um quadro-resumo**, que é a figura mais útil do trabalho:

| Estratégia | Tempo (10.000) | Precisão | Ordena por relevância? | Custo em disco | Trata acento? | Recomendada? |
|---|---|---|---|---|---|---|
| E1 | | | Não | Nenhum | | |
| E2 | | | Não | | | |
| E3 | | | Sim | | | |
| E4 | | | Sim | | | |

**3. Revisem o código dos três.** Rodem tudo do zero, na ordem do README, em uma máquina limpa. Se algum script não rodar, conserte agora.

---

### Passo a passo do Aluno B

**1. Revisar todo o material do TCC**, com o [checklist das orientações gerais](../../../README.md#checklist-antes-de-enviar-uma-versão-ao-orientador). Confira item a item:

- toda figura e tabela com identificação **em cima**, centralizada, e fonte **embaixo**;
- toda figura e tabela **citada no texto antes** de aparecer, e explicada depois;
- toda obra citada no texto está nas Referências, e toda referência foi citada;
- referências em ordem alfabética, no padrão da NBR 6023:2018;
- siglas escritas por extenso na primeira vez.

---

### Passo a passo do Aluno C

**1. Organizar o repositório:** scripts numerados na ordem de execução, cada um com um comentário no topo dizendo o que faz, sem código morto e sem caminho fixo da máquina de vocês (`C:\Users\...`) dentro do código.

**2. Confiram que nada de indevido foi comitado:** `git log --stat` não pode mostrar nenhum arquivo fora de `italo/`, e o `config_local.py` com a senha não pode estar no histórico.

**3. A apresentação** (10 minutos, 10 a 12 slides): o problema, a base de teste, as quatro estratégias, como mediram, dois gráficos, o quadro-resumo e a recomendação. Demonstrem o protótipo ao vivo se der.

### Como saber que a Sprint 8 deu certo

- [ ] Recomendação técnica escrita, com o quadro-resumo.
- [ ] Tudo roda do zero seguindo o README.
- [ ] Repositório organizado, sem senha e sem arquivo fora da subpasta.
- [ ] Apresentação montada.

---

## Quadro-resumo das sprints

| Sprint | Período | O que entrega | O que aprende |
|---|---|---|---|
| 1 | 22/09 a 28/09 | Ambiente, corpus e tabelas nos dois bancos | Git, protocolo de experimento, domínio público |
| 2 | 29/09 a 05/10 | Três bases carregadas nos dois bancos | geração de dados, codificação, carga em lote |
| 3 | 06/10 a 12/10 | E1 e E2 medidas, com planos de execução | cronometragem, índices, injeção de SQL |
| 4 | 13/10 a 19/10 | E3 (FTS5) medida | índice invertido, relevância, acentos |
| 5 | 20/10 a 26/10 | E4 (MySQL) e gabarito de relevância | FULLTEXT, avaliação cega |
| 6 | 27/10 a 02/11 | Métricas, tabelas e gráficos | precisão, revocação, P@10 |
| 7 | 03/11 a 09/11 | Protótipo e repetição em outra máquina | reprodutibilidade |
| 8 | 10/11 a 16/11 | Recomendação e fechamento | síntese |

---

## Se algo der errado no cronograma

| Problema | O que fazer |
|---|---|
| FTS5 não disponível no Python da máquina | Avisem o orientador **na Sprint 1**. Existe alternativa, mas ela precisa ser decidida cedo |
| Sem acesso ao MySQL do laboratório | Sigam com as três estratégias do SQLite e declarem a E4 como trabalho futuro |
| Gerar a base de 10.000 demora demais | Trabalhem com 100 e 1.000 durante o desenvolvimento, e gerem a de 10.000 só uma vez, para a medição final |
| Medições muito instáveis | Fechem todos os outros programas e refaçam. Se continuar, falem com o orientador **na Sprint 3** |
| Julgamento do gabarito atrasou | Reduzam de 12 para 8 consultas. Melhor um gabarito menor e bem-feito do que um grande e apressado |
| Atraso geral | Cortem o protótipo (Sprint 7) e a repetição em outra máquina. **Não cortem** as repetições das medições nem o gabarito |

**Se precisarem cortar, cortem quantidade, não qualidade.** Três estratégias bem medidas valem mais que quatro medidas de qualquer jeito.

---

## Se sobrar tempo (opcional)

- **E1.** Testar o tokenizador `trigram` do FTS5, que tem um comportamento diferente para busca parcial de palavras.
- **E2.** Testar o modo `IN BOOLEAN MODE` do MySQL e comparar com o `NATURAL LANGUAGE MODE`.
- **E3.** Trocar a lista de palavras ignoradas do MySQL por uma lista em português e medir o efeito no tamanho do índice.
- **E4.** Gerar uma base de 50.000 narrativas e ver se a ordem das estratégias se mantém.
- **E5.** Medir o tempo de busca combinada com filtro (por tipo ou por cidade), que é o que a tela do portal realmente vai fazer.

---

## Relação com o TCC

O desenvolvimento e a escrita andam juntos (ver `01_italo_narrativas_tarefas_escrita.md`). O Ítalo escreve o texto, mas **B e C entregam o material de cada capítulo antes do prazo**, para ele ter tempo de integrar:

| Capítulo do TCC | De onde vem o conteúdo | Quem entrega o material |
|---|---|---|
| Referencial Teórico | leituras das Sprints 1 a 5 | os três, com duas ou três fontes cada |
| Metodologia | protocolo da Sprint 1 e gabarito da Sprint 5 | Ítalo e B |
| Materiais e Métodos | Sprints 1 e 2 (ferramentas, versões, corpus, máquina) | B e C |
| Resultados | Sprints 3 a 7 | os três |
| Conclusão | `docs/diario.md` e a recomendação da Sprint 8 | Ítalo |

**Nunca apaguem uma medição das planilhas.** Rodada estranha vira observação no TCC, não lixo.
