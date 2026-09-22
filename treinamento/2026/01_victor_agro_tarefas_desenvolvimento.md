# Plano de tarefas de desenvolvimento – Victor (Tecnologia em Sistemas para Internet)

**Projeto pai:** AgroAgreste – Observatório Territorial da Agricultura Familiar no Agreste do Rio Grande do Norte (ver [projeto.md](../projeto.md)).

**Temática escolhida:** S4 – Monitoramento da vegetação e das áreas agrícolas por imagens de satélite, com o índice NDVI (ver [tematicas.md](../tematicas.md)).

**Perfil do aluno:** 1 aluno do Curso Superior de Tecnologia em Sistemas para Internet, com conhecimentos **básicos** em Python, em treinamento, e **sem conhecimento de banco de dados**. As tarefas são pequenas e muito detalhadas de propósito. Nada aqui exige banco de dados: os resultados são guardados em planilhas CSV, que é o formato certo para o volume deste trabalho.

**Duração:** 8 sprints de 1 semana (22/09/2026 a 16/11/2026).

**Onde o trabalho acontece:** o **repositório de treinamento do projeto já existe** e é compartilhado com os outros alunos. Você **não vai criar repositório nenhum**. Todo o seu trabalho fica dentro de **uma única subpasta sua**:

```
<repositorio-de-treinamento>/
├── ...              ← pastas de outros alunos (não mexa)
└── victor/          ← a sua subpasta: tudo o que você fizer fica aqui dentro
```

Confirme com o orientador o **endereço do repositório** e o **nome exato da sua subpasta** antes de começar. Todos os caminhos deste documento são relativos a ela.

---

## A ideia do trabalho, em uma página

O observatório AgroAgreste quer acompanhar as condições da vegetação e das lavouras no Agreste potiguar. Hoje não existe esse acompanhamento: sabe-se que houve seca ou que choveu bem, mas não há um **número** que descreva, mês a mês, como a vegetação de cada município respondeu.

Satélites fotografam a Terra inteira, de graça, a cada poucos dias. A partir dessas imagens é possível calcular o **NDVI**, um índice que mede o **vigor da vegetação**: quanto mais verde e viçosa a planta, maior o valor. Acompanhar o NDVI ao longo dos meses mostra o ciclo da vegetação; comparar anos mostra o efeito das secas.

A pergunta que este trabalho responde é:

> **É possível construir, com imagens de satélite gratuitas, um indicador mensal de vigor da vegetação para os municípios do Agreste potiguar? E esse indicador se comporta como a literatura prevê, respondendo à chuva?**

### O que você vai construir

Um processo em Python que, para cada município escolhido e cada mês:

1. procura no catálogo de satélites uma imagem com pouca nuvem;
2. baixa **apenas o pedaço da imagem que cobre aquele município** (e não a cena inteira);
3. descarta os pixels cobertos por nuvem;
4. calcula o NDVI de cada pixel restante;
5. guarda **uma linha em uma planilha** com o NDVI médio daquele município naquele mês;
6. joga fora a imagem.

No fim, você tem uma planilha com a série temporal do NDVI. Aí começa a parte de análise: comparar com a chuva, comparar anos secos com anos chuvosos, fazer gráficos e mapas.

### O que vai ser medido (é isso que faz o trabalho ser um artigo, e não um relatório)

| O que | Como |
|---|---|
| **Resposta à chuva** | Correlação entre o NDVI do mês e a chuva daquele mês, do mês anterior e de dois meses antes. A literatura diz que a vegetação responde com atraso — você vai verificar se é verdade no Agreste |
| **Anos secos × anos chuvosos** | Comparação do NDVI médio entre os anos de maior e menor chuva da série |
| **Diferença entre municípios** | O NDVI e o padrão sazonal são iguais em todos os municípios escolhidos? |
| **Custo computacional** | Tempo de processamento e **volume de dados baixados** por município e por ano |

A última linha não é detalhe: se o observatório for adotar esse indicador, alguém vai perguntar quanto custa rodar isso todo mês para o Agreste inteiro. Você vai ter a resposta medida.

### O recorte

**De 3 a 5 municípios do Agreste Potiguar**, escolhidos por contraste — por exemplo, um com mais área agrícola e outro com mais caatinga preservada. **A lista final é definida com o orientador na Sprint 1**, e precisa ser a mesma usada pelos outros TCCs do projeto.

Municípios que costumam aparecer como referência na região: Santa Cruz, Nova Cruz, São Paulo do Potengi, Tangará, Japi. **Confirme a lista oficial com o orientador** — não a invente.

**Período:** de 2021 a 2025, cinco anos completos. Cinco anos é o mínimo para comparar ano seco com ano chuvoso.

### O que este trabalho **não** é

Não é "fazer o mapa do observatório". A plataforma é o **contexto** que justifica a pergunta. O objeto do artigo é o **indicador construído e validado por medição**. Escreva isso na Introdução — é o que separa um artigo de um manual de programa.

---

## Decisões técnicas já fechadas

| Item | Decisão |
|---|---|
| Linguagem | **Python 3** |
| Banco de dados | **Nenhum.** Os resultados cabem em planilhas CSV, e o módulo `csv` (ou o `pandas`) resolve. Escolher a ferramenta do tamanho do problema é uma decisão técnica legítima, e você vai justificá-la no artigo |
| Fonte das imagens | **Microsoft Planetary Computer**, catálogo gratuito e sem cadastro para consulta |
| Satélite | **Sentinel-2**, nível L2A (já corrigido), bandas de 20 m |
| Fonte da chuva | **NASA POWER**, que é uma API gratuita e simples |
| Limites dos municípios | **API de malhas do IBGE** |
| Gráficos | `matplotlib` |
| O que **não** entra | Docker, Django, banco de dados, aprendizado de máquina, Google Earth Engine, QGIS |

**Tudo é instalado com `pip`**, porque as máquinas do laboratório não permitem instalar programas. Nenhuma biblioteca desta lista exige instalação de aplicativo externo.

### Como o trabalho foi dimensionado para a rede do laboratório

Baixar imagens de satélite pode consumir muita banda e muito disco. Duas decisões evitam isso:

1. **Você nunca baixa a cena inteira.** As imagens do Sentinel-2 ficam guardadas em um formato (COG) que permite pedir **só o pedaço que interessa**. Um município do Agreste ocupa uma fração mínima de uma cena de 110 km × 110 km;
2. **Você não guarda as imagens.** O programa baixa o recorte, calcula o número, grava **uma linha** no CSV e descarta a imagem. O disco fica praticamente vazio.

**Na Sprint 2 você vai medir** quanto tempo e quantos MB custa processar uma data. Se o custo for alto demais para a rede do laboratório, existe um **plano B** já definido (ver a seção de riscos, no fim deste documento) — e essa medição, em si, é um dos resultados do artigo.

---

## Combinados gerais

- **Repositório:** já existe e é compartilhado. Trabalhe **somente dentro da sua subpasta**.
- **Commits:** pelo menos 3 por sprint, com mensagem em português dizendo o que foi feito.
- **Reunião semanal:** no começo de cada sprint você mostra ao orientador o que fez, **rodando na máquina**.
- **Travou mais de 40 minutos no mesmo erro? Peça ajuda.** Nesta temática isso é ainda mais importante: erro de projeção de mapa e erro de máscara de nuvem são difíceis de perceber sozinho.
- **Planilha de resultados:** tudo o que o programa calcula vai para `dados/`. **Nunca apague uma linha.**
- **Diário:** `docs/diario.md`, três linhas no fim de cada sprint — o que funcionou, o que deu errado, o que aprendi. Vira a Conclusão do artigo.
- **Prints e mapas:** em `docs/evidencias/`. Vão para o capítulo de Resultados.
- **Olhe as imagens.** Este é um trabalho visual. Não confie só nos números: abra o mapa de NDVI e veja se faz sentido. Mata é verde-escuro, solo exposto é claro, água é escuro. Se estiver invertido, tem erro no código.

### Convivência em repositório compartilhado

1. **Só altere arquivos dentro de `victor/`.** Nunca edite, mova ou apague arquivo de outro aluno.
2. **Comece o dia com `git pull`.**
3. **Comite só o que é seu:** use `git add victor/`, nunca `git add .`. Confira com `git status` antes.
4. **Não comite imagens de satélite** nem a pasta `.venv/`. Comite os CSV de resultado e os gráficos, que são pequenos.
5. **Deu `CONFLICT`? Pare e chame o orientador.**
6. **`git push` no fim de cada dia.**

---

# Sprint 1 — 22/09 a 28/09/2026
## Ambiente e "eu consigo achar uma imagem?"

**Objetivo:** ao final da semana, ter o ambiente funcionando e um script que **encontra** imagens de satélite de um município do Agreste e lista as datas disponíveis. Ainda não vai baixar nada.

Esta sprint é um **teste de viabilidade**. Se o laboratório bloquear o acesso ao catálogo de imagens, é melhor descobrir agora do que na Sprint 4.

### O que você vai fazer

1. Criar a subpasta e preparar o ambiente.
2. Instalar as bibliotecas.
3. Buscar no catálogo as imagens disponíveis para um ponto do Agreste.
4. Definir, com o orientador, a lista final de municípios.

### Passo a passo

**1. Clonar o repositório e criar a subpasta.**

```
git clone <endereço-do-repositório-de-treinamento>
cd <pasta-do-repositório>
mkdir victor
cd victor
```

Estrutura a criar:

```
victor/
├── scripts/             ← os programas Python, numerados na ordem
├── dados/               ← as planilhas de resultado (CSV)
├── graficos/
├── temp/                ← recortes de imagem temporários (não vão para o Git)
├── docs/
│   ├── diario.md
│   ├── ambiente.md
│   └── evidencias/
├── .gitignore
├── requirements.txt
└── README.md
```

**2. Ambiente virtual e bibliotecas.**

```
python -m venv .venv
.venv\Scripts\activate
pip install pystac-client planetary-computer rioxarray shapely requests pandas matplotlib
pip freeze > requirements.txt
```

Para que serve cada uma:

| Biblioteca | Para quê |
|---|---|
| `pystac-client` | Procurar imagens no catálogo de satélites |
| `planetary-computer` | Liberar o acesso aos arquivos de imagem encontrados |
| `rioxarray` | Abrir e recortar imagens de satélite (traz junto o `rasterio` e o `xarray`) |
| `shapely` | Trabalhar com o contorno do município |
| `requests` | Conversar com as APIs do IBGE e da NASA |
| `pandas` | Organizar as planilhas |
| `matplotlib` | Fazer os gráficos e os mapas |

A instalação do `rioxarray` baixa bastante coisa e pode demorar alguns minutos. É normal.

**3. O `.gitignore` da sua subpasta:**

```
.venv/
__pycache__/
*.pyc
temp/
*.tif
```

**4. Testar se o catálogo responde.** Crie `scripts/01_testar_catalogo.py`:

```python
import pystac_client
import planetary_computer

# ponto aproximado no Agreste potiguar (confirme depois com o orientador)
LONGITUDE = -35.88
LATITUDE = -6.23

catalogo = pystac_client.Client.open(
    "https://planetarycomputer.microsoft.com/api/stac/v1",
    modifier=planetary_computer.sign_inplace,
)

busca = catalogo.search(
    collections=["sentinel-2-l2a"],
    intersects={"type": "Point", "coordinates": [LONGITUDE, LATITUDE]},
    datetime="2024-01-01/2024-03-31",
    query={"eo:cloud_cover": {"lt": 30}},
)

itens = list(busca.items())
print(f"Imagens encontradas: {len(itens)}")

for item in itens[:5]:
    print(item.datetime.date(), "- nuvem:", item.properties["eo:cloud_cover"], "%")
```

Rode. Se aparecer uma lista de datas, **o acesso funciona** e a maior incerteza do trabalho está resolvida. Tire print e comemore.

**Se der erro de conexão**, pode ser bloqueio de rede ou *proxy* do laboratório. **Avise o orientador nesta semana**, não na próxima.

**5. Entender o que você acabou de fazer.** Três conceitos novos, explicados de forma simples:

- **catálogo STAC**: um catálogo padronizado de imagens de satélite. Você diz "quero imagens deste lugar, nesta data, com pouca nuvem" e ele devolve a lista;
- **`eo:cloud_cover`**: a porcentagem de nuvem da cena inteira. Filtrar por menos de 30% já elimina a maioria das imagens inúteis, antes mesmo de baixar qualquer coisa;
- **Sentinel-2 L2A**: L2A significa que a imagem já vem corrigida dos efeitos da atmosfera. É a versão que se deve usar para calcular índices de vegetação. Existe a L1C, sem essa correção — **não use**, e explique no artigo por quê.

**6. Fechar a lista de municípios com o orientador.** De 3 a 5 municípios do Agreste Potiguar, escolhidos por contraste. Para cada um, você precisa do **código IBGE de 7 dígitos**. Consulte assim:

```python
import requests

resposta = requests.get(
    "https://servicodados.ibge.gov.br/api/v1/localidades/estados/RN/municipios"
)
for municipio in resposta.json():
    print(municipio["id"], municipio["nome"])
```

Salve a lista em `dados/municipios.csv`:

```
codigo_ibge,nome,justificativa_da_escolha
2411205,Santa Cruz,...
```

A coluna de justificativa vai direto para o capítulo de Metodologia do artigo.

**7. Comece o `docs/ambiente.md`** anotando: versão do Python, versões das bibliotecas, processador, memória RAM, tipo de disco, sistema operacional e a velocidade da internet do laboratório. Os tempos que você vai medir não significam nada sem isso.

### Como saber que deu certo

- [ ] Subpasta criada, com a estrutura de pastas.
- [ ] Bibliotecas instaladas, `requirements.txt` comitado.
- [ ] `python scripts/01_testar_catalogo.py` lista datas de imagens.
- [ ] `dados/municipios.csv` com a lista definida com o orientador.
- [ ] `docs/ambiente.md` iniciado.

### Erros comuns

- **`ConnectionError` ou tempo esgotado:** bloqueio de rede. Avise o orientador.
- **`pip install rioxarray` falha:** copie a mensagem de erro inteira e leve ao orientador. Pode ser versão do Python incompatível.
- **Nenhuma imagem encontrada:** confira as coordenadas. Longitude no Brasil é **negativa** e vem **primeiro** no formato do STAC (`[longitude, latitude]`). Trocar a ordem é o erro mais comum aqui.

---

# Sprint 2 — 29/09 a 05/10/2026
## Baixar o recorte de um município e ver o primeiro mapa de NDVI

**Objetivo:** calcular o NDVI de **uma data**, de **um município**, e ver o mapa na tela. E medir quanto isso custou em tempo e em MB.

### O que você vai fazer

1. Pegar o contorno do município na API do IBGE.
2. Baixar apenas o recorte das duas bandas necessárias.
3. Calcular o NDVI.
4. Salvar o mapa como imagem.
5. **Medir o tempo e o volume baixado.**

### Passo a passo

**1. O contorno do município.** O IBGE tem uma API que devolve o desenho do limite de qualquer município:

```python
import requests
from shapely.geometry import shape

CODIGO = 2411205      # troque pelo codigo do seu municipio

url = (f"https://servicodados.ibge.gov.br/api/v3/malhas/municipios/{CODIGO}"
       "?formato=application/vnd.geo+json")

geojson = requests.get(url).json()
geometria = shape(geojson["features"][0]["geometry"])

print("Area aproximada (graus quadrados):", geometria.area)
print("Retangulo que contem o municipio:", geometria.bounds)
```

O `bounds` devolve `(oeste, sul, leste, norte)` — o retângulo que envolve o município. É ele que você usa para procurar imagens e para recortar.

**Salve o contorno em um arquivo**, para não ficar pedindo ao IBGE toda hora:

```python
import json
with open(f"dados/limite_{CODIGO}.geojson", "w", encoding="utf-8") as arquivo:
    json.dump(geojson, arquivo)
```

**2. Entender o NDVI antes de programar.** O NDVI usa duas faixas de luz que o satélite enxerga:

- **vermelho (banda B04)**: a planta saudável **absorve** essa luz para fazer fotossíntese, então reflete pouco;
- **infravermelho próximo (banda B8A)**: a planta **reflete muito** essa luz, que o olho humano não vê.

A fórmula combina as duas:

```
NDVI = (infravermelho − vermelho) / (infravermelho + vermelho)
```

O resultado vai de −1 a +1:

| Faixa | O que costuma ser |
|---|---|
| abaixo de 0 | água, nuvem |
| 0 a 0,2 | solo exposto, rocha, área construída |
| 0,2 a 0,4 | vegetação rala ou seca |
| 0,4 a 0,7 | vegetação em bom vigor |
| acima de 0,7 | vegetação densa e muito viçosa |

Na caatinga, o NDVI varia **muito** entre a seca e a chuva, porque a vegetação perde as folhas no período seco. Essa variação forte é exatamente o que torna a região interessante para este estudo — e é um bom parágrafo para o artigo.

**3. Escolher uma imagem.** Use a busca da Sprint 1, agora com o retângulo do município e ordenando pela menos nublada:

```python
busca = catalogo.search(
    collections=["sentinel-2-l2a"],
    bbox=geometria.bounds,
    datetime="2024-08-01/2024-08-31",
    query={"eo:cloud_cover": {"lt": 30}},
)
itens = sorted(busca.items(), key=lambda i: i.properties["eo:cloud_cover"])
item = itens[0]      # a menos nublada do mes
print("Escolhida:", item.datetime.date(), item.properties["eo:cloud_cover"], "%")
```

**4. Baixar só o recorte.** Esta é a parte mais importante da sprint:

```python
import rioxarray

def abrir_recorte(item, nome_banda, geometria):
    url = item.assets[nome_banda].href
    imagem = rioxarray.open_rasterio(url, masked=True)
    recorte = imagem.rio.clip([geometria], crs="EPSG:4326", from_disk=True)
    return recorte.squeeze()

vermelho = abrir_recorte(item, "B04", geometria)
infravermelho = abrir_recorte(item, "B8A", geometria)
```

**O que está acontecendo aqui:** o `open_rasterio` **não** baixa a imagem inteira. As imagens do Sentinel-2 ficam guardadas em um formato que permite ler pedaços. O `clip` pede só os pixels dentro do município, e só esses trafegam pela rede. É por isso que este trabalho cabe na rede do laboratório.

> **Sobre as bandas:** o `B04` (vermelho) existe em 10 m e o `B8A` (infravermelho próximo) em 20 m. **Use as duas em 20 m**, para que tenham o mesmo tamanho e o cálculo case pixel a pixel. Nas coleções do Planetary Computer, os nomes dos arquivos incluem a resolução — confira na primeira execução e **anote qual você usou**, porque isso vai para o capítulo de Materiais e Métodos. Se as duas imagens saírem com números de linhas e colunas diferentes, o problema é esse.

**5. Calcular e desenhar o NDVI:**

```python
import matplotlib.pyplot as plt

ndvi = (infravermelho - vermelho) / (infravermelho + vermelho)

ndvi.plot(cmap="RdYlGn", vmin=-0.2, vmax=0.9)
plt.title("")                        # o titulo vai na legenda ABNT, fora da imagem
plt.savefig("docs/evidencias/ndvi_exemplo.png", dpi=150, bbox_inches="tight")
```

O mapa de cores `RdYlGn` vai do vermelho (pouco vigor) ao verde (muito vigor), que é a leitura intuitiva.

**6. Olhe o mapa.** Sério: abra a imagem. Os açudes têm que aparecer em vermelho-escuro (água tem NDVI negativo), a área urbana em tons claros, e a vegetação em verde. **Se estiver tudo invertido, você trocou as bandas na fórmula.** É o erro mais comum, e ele não gera mensagem de erro nenhuma — só um resultado errado.

**7. Medir o custo.** Esta medição é um dos resultados do artigo:

```python
import time
inicio = time.perf_counter()
# ... todo o processo de uma data ...
print(f"Tempo: {time.perf_counter() - inicio:.1f} segundos")
```

Para o volume de dados, o jeito mais simples é salvar o recorte em disco e olhar o tamanho:

```python
vermelho.rio.to_raster("temp/b04.tif")
infravermelho.rio.to_raster("temp/b8a.tif")
```

e somar o tamanho dos dois arquivos com `os.path.getsize`. É uma boa aproximação do que trafegou.

**Anote em `docs/diario.md`: quantos segundos e quantos MB por data.** Multiplique mentalmente: 12 meses × 5 anos × 4 municípios = 240 datas. Se cada uma custar 30 segundos e 5 MB, o total é 2 horas e 1,2 GB — viável, distribuído ao longo das sprints. Se custar 5 minutos e 50 MB, é inviável, e aí entra o plano B da seção de riscos. **Leve esse número ao orientador na reunião.**

### Como saber que deu certo

- [ ] Contorno do município salvo em `dados/`.
- [ ] Mapa de NDVI gerado e salvo em `docs/evidencias/`.
- [ ] O mapa faz sentido visualmente (água escura, vegetação verde).
- [ ] Tempo e MB por data anotados no diário e levados ao orientador.

### Erros comuns

- **As duas bandas têm tamanhos diferentes:** você pegou uma em 10 m e outra em 20 m. Use as duas em 20 m.
- **Tudo com NDVI negativo:** bandas trocadas na fórmula.
- **`clip` devolve vazio:** a geometria e a imagem estão em sistemas de coordenadas diferentes. O parâmetro `crs="EPSG:4326"` no `clip` é o que resolve — ele avisa ao rioxarray em que sistema está o contorno do município.
- **Muito lento:** confira se você não está esquecendo o `clip` e baixando a cena inteira.

---

# Sprint 3 — 06/10 a 12/10/2026
## Tirar as nuvens e calcular o NDVI médio de uma data

**Objetivo:** transformar um mapa de NDVI em **um número só** — o NDVI médio do município naquela data — descartando os pixels que estão debaixo de nuvem.

> **Atenção:** 12/10 é feriado e cai no último dia desta sprint.

### Por que isso importa

Nuvem é branca e reflete tanto no vermelho quanto no infravermelho. O NDVI de uma nuvem dá um valor baixo, parecido com solo exposto. Se você calcular a média sem tirar as nuvens, um mês nublado vai parecer um mês de vegetação seca — e a sua série temporal inteira fica errada.

**Esta é a parte do trabalho que mais influencia a qualidade do resultado.** Vale escrever bastante sobre ela no artigo.

### O que você vai fazer

1. Baixar a camada de classificação de cena (SCL).
2. Montar a máscara de nuvem.
3. Calcular o NDVI médio dos pixels válidos e a porcentagem de pixels válidos.
4. Definir a regra de aceitação de uma data.

### Passo a passo

**1. O que é o SCL.** O Sentinel-2 L2A vem com uma banda extra chamada **SCL** (*Scene Classification Layer*), em 20 m, em que cada pixel já vem classificado por um número:

| Valor | Significado |
|---|---|
| 3 | Sombra de nuvem |
| 4 | Vegetação |
| 5 | Solo descoberto |
| 6 | Água |
| 8 | Nuvem, probabilidade média |
| 9 | Nuvem, probabilidade alta |
| 10 | Cirros (nuvem fina e alta) |

Os valores 0, 1, 2, 7 e 11 são outras situações (sem dado, saturado, sombra escura, neve). **Confirme a tabela completa na documentação oficial do Sentinel-2** e cite essa fonte no artigo.

**2. Montar a máscara:**

```python
scl = abrir_recorte(item, "SCL", geometria)

# valores que NAO servem: sombra de nuvem, nuvens e cirros
RUINS = [3, 8, 9, 10]

valido = ~scl.isin(RUINS)
ndvi_limpo = ndvi.where(valido)
```

O `where` mantém os pixels bons e transforma os ruins em "sem valor". Eles somem da média automaticamente.

**3. Calcular os dois números que interessam:**

```python
import numpy as np

total_pixels = int(valido.size)
pixels_validos = int(valido.sum())
percentual_valido = 100 * pixels_validos / total_pixels

ndvi_medio = float(ndvi_limpo.mean())

print(f"NDVI medio: {ndvi_medio:.3f}")
print(f"Pixels validos: {percentual_valido:.1f}%")
```

**4. A regra de aceitação — e esta é uma decisão sua, que precisa ser justificada no artigo.** Se 90% do município estava debaixo de nuvem, a média dos 10% restantes não representa o município. Defina um mínimo.

**Sugestão: aceitar a data apenas se pelo menos 60% dos pixels forem válidos.** Se nenhuma imagem do mês atingir isso, aquele mês fica **sem dado** — e isso é honesto. Meses sem dado, principalmente na estação chuvosa, são um resultado do trabalho, não uma falha: eles mostram uma limitação real do uso de satélite óptico em região com nuvem.

**Teste dois ou três limiares** (por exemplo, 40%, 60% e 80%) e veja quantos meses cada um descarta. Escolha um, registre a escolha e mostre a comparação no artigo. Isso se chama análise de sensibilidade e eleva bastante o nível do trabalho.

**5. Compare visualmente.** Gere dois mapas lado a lado da mesma data nublada: o NDVI sem máscara e o NDVI com máscara. É uma das melhores figuras que o seu artigo pode ter, porque mostra o problema e a solução na mesma imagem.

**6. Organize o código em uma função.** Ao final desta sprint, você deve ter uma função que faz tudo de uma data:

```python
def processar_data(item, geometria):
    """Devolve um dicionario com o resultado de uma data, ou None se a data
    for descartada por excesso de nuvem."""
    ...
    return {
        "data_imagem": item.datetime.date().isoformat(),
        "nuvem_cena": item.properties["eo:cloud_cover"],
        "ndvi_medio": ndvi_medio,
        "ndvi_mediana": ndvi_mediana,
        "percentual_valido": percentual_valido,
        "pixels_validos": pixels_validos,
        "segundos": duracao,
        "mb_baixados": mb,
    }
```

**Guarde também a mediana do NDVI, além da média.** Elas quase sempre são parecidas; quando forem muito diferentes, é sinal de que sobrou alguma coisa estranha na imagem, e você quer saber disso.

### Como saber que deu certo

- [ ] A máscara de nuvem funciona e o percentual de pixels válidos é calculado.
- [ ] Figura comparando NDVI com e sem máscara, na mesma data nublada.
- [ ] Limiar de aceitação escolhido e **justificado por escrito**, com a comparação entre limiares.
- [ ] Função `processar_data` pronta e testada em pelo menos 5 datas diferentes.

### Erros comuns

- **O SCL tem tamanho diferente das outras bandas:** ele é de 20 m, então case com as bandas de 20 m.
- **NDVI médio dá `nan`:** todos os pixels foram mascarados. Trate esse caso na função, devolvendo `None` em vez de quebrar.
- **Percentual de válidos sempre 100%:** a máscara não está sendo aplicada. Confira se a lista `RUINS` está certa e se o `~` (que inverte a condição) está lá.

---

# Sprint 4 — 13/10 a 19/10/2026
## A série temporal de um município

**Objetivo:** rodar o processo para **todos os meses de 2021 a 2025** em **um município**, e ver o gráfico da série temporal.

### O que você vai fazer

1. Escrever o laço que percorre os meses.
2. Fazer o programa continuar de onde parou, se for interrompido.
3. Rodar a série completa de um município.
4. Fazer o primeiro gráfico da série temporal.

### Passo a passo

**1. A lógica do laço.** Para cada mês de cada ano: buscar as imagens, escolher a menos nublada, processar e gravar a linha. Se nenhuma imagem do mês passar no critério, grave uma linha marcando o mês como sem dado.

```python
ANOS = range(2021, 2026)     # 2021 a 2025
MESES = range(1, 13)

for ano in ANOS:
    for mes in MESES:
        # monta o intervalo de datas do mes
        # busca as imagens
        # tenta a menos nublada; se reprovar no criterio, tenta a proxima
        # grava a linha no CSV
```

**Detalhe que vale a pena:** se a imagem menos nublada da cena for reprovada pelo critério de pixels válidos, **tente a segunda menos nublada**, e assim por diante, até três tentativas. A nuvem pode estar longe do município — a porcentagem da cena inteira não diz o que está acontecendo exatamente sobre a sua área.

**2. Fazer o programa continuar de onde parou.** Isso é essencial com rede de laboratório: se a conexão cair na metade, você não pode perder tudo e recomeçar.

A solução é simples: antes de processar um mês, verifique se ele já está no CSV. Se estiver, pule.

```python
import os
import pandas as pd

def ja_processado(caminho_csv, codigo, ano, mes):
    if not os.path.exists(caminho_csv):
        return False
    tabela = pd.read_csv(caminho_csv)
    filtro = ((tabela["codigo_ibge"] == codigo) &
              (tabela["ano"] == ano) &
              (tabela["mes"] == mes))
    return filtro.any()
```

E grave o CSV **a cada mês processado**, não só no final:

```python
linha = pd.DataFrame([resultado])
linha.to_csv(caminho_csv, mode="a", header=not os.path.exists(caminho_csv), index=False)
```

O `mode="a"` acrescenta ao arquivo em vez de sobrescrever. Assim, se o programa cair, tudo o que já foi feito está salvo.

**3. O formato do arquivo `dados/ndvi_mensal.csv`:**

```
codigo_ibge,municipio,ano,mes,data_imagem,nuvem_cena,percentual_valido,ndvi_medio,ndvi_mediana,pixels_validos,segundos,mb_baixados,situacao
```

A coluna `situacao` recebe `ok` ou `sem_dado`, com o motivo. Meses sem dado precisam aparecer na planilha, e não simplesmente faltar.

**4. Mostre o progresso na tela.** Um laço que roda por uma hora em silêncio parece travado:

```python
print(f"[{ano}-{mes:02d}] {municipio}: NDVI={ndvi_medio:.3f} "
      f"({percentual_valido:.0f}% valido, {mb:.1f} MB, {segundos:.0f}s)")
```

**5. Rode a série completa de um município.** São 60 meses. Reserve tempo: pode levar de meia hora a algumas horas, dependendo da rede. Deixe rodando e vá fazer outra coisa.

**6. O primeiro gráfico.** Uma linha com o NDVI ao longo do tempo:

```python
import pandas as pd
import matplotlib.pyplot as plt

tabela = pd.read_csv("dados/ndvi_mensal.csv")
tabela["data"] = pd.to_datetime(dict(year=tabela.ano, month=tabela.mes, day=1))

plt.figure(figsize=(12, 4))
plt.plot(tabela["data"], tabela["ndvi_medio"], marker="o")
plt.ylabel("NDVI medio")
plt.xlabel("Mes")
plt.grid(alpha=0.3)
plt.savefig("graficos/serie_temporal.png", dpi=150, bbox_inches="tight")
```

**7. Olhe o gráfico e converse com ele.** Você deve ver um padrão que sobe e desce todo ano: o NDVI cresce alguns meses depois do começo das chuvas e cai na estiagem. **Se você vê esse padrão, o seu indicador está funcionando** — e esse é o primeiro resultado de verdade do trabalho. Anote no diário o que você observou; esse parágrafo vai para os Resultados.

Se o gráfico estiver todo serrilhado, sem padrão nenhum, provavelmente sobrou nuvem. Volte ao limiar da Sprint 3.

### Como saber que deu certo

- [ ] `dados/ndvi_mensal.csv` com 60 linhas de um município (contando os meses sem dado).
- [ ] O programa continua de onde parou quando é interrompido e executado de novo.
- [ ] Gráfico da série temporal gerado.
- [ ] Dá para ver o ciclo anual da vegetação no gráfico.
- [ ] Quantos meses ficaram sem dado, e em que época do ano eles se concentram.

### Erros comuns

- **O programa refaz tudo do zero:** a verificação de "já processado" não está funcionando. Teste-a isoladamente.
- **Muitos meses sem dado:** normal na estação chuvosa. Conte quantos e em que meses — é resultado, não erro.
- **Memória estourando:** você está guardando todas as imagens em uma lista. Processe e descarte uma de cada vez.

---

# Sprint 5 — 20/10 a 26/10/2026
## Os outros municípios e os dados de chuva

**Objetivo:** ter a série de NDVI de todos os municípios e a série de chuva para comparar.

### O que você vai fazer

1. Rodar a série para os municípios restantes.
2. Baixar os dados de chuva da NASA POWER.
3. Montar a tabela que junta NDVI e chuva.

### Passo a passo

**1. Rodar os demais municípios.** Se o seu programa da Sprint 4 já lê a lista de `dados/municipios.csv`, é só rodar. Deixe processando ao longo da semana. **Rode um município por vez** e confira o resultado antes de passar ao próximo.

**2. A chuva pela NASA POWER.** É uma API gratuita, sem cadastro, que devolve dados climáticos para qualquer coordenada do planeta. Use o **centro do município** como ponto de consulta.

```python
import requests

def baixar_chuva(longitude, latitude, ano_inicio, ano_fim):
    url = "https://power.larc.nasa.gov/api/temporal/monthly/point"
    parametros = {
        "parameters": "PRECTOTCORR",     # precipitacao corrigida
        "community": "AG",               # comunidade agricultura
        "longitude": longitude,
        "latitude": latitude,
        "start": ano_inicio,
        "end": ano_fim,
        "format": "JSON",
    }
    resposta = requests.get(url, params=parametros, timeout=60)
    resposta.raise_for_status()
    return resposta.json()
```

O `PRECTOTCORR` é a precipitação em milímetros por dia, na média do mês. **Confira na documentação da NASA POWER qual é exatamente a unidade** do parâmetro mensal antes de usar, e registre isso no artigo — errar a unidade é o tipo de detalhe que invalida uma correlação.

O centro do município você já tem:

```python
centro = geometria.centroid
print(centro.x, centro.y)     # longitude, latitude
```

**3. Salve em `dados/chuva_mensal.csv`:**

```
codigo_ibge,municipio,ano,mes,chuva_mm
```

**4. Confira se os dados fazem sentido.** O Agreste potiguar tem estação chuvosa concentrada entre fevereiro e julho, aproximadamente, e uma estiagem marcada no segundo semestre. Faça um gráfico de barras da chuva mensal e veja se o padrão aparece. Se a chuva estiver distribuída igualmente pelo ano, tem algo errado — provavelmente unidade ou coordenada trocada.

**Este é o momento de confirmar o padrão com a literatura**, e não com a sua intuição. Pesquise sobre o regime de chuvas do Agreste potiguar e cite a fonte no artigo.

**5. Juntar as duas tabelas:**

```python
ndvi = pd.read_csv("dados/ndvi_mensal.csv")
chuva = pd.read_csv("dados/chuva_mensal.csv")

junto = ndvi.merge(chuva, on=["codigo_ibge", "ano", "mes"], how="left")
junto.to_csv("dados/ndvi_chuva.csv", index=False)
```

**Confira quantas linhas sobraram.** Se o `merge` reduziu ou multiplicou o número de linhas, há algo desalinhado entre as duas tabelas — quase sempre uma diferença de tipo (o código IBGE lido como texto em uma tabela e como número na outra).

**6. Um gráfico com as duas séries juntas.** NDVI em linha e chuva em barras, no mesmo eixo de tempo, com dois eixos verticais. Pesquise por `twinx` no matplotlib. **Este vai ser provavelmente o gráfico principal do seu artigo** — é nele que se vê, a olho nu, a vegetação respondendo à chuva com alguns meses de atraso.

### Como saber que deu certo

- [ ] Série de NDVI completa para todos os municípios.
- [ ] `dados/chuva_mensal.csv` preenchido.
- [ ] O padrão sazonal de chuva do Agreste aparece no gráfico.
- [ ] `dados/ndvi_chuva.csv` com as duas séries juntas, sem perder linhas.
- [ ] Gráfico combinado NDVI + chuva gerado.

### Erros comuns

- **NASA POWER devolve erro:** confira o formato das datas (a API mensal usa só o ano) e o nome do parâmetro.
- **O `merge` perdeu linhas:** tipos diferentes na coluna de junção. Force com `astype(int)` nas duas.
- **A chuva não tem sazonalidade:** coordenada trocada (longitude e latitude invertidas) ou unidade errada.

---

# Sprint 6 — 27/10 a 02/11/2026
## A pergunta central: o NDVI responde à chuva?

**Objetivo:** medir a relação entre o NDVI e a chuva, e descobrir com quantos meses de atraso a vegetação responde.

> **Atenção:** 02/11 é feriado e cai no último dia desta sprint.

### A ideia, explicada

Quando chove, a vegetação não fica verde no mesmo dia. Ela leva algumas semanas para responder. Então o NDVI de maio provavelmente tem mais a ver com a chuva de **abril** ou de **março** do que com a de maio.

Esse atraso se chama **defasagem** (*lag*). Descobrir qual é a defasagem do Agreste potiguar é o resultado mais interessante do seu trabalho, e é uma informação que o observatório pode usar de verdade.

### O que você vai fazer

1. Criar as colunas de chuva defasada.
2. Calcular a correlação para cada defasagem.
3. Descobrir qual defasagem dá a maior correlação.
4. Comparar entre os municípios.

### Passo a passo

**1. Criar as colunas de chuva com atraso.** O `pandas` faz isso com uma função só, mas **cuidado**: a tabela precisa estar ordenada por município e por data, e a defasagem tem de ser feita **dentro de cada município**, separadamente. Senão, a chuva de dezembro de um município vai virar a "chuva do mês anterior" de janeiro de outro.

```python
tabela = tabela.sort_values(["codigo_ibge", "ano", "mes"])

for atraso in [1, 2, 3]:
    tabela[f"chuva_lag{atraso}"] = (
        tabela.groupby("codigo_ibge")["chuva_mm"].shift(atraso)
    )
```

O `groupby` antes do `shift` é o que garante isso. **Confira o resultado olhando algumas linhas** antes de seguir.

**2. Calcular a correlação.** A correlação é um número entre −1 e +1 que diz o quanto duas coisas variam juntas:

| Valor | Leitura |
|---|---|
| próximo de +1 | quando uma sobe, a outra sobe |
| próximo de 0 | não têm relação |
| próximo de −1 | quando uma sobe, a outra desce |

```python
for atraso in [0, 1, 2, 3]:
    coluna = "chuva_mm" if atraso == 0 else f"chuva_lag{atraso}"
    correlacao = tabela["ndvi_medio"].corr(tabela[coluna])
    print(f"Defasagem de {atraso} mes(es): correlacao = {correlacao:.3f}")
```

**3. Faça isso por município e no conjunto todo.** Monte a tabela:

| Município | Sem defasagem | 1 mês | 2 meses | 3 meses |
|---|---|---|---|---|

**4. A pergunta a responder:** em qual defasagem a correlação é mais alta? Se for em 1 ou 2 meses, você confirmou o comportamento que a literatura descreve, medindo no seu território. **Escreva isso com destaque nos Resultados.**

**5. Um gráfico de dispersão.** Ponha a chuva defasada no eixo horizontal e o NDVI no vertical, um ponto por mês. Se houver relação, os pontos formam uma nuvem inclinada. Faça um gráfico para a defasagem que deu a maior correlação.

**6. Dois cuidados honestos, que precisam estar no artigo:**

- **correlação não é causa.** Você mostrou que as duas coisas variam juntas, o que é coerente com o que se sabe sobre a vegetação do semiárido. Não escreva que "provou" que a chuva causa o aumento do NDVI;
- **as duas séries têm sazonalidade**, e isso infla a correlação. Ambas sobem e descem todo ano, então parte da correlação vem só do fato de as duas seguirem o calendário. Mencione essa limitação. Se quiser ir além (opcional), calcule a correlação **dentro de cada mês** ao longo dos anos — por exemplo, só os cinco meses de maio da série — o que remove o efeito do calendário.

**7. Se quiser um número a mais (opcional):** o `pandas` também calcula a correlação de **Spearman**, com `.corr(method="spearman")`. Ela mede se as duas variam juntas mesmo que a relação não seja em linha reta. Apresentar as duas é fácil e dá robustez ao resultado.

### Como saber que deu certo

- [ ] Colunas de chuva defasada criadas corretamente, por município.
- [ ] Tabela de correlações por município e por defasagem.
- [ ] A defasagem de maior correlação identificada.
- [ ] Gráfico de dispersão da melhor defasagem.
- [ ] As duas ressalvas (causalidade e sazonalidade) anotadas para o artigo.

### Erros comuns

- **Correlação estranhamente baixa:** confira se a defasagem foi feita dentro de cada município e se a tabela estava ordenada.
- **Correlação exatamente 1 ou muito próxima:** provavelmente você correlacionou a coluna com ela mesma.
- **`nan` no resultado:** há meses sem dado. Use `.dropna()` antes de correlacionar, e **informe quantas linhas foram descartadas**.

---

# Sprint 7 — 03/11 a 09/11/2026
## Anos secos contra anos chuvosos, e os mapas

**Objetivo:** mostrar o efeito das secas no NDVI e produzir as figuras finais do artigo.

### O que você vai fazer

1. Classificar os anos por total de chuva.
2. Comparar o NDVI entre o ano mais seco e o mais chuvoso.
3. Gerar os mapas de NDVI para comparação visual.
4. Comparar os municípios entre si.

### Passo a passo

**1. Classificar os anos.** Some a chuva de cada ano, por município, e ordene:

```python
por_ano = tabela.groupby(["codigo_ibge", "ano"]).agg(
    chuva_total=("chuva_mm", "sum"),
    ndvi_medio_ano=("ndvi_medio", "mean"),
).reset_index()
```

Identifique o **ano mais seco** e o **ano mais chuvoso** da série, por município.

**2. Confira com a realidade.** Isto é importante e é fácil de esquecer: pesquise se os anos que apareceram como secos na sua análise foram, de fato, anos de seca reconhecida no Rio Grande do Norte. O **Monitor de Secas**, da ANA, publica mapas mensais de severidade da seca e é a fonte natural para essa conferência. Notícias e boletins da EMPARN também servem.

**Se bater, você tem uma validação externa do seu indicador** — ou seja, a sua medição concorda com uma fonte independente. Isso é um argumento forte no artigo. Se não bater, investigue e relate: também é resultado.

**3. Comparar o NDVI entre os anos extremos.** Monte a tabela:

| Município | Ano mais seco | Chuva (mm) | NDVI médio | Ano mais chuvoso | Chuva (mm) | NDVI médio | Diferença |
|---|---|---|---|---|---|---|---|

E um gráfico com as duas curvas mensais sobrepostas: o ano seco e o ano chuvoso, mês a mês. Dá para ver a diferença de amplitude e, às vezes, de duração do período verde.

**4. Os mapas.** Gere o mapa de NDVI do **mesmo mês** em um ano seco e em um ano chuvoso, lado a lado, **com a mesma escala de cores** (use os mesmos `vmin` e `vmax` nos dois).

> **Usar a mesma escala nos dois mapas é obrigatório.** Se cada mapa usar a sua própria escala, os dois vão parecer iguais, e a comparação vira ilusão de ótica. Esse é um erro comum e sério em trabalhos com mapas.

Esses dois mapas lado a lado são, provavelmente, **a figura mais forte do seu artigo**: qualquer pessoa entende o resultado em dois segundos.

**5. Comparar os municípios.** O ciclo anual é igual em todos? Algum mantém o NDVI mais alto na seca (o que pode indicar mais vegetação perene ou irrigação)? Algum varia muito mais?

Monte um gráfico com as séries dos municípios sobrepostas, e uma tabela com NDVI médio, mínimo, máximo e amplitude por município. **Relacione as diferenças com o que você sabe do território** — e aqui vale conversar com o orientador, que conhece a região.

**6. Revise todas as figuras.** Para cada gráfico e mapa: eixos com nome e unidade, legenda, sem título dentro da imagem (na ABNT o título vai acima da figura), e salvos com `dpi=150` ou mais.

### Como saber que deu certo

- [ ] Anos classificados por chuva, por município.
- [ ] Conferência com o Monitor de Secas feita e anotada.
- [ ] Tabela e gráfico comparando ano seco e ano chuvoso.
- [ ] Mapas lado a lado, com a mesma escala de cores.
- [ ] Comparação entre municípios feita.
- [ ] Todas as figuras revisadas.

---

# Sprint 8 — 10/11 a 16/11/2026
## Fechamento: custo, documentação e recomendação

**Objetivo:** responder "quanto custa rodar isso?", deixar tudo reproduzível e escrever a recomendação para o observatório.

> **Atenção:** 15/11 é feriado e cai nesta sprint.

### O que você vai fazer

1. Consolidar as medições de custo computacional.
2. Escrever o `README.md`.
3. Escrever a recomendação para o AgroAgreste.
4. Montar a apresentação.
5. **Tarefa extra, só se tudo o resto estiver pronto:** o MapBiomas.

### Passo a passo

**1. O custo computacional.** Você vem gravando `segundos` e `mb_baixados` em cada linha do CSV desde a Sprint 4. Agora consolide:

| Município | Meses processados | Meses sem dado | Tempo total (min) | Dados baixados (MB) | Tempo médio por mês (s) | MB por mês |
|---|---|---|---|---|---|---|

E responda à pergunta prática: **quanto custaria rodar isso para todos os municípios do Agreste, uma vez por mês?** É uma regra de três a partir dos seus números, e é exatamente o que a equipe do observatório precisa saber. Diga também quanto espaço em disco seria necessário (praticamente nenhum, porque as imagens são descartadas — e esse é um ponto de projeto que vale destacar).

**2. O `README.md` da subpasta**, que precisa permitir que outra pessoa repita tudo:

- o que é o trabalho e a que projeto pertence;
- o que instalar (`pip install -r requirements.txt`);
- a lista de municípios e o período analisado;
- **a ordem dos scripts**, numerada, com uma linha explicando o que cada um faz e quanto tempo demora;
- quanto de rede e de disco é preciso;
- as fontes de dados usadas, com endereço e data de acesso;
- a configuração da máquina onde as medições foram feitas.

**3. A recomendação para o AgroAgreste** (`docs/recomendacao.md`), em uma página, escrita para a equipe do projeto:

- o indicador funciona? Ele responde à chuva como esperado?
- com que frequência ele poderia ser atualizado no observatório?
- quanto custa, em tempo e em rede?
- quais são as limitações que a equipe precisa conhecer (meses sem dado por nuvem, resolução, o fato de a média do município misturar tipos de uso da terra diferentes);
- o que seria preciso para levar isso ao observatório de verdade.

**4. Revise o código.** Scripts numerados na ordem de execução, cada um com um comentário no topo dizendo o que faz, sem código morto e sem caminho fixo da sua máquina (`C:\Users\...`) dentro do código.

**5. A apresentação** (8 a 10 slides): o problema, como o NDVI funciona, como você coletou, o gráfico NDVI + chuva, a tabela de correlações, os dois mapas lado a lado, o custo, a recomendação.

---

### Tarefa extra: separar as áreas agrícolas com o MapBiomas

**Faça isto apenas se tudo acima estiver pronto e conferido.** É a parte mais pesada da temática, e foi deixada como opcional justamente por isso.

**A ideia:** até agora, o NDVI médio do município mistura tudo — lavoura, pastagem, caatinga, cidade, açude. O MapBiomas publica mapas anuais que dizem, para cada pedaço do território, qual é o uso da terra. Com ele, dá para calcular o NDVI **separado por classe** e responder: a agricultura responde à chuva de forma diferente da caatinga?

**Se for fazer:**

1. baixe o mapa de uso da terra do MapBiomas para o Rio Grande do Norte, do ano que você quiser analisar. Confira a licença de uso e **registre a fonte e a coleção** (o MapBiomas numera suas versões, e a versão usada precisa estar no artigo);
2. recorte-o para o município, igual ao que você já faz com as imagens;
3. **cuidado com a resolução:** o MapBiomas é de 30 m e o seu NDVI é de 20 m. Os dois precisam ser colocados na mesma grade antes de comparar. O `rioxarray` tem `reproject_match` para isso;
4. agrupe os pixels por classe e calcule o NDVI médio de cada uma.

**Se não der tempo, escreva no artigo** que a separação por uso da terra foi identificada como o próximo passo natural e fica como trabalho futuro. Limitação declarada não tira valor do trabalho.

### Como saber que a Sprint 8 deu certo

- [ ] Tabela de custo computacional consolidada, com a projeção para o Agreste inteiro.
- [ ] `README.md` permite que outra pessoa repita o trabalho.
- [ ] `docs/recomendacao.md` escrito.
- [ ] Subpasta limpa, sem imagens nem `.venv` comitados.
- [ ] `git log --stat` não mostra nenhum arquivo fora da sua subpasta.
- [ ] Apresentação montada.

---

## Quadro-resumo das sprints

| Sprint | Período | O que entrega | O que aprende |
|---|---|---|---|
| 1 | 22/09 a 28/09 | Ambiente e busca no catálogo de satélites | STAC, Sentinel-2, API do IBGE |
| 2 | 29/09 a 05/10 | Primeiro mapa de NDVI de um município | bandas, recorte, fórmula do NDVI |
| 3 | 06/10 a 12/10 | Máscara de nuvem e NDVI médio de uma data | SCL, máscara, critério de aceitação |
| 4 | 13/10 a 19/10 | Série temporal de 5 anos de um município | laços, gravação incremental, retomada |
| 5 | 20/10 a 26/10 | Demais municípios e dados de chuva | NASA POWER, junção de tabelas |
| 6 | 27/10 a 02/11 | Correlação NDVI × chuva com defasagem | defasagem, correlação, cuidados |
| 7 | 03/11 a 09/11 | Anos secos × chuvosos e mapas | validação externa, comparação visual |
| 8 | 10/11 a 16/11 | Custo, documentação e recomendação | reprodutibilidade, síntese |

---

## Se algo der errado no cronograma

| Problema | O que fazer |
|---|---|
| A rede bloqueia o catálogo de imagens | Avise o orientador **na Sprint 1**. É o risco mais sério deste trabalho |
| Cada data custa tempo ou MB demais | **Plano B:** trocar o Sentinel-2 pelo produto de NDVI do **MODIS**, que já vem com o NDVI calculado, em 250 m de resolução e arquivos muito menores. O método do artigo continua exatamente o mesmo — muda só a fonte e a resolução, o que vira uma limitação declarada. Decida isso com o orientador logo após a medição da Sprint 2 |
| Muitos meses sem imagem boa | Baixe o limiar de pixels válidos (de 60% para 40%) e **relate a mudança**. Ou apresente a série em intervalos de dois meses |
| A série de um município demora horas | Deixe rodando à noite ou em outro horário. A retomada automática da Sprint 4 garante que nada se perde |
| Atraso geral | Reduza de 5 para 3 municípios, ou de 5 para 3 anos. **Não reduza** a máscara de nuvem nem a medição de custo |

**Se precisar cortar, corte quantidade, não qualidade.** Três municípios bem processados valem mais que cinco processados de qualquer jeito.

---

## Se sobrar tempo (opcional)

- **E1.** Calcular também o **SAVI**, um índice parecido com o NDVI mas criado para regiões de vegetação rala, onde o solo aparece entre as plantas — exatamente o caso da caatinga. Comparar os dois seria um ótimo acréscimo.
- **E2.** Comparar a chuva da NASA POWER com a de uma estação do INMET próxima, para verificar se a fonte usada é confiável na região.
- **E3.** Gerar um mapa animado (um quadro por mês) mostrando o verde chegando e indo embora ao longo do ano.
- **E4.** Testar se o resultado muda ao usar a mediana em vez da média do NDVI do município.

---

## Relação com o artigo

O desenvolvimento e a escrita andam juntos (ver `01_victor_agro_tarefas_escrita.md`):

| Seção do artigo | De onde vem o conteúdo |
|---|---|
| Referencial Teórico | leituras das Sprints 2 a 6 (sensoriamento remoto, NDVI, caatinga, chuva) |
| Metodologia | escolha dos municípios (Sprint 1) e o critério de nuvem (Sprint 3) |
| Materiais e Métodos | Sprints 1 a 5 (bibliotecas, versões, fontes de dados, máquina) |
| Resultados | Sprints 4 a 8 (séries, correlações, mapas, custo) |
| Conclusão | `docs/diario.md` e a recomendação da Sprint 8 |

**Nunca apague uma linha das planilhas.** Mês sem dado vira observação no artigo, não lixo — é ele que mostra a limitação real do satélite óptico em região com nuvem.
