# Plano de tarefas de desenvolvimento – Teófilo e dupla (Tecnologia em Sistemas para Internet)

**Projeto pai:** AgroAgreste – Observatório Territorial da Agricultura Familiar no Agreste do Rio Grande do Norte (ver [projeto.md](../projeto.md)).

**Temática escolhida:** S5 – Previsão da produção de mandioca com aprendizado de máquina a partir de dados climáticos (ver [tematicas.md](../tematicas.md)).

**Perfil dos alunos:** **2 alunos** do Curso Superior de Tecnologia em Sistemas para Internet, com conhecimentos **básicos** em Python e em treinamento. As tarefas são pequenas, muito detalhadas e divididas entre os dois de propósito. Nenhum passo exige saber aprendizado de máquina antes de começar: a parte de modelos só aparece na Sprint 5, depois de quatro semanas construindo a base de dados.

**Duração:** 8 sprints de 1 semana (22/09/2026 a 16/11/2026).

**Onde o trabalho acontece:** o **repositório de treinamento do projeto já existe** e é compartilhado com os outros alunos. Vocês **não vão criar repositório nenhum**. Todo o trabalho da dupla fica dentro de **uma única subpasta**, compartilhada pelos dois:

```
<repositorio-de-treinamento>/
├── ...              ← pastas de outros alunos (não mexam)
└── teofilo/         ← a subpasta da dupla: tudo o que vocês fizerem fica aqui dentro
```

Confirmem com o orientador o **endereço do repositório** e o **nome exato da subpasta** antes de começar. Todos os caminhos deste documento são relativos a ela.

---

## A ideia do trabalho, em uma página

A mandioca é a principal cultura da agricultura familiar do Agreste potiguar. A produção varia muito de um ano para outro, e quase todo mundo na região diz o mesmo quando perguntado por quê: **foi a chuva**. Só que "foi a chuva" é uma explicação, não é um número. Ninguém consegue dizer *quanto* da variação a chuva explica, nem *qual* chuva importa mais — a do começo do ciclo, a do ano inteiro, a do ano anterior.

O IBGE publica, todo ano, quanto cada município plantou e colheu. A NASA publica, de graça, a série diária de chuva e temperatura de qualquer ponto do planeta. As duas bases existem há décadas e nunca foram cruzadas para esta região.

A pergunta que este trabalho responde é:

> **É possível estimar o rendimento da mandioca dos municípios do Agreste potiguar a partir de dados climáticos públicos? E um modelo de aprendizado de máquina acerta mais do que a previsão mais ingênua possível — repetir o resultado do ano anterior?**

A segunda metade da pergunta é a parte séria. É fácil treinar um modelo e mostrar um gráfico bonito. O que faz este trabalho ser um artigo é **provar que o modelo vale mais do que o chute óbvio** — ou mostrar, com honestidade e com números, que não vale.

### O que vocês vão construir

1. Uma rotina em Python que baixa do **IBGE** a série histórica de área plantada, área colhida e quantidade produzida de **mandioca** para todos os municípios do Agreste potiguar;
2. Uma rotina que baixa da **NASA POWER** a série diária de chuva e temperatura de cada um desses municípios;
3. Uma **tabela única**, em que cada linha é um par *município + ano* e as colunas são: o **rendimento da mandioca daquele ano** (o que queremos prever) e um conjunto de **variáveis climáticas** daquele ano e do anterior (com o que vamos prever);
4. Uma **linha de base** — a previsão ingênua — e três modelos: regressão linear, Random Forest e uma árvore com *boosting*;
5. Uma **avaliação temporal honesta**: treinar só com o passado, testar só no futuro, e medir o erro de cada modelo contra a linha de base;
6. Uma análise de **quais variáveis climáticas mais pesam** na previsão.

### O que vai ser medido (é isso que faz o trabalho ser um artigo, e não um relatório)

| O que | Como |
|---|---|
| **Erro de previsão** | MAE, RMSE e MAPE de cada modelo, calculados sempre em anos que o modelo nunca viu |
| **Ganho sobre a linha de base** | Quantos por cento de erro cada modelo reduz em relação à previsão ingênua. **É o número central do artigo** |
| **Quais variáveis importam** | Importância por permutação: qual variável climática, se embaralhada, mais estraga a previsão |
| **Onde o modelo erra** | O erro é igual em todos os anos? Em todos os municípios? Ele erra mais justamente nos anos de seca, que são os que interessam? |
| **Custo** | Tempo de coleta dos dados e tempo de treino, para dizer se o observatório consegue rodar isso todo ano |

A quarta linha costuma ser a mais interessante do artigo. Um modelo que acerta bem nos anos normais e erra feio nos anos de seca **é inútil para o planejamento territorial**, mesmo tendo erro médio baixo. Descobrir isso é um resultado de verdade.

### O recorte

**Todos os municípios do Agreste Potiguar** que tenham produção de mandioca registrada. São por volta de 40 — vocês vão levantar a lista oficial na Sprint 1, a partir da API do IBGE, e **confirmá-la com o orientador**, porque precisa ser a mesma lista usada pelos outros TCCs do projeto.

**Período:** de **2000 até o último ano disponível** na Produção Agrícola Municipal (confirmem qual é na Sprint 1; provavelmente 2023 ou 2024). São mais de vinte anos, o que dá algo em torno de **800 a 1.000 linhas** na tabela final. É pouco para aprendizado de máquina moderno e é uma limitação que vocês vão declarar no artigo — mas é exatamente por isso que a comparação com a linha de base é obrigatória.

### O que se quer prever, exatamente

O alvo é o **rendimento médio da mandioca, em quilos por hectare**, de cada município em cada ano.

Por que rendimento e não produção total? Porque a produção total depende de quanto se plantou, e quanto se planta depende de decisão do agricultor, preço, crédito, política pública — coisas que não estão nos dados de clima. O rendimento isola melhor o efeito do tempo: é *quanto rendeu cada hectare que foi colhido*. Escrevam essa justificativa no artigo; ela mostra que a escolha do alvo foi pensada.

Vocês mesmos vão calcular o rendimento:

```
rendimento (kg/ha) = quantidade produzida (t) × 1000 ÷ área colhida (ha)
```

O IBGE também publica uma coluna de rendimento pronta. Vocês vão baixá-la **só para conferir** se a conta de vocês bate com a dele. Se bater, é um sinal de que a base foi montada certo.

### O que este trabalho **não** é

- **Não é previsão do tempo.** Vocês não preveem a chuva; vocês usam a chuva que já aconteceu para explicar a colheita que veio depois.
- **Não é dizer a um agricultor quanto ele vai colher.** A previsão é por **município**, sobre uma média de muitas propriedades. Deixem isso explícito no artigo — é um limite real e um revisor vai cobrar.
- **Não é construir o observatório.** O AgroAgreste é o **contexto** que justifica a pergunta. O objeto do artigo é o **modelo avaliado**. Se o texto virar um manual dos scripts, o trabalho perde o valor.

---

## Decisões técnicas já fechadas

| Item | Decisão |
|---|---|
| Linguagem | **Python 3** |
| Dados de produção | **IBGE / Produção Agrícola Municipal**, tabela 5457 do SIDRA |
| Dados de clima | **NASA POWER**, série diária por ponto, API gratuita e sem cadastro |
| Lista de municípios | **API de Localidades do IBGE** |
| Armazenamento durante o trabalho | **Arquivos CSV** |
| Banco de dados | **MySQL, só na Sprint 8 e como entrega opcional** (ver a seção abaixo) |
| Aprendizado de máquina | **`scikit-learn`** — e só ele. Linha de base, regressão linear, Random Forest e `HistGradientBoostingRegressor` já vêm nessa biblioteca |
| Gráficos | `matplotlib` |
| O que **não** entra | Docker, Django, redes neurais, aprendizado profundo, dados que envolvam pessoas |

**Tudo é instalado com `pip`**, porque as máquinas do laboratório não permitem instalar programas. Nenhuma biblioteca desta lista exige aplicativo externo.

### Sobre o banco de dados (MySQL)

O MySQL está instalado no laboratório, mas **durante as sete primeiras sprints vocês não vão usá-lo**, e isso é uma decisão técnica, não preguiça.

A base final deste trabalho tem cerca de mil linhas e cinquenta colunas. Isso cabe folgadamente em um arquivo CSV, é lido pelo `pandas` em uma linha de código e pode ser aberto no Excel para conferência visual — que é uma coisa que vocês vão fazer muito. Colocar um banco no meio do caminho, nesta fase, só acrescentaria um ponto de falha entre vocês e os dados.

**Na Sprint 8**, como entrega final e opcional, vocês vão escrever um script que **carrega a tabela final no MySQL**. Isso tem um propósito claro: o observatório AgroAgreste vai precisar dos dados em banco para alimentar seus painéis, e deixar essa ponte pronta é uma contribuição concreta do TCC. Peçam ao coordenador, **já na Sprint 1**, o usuário e a senha do MySQL do laboratório, para não descobrir na última semana que não têm acesso.

A biblioteca de acesso (`mysql-connector-python` ou `PyMySQL` com `SQLAlchemy`) instala por `pip` normalmente.

No artigo, essa decisão vira um parágrafo da seção de Materiais e Métodos: *o processamento foi feito em arquivos CSV, adequados ao volume de dados; a persistência em MySQL foi implementada como camada de integração com o observatório*. Justificar a ferramenta que você **não** usou é sinal de maturidade técnica.

### Redução de escopo já aplicada

A temática S5, como está descrita no `tematicas.md`, previa também XGBoost ou LightGBM. **Isso foi cortado** do escopo obrigatório, por três motivos: são bibliotecas a mais para instalar em máquina bloqueada, exigem ajuste de hiperparâmetros para render alguma coisa, e o `HistGradientBoostingRegressor` do `scikit-learn` é do mesmo tipo de algoritmo, já vem instalado junto e resolve a mesma pergunta do artigo.

Se sobrar tempo na Sprint 8, o XGBoost entra como experimento extra. Se não sobrar, **o artigo não perde nada** — o que sustenta o trabalho é a comparação com a linha de base, não a quantidade de modelos.

---

## Como os dois alunos se dividem

Este é o ponto que mais dá errado em trabalho de dupla. A regra é simples: **cada arquivo tem um dono**. Duas pessoas editando o mesmo arquivo no mesmo dia geram conflito no Git, e conflito de Git com aluno em treinamento custa uma tarde.

### Trilhas

| | **Aluno A — trilha Produção** | **Aluno B — trilha Clima** |
|---|---|---|
| Sprints 1 a 4 | Dados do IBGE: lista de municípios, série da mandioca, limpeza, cálculo do rendimento, gráficos exploratórios da produção | Dados da NASA POWER: coordenadas dos municípios, série diária de chuva e temperatura, agregação por ano, gráficos exploratórios do clima |
| Sprint 4 | Junta as duas bases e gera a tabela final | Cria as variáveis climáticas derivadas (acumulados, dias secos, médias) |
| Sprint 5 | Linha de base e função de avaliação temporal | Prepara a separação treino/teste e a montagem das variáveis defasadas |
| Sprint 6 | Regressão linear | Random Forest |
| Sprint 7 | Análise de erro por ano e por município | Importância das variáveis e o modelo com *boosting* |
| Sprint 8 | README, reprodutibilidade, execução do zero | Script de carga no MySQL e medição de custo |

Definam na Sprint 1 **quem é o A e quem é o B** e anotem no `README.md` da subpasta. O orientador precisa saber quem fez o quê — e o artigo tem dois autores, que precisam poder responder pelo trabalho inteiro.

### As três regras da dupla

1. **Cada script tem um dono.** Quem não é dono **lê e comenta, mas não edita**. Se precisar mudar algo no script do colega, avise e deixe a pessoa mudar.
2. **Revisão cruzada toda sexta.** Cada um baixa o repositório atualizado e **roda o script do outro na própria máquina**. É a forma mais barata de descobrir os "só funciona no meu computador" — caminho de arquivo fixo na máquina, biblioteca instalada só de um lado, arquivo que não foi comitado.
3. **Os dois precisam entender o trabalho inteiro.** Vocês vão apresentar juntos e escrever um artigo só. Na reunião semanal, o orientador pode pedir para o aluno A explicar a parte do B. Isso não é armadilha, é o combinado.

---

## Combinados gerais

- **Repositório:** já existe e é compartilhado. Trabalhem **somente dentro da subpasta de vocês**.
- **Commits:** pelo menos 3 por sprint **por aluno**, com mensagem em português dizendo o que foi feito.
- **Reunião semanal:** no começo de cada sprint vocês mostram ao orientador o que fizeram, **rodando na máquina**.
- **Travou mais de 40 minutos no mesmo erro? Peça ajuda** — primeiro ao colega, depois ao orientador.
- **Dados:** tudo o que for baixado vai para `dados/`. **Nunca apaguem uma linha de dado bruto.** Se um município não tem produção de mandioca em certo ano, isso é informação, não lixo.
- **Diário:** `docs/diario.md`, três linhas no fim de cada sprint, por aluno — o que funcionou, o que deu errado, o que aprendi. Vira a Conclusão do artigo.
- **Prints e gráficos:** em `docs/evidencias/`. Vão para o capítulo de Resultados.
- **`random_state=42` em tudo.** Todo modelo que sorteia alguma coisa recebe uma semente fixa. Sem isso, os números mudam a cada execução e o artigo fica irreprodutível — e vocês vão enlouquecer tentando entender por que o resultado "mudou sozinho".
- **Desconfiem dos números bons.** Em aprendizado de máquina, resultado bom demais quase sempre é erro — normalmente informação do futuro vazando para o treino. A Sprint 5 trata disso em detalhe.

### Convivência em repositório compartilhado

1. **Só alterem arquivos dentro da subpasta de vocês.** Nunca editem, movam ou apaguem arquivo de outro aluno.
2. **Comecem o dia com `git pull`.** Na dupla isso vale em dobro: o colega mexeu ontem à noite.
3. **Comitem só o que é de vocês:** usem `git add teofilo/`, nunca `git add .`. Confiram com `git status` antes.
4. **Não comitem** a pasta `.venv/` nem os dados brutos grandes (os JSON da NASA). Comitem os CSV consolidados e os gráficos, que são pequenos.
5. **Deu `CONFLICT`? Parem e chamem o orientador.** Não tentem resolver "no chute" — em dupla, um conflito mal resolvido apaga o trabalho de alguém.
6. **`git push` no fim de cada dia**, mesmo que não esteja pronto.

### Estrutura da subpasta

```
teofilo/
├── scripts/
│   ├── 01_municipios.py
│   ├── 02_ibge_mandioca.py
│   ├── 03_nasa_power.py
│   ├── 04_variaveis_clima.py
│   ├── 05_montar_base.py
│   ├── 06_linha_de_base.py
│   ├── 07_modelos.py
│   ├── 08_analise_erros.py
│   └── 09_carregar_mysql.py
├── dados/
│   ├── brutos/            ← o que veio das APIs, sem mexer
│   ├── intermediarios/
│   └── final/             ← base_modelagem.csv
├── resultados/            ← tabelas de métricas
├── graficos/
├── docs/
│   ├── diario.md
│   ├── ambiente.md
│   └── evidencias/
├── .gitignore
├── requirements.txt
└── README.md
```

---

# Sprint 1 — 22/09 a 28/09/2026
## Ambiente, lista de municípios e o primeiro dado do IBGE na tela

**Objetivo:** ao final da semana, ter o ambiente funcionando, a lista oficial dos municípios do Agreste potiguar em um CSV, e um script que traz do IBGE a produção de mandioca de **um** município.

Esta sprint é um **teste de viabilidade**. Se a rede do laboratório bloquear as APIs do IBGE ou da NASA, é melhor descobrir agora do que na Sprint 4.

### O que vocês vão fazer

1. Preparar o ambiente e a estrutura de pastas (os dois juntos, na mesma mesa, no primeiro dia).
2. **Aluno A:** baixar a lista de municípios do Agreste potiguar pela API do IBGE.
3. **Aluno B:** baixar as coordenadas desses municípios e testar a API da NASA POWER para um ponto.
4. **Aluno A:** fazer a primeira consulta ao SIDRA e descobrir os códigos da tabela.
5. Definir com o orientador a lista final e o período.
6. Pedir ao coordenador o acesso ao MySQL (para usar só na Sprint 8).

### Passo a passo

**1. Clonar o repositório e criar a subpasta** (façam isso uma vez, juntos; depois cada um clona na sua máquina).

```
git clone <endereço-do-repositório-de-treinamento>
cd <pasta-do-repositório>
mkdir teofilo
cd teofilo
```

Criem as pastas da estrutura mostrada acima. Pastas vazias não vão para o Git, então coloquem um arquivo `.gitkeep` vazio dentro de cada uma.

**2. Ambiente virtual e bibliotecas** (cada aluno faz na sua máquina):

```
python -m venv .venv
.venv\Scripts\activate
pip install requests pandas matplotlib scikit-learn
pip freeze > requirements.txt
```

| Biblioteca | Para quê |
|---|---|
| `requests` | Conversar com as APIs do IBGE e da NASA |
| `pandas` | Organizar as tabelas — é a ferramenta central deste trabalho |
| `matplotlib` | Gráficos |
| `scikit-learn` | Os modelos, a partir da Sprint 5 |

Se quiserem, instalem também `sidrapy`, que é uma biblioteca brasileira que facilita a consulta ao SIDRA. Ela é conveniente, mas **não é obrigatória**: dá para fazer tudo com `requests`. Comecem com `requests` para entender o que está acontecendo, e só depois avaliem se vale trocar.

**3. O `.gitignore` da subpasta:**

```
.venv/
__pycache__/
*.pyc
dados/brutos/*.json
```

**4. A lista de municípios (Aluno A).** Crie `scripts/01_municipios.py`:

```python
import requests
import pandas as pd

# A API de Localidades do IBGE devolve todos os municipios do RN (UF 24),
# com a microrregiao e a mesorregiao de cada um.
URL = "https://servicodados.ibge.gov.br/api/v1/localidades/estados/24/municipios"

resposta = requests.get(URL, timeout=60)
resposta.raise_for_status()
municipios = resposta.json()

print("Total de municipios do RN:", len(municipios))

linhas = []
for m in municipios:
    mesorregiao = m["microrregiao"]["mesorregiao"]["nome"]
    if mesorregiao == "Agreste Potiguar":
        linhas.append({
            "codigo_ibge": m["id"],
            "municipio": m["nome"],
            "microrregiao": m["microrregiao"]["nome"],
            "mesorregiao": mesorregiao,
        })

df = pd.DataFrame(linhas).sort_values("municipio")
df.to_csv("dados/final/municipios_agreste.csv", index=False, encoding="utf-8")

print("Municipios do Agreste Potiguar:", len(df))
print(df.head(10))
```

Duas observações que valem para o artigo:

- A mesorregião "Agreste Potiguar" é uma divisão **antiga** do IBGE, substituída em 2017 pelas regiões geográficas intermediárias e imediatas. A API ainda a expõe, e ela continua sendo a referência mais usada nos trabalhos sobre a região. **Usem ela, e digam no artigo que é a divisão de 2010 do IBGE** — recorte declarado é recorte defendido.
- O código do município tem 7 dígitos. É ele que liga a base do IBGE à base da NASA e a tudo mais. **Nunca usem o nome do município como chave** — acento, hífen e grafia mudam entre fontes e vocês vão perder linhas sem perceber.

**5. As coordenadas dos municípios (Aluno B).** A NASA POWER trabalha por ponto — latitude e longitude. Vocês precisam de um ponto por município. Duas opções:

*Opção 1 (mais simples, recomendada):* usar as coordenadas da **sede** do município, que estão no serviço de malhas/localidades do IBGE. Crie `scripts/01b_coordenadas.py`:

```python
import requests
import pandas as pd
import time

municipios = pd.read_csv("dados/final/municipios_agreste.csv")

linhas = []
for _, linha in municipios.iterrows():
    codigo = linha["codigo_ibge"]
    url = f"https://servicodados.ibge.gov.br/api/v3/malhas/municipios/{codigo}/metadados"
    r = requests.get(url, timeout=60)
    if r.status_code != 200:
        print("Falhou:", linha["municipio"], r.status_code)
        continue
    dados = r.json()[0]
    linhas.append({
        "codigo_ibge": codigo,
        "municipio": linha["municipio"],
        "latitude": dados["centroide"]["latitude"],
        "longitude": dados["centroide"]["longitude"],
    })
    time.sleep(0.5)   # nao martele a API

pd.DataFrame(linhas).to_csv("dados/final/coordenadas.csv", index=False)
print("Coordenadas obtidas:", len(linhas))
```

*Opção 2 (plano B):* se esse serviço não responder, procurem no portal do IBGE a planilha de **sedes municipais** com coordenadas e baixem à mão. Um download único de uma planilha é uma solução perfeitamente legítima; anotem no artigo qual foi a fonte e a data de acesso.

**Confiram os números.** O Agreste potiguar fica por volta da latitude **-6** e da longitude **-35,5**. Se aparecer latitude positiva ou longitude -70, algo está trocado. Abram o CSV e olhem.

**6. Testar a NASA POWER (Aluno B).** Crie `scripts/03_nasa_power.py` com uma primeira versão que busca **um** município e **um** ano:

```python
import requests

# exemplo: um ponto no Agreste potiguar. Troque pelas coordenadas reais de um municipio.
lat, lon = -6.23, -35.99

url = "https://power.larc.nasa.gov/api/temporal/daily/point"
parametros = {
    "parameters": "PRECTOTCORR,T2M,T2M_MAX",
    "community": "AG",          # comunidade "agroclimatology"
    "latitude": lat,
    "longitude": lon,
    "start": "20200101",
    "end": "20201231",
    "format": "JSON",
}

r = requests.get(url, params=parametros, timeout=120)
r.raise_for_status()
dados = r.json()

chuva = dados["properties"]["parameter"]["PRECTOTCORR"]
print("Dias recebidos:", len(chuva))
print("Primeiros dias:", list(chuva.items())[:5])
print("Chuva total do ano (mm):", round(sum(v for v in chuva.values() if v >= 0), 1))
```

O que cada parâmetro significa:

| Parâmetro | O que é |
|---|---|
| `PRECTOTCORR` | Precipitação total diária corrigida, em **mm/dia**. É a chuva |
| `T2M` | Temperatura média do ar a 2 metros do chão, em °C |
| `T2M_MAX` | Temperatura máxima do dia, em °C |
| `community=AG` | Diz à API que o uso é agroclimatológico. Muda as unidades padrão — por isso está fixo |

**Atenção ao valor `-999`.** A NASA POWER usa `-999` para "sem dado". Se vocês somarem isso como se fosse chuva, o total do ano fica negativo. Por isso o filtro `if v >= 0` no código acima. **Escrevam esse tratamento no artigo**, na seção de Materiais e Métodos — é exatamente o tipo de detalhe que separa um método reprodutível de um método vago.

**Teste de sanidade:** a chuva anual no Agreste potiguar fica, grosso modo, entre **400 e 900 mm**. Se o seu total der 50 mm ou 4.000 mm, tem erro — coordenada trocada, `-999` entrando na conta, ou unidade errada.

**7. A primeira consulta ao IBGE (Aluno A).** Aqui vocês vão precisar **descobrir códigos**, e isso é parte da tarefa.

Abram no navegador a **tabela 5457 do SIDRA** ("Área plantada ou destinada à colheita, área colhida, quantidade produzida, rendimento médio e valor da produção das lavouras temporárias e permanentes"). Na página da tabela, anotem:

- o **código de cada variável** que interessa: área plantada, área colhida, quantidade produzida e rendimento médio;
- o **código do produto "Mandioca"** dentro da classificação de produtos das lavouras;
- o **último ano disponível**.

**Escrevam os códigos no `README.md` da subpasta**, com a data em que consultaram. Vocês vão usá-los no resto do trabalho e vão precisar deles na seção de Materiais e Métodos do artigo.

A API do SIDRA é acessada por uma URL com essa forma:

```
https://apisidra.ibge.gov.br/values/t/5457/n6/all/v/<VARIAVEIS>/p/all/c782/<CODIGO_MANDIOCA>
```

- `t/5457` → a tabela
- `n6/all` → nível territorial 6, que é **município**; `all` = todos
- `v/...` → as variáveis, separadas por vírgula
- `p/all` → todos os períodos (anos)
- `c782/...` → a classificação de produto, com o código da mandioca

Testem essa URL **primeiro no navegador**, com um município só, antes de escrever código. Se o navegador devolver JSON, a API está liberada na rede do laboratório. Se não devolver, avisem o orientador **ainda nesta sprint**.

**Plano B do IBGE:** se a API estiver bloqueada, o SIDRA permite **baixar a tabela em CSV/XLSX pelo navegador**. Baixem os arquivos uma vez, guardem em `dados/brutos/` e sigam o trabalho lendo os arquivos locais. O artigo não muda — muda uma frase em Materiais e Métodos. **Não parem o trabalho por causa disso.**

**8. Fechar a lista e o período com o orientador.** Levem para a reunião: o CSV de municípios, o número de municípios encontrados, o último ano disponível da PAM e a proposta de período (2000 até o último ano). Saiam da reunião com essas três coisas **fechadas e anotadas no README**.

**9. Pedir o acesso ao MySQL.** Mandem uma mensagem ao coordenador pedindo usuário, senha e nome do banco no MySQL do laboratório. É para a Sprint 8, mas o pedido é hoje.

### Como saber que deu certo

- [ ] Os dois alunos têm o repositório clonado, o ambiente virtual funcionando e conseguem rodar um script Python.
- [ ] `dados/final/municipios_agreste.csv` existe, com uma linha por município e o código IBGE de 7 dígitos.
- [ ] `dados/final/coordenadas.csv` existe e as coordenadas estão na faixa certa.
- [ ] O script da NASA POWER trouxe 365 dias e um total de chuva plausível.
- [ ] Os códigos da tabela 5457 estão anotados no `README.md`.
- [ ] A lista de municípios e o período foram aprovados pelo orientador.
- [ ] Pelo menos 3 commits de cada aluno.

### Erros comuns

| Erro | O que está acontecendo |
|---|---|
| `ModuleNotFoundError` depois de instalar | O ambiente virtual não está ativo. Rode `.venv\Scripts\activate` de novo — o prompt precisa mostrar `(.venv)` |
| A lista vem com 167 municípios | Não filtrou pela mesorregião: são todos os municípios do RN |
| Chuva anual negativa | Os valores `-999` entraram na soma |
| Acento sai como `Ã§` no CSV | Falta `encoding="utf-8"` ao salvar, ou o Excel está abrindo como ANSI. Salvem em UTF-8 e abram pelo "Importar dados" do Excel |
| A API do IBGE devolve erro 500 de vez em quando | É normal. Coloquem uma tentativa de repetição e um `time.sleep` entre as chamadas |

---

# Sprint 2 — 29/09 a 05/10/2026
## A série histórica da mandioca, limpa e conferida

**Objetivo:** ao final da semana, ter um CSV com a série completa de área plantada, área colhida, quantidade produzida e rendimento da mandioca, para todos os municípios do Agreste, de 2000 até o último ano — e saber que ele está correto.

Esta é a sprint do **Aluno A**. O Aluno B trabalha em paralelo na Sprint 3, que já pode começar — as duas trilhas são independentes até a Sprint 4. Quem terminar primeiro ajuda o outro.

### Por que isso importa

Todo o trabalho vai ser construído em cima desta tabela. Um erro aqui — um município faltando, uma unidade trocada, um valor especial lido como número — contamina os modelos, os gráficos e as conclusões, e é **muito difícil de descobrir depois**. Vale gastar a semana inteira conferindo.

### O que vocês vão fazer

1. Baixar a série completa do SIDRA para todos os municípios e todos os anos.
2. Tratar os valores especiais do IBGE.
3. Calcular o rendimento e conferir contra a coluna do próprio IBGE.
4. Descrever a base: quantos municípios, quantos anos, quantos buracos.
5. Fazer os primeiros gráficos exploratórios.

### Passo a passo

**1. Baixar tudo.** Em `scripts/02_ibge_mandioca.py`, montem a URL da API com os códigos anotados na Sprint 1 e peçam **todos os municípios do Brasil** (`n6/all`) para as variáveis e o produto mandioca; depois filtrem pelos códigos do Agreste. É mais simples que pedir município por município, e a API aceita bem.

```python
import requests
import pandas as pd

VARIAVEIS = "..."          # os codigos anotados na Sprint 1
COD_MANDIOCA = "..."       # idem

url = (
    "https://apisidra.ibge.gov.br/values"
    f"/t/5457/n6/all/v/{VARIAVEIS}/p/all/c782/{COD_MANDIOCA}"
)

r = requests.get(url, timeout=600)
r.raise_for_status()
bruto = r.json()

# A primeira linha do retorno do SIDRA e o cabecalho descritivo, nao e dado.
cabecalho, registros = bruto[0], bruto[1:]
print("Cabecalho:", cabecalho)
print("Registros:", len(registros))

df = pd.DataFrame(registros)
df.to_csv("dados/brutos/sidra_mandioca_bruto.csv", index=False, encoding="utf-8")
```

**Salvem o bruto primeiro, sempre.** Se o script de limpeza quebrar amanhã, vocês não precisam baixar tudo de novo — e a rede do laboratório agradece.

Se a consulta inteira for pesada demais e der tempo esgotado, **quebrem por período**: um bloco de anos por vez, salvando cada bloco, e juntem depois. Cinco consultas de cinco anos funcionam melhor que uma de vinte e cinco.

**2. Entender o formato do SIDRA.** O retorno vem com colunas de nome numérico (`D1C`, `D1N`, `V`, ...), em que `N` é nome e `C` é código. Rodem isto e leiam com calma:

```python
print(cabecalho)          # diz o que e cada coluna
print(df.head(3).T)       # transposto, fica legivel
```

Renomeiem as colunas para nomes que vocês entendam: `codigo_ibge`, `municipio`, `ano`, `variavel`, `valor`, `unidade`.

**3. Tratar os valores especiais.** Esta é a parte que o IBGE não facilita. Nos dados da PAM, a coluna de valor pode conter:

| Símbolo | Significado | O que fazer |
|---|---|---|
| `-` | Zero absoluto (não houve produção) | Virar `0` |
| `..` | Não se aplica | Virar vazio (`NaN`) |
| `...` | Dado não disponível | Virar vazio (`NaN`) |
| `X` | Valor omitido para não identificar o informante | Virar vazio (`NaN`) |

```python
ESPECIAIS = {"-": "0", "..": None, "...": None, "X": None, "..X": None}

df["valor"] = df["valor"].replace(ESPECIAIS)
df["valor"] = pd.to_numeric(df["valor"], errors="coerce")
```

**Contem quantos de cada tipo apareceram e anotem.** Esse número vai para o artigo: *"em N% dos pares município-ano o valor foi omitido pelo IBGE"* é uma informação que um revisor da área valoriza, porque mostra que vocês olharam o dado.

**Nunca troquem `NaN` por zero.** "Não sei quanto foi" e "foi zero" são coisas diferentes, e confundir as duas é um erro grave de método: vai parecer que dezenas de municípios tiveram quebra total de safra.

**4. Passar para formato largo e calcular o rendimento.** Hoje cada variável está em uma linha. Vocês precisam de uma linha por município-ano:

```python
largo = df.pivot_table(
    index=["codigo_ibge", "municipio", "ano"],
    columns="variavel",
    values="valor",
).reset_index()

largo.columns.name = None
largo = largo.rename(columns={
    "Área plantada ou destinada à colheita": "area_plantada_ha",
    "Área colhida": "area_colhida_ha",
    "Quantidade produzida": "producao_t",
    "Rendimento médio da produção": "rendimento_ibge_kg_ha",
})

# o alvo do trabalho, calculado por voces
largo["rendimento_kg_ha"] = (largo["producao_t"] * 1000) / largo["area_colhida_ha"]
```

**5. Conferir contra o IBGE.** Aqui está a validação da sprint:

```python
comp = largo.dropna(subset=["rendimento_kg_ha", "rendimento_ibge_kg_ha"])
diferenca = (comp["rendimento_kg_ha"] - comp["rendimento_ibge_kg_ha"]).abs()
print("Linhas comparadas:", len(comp))
print("Diferenca media (kg/ha):", diferenca.mean().round(2))
print("Diferenca maxima (kg/ha):", diferenca.max().round(2))
print("Linhas com diferenca acima de 1 kg/ha:", (diferenca > 1).sum())
```

Diferenças de poucos quilos são arredondamento do IBGE e estão ótimas. Diferença grande em muitas linhas significa que alguma coluna foi trocada no `rename` — voltem e confiram.

**Guardem esse resultado em `docs/evidencias/`.** Ele é a prova de que a base foi montada certo, e vira uma frase na seção de Resultados do artigo.

**6. Descrever a base.** Respondam, com código, e anotem as respostas:

- Quantos municípios do Agreste aparecem com mandioca? (Pode ser menos que a lista completa.)
- Quantos anos tem a série?
- Quantos pares município-ano existem? Quantos estão completos?
- Qual o rendimento médio, mínimo e máximo? Existe algum valor absurdo (rendimento de 200.000 kg/ha, por exemplo)?
- Algum município tem área colhida zero e produção maior que zero? Isso é inconsistência da fonte — anotem e tratem.

```python
print(largo.groupby("ano")["rendimento_kg_ha"].describe())
```

**Um alerta importante:** a PAM municipal é construída em boa parte por **estimativa** de técnicos locais, não por censo. Isso significa que a série tem ruído, e em alguns municípios o valor se repete idêntico por vários anos seguidos. **Verifiquem isso** — contem quantas vezes o rendimento de um município é exatamente igual ao do ano anterior. Se for muito frequente, vocês encontraram uma limitação central do trabalho, que precisa estar no artigo e que ajuda a explicar por que a linha de base "repetir o ano anterior" é difícil de bater.

**7. Gráficos exploratórios.** Salvem em `graficos/`:

- A série do rendimento médio do Agreste ao longo dos anos (uma linha);
- A série de 4 ou 5 municípios escolhidos, no mesmo gráfico;
- Um histograma dos rendimentos;
- Um gráfico de barras com a produção total de mandioca do Agreste por ano.

Olhem esses gráficos com o orientador. Anos de queda brusca devem corresponder a secas conhecidas da região — a seca de 2012 a 2017 no semiárido é a referência mais óbvia. Se a queda aparecer, **vocês acabaram de ganhar a primeira validação externa do trabalho**, antes mesmo de treinar qualquer modelo.

**8. Salvar.** `dados/intermediarios/mandioca_agreste.csv`.

### Como saber que deu certo

- [ ] O CSV tem uma linha por município-ano, com área plantada, área colhida, produção e rendimento.
- [ ] O rendimento calculado bate com o do IBGE (diferença média abaixo de 1 kg/ha).
- [ ] Os valores especiais do IBGE foram tratados e contados.
- [ ] Vocês sabem responder quantos municípios, quantos anos e quantos buracos a base tem.
- [ ] Os quatro gráficos estão salvos.
- [ ] O dado bruto está guardado em `dados/brutos/`.

### Erros comuns

| Erro | O que está acontecendo |
|---|---|
| `could not convert string to float: '-'` | Faltou tratar os valores especiais antes do `to_numeric` |
| Rendimento na casa dos milhões | Produção em toneladas multiplicada errado, ou área colhida próxima de zero. Filtrem linhas com área colhida muito pequena e **declarem o filtro no artigo** |
| O `pivot_table` devolve tabela vazia | Os nomes das variáveis no `rename` não batem com o que veio do SIDRA. Imprimam os valores únicos da coluna antes |
| Faltam municípios | Um município sem produção de mandioca simplesmente não aparece na resposta do SIDRA. Isso é esperado — registrem quais |

---

# Sprint 3 — 06/10 a 12/10/2026
## O clima de todos os municípios, de todos os anos

**Objetivo:** ao final da semana, ter a série diária de chuva e temperatura de cada município do Agreste, para todo o período, guardada em disco.

Sprint do **Aluno B**. Se a Sprint 2 atrasou, o Aluno A continua nela — as trilhas ainda são independentes.

### O que vocês vão fazer

1. Montar o laço que percorre os municípios e baixa a série completa de cada um.
2. Fazer o script ser **retomável**: se cair na metade, continua de onde parou.
3. Consolidar tudo em um CSV diário único.
4. Conferir os dados contra o que se sabe do clima da região.

### Passo a passo

**1. Baixar a série completa de um município, do começo ao fim do período.** Evoluam o script da Sprint 1 para pedir de `20000101` até o último dia do último ano. A NASA POWER aceita séries longas em uma única chamada — são cerca de 9.000 dias, o que dá um JSON de poucos megabytes.

**2. O laço com retomada.** Este é o padrão mais importante que vocês vão aprender nesta sprint: **nunca escrevam um laço longo que perde tudo se cair**.

```python
import os
import json
import time
import requests
import pandas as pd

coords = pd.read_csv("dados/final/coordenadas.csv")
INICIO, FIM = "20000101", "20231231"      # confirme o ano final
PASTA = "dados/brutos/nasa"
os.makedirs(PASTA, exist_ok=True)

for _, linha in coords.iterrows():
    codigo = int(linha["codigo_ibge"])
    destino = f"{PASTA}/{codigo}.json"

    if os.path.exists(destino):          # ja baixei, pulo
        print("ja existe:", linha["municipio"])
        continue

    parametros = {
        "parameters": "PRECTOTCORR,T2M,T2M_MAX,T2M_MIN",
        "community": "AG",
        "latitude": linha["latitude"],
        "longitude": linha["longitude"],
        "start": INICIO,
        "end": FIM,
        "format": "JSON",
    }

    try:
        r = requests.get(
            "https://power.larc.nasa.gov/api/temporal/daily/point",
            params=parametros, timeout=300,
        )
        r.raise_for_status()
    except Exception as erro:
        print("ERRO em", linha["municipio"], erro)
        continue                          # tenta de novo na proxima execucao

    with open(destino, "w", encoding="utf-8") as arq:
        json.dump(r.json(), arq)

    print("ok:", linha["municipio"])
    time.sleep(2)                         # educacao com a API
```

Rodem, deixem terminar, e **rodem de novo**. Na segunda vez ele deve dizer "já existe" para todos e não baixar nada. Isso prova que a retomada funciona. Se algum município deu erro na primeira passada, a segunda execução pega só ele.

**Meçam o tempo total.** `time.time()` no começo e no fim, e anotem. Esse número vai para o artigo, na parte de custo computacional.

**3. Consolidar em um CSV diário.** Leiam os JSON e montem uma tabela longa: uma linha por município-dia.

```python
import glob

linhas = []
for caminho in glob.glob(f"{PASTA}/*.json"):
    codigo = int(os.path.basename(caminho).replace(".json", ""))
    with open(caminho, encoding="utf-8") as arq:
        dados = json.load(arq)

    parametros = dados["properties"]["parameter"]
    for data_txt in parametros["PRECTOTCORR"]:
        linhas.append({
            "codigo_ibge": codigo,
            "data": data_txt,
            "chuva_mm": parametros["PRECTOTCORR"][data_txt],
            "temp_media": parametros["T2M"][data_txt],
            "temp_max": parametros["T2M_MAX"][data_txt],
            "temp_min": parametros["T2M_MIN"][data_txt],
        })

clima = pd.DataFrame(linhas)
clima["data"] = pd.to_datetime(clima["data"], format="%Y%m%d")

# valores faltantes da NASA POWER
for coluna in ["chuva_mm", "temp_media", "temp_max", "temp_min"]:
    clima.loc[clima[coluna] <= -900, coluna] = pd.NA

clima.to_csv("dados/intermediarios/clima_diario.csv", index=False)
print("Linhas:", len(clima), "| Municipios:", clima["codigo_ibge"].nunique())
```

**Não comitem o CSV diário nem os JSON.** São arquivos grandes; ponham no `.gitignore`. O que vai para o Git é o resultado agregado da Sprint 4. Deixem claro no `README.md` como regerá-los — reprodutibilidade não exige comitar dado bruto, exige que o script que o baixa esteja lá.

**4. Conferir o clima.** Quatro checagens, todas rápidas:

- **Total anual por município:** deve ficar entre 400 e 900 mm na maioria dos casos. Imprimam a tabela e olhem.
- **Sazonalidade:** a chuva média por mês, somando todos os municípios. O Agreste potiguar tem estação chuvosa concentrada mais ou menos de **fevereiro a julho**, com pico por volta de março-abril, e uma estiagem marcada no segundo semestre. Se o gráfico mostrar chuva espalhada igualmente pelo ano, tem erro.
- **Temperatura:** média por volta de 24 a 27 °C. Se der 5 °C ou 40 °C, tem coordenada errada.
- **Faltantes:** quantos dias sem dado, por município. Deve ser quase zero.

Façam um **gráfico da chuva média mensal** e comparem com o que a literatura descreve para o Agreste. Essa é a validação da sprint, e a figura pode até entrar no artigo, na caracterização da área de estudo.

**Se sobrar tempo (opcional, mas rende no artigo):** escolham uma estação do INMET dentro do Agreste, baixem a série de chuva dela pelo portal do BDMEP e comparem com a série da NASA POWER no mesmo ponto e período. Se as duas concordarem razoavelmente, vocês têm uma **validação independente da fonte de clima**, o que é um argumento forte na seção de Materiais e Métodos.

### Como saber que deu certo

- [ ] Existe um JSON por município em `dados/brutos/nasa/`.
- [ ] Rodar o script de novo não baixa nada (retomada funcionando).
- [ ] O CSV diário tem aproximadamente (nº de municípios × nº de dias) linhas.
- [ ] Os totais anuais, a sazonalidade e as temperaturas passaram nas quatro checagens.
- [ ] O tempo total de download está anotado no diário.

### Erros comuns

| Erro | O que está acontecendo |
|---|---|
| Tempo esgotado no meio do laço | Normal. É para isso que serve a retomada: rode de novo |
| `KeyError: 'PRECTOTCORR'` | A API devolveu erro em vez de dados. Imprimam `r.text` para ver a mensagem |
| Chuva total anual de 20.000 mm | Os `-999` viraram positivos, ou a unidade está trocada |
| O CSV diário tem 3 GB | Vocês pediram todos os parâmetros da API. Peçam só os quatro da lista |
| Todos os municípios com a mesma chuva | O laço está usando sempre a mesma coordenada — provavelmente uma variável fora do laço |

---

# Sprint 4 — 13/10 a 19/10/2026
## As variáveis climáticas e a tabela final

**Objetivo:** ao final da semana, ter o arquivo `dados/final/base_modelagem.csv`: uma linha por município-ano, com o rendimento da mandioca e as variáveis climáticas que vão tentar explicá-lo.

Esta é a sprint em que as duas trilhas se encontram. **É a sprint mais importante do trabalho depois da Sprint 5** — a qualidade das variáveis criadas aqui determina o teto do que os modelos vão conseguir.

### A ideia, explicada

A mandioca não tem ciclo de um ano civil. Ela é plantada no começo da estação chuvosa e colhida **12 a 18 meses depois**. Quando o IBGE registra a colheita de 2020, boa parte da água que fez aquela raiz crescer caiu em **2019**.

Isso tem uma consequência direta: **não adianta usar só a chuva do ano da colheita**. Vocês precisam de variáveis que cubram o ciclo inteiro, incluindo o ano anterior.

E tem uma consequência metodológica ainda mais importante: essa defasagem é o que torna a previsão **útil**. Se o rendimento de 2020 depende da chuva de 2019 e do começo de 2020, dá para estimar a safra **antes da colheita**. É exatamente isso que o observatório quer.

**Conversem com o orientador sobre o calendário real da mandioca na região** antes de fechar as janelas de tempo. Se ele souber (ou souber quem saiba) o mês típico de plantio e de colheita no Agreste, as variáveis ficam muito melhores. Se não houver essa informação, usem as janelas sugeridas abaixo e **digam no artigo que foram definidas a partir do regime de chuvas da região**, não por informação de campo.

### O que vocês vão fazer

1. **Aluno B:** criar as variáveis climáticas por município-ano.
2. **Aluno A:** juntar clima e produção e gerar a base final.
3. Os dois: conferir a base junta e fazer os primeiros gráficos de relação.

### Passo a passo

**1. Definir o "ano-safra" (Aluno B).** Para o rendimento registrado no ano `Y`, proponham estas janelas:

| Variável | Janela | Por quê |
|---|---|---|
| `chuva_ano_anterior` | jan a dez de `Y-1` | Cobre o plantio e o crescimento do ciclo longo |
| `chuva_chuvosa_anterior` | fev a jul de `Y-1` | A estação chuvosa em que a roça foi plantada |
| `chuva_seca_anterior` | ago a dez de `Y-1` | O estresse hídrico do segundo semestre |
| `chuva_chuvosa_atual` | fev a jul de `Y` | A última chuva antes da colheita |
| `chuva_12m` | jul de `Y-1` a jun de `Y` | Os 12 meses que antecedem a colheita típica |
| `dias_secos_max_anterior` | maior sequência de dias sem chuva em `Y-1` | Veranico: mede o pior momento, não a média |
| `dias_com_chuva_anterior` | dias com chuva > 1 mm em `Y-1` | Distribuição: 600 mm bem espalhados ≠ 600 mm em duas semanas |
| `temp_media_anterior` | média de `T2M` em `Y-1` | |
| `temp_max_media_chuvosa` | média de `T2M_MAX` na estação chuvosa de `Y-1` | Calor durante o crescimento |

Isso dá 9 variáveis climáticas. **Não inventem mais do que isso.** Com cerca de mil linhas, muita variável só aumenta o risco de o modelo decorar ruído.

Esqueleto do cálculo:

```python
import pandas as pd
import numpy as np

clima = pd.read_csv("dados/intermediarios/clima_diario.csv", parse_dates=["data"])
clima["ano"] = clima["data"].dt.year
clima["mes"] = clima["data"].dt.month


def maior_sequencia_seca(serie_chuva, limiar=1.0):
    """Maior numero de dias consecutivos com chuva abaixo do limiar."""
    seco = (serie_chuva.fillna(0) < limiar).astype(int)
    maior = atual = 0
    for valor in seco:
        atual = atual + 1 if valor else 0
        maior = max(maior, atual)
    return maior


def resumo_do_ano(grupo):
    chuvosa = grupo[grupo["mes"].between(2, 7)]
    seca = grupo[grupo["mes"].between(8, 12)]
    return pd.Series({
        "chuva_total": grupo["chuva_mm"].sum(),
        "chuva_chuvosa": chuvosa["chuva_mm"].sum(),
        "chuva_seca": seca["chuva_mm"].sum(),
        "dias_secos_max": maior_sequencia_seca(grupo["chuva_mm"]),
        "dias_com_chuva": (grupo["chuva_mm"] > 1).sum(),
        "temp_media": grupo["temp_media"].mean(),
        "temp_max_media_chuvosa": chuvosa["temp_max"].mean(),
    })


anual = (
    clima.groupby(["codigo_ibge", "ano"])
    .apply(resumo_do_ano)
    .reset_index()
)
anual.to_csv("dados/intermediarios/clima_anual.csv", index=False)
```

**2. Criar as versões defasadas (Aluno B).** Agora vem o passo que exige cuidado. Para cada município, as variáveis do ano anterior viram colunas da linha do ano atual:

```python
anual = anual.sort_values(["codigo_ibge", "ano"])

colunas_clima = ["chuva_total", "chuva_chuvosa", "chuva_seca",
                 "dias_secos_max", "dias_com_chuva", "temp_media",
                 "temp_max_media_chuvosa"]

for coluna in colunas_clima:
    anual[f"{coluna}_ant"] = anual.groupby("codigo_ibge")[coluna].shift(1)
```

**O `groupby` antes do `shift` não é detalhe.** Sem ele, a última linha de um município puxa o valor do primeiro ano do município seguinte, e vocês não têm como perceber olhando a planilha. Confiram: ordenem por município e ano, imprimam as 30 primeiras linhas e verifiquem à mão que `chuva_total_ant` da linha de 2005 é igual a `chuva_total` da linha de 2004 **do mesmo município**.

**3. Juntar as duas bases (Aluno A).**

```python
producao = pd.read_csv("dados/intermediarios/mandioca_agreste.csv")
clima_anual = pd.read_csv("dados/intermediarios/clima_anual.csv")

base = producao.merge(clima_anual, on=["codigo_ibge", "ano"], how="inner")

print("Producao:", len(producao))
print("Clima:", len(clima_anual))
print("Base juntada:", len(base))
```

**Olhem esses três números.** Se a base juntada tiver muito menos linhas que a de produção, a junção falhou — quase sempre porque o `codigo_ibge` está como texto de um lado e número do outro, ou porque um deles tem 6 dígitos e o outro 7. Conferir tipo de chave é a primeira coisa a fazer quando um `merge` "come" linhas.

**4. Acrescentar as variáveis do próprio histórico (Aluno A).** Além do clima, dois preditores óbvios:

```python
base = base.sort_values(["codigo_ibge", "ano"])
base["rendimento_ant"] = base.groupby("codigo_ibge")["rendimento_kg_ha"].shift(1)
base["rendimento_ant2"] = base.groupby("codigo_ibge")["rendimento_kg_ha"].shift(2)
base["area_plantada_ant"] = base.groupby("codigo_ibge")["area_plantada_ha"].shift(1)
```

**Um aviso que vale o trabalho inteiro:** repare que **tudo** aqui é `shift(1)` ou `shift(2)` — informação do passado. Nunca criem uma variável que use o ano que está sendo previsto, e nunca usem a média histórica calculada sobre a série toda (ela contém os anos de teste). Isso se chama **vazamento de dados** (*data leakage*), produz resultados excelentes e completamente falsos, e é o erro número um de quem está começando. Na Sprint 5 vocês vão ver como calcular médias históricas do jeito certo.

**5. Limpar e fechar a base.**

- Removam as linhas em que o alvo (`rendimento_kg_ha`) está vazio — não dá para treinar nem avaliar sem ele. **Contem quantas foram** e registrem.
- Removam o primeiro ano de cada município, que não tem `_ant`.
- Decidam o que fazer com linhas em que uma variável climática está vazia. Com poucas, removam; se forem muitas, avisem o orientador.
- Definam um filtro de área mínima (por exemplo, área colhida de pelo menos 5 ha) para evitar rendimentos absurdos calculados sobre áreas minúsculas. **Registrem o filtro e quantas linhas ele tirou** — isso vai para Materiais e Métodos.

```python
base.to_csv("dados/final/base_modelagem.csv", index=False)
print(base.shape)
print(base.isna().sum())
```

**6. Os primeiros gráficos de relação (os dois juntos).** Antes de qualquer modelo, olhem os dados:

- Dispersão de `chuva_ano_anterior` × `rendimento_kg_ha`, todos os municípios e anos;
- O mesmo, mas para `chuva_chuvosa_anterior`;
- Dispersão de `dias_secos_max_ant` × `rendimento_kg_ha`;
- Matriz de correlação entre as variáveis climáticas e o rendimento (`base.corr(numeric_only=True)["rendimento_kg_ha"].sort_values()`).

**Levem essa matriz para a reunião.** Se nenhuma variável climática tiver correlação acima de 0,2 com o rendimento, é um sinal precoce e muito importante: os modelos provavelmente não vão bater a linha de base, e o artigo vai ser sobre **por que** o clima sozinho não explica a produção municipal de mandioca. Esse artigo é publicável — não é um fracasso. Mas é melhor saber disso na Sprint 4 do que na Sprint 7.

### Como saber que deu certo

- [ ] `dados/final/base_modelagem.csv` existe, com uma linha por município-ano.
- [ ] A junção não perdeu linhas inesperadamente, e vocês sabem explicar as que se perderam.
- [ ] As colunas `_ant` foram conferidas à mão em pelo menos 30 linhas.
- [ ] Nenhuma variável usa informação do ano que será previsto.
- [ ] A matriz de correlação está calculada e foi discutida com o orientador.
- [ ] Os quatro gráficos estão em `graficos/`.

### Erros comuns

| Erro | O que está acontecendo |
|---|---|
| O `merge` devolve quase nada | Tipo da chave diferente entre as tabelas. Forcem `astype(int)` nos dois lados |
| `chuva_total_ant` vazia em todas as linhas | Falta ordenar por ano antes do `shift`, ou o `groupby` ficou de fora |
| `SettingWithCopyWarning` | Vocês criaram uma fatia e escreveram nela. Usem `.copy()` ao filtrar |
| Correlação perfeita (1,0) com alguma variável | Vazamento. Alguma coluna é o próprio alvo disfarçado — produção e área colhida, por exemplo, reconstroem o rendimento exatamente |

---

# Sprint 5 — 20/10 a 26/10/2026
## A linha de base e a validação temporal

**Objetivo:** ao final da semana, ter a **linha de base** medida e a **função de avaliação** pronta. Nenhum modelo de aprendizado de máquina ainda.

Se houver uma sprint para não atropelar, é esta. Ela define o padrão de comparação do artigo inteiro.

### Por que isso importa

Imaginem que vocês treinam um Random Forest e ele erra, em média, 1.800 kg/ha. Isso é bom ou ruim?

Não dá para responder. Falta o padrão de comparação. Se simplesmente **repetir o rendimento do ano anterior** errasse 1.700 kg/ha, o modelo é pior que não fazer nada — e teria custado quatro semanas de trabalho.

A linha de base é o que transforma um número solto em um resultado. E em previsão agrícola municipal ela costuma ser **difícil de bater**, porque o rendimento de um município é bastante estável de um ano para outro. Saibam disso desde já: **bater a linha de base é a conquista do trabalho, não o ponto de partida.**

### A validação temporal, explicada

O jeito comum de avaliar um modelo é sortear 80% das linhas para treino e 20% para teste. **Aqui isso está errado**, e o motivo é importante o suficiente para virar parágrafo no artigo.

Se vocês sorteiam, o modelo pode treinar com o ano de 2021 de um município e ser testado no ano de 2018 do mesmo município — ou seja, ele usa o **futuro** para prever o **passado**. O resultado fica ótimo e não significa nada, porque na vida real o observatório vai prever 2027 sabendo apenas até 2026.

O jeito certo é a **validação temporal com janela expansiva**:

```
treina com 2001..2014  →  testa em 2015
treina com 2001..2015  →  testa em 2016
treina com 2001..2016  →  testa em 2017
...
treina com 2001..2022  →  testa em 2023
```

Cada ano de teste é previsto por um modelo que nunca o viu, nem viu nada depois dele. No fim, juntam-se todas as previsões de teste e calculam-se as métricas. É mais trabalhoso e é a única forma honesta de responder à pergunta do artigo.

### O que vocês vão fazer

1. **Aluno A:** escrever as três linhas de base.
2. **Aluno B:** escrever a função de validação temporal.
3. Os dois: rodar e registrar as métricas das linhas de base.

### Passo a passo

**1. As três linhas de base (Aluno A).**

| Linha de base | Previsão para o município M no ano Y |
|---|---|
| **B1 — Persistência** | O rendimento de M em `Y-1` |
| **B2 — Média móvel** | A média do rendimento de M nos 3 anos anteriores |
| **B3 — Média histórica** | A média do rendimento de M **em todos os anos de treino** |

A B1 é a previsão ingênua clássica e provavelmente a mais difícil de bater. A B3 precisa de cuidado: a média tem de ser calculada **somente com os anos de treino**, nunca com a série completa. Aqui está a diferença entre método certo e método furado.

**2. As três métricas.**

| Métrica | O que significa | Cuidado |
|---|---|---|
| **MAE** | Erro absoluto médio, em kg/ha. O mais fácil de explicar | — |
| **RMSE** | Penaliza mais os erros grandes. Útil porque errar feio em ano de seca é pior que errar pouco sempre | Sempre maior ou igual ao MAE |
| **MAPE** | Erro percentual médio. Permite comparar municípios de rendimentos diferentes | **Explode se algum rendimento for zero ou muito baixo.** Filtrem esses casos e digam no artigo que filtraram |

```python
import numpy as np
from sklearn.metrics import mean_absolute_error, mean_squared_error


def metricas(y_real, y_previsto):
    y_real = np.asarray(y_real, dtype=float)
    y_previsto = np.asarray(y_previsto, dtype=float)
    mae = mean_absolute_error(y_real, y_previsto)
    rmse = np.sqrt(mean_squared_error(y_real, y_previsto))
    valido = y_real > 0
    mape = np.mean(np.abs((y_real[valido] - y_previsto[valido]) / y_real[valido])) * 100
    return {"MAE": round(mae, 1), "RMSE": round(rmse, 1), "MAPE": round(mape, 1)}
```

**3. A função de validação temporal (Aluno B).** Esta função é o coração do trabalho. Escrevam com calma e testem:

```python
import pandas as pd

VARIAVEIS = [
    "chuva_total_ant", "chuva_chuvosa_ant", "chuva_seca_ant",
    "dias_secos_max_ant", "dias_com_chuva_ant", "temp_media_ant",
    "temp_max_media_chuvosa_ant", "chuva_chuvosa", "chuva_total",
    "rendimento_ant", "rendimento_ant2",
]
ALVO = "rendimento_kg_ha"
PRIMEIRO_ANO_TESTE = 2015


def validacao_temporal(base, criar_modelo, variaveis=VARIAVEIS):
    """Treina com o passado e testa em cada ano, um de cada vez.

    criar_modelo: funcao sem argumentos que devolve um modelo novo do
    scikit-learn (nao passe um modelo ja treinado: cada ano precisa do seu).
    """
    resultados = []
    anos_de_teste = sorted(a for a in base["ano"].unique() if a >= PRIMEIRO_ANO_TESTE)

    for ano in anos_de_teste:
        treino = base[base["ano"] < ano].dropna(subset=variaveis + [ALVO])
        teste = base[base["ano"] == ano].dropna(subset=variaveis + [ALVO])
        if len(treino) < 50 or len(teste) == 0:
            continue

        modelo = criar_modelo()
        modelo.fit(treino[variaveis], treino[ALVO])
        previsto = modelo.predict(teste[variaveis])

        resultados.append(pd.DataFrame({
            "ano": ano,
            "codigo_ibge": teste["codigo_ibge"].values,
            "municipio": teste["municipio"].values,
            "real": teste[ALVO].values,
            "previsto": previsto,
        }))

    return pd.concat(resultados, ignore_index=True)
```

**Reparem no `dropna` dentro do laço e no modelo novo a cada ano.** Reaproveitar um modelo já treinado entre os anos faz o ano seguinte enxergar o anterior de um jeito que não estava previsto; criar um novo a cada iteração é o que mantém a avaliação limpa.

**4. Avaliar as linhas de base.** As linhas de base não são modelos do `scikit-learn`, então avaliem direto:

```python
base = pd.read_csv("dados/final/base_modelagem.csv")
teste = base[base["ano"] >= PRIMEIRO_ANO_TESTE].dropna(subset=["rendimento_ant", ALVO])

print("B1 persistencia:", metricas(teste[ALVO], teste["rendimento_ant"]))
```

Para a B3, calculem a média histórica **ano a ano**, dentro do mesmo laço da validação temporal, usando só os anos anteriores. Escrevam esse laço explicitamente — é a demonstração de que vocês entenderam o problema do vazamento.

**5. Registrar.** Criem `resultados/metricas.csv` com uma linha por modelo:

| modelo | MAE | RMSE | MAPE | ganho_sobre_B1 |
|---|---|---|---|---|
| B1 – persistência | ... | ... | ... | 0,0% |
| B2 – média móvel 3 anos | ... | ... | ... | ... |
| B3 – média histórica | ... | ... | ... | ... |

O `ganho_sobre_B1` é `(MAE_B1 - MAE_modelo) / MAE_B1 × 100`. **Esta coluna é o número central do artigo.**

**6. Um gráfico que vale a sprint.** Para 3 ou 4 municípios, ponham no mesmo eixo o rendimento real ao longo dos anos e a previsão da B1. Vocês vão ver a linha da previsão **atrasada um ano** em relação à real. Esse gráfico explica visualmente, para qualquer leitor, o que uma linha de base de persistência faz — e por que ela é boa quando a série é estável e ruim quando há quebra de safra.

### Como saber que deu certo

- [ ] `resultados/metricas.csv` tem as três linhas de base com MAE, RMSE e MAPE.
- [ ] A função `validacao_temporal` roda sem erro e devolve uma linha por município-ano testado.
- [ ] Nenhuma média histórica foi calculada com anos de teste. **Os dois alunos conseguem explicar por que isso importa.**
- [ ] Vocês sabem qual é a linha de base mais difícil de bater e por quê.
- [ ] O gráfico da persistência está salvo.

### Erros comuns

| Erro | O que está acontecendo |
|---|---|
| MAPE gigante (milhares de por cento) | Rendimentos próximos de zero no denominador. Filtrem e digam no artigo |
| A validação devolve tabela vazia | O primeiro ano de teste está depois do último ano da base, ou o `dropna` limpou tudo (alguma variável está toda vazia) |
| O erro cai quando você usa mais variáveis do futuro | Vazamento. Revisem a lista `VARIAVEIS`: `producao_t` e `area_colhida_ha` do ano atual **não podem estar lá** |
| A linha de base parece boa demais | Provavelmente é. Confiram se `rendimento_ant` está mesmo defasado |

---

# Sprint 6 — 27/10 a 02/11/2026
## Os modelos: regressão linear e Random Forest

**Objetivo:** ao final da semana, ter três modelos avaliados exatamente com o mesmo protocolo das linhas de base, e a tabela comparativa completa.

Agora que a régua existe, medir é rápido. É por isso que esta sprint parece a mais importante e não é.

### O que vocês vão fazer

1. **Aluno A:** regressão linear (e Ridge).
2. **Aluno B:** Random Forest.
3. Os dois: a tabela comparativa e o gráfico de dispersão real × previsto.

### Passo a passo

**1. Regressão linear (Aluno A).** É o modelo mais simples e o mais fácil de explicar no artigo: ele ajusta uma reta (em várias dimensões) entre as variáveis e o alvo.

Variáveis em escalas muito diferentes (chuva em centenas de mm, temperatura em dezenas de °C, rendimento em milhares de kg/ha) atrapalham a regressão regularizada. A solução é padronizar, e o `Pipeline` do `scikit-learn` faz isso **dentro de cada treino**, que é o jeito certo — padronizar antes de separar treino e teste é outra forma de vazamento:

```python
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression, Ridge


def criar_linear():
    return make_pipeline(StandardScaler(), LinearRegression())


def criar_ridge():
    return make_pipeline(StandardScaler(), Ridge(alpha=1.0, random_state=42))


previsoes = validacao_temporal(base, criar_linear)
print("Regressao linear:", metricas(previsoes["real"], previsoes["previsto"]))
```

**Guardem os coeficientes** do modelo treinado com a série completa (só para interpretação, não para avaliação): eles dizem se mais chuva no ano anterior está associada a mais ou menos rendimento, e em que magnitude. Isso rende discussão no artigo.

**2. Random Forest (Aluno B).** É um conjunto de muitas árvores de decisão, cada uma treinada em uma amostra diferente dos dados; a previsão é a média delas. Ele capta relações que não são retas — por exemplo, "chuva ajuda até certo ponto, depois o excesso atrapalha" — e não precisa de padronização.

```python
from sklearn.ensemble import RandomForestRegressor


def criar_rf():
    return RandomForestRegressor(
        n_estimators=300,
        min_samples_leaf=3,
        random_state=42,
        n_jobs=-1,
    )


previsoes_rf = validacao_temporal(base, criar_rf)
print("Random Forest:", metricas(previsoes_rf["real"], previsoes_rf["previsto"]))
```

Sobre os parâmetros: `n_estimators=300` é número de árvores (mais é melhor até estabilizar, e custa tempo); `min_samples_leaf=3` impede que uma folha da árvore fique com uma linha só, o que é a principal defesa contra decorar os dados em base pequena. **Não saiam ajustando parâmetro no escuro.** Se quiserem testar, testem **dois ou três valores de `min_samples_leaf`**, registrem todos os resultados na tabela e **declarem no artigo que testaram**. Ajuste escondido é um problema de método.

**3. A tabela comparativa (os dois).** Acrescentem as linhas em `resultados/metricas.csv`:

| modelo | MAE | RMSE | MAPE | ganho sobre B1 | tempo de treino |
|---|---|---|---|---|---|
| B1 – persistência | | | | 0,0% | — |
| B2 – média móvel | | | | | — |
| B3 – média histórica | | | | | — |
| Regressão linear | | | | | |
| Ridge | | | | | |
| Random Forest | | | | | |

**Esta tabela é a figura central do artigo.** Formatem com cuidado desde já, porque ela vai direto para a seção de Resultados.

**4. O gráfico real × previsto (os dois).** Para o melhor modelo e para a B1, façam um gráfico de dispersão com o rendimento real no eixo X e o previsto no eixo Y, mais a **reta de 45 graus** (previsão perfeita). Os pontos devem se distribuir em torno da reta.

Olhem o padrão, porque ele diz coisas:

- Pontos espalhados na horizontal significam que o modelo prevê quase a mesma coisa para todo mundo — sinal de que ele não aprendeu nada útil e está chutando a média;
- Pontos acima da reta na parte baixa e abaixo na parte alta significam que o modelo **encolhe para a média**: subestima os rendimentos altos e superestima os baixos. Isso é comum e precisa ser discutido, porque significa que o modelo é ruim exatamente nos extremos — que é onde o planejamento territorial precisa dele.

**5. Rodem tudo duas vezes.** Com `random_state=42` fixo, os números têm de ser idênticos. Se mudarem, tem uma semente solta em algum lugar. Isso não é frescura: o artigo precisa ser reprodutível, e vocês vão precisar recalcular tudo depois de qualquer ajuste na base.

### Como saber que deu certo

- [ ] Os três modelos foram avaliados com **exatamente a mesma** função de validação temporal das linhas de base.
- [ ] `resultados/metricas.csv` está completo.
- [ ] Vocês sabem dizer, em uma frase, se algum modelo bateu a linha de base e por quanto.
- [ ] Os gráficos de dispersão estão salvos.
- [ ] Duas execuções seguidas dão exatamente os mesmos números.

### Erros comuns

| Erro | O que está acontecendo |
|---|---|
| A regressão linear devolve previsões absurdas (negativas, ou milhões) | Alguma variável com escala muito diferente e forte colinearidade. Usem o Ridge e verifiquem a matriz de correlação entre as variáveis |
| O Random Forest acerta quase perfeitamente | Vazamento. Quase certamente `producao_t` ou `area_colhida_ha` do ano atual entrou na lista de variáveis |
| `ValueError: Input contains NaN` | Faltou `dropna` nas variáveis usadas |
| O Random Forest demora muito | Reduzam `n_estimators` para 100. Com mil linhas deve levar segundos — se demorar minutos, algo está errado |

---

# Sprint 7 — 03/11 a 09/11/2026
## Onde o modelo erra e o que ele olha

**Objetivo:** ao final da semana, saber **quais variáveis importam**, **em que anos e municípios o modelo erra mais**, e ter todos os gráficos do artigo prontos.

É a sprint que transforma uma tabela de métricas em discussão científica. Sem ela, o artigo tem resultado mas não tem análise.

### O que vocês vão fazer

1. **Aluno B:** importância das variáveis e o modelo com *boosting*.
2. **Aluno A:** análise de erro por ano e por município.
3. Os dois: fechar o conjunto de figuras.

### Passo a passo

**1. Importância por permutação (Aluno B).** O Random Forest tem um atributo `feature_importances_`, mas ele é **enviesado**: favorece variáveis com muitos valores distintos. A forma correta é a **importância por permutação**: embaralhar os valores de uma variável e medir o quanto a previsão piora. Se piorar muito, a variável importava.

```python
from sklearn.inspection import permutation_importance

treino = base[base["ano"] < 2015].dropna(subset=VARIAVEIS + [ALVO])
teste = base[base["ano"] >= 2015].dropna(subset=VARIAVEIS + [ALVO])

modelo = criar_rf()
modelo.fit(treino[VARIAVEIS], treino[ALVO])

resultado = permutation_importance(
    modelo, teste[VARIAVEIS], teste[ALVO],
    n_repeats=20, random_state=42, scoring="neg_mean_absolute_error",
)

importancia = (
    pd.DataFrame({
        "variavel": VARIAVEIS,
        "importancia": resultado.importances_mean,
        "desvio": resultado.importances_std,
    })
    .sort_values("importancia", ascending=False)
)
print(importancia)
importancia.to_csv("resultados/importancia.csv", index=False)
```

Façam um **gráfico de barras horizontais** com esse resultado. Ele vai para o artigo.

**O que esperar, e como discutir cada caso:**

- Se `rendimento_ant` dominar tudo e as variáveis climáticas ficarem perto de zero, o resultado é: **o melhor preditor do rendimento de um município é o próprio rendimento passado, e o clima acrescenta pouco**. Esse é um achado legítimo e interessante, e explica por que a linha de base é difícil de bater. Discutam as razões: a PAM municipal é em parte estimada e tem inércia; o clima varia menos entre municípios vizinhos do que a produção varia entre eles; a mandioca é uma cultura notoriamente resistente à seca, o que pode atenuar o efeito da chuva justamente nesta cultura.
- Se alguma variável de chuva aparecer com peso relevante, **digam qual janela** e liguem isso ao ciclo da cultura. É o resultado mais interessante possível para o artigo.
- Se `dias_secos_max_ant` pesar mais que `chuva_total_ant`, vocês têm um achado bonito: **a distribuição da chuva importa mais que o total**. Essa frase é quase um título.

**2. O modelo com *boosting* (Aluno B).** Uma terceira família de modelos, já incluída no `scikit-learn`:

```python
from sklearn.ensemble import HistGradientBoostingRegressor


def criar_boosting():
    return HistGradientBoostingRegressor(
        max_iter=300, learning_rate=0.05,
        min_samples_leaf=5, random_state=42,
    )
```

Avaliem com a mesma função de sempre e acrescentem a linha na tabela. **Não gastem mais de um dia nisso.** Se não melhorar, é um resultado — e um resultado que reforça a conclusão.

**3. Erro por ano (Aluno A).**

```python
por_ano = previsoes_rf.copy()
por_ano["erro_abs"] = (por_ano["real"] - por_ano["previsto"]).abs()
print(por_ano.groupby("ano")["erro_abs"].agg(["mean", "median", "count"]))
```

Façam um gráfico de barras do MAE por ano, com as barras do modelo e da linha de base lado a lado.

**A pergunta a responder:** o erro é maior nos **anos de seca**? Cruzem com os totais de chuva que vocês já têm e com os anos que a ANA reconheceu como de seca no semiárido. Se o modelo erra mais justamente nos anos extremos, isso é uma limitação séria e **precisa estar em destaque no artigo**, porque é nesses anos que uma previsão seria mais valiosa. Um modelo que só funciona quando nada de interessante acontece não serve ao observatório — e dizer isso com clareza é o que separa um trabalho honesto de um trabalho decorativo.

**4. Erro por município (Aluno A).** Mesma conta, agrupando por município. Listem os 5 municípios de maior e de menor erro e investiguem: os de maior erro têm área plantada pequena? Série muito irregular? Muitos anos com dado omitido pelo IBGE? Essa investigação vale um parágrafo forte de discussão.

Se der tempo, façam um **mapa simples** do MAE por município. Não precisa de `geopandas`: um gráfico de dispersão das coordenadas com a cor proporcional ao erro já comunica a ideia, e custa cinco linhas de `matplotlib`.

**5. Fechar o conjunto de figuras (os dois).** O artigo deve ter, no máximo, 6 a 8 figuras. Sugestão:

| # | Figura | De onde vem |
|---|---|---|
| 1 | Mapa ou lista dos municípios estudados | Sprint 1 |
| 2 | Chuva média mensal do Agreste (caracterização) | Sprint 3 |
| 3 | Série histórica do rendimento da mandioca | Sprint 2 |
| 4 | Dispersão chuva × rendimento | Sprint 4 |
| 5 | **Tabela comparativa de modelos** | Sprint 6 |
| 6 | Real × previsto do melhor modelo | Sprint 6 |
| 7 | **Importância das variáveis** | Sprint 7 |
| 8 | MAE por ano, modelo × linha de base | Sprint 7 |

Salvem todas em **PNG com 300 dpi** (`plt.savefig(caminho, dpi=300, bbox_inches="tight")`), com **eixos rotulados e unidades**. Figura de artigo sem unidade no eixo volta da revisão.

### Como saber que deu certo

- [ ] A tabela de importância está calculada por permutação e o gráfico está salvo.
- [ ] O modelo com *boosting* está na tabela comparativa.
- [ ] Vocês sabem responder: o erro é maior em anos secos?
- [ ] Os 5 municípios de maior erro foram investigados e há uma hipótese para cada.
- [ ] As figuras do artigo estão salvas em 300 dpi, com eixos rotulados.

### Erros comuns

| Erro | O que está acontecendo |
|---|---|
| `permutation_importance` demora demais | Reduzam `n_repeats` para 10 |
| Todas as importâncias dão zero ou negativo | O modelo não aprendeu nada além da média. É um resultado — verifiquem antes se não há erro na base |
| O gráfico de barras sai ilegível | Usem barras horizontais e ordenem por importância |
| Os números mudam a cada execução | Falta `random_state` em algum lugar |

---

# Sprint 8 — 10/11 a 16/11/2026
## Fechamento: reprodutibilidade, MySQL e recomendação

**Objetivo:** ao final da semana, qualquer pessoa deve conseguir clonar o repositório, rodar os scripts na ordem e chegar exatamente aos mesmos números do artigo. E o orientador deve ter uma recomendação clara sobre adotar ou não o modelo no observatório.

### O que vocês vão fazer

1. **Aluno A:** README, execução do zero, versões.
2. **Aluno B:** script de carga no MySQL e medição de custo.
3. Os dois: a recomendação final e o fechamento do diário.

### Passo a passo

**1. O `README.md` da subpasta (Aluno A).** Precisa conter:

- O que o trabalho faz, em um parágrafo;
- Os dois autores e quem fez o quê;
- As fontes de dados, com endereço e **data de acesso**;
- **Os códigos do SIDRA** usados (tabela, variáveis, produto);
- Como instalar: `pip install -r requirements.txt`;
- **A ordem de execução dos scripts**, numerada, dizendo qual arquivo cada um gera;
- Quanto tempo leva cada etapa;
- A tabela final de métricas;
- Uma nota dizendo que os dados brutos não estão versionados e como regerá-los.

**2. A execução do zero (Aluno A).** Esta é a prova de reprodutibilidade, e é preciso fazer de verdade:

1. Renomeiem `dados/` para `dados_backup/`;
2. Criem a estrutura vazia de novo;
3. Criem um ambiente virtual **novo** e instalem a partir do `requirements.txt`;
4. Rodem os scripts na ordem do README;
5. Comparem os números finais com os do backup.

Se der diferente, achem o motivo — quase sempre é um passo manual que ficou de fora do README (um arquivo baixado à mão, um código digitado direto no script). **Anotem o tempo total.** Esse número vai para o artigo.

**3. Versões das bibliotecas (Aluno A).** `pip freeze > requirements.txt` e anotem também a versão do Python e as características da máquina (processador, RAM, sistema). Em aprendizado de máquina, mudança de versão do `scikit-learn` muda resultado — sem essas informações o método não é reprodutível.

**4. A carga no MySQL (Aluno B).** Agora sim o banco entra. O objetivo é deixar a tabela final disponível para o observatório:

```
pip install sqlalchemy pymysql
```

```python
import pandas as pd
from sqlalchemy import create_engine

USUARIO, SENHA = "...", "..."          # peca ao coordenador; nao comite isso
SERVIDOR, BANCO = "localhost", "agroagreste"

engine = create_engine(f"mysql+pymysql://{USUARIO}:{SENHA}@{SERVIDOR}/{BANCO}")

base = pd.read_csv("dados/final/base_modelagem.csv")
base.to_sql("mandioca_clima_agreste", engine, if_exists="replace", index=False)

previsoes = pd.read_csv("resultados/previsoes_melhor_modelo.csv")
previsoes.to_sql("previsoes_rendimento", engine, if_exists="replace", index=False)

print("Carregado.")
```

Confiram com um `SELECT COUNT(*)` que o número de linhas bate com o CSV.

**Nunca comitem usuário e senha.** Coloquem em um arquivo `config.py` listado no `.gitignore`, e deixem um `config_exemplo.py` com os campos em branco. Isso é higiene básica e vale um comentário na seção de Materiais e Métodos.

Se o acesso ao MySQL não tiver saído a tempo, **deixem o script pronto e testado contra o SQLite** (que vem com o Python, sem instalar nada: basta trocar a linha do `create_engine`) e registrem no artigo que a carga foi implementada e validada, restando executá-la no banco do observatório. Isso é uma entrega honesta e completa.

**5. A medição de custo (Aluno B).** Montem a tabela:

| Etapa | Tempo | Volume |
|---|---|---|
| Coleta IBGE | | |
| Coleta NASA POWER (todos os municípios) | | |
| Montagem da base | | |
| Treino de um modelo | | |
| Validação temporal completa | | |

E a projeção: **quanto custaria atualizar isso uma vez por ano?** A resposta provavelmente é "minutos, em um computador comum" — e essa é uma informação prática relevante para o observatório, que não tem servidor dedicado.

**6. A recomendação final (os dois).** Escrevam em `docs/recomendacao.md`, meia página, respondendo diretamente: **o AgroAgreste deve adotar esse modelo de previsão?**

Há três respostas possíveis, e todas são defensáveis:

- **Sim**, porque o modelo reduziu o erro em X% em relação à linha de base, e a previsão sai com meses de antecedência da colheita;
- **Sim, com ressalva**, porque funciona bem em anos normais mas erra nos extremos — que são os que mais importam. Sirva como indicador de tendência, não como previsão operacional;
- **Ainda não**, porque o modelo não superou a previsão ingênua. Neste caso, a recomendação concreta é: publicar no observatório a **série histórica cruzada de clima e produção** (que é uma contribuição real, e ficou pronta), e listar o que faria falta para melhorar — dados de produção de melhor qualidade, escala sub-municipal, NDVI da lavoura, séries mais longas.

**Nenhuma dessas respostas é fracasso.** A terceira é, inclusive, a mais honesta e a mais útil para o projeto, porque impede que o observatório publique um número em que não se pode confiar.

**7. Fechar o diário (os dois).** Releiam `docs/diario.md` inteiro e escrevam um fechamento de meia página cada um: o que funcionou, o que deu mais trabalho, o que fariam diferente. Isso é a matéria-prima da Conclusão do artigo, e escrever agora, com tudo fresco, poupa um dia na semana da Conclusão.

### Como saber que a Sprint 8 deu certo

- [ ] Uma pessoa de fora consegue rodar tudo pelo README e chegar aos mesmos números.
- [ ] O `requirements.txt` está atualizado e as versões estão registradas.
- [ ] O script de carga em banco roda (no MySQL ou, na falta de acesso, no SQLite) e o número de linhas confere.
- [ ] Nenhuma senha está versionada.
- [ ] A tabela de custo está preenchida.
- [ ] `docs/recomendacao.md` existe e responde à pergunta de forma direta.
- [ ] Todas as figuras do artigo estão salvas em 300 dpi.

### Tarefa extra, se sobrar tempo

- **E1.** XGBoost (`pip install xgboost`), avaliado com o mesmo protocolo. Uma linha a mais na tabela.
- **E2.** Prever a **variação** do rendimento (`rendimento_Y − rendimento_{Y-1}`) em vez do valor absoluto. Muda o problema e às vezes melhora muito, porque tira a inércia da série.
- **E3.** Testar o modelo em **outra cultura** (feijão ou milho), que são de ciclo curto e mais sensíveis à chuva do ano. Se o clima funcionar melhor para elas do que para a mandioca, isso é uma discussão excelente para o artigo — e é um resultado que faz sentido agronômico.
- **E4.** Incluir uma variável de município (o código como categoria) e ver se o modelo melhora. Cuidado: com poucos anos por município, isso pode virar decoreba.

---

## Quadro-resumo das sprints

| Sprint | Período | O que entrega | Quem puxa |
|---|---|---|---|
| 1 | 22/09 a 28/09 | Ambiente, lista de municípios, coordenadas, APIs testadas | Os dois |
| 2 | 29/09 a 05/10 | Série histórica da mandioca, limpa e conferida | Aluno A |
| 3 | 06/10 a 12/10 | Série diária de clima de todos os municípios | Aluno B |
| 4 | 13/10 a 19/10 | **Base de modelagem** (município-ano, alvo + variáveis) | Os dois |
| 5 | 20/10 a 26/10 | **Linha de base e validação temporal** | Os dois |
| 6 | 27/10 a 02/11 | Regressão linear, Random Forest e a tabela comparativa | Os dois |
| 7 | 03/11 a 09/11 | Importância das variáveis, análise de erro, figuras | Os dois |
| 8 | 10/11 a 16/11 | Reprodutibilidade, carga no MySQL, recomendação | Os dois |

---

## Se algo der errado no cronograma

| Problema | O que fazer |
|---|---|
| A rede bloqueia a API do IBGE | Baixem as tabelas em CSV pelo navegador, uma vez, e sigam com arquivos locais. Avisem o orientador **na Sprint 1** |
| A rede bloqueia a NASA POWER | **Risco mais sério do trabalho.** Avisem imediatamente. Plano B: baixar dados do INMET/BDMEP das estações do Agreste e usar a estação mais próxima de cada município — muda a fonte e vira uma limitação declarada, o método continua igual |
| A Sprint 2 ou a 3 atrasou | As duas são independentes: quem terminou ajuda o outro. Só a Sprint 4 depende das duas |
| A base final ficou com poucas linhas | Reduzam o ano inicial (de 2000 para 1995, se a PAM tiver) ou aceitem menos municípios. **Não reduzam o período de teste** |
| Nenhum modelo bate a linha de base | **Não é atraso, é resultado.** Sigam para a Sprint 7 e invistam na análise de por quê. O artigo continua de pé |
| Atraso geral na Sprint 6 | Cortem o *boosting* e o Ridge. Mantenham **linha de base + regressão linear + Random Forest** — é o mínimo que responde à pergunta do artigo |
| Falta de acesso ao MySQL | Usem SQLite (já vem no Python) e registrem no artigo. **Não deixem isso travar a Sprint 8** |

**Se precisarem cortar, cortem modelos, nunca o protocolo de avaliação.** Um modelo bem avaliado vale mais que quatro modelos mal avaliados — e um trabalho com vazamento de dados não vale nada, por mais modelos que tenha.

---

## Relação com o artigo

O desenvolvimento e a escrita andam juntos (ver `01_teofilo_agro_tarefas_escrita.md`):

| Seção do artigo | De onde vem o conteúdo |
|---|---|
| Referencial Teórico | leituras das Sprints 2 a 6 (agricultura familiar, mandioca e clima, aprendizado de máquina aplicado à agricultura, validação temporal) |
| Metodologia | a escolha do alvo e do recorte (Sprints 1 e 2) e o protocolo de validação (Sprint 5) |
| Materiais e Métodos | Sprints 1 a 5 (fontes, códigos do SIDRA, parâmetros da NASA, variáveis criadas, bibliotecas, versões, máquina) |
| Resultados | Sprints 5 a 8 (tabela de métricas, importância, análise de erro, custo) |
| Conclusão | `docs/diario.md` e `docs/recomendacao.md` da Sprint 8 |

**Duas coisas que precisam estar no artigo e que só existem se forem anotadas na hora:** os **códigos do SIDRA** usados e o **tratamento dos valores faltantes** das duas fontes. Anotem na semana em que acontecerem; ninguém lembra disso em novembro.
