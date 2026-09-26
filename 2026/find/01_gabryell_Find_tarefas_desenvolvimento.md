# Plano de desenvolvimento do TCC - Gabryell (Projeto FIND)

**Projeto pai:** FIND - Plataforma e Aplicativo Móvel para Gestão de Objetos Perdidos e Encontrados (ver [projeto.md](../projeto.md)).

**Temática:** avaliação de técnicas para a **correspondência automática entre itens perdidos e encontrados** - um mecanismo que, a partir de um objeto cadastrado como **perdido**, sugere os objetos cadastrados como **encontrados** com maior chance de serem o mesmo objeto.

**Onde o trabalho é feito:** no próprio repositório do FIND (https://github.com/gabryellgs/projeto-find), em uma ***branch* própria** (`tcc-correspondencia`) e dentro de uma **app Django nova**, chamada `correspondencia`. O aplicativo móvel (https://github.com/gabryellgs/find-app) não entra neste trabalho.

**Plano de escrita:** [01_gabryell_Find_tarefas_escrita.md](01_gabryell_Find_tarefas_escrita.md). Os dois documentos andam juntos: cada semana de desenvolvimento alimenta uma seção do texto.

> **Como usar este documento.** Leia as seções 1 a 8 inteiras antes de começar; elas explicam o trabalho. Depois, siga **uma semana por vez**. Cada tarefa diz *o que fazer*, *como fazer* e *quando está pronta*. Boa parte do código já está escrita aqui: a sua parte é **entender cada linha**, adaptar o que for preciso ao FIND, rodar e conferir. Quando uma instrução não estiver clara, pergunte antes de inventar uma solução.

---

## Sumário

- [1. O trabalho em 5 minutos](#1-o-trabalho-em-5-minutos)
- [2. Regras do trabalho](#2-regras-do-trabalho)
- [3. Glossário](#3-glossário)
- [4. O que o FIND já tem](#4-o-que-o-find-já-tem)
- [5. As estratégias comparadas](#5-as-estratégias-comparadas)
- [6. Os dados do experimento](#6-os-dados-do-experimento)
- [7. Como fica o repositório](#7-como-fica-o-repositório)
- [8. Cronograma](#8-cronograma)
- [Semana 1: FIND rodando e linha de base](#semana-1-find-rodando-e-linha-de-base)
- [Semana 2: fotos e dados](#semana-2-fotos-e-dados)
- [Semana 3: texto, métricas e primeira avaliação](#semana-3-texto-métricas-e-primeira-avaliação)
- [Semana 4: imagem e combinação](#semana-4-imagem-e-combinação)
- [Semana 5: tempo, sugestões, testes e README](#semana-5-tempo-sugestões-testes-e-readme)
- [Semanas 6 e 7: folga, análise de erros e extras](#semanas-6-e-7-folga-análise-de-erros-e-extras)
- [Se algo der errado](#se-algo-der-errado)
- [Checklist final](#checklist-final)

---

## 1. O trabalho em 5 minutos

Pense em uma **busca do Google**:

- a **consulta** é um item **perdido** ("procuro squeeze azul");
- os **documentos** são os itens **achados** cadastrados no FIND;
- a **estratégia** dá uma **pontuação** para cada achado e os ordena, do mais parecido para o menos parecido;
- como você mesmo monta os dados, você sabe **qual achado é o correto** para cada perdido (o **gabarito**);
- então dá para ver **em que posição** o achado correto ficou. Se ficou em 1º, ótimo. Se ficou em 15º, o dono nunca vai vê-lo, porque o FIND mostra só **6** sugestões.

O trabalho inteiro é isso: montar um conjunto de itens com gabarito, rodar algumas estratégias e comparar **as posições em que cada uma coloca o item correto**.

Exemplo com três itens perdidos:

| Perdido | Posição do correto na estratégia X | Posição do correto na estratégia Y |
|---|---|---|
| "squeeze azul" | 1º | 3º |
| "garafa verde" | 2º | 12º |
| "oculos preto" | 1º | 1º |

A estratégia X colocou o correto entre os 6 primeiros nos 3 casos. A Y, em 2 de 3. É esse tipo de comparação que vai para o TCC, usando as métricas da Tarefa 3.2.

---

## 2. Regras do trabalho

- **O FIND não pode quebrar.** Todo o seu código fica na app nova `correspondencia/`, na *branch* `tcc-correspondencia`. Você **não altera** as apps que já existem (`items`, `mainpage` etc.). Fora da sua app, as únicas mudanças são: **uma linha** no `INSTALLED_APPS`, **uma linha** no `.gitignore` e o arquivo `pytest.ini`.
- **Sem inteligência artificial.** Nada de *embeddings*, redes neurais, CLIP, Gemini, ChatGPT ou qualquer API de IA. O trabalho avalia **técnicas clássicas**, leves e explicáveis. Isso não é uma limitação: é o **recorte** do trabalho, e ele será defendido no texto (custo zero, sem GPU, sem enviar fotos a terceiros e com uma pontuação que dá para explicar ao usuário).
- **Somente ferramentas gratuitas, instaladas com `pip`.** Os computadores do laboratório não permitem instalar programas. Já estão instalados: Python 3.12, Git, VS Code e DB Browser for SQLite. Não usamos Docker.
- **Banco de dados: SQLite**, que o FIND já usa em desenvolvimento local.
- **Sem participantes humanos.** Os textos dos itens são gerados por *script*, e as fotos são tiradas **por você**, de objetos seus ou do laboratório. Isso dispensa questionários, voluntários e Comitê de Ética.
- **Nenhum ajuste depois de ver os resultados.** As configurações de cada estratégia e os pesos da combinação já estão definidos neste documento. Você **não** muda nada porque o resultado ficou ruim. Um resultado ruim também é um resultado.
- **Tudo reproduzível.** Toda tabela e todo gráfico do TCC saem de um comando. A semente aleatória é sempre `42`.

**Como organizar cada semana:**

1. **Segunda-feira:** leia a semana inteira neste documento e anote as dúvidas.
2. **Até quarta-feira:** mande as dúvidas ao orientador. Não espere a sexta para dizer que travou.
3. **Todo dia em que programar:** termine com um *commit* do que ficou pronto.
4. **Sexta-feira:** mostre ao orientador o que ficou pronto (código rodando, tabela ou gráfico) e confira o "Pronto quando" de cada tarefa.

---

## 3. Glossário

| Palavra | O que significa neste trabalho |
|---|---|
| **Perdido** | Item cadastrado com status `perdido`. É a **consulta**. |
| **Achado** | Item cadastrado com status `achado`. É o que a estratégia ordena. |
| **Candidatos** | Todos os achados que entram na comparação. |
| **Gabarito** | A ligação "este perdido corresponde a este achado". Como você cria os dois, você sabe a resposta certa. |
| **Distrator** | Achado que **não** é par de ninguém. Serve para dificultar o teste. |
| **Estratégia** | Uma forma de pontuar os candidatos (B0, T1, V ou F). |
| **Posição** | Lugar em que o achado correto ficou na lista ordenada (1 = primeiro). |
| **Linha de base** (*baseline*) | A estratégia de referência: o que o FIND já faz hoje. As outras são comparadas com ela. |
| **Variação** | Mudança proposital no texto do perdido (sinônimo, erro de digitação ou falta de acento), para imitar o modo como as pessoas escrevem. |
| **Semente** | Número que faz o sorteio do Python dar sempre o mesmo resultado. Aqui é sempre `42`. |

---

## 4. O que o FIND já tem

Na primeira semana, leia estes trechos do `projeto-find`. Eles são a **linha de base** do trabalho.

| O que existe | Onde está | Como funciona |
|---|---|---|
| Modelos `Categoria` e `Item` | `items/models.py` | `titulo` (45 caracteres), `descricao` (200), `status` (`perdido`, `achado`, `pendente_confirmacao`, `confirmado`, `devolvido`), `local` (45), `data`, `categoria`, `imagem`, `image_hash` e o usuário que cadastrou |
| Categorias padrão | comando `criar_categorias` | Cria as 6 categorias usadas no sistema |
| Imagens | `find/storage.py` | As fotos são gravadas **dentro do banco**, e o `image_hash` (pHash) é calculado quando o item é salvo (`Item._gerar_image_hash`) |
| "Smart Match" | função `_calcular_match_score`, em `mainpage/views.py` | Para cada perdido, pontua os achados: **categoria igual (35 pontos) + proporção de palavras do título em comum (até 40) + proporção de palavras da descrição em comum (até 25)**. Mostra até **6** sugestões com pontuação **≥ 30** |
| Busca por imagem | método `buscar_por_imagem`, em `items/models.py` | **pHash 16×16** comparado pela distância de Hamming (50%) + **interseção de histogramas de cor HSV** (50%) |

**Onde estão as limitações:** a comparação por palavras em comum não trata acentos, erros de digitação nem sinônimos. "garrafa" não combina com "squeeze", e "oculos" não combina com "óculos". O pHash foi feito para achar a **mesma foto** redimensionada, e não o **mesmo objeto** fotografado em outro lugar. O seu trabalho vai **medir** essas limitações e testar alternativas.

Como o experimento fica dentro do FIND, a linha de base **não precisa ser copiada**: você chama a função real do FIND.

---

## 5. As estratégias comparadas

São **quatro** estratégias. Todas recebem um item perdido e devolvem uma pontuação **de 0 a 1** para cada candidato.

| Código | Estratégia | O que compara | Onde está pronta |
|---|---|---|---|
| **B0** | Heurística atual do FIND (linha de base) | Categoria + palavras em comum | a própria função do FIND |
| **T1** | TF-IDF com similaridade do cosseno, sobre trechos de 3 a 5 letras | Texto do perdido × texto do achado | `scikit-learn` |
| **V** | pHash + histograma de cor (50/50), como no FIND | Foto do perdido × foto do achado | `ImageHash`, `Pillow`, `numpy` |
| **F** | Combinação: 0,6 × T1 + 0,3 × V + 0,1 × categoria | Tudo junto | - |

A **F** roda de dois jeitos: **com foto** e **sem foto** (como se o dono não tivesse foto do objeto). Assim, com os mesmos perdidos, você mede quanto a foto ajuda.

"Texto do item" é sempre `titulo + " " + descricao`.

**Por que a T1 resolve parte do problema:** ela compara pedaços de palavras ("gar", "arr", "rra"...). Se uma letra estiver errada, a maioria dos pedaços continua igual, e a pontuação cai pouco. Ela também dá mais peso aos pedaços raros ("Stanley") do que aos comuns. **O que ela não resolve:** ela não sabe que "squeeze" e "garrafa" são a mesma coisa. Isso é esperado e vai aparecer nos resultados.

---

## 6. Os dados do experimento

Você vai fotografar **40 objetos reais**. Cada objeto vira **três itens** no FIND:

| Item | Status | Foto | Texto | Exemplo |
|---|---|---|---|---|
| **Achado verdadeiro** | `achado` | foto A (de quem achou) | descrição padrão | "Garrafa azul. Marca: Stanley. Adesivo do IFRN na lateral." |
| **Perdido** | `perdido` | foto B (do dono) | descrição do dono, **com uma variação** | "Procuro squeeze azul. É da marca Stanley. Detalhe: adesivo do IFRN na lateral." |
| **Distrator "quase igual"** | `achado` | sem foto | descrição padrão com **outra cor** | "Garrafa verde. Marca: Stanley. Adesivo do IFRN na lateral." |

No final, o banco terá **40 perdidos**, **80 achados** (40 verdadeiros + 40 distratores) e **40 pares** no gabarito.

Os 40 perdidos são divididos em **4 grupos de 10**, por sorteio (o grupo `sem_acento` é sorteado só entre os objetos que têm acento no texto). Cada grupo recebe **um único tipo** de variação:

| Grupo | O que acontece com o texto do perdido | Exemplo |
|---|---|---|
| `nenhuma` | nada: só o jeito de escrever é diferente do achado | "Procuro garrafa azul." |
| `sinonimo` | o nome do objeto é trocado por um sinônimo | "Procuro squeeze azul." |
| `erro_digitacao` | o nome do objeto é escrito com uma letra trocada, faltando ou sobrando | "Procuro garafa azul." |
| `sem_acento` | todos os acentos são retirados | "Procuro oculos preto." |

O grupo `nenhuma` é a **referência**: mostra como cada estratégia se sai quando a pessoa escreve bem. Os outros mostram **quanto cada problema atrapalha**.

---

## 7. Como fica o repositório

```
projeto-find/
├── find/settings.py              # + "correspondencia" no INSTALLED_APPS (1 linha)
├── .gitignore                    # + correspondencia/dados/fotos_originais/ (1 linha)
├── pytest.ini                    # novo (Tarefa 1.3)
├── items/, mainpage/, ...        # apps do FIND - NÃO ALTERAR
└── correspondencia/              # a sua app
    ├── models.py                 # ParGabarito
    ├── admin.py
    ├── texto.py                  # normalizar() e texto_do_item()
    ├── estrategias.py            # B0, T1, V e F
    ├── metricas.py               # Recall@k e MRR
    ├── management/commands/
    │   ├── preparar_fotos.py
    │   ├── gerar_dados.py
    │   ├── avaliar.py
    │   └── sugerir.py
    ├── tests/
    ├── dados/
    │   ├── catalogo.csv          # os 40 objetos (escrito por você)
    │   ├── sinonimos.json
    │   ├── locais.txt
    │   ├── fotos_originais/      # NÃO vai para o Git
    │   └── fotos/                # fotos tratadas (vão para o Git)
    ├── resultados/               # CSVs e gráficos gerados pelo avaliar
    ├── requirements-tcc.txt
    └── README.md
```

**Quatro comandos** fazem todo o experimento:

| Comando | O que faz |
|---|---|
| `python manage.py preparar_fotos` | Trata as fotos do celular (gira, reduz e apaga os metadados) |
| `python manage.py gerar_dados --semente 42` | Cria os perdidos, os achados e o gabarito no banco |
| `python manage.py avaliar` | Roda as estratégias e gera todas as tabelas e gráficos em `resultados/` |
| `python manage.py sugerir <id>` | Mostra as 6 sugestões da F para um perdido, com as partes da pontuação |

> Todos os comandos são rodados na raiz do `projeto-find`, com o ambiente virtual ativado (`venv\Scripts\activate`).

---

## 8. Cronograma

Os experimentos ficam **fechados em 30/10/2026**, duas semanas antes da entrega dos Resultados (13/11/2026). As semanas 6 e 7 são **folga** para atrasos e para escrever.

| Semana | Período | Entrega de desenvolvimento | Entrega de escrita no mesmo período |
|---|---|---|---|
| 1 | 25/09 a 02/10 | FIND rodando, *branch*, app criada e B0 | Introdução e Objetivo Geral (02/10) |
| 2 | 05/10 a 09/10 | Fotos, catálogo, `preparar_fotos` e `gerar_dados` | Referencial Teórico (em andamento) |
| 3 | 12/10 a 16/10 | `normalizar`, métricas, T1 e `avaliar` com B0 e T1 | Referencial Teórico (16/10) |
| 4 | 19/10 a 23/10 | V, F, robustez, gráficos e tabela principal | Metodologia (23/10) |
| 5 | 26/10 a 30/10 | Tempo, `sugerir`, testes, README e *tag* | Materiais e Métodos (30/10) |
| 6 e 7 | 02/11 a 13/11 | Folga, análise de erros e extras opcionais | Resultados (13/11) |

Da semana 8 em diante não há desenvolvimento novo: só correções pedidas na revisão do texto.

---

## Semana 1: FIND rodando e linha de base

**Período:** 25/09 a 02/10. **Objetivo:** ter o FIND funcionando no laboratório e entender como ele pontua hoje.

### Tarefa 1.1 - Rodar o FIND no laboratório

No PowerShell, na sua pasta de trabalho:

```powershell
git clone https://github.com/gabryellgs/projeto-find.git
cd projeto-find
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
pip install python-magic-bin
```

> Se o PowerShell bloquear o `activate`, rode antes: `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`.

Crie o arquivo `.env` na raiz do projeto:

```
SECRET_KEY=chave-local-qualquer
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
```

```powershell
python manage.py migrate
python manage.py criar_categorias
python manage.py createsuperuser
python manage.py runserver
```

**Pronto quando:** o FIND abre em `http://127.0.0.1:8000` e você consegue cadastrar um item pelo `/admin/`. **Se não conseguir até terça-feira, avise o orientador.**

### Tarefa 1.2 - Criar a *branch* e a app

```powershell
git checkout -b tcc-correspondencia
python manage.py startapp correspondencia
```

1. Em `find/settings.py`, acrescente `"correspondencia"` ao final do `INSTALLED_APPS`.
2. No `.gitignore`, acrescente a linha `correspondencia/dados/fotos_originais/`. Confira se `db.sqlite3` e `.env` já estão lá.
3. Crie `correspondencia/requirements-tcc.txt`. Essas bibliotecas ficam **separadas** do `requirements.txt` do FIND para não irem para o servidor de produção (`Pillow`, `ImageHash` e `numpy` já vêm com o FIND):

```
scikit-learn
nltk
pandas
matplotlib
pytest
pytest-django
```

4. Instale e guarde as versões:

```powershell
pip install -r correspondencia/requirements-tcc.txt
pip freeze > correspondencia/requirements-tcc-versoes.txt
python -c "import nltk; nltk.download('stopwords')"
```

O `requirements-tcc-versoes.txt` guarda as **versões exatas** usadas no experimento. Elas vão para o quadro de Materiais do TCC.

5. Faça o primeiro *commit* e envie a *branch*:

```powershell
git add .
git status
git commit -m "feat(correspondencia): cria a app do experimento"
git push -u origin tcc-correspondencia
```

**Regras de Git para todo o trabalho:**

- antes de cada *commit*, rode `git branch` e confira se está na `tcc-correspondencia`;
- rode `git status` e leia a lista. Se aparecer arquivo alterado **fora** de `correspondencia/` (além de `settings.py`, `.gitignore` e `pytest.ini`), **não faça *commit*** dele: desfaça com `git checkout -- <arquivo>`;
- **não** traga as mudanças da `main` para a sua *branch* durante o trabalho. Se for preciso, faça isso junto com o orientador;
- mensagens no padrão *Conventional Commits*: `feat(correspondencia): ...` (código novo), `test(correspondencia): ...` (testes), `docs(correspondencia): ...` (README);
- nunca use `git push --force`.

**Pronto quando:** a *branch* `tcc-correspondencia` aparece no GitHub com a app vazia, e o FIND continua abrindo normalmente.

### Tarefa 1.3 - Entender e chamar a linha de base (B0)

**Passo 1 - Ler.** Abra `mainpage/views.py` e leia a função `_calcular_match_score` com calma. Responda no seu caderno:

1. Quais parâmetros ela recebe?
2. Como ela separa as palavras do título e da descrição? Ela tira acentos? Deixa tudo em minúsculas?
3. Como calcula cada parte (35 + 40 + 25)? A "proporção de palavras em comum" é dividida por quê?
4. Na *view* que chama essa função: quais status os candidatos podem ter? Os itens do próprio usuário são excluídos?

Essas respostas vão para a Metodologia do TCC. Leve-as para a conversa de sexta-feira.

**Passo 2 - Criar a base das estratégias.** Em `correspondencia/estrategias.py`:

```python
from mainpage.views import _calcular_match_score

# Os mesmos status que o FIND usa para buscar candidatos (confira na view que você leu).
STATUS_CANDIDATOS = ["achado", "pendente_confirmacao", "confirmado"]


class Estrategia:
    """Forma comum de todas as estratégias."""

    nome = ""

    def preparar(self, candidatos):
        """Recebe todos os candidatos uma única vez (ex.: montar a matriz do TF-IDF)."""
        self.candidatos = list(candidatos)

    def pontuar(self, perdido):
        """Devolve {id_do_candidato: pontuação de 0 a 1}."""
        raise NotImplementedError


class B0(Estrategia):
    nome = "B0"

    def pontuar(self, perdido):
        # A pontuação do FIND vai de 0 a 100; aqui ela é dividida por 100.
        return {c.id: _calcular_match_score(perdido, c) / 100 for c in self.candidatos}
```

Toda estratégia segue essa forma: **`preparar` uma vez** com os candidatos e **`pontuar` uma vez para cada perdido**. É isso que permite comparar todas do mesmo jeito.

> Se a função do FIND receber outros parâmetros, ajuste a chamada. Se ela depender do `request` ou fizer outra coisa além de calcular a pontuação, **não altere o FIND**: copie a função para `estrategias.py` **sem mudar nada**, anote no topo de qual *commit* ela foi copiada e avise o orientador.

**Passo 3 - Testar.** Crie `pytest.ini` na raiz do projeto (se o FIND ainda não tiver um):

```ini
[pytest]
DJANGO_SETTINGS_MODULE = find.settings
```

Crie a pasta `correspondencia/tests/`, com um arquivo vazio `__init__.py` e o arquivo `test_b0.py`. Antes de rodar, **calcule à mão** a pontuação esperada. Exemplo: mesma categoria, títulos iguais ("Garrafa azul" e "Garrafa azul") e descrições sem nenhuma palavra em comum → 35 + 40 + 0 = 75 → a B0 devolve `0.75`.

```python
import pytest

from correspondencia.estrategias import B0
from items.models import Categoria, Item


@pytest.mark.django_db
def test_mesma_categoria_mesmo_titulo_descricoes_diferentes():
    categoria = Categoria.objects.create(nome="Acessórios")  # confira o nome do campo em items/models.py
    perdido = Item(titulo="Garrafa azul", descricao="perdi ontem", categoria=categoria, status="perdido")
    achado = Item(id=1, titulo="Garrafa azul", descricao="encontrada na cantina", categoria=categoria, status="achado")

    b0 = B0()
    b0.preparar([achado])

    assert b0.pontuar(perdido)[1] == pytest.approx(0.75)
```

Escreva mais **2 testes** do mesmo jeito, com casos que você inventar (por exemplo: categorias diferentes e metade das palavras do título em comum). Sempre calcule o resultado esperado **antes** de rodar.

```powershell
pytest correspondencia
```

Se um teste falhar, **não mude o número esperado para o teste passar**: descubra se o erro está no seu cálculo à mão ou no seu entendimento da função. Esse é o objetivo do teste.

**Pronto quando:** os 3 testes passam e você consegue explicar ao orientador, com um exemplo no papel, como o FIND pontua um par.

---

## Semana 2: fotos e dados

**Período:** 05/10 a 09/10. **Objetivo:** ter no banco os 40 perdidos, os 80 achados e o gabarito.

Esta é a semana mais importante: **todos os resultados dependem dos dados**. Tire as fotos **na segunda e na terça-feira**.

### Tarefa 2.1 - Escolher e catalogar os objetos

1. Separe **40 objetos** comuns em um campus, espalhados pelas 6 categorias do FIND.
2. Inclua de propósito **grupos de objetos parecidos**: por exemplo, 5 garrafas, 5 mochilas ou estojos, 4 carregadores, 4 chaveiros e 4 fones de ouvido. São eles que tornam o teste difícil e honesto.
3. **Não use** documentos, cartões, crachás ou qualquer objeto com nome, foto ou número de outra pessoa.
4. Preencha `correspondencia/dados/catalogo.csv` no VS Code, uma linha por objeto:

```csv
id,categoria,tipo,cor,marca,detalhe
1,Eletrônicos,carregador,branco,Samsung,cabo USB-C com fita isolante
2,Acessórios,garrafa,azul,,adesivo do IFRN na lateral
3,Acessórios,garrafa,azul,Stanley,sem tampa
4,Acessórios,mochila,preta,Nike,
...
40,...
```

Regras de preenchimento:

- `id` de 1 a 40, sem pular número;
- `categoria` escrita **exatamente** como no FIND (confira no `/admin/`);
- `tipo` em minúsculas, no singular, com **pelo menos 4 letras** ("garrafa", "fone de ouvido");
- `cor` **sempre preenchida**, combinando com o tipo ("mochila preta", "carregador branco");
- `marca` e `detalhe` podem ficar em branco. O `detalhe` é o que ajuda o dono a reconhecer o objeto (um adesivo, um arranhão, um chaveiro pendurado);
- **pelo menos 15 objetos** precisam ter acento no `tipo`, na `cor` ou no `detalhe` ("óculos", "relógio", "boné", "estojo com zíper", "garrafa térmica", "adesivo da música"). Sem acento no texto, a variação `sem_acento` não teria o que mudar.

### Tarefa 2.2 - Fotografar

Cada objeto recebe **duas fotos**, tiradas com o celular:

| Foto | Quem "tirou" | Onde e como | Nome do arquivo |
|---|---|---|---|
| **A** | quem achou | no lugar onde o objeto "foi achado" (bancada, chão do corredor, mesa da biblioteca), com a luz do local, de frente | `001_A.jpg` |
| **B** | o dono | em **outro** lugar (em casa, outra mesa, outro fundo), com **outro ângulo** e outra luz, como a foto que o dono teria no próprio celular | `001_B.jpg` |

São **80 fotos**. Use o `id` do catálogo com três dígitos (`001`, `002`, ..., `040`) e extensão `.jpg` em minúsculas. Guarde tudo em `correspondencia/dados/fotos_originais/`.

Cuidados:

- nenhuma pessoa, rosto, tela com dados pessoais ou placa de carro na imagem;
- o objeto tem de aparecer inteiro e ocupar boa parte da foto;
- se o celular for iPhone, configure a câmera para salvar em JPG (**Ajustes → Câmera → Formatos → Mais Compatível**); fotos `.heic` não funcionam.

### Tarefa 2.3 - Tratar as fotos (`preparar_fotos`)

As fotos do celular são grandes e guardam, nos metadados (EXIF), **a localização GPS** de onde foram tiradas. Por isso elas nunca vão para o Git como saíram do celular.

Crie as pastas `correspondencia/management/` e `correspondencia/management/commands/`, **cada uma com um arquivo vazio `__init__.py`** (sem ele, o Django não encontra os comandos). Depois crie `correspondencia/management/commands/preparar_fotos.py`:

```python
from pathlib import Path

from django.core.management.base import BaseCommand
from PIL import Image, ImageOps

DADOS = Path(__file__).resolve().parents[2] / "dados"


class Command(BaseCommand):
    help = "Gira, reduz para 800 px e remove os metadados das fotos."

    def handle(self, *args, **opcoes):
        destino = DADOS / "fotos"
        destino.mkdir(exist_ok=True)
        for origem in sorted((DADOS / "fotos_originais").glob("*.jpg")):
            imagem = ImageOps.exif_transpose(Image.open(origem)).convert("RGB")  # 1. corrige a rotação
            imagem.thumbnail((800, 800))                                          # 2. lado maior com 800 px
            imagem.save(destino / origem.name, "JPEG", quality=85)                # 3. salva sem o EXIF
            self.stdout.write(f"ok {origem.name}")
```

Rode `python manage.py preparar_fotos` e abra algumas fotos de `fotos/` para conferir se estão na posição certa.

**Pronto quando:** as 80 fotos tratadas estão em `correspondencia/dados/fotos/` e no GitHub.

### Tarefa 2.4 - Escrever os dicionários

`correspondencia/dados/sinonimos.json`: para **cada `tipo` do catálogo**, pelo menos 2 outras formas de chamá-lo. Pense em como um colega chamaria o objeto:

```json
{
  "garrafa": ["garrafinha", "squeeze", "garrafa térmica"],
  "mochila": ["bolsa", "mochila de costas"],
  "fone de ouvido": ["fone", "headphone"],
  "carregador": ["fonte", "cabo de carregar"]
}
```

`correspondencia/dados/locais.txt`: 20 a 30 locais do campus, um por linha, com até 45 caracteres: `Bloco A - sala 3`, `Biblioteca`, `Cantina`, `Quadra`, `Laboratório de Informática 2`...

### Tarefa 2.5 - Modelo do gabarito

Em `correspondencia/models.py`:

```python
from django.db import models


class ParGabarito(models.Model):
    """Liga cada item perdido ao item achado correto."""

    perdido = models.OneToOneField("items.Item", on_delete=models.CASCADE, related_name="gabarito")
    achado = models.ForeignKey("items.Item", on_delete=models.CASCADE, related_name="+")
    variacao = models.CharField(max_length=20)       # nenhuma, sinonimo, erro_digitacao ou sem_acento
    objeto_parecido = models.BooleanField()          # há outro objeto do mesmo tipo no catálogo?
```

Em `correspondencia/admin.py`:

```python
from django.contrib import admin

from .models import ParGabarito

admin.site.register(ParGabarito)
```

```powershell
python manage.py makemigrations correspondencia
python manage.py migrate
```

> Use sempre `makemigrations correspondencia`, com o nome da app. Se aparecer migração de **outra** app, não faça *commit* dela e avise o orientador.

### Tarefa 2.6 - Gerador de dados (`gerar_dados`)

O código abaixo está quase completo. Antes de rodar, abra `items/models.py` e confira **três nomes** marcados com `# CONFIRA`: o campo do nome da categoria, o campo do usuário que cadastrou o item e o campo da data.

Leia o código com calma e acompanhe pelos comentários numerados. Crie `correspondencia/management/commands/gerar_dados.py`:

```python
import csv
import json
import random
import unicodedata
from collections import Counter
from datetime import date
from pathlib import Path

from django.conf import settings
from django.contrib.auth import get_user_model
from django.core.files.base import ContentFile
from django.core.management.base import BaseCommand, CommandError

from correspondencia.models import ParGabarito
from items.models import Categoria, Item

DADOS = Path(__file__).resolve().parents[2] / "dados"
# Cores dos distratores: palavras que não mudam com o gênero ("mochila verde", "carregador verde").
CORES_TROCA = ["azul", "verde", "cinza", "rosa", "marrom", "bege", "laranja", "vinho"]


def tirar_acentos(texto):
    return "".join(c for c in unicodedata.normalize("NFKD", texto) if not unicodedata.combining(c))


def tem_acento(obj):
    texto = f"{obj['tipo']} {obj['cor']} {obj['detalhe']}"
    return tirar_acentos(texto) != texto


def errar_digitacao(texto, rng):
    """Troca, apaga ou repete uma letra em uma palavra com 4 letras ou mais."""
    palavras = texto.split()
    candidatas = [i for i, p in enumerate(palavras) if len(p) >= 4]
    while True:
        i = rng.choice(candidatas)
        p = palavras[i]
        pos = rng.randrange(1, len(p) - 1)
        tipo = rng.choice(["troca", "falta", "sobra"])
        if tipo == "troca":
            nova = p[:pos] + p[pos + 1] + p[pos] + p[pos + 2:]
        elif tipo == "falta":
            nova = p[:pos] + p[pos + 1:]
        else:
            nova = p[:pos] + p[pos] + p[pos:]
        if nova != p:  # "garrafa" trocando "rr" continua igual; sorteia de novo
            palavras[i] = nova
            return " ".join(palavras)


def maiuscula(texto):
    return texto[0].upper() + texto[1:] if texto else texto


def texto_achado(obj):
    titulo = maiuscula(f"{obj['tipo']} {obj['cor']}")
    partes = [f"{titulo}."]
    if obj["marca"]:
        partes.append(f"Marca: {obj['marca']}.")
    if obj["detalhe"]:
        partes.append(f"{maiuscula(obj['detalhe'])}.")
    return titulo[:45], " ".join(partes)[:200]


def texto_perdido(obj, tipo):
    titulo = maiuscula(f"{tipo} {obj['cor']}")
    partes = [f"Procuro {tipo} {obj['cor']}."]
    if obj["marca"]:
        partes.append(f"É da marca {obj['marca']}.")
    if obj["detalhe"]:
        partes.append(f"Detalhe: {obj['detalhe']}.")
    return titulo[:45], " ".join(partes)[:200]


def criar_item(titulo, descricao, status, categoria, local, usuario, foto=None):
    item = Item(
        titulo=titulo,
        descricao=descricao,
        status=status,
        categoria=categoria,
        local=local[:45],
        usuario=usuario,    # CONFIRA o nome do campo do usuário (usuario, user, dono...)
        data=date.today(),  # CONFIRA; se a data for preenchida automaticamente, apague esta linha
    )
    if foto:
        # O próprio FIND grava a imagem no banco e calcula o image_hash no save().
        item.imagem.save(foto.name, ContentFile(foto.read_bytes()), save=False)
    item.save()
    return item


class Command(BaseCommand):
    help = "Cria os perdidos, os achados e o gabarito do experimento."

    def add_arguments(self, parser):
        parser.add_argument("--semente", type=int, default=42)

    def handle(self, *args, **opcoes):
        # 1. Segurança: nunca roda fora do ambiente local.
        if not settings.DEBUG:
            raise CommandError("Este comando só roda com DEBUG=True.")

        # 2. Um único sorteador para o comando inteiro. Nunca use random.choice direto.
        rng = random.Random(opcoes["semente"])

        # 3. Lê os arquivos de dados.
        with open(DADOS / "catalogo.csv", encoding="utf-8-sig") as arquivo:
            catalogo = list(csv.DictReader(arquivo))
        sinonimos = json.loads((DADOS / "sinonimos.json").read_text(encoding="utf-8"))
        locais = (DADOS / "locais.txt").read_text(encoding="utf-8").splitlines()

        # 4. Apaga só o que este comando criou na rodada anterior (usuários "tcc_").
        Item.objects.filter(usuario__username__startswith="tcc_").delete()  # CONFIRA "usuario"
        Usuario = get_user_model()
        dono, _ = Usuario.objects.get_or_create(username="tcc_dono")
        achador, _ = Usuario.objects.get_or_create(username="tcc_achador")

        # 5. Sorteia o grupo de variação de cada objeto: 10 em cada grupo.
        #    O grupo "sem_acento" só pode receber objetos que têm acento no texto.
        com_acento = [obj["id"] for obj in catalogo if tem_acento(obj)]
        if len(com_acento) < 10:
            raise CommandError("O catálogo precisa de pelo menos 10 objetos com acento.")
        grupo = {id_: "sem_acento" for id_ in rng.sample(com_acento, 10)}
        resto = [obj["id"] for obj in catalogo if obj["id"] not in grupo]
        rng.shuffle(resto)
        outros = ["nenhuma", "sinonimo", "erro_digitacao"]
        grupo.update({id_: outros[i % 3] for i, id_ in enumerate(resto)})
        quantos_do_tipo = Counter(obj["tipo"] for obj in catalogo)

        for obj in catalogo:
            numero = int(obj["id"])
            categoria = Categoria.objects.get(nome=obj["categoria"])  # CONFIRA "nome"
            local = rng.choice(locais)

            # 6. Achado verdadeiro: foto A e texto padrão.
            titulo, descricao = texto_achado(obj)
            achado = criar_item(titulo, descricao, "achado", categoria, local, achador,
                                DADOS / "fotos" / f"{numero:03d}_A.jpg")

            # 7. Perdido: foto B e texto do dono, com a variação do grupo.
            variacao = grupo[obj["id"]]
            tipo = obj["tipo"]
            if variacao == "sinonimo":
                tipo = rng.choice(sinonimos[obj["tipo"]])
            elif variacao == "erro_digitacao":
                tipo = errar_digitacao(tipo, rng)
            titulo, descricao = texto_perdido(obj, tipo)
            if variacao == "sem_acento":
                titulo, descricao = tirar_acentos(titulo), tirar_acentos(descricao)
            perdido = criar_item(titulo, descricao, "perdido", categoria, rng.choice(locais), dono,
                                 DADOS / "fotos" / f"{numero:03d}_B.jpg")

            # 8. Gabarito.
            ParGabarito.objects.create(
                perdido=perdido,
                achado=achado,
                variacao=variacao,
                objeto_parecido=quantos_do_tipo[obj["tipo"]] > 1,
            )

            # 9. Distrator "quase igual": sem foto, com outra cor.
            outra_cor = rng.choice([c for c in CORES_TROCA if c != obj["cor"]])
            titulo, descricao = texto_achado({**obj, "cor": outra_cor})
            criar_item(titulo, descricao, "achado", categoria, rng.choice(locais), achador)

        self.stdout.write(self.style.SUCCESS(
            f"{Item.objects.filter(status='perdido', usuario=dono).count()} perdidos, "
            f"{Item.objects.filter(status='achado', usuario=achador).count()} achados, "
            f"{ParGabarito.objects.count()} pares."
        ))
```

**Por que o sorteador único importa:** com a mesma semente, `rng` sorteia sempre os mesmos números, **na mesma ordem**. Por isso o comando gera sempre os mesmos itens. Se você usar `random.choice` em algum lugar, ou mudar a ordem das linhas que sorteiam, os dados mudam.

**Como conferir:**

1. Rode `python manage.py gerar_dados --semente 42`. A mensagem final deve dizer **40 perdidos, 80 achados, 40 pares**.
2. No `/admin/`, abra 3 pares de cada grupo e confira se a variação foi aplicada ("squeeze" no lugar de "garrafa", "garafa", "oculos").
3. Anote o título de 3 perdidos, rode o comando de novo e confira se os títulos são **exatamente os mesmos**.

**Pronto quando:** os três itens acima estão corretos e você mostra ao orientador um par de cada grupo.

---

## Semana 3: texto, métricas e primeira avaliação

**Período:** 12/10 a 16/10. **Objetivo:** ter a primeira tabela de resultados, comparando B0 e T1.

### Tarefa 3.1 - Normalização do texto

Em `correspondencia/texto.py`:

```python
import string
import unicodedata

from nltk.corpus import stopwords


def tirar_acentos(texto):
    return "".join(c for c in unicodedata.normalize("NFKD", texto) if not unicodedata.combining(c))


STOPWORDS = {tirar_acentos(p) for p in stopwords.words("portuguese")}


def normalizar(texto):
    """Minúsculas, sem acentos, sem pontuação e sem stopwords."""
    texto = tirar_acentos(texto.lower())
    texto = texto.translate(str.maketrans(string.punctuation, " " * len(string.punctuation)))
    return " ".join(p for p in texto.split() if p not in STOPWORDS)


def texto_do_item(item):
    return f"{item.titulo} {item.descricao}"
```

*Stopwords* são palavras muito comuns que não ajudam a diferenciar os itens ("de", "a", "com", "na"). Teste no terminal (`python manage.py shell`):

```python
from correspondencia.texto import normalizar
normalizar("Óculos de sol, pretos!")   # deve dar "oculos sol pretos"
```

### Tarefa 3.2 - Métricas

Para cada perdido, a estratégia ordena os 80 achados. O que importa é a **posição** em que o achado correto ficou. Com a posição de todos os perdidos, calcule:

| Métrica | Em palavras | O que diz ao usuário |
|---|---|---|
| **Recall@1** | fração dos perdidos em que o correto ficou em **1º** | a estratégia "acertou de primeira"? |
| **Recall@6** | fração dos perdidos em que o correto ficou **entre os 6 primeiros** | o FIND mostra 6 sugestões: é a chance de o dono **ver** o seu objeto |
| **MRR** | média de `1 / posição` | resume tudo em um número: 1º vale 1; 2º vale 0,5; 4º vale 0,25; 20º vale 0,05 |

Em `correspondencia/metricas.py`:

```python
def recall_em_k(posicoes, k):
    return sum(1 for p in posicoes if p <= k) / len(posicoes)


def mrr(posicoes):
    return sum(1 / p for p in posicoes) / len(posicoes)


def posicao_do_correto(pontuacoes, id_correto):
    """Ordena da maior para a menor pontuação; em empate, pelo menor id."""
    ordem = sorted(pontuacoes, key=lambda id_: (-pontuacoes[id_], id_))
    return ordem.index(id_correto) + 1
```

Calcule à mão e depois confira com um teste: posições `[1, 2, 4]` → Recall@1 = 0,333; Recall@6 = 1,0; MRR = (1 + 0,5 + 0,25) / 3 ≈ 0,583.

### Tarefa 3.3 - Estratégia T1 (TF-IDF)

Acrescente em `correspondencia/estrategias.py`:

```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

from .texto import normalizar, texto_do_item


class T1(Estrategia):
    nome = "T1"

    def preparar(self, candidatos):
        super().preparar(candidatos)
        # Cada texto vira um vetor com o "peso" de cada trecho de 3 a 5 letras.
        self.vetorizador = TfidfVectorizer(analyzer="char_wb", ngram_range=(3, 5))
        textos = [normalizar(texto_do_item(c)) for c in self.candidatos]
        self.matriz = self.vetorizador.fit_transform(textos)

    def pontuar(self, perdido):
        consulta = self.vetorizador.transform([normalizar(texto_do_item(perdido))])
        similaridades = cosine_similarity(consulta, self.matriz)[0]  # de 0 a 1
        return {c.id: float(s) for c, s in zip(self.candidatos, similaridades)}
```

Para entender o que a T1 faz, rode no `python manage.py shell`:

```python
from sklearn.feature_extraction.text import TfidfVectorizer
v = TfidfVectorizer(analyzer="char_wb", ngram_range=(3, 5))
v.fit(["garrafa azul"])
print(v.get_feature_names_out())   # os trechos de letras que a T1 compara
```

As configurações (`char_wb`, de 3 a 5 letras) estão **fixadas** e não serão trocadas. No texto, você vai justificar a escolha com a literatura.

### Tarefa 3.4 - Comando `avaliar`

Crie `correspondencia/management/commands/avaliar.py`. Nesta semana, a lista `estrategias` tem só B0 e T1; na semana 4 você acrescenta as outras.

```python
from pathlib import Path

import matplotlib

matplotlib.use("Agg")  # gera os gráficos sem abrir janela
import matplotlib.pyplot as plt
import pandas as pd
from django.core.management.base import BaseCommand

from correspondencia.estrategias import B0, STATUS_CANDIDATOS, T1
from correspondencia.metricas import mrr, posicao_do_correto, recall_em_k
from correspondencia.models import ParGabarito
from items.models import Item

RESULTADOS = Path(__file__).resolve().parents[2] / "resultados"


def resumir(posicoes, colunas):
    """Calcula as métricas agrupando as posições pelas colunas indicadas."""
    return (
        posicoes.groupby(colunas, sort=False)["posicao"]
        .agg(
            consultas="count",
            recall_1=lambda p: recall_em_k(list(p), 1),
            recall_6=lambda p: recall_em_k(list(p), 6),
            mrr=lambda p: mrr(list(p)),
        )
        .round(3)
        .reset_index()
    )


class Command(BaseCommand):
    help = "Roda as estratégias e gera as tabelas e os gráficos em resultados/."

    def handle(self, *args, **opcoes):
        RESULTADOS.mkdir(exist_ok=True)
        candidatos = list(Item.objects.filter(status__in=STATUS_CANDIDATOS))
        pares = list(ParGabarito.objects.select_related("perdido", "achado"))
        estrategias = [B0(), T1()]

        # 1. Posição do achado correto para cada perdido e cada estratégia.
        linhas = []
        for estrategia in estrategias:
            estrategia.preparar(candidatos)
            for par in pares:
                pontuacoes = estrategia.pontuar(par.perdido)
                linhas.append({
                    "estrategia": estrategia.nome,
                    "perdido_id": par.perdido_id,
                    "posicao": posicao_do_correto(pontuacoes, par.achado_id),
                    "pontuacao_correto": round(pontuacoes[par.achado_id], 3),
                    "variacao": par.variacao,
                    "objeto_parecido": par.objeto_parecido,
                })
        posicoes = pd.DataFrame(linhas)
        posicoes.to_csv(RESULTADOS / "posicoes.csv", index=False)

        # 2. Tabela principal.
        metricas = resumir(posicoes, ["estrategia"])
        metricas.to_csv(RESULTADOS / "metricas.csv", index=False)
        self.stdout.write(metricas.to_string(index=False))

        # 3. Quantas vezes o FIND de hoje nem mostraria o correto (pontuação abaixo de 30).
        b0 = posicoes[posicoes["estrategia"] == "B0"]
        abaixo = int((b0["pontuacao_correto"] < 0.30).sum())
        self.stdout.write(f"B0: correto abaixo de 0,30 em {abaixo} de {len(b0)} perdidos")
```

Rode `python manage.py avaliar`. Abra `resultados/metricas.csv` e `resultados/posicoes.csv` no VS Code e confira se os números fazem sentido (por exemplo, nenhuma posição maior que 80).

> **Sobre o limiar de 30 do FIND:** na avaliação, a B0 ordena **todos** os candidatos, sem o corte de 30 pontos, para sabermos em que posição o correto ficou. A última linha do comando conta em quantos casos o FIND **nem mostraria** o item correto. É um dado simples e forte para a discussão.

**Pronto quando:** `metricas.csv` tem as linhas de B0 e T1, e você mostra a tabela ao orientador.

---

## Semana 4: imagem e combinação

**Período:** 19/10 a 23/10. **Objetivo:** ter a **tabela principal** do TCC, com as 4 estratégias, e o gráfico de robustez.

### Tarefa 4.1 - Estratégia V (pHash + histograma de cor)

1. Leia o método `buscar_por_imagem` e o `_gerar_image_hash` em `items/models.py`. Anote: o tamanho do pHash, **quantas faixas** (*bins*) o histograma HSV usa e como os dois são combinados.
2. Acrescente em `estrategias.py` o código abaixo. Ele segue a mesma lógica do FIND. **Troque `FAIXAS = (8, 8, 8)` pelas faixas que o FIND usa**, se forem diferentes.

```python
import imagehash
import numpy as np
from PIL import Image

FAIXAS = (8, 8, 8)  # CONFIRA: faixas de H, S e V usadas no FIND


def histograma(item):
    """Histograma de cor HSV da foto do item, normalizado para somar 1."""
    with item.imagem.open("rb") as arquivo:
        hsv = np.array(Image.open(arquivo).convert("RGB").convert("HSV"))
    hist, _ = np.histogramdd(hsv.reshape(-1, 3), bins=FAIXAS, range=((0, 256),) * 3)
    return hist.ravel() / hist.sum()


class V(Estrategia):
    nome = "V"

    def preparar(self, candidatos):
        super().preparar(candidatos)
        # Hash e histograma de cada candidato com foto, calculados uma única vez.
        self.fotos = {
            c.id: (imagehash.hex_to_hash(c.image_hash), histograma(c))
            for c in self.candidatos
            if c.imagem and c.image_hash
        }

    def pontuar(self, perdido):
        hash_p = imagehash.hex_to_hash(perdido.image_hash)
        hist_p = histograma(perdido)
        pontuacoes = {}
        for c in self.candidatos:
            if c.id not in self.fotos:
                pontuacoes[c.id] = 0.0  # achado sem foto não pode ser confirmado pela imagem
                continue
            hash_c, hist_c = self.fotos[c.id]
            nota_hash = 1 - (hash_p - hash_c) / hash_p.hash.size  # 1 - Hamming / 256
            nota_hist = float(np.minimum(hist_p, hist_c).sum())    # interseção de histogramas
            pontuacoes[c.id] = 0.5 * nota_hash + 0.5 * nota_hist
        return pontuacoes
```

Para entender, anote o que cada parte mede:

- `hash_p - hash_c` é a **distância de Hamming**: quantos dos 256 bits são diferentes. Fotos iguais → 0 → nota 1;
- a **interseção de histogramas** soma, faixa por faixa, o menor dos dois valores. Fotos com a mesma "paleta" de cores → perto de 1.

### Tarefa 4.2 - Estratégia F (combinação)

```
com foto:  F = 0,6 × T1 + 0,3 × V + 0,1 × categoria
sem foto:  F = (0,6 × T1 + 0,1 × categoria) / 0,7     →  ≈ 0,857 × T1 + 0,143 × categoria
```

`categoria` vale 1 se a categoria do achado é a mesma do perdido, e 0 se não é. Sem foto, a parte da imagem sai, e os pesos que sobram são **divididos por 0,7** para continuarem somando 1.

**Por que esses pesos?** O texto existe em todos os itens e é a evidência mais completa; a foto ajuda, mas nem sempre existe e sofre com fundo e luz; a categoria é grosseira (muitos objetos diferentes têm a mesma), mas já é usada pelo FIND. Os pesos **são fixados antes** de rodar e **não serão ajustados**.

```python
class F(Estrategia):

    def __init__(self, usar_foto=True):
        self.usar_foto = usar_foto
        self.nome = "F" if usar_foto else "F (sem foto)"
        self.t1 = T1()
        self.v = V()

    def preparar(self, candidatos):
        super().preparar(candidatos)
        self.t1.preparar(self.candidatos)
        if self.usar_foto:
            self.v.preparar(self.candidatos)

    def partes(self, perdido):
        """Devolve, para cada candidato, as três partes da pontuação e a pontuação final."""
        texto = self.t1.pontuar(perdido)
        imagem = self.v.pontuar(perdido) if self.usar_foto else None
        resultado = {}
        for c in self.candidatos:
            categoria = 1.0 if c.categoria_id == perdido.categoria_id else 0.0
            if imagem is None:
                final = (0.6 * texto[c.id] + 0.1 * categoria) / 0.7
            else:
                final = 0.6 * texto[c.id] + 0.3 * imagem[c.id] + 0.1 * categoria
            resultado[c.id] = {
                "texto": texto[c.id],
                "imagem": imagem[c.id] if imagem is not None else None,
                "categoria": categoria,
                "final": final,
            }
        return resultado

    def pontuar(self, perdido):
        return {id_: p["final"] for id_, p in self.partes(perdido).items()}
```

A F guarda **as três partes** porque elas explicam a sugestão ao usuário ("apareceu porque o texto é 82% parecido e a categoria é a mesma"). O comando `sugerir` (Tarefa 5.2) mostra isso.

### Tarefa 4.3 - Completar o `avaliar`: tabela principal, robustez e gráficos

1. No `avaliar.py`, importe `V` e `F` e troque a lista de estratégias por:

```python
estrategias = [B0(), T1(), V(), F(usar_foto=True), F(usar_foto=False)]
```

2. No final do `handle`, acrescente a **robustez** (as métricas separadas por grupo) e os **gráficos**:

```python
        # 4. Robustez: métricas por grupo de variação e por objeto parecido.
        resumir(posicoes, ["estrategia", "variacao"]).to_csv(RESULTADOS / "robustez_variacao.csv", index=False)
        resumir(posicoes, ["estrategia", "objeto_parecido"]).to_csv(RESULTADOS / "robustez_parecido.csv", index=False)

        # 5. Gráficos (PNG, 300 dpi).
        graficos = RESULTADOS / "graficos"
        graficos.mkdir(exist_ok=True)

        eixo = metricas.set_index("estrategia")[["recall_1", "recall_6", "mrr"]].plot.bar(rot=0)
        eixo.set_xlabel("Estratégia")
        eixo.set_ylabel("Valor da métrica")
        eixo.set_ylim(0, 1)
        plt.tight_layout()
        plt.savefig(graficos / "metricas.png", dpi=300)
        plt.close()

        robustez = resumir(posicoes, ["estrategia", "variacao"])
        tabela = robustez.pivot(index="variacao", columns="estrategia", values="recall_6")
        eixo = tabela[["B0", "T1", "F", "F (sem foto)"]].plot.bar(rot=0)
        eixo.set_xlabel("Variação no texto do perdido")
        eixo.set_ylabel("Recall@6")
        eixo.set_ylim(0, 1)
        plt.tight_layout()
        plt.savefig(graficos / "robustez.png", dpi=300)
        plt.close()
```

3. Rode `python manage.py avaliar` e abra os dois gráficos.

**Como ler a robustez:** cada grupo tem só **10 perdidos**. Uma diferença de 0,1 no Recall@6 é **um** perdido a mais ou a menos. No texto, sempre diga quantos perdidos há em cada grupo antes de tirar conclusões.

**Pronto quando:** `metricas.csv` tem as 5 linhas (B0, T1, V, F e F sem foto), os dois CSVs de robustez e os dois gráficos estão em `resultados/`, e você mostra tudo ao orientador. Essa é a **tabela principal** do TCC.

---

## Semana 5: tempo, sugestões, testes e README

**Período:** 26/10 a 30/10. **Objetivo:** fechar o experimento. Depois desta semana, o código só muda para corrigir erros.

### Tarefa 5.1 - Tempo de resposta

A pergunta é: **as estratégias continuam rápidas com muitos itens cadastrados?** Para isso, o comando junta aos 80 achados reais **1.000 achados extras** criados só na memória (sem salvar no banco).

1. No `avaliar.py`, acrescente a opção `--tempo`:

```python
    def add_arguments(self, parser):
        parser.add_argument("--tempo", action="store_true", help="Mede o tempo de resposta.")
```

2. No início do `handle`, logo depois de buscar `candidatos` e `pares`:

```python
        if opcoes["tempo"]:
            self.medir_tempo(candidatos, pares)
            return
```

3. Acrescente o método na classe `Command` (e `import time` no topo do arquivo):

```python
    def medir_tempo(self, candidatos, pares):
        # 1.000 achados extras só de texto: os 40 distratores repetidos 25 vezes, sem salvar no banco.
        distratores = [c for c in candidatos if not c.imagem]
        extras = [
            Item(id=1_000_000 + i, titulo=d.titulo, descricao=d.descricao,
                 categoria=d.categoria, status="achado")
            for i, d in enumerate(distratores * 25)
        ]
        todos = candidatos + extras

        linhas = []
        for estrategia in [B0(), T1(), F(usar_foto=False)]:
            inicio = time.perf_counter()
            estrategia.preparar(todos)
            preparar_ms = (time.perf_counter() - inicio) * 1000

            tempos = []
            for par in pares[:31]:
                inicio = time.perf_counter()
                estrategia.pontuar(par.perdido)
                tempos.append((time.perf_counter() - inicio) * 1000)
            tempos = tempos[1:]  # descarta a primeira consulta (aquecimento)

            linhas.append({
                "estrategia": estrategia.nome,
                "candidatos": len(todos),
                "preparar_ms": round(preparar_ms, 1),
                "consulta_ms": round(sum(tempos) / len(tempos), 1),
            })

        # Parte da imagem: tempo de calcular o histograma de uma foto (média de 10 fotos).
        tempos = []
        for par in pares[:10]:
            inicio = time.perf_counter()
            histograma(par.perdido)
            tempos.append((time.perf_counter() - inicio) * 1000)
        linhas.append({"estrategia": "V (histograma de 1 foto)", "candidatos": 1,
                       "preparar_ms": None, "consulta_ms": round(sum(tempos) / len(tempos), 1)})

        tabela = pd.DataFrame(linhas)
        tabela.to_csv(RESULTADOS / "tempos.csv", index=False)
        self.stdout.write(tabela.to_string(index=False))
```

(Importe também `histograma` e `F` de `correspondencia.estrategias`.)

4. Rode `python manage.py avaliar --tempo` com **nenhum outro programa pesado aberto**. Anote o **processador** e a **memória** do computador (Configurações → Sistema → Sobre).

A V não entra na medição com 1.000 extras porque os extras não têm foto. O hash já é calculado pelo FIND quando o item é cadastrado; o histograma, como mostra o tempo medido, também poderia ser.

### Tarefa 5.2 - Comando `sugerir`

Mostra, no terminal, as 6 sugestões da F para um perdido, com as partes da pontuação. É a "tela" que você vai usar na análise de erros e no TCC para mostrar que a sugestão é **explicável**.

`correspondencia/management/commands/sugerir.py`:

```python
from django.core.management.base import BaseCommand

from correspondencia.estrategias import F, STATUS_CANDIDATOS
from items.models import Item


class Command(BaseCommand):
    help = "Mostra as 6 sugestões da F para um item perdido."

    def add_arguments(self, parser):
        parser.add_argument("perdido_id", type=int)

    def handle(self, *args, **opcoes):
        perdido = Item.objects.get(id=opcoes["perdido_id"])
        f = F()
        f.preparar(Item.objects.filter(status__in=STATUS_CANDIDATOS))
        partes = f.partes(perdido)
        itens = {c.id: c for c in f.candidatos}
        correto = perdido.gabarito.achado_id

        self.stdout.write(f"PERDIDO: {perdido.titulo} | {perdido.descricao}\n")
        melhores = sorted(partes, key=lambda id_: (-partes[id_]["final"], id_))[:6]
        for posicao, id_ in enumerate(melhores, start=1):
            p = partes[id_]
            marca = "  <-- CORRETO" if id_ == correto else ""
            self.stdout.write(
                f"{posicao}. {itens[id_].titulo:<30} final {p['final']:.2f} | "
                f"texto {p['texto']:.2f} | imagem {p['imagem']:.2f} | categoria {p['categoria']:.0f}{marca}"
            )
```

Descubra o `id` de um perdido no `/admin/` e rode `python manage.py sugerir <id>`.

### Tarefa 5.3 - Testes automatizados

Em `correspondencia/tests/`, garanta estes 6 testes (os 3 primeiros você já tem):

| Teste | O que confere |
|---|---|
| `test_b0.py` | os 3 casos calculados à mão (Tarefa 1.3) |
| `test_texto.py` | `normalizar("Óculos de sol, pretos!") == "oculos sol pretos"` |
| `test_metricas.py` | posições `[1, 2, 4]` → Recall@1 = 1/3, Recall@6 = 1, MRR ≈ 0,583 |
| `test_t1.py` | um achado com o **mesmo texto** do perdido fica em 1º |
| `test_f.py` | com `usar_foto=False`, mesmo texto e mesma categoria → pontuação final = 1 (os pesos somam 1) |
| `test_fotos.py` | uma foto de `dados/fotos/` não tem EXIF: `Image.open(caminho).getexif()` está vazio |

Exemplo do teste das métricas:

```python
import pytest

from correspondencia.metricas import mrr, recall_em_k


def test_metricas_com_exemplo_calculado_a_mao():
    posicoes = [1, 2, 4]
    assert recall_em_k(posicoes, 1) == pytest.approx(1 / 3)
    assert recall_em_k(posicoes, 6) == 1
    assert mrr(posicoes) == pytest.approx(0.5833, abs=0.001)
```

Rode `pytest`. Os seus testes e os do FIND (se houver) têm de passar.

### Tarefa 5.4 - README e *tag*

`correspondencia/README.md` deve permitir que **outra pessoa** reproduza tudo, do zero, em um Windows com Python. Escreva nesta ordem:

1. **O que é:** duas frases sobre o experimento.
2. **Instalação:** clonar o FIND, trocar para a *branch* `tcc-correspondencia`, criar o ambiente, instalar os dois `requirements`, baixar as *stopwords* e criar o `.env`.
3. **Dados:** `migrate`, `criar_categorias` e `gerar_dados --semente 42` (as fotos tratadas já estão no repositório).
4. **Avaliação:** `avaliar` e `avaliar --tempo`, com uma tabela dizendo **qual tabela ou figura do TCC** cada arquivo de `resultados/` vira.
5. **Sugestões:** como usar o `sugerir`.
6. **Computador usado:** processador e memória em que os tempos foram medidos.

Depois, **teste o README**: apague o `db.sqlite3` e a pasta `resultados/`, siga o README do início e confira se `metricas.csv` sai com **os mesmos números**. Se sair, marque a versão:

```powershell
git tag -a tcc-resultados -m "Versão usada nos resultados do TCC"
git push origin tcc-resultados
```

**Pronto quando:** o README reproduz os mesmos números e a *tag* `tcc-resultados` está no GitHub.

---

## Semanas 6 e 7: folga, análise de erros e extras

**Período:** 02/11 a 13/11. Estas duas semanas existem para **absorver atrasos** e para você **escrever os Resultados** com calma.

**Análise de erros (obrigatória, e é a parte mais importante):**

1. Abra `resultados/posicoes.csv` e filtre as linhas da estratégia `F` com `posicao` maior que 6.
2. Escolha de 3 a 5 desses perdidos, de grupos diferentes, se possível.
3. Para cada um, rode `python manage.py sugerir <id>` e anote em uma tabela: os dois textos, as duas fotos, a posição do correto e **a causa provável** (sinônimo desconhecido, objeto parecido com o mesmo vocabulário, foto escura, fundo dominante...).
4. Faça o mesmo com **1 caso em que a F acertou e a B0 errou**. Ele mostra, na prática, o que a combinação ganha.

Essa tabela vai direto para os Resultados.

**Extras opcionais** - só com o experimento principal **fechado e aprovado pelo orientador**, e **um de cada vez**:

- estratégia **S1**, de similaridade de *strings* (`rapidfuzz`, `fuzz.token_set_ratio`), como mais uma técnica textual;
- teste de Wilcoxon pareado (`scipy.stats.wilcoxon`) sobre o `1 / posição` de cada perdido, comparando F × B0;
- uma página no FIND que mostre o resultado do `sugerir` com as fotos.

Se não der tempo de fazer os extras, **não tem problema**: eles viram trabalhos futuros no texto.

---

## Se algo der errado

| Problema | O que fazer |
|---|---|
| O FIND não roda no laboratório | Avise o orientador **no mesmo dia**. Plano B: um projeto Django separado, com cópia dos modelos `Categoria` e `Item` |
| `Unknown command: 'gerar_dados'` | Falta o `__init__.py` em `management/` ou em `management/commands/`, ou a app não está no `INSTALLED_APPS` |
| A `_calcular_match_score` não pode ser chamada de fora | Copie a função para `estrategias.py` sem alterar nada e anote o *commit* de origem (Tarefa 1.3) |
| `gerar_dados` dá erro de campo obrigatório | Abra `items/models.py`, veja o campo que falta e preencha no `criar_item` |
| Gravar a foto no item dá erro | Veja como o formulário de cadastro do FIND salva a imagem e faça igual; se não resolver, pergunte |
| `KeyError` com o nome de um tipo | Esse `tipo` do catálogo não está no `sinonimos.json`, ou está escrito diferente |
| As fotos atrasaram | Não reduza para menos de 30 objetos; avise o orientador antes |
| Um resultado ficou "ruim" | **Não mexa em nada.** Anote e leve para a discussão |

**Como pedir ajuda.** Mande, em uma única mensagem: (1) o que você estava tentando fazer (número da tarefa); (2) o comando que rodou; (3) o erro completo, copiado do terminal como texto, e não como foto da tela; (4) o que você já tentou. Assim a resposta vem mais rápido.

---

## Checklist final

- [ ] Todo o código em `correspondencia/`, na *branch* `tcc-correspondencia`; fora dela, só `settings.py`, `.gitignore` e `pytest.ini`.
- [ ] B0 chamando a função real do FIND, com 3 testes calculados à mão.
- [ ] Catálogo, sinônimos, locais e 80 fotos tratadas (sem EXIF) no repositório.
- [ ] `gerar_dados --semente 42` gera 40 perdidos, 80 achados e 40 pares, sempre iguais.
- [ ] B0, T1, V e F (com e sem foto) seguindo a mesma forma (`preparar` e `pontuar`).
- [ ] Nenhum parâmetro alterado depois de ver os resultados.
- [ ] Em `resultados/`: `metricas.csv`, `posicoes.csv`, `robustez_variacao.csv`, `robustez_parecido.csv`, `tempos.csv` e os 2 gráficos.
- [ ] Comando `sugerir` funcionando.
- [ ] Análise de erros com 3 a 5 casos e 1 acerto da F sobre a B0.
- [ ] `pytest` passando.
- [ ] README que reproduz tudo do zero e *tag* `tcc-resultados` no GitHub.
