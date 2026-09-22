# Plano de tarefas de desenvolvimento – Kaio (Técnico Integrado em Informática)

**Projeto pai:** iFIC – Desenvolvimento de Funcionalidades de Autenticação, Administração e Gerenciamento de Cursos de Formação Inicial e Continuada (ver `.llm/ific/projeto.md`).

**Temática escolhida:** T1 – Validador e importador de planilhas de cursos FIC (ver `.llm/ific/tematicas.md`).

**Perfil do aluno:** 1 aluno do Técnico Integrado em Informática, com conhecimentos básicos de Python e em treinamento. Por isso as primeiras sprints são propositalmente pequenas: o objetivo inicial é que ele se acostume com o fluxo de trabalho (Git, ambiente virtual, execução de scripts) antes de aumentar a dificuldade.

**Duração:** 8 sprints de 1 semana (22/09/2026 a 16/11/2026).

**Onde o trabalho acontece:** o **repositório de treinamento do projeto já existe** e é compartilhado com os outros alunos. Você **não vai criar repositório nenhum**. Todo o seu trabalho fica dentro de **uma única subpasta sua** nesse repositório:

```
<repositorio-de-treinamento>/
├── ...              ← pastas de outros alunos (não mexa)
└── kaio/            ← a sua subpasta: tudo o que você fizer fica aqui dentro
```

Confirme com o orientador o **endereço do repositório** e o **nome exato da sua subpasta** antes de começar a Sprint 1. Daqui em diante, todos os caminhos citados neste documento (`src/`, `dados/`, `docs/`...) são **relativos à sua subpasta**.

---

## Visão geral do produto a ser construído

Ao final das 8 sprints, o aluno deve entregar uma ferramenta de linha de comando em Python que:

1. lê uma planilha de cursos FIC (`.csv` e `.xlsx`);
2. valida cada linha segundo um conjunto de regras;
3. gera um **relatório de erros**, indicando linha, coluna, regra violada e valor encontrado;
4. gera uma **planilha limpa**, apenas com as linhas válidas;
5. importa as linhas válidas para um banco **SQLite**;
6. é validado por **medição**: comparação do relatório com um gabarito de erros conhecidos e medição do tempo de processamento para 100, 1.000 e 10.000 linhas.

### Formato da planilha (definido na Sprint 2, usado até o fim)

| Coluna | Tipo | Exemplo |
|---|---|---|
| `codigo` | texto, único | `FIC-2026-001` |
| `nome_curso` | texto | `Informática Básica` |
| `campus` | texto (lista fechada) | `Natal-Central` |
| `eixo_tecnologico` | texto | `Informação e Comunicação` |
| `carga_horaria` | inteiro > 0 | `160` |
| `turno` | texto (lista fechada) | `noturno` |
| `vagas` | inteiro > 0 | `30` |
| `data_inicio` | data `DD/MM/AAAA` | `02/03/2026` |
| `data_fim` | data `DD/MM/AAAA` | `30/06/2026` |

### Regras de validação (implementadas ao longo das Sprints 2, 3 e 4)

| Código | Regra |
|---|---|
| R01 | Campo obrigatório não pode estar vazio (todas as colunas são obrigatórias) |
| R02 | `codigo` não pode se repetir na planilha |
| R03 | `carga_horaria` deve ser um número inteiro maior que zero |
| R04 | `vagas` deve ser um número inteiro maior que zero |
| R05 | `turno` deve estar na lista permitida (matutino, vespertino, noturno, integral) |
| R06 | `data_inicio` e `data_fim` devem estar no formato `DD/MM/AAAA` e ser datas reais |
| R07 | `data_fim` deve ser posterior a `data_inicio` |
| R08 | `campus` deve estar na lista de campi do IFRN |
| R09 | `nome_curso` deve ter pelo menos 5 caracteres |
| R10 | A planilha deve conter exatamente as colunas esperadas (nem faltando, nem com nome errado) |

> **Regra de ouro do projeto:** nenhum dado real de pessoas. Todos os dados de teste são fictícios, gerados pelo próprio aluno (LGPD, Lei nº 13.709/2018).

---

## Combinados gerais (valem para todas as sprints)

- **Repositório:** o repositório de treinamento já existe e é compartilhado. Não crie outro. Trabalhe **somente dentro da sua subpasta**.
- **Commits:** pelo menos 3 commits por sprint, com mensagens curtas em português descrevendo o que foi feito (ex.: `Adiciona validação de carga horária`). Commit com mensagem `atualizações` não conta.
- **Reunião semanal:** no início de cada sprint, o aluno apresenta o que foi feito na sprint anterior rodando o código na frente do orientador.
- **Sempre que travar por mais de 40 minutos no mesmo erro, peça ajuda.** Travar faz parte; ficar travado a semana inteira em silêncio, não.
- **Print de tudo:** ao final de cada sprint, salvar uma captura de tela do terminal mostrando o programa funcionando, em uma pasta `docs/evidencias/` (dentro da sua subpasta). Essas imagens serão usadas no capítulo de Resultados do artigo.

### Convivência em repositório compartilhado

Como o repositório é usado por mais de uma pessoa, estas regras valem o tempo todo:

1. **Só altere arquivos da sua subpasta.** Nunca edite, mova ou apague arquivo de outro aluno. Se achar que precisa mexer em algo fora dela, fale com o orientador antes.
2. **Sempre comece o dia com `git pull`.** Assim você já parte da versão mais recente e evita conflito.
3. **Comite apenas o que é seu.** Prefira `git add kaio/` (o nome da sua subpasta) a `git add .`, que varre o repositório inteiro e pode levar junto alteração de outra pessoa.
4. **Não comite `.venv/`, banco de dados (`.db`) nem planilhas geradas automaticamente.** Eles são pesados, mudam a cada execução e sujam o histórico de todo mundo.
5. **Se aparecer conflito (`CONFLICT`), não tente adivinhar.** Pare e chame o orientador. Conflito mal resolvido apaga trabalho alheio.
6. **Dê `git push` no fim de cada dia de trabalho.** Código que só existe na sua máquina não conta como entregue, e o orientador não consegue acompanhar.

---

# Sprint 1 — 22/09 a 28/09/2026
## Preparar o ambiente e ler o primeiro arquivo

**Objetivo da sprint:** ter o ambiente funcionando, a sua subpasta criada no repositório e um script Python que abre um arquivo CSV e mostra o conteúdo na tela. Nada além disso.

### Tarefas

1. Instalar Python 3.12 (ou superior) e o Visual Studio Code, com a extensão oficial de Python.
2. Pedir ao orientador o endereço do **repositório de treinamento** e o acesso de escrita a ele.
3. Clonar o repositório para o computador e criar **a sua subpasta** dentro dele, com a estrutura de pastas inicial.
4. Criar e ativar um ambiente virtual (`venv`) dentro da sua subpasta.
5. Criar manualmente uma planilha `cursos_exemplo.csv` com 10 linhas fictícias, seguindo as colunas da tabela acima.
6. Escrever o script `ler_planilha.py`, que abre o CSV e imprime cada linha no terminal.
7. Fazer o primeiro `commit` e `push`, comitando apenas os arquivos da sua subpasta.

### Ajuda / direcionamento

**Clonar o repositório (uma única vez):**

```
git clone <endereço-do-repositório-de-treinamento>
cd <pasta-do-repositório>
```

**Estrutura a criar dentro da sua subpasta:**

```
<repositório-de-treinamento>/
└── kaio/                        ← a sua subpasta (só mexa aqui)
    ├── dados/
    │   └── cursos_exemplo.csv
    ├── docs/
    │   └── evidencias/
    ├── src/
    │   └── ler_planilha.py
    ├── .gitignore
    └── README.md
```

O `README.md` e o `.gitignore` acima são **os da sua subpasta**, e não os da raiz do repositório. O repositório já tem os dele; não os altere.

**Ambiente virtual (no terminal, dentro da sua subpasta):**

```
cd kaio
python -m venv .venv
.venv\Scripts\activate      (Windows)
source .venv/bin/activate   (Linux/Mac)
```

Quando o ambiente estiver ativo, aparece `(.venv)` no começo da linha do terminal. Crie o arquivo `kaio/.gitignore` contendo as linhas abaixo, para que esses arquivos **não** subam para o repositório compartilhado:

```
.venv/
__pycache__/
*.db
saida/
```

**Como criar o CSV:** faça no Excel ou no LibreOffice e salve como "CSV (separado por vírgulas)" — ou escreva direto no VS Code, que é mais simples. A primeira linha é o cabeçalho:

```
codigo,nome_curso,campus,eixo_tecnologico,carga_horaria,turno,vagas,data_inicio,data_fim
FIC-2026-001,Informática Básica,Natal-Central,Informação e Comunicação,160,noturno,30,02/03/2026,30/06/2026
```

Coloque 10 linhas, todas **corretas** por enquanto. Os erros entram na Sprint 3.

**Para ler o CSV,** use o módulo `csv`, que já vem com o Python (não precisa instalar nada). Pesquise por `csv.DictReader python exemplo`. A ideia é:

- abrir o arquivo com `open(...)` usando `encoding="utf-8"`;
- criar um `csv.DictReader` a partir dele;
- percorrer com um `for` e dar `print` em cada linha.

O `DictReader` devolve cada linha como um **dicionário**, em que a chave é o nome da coluna. Ou seja, `linha["nome_curso"]` devolve o nome do curso. Isso vai facilitar muito o resto do projeto — por isso ele, e não o `csv.reader` comum.

**Comandos de Git desta sprint** (rodados a partir da raiz do repositório):

```
git pull
git add kaio/
git commit -m "Cria estrutura inicial da subpasta e leitura do CSV"
git push
```

Repare no `git add kaio/` em vez de `git add .`: assim você comita **só o que é seu**. Antes de comitar, confira com `git status` que nenhum arquivo fora da sua subpasta aparece na lista.

### Entrega da sprint

- [ ] Sua subpasta criada no repositório de treinamento, com a estrutura de pastas.
- [ ] `python src/ler_planilha.py` imprime as 10 linhas do CSV no terminal.
- [ ] `.gitignore` da subpasta ignorando `.venv/`, `__pycache__/`, `*.db` e `saida/`.
- [ ] Pelo menos 1 commit enviado (`push`), contendo apenas arquivos da sua subpasta.

### Cuidado comum

Se aparecerem caracteres estranhos no lugar de acentos (`InformÃ¡tica`), o problema é de **codificação**. Salve o CSV como UTF-8 e use `encoding="utf-8"` no `open`. Se o Excel tiver salvado em outra codificação, teste `encoding="utf-8-sig"` ou `encoding="latin-1"`. Anote o que funcionou — isso vira uma dificuldade interessante para relatar na Conclusão do artigo.

---

# Sprint 2 — 29/09 a 05/10/2026
## Organizar o código em funções e definir o formato oficial da planilha

**Objetivo da sprint:** parar de escrever "código solto" e aprender a separar o programa em funções. Ao final, o script deve ler a planilha, contar as linhas e mostrar um resumo.

### Tarefas

1. Criar o arquivo `src/leitor.py` com uma função `ler_csv(caminho)` que devolve uma **lista de dicionários**.
2. Criar o arquivo `src/config.py` com as constantes do projeto: lista de colunas obrigatórias, lista de turnos permitidos e lista de campi do IFRN.
3. Criar o arquivo `src/main.py`, que chama as funções e mostra um resumo: nome do arquivo lido, quantidade de linhas e nomes das colunas encontradas.
4. Implementar a **regra R10**: verificar se a planilha tem exatamente as colunas esperadas. Se faltar alguma, mostrar uma mensagem clara e encerrar.
5. Escrever o `README.md` **da sua subpasta** explicando o que é o projeto e como executá-lo.

### Ajuda / direcionamento

**O que é "separar em funções" e por que fazer isso:** em vez de um arquivo único com tudo misturado, cada arquivo passa a ter uma responsabilidade. `leitor.py` só sabe ler arquivos; `config.py` só guarda as listas fixas; `main.py` é o "maestro" que chama os outros. Isso vai ser essencial nas próximas sprints, quando o validador crescer — e é exatamente o tipo de decisão de projeto que você vai descrever no capítulo de Materiais e Métodos do artigo.

**Modelo do `config.py`:**

```python
COLUNAS_ESPERADAS = [
    "codigo", "nome_curso", "campus", "eixo_tecnologico",
    "carga_horaria", "turno", "vagas", "data_inicio", "data_fim",
]

TURNOS_PERMITIDOS = ["matutino", "vespertino", "noturno", "integral"]

CAMPI_IFRN = [
    "Natal-Central", "Natal-Zona Norte", "Natal-Zona Leste",
    "Parnamirim", "São Gonçalo do Amarante", "Mossoró", "Caicó",
    "Currais Novos", "Santa Cruz", "Ipanguaçu", "João Câmara",
    "Macau", "Pau dos Ferros", "Apodi", "Nova Cruz",
]
```

> Confirme a lista de campi na página oficial do IFRN antes de fixá-la. No artigo, essa lista precisa de uma referência.

**Modelo da função de leitura:**

```python
import csv

def ler_csv(caminho):
    """Lê um arquivo CSV e devolve uma lista de dicionários."""
    with open(caminho, encoding="utf-8", newline="") as arquivo:
        leitor = csv.DictReader(arquivo)
        return list(leitor)
```

**Para a regra R10,** compare a lista de colunas do arquivo com `COLUNAS_ESPERADAS`. Pesquise sobre o método `.keys()` de dicionário e sobre comparação de listas em Python. Uma forma simples:

```python
def validar_colunas(linhas):
    colunas_encontradas = list(linhas[0].keys())
    faltando = [c for c in COLUNAS_ESPERADAS if c not in colunas_encontradas]
    return faltando   # lista vazia significa que está tudo certo
```

Essa construção `[c for c in lista if condição]` chama-se **list comprehension**. Vale a pena pesquisar e entender agora, porque ela vai aparecer várias vezes até o fim do projeto.

**Para importar um arquivo no outro,** dentro da pasta `src/`:

```python
from config import COLUNAS_ESPERADAS, TURNOS_PERMITIDOS
from leitor import ler_csv
```

Se der `ModuleNotFoundError`, execute a partir da pasta `src` (`cd src` e depois `python main.py`) ou pesquise sobre "python executar módulo mesma pasta".

### Entrega da sprint

- [ ] Código separado em `config.py`, `leitor.py` e `main.py`.
- [ ] `python main.py ../dados/cursos_exemplo.csv` mostra um resumo da planilha.
- [ ] Se uma coluna for renomeada de propósito, o programa avisa qual está faltando.
- [ ] `README.md` escrito com instruções de instalação e execução.

---

# Sprint 3 — 06/10 a 12/10/2026
## Primeiras regras de validação (campos obrigatórios e números)

**Objetivo da sprint:** implementar as regras R01, R03 e R04 e produzir a primeira lista de erros encontrados.

### Tarefas

1. Criar o arquivo `src/validadores.py`.
2. Implementar `esta_vazio(valor)` → regra R01.
3. Implementar `inteiro_positivo(valor)` → regras R03 e R04.
4. Criar a função `validar_linha(linha, numero_linha)`, que aplica essas regras e devolve uma **lista de erros** daquela linha.
5. Criar a função `validar_planilha(linhas)`, que percorre todas as linhas e junta todos os erros.
6. Fazer `main.py` imprimir os erros encontrados no formato: `Linha 7 | carga_horaria | R03 | valor encontrado: 'abc'`.
7. Editar `cursos_exemplo.csv` inserindo uns 4 erros propositais para testar.

### Ajuda / direcionamento

**Como representar um erro:** use um dicionário. Fica fácil de imprimir agora e de gravar em arquivo depois (Sprint 5):

```python
def novo_erro(numero_linha, coluna, regra, mensagem, valor):
    return {
        "linha": numero_linha,
        "coluna": coluna,
        "regra": regra,
        "mensagem": mensagem,
        "valor": valor,
    }
```

**Validação de campo vazio:** cuidado com o espaço em branco. `" "` parece preenchido, mas não é. Use `.strip()` para remover os espaços das pontas antes de testar. Também trate o caso de o valor ser `None`.

```python
def esta_vazio(valor):
    return valor is None or valor.strip() == ""
```

**Validação de inteiro positivo:** o CSV devolve tudo como **texto**. `"160"` é texto, não número. Para converter, use `int(valor)` — mas se o valor for `"abc"`, o `int()` lança um erro e o programa quebra. Por isso use `try/except`:

```python
def inteiro_positivo(valor):
    try:
        numero = int(valor.strip())
    except (ValueError, AttributeError):
        return False
    return numero > 0
```

Pesquise sobre **tratamento de exceções em Python (`try` / `except`)**. É um dos conceitos mais importantes desta sprint, e você vai precisar explicá-lo no artigo.

**Estrutura da validação da linha:**

```python
def validar_linha(linha, numero_linha):
    erros = []
    for coluna in COLUNAS_ESPERADAS:
        if esta_vazio(linha.get(coluna)):
            erros.append(novo_erro(numero_linha, coluna, "R01",
                                   "Campo obrigatório vazio", linha.get(coluna)))
    if not inteiro_positivo(linha.get("carga_horaria")):
        erros.append(...)
    # ... e assim por diante
    return erros
```

**Atenção ao número da linha.** Se o cabeçalho é a linha 1 da planilha, a primeira linha de dados é a linha 2. O relatório precisa apontar o número que a pessoa vê quando abre a planilha no Excel, senão ela não acha o erro. Use `enumerate(linhas, start=2)`.

**Decisão de projeto para registrar:** quando um campo está vazio (R01), ele também vai falhar em R03 ou R05, gerando dois erros para o mesmo problema. Decida se a linha para na primeira falha de cada coluna ou se acumula todas, e **anote a decisão com a justificativa** — isso é conteúdo direto para o capítulo de Resultados, e afeta a contagem de falsos positivos na Sprint 6.

### Entrega da sprint

- [ ] `validadores.py` com as funções funcionando.
- [ ] O programa lista todos os erros de R01, R03 e R04 da planilha de exemplo.
- [ ] Nenhum erro na planilha faz o programa quebrar (nada de `Traceback` na tela).
- [ ] Print do terminal salvo em `docs/evidencias/`.

---

# Sprint 4 — 13/10 a 19/10/2026
## Regras de datas, listas fechadas e código duplicado

**Objetivo da sprint:** completar o conjunto de regras (R02, R05, R06, R07, R08, R09). Ao final desta sprint, o validador está **funcionalmente completo** para CSV.

### Tarefas

1. Implementar `converter_data(valor)` → regra R06, usando o módulo `datetime`.
2. Implementar a comparação `data_fim > data_inicio` → regra R07.
3. Implementar `valor_em_lista(valor, lista)` → regras R05 (turno) e R08 (campus).
4. Implementar a detecção de `codigo` duplicado → regra R02 (é a única regra que olha a planilha inteira, e não uma linha isolada).
5. Implementar o tamanho mínimo de `nome_curso` → regra R09.
6. Atualizar `cursos_exemplo.csv` para ter pelo menos um exemplo de cada tipo de erro.

### Ajuda / direcionamento

**Datas:** use `datetime.strptime`, que transforma texto em data. Se o texto não for uma data válida, ele lança `ValueError` — de novo o `try/except`:

```python
from datetime import datetime

def converter_data(valor):
    """Devolve um objeto date, ou None se o valor não for uma data válida."""
    try:
        return datetime.strptime(valor.strip(), "%d/%m/%Y").date()
    except (ValueError, AttributeError):
        return None
```

O `%d/%m/%Y` é o "molde" do formato. Teste com `31/02/2026`: é uma data **impossível** (fevereiro não tem 31 dias) e o `strptime` corretamente a rejeita. Esse é um ótimo exemplo para colocar no artigo, porque mostra a diferença entre "está no formato certo" e "é uma data que existe".

**Comparação de datas:** depois de convertidas, datas podem ser comparadas com `>` e `<` normalmente. Mas só compare se **as duas** forem válidas — senão você estará comparando com `None` e o programa quebra.

**Listas fechadas:** compare sempre em minúsculas e sem espaços, para que `"Noturno "` e `"noturno"` sejam aceitos como o mesmo valor:

```python
def valor_em_lista(valor, lista):
    if valor is None:
        return False
    return valor.strip().lower() in [item.lower() for item in lista]
```

**Códigos duplicados:** percorra a planilha guardando os códigos já vistos em um dicionário que liga o código ao número da linha onde ele apareceu pela primeira vez. Se o código já estiver no dicionário, é duplicata — e a mensagem de erro fica muito mais útil se disser *onde* ele apareceu antes: `"Código já utilizado na linha 12"`.

```python
def validar_codigos_duplicados(linhas):
    erros = []
    vistos = {}
    for numero_linha, linha in enumerate(linhas, start=2):
        codigo = (linha.get("codigo") or "").strip()
        if codigo in vistos:
            erros.append(novo_erro(numero_linha, "codigo", "R02",
                f"Código já utilizado na linha {vistos[codigo]}", codigo))
        else:
            vistos[codigo] = numero_linha
    return erros
```

Pesquise sobre **dicionários em Python** (`dict`) e sobre por que buscar em um dicionário é muito mais rápido do que buscar em uma lista. Esse detalhe vale um parágrafo no artigo, quando você for falar do tempo de processamento.

### Entrega da sprint

- [ ] Todas as 10 regras (R01 a R10) implementadas e funcionando.
- [ ] A planilha de exemplo contém pelo menos um erro de cada regra, e o programa detecta todos.
- [ ] Cada erro é reportado com linha, coluna, código da regra, mensagem e valor encontrado.

---

# Sprint 5 — 20/10 a 26/10/2026
## Suporte a `.xlsx`, relatório em arquivo e planilha limpa

**Objetivo da sprint:** o programa deixa de só reclamar na tela e passa a **entregar arquivos**: um relatório de erros e uma planilha pronta para importação.

### Tarefas

1. Instalar a biblioteca `openpyxl` e registrá-la em um arquivo `requirements.txt`.
2. Criar a função `ler_xlsx(caminho)` em `leitor.py`, devolvendo o mesmo formato (lista de dicionários) que o `ler_csv`.
3. Criar a função `ler_planilha(caminho)`, que escolhe o leitor certo conforme a extensão do arquivo.
4. Criar `src/relatorio.py` com a função `gravar_relatorio(erros, caminho_saida)`, que grava os erros em um CSV.
5. Criar a função `gravar_planilha_limpa(linhas_validas, caminho_saida)`, que grava um CSV apenas com as linhas sem nenhum erro.
6. Imprimir no terminal um resumo final: total de linhas, linhas válidas, linhas com erro e total de erros por regra.

### Ajuda / direcionamento

**Instalação e `requirements.txt`:**

```
pip install openpyxl
pip freeze > requirements.txt
```

O `requirements.txt` fica **dentro da sua subpasta** (`kaio/requirements.txt`), e não na raiz do repositório: cada aluno tem as suas dependências. Ele é o que permite outra pessoa reproduzir seu ambiente — e a reprodutibilidade é um requisito do TCC. Comite esse arquivo.

**Leitura de `.xlsx`:** o `openpyxl` não devolve dicionários prontos como o `DictReader`. Ele devolve linhas de células. O caminho é: ler a primeira linha como cabeçalho e montar os dicionários manualmente com `zip`.

```python
from openpyxl import load_workbook

def ler_xlsx(caminho):
    planilha = load_workbook(caminho, data_only=True)
    aba = planilha.active
    linhas = list(aba.iter_rows(values_only=True))
    cabecalho = [str(c).strip() if c is not None else "" for c in linhas[0]]
    resultado = []
    for valores in linhas[1:]:
        valores_texto = ["" if v is None else str(v).strip() for v in valores]
        resultado.append(dict(zip(cabecalho, valores_texto)))
    return resultado
```

Pesquise sobre a função `zip()`. Ela junta duas listas em pares — exatamente o que é preciso para casar cabeçalho com valores.

**Armadilha importante do Excel:** se a coluna estiver formatada como data, o `openpyxl` devolve um objeto `datetime`, e não o texto `"02/03/2026"`. Ao converter com `str()`, você vai receber `"2026-03-02 00:00:00"`, e a sua regra R06 vai reprovar uma data que está correta. Decida como tratar isso (por exemplo, detectar se o valor já é um `datetime` e formatá-lo com `.strftime("%d/%m/%Y")`) e **anote a decisão**: esse é um achado técnico legítimo, que merece aparecer nos Resultados do artigo.

**Escolha do leitor pela extensão:**

```python
import os

def ler_planilha(caminho):
    extensao = os.path.splitext(caminho)[1].lower()
    if extensao == ".csv":
        return ler_csv(caminho)
    if extensao == ".xlsx":
        return ler_xlsx(caminho)
    raise ValueError(f"Formato não suportado: {extensao}")
```

**Resumo por regra:** use um dicionário contando quantas vezes cada código de regra apareceu na lista de erros. Pesquise sobre `collections.Counter` — resolve em uma linha.

### Entrega da sprint

- [ ] O mesmo comando funciona para `.csv` e para `.xlsx`.
- [ ] `saida/relatorio_erros.csv` é gerado com uma linha por erro.
- [ ] `saida/cursos_limpos.csv` é gerado apenas com as linhas válidas.
- [ ] O terminal mostra o resumo com a contagem de erros por regra.
- [ ] `requirements.txt` comitado.

---

# Sprint 6 — 27/10 a 02/11/2026
## Massa de testes com gabarito

**Objetivo da sprint:** construir a base da validação científica do trabalho. Sem esta sprint, o artigo não tem como provar que o validador funciona.

### Tarefas

1. Criar `src/gerador_massa.py`, um script que gera uma planilha fictícia de cursos FIC com a quantidade de linhas que for pedida.
2. Fazer o gerador inserir erros **de propósito**, em posições controladas, e gravar um arquivo de **gabarito** com a lista exata dos erros inseridos.
3. Gerar três massas: 100, 1.000 e 10.000 linhas, cada uma com cerca de 20% de linhas com erro.
4. Criar `src/comparador.py`, que compara o relatório do validador com o gabarito e calcula: **acertos** (erros detectados corretamente), **falsos negativos** (erros que passaram despercebidos) e **falsos positivos** (alarmes falsos).
5. Rodar a comparação nas três massas e anotar os números em `docs/resultados.md`.

### Ajuda / direcionamento

**A ideia do gabarito.** Você não pode afirmar no artigo que "o validador funciona" só porque ele imprimiu alguns erros. Você precisa saber, de antemão, **exatamente** quais erros existem na planilha. Por isso o gerador deve trabalhar assim: primeiro cria uma linha perfeitamente válida; depois sorteia se aquela linha vai receber um erro; se for receber, sorteia qual regra vai ser violada, estraga o campo correspondente e **registra no gabarito** (`linha`, `coluna`, `regra`).

```python
import random

def gerar_linha_valida(indice):
    return {
        "codigo": f"FIC-2026-{indice:05d}",
        "nome_curso": random.choice(NOMES_CURSOS),
        "campus": random.choice(CAMPI_IFRN),
        # ... demais campos
    }

def estragar(linha, regra):
    """Modifica a linha para violar a regra indicada e devolve a coluna afetada."""
    if regra == "R03":
        linha["carga_horaria"] = random.choice(["", "-40", "abc", "0"])
        return "carga_horaria"
    if regra == "R07":
        linha["data_fim"] = "01/01/2025"   # anterior ao início
        return "data_fim"
    # ... demais regras
```

Use uma lista `NOMES_CURSOS` com nomes reais de cursos FIC (Informática Básica, Operador de Computador, Eletricista Instalador Predial, Auxiliar Administrativo, Costureiro, Cuidador de Idosos...). O **Guia Pronatec de Cursos FIC** é público e serve de fonte — e citá-lo no artigo mostra que a massa sintética é realista.

**Semente aleatória (`random.seed`).** Coloque `random.seed(42)` no começo do gerador. Isso faz com que ele gere **sempre a mesma planilha**, o que é essencial para a reprodutibilidade: qualquer pessoa que rodar o seu script vai obter os mesmos números que você publicou no artigo. Esse é um ponto forte para destacar na Metodologia.

**Os três números que você vai apresentar:**

| Termo | Significado no seu trabalho |
|---|---|
| Verdadeiro positivo (acerto) | O gabarito diz que há um erro na linha X, coluna Y, e o validador o apontou |
| Falso negativo | O gabarito diz que há um erro, e o validador **não** o apontou |
| Falso positivo | O validador apontou um erro que **não** está no gabarito |

A partir deles calcule **precisão** = acertos / (acertos + falsos positivos) e **revocação** = acertos / (acertos + falsos negativos). Pesquise esses dois conceitos: eles são padrão na área e vão dar solidez ao capítulo de Resultados.

**Dica de depuração:** se aparecerem muitos falsos positivos, na maioria das vezes a causa não é o validador. Verifique primeiro se o gerador criou, sem querer, uma linha inválida que ele registrou como válida (por exemplo, sorteando uma data de fim anterior à de início por acaso) e se a sua decisão da Sprint 3 sobre erros acumulados está sendo considerada na comparação.

### Entrega da sprint

- [ ] `gerador_massa.py` gera planilha + gabarito, de forma reprodutível (`random.seed`).
- [ ] Massas de 100, 1.000 e 10.000 linhas geradas na sua máquina. **Não comite as planilhas grandes** no repositório compartilhado: como a geração é reprodutível pela semente, basta comitar o script e deixar no `README` o comando que recria cada massa. Se quiser comitar alguma, comite só a de 100 linhas, como exemplo.
- [ ] `comparador.py` imprime acertos, falsos negativos, falsos positivos, precisão e revocação.
- [ ] Tabela com os resultados das três massas anotada em `docs/resultados.md`.

---

# Sprint 7 — 03/11 a 09/11/2026
## Medição de desempenho e importação para o SQLite

**Objetivo da sprint:** medir o tempo de processamento e fechar o ciclo, levando as linhas válidas para um banco de dados.

### Tarefas

1. Medir o tempo de processamento das planilhas de 100, 1.000 e 10.000 linhas.
2. Repetir cada medição **5 vezes** e calcular a média e o desvio padrão.
3. Criar `src/banco.py`, que cria um banco SQLite com a tabela `curso_fic`.
4. Implementar a importação das linhas válidas para o banco.
5. Garantir que a importação não duplique registros: se o `codigo` já existir no banco, atualizar em vez de inserir.
6. Registrar as versões de tudo (Python, openpyxl, sistema operacional, processador, memória) em `docs/ambiente.md`.

### Ajuda / direcionamento

**Medição de tempo:** use `time.perf_counter()`, que é mais preciso que `time.time()` para medir duração.

```python
import time

inicio = time.perf_counter()
# ... processamento ...
duracao = time.perf_counter() - inicio
print(f"Tempo: {duracao:.4f} segundos")
```

**Por que 5 repetições?** Porque o computador está rodando outras coisas ao mesmo tempo, e uma única medição pode sair distorcida. Apresentar a média de 5 execuções, com o desvio padrão, é o mínimo esperado em um trabalho que se propõe a medir desempenho. Use `statistics.mean` e `statistics.stdev`, que já vêm com o Python. Feche o navegador e os outros programas antes de medir.

**Por que registrar o ambiente?** Porque "processou 10.000 linhas em 2 segundos" não significa nada sem dizer em qual máquina. No artigo, essa informação vai no capítulo de Materiais e Métodos.

**SQLite:** já vem com o Python, no módulo `sqlite3`. Não precisa instalar servidor nenhum — o banco inteiro é um arquivo.

```python
import sqlite3

def criar_banco(caminho="cursos_fic.db"):
    conexao = sqlite3.connect(caminho)
    conexao.execute("""
        CREATE TABLE IF NOT EXISTS curso_fic (
            codigo TEXT PRIMARY KEY,
            nome_curso TEXT NOT NULL,
            campus TEXT NOT NULL,
            eixo_tecnologico TEXT NOT NULL,
            carga_horaria INTEGER NOT NULL,
            turno TEXT NOT NULL,
            vagas INTEGER NOT NULL,
            data_inicio TEXT NOT NULL,
            data_fim TEXT NOT NULL
        )
    """)
    conexao.commit()
    return conexao
```

**Sobre não duplicar:** pesquise o comando `INSERT ... ON CONFLICT(codigo) DO UPDATE SET ...` do SQLite (chamado de *upsert*). Ele resolve o problema em um único comando. Repare como isso conversa com a regra R02: o `PRIMARY KEY` faz o banco recusar códigos repetidos, ou seja, o banco é a **segunda** barreira de proteção, depois do validador. Esse raciocínio de "validar antes de inserir, e ainda assim proteger no banco" rende um bom parágrafo nos Resultados.

**Sempre use parâmetros (`?`) nas consultas,** nunca monte o SQL concatenando texto. Pesquise "injeção de SQL" para entender o motivo — vale uma menção no artigo.

```python
conexao.execute(
    "INSERT INTO curso_fic VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)",
    (codigo, nome, campus, eixo, carga, turno, vagas, inicio, fim),
)
```

**Para conferir o resultado,** instale a extensão "SQLite Viewer" no VS Code ou baixe o DB Browser for SQLite. Tire um print da tabela preenchida — ele vai para os Resultados.

### Entrega da sprint

- [ ] Tabela de tempos (100, 1.000, 10.000 linhas) com média e desvio padrão de 5 execuções.
- [ ] `docs/ambiente.md` com as versões e a configuração da máquina.
- [ ] Banco `cursos_fic.db` sendo criado e populado com as linhas válidas (o arquivo `.db` fica no seu computador, ignorado pelo `.gitignore` — o que se comita é o código que o cria).
- [ ] Executar o importador duas vezes seguidas **não** duplica registros.
- [ ] Print do banco preenchido em `docs/evidencias/`.

---

# Sprint 8 — 10/11 a 16/11/2026
## Fechamento: interface de linha de comando, testes e documentação

**Objetivo da sprint:** transformar um conjunto de scripts em uma ferramenta que outra pessoa consegue instalar e usar sozinha, lendo apenas o `README.md` da sua subpasta.

### Tarefas

1. Criar uma interface de linha de comando com `argparse`, aceitando o arquivo de entrada e as opções de saída.
2. Escrever pelo menos 10 testes automatizados simples com `pytest`, cobrindo as funções de validação.
3. Finalizar o `README.md` da subpasta: o que é, como instalar, como executar, como reproduzir as medições, exemplo de saída.
4. Revisar o código: nomes de variáveis em português e claros, remoção de código morto, comentários onde necessário.
5. Montar a apresentação final (8 a 10 slides) com o que foi feito e os resultados medidos.

### Ajuda / direcionamento

**Interface de linha de comando com `argparse`** (módulo nativo). O objetivo é que o programa seja usado assim:

```
python src/main.py dados/cursos.xlsx --relatorio saida/erros.csv --limpo saida/cursos_limpos.csv --banco cursos_fic.db
```

```python
import argparse

parser = argparse.ArgumentParser(description="Validador de planilhas de cursos FIC")
parser.add_argument("entrada", help="Caminho da planilha (.csv ou .xlsx)")
parser.add_argument("--relatorio", default="saida/relatorio_erros.csv")
parser.add_argument("--limpo", default="saida/cursos_limpos.csv")
parser.add_argument("--banco", default=None, help="Se informado, importa para este banco SQLite")
argumentos = parser.parse_args()
```

**Testes com `pytest`:** instale com `pip install pytest`. Crie uma pasta `testes/` com um arquivo `test_validadores.py`. Cada teste é uma função que começa com `test_` e usa `assert`:

```python
from validadores import inteiro_positivo, converter_data

def test_inteiro_positivo_aceita_numero_valido():
    assert inteiro_positivo("160") is True

def test_inteiro_positivo_rejeita_texto():
    assert inteiro_positivo("abc") is False

def test_inteiro_positivo_rejeita_zero():
    assert inteiro_positivo("0") is False

def test_converter_data_rejeita_data_inexistente():
    assert converter_data("31/02/2026") is None
```

Rode com `pytest -v`. Escolha os testes com intenção: para cada regra, um caso **válido**, um caso **inválido** e um **caso-limite** (zero, campo vazio, data no último dia do mês, data de fim igual à de início). O número de testes e a quantidade de aprovados é mais um resultado mensurável para o artigo.

**O `README.md` da sua subpasta é parte da entrega do TCC,** não um detalhe. Como o repositório é compartilhado, ele também é o que explica a um colega o que existe dentro da sua pasta. Precisa ter: descrição do projeto e vínculo com o iFIC; requisitos (Python 3.12, `pip install -r requirements.txt`); como executar com um exemplo real de comando, deixando claro que os comandos são rodados **de dentro da subpasta**; descrição de cada regra de validação (a tabela R01–R10); como gerar a massa de testes e reproduzir as medições; e a estrutura de pastas.

**Revisão de código:** leia o seu próprio código imaginando que outra pessoa vai mantê-lo. Se você precisar de mais de 10 segundos para entender uma função, o nome ou a estrutura dela precisa melhorar. Funções com mais de 30 linhas geralmente estão fazendo coisas demais.

### Entrega da sprint

- [ ] Ferramenta executável por linha de comando com `argparse`.
- [ ] Pelo menos 10 testes passando com `pytest`.
- [ ] `README.md` da subpasta completo, permitindo que outra pessoa reproduza tudo.
- [ ] Subpasta organizada, sem arquivos temporários, sem `.venv`, sem `.db` e sem planilhas grandes comitadas.
- [ ] Nenhum arquivo fora da sua subpasta foi alterado ao longo das 8 sprints (confira com `git log --stat`).
- [ ] Apresentação final montada.

---

## Quadro-resumo das sprints

| Sprint | Período | Entrega principal | Conceitos novos |
|---|---|---|---|
| 1 | 22/09 a 28/09 | Ambiente, subpasta no repositório e leitura de CSV | venv, Git, `csv.DictReader` |
| 2 | 29/09 a 05/10 | Código em módulos e verificação de colunas (R10) | funções, módulos, list comprehension |
| 3 | 06/10 a 12/10 | Regras R01, R03, R04 | `try/except`, conversão de tipos |
| 4 | 13/10 a 19/10 | Regras R02, R05 a R09 | `datetime`, dicionários, `enumerate` |
| 5 | 20/10 a 26/10 | Leitura de `.xlsx`, relatório e planilha limpa | `openpyxl`, `zip`, escrita de arquivos |
| 6 | 27/10 a 02/11 | Gerador de massa com gabarito e comparador | `random.seed`, precisão e revocação |
| 7 | 03/11 a 09/11 | Medição de tempo e importação para SQLite | `perf_counter`, `sqlite3`, *upsert* |
| 8 | 10/11 a 16/11 | CLI, testes e documentação | `argparse`, `pytest` |

---

## Se sobrar tempo (tarefas extras, opcionais)

Só comece alguma delas se o cronograma principal estiver em dia. É melhor entregar o escopo fechado bem-feito do que um escopo maior pela metade.

- **E1.** Sugestão automática de correção: quando o turno for `"Noturnoo"`, sugerir `"noturno"` (pesquise `difflib.get_close_matches`, que já vem com o Python).
- **E2.** Exportar o relatório de erros também em `.xlsx`, com as células problemáticas pintadas de vermelho.
- **E3.** Permitir que as regras sejam configuradas em um arquivo `regras.json`, sem alterar o código.
- **E4.** Medir também o consumo de memória para a massa de 10.000 linhas.

---

## Relação com o artigo

O desenvolvimento e a escrita andam em paralelo (ver `01_kaio_ific_tarefas_escrita.md`). A tabela abaixo mostra de onde sai o conteúdo de cada capítulo:

| Capítulo do artigo | Sprints que geram o conteúdo |
|---|---|
| Materiais e Métodos | 1, 2, 5, 7 (ferramentas, versões, ambiente de medição) |
| Metodologia | 1 a 8 (etapas do desenvolvimento, em ordem cronológica) |
| Resultados | 4 (regras), 5 (saídas), 6 (precisão e revocação), 7 (tempos), 8 (testes) |
| Conclusão | dificuldades registradas ao longo de todas as sprints |

**Recomendação prática:** mantenha um arquivo `docs/diario.md` e anote, ao final de cada sprint, três linhas — o que funcionou, o que deu errado e o que você aprendeu. Quando chegar a hora de escrever a Conclusão, esse diário vai economizar horas de trabalho e evitar que as dificuldades reais sejam esquecidas.
