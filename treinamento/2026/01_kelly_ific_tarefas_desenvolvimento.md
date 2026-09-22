# Plano de tarefas de desenvolvimento – Kelly (Tecnologia em Sistemas para Internet)

**Projeto pai:** iFIC – Desenvolvimento de Funcionalidades de Autenticação, Administração e Gerenciamento de Cursos de Formação Inicial e Continuada (ver `.llm/ific/projeto.md`).

**Temática escolhida:** S7 – Busca de cursos: comparação entre a busca textual do MySQL e uma camada de busca dedicada (ver `.llm/ific/tematicas.md`).

**Perfil do aluno:** 1 aluno do Curso Superior de Tecnologia em Sistemas para Internet, com conhecimentos **básicos a intermediários** em Python, em treinamento.

**Duração:** 8 sprints de 1 semana (22/09/2026 a 16/11/2026).

---

## Como este documento funciona

Cada sprint tem três partes:

- **O que você vai entregar** — em uma frase, o que precisa estar funcionando no fim da semana;
- **Passo a passo** — a lista numerada do que fazer, na ordem. Siga na ordem, sem pular;
- **Como saber que deu certo** — o que você deve ver na tela. Se não vir isso, ainda não terminou.

**Regra de ouro:** cada sprint é pequena de propósito. Se terminar antes, **não comece a próxima**: use o tempo que sobrou para entender melhor o que fez e para escrever o artigo. O plano de escrita (`01_kelly_ific_tarefas_escrita.md`) anda em paralelo e é tão importante quanto o código.

**Travou mais de 40 minutos no mesmo erro? Pare e peça ajuda.** Isso não é desistir, é administrar o tempo. Mande a mensagem de erro **inteira**, copiada e colada, não um resumo dela.

---

## O ambiente do laboratório

Duas características do ambiente definiram a montagem deste trabalho:

1. **O MySQL já está instalado.** Ótimo: é o mesmo banco do projeto iFIC, então tudo o que você medir vale diretamente para a plataforma. A Busca 2 do seu trabalho é o recurso de busca textual do próprio MySQL;
2. **Não é possível instalar aplicativos novos.** Ferramentas de busca de mercado (Elasticsearch, Meilisearch, Solr) rodam como serviço separado e precisariam ser instaladas — não dá. Por isso a camada de busca dedicada (a Busca 3) é **construída em Python**, com bibliotecas instaladas por `pip`.

Isso não empobrece o trabalho. A Busca 3 usa os mesmos mecanismos que existem dentro das ferramentas grandes — índice invertido, BM25, radical das palavras, tolerância a erro de digitação. **Você vai entender melhor** do que se apenas configurasse uma ferramenta pronta, porque vai ver cada peça funcionando e vai medir o efeito de cada uma separadamente.

### O que você vai usar

| Ferramenta | Como obtém | Para quê |
|---|---|---|
| **Python 3.10+** | já instalado (confirme a versão) | linguagem do trabalho |
| **MySQL 8** | **já instalado no laboratório** | banco de dados do catálogo e a Busca 2 |
| `PyMySQL` | `pip install PyMySQL` | conectar o Python ao MySQL |
| `rank_bm25` | `pip install rank_bm25` | pontuação BM25 da busca em Python |
| `snowballstemmer` | `pip install snowballstemmer` | redução de palavras ao radical, em português |
| `difflib` | **já vem com o Python** | correção de erro de digitação |
| `matplotlib` | `pip install matplotlib` | gráficos do artigo |
| `django` | `pip install django` | a página web, só na Sprint 7 |

São **cinco** pacotes a instalar. Só isso.

> **Por que `PyMySQL` e não `mysqlclient`?** Os dois conectam o Python ao MySQL. O `mysqlclient` é mais rápido, mas precisa ser compilado e falha com frequência ao instalar no Windows. O `PyMySQL` é Python puro e instala sempre. Para este trabalho a diferença de velocidade é irrelevante — e, de qualquer forma, **as três buscas usam o mesmo driver**, então a comparação não é afetada. Registre essa escolha em `docs/ambiente.md`: ela entra em Materiais e Métodos.

> **Duas coisas para confirmar com o orientador na Sprint 1:**
> 1. **Acesso ao MySQL** — endereço, porta, usuário, senha, e se você tem permissão para **criar um banco de dados**. Se não tiver, peça que criem um para você (`ific_busca`) com permissão de criar tabelas. Sem isso, a Sprint 2 não anda;
> 2. **Git** — confirme se está instalado. Se não estiver, combine outra forma de entrega (enviar os arquivos pela página do GitHub, no navegador, funciona e não exige instalação).
>
> Confirme também, no primeiro dia, que o `pip install` funciona na máquina do laboratório. Se houver proxy ou bloqueio, isso precisa ser resolvido **na Sprint 1**, e não na semana em que você precisar entregar resultado.

---

## Onde o trabalho acontece

O **repositório de treinamento do projeto já existe** e é compartilhado com os outros alunos. Você **não cria repositório nenhum**. Todo o seu trabalho fica dentro de **uma única subpasta sua**:

```
<repositorio-de-treinamento>/
├── ...              ← pastas de outros alunos (não mexa)
└── kelly/           ← a sua subpasta: tudo o que você fizer fica aqui dentro
```

Confirme com o orientador o **endereço do repositório** e o **nome exato da sua subpasta** antes de começar. Todos os caminhos citados neste documento são **relativos à sua subpasta**.

### Regras do repositório compartilhado

1. **Só altere arquivos da sua subpasta.** Nunca edite, mova ou apague arquivo de outro aluno.
2. **Comece o dia com `git pull`.**
3. **Envie apenas o que é seu:** `git add kelly/` — nunca `git add .`. Confira com `git status` antes.
4. **Não envie** a pasta `.venv/`, `__pycache__/` nem o arquivo `config.py` (que tem a senha do banco).
5. **Deu conflito (`CONFLICT`)? Pare e chame o orientador.** Conflito mal resolvido apaga o trabalho dos outros.
6. **Envie ao fim de cada dia.** Código que só existe na sua máquina não foi entregue.

---

## A estrutura de pastas que você vai construir

Você não precisa criar tudo de uma vez — cada sprint cria a sua parte. Esta é a figura final, para você saber onde está indo:

```
kelly/
├── dados/
│   ├── cursos.csv            ← o catálogo de cursos (Sprint 2)
│   ├── consultas.csv         ← as buscas de teste (Sprint 3)
│   └── gabarito.csv          ← quais cursos são a resposta certa (Sprint 3)
├── buscadores/
│   ├── __init__.py
│   ├── busca1_like.py        ← Sprint 2
│   ├── busca2_fulltext.py    ← Sprint 4
│   └── busca3_python.py      ← Sprints 5 e 6
├── banco.py                  ← a conexão com o MySQL (Sprint 1)
├── config.py                 ← usuário e senha — NÃO vai para o Git
├── config_exemplo.py         ← modelo sem a senha — esse vai
├── criar_banco.py            ← Sprint 2
├── avaliar.py                ← Sprint 3
├── graficos.py               ← Sprint 8
├── site/                     ← a página web em Django (Sprint 7)
├── docs/
│   ├── ambiente.md
│   ├── resultados.csv
│   ├── diario.md
│   └── evidencias/           ← prints de tela
├── requirements.txt
└── README.md
```

---

## O que vai ser comparado

Três formas de buscar um curso, **sobre o mesmo catálogo e com as mesmas consultas**:

| Nome | O que é | Onde a busca acontece |
|---|---|---|
| **Busca 1** | `LIKE '%termo%'` em SQL — o jeito mais simples e mais comum | dentro do MySQL, sem índice de texto |
| **Busca 2** | **`FULLTEXT` do MySQL**, com `MATCH ... AGAINST` | dentro do MySQL, com índice invertido e pontuação de relevância |
| **Busca 3** | Um buscador escrito em Python, com recursos de linguagem: radical das palavras, sinônimos e tolerância a erro de digitação | fora do banco, em uma camada separada |

**Por que as três ao mesmo tempo, no mesmo projeto?** Porque assim elas respondem às **mesmas consultas, sobre o mesmo catálogo, na mesma máquina, no mesmo dia**. Se você medisse uma em cada semana, qualquer diferença da máquina estragaria a comparação. Guarde esta frase: ela volta na Metodologia do artigo.

---

## Combinados que valem para todas as sprints

- **Diário (`docs/diario.md`):** ao fim de cada sprint, escreva 3 linhas — o que funcionou, o que deu errado, o que aprendi. Leva cinco minutos e vai salvar a sua Conclusão daqui a dois meses.
- **Planilha de resultados (`docs/resultados.csv`):** a partir da Sprint 3, cada medição vira uma linha. **Nunca apague uma linha.**
- **Prints (`docs/evidencias/`):** sempre que algo funcionar, tire um print. Eles viram figuras do artigo.
- **Envios (*commits*):** pelo menos 3 por semana, com mensagem curta em português (`Adiciona indice FULLTEXT`). Mensagem `ajustes` não conta.
- **Reunião semanal:** no começo de cada sprint você mostra ao orientador o que fez, **rodando na tela**. A partir da Sprint 3, "está funcionando" não basta: tem que ter número.

---

# Sprint 1 — 22/09 a 28/09/2026
## Preparar o ambiente e conversar com o MySQL

**O que você vai entregar:** a sua subpasta criada, o Python com as bibliotecas instaladas, e um script que conecta no MySQL e imprime a versão dele.

Esta sprint é curta de propósito. O objetivo é **eliminar todas as surpresas de ambiente agora**, e não na semana em que você precisar entregar resultado.

### Passo a passo

**1. Confirme o Python.** Abra o Prompt de Comando (tecle `Win`, digite `cmd`, Enter) e rode:

```
python --version
pip --version
```

Você deve ver algo como `Python 3.11.5` e uma linha do `pip`. Se aparecer "não é reconhecido como comando", chame o orientador antes de continuar. **Anote as duas versões em `docs/ambiente.md`.**

**2. Peça o acesso ao MySQL.** Você precisa de: endereço do servidor (provavelmente `localhost`), porta (normalmente `3306`), usuário, senha, e a confirmação de que pode **criar um banco de dados**. Anote tudo — menos a senha, que não vai para lugar nenhum público.

**3. Pegue o repositório.** Com o Git disponível:

```
git clone <endereco-do-repositorio>
cd <nome-do-repositorio>
mkdir kelly
cd kelly
```

Se o Git **não** estiver instalado, combine com o orientador a forma de entrega e siga em frente — não perca a semana nisso.

**4. Crie o ambiente virtual.** Dentro de `kelly/`:

```
python -m venv .venv
.venv\Scripts\activate
```

Depois de ativar, o começo da linha passa a mostrar `(.venv)`. **Se não mostrar, o ambiente não está ativo** e tudo o que você instalar vai para o lugar errado. Toda vez que abrir um Prompt novo, precisa ativar de novo.

> Se você estiver no PowerShell e aparecer erro de "execução de scripts desabilitada", use o Prompt de Comando (`cmd`), que não tem essa restrição.

**5. Instale as bibliotecas:**

```
pip install PyMySQL rank_bm25 snowballstemmer matplotlib
pip freeze > requirements.txt
```

Se der erro de rede ou de proxy, é o momento de resolver — chame o orientador.

**6. Crie a estrutura de pastas.** Ainda dentro de `kelly/`:

```
mkdir dados
mkdir buscadores
mkdir docs
mkdir docs\evidencias
```

**7. Guarde a senha fora do código.** Crie `config.py`:

```python
BANCO = {
    "host": "localhost",
    "port": 3306,
    "user": "seu_usuario",
    "password": "sua_senha",
    "database": "ific_busca",
    "charset": "utf8mb4",
}
```

Crie também `config_exemplo.py`, igual, mas com `"password": "coloque-a-senha-aqui"`. O `config_exemplo.py` vai para o Git; o `config.py`, **não**.

Crie um arquivo `.gitignore` dentro de `kelly/`:

```
.venv/
__pycache__/
*.pyc
config.py
docs/evidencias/*.mp4
```

**Senha em repositório compartilhado não é preciosismo:** é a diferença entre um segredo seu e um segredo de todo mundo que tem acesso ao repositório.

**8. Escreva o módulo de conexão.** Crie `banco.py`:

```python
import pymysql
from config import BANCO

def conectar(com_banco=True):
    """Abre uma conexao com o MySQL.

    com_banco=False conecta sem escolher banco — usado so para criar o banco.
    """
    parametros = dict(BANCO)
    if not com_banco:
        parametros.pop("database")
    return pymysql.connect(**parametros)
```

**9. Escreva o script de verificação.** Crie `verificar_ambiente.py`:

```python
import sys
import pymysql
from config import BANCO

print("Python:", sys.version)
print("PyMySQL:", pymysql.__version__)

parametros = dict(BANCO)
parametros.pop("database")          # o banco ainda nao existe
conexao = pymysql.connect(**parametros)

with conexao.cursor() as cursor:
    cursor.execute("SELECT VERSION()")
    print("MySQL:", cursor.fetchone()[0])

    # o MySQL considera 'informatica' e 'informática' a mesma coisa?
    cursor.execute("SELECT 'informática' = 'informatica'")
    print("Acentos ignorados na comparacao:", cursor.fetchone()[0])

    cursor.execute("SHOW VARIABLES LIKE 'innodb_ft_min_token_size'")
    print("Tamanho minimo de palavra indexada:", cursor.fetchone())

conexao.close()

import rank_bm25
import snowballstemmer

radicalizador = snowballstemmer.stemmer("portuguese")
print("Radical de 'costureiras':", radicalizador.stemWords(["costureiras"]))
```

Rode com `python verificar_ambiente.py`.

**10. Entenda o que esse script está perguntando ao banco** — porque as três respostas vão para o artigo:

- **a versão do MySQL.** Precisa ser 8.x. Se for 5.7, avise o orientador: quase tudo funciona igual, mas o nome da *collation* muda (veja a Sprint 2);
- **se os acentos são ignorados.** Se imprimir `1`, o servidor já trata "informatica" e "informática" como iguais. Isso vem da *collation* — a regra de comparação de texto do banco — e é um recurso que você vai usar de graça. Se imprimir `0`, você resolve isso ao criar o banco, na Sprint 2;
- **`innodb_ft_min_token_size`.** É o tamanho mínimo de palavra que o índice de texto do MySQL guarda. O padrão é 3, ou seja, palavras de 1 ou 2 letras (como "TI" ou "3D") **não são indexadas**. Mudar isso exige mexer na configuração do servidor e reiniciá-lo — coisa que você não pode fazer no laboratório. **Não tem problema: vira uma limitação declarada no artigo**, e limitação declarada fortalece o texto.

**11. Preencha `docs/ambiente.md`:** versão do Python, versão do MySQL, driver utilizado, resultado do teste de acentos, valor do `innodb_ft_min_token_size`, e a configuração da máquina (processador, memória RAM, sistema operacional).

### Como saber que deu certo

Você deve ver na tela, mais ou menos, isto:

```
Python: 3.11.5 ...
PyMySQL: 1.1.0
MySQL: 8.0.36
Acentos ignorados na comparacao: 1
Tamanho minimo de palavra indexada: ('innodb_ft_min_token_size', '3')
Radical de 'costureiras': ['costur']
```

Tire um print e guarde em `docs/evidencias/`.

> **Erros comuns nesta etapa e o que significam:**
> - `Access denied for user` → usuário ou senha errados no `config.py`;
> - `Can't connect to MySQL server` → o servidor não está no ar, ou o endereço/porta estão errados;
> - `ModuleNotFoundError: No module named 'pymysql'` → o ambiente virtual não está ativo (olhe se aparece `(.venv)` na linha).

### Entrega da sprint

- [ ] Subpasta `kelly/` criada no repositório.
- [ ] Ambiente virtual criado e as quatro bibliotecas instaladas.
- [ ] `requirements.txt` gerado.
- [ ] `config.py` criado e **fora do Git**; `config_exemplo.py` dentro.
- [ ] `banco.py` e `verificar_ambiente.py` funcionando, com print em `docs/evidencias/`.
- [ ] `docs/ambiente.md` preenchido, incluindo o teste de acentos e o tamanho mínimo de palavra.
- [ ] Acesso ao MySQL e situação do Git conversados com o orientador.
- [ ] `docs/diario.md` criado, com as 3 linhas da semana.

---

# Sprint 2 — 29/09 a 05/10/2026
## O catálogo de cursos e a Busca 1

**O que você vai entregar:** um arquivo com 200 a 300 cursos, carregado em uma tabela do MySQL, e a primeira busca funcionando no terminal.

**Aviso:** montar o catálogo dá mais trabalho do que parece, e **tudo** depois depende dele. Comece por ele na segunda-feira.

### Passo a passo

**1. Monte o arquivo de cursos.** Abra o **Guia Pronatec de Cursos FIC** (documento público) e também o portal de cursos do IFRN. Copie os cursos para uma planilha (Excel ou Planilhas Google) com exatamente estas colunas:

```
codigo,nome,eixo,carga_horaria,ementa
```

Preencha assim:

- `codigo`: um sequencial que você inventa — `FIC001`, `FIC002`, ... Vai ser a identidade do curso no trabalho inteiro;
- `nome`: o nome do curso, como está no guia;
- `eixo`: o eixo tecnológico (Informação e Comunicação, Produção Alimentícia, Infraestrutura, etc.);
- `carga_horaria`: o número de horas, só o número;
- `ementa`: **2 a 4 frases** descrevendo o que a pessoa aprende no curso.

**Sobre a ementa — leia com atenção, é o ponto mais importante da semana.** É na ementa que estão as palavras que o candidato digita e que **não** aparecem no título. Se o guia trouxer a descrição do curso, use. Se não trouxer, **escreva você mesmo**, em duas ou três frases, com as palavras que uma pessoa comum usaria.

Exemplo do que funciona:

> **Nome:** Operador de Computador
> **Ementa:** Curso voltado a quem quer aprender a usar o computador no dia a dia e no trabalho. Aborda Windows, digitação de textos no Word, planilhas no Excel, navegação na internet e uso de e-mail. Indicado para quem tem pouca ou nenhuma experiência com informática.

Repare: a palavra "Excel" não está no título, mas está na ementa. É exatamente esse tipo de caso que o seu trabalho vai medir.

**Duas regras que não podem ser quebradas:**

- **a ementa tem que ter relação real com o nome do curso.** Texto aleatório destrói o trabalho inteiro;
- **anote quantas ementas vieram do guia e quantas você escreveu.** Esse número vai para o artigo. Declarar isso é honestidade científica, e fortalece o texto em vez de enfraquecer.

Salve como **CSV UTF-8** em `dados/cursos.csv`. No Excel: *Salvar como → CSV UTF-8 (delimitado por vírgula)*. Se o seu Excel salvar separando por ponto e vírgula, avise no código: `csv.DictReader(arquivo, delimiter=";")`.

**Meta: 200 cursos bastam.** Se chegar a 300, melhor. **Não pare o trabalho para chegar a 500** — o objeto de estudo é a qualidade da busca, não o tamanho do catálogo.

**2. Crie o banco e a tabela.** Escreva `criar_banco.py`:

```python
import csv
from config import BANCO
from banco import conectar

# 1) cria o banco, se ainda nao existir
conexao = conectar(com_banco=False)
with conexao.cursor() as cursor:
    cursor.execute(
        f"CREATE DATABASE IF NOT EXISTS {BANCO['database']} "
        "CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci"
    )
conexao.close()

# 2) cria a tabela e carrega o CSV
conexao = conectar()
with conexao.cursor() as cursor:
    cursor.execute("DROP TABLE IF EXISTS cursos")
    cursor.execute("""
        CREATE TABLE cursos (
            id            INT AUTO_INCREMENT PRIMARY KEY,
            codigo        VARCHAR(20) UNIQUE,
            nome          VARCHAR(200),
            eixo          VARCHAR(120),
            carga_horaria INT,
            ementa        TEXT
        ) ENGINE=InnoDB
    """)

    with open("dados/cursos.csv", encoding="utf-8") as arquivo:
        for linha in csv.DictReader(arquivo):
            cursor.execute(
                "INSERT INTO cursos (codigo, nome, eixo, carga_horaria, ementa)"
                " VALUES (%s, %s, %s, %s, %s)",
                (linha["codigo"].strip().upper(),
                 linha["nome"].strip(),
                 linha["eixo"].strip(),
                 int(linha["carga_horaria"]),
                 linha["ementa"].strip()),
            )

    conexao.commit()
    cursor.execute("SELECT COUNT(*) FROM cursos")
    print(f"{cursor.fetchone()[0]} cursos carregados.")
conexao.close()
```

Rode com `python criar_banco.py`.

**Três detalhes importantes neste código:**

- **`COLLATE utf8mb4_0900_ai_ci`** — a *collation* é a regra que o banco usa para comparar texto. O `ai` significa *accent insensitive* (ignora acento) e o `ci`, *case insensitive* (ignora maiúscula e minúscula). É graças a isso que "informatica" vai encontrar "informática" sem você escrever nenhum código para isso. **Esse detalhe é conteúdo do seu artigo**, não configuração burocrática;

  > **Se o MySQL for 5.7**, essa collation não existe. Use `utf8mb4_unicode_ci`, que faz o mesmo papel. Anote qual você usou.

- **`ENGINE=InnoDB`** — é o mecanismo de armazenamento do MySQL que suporta índice `FULLTEXT`, que você vai criar na Sprint 4. Normalmente já é o padrão, mas deixar escrito evita surpresa;

- **`.upper()` no código do curso** — mais adiante você vai comparar códigos vindos de arquivos diferentes, e em Python `"FIC001"` e `"fic001"` são textos diferentes. Padronizar agora evita um erro chato daqui a duas semanas.

**3. Escreva a Busca 1.** Crie `buscadores/busca1_like.py`:

```python
from banco import conectar

def buscar(termo, limite=20):
    """Busca 1: LIKE. Procura o texto digitado dentro do nome ou da ementa."""
    padrao = f"%{termo}%"
    conexao = conectar()
    with conexao.cursor() as cursor:
        cursor.execute(
            """SELECT codigo FROM cursos
               WHERE nome LIKE %s OR ementa LIKE %s
               ORDER BY nome
               LIMIT %s""",
            (padrao, padrao, limite),
        )
        linhas = cursor.fetchall()
    conexao.close()
    return [linha[0] for linha in linhas]

if __name__ == "__main__":
    termo = input("Buscar: ")
    resultados = buscar(termo)
    print(f"{len(resultados)} resultado(s): {resultados}")
```

Crie também um arquivo **vazio** chamado `buscadores/__init__.py`. É ele que faz o Python enxergar a pasta como um módulo — sem ele, o script da Sprint 3 não vai conseguir importar as buscas.

**Combinado que vale para as três buscas** — decida agora e não mude mais:

- a função se chama sempre **`buscar(termo, limite=20)`**;
- ela devolve sempre uma **lista de códigos de curso**, em ordem, **no máximo 20**;
- é só isso. Nada de imprimir dentro dela, nada de devolver formato diferente.

Com as três buscas tendo a mesma "cara", o script de avaliação da Sprint 3 funciona para todas sem mudar nada. **Essa padronização é o que faz o resto do trabalho ficar fácil.**

**4. Teste a busca e anote o que dá errado.** Rode o script e teste, no mínimo:

| Digite | O que você espera | O que aconteceu |
|---|---|---|
| `informática` | cursos de informática | |
| `informatica` (sem acento) | os mesmos | |
| `exel` | cursos de Excel | |
| `informática básica` | cursos de informática básica | |
| `básica informática` | os mesmos de cima | |
| `costureiras` | cursos de costura | |

Preencha a coluna da direita e **cole essa tabela no seu diário**. Ela é ouro: cada linha que deu errado vira um exemplo concreto na problemática do artigo, e exemplo concreto convence muito mais do que frase genérica.

> Repare que a linha do "sem acento" provavelmente **vai funcionar**, por causa da collation. Registre isso: é um recurso que o banco já dá de graça, e saber disso é resultado.

### Como saber que deu certo

- `python criar_banco.py` imprime algo como `247 cursos carregados.`
- `python buscadores/busca1_like.py`, digitando `costura`, devolve uma lista de códigos.
- A tabela de testes está preenchida, e você já sabe apontar pelo menos **quatro coisas que a Busca 1 não consegue fazer**.

### Entrega da sprint

- [ ] `dados/cursos.csv` com 200+ cursos, todos com ementa preenchida.
- [ ] Anotado quantas ementas são do guia e quantas você escreveu.
- [ ] `criar_banco.py` funcionando; rodar duas vezes não quebra nada.
- [ ] Collation usada registrada em `docs/ambiente.md`.
- [ ] `buscadores/busca1_like.py` e `buscadores/__init__.py` criados.
- [ ] Tabela de testes preenchida em `docs/diario.md`.
- [ ] Print da busca funcionando em `docs/evidencias/`.

---

# Sprint 3 — 06/10 a 12/10/2026
## Como medir se uma busca é boa

**O que você vai entregar:** 30 consultas de teste, o gabarito de respostas certas, e um script que dá uma nota para qualquer busca.

**Esta é a sprint mais importante do trabalho.** Sem ela, tudo o que você disser depois é opinião. Com ela, vira medição.

**A ideia, em uma frase:** para saber se uma busca é boa, você precisa de (1) uma lista de buscas que as pessoas fariam e (2) uma lista do que seria a resposta certa para cada uma. Depois é só comparar o que a busca devolveu com o que deveria ter devolvido. Essa forma de avaliar tem nome e quase 60 anos — chama-se **paradigma de Cranfield**, e vai para o seu Referencial Teórico.

### Passo a passo

**1. Escreva 30 consultas de teste**, cinco de cada uma destas seis categorias:

| Categoria | O que testa | Exemplos |
|---|---|---|
| `exato` | o básico: o termo está no título | `eletricista`, `panificação` |
| `generico` | palavras que estão na ementa, não no título | `computador`, `alimentação`, `excel` |
| `sem_acento` | o que acontece sem acentuação | `informatica`, `mecanica`, `producao` |
| `erro_digitacao` | quando a pessoa erra ao digitar | `exel`, `enfermagen`, `eletrisista` |
| `plural` | variação da palavra | `costureiras`, `eletricistas`, `padeiros` |
| `sinonimo` | o nome popular, diferente do nome oficial | `faxina` (para *Serviços domésticos*), `curso de costura` |

**Por que categorias, e não 30 consultas soltas?** Porque o resultado mais interessante do seu trabalho não vai ser "a Busca 3 é melhor". Vai ser "**a Busca 3 é melhor exatamente nestas duas categorias, e empata nas outras quatro**". Isso só aparece se as consultas estiverem organizadas assim desde o começo.

Salve em `dados/consultas.csv`:

```
id_consulta,texto,categoria
q01,eletricista,exato
q02,computador,generico
q03,exel,erro_digitacao
```

**2. Monte o gabarito.** Para cada consulta, abra o `dados/cursos.csv`, leia os cursos e anote **quais seriam uma resposta certa** para quem digitou aquilo. Salve em `dados/gabarito.csv`:

```
id_consulta,codigo_curso
q01,FIC014
q01,FIC052
q02,FIC003
```

Uma linha por par consulta–curso. Uma consulta pode ter 1 curso certo ou 8; o que não pode é ter zero — se não tiver nenhum, troque a consulta.

**Três regras do gabarito, leia antes de começar:**

1. **Monte o gabarito ANTES de rodar as buscas.** Se você rodar a Busca 3, olhar o resultado e só então decidir o que é relevante, está fazendo um gabarito que favorece a Busca 3 — e isso invalida o experimento inteiro. Monte lendo o **catálogo**, não os resultados;
2. **Escreva o seu critério** em `dados/criterio.md`, em cinco linhas: o que você considerou "resposta certa". Por exemplo: *"Considerei relevante todo curso em que uma pessoa que digitou aquele termo se inscreveria, ou que consideraria seriamente. Não considerei cursos que apenas mencionam a palavra de passagem."* Esse texto vai para a Metodologia do artigo;
3. **Peça ao orientador para conferir 10 consultas.** Mostre o catálogo e essas 10 consultas, peça que ele diga o que consideraria certo, e compare com o seu. Onde vocês discordarem, converse e ajuste. Leva meia hora e dá **muita** credibilidade ao trabalho — descreva essa conferência no artigo.

> **Isto não é pesquisa com pessoas.** Você julgando a relevância dos cursos faz parte de construir o instrumento de medida, e o orientador conferindo faz parte da orientação. Não há participantes, não há coleta de dados de pessoas, não há nada a submeter ao Comitê de Ética. Deixe isso escrito no artigo — é uma dúvida comum de quem avalia.

**3. Entenda as três notas antes de programá-las.** Suponha que a consulta `q02` tenha 4 cursos certos no gabarito, e que a busca tenha devolvido 20 resultados, dos quais os das posições 1, 2 e 7 estão certos.

- **P@5 (precisão nos 5 primeiros)** = quantos dos 5 primeiros estão certos, dividido por 5 → 2 certos entre os 5 primeiros = **0,40**.
  *Responde: o que apareceu na primeira tela presta?* É a nota mais importante, porque candidato não rola a página.
- **Revocação** = quantos dos certos a busca achou, dividido pelo total de certos → achou 3 dos 4 = **0,75**.
  *Responde: deixou passar algum curso bom?*
- **RR (posição do primeiro acerto)** = 1 dividido pela posição do primeiro resultado certo → primeiro certo na posição 1 = **1,00**. Se estivesse na posição 4, seria 0,25.
  *Responde: a pessoa achou logo de cara?* A média do RR de todas as consultas chama-se **MRR**.

**4. Escreva o script de avaliação.** Crie `avaliar.py`:

```python
import csv
import importlib
import os
import statistics
import time

def carregar_consultas():
    with open("dados/consultas.csv", encoding="utf-8") as arquivo:
        return list(csv.DictReader(arquivo))

def carregar_gabarito():
    gabarito = {}
    with open("dados/gabarito.csv", encoding="utf-8") as arquivo:
        for linha in csv.DictReader(arquivo):
            id_consulta = linha["id_consulta"].strip()
            codigo = linha["codigo_curso"].strip().upper()
            gabarito.setdefault(id_consulta, set()).add(codigo)
    return gabarito

def precisao_em_5(resultados, certos):
    primeiros = resultados[:5]
    if not primeiros:
        return 0.0
    return sum(1 for codigo in primeiros if codigo in certos) / 5

def revocacao(resultados, certos):
    if not certos:
        return 0.0
    return sum(1 for codigo in resultados if codigo in certos) / len(certos)

def posicao_do_primeiro_acerto(resultados, certos):
    for posicao, codigo in enumerate(resultados, start=1):
        if codigo in certos:
            return 1 / posicao
    return 0.0

def avaliar(nome_do_modulo, rotulo):
    modulo = importlib.import_module(nome_do_modulo)
    consultas = carregar_consultas()
    gabarito = carregar_gabarito()
    linhas = []

    for consulta in consultas:
        id_consulta = consulta["id_consulta"].strip()
        certos = gabarito.get(id_consulta, set())

        inicio = time.perf_counter()
        resultados = [c.strip().upper() for c in modulo.buscar(consulta["texto"])]
        tempo_ms = (time.perf_counter() - inicio) * 1000

        linhas.append({
            "busca": rotulo,
            "id_consulta": id_consulta,
            "categoria": consulta["categoria"],
            "p5": round(precisao_em_5(resultados, certos), 4),
            "revocacao": round(revocacao(resultados, certos), 4),
            "rr": round(posicao_do_primeiro_acerto(resultados, certos), 4),
            "tempo_ms": round(tempo_ms, 2),
            "qtd_resultados": len(resultados),
        })

    print(f"\n=== {rotulo} ===")
    for campo in ["p5", "revocacao", "rr"]:
        media = statistics.mean(linha[campo] for linha in linhas)
        print(f"{campo}: {media:.3f}")
    return linhas

def salvar(linhas, caminho="docs/resultados.csv"):
    existe = os.path.exists(caminho)
    with open(caminho, "a", newline="", encoding="utf-8") as arquivo:
        escritor = csv.DictWriter(arquivo, fieldnames=list(linhas[0].keys()))
        if not existe:
            escritor.writeheader()
        escritor.writerows(linhas)

if __name__ == "__main__":
    salvar(avaliar("buscadores.busca1_like", "busca1_like"))
```

Rode com `python avaliar.py`.

> **Se der `ModuleNotFoundError: No module named 'buscadores'`**, é porque falta o arquivo vazio `buscadores/__init__.py`, ou porque você está rodando de dentro de outra pasta. Rode sempre de dentro de `kelly/`.

**5. Guarde uma linha por consulta, nunca só a média.** Repare que o script salva o detalhe de cada consulta. É esse detalhe que vai produzir a análise por categoria — o melhor resultado do seu trabalho. A média sozinha não conta a história.

### Como saber que deu certo

O script imprime as três médias da Busca 1, e o `docs/resultados.csv` fica com 30 linhas. As médias provavelmente vão ser **baixas** — é isso mesmo, a Busca 1 é a linha de base e ela é fraca de propósito. **Anote os três números no diário**: eles são o ponto de partida de toda a comparação.

### Entrega da sprint

- [ ] `dados/consultas.csv` com 30 consultas, 5 de cada categoria.
- [ ] `dados/gabarito.csv` completo.
- [ ] `dados/criterio.md` escrito.
- [ ] 10 consultas conferidas com o orientador, e as divergências anotadas.
- [ ] `avaliar.py` rodando de ponta a ponta.
- [ ] Notas da Busca 1 em `docs/resultados.csv` e no diário.

---

# Sprint 4 — 13/10 a 19/10/2026
## Busca 2: a busca textual do MySQL (`FULLTEXT`)

**O que você vai entregar:** a segunda busca funcionando, usando o índice de texto do próprio MySQL, e a comparação com a Busca 1.

**A ideia, em uma frase:** em vez de varrer todas as linhas procurando um pedaço de texto, o MySQL monta antes uma lista de "em quais cursos cada palavra aparece" — isso se chama **índice invertido** — e usa essa lista para responder rápido e **ordenado por relevância**.

### Passo a passo

**1. Crie os índices `FULLTEXT`.** Acrescente em `criar_banco.py`, logo antes do `conexao.close()`:

```python
    cursor.execute("ALTER TABLE cursos ADD FULLTEXT INDEX ft_nome (nome)")
    cursor.execute("ALTER TABLE cursos ADD FULLTEXT INDEX ft_ementa (ementa)")
    conexao.commit()
    print("Indices FULLTEXT criados.")
```

**Por que dois índices separados, e não um só sobre as duas colunas?** Porque assim você pode dar **pesos diferentes** ao nome e à ementa — casar no título deve valer mais do que casar na ementa. No MySQL, o `MATCH()` só funciona se existir um índice `FULLTEXT` **exatamente** sobre aquelas colunas; com dois índices separados, dá para somar as duas pontuações com pesos. Sem isso, você não teria como priorizar o título.

Rode `python criar_banco.py` de novo e confirme que imprime `Indices FULLTEXT criados.`

**2. Escreva a Busca 2.** Crie `buscadores/busca2_fulltext.py`:

```python
import re
from banco import conectar

def limpar(termo):
    """Mantem apenas letras, numeros e espacos.

    Sinais como +, -, *, " e ( tem significado especial na busca do MySQL
    e podem causar erro ou resultado estranho quando vem do usuario.
    """
    return re.sub(r"[^\w\s]", " ", termo, flags=re.UNICODE).strip()

def buscar(termo, limite=20, peso_nome=3, peso_ementa=1):
    """Busca 2: FULLTEXT do MySQL, ordenada por relevancia."""
    consulta = limpar(termo)
    if not consulta:
        return []

    sql = """
        SELECT codigo,
               (MATCH(nome)   AGAINST (%s IN NATURAL LANGUAGE MODE)) * %s
             + (MATCH(ementa) AGAINST (%s IN NATURAL LANGUAGE MODE)) * %s
               AS relevancia
        FROM cursos
        HAVING relevancia > 0
        ORDER BY relevancia DESC
        LIMIT %s
    """
    conexao = conectar()
    with conexao.cursor() as cursor:
        cursor.execute(sql, (consulta, peso_nome, consulta, peso_ementa, limite))
        linhas = cursor.fetchall()
    conexao.close()
    return [linha[0] for linha in linhas]

if __name__ == "__main__":
    termo = input("Buscar: ")
    print(buscar(termo))
```

Quatro pontos para entender (e escrever no artigo):

- **O que mudou de verdade:** agora existe uma **pontuação de relevância** calculada pelo banco, e os resultados vêm ordenados por ela. Deixou de ser "contém este texto" e passou a ser "o quanto este curso combina com a busca". **Esse salto conceitual é mais importante que o ganho numérico** — explique-o no artigo;
- **`IN NATURAL LANGUAGE MODE`** é o modo padrão: o MySQL separa a busca em palavras e procura cada uma. É por isso que "básica informática" passa a encontrar "Informática básica", coisa que o `LIKE` não fazia;
- **no MySQL a pontuação é positiva, e quanto maior, melhor** — daí o `ORDER BY relevancia DESC`;
- **`HAVING` em vez de `WHERE`** — como `relevancia` é um apelido criado na própria consulta, o MySQL só permite filtrá-lo no `HAVING`. É uma particularidade do SQL, e vale anotar no diário.

**3. Teste os pesos.** Rode a avaliação com `peso_nome` em 1, 3 e 5 (mantendo `peso_ementa=1`) e veja qual dá a melhor nota. **Escolha pelo número, não pela intuição**, e monte uma tabelinha — ela vira um parágrafo em Materiais e Métodos.

**4. Meça.** No final de `avaliar.py`, acrescente:

```python
    salvar(avaliar("buscadores.busca2_fulltext", "busca2_fulltext"))
```

**5. Compare as duas.** Monte no diário a tabela das médias:

| Busca | P@5 | Revocação | MRR |
|---|---|---|---|
| Busca 1 (LIKE) | | | |
| Busca 2 (FULLTEXT) | | | |

E depois olhe o detalhe: **em quais consultas a Busca 2 ganhou muito, e em quais não mudou nada?** Anote pelo menos 3 de cada.

**O que você deve observar** (e se observar, terá entendido a semana):

- **melhora grande** nas consultas de termo genérico e nas de duas palavras, porque agora existe ordenação por relevância e a busca separa a frase em palavras;
- **continua funcionando** nas consultas sem acento, por causa da collation;
- **nada muda** nas consultas com erro de digitação — `exel` continua não achando `Excel`. O `FULLTEXT` não tem como tratar isso;
- **nada muda** nos plurais — `costureiras` não acha "costureiro", porque o índice guarda a palavra inteira.

Esses dois últimos pontos **não são um defeito do seu trabalho**. São a descoberta que justifica a Busca 3. Anote com destaque.

**6. Investigue duas limitações do MySQL, e registre as duas.** São material de primeira qualidade para o artigo:

**a) Palavras curtas não são indexadas.** Confirme o valor que você já viu na Sprint 1:

```sql
SHOW VARIABLES LIKE 'innodb_ft_min_token_size';
```

Com o padrão 3, buscas como "TI" ou "3D" devolvem vazio. Teste na prática e registre. Mudar isso exige alterar a configuração do servidor e reiniciá-lo — o que você não pode fazer no laboratório. **Declare como limitação no artigo.**

**b) A lista de palavras vazias é em inglês.** Rode:

```sql
SELECT * FROM INFORMATION_SCHEMA.INNODB_FT_DEFAULT_STOPWORD;
```

Você vai ver "the", "and", "for"... e nenhuma palavra em português. Ou seja, "de", "para" e "com" **são indexadas** no seu catálogo, mesmo não distinguindo nada. Trocar essa lista também exige configuração do servidor. **Declare como limitação** — e note que a Busca 3, feita em Python, vai resolver isso com três linhas de código. Esse contraste é um dos melhores parágrafos do seu artigo.

### Como saber que deu certo

- `python buscadores/busca2_fulltext.py`, digitando `computador`, devolve cursos de informática **mesmo que "computador" não esteja no título deles**.
- Digitando `basica informatica`, devolve os cursos de informática básica.
- A tabela comparativa está no diário, e o `docs/resultados.csv` tem agora 60 linhas.

> **Se a Busca 2 devolver listas vazias para quase tudo**, verifique nesta ordem: (a) os índices `FULLTEXT` foram mesmo criados? (`SHOW INDEX FROM cursos`); (b) as palavras da sua busca têm 3 letras ou mais?; (c) a palavra buscada aparece em quase todos os cursos? Palavra muito frequente recebe pontuação quase nula — é assim que o cálculo de relevância funciona, e isso é resultado, não defeito. **Teste com a palavra "curso" e veja o que acontece.**

### Entrega da sprint

- [ ] Índices `FULLTEXT` criados por `criar_banco.py`.
- [ ] `buscadores/busca2_fulltext.py` funcionando.
- [ ] Teste dos pesos do nome (1, 3, 5) feito e anotado.
- [ ] Busca 2 medida e salva em `docs/resultados.csv`.
- [ ] Tabela comparativa Busca 1 × Busca 2 no diário.
- [ ] As duas limitações do MySQL (palavra curta e palavras vazias em inglês) testadas e registradas.
- [ ] 3 consultas em que a Busca 2 ganhou e 3 em que empatou, anotadas com os resultados.

---

# Sprint 5 — 20/10 a 26/10/2026
## Busca 3, parte 1: buscador em Python com radical das palavras

**O que você vai entregar:** a terceira busca funcionando, feita em Python, tratando plural e variação de palavras.

**A ideia, em uma frase:** em vez de guardar a palavra inteira no índice, guardar só o **radical** dela — assim "costureiras", "costureira" e "costureiro" viram todas `costur` e passam a casar entre si.

Esta sprint tem bastante código novo, mas é código curto. **Escreva uma função por vez e teste cada uma antes de passar para a próxima.**

### Passo a passo

**1. Comece pelas funções de preparação do texto.** Crie `buscadores/busca3_python.py` e escreva **só isto**, primeiro:

```python
import re
import unicodedata
import snowballstemmer

RADICALIZADOR = snowballstemmer.stemmer("portuguese")

PALAVRAS_VAZIAS = {
    "a", "as", "o", "os", "de", "da", "do", "das", "dos", "e", "em", "na", "no",
    "para", "por", "com", "um", "uma", "que", "ao", "aos", "curso", "cursos",
}

def sem_acento(texto):
    """'informática' -> 'informatica'"""
    texto = unicodedata.normalize("NFKD", texto)
    return "".join(letra for letra in texto if not unicodedata.combining(letra))

def separar_palavras(texto):
    """'Informática Básica!' -> ['informatica', 'basica']"""
    texto = sem_acento(texto.lower())
    return re.findall(r"[a-z0-9]+", texto)

def preparar(texto):
    """Texto -> lista de radicais, sem as palavras vazias.

    'Curso de Costureiras' -> ['costur']
    """
    palavras = separar_palavras(texto)
    palavras = [p for p in palavras if p not in PALAVRAS_VAZIAS and len(p) > 2]
    return RADICALIZADOR.stemWords(palavras)
```

**Teste agora, antes de continuar.** No final do arquivo, temporariamente:

```python
if __name__ == "__main__":
    print(preparar("Curso de Costureiras"))
    print(preparar("informática básica"))
```

Você deve ver algo como `['costur']` e `['informat', 'basic']`. Se viu, as três funções estão certas. **Só então continue.**

Entenda o que cada peça faz, porque cada uma é um conceito do seu Referencial Teórico — **e porque cada uma resolve algo que o MySQL resolve ou não**:

| Peça | Conceito | O que resolve | O MySQL faz? |
|---|---|---|---|
| `sem_acento` | normalização | "informatica" casar com "informática" | sim, pela collation |
| `separar_palavras` | tokenização | quebrar a frase em palavras | sim |
| `PALAVRAS_VAZIAS` | *stop words* | "de", "para", "curso" não distinguem nada | só em inglês |
| `RADICALIZADOR` | *stemming* | "costureiras" casar com "costureiro" | **não** |

Essa tabela, preenchida com os seus resultados, é uma ótima figura para o artigo.

**2. Monte o índice em memória.** Acrescente ao mesmo arquivo:

```python
from banco import conectar
from rank_bm25 import BM25Okapi

def carregar_cursos():
    conexao = conectar()
    with conexao.cursor() as cursor:
        cursor.execute("SELECT codigo, nome, ementa FROM cursos")
        linhas = cursor.fetchall()
    conexao.close()
    return linhas

def montar_indice():
    """Prepara o texto de todos os cursos e monta o modelo BM25."""
    codigos = []
    documentos = []
    for codigo, nome, ementa in carregar_cursos():
        texto = f"{nome} {nome} {ementa}"   # o nome entra 2x para pesar mais
        codigos.append(codigo)
        documentos.append(preparar(texto))
    return codigos, documentos, BM25Okapi(documentos)

CODIGOS, DOCUMENTOS, MODELO = montar_indice()
```

> **Por que o nome entra duas vezes?** É a forma mais simples de dar mais peso ao título, equivalente ao `peso_nome=3` que você usou na Busca 2. É uma decisão de projeto, e **precisa estar declarada no artigo** — não é um detalhe escondido. Teste com uma, duas e três repetições, e veja qual dá a melhor nota.

> **Repare em uma diferença importante:** a Busca 3 lê os cursos **do MySQL** e monta o índice **na memória do Python**. Ou seja, o índice passa a viver **fora do banco**. Isso traz recursos novos, mas cria um problema que a Busca 2 não tem — se um curso mudar no banco, o índice em memória fica desatualizado até ser refeito. Guarde essa observação: ela vira uma das melhores discussões dos seus Resultados.

**3. Escreva a busca.** Ainda no mesmo arquivo:

```python
def buscar(termo, limite=20):
    """Busca 3: BM25 em Python, sobre radicais de palavras."""
    consulta = preparar(termo)
    if not consulta:
        return []

    notas = MODELO.get_scores(consulta)
    pares = [(nota, codigo) for nota, codigo in zip(notas, CODIGOS) if nota > 0]
    pares.sort(reverse=True)
    return [codigo for _nota, codigo in pares[:limite]]

if __name__ == "__main__":
    termo = input("Buscar: ")
    print(buscar(termo))
```

**4. Meça.** Acrescente em `avaliar.py`:

```python
    salvar(avaliar("buscadores.busca3_python", "busca3_v1_stemming"))
```

**5. Compare as três.** Atualize a tabela do diário. **O que você deve observar:** a Busca 3 empata ou ganha um pouco da Busca 2 na maioria das categorias, e **ganha claramente na categoria `plural`** — porque agora "costureiras" e "costureiro" têm o mesmo radical. Se for isso que acontecer, você acabou de medir o efeito do *stemming*, isoladamente. Anote.

E continua sem resolver o **erro de digitação**. Essa é a Sprint 6.

### Como saber que deu certo

- `preparar("Curso de Costureiras")` devolve `['costur']`.
- `python buscadores/busca3_python.py`, digitando `costureiras`, devolve cursos de costura.
- O `docs/resultados.csv` tem agora 90 linhas.

> **Se a Busca 3 vier pior que a Busca 2**, não entre em pânico e **não mexa no gabarito**. Verifique nesta ordem: (a) a lista está ordenada da maior nota para a menor? (b) o `preparar()` está sendo aplicado tanto nos cursos quanto na consulta? (c) a lista de palavras vazias não está jogando fora algo importante? Se ainda assim vier pior, **isso é um resultado legítimo** — leve para o orientador na reunião.

### Entrega da sprint

- [ ] `sem_acento`, `separar_palavras` e `preparar` escritas e testadas separadamente.
- [ ] Índice BM25 montado a partir dos dados do MySQL.
- [ ] `buscar()` funcionando, com a mesma assinatura das outras duas.
- [ ] Teste da repetição do nome (1×, 2×, 3×) feito e anotado.
- [ ] Busca 3 medida e salva.
- [ ] Tabela com as três buscas no diário.
- [ ] Tabela "o que cada peça resolve × o MySQL faz?" preenchida.

---

# Sprint 6 — 27/10 a 02/11/2026
## Busca 3, parte 2: erro de digitação e sinônimos

**O que você vai entregar:** a Busca 3 corrigindo o que a pessoa digitou errado e entendendo termos populares; e a medição do efeito de cada um desses dois recursos, **separadamente**.

**A ideia, em uma frase:** antes de buscar, olhar cada palavra digitada e perguntar "existe alguma palavra parecida no meu catálogo?" — se existir, trocar.

### Passo a passo

**1. Monte o vocabulário do catálogo.** Acrescente em `busca3_python.py`, depois de `montar_indice()`:

```python
def montar_vocabulario(documentos):
    """Todos os radicais que existem no catalogo, sem repetir."""
    vocabulario = set()
    for documento in documentos:
        vocabulario.update(documento)
    return sorted(vocabulario)

VOCABULARIO = montar_vocabulario(DOCUMENTOS)
```

**2. Escreva a correção de digitação.** Use o `difflib`, que **já vem com o Python**:

```python
import difflib

def corrigir(palavras, vocabulario, corte=0.8):
    """Troca cada palavra desconhecida pela mais parecida do catalogo.

    'exel' -> 'excel'. Palavras que ja existem passam sem alteracao.
    """
    corrigidas = []
    for palavra in palavras:
        if palavra in vocabulario:
            corrigidas.append(palavra)
            continue
        if len(palavra) < 4:
            corrigidas.append(palavra)     # palavra curta: nao arrisca
            continue
        parecidas = difflib.get_close_matches(palavra, vocabulario, n=1, cutoff=corte)
        corrigidas.append(parecidas[0] if parecidas else palavra)
    return corrigidas
```

Três decisões neste código, e as três vão para o artigo:

- **`corte=0.8`** — o quanto duas palavras precisam ser parecidas para serem trocadas. **Teste 0,7, 0,8 e 0,9 e meça cada um.** Valor baixo demais troca palavras que não deviam ser trocadas; alto demais não corrige nada. Achar esse ponto **medindo** é um resultado do trabalho;
- **`len(palavra) < 4`** — palavras curtas não são corrigidas, porque uma letra de diferença em palavra curta muda o sentido ("mala" e "mola" são coisas diferentes). Motores de busca profissionais fazem exatamente isso;
- **comparar com o vocabulário do catálogo**, e não com um dicionário de português: porque o que interessa não é se a palavra existe, é se ela **existe nos seus cursos**.

> O conceito por trás disso chama-se **distância de edição**, ou **distância de Levenshtein**: o número mínimo de letras a inserir, remover ou trocar para transformar uma palavra na outra. De `exel` para `excel` é uma inserção. Pesquise esse nome — ele é obrigatório no seu Referencial Teórico. **E registre que o MySQL não oferece nada equivalente**: é a diferença mais visível entre as duas abordagens.

**3. Escreva os sinônimos.** É um dicionário simples:

```python
SINONIMOS = {
    "faxina": "domestic",
    "limpeza": "domestic",
    "computador": "informat",
    "costura": "costur",
    # ... 10 a 15 entradas, no maximo
}

def aplicar_sinonimos(palavras):
    return [SINONIMOS.get(palavra, palavra) for palavra in palavras]
```

Repare que o **valor** é o radical, porque é isso que está no índice.

> **Cuidado sério, e isto conta no artigo:** é tentador cadastrar exatamente os sinônimos das suas 5 consultas de teste da categoria `sinonimo`. Isso é ajustar o buscador ao gabarito, e invalida a comparação. **Monte a lista pensando no domínio** — quais termos populares o público dos cursos FIC usaria —, limite-se a 10 ou 15 entradas, e **relate no artigo a nota com e sem sinônimos**. A nota sem sinônimos é a comparação limpa; a nota com sinônimos mostra o que o recurso consegue. Apresentar as duas é o que torna o resultado honesto.

**4. Junte tudo na função `buscar`:**

```python
def buscar(termo, limite=20, usar_correcao=True, usar_sinonimos=True):
    consulta = preparar(termo)
    if usar_sinonimos:
        consulta = aplicar_sinonimos(consulta)
    if usar_correcao:
        consulta = corrigir(consulta, VOCABULARIO)
    if not consulta:
        return []

    notas = MODELO.get_scores(consulta)
    pares = [(nota, codigo) for nota, codigo in zip(notas, CODIGOS) if nota > 0]
    pares.sort(reverse=True)
    return [codigo for _nota, codigo in pares[:limite]]
```

**5. Meça as quatro versões separadamente — é a parte mais importante da sprint.**

| Versão | Correção | Sinônimos | Rótulo em `resultados.csv` |
|---|---|---|---|
| 3.1 | não | não | `busca3_v1_stemming` (já medida na Sprint 5) |
| 3.2 | **sim** | não | `busca3_v2_correcao` |
| 3.3 | não | **sim** | `busca3_v3_sinonimos` |
| 3.4 | **sim** | **sim** | `busca3_v4_completa` |

O jeito mais simples de medir as variações é criar arquivinhos de três linhas que chamam a busca com os parâmetros certos. Por exemplo, `buscadores/busca3_v2.py`:

```python
from buscadores.busca3_python import buscar as buscar_completo

def buscar(termo, limite=20):
    return buscar_completo(termo, limite, usar_correcao=True, usar_sinonimos=False)
```

**Por que medir separadamente?** Porque assim você consegue dizer **quanto cada recurso rendeu sozinho**. Se medisse só a versão completa, saberia que melhorou, mas não saberia por causa de quê. Essa é a diferença entre um trabalho que descreve e um trabalho que explica — e é a razão de cada sprint acrescentar **uma coisa de cada vez**.

**6. Olhe o que mudou.** Você deve ver um salto na categoria `erro_digitacao` (de quase zero para um valor alto) e na `sinonimo`. Nas outras categorias, pouca coisa. **Anote as notas por categoria** — essa tabela é a figura principal do seu artigo.

### Como saber que deu certo

- `buscar("exel")` devolve cursos de informática / Excel.
- `buscar("faxina")` devolve cursos de serviços domésticos.
- `buscar("informatica basica")` continua devolvendo o que devolvia antes — ou seja, a correção não estragou o que já funcionava. **Confira isso, é importante.**
- O `docs/resultados.csv` tem agora 180 linhas.

> **Procure um caso em que a correção ESTRAGOU o resultado.** Ele existe: alguma palavra vai ser trocada por outra parecida e errada. Quando achar, **guarde**: mostrar onde a sua própria solução falha é o que impede o artigo de parecer propaganda, e é exatamente o que um avaliador procura.

### Entrega da sprint

- [ ] Correção de digitação funcionando, com o corte testado em 0,7, 0,8 e 0,9.
- [ ] Lista de 10 a 15 sinônimos, montada pelo domínio e não pelas consultas de teste.
- [ ] As quatro versões medidas separadamente e salvas.
- [ ] Tabela de P@5 por categoria, com as três buscas, montada no diário.
- [ ] Pelo menos um caso em que a correção errou, documentado.

---

# Sprint 7 — 03/11 a 09/11/2026
## A página web e a medição de tempo

**O que você vai entregar:** uma página simples em Django onde dá para digitar e ver o resultado das três buscas, e a medição de quanto cada uma demora.

Esta sprint tem duas metades independentes. **Se o tempo apertar, faça a Parte B primeiro** — ela é resultado do artigo; a página é a ligação com o projeto iFIC.

### Parte A — A página em Django

**1. Instale e crie o projeto.** Dentro de `kelly/`, com o ambiente virtual ativo:

```
pip install django
django-admin startproject site
cd site
python manage.py startapp busca
```

**2. Registre o app.** Em `site/site/settings.py`, na lista `INSTALLED_APPS`, acrescente `"busca",`.

**3. Escreva a view.** Em `site/busca/views.py`:

```python
import sys
from pathlib import Path
from django.shortcuts import render

# permite importar os buscadores que estao na pasta de cima
sys.path.insert(0, str(Path(__file__).resolve().parent.parent.parent))

from buscadores import busca1_like, busca2_fulltext, busca3_python

MOTORES = {
    "1": ("Busca 1 - LIKE", busca1_like),
    "2": ("Busca 2 - FULLTEXT do MySQL", busca2_fulltext),
    "3": ("Busca 3 - Python com recursos de linguagem", busca3_python),
}

def pagina(request):
    termo = request.GET.get("q", "")
    motor = request.GET.get("motor", "3")
    rotulo, modulo = MOTORES.get(motor, MOTORES["3"])
    codigos = modulo.buscar(termo) if termo else []
    return render(request, "busca/pagina.html", {
        "termo": termo,
        "motor": motor,
        "rotulo": rotulo,
        "codigos": codigos,
    })
```

**4. O template.** Crie `site/busca/templates/busca/pagina.html` com um formulário (um campo de texto, um seletor com as três buscas, um botão) e a lista de resultados. **Simples mesmo**: nada de CSS elaborado. O objeto do trabalho é a busca, não o visual.

**5. A rota.** Em `site/site/urls.py`, ligue a raiz (`""`) à view `pagina`.

**6. Rode:** `python manage.py runserver` e abra `http://127.0.0.1:8000/` no navegador.

> Você vai ver um aviso sobre migrações pendentes. **Pode ignorar**: este protótipo não usa os modelos do Django, ele conversa com o MySQL pelo `banco.py`. Se o aviso incomodar, rode `python manage.py migrate` uma vez — o Django vai criar as tabelas internas dele em um SQLite próprio, separado do seu catálogo, e isso não interfere em nada.

**7. Tire prints das três buscas respondendo à mesma consulta** e guarde em `docs/evidencias/`. Essa comparação lado a lado é uma ótima figura para o artigo.

### Parte B — Medir o tempo

**1. Como medir direito.** Tempo de computador varia a cada execução; um número só não significa nada. Para cada busca e cada consulta, rode **6 vezes**, jogue fora a primeira e fique com a **mediana** das outras cinco:

```python
import statistics
import time

def medir(modulo, termo, repeticoes=6):
    tempos = []
    for _ in range(repeticoes):
        inicio = time.perf_counter()
        modulo.buscar(termo)
        tempos.append((time.perf_counter() - inicio) * 1000)
    tempos = tempos[1:]                       # descarta o aquecimento
    return statistics.median(tempos), statistics.stdev(tempos)
```

Três coisas para explicar no artigo:

- **por que descartar a primeira:** a primeira execução ainda está abrindo conexão e lendo dados do disco; as seguintes já encontram tudo em memória. O MySQL mantém páginas de dados na memória (o *buffer pool*), então a primeira consulta é sempre a mais lenta. Isso se chama **aquecimento**;
- **por que mediana, e não média:** a mediana não é distorcida por uma execução esquisita, que acontece quando o Windows resolve fazer outra coisa no meio da medição;
- **o mesmo procedimento nas três buscas.** As Buscas 1 e 2 abrem conexão com o MySQL a cada chamada, e isso entra no tempo medido. É uma limitação, mas é **igual para as duas**, e a comparação é relativa. Declare isso.

**Antes de medir, feche o navegador e tudo o mais que estiver aberto.** E registre isso: faz parte do protocolo.

**2. Uma observação importante sobre a Busca 3.** Ela monta o índice **uma vez**, quando o módulo é importado, e depois responde rápido. Meça **as duas coisas separadamente**: (a) quanto tempo leva para montar o índice no início e (b) quanto tempo leva cada busca depois. São custos de natureza diferente, e essa distinção é exatamente o que separa uma busca que mora dentro do banco de uma busca em camada separada.

**3. Teste com catálogo maior.** Para responder "e quando o catálogo crescer?", gere uma cópia ampliada do catálogo repetindo os cursos com um sufixo no código (10× ou 20× o tamanho original) e refaça a medição de tempo das três buscas.

**O que você deve observar:** a Busca 1 (`LIKE '%termo%'`) demora proporcionalmente mais, porque o MySQL precisa ler todas as linhas — o índice comum não serve quando o texto procurado pode estar no meio do campo. As Buscas 2 e 3 crescem bem menos, porque usam índice invertido. Um gráfico com essas três linhas é uma das melhores figuras do artigo.

> **Não recalcule P@5 nem revocação no catálogo ampliado** — o gabarito não vale para ele. Ali só se mede tempo. Diga isso no artigo, senão parece esquecimento.

**4. Meça o espaço ocupado.** Rode, antes e depois de criar os índices `FULLTEXT`:

```sql
SELECT table_name, data_length, index_length
FROM information_schema.tables
WHERE table_schema = 'ific_busca';
```

A diferença em `index_length` é o custo do índice em disco.

> **Um aviso honesto:** o MySQL guarda os índices `FULLTEXT` do InnoDB em tabelas internas auxiliares, que podem não aparecer nesse número. Se o valor não mudar como você esperava, **não invente**: registre o que observou e diga no artigo que a medição do espaço do índice não pôde ser feita com precisão por essa razão. Relatar uma medição que não deu certo, explicando por quê, é ciência; forçar um número é o contrário.

### Como saber que deu certo

- A página abre no navegador, e trocar de busca no seletor muda os resultados.
- Você tem uma tabela com o tempo mediano das três buscas, nos dois tamanhos de catálogo.
- Você sabe dizer quanto tempo a Busca 3 leva para montar o índice.

### Entrega da sprint

- [ ] Página Django funcionando com as três buscas.
- [ ] Prints das três respondendo à mesma consulta.
- [ ] Tempos medidos com 6 repetições, mediana e desvio.
- [ ] Tempo de montagem do índice da Busca 3 medido.
- [ ] Medição com catálogo ampliado feita.
- [ ] Espaço dos índices medido (ou a impossibilidade da medição registrada).

---

# Sprint 8 — 10/11 a 16/11/2026
## Entender os erros, fazer os gráficos e documentar

**O que você vai entregar:** a rodada final de medições, os gráficos do artigo, a explicação de por que cada busca errou onde errou, e o `README.md`.

É nesta semana que o trabalho deixa de ser "três buscas programadas" e passa a ser um artigo com achado.

### Passo a passo

**1. Rode a bateria final, do zero, de uma vez só.** Renomeie o `docs/resultados.csv` atual para `docs/resultados_historico.csv` (não apague), recrie o banco e rode a avaliação das três buscas na mesma sessão. **É essa rodada que vai para o artigo**, e ela precisa ter sido feita toda no mesmo dia, na mesma máquina.

**2. Faça os gráficos por script.** Crie `graficos.py`, que lê o `docs/resultados.csv` e gera as figuras com `matplotlib`. **Gráfico feito por script é reproduzível; print de planilha não é.** Faça três:

- **Gráfico 1 — P@5 por busca:** três barras. É a figura mais simples e a que resume o trabalho;
- **Gráfico 2 — P@5 por categoria de consulta:** seis grupos (exato, genérico, sem acento, erro de digitação, plural, sinônimo), três barras em cada. **Esta é a figura mais importante do artigo**, porque mostra *onde* cada busca ganha, e não só que ganha;
- **Gráfico 3 — tempo × tamanho do catálogo:** três linhas.

Cuidados: escreva o que é cada eixo e a unidade; se o eixo vertical não começar em zero, avise na legenda.

Estrutura mínima para começar:

```python
import csv
import statistics
from collections import defaultdict
import matplotlib.pyplot as plt

with open("docs/resultados.csv", encoding="utf-8") as arquivo:
    linhas = list(csv.DictReader(arquivo))

medias = defaultdict(list)
for linha in linhas:
    medias[linha["busca"]].append(float(linha["p5"]))

nomes = list(medias.keys())
valores = [statistics.mean(medias[nome]) for nome in nomes]

plt.bar(nomes, valores)
plt.ylabel("Precisão nos 5 primeiros resultados (P@5)")
plt.title("Qualidade da busca por abordagem")
plt.savefig("docs/evidencias/grafico1_p5.png", dpi=150, bbox_inches="tight")
```

**3. Faça a análise dos erros — é aqui que está o valor do trabalho.** Pegue as 10 consultas com pior P@5 em cada busca e responda, para cada uma, **por quê**. Monte uma tabela assim:

| Consulta | Busca | O que devolveu | Por quê |
|---|---|---|---|
| `exel` | 1 e 2 | nada | nenhuma das duas trata erro de digitação |
| `costureiras` | 1 e 2 | nada | o índice do MySQL guarda a palavra inteira, não o radical |
| `TI` | 2 | nada | palavra de 2 letras, abaixo do `innodb_ft_min_token_size` |
| `faxina` | 1, 2 e 3 sem sinônimo | nada | a palavra não existe no catálogo; só resolve com sinônimo |
| `curso de excel` | 1 | resultados sem relação | o `LIKE` procura a frase inteira e não ordena por relevância |
| (o seu caso) | 3 | curso errado | a correção trocou por uma palavra parecida e errada |

**Uma tabela dessas vale mais que dez parágrafos.** Ela transforma número em explicação. E cada "por quê" usa um conceito do seu Referencial Teórico — é assim que as duas seções se amarram.

**Inclua obrigatoriamente pelo menos um caso em que a Busca 3 perdeu.** Você já encontrou um na Sprint 6. Mostrá-lo é o que dá credibilidade ao resto.

**4. Escreva o `README.md` da sua subpasta.** Ele precisa permitir que outra pessoa repita tudo. Escreva na ordem em que a pessoa faria:

1. o que precisa ter: Python 3.x e acesso a um servidor MySQL 8;
2. como criar o ambiente virtual e instalar (`pip install -r requirements.txt`);
3. como preencher o `config.py` a partir do `config_exemplo.py`;
4. como criar o banco e os índices (`python criar_banco.py`);
5. como testar cada busca;
6. como rodar a avaliação (`python avaliar.py`);
7. como gerar os gráficos (`python graficos.py`);
8. como abrir a página web;
9. o que tem em cada pasta.

**Teste o seu próprio README:** apague a pasta `.venv`, derrube o banco (`DROP DATABASE ific_busca`) e siga o seu texto do zero. É a única forma de saber que ele está completo.

**5. Limpe a subpasta.** Não deixe no repositório: `.venv/`, `__pycache__/`, `config.py` (com a senha!), arquivos de teste soltos. Rode `git status` e confira se aparece algum arquivo fora de `kelly/` — se aparecer, **não envie** e chame o orientador.

**6. Monte a apresentação.** Dez minutos: o problema (com um exemplo real do seu catálogo), as três buscas, o Gráfico 2 (por categoria), a tabela de erros, e a recomendação para o iFIC.

### Como saber que deu certo

- Os três gráficos estão em `docs/evidencias/`, gerados pelo `graficos.py`.
- A tabela de erros está pronta, com pelo menos uma falha da Busca 3.
- Você conseguiu seguir o seu próprio `README.md` do zero.

### Entrega da sprint

- [ ] Bateria final rodada de uma vez só.
- [ ] `graficos.py` comitado, gerando os três gráficos.
- [ ] Tabela de análise de erros completa.
- [ ] `README.md` escrito e testado.
- [ ] Subpasta limpa, **sem o `config.py`**.
- [ ] Apresentação montada.

---

## Quadro-resumo das sprints

| Sprint | Período | O que entrega | Conceitos novos |
|---|---|---|---|
| 1 | 22/09 a 28/09 | Ambiente Python conversando com o MySQL | ambiente virtual, `pip`, driver, collation |
| 2 | 29/09 a 05/10 | Catálogo no MySQL e Busca 1 | CSV, SQL, `LIKE`, limitações da busca simples |
| 3 | 06/10 a 12/10 | Consultas, gabarito e script de notas | Cranfield, P@5, revocação, MRR |
| 4 | 13/10 a 19/10 | Busca 2 (`FULLTEXT` do MySQL) | índice invertido, relevância, limites do MySQL |
| 5 | 20/10 a 26/10 | Busca 3 com radical das palavras | tokenização, palavras vazias, *stemming*, BM25 |
| 6 | 27/10 a 02/11 | Busca 3 com correção e sinônimos | distância de edição, sinônimos, medição isolada |
| 7 | 03/11 a 09/11 | Página web e medição de tempo | Django, mediana, aquecimento, crescimento do tempo |
| 8 | 10/11 a 16/11 | Gráficos, análise de erros e README | interpretação dos dados, reprodutibilidade |

---

## Riscos e planos B

| Risco | Sinal de alerta | O que fazer |
|---|---|---|
| Sem permissão para criar banco no MySQL | Sprint 1 travada | Pedir que criem o banco `ific_busca` com permissão de criar tabelas. **Resolver na primeira semana** |
| `pip install` bloqueado no laboratório | Sprint 1 travada | Resolver com o orientador **na primeira semana**. Em último caso, trabalhar em máquina própria e declarar isso no artigo |
| MySQL é 5.7, e não 8 | `verificar_ambiente.py` acusa | Trocar a collation para `utf8mb4_unicode_ci`. O resto funciona igual — só registre a versão no artigo |
| Git não instalado | Sprint 1 | Combinar entrega pela página do GitHub, no navegador |
| Montar o catálogo consome a sprint inteira | Sprint 2 acabando sem CSV pronto | Reduzir para 150 cursos e seguir. Catálogo menor é limitação declarada; catálogo inexistente é trabalho parado |
| Montar o gabarito consome a sprint inteira | Sprint 3 acabando sem `avaliar.py` | Reduzir para 18 consultas, **mantendo as 6 categorias** (3 de cada). Categoria importa mais que quantidade |
| A Busca 2 devolve quase tudo vazio | Sprint 4 | Conferir se os índices foram criados (`SHOW INDEX FROM cursos`) e se as palavras têm 3 letras ou mais |
| A Busca 3 sai pior que a Busca 2 | Sprint 5 | Conferir ordenação, `preparar()` e palavras vazias. Se persistir, é resultado legítimo — leve ao orientador |
| Django atrasa | Sprint 7 acabando sem a página | Entregar a medição de tempo (que é resultado) e declarar a interface web como trabalho futuro |

**Se algo tiver de ser cortado, corte largura, não profundidade.** É melhor ter 18 consultas bem julgadas e três buscas bem medidas do que 40 consultas com gabarito no chute. O que **não** pode faltar é o gabarito, as três notas e a análise por categoria — isso é o trabalho.

---

## Se sobrar tempo (opcional)

- **E1.** Testar o **modo booleano** do MySQL (`IN BOOLEAN MODE`) com expansão de prefixo (`informatica*`) e medir se ele ajuda nos plurais — é a coisa mais próxima de um *stemming* que o MySQL oferece sem mexer no servidor.
- **E2.** Implementar uma rede de segurança na Busca 2: quando o `FULLTEXT` não devolve nada, cair para o `LIKE`. Medir com e sem, e discutir o compromisso entre precisão e não deixar a tela vazia.
- **E3.** Implementar "você quis dizer...?", mostrando na tela a consulta corrigida.
- **E4.** Testar outros valores de corte da correção (0,6 a 0,95) e montar um gráfico do efeito.
- **E5.** Comparar o radicalizador do `snowballstemmer` com o algoritmo RSLP (removedor de sufixos da língua portuguesa) e medir a diferença.
- **E6.** Medir se cursos com ementa curta são encontrados menos que cursos com ementa longa.

---

## Relação com o artigo

O desenvolvimento e a escrita andam juntos (ver `01_kelly_ific_tarefas_escrita.md`):

| Seção do artigo | Sprints que geram o conteúdo |
|---|---|
| Referencial Teórico | leituras das Sprints 3 a 6 (Cranfield, métricas, índice invertido, *stemming*, distância de edição) |
| Metodologia | 3 (consultas, gabarito e protocolo) |
| Materiais e Métodos | 1, 2, 4, 5 e 6 (ferramentas, catálogo, como cada busca foi feita) |
| Resultados | 4, 5, 6 e 7 (as notas e os tempos) e 8 (análise de erros) |
| Conclusão | `docs/diario.md` acumulado nas oito sprints |

**Nunca apague uma linha de `docs/resultados.csv`, e nunca mude o gabarito depois da Sprint 3.** A confiabilidade do seu trabalho inteiro está nesses dois arquivos.
