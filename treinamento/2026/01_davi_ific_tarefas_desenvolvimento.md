# Plano de tarefas de desenvolvimento – Davi (Tecnologia em Sistemas para Internet)

**Projeto pai:** iFIC – Desenvolvimento de Funcionalidades de Autenticação, Administração e Gerenciamento de Cursos de Formação Inicial e Continuada (ver `.llm/ific/projeto.md`).

**Temática escolhida:** S5 – Otimização de desempenho: consultas no ORM do Django e cache com Redis (ver `.llm/ific/tematicas.md`).

**Perfil do aluno:** 1 aluno do Curso Superior de Tecnologia em Sistemas para Internet, com conhecimentos intermediários em Python e em treinamento. As sprints são pequenas e detalhadas de propósito. Você já sabe programar; o que vai aprender aqui é uma coisa nova e específica: **medir antes, mudar uma coisa só, medir de novo**.

**Duração:** 8 sprints de 1 semana (22/09/2026 a 16/11/2026).

**Onde o trabalho acontece:** o **repositório de treinamento do projeto já existe** e é compartilhado com os outros alunos. Você **não vai criar repositório nenhum**. Todo o seu trabalho fica dentro de **uma única subpasta sua**:

```
<repositorio-de-treinamento>/
├── ...              ← pastas de outros alunos (não mexa)
└── davi/            ← a sua subpasta: tudo o que você fizer fica aqui dentro
```

Confirme com o orientador o **endereço do repositório** e o **nome exato da sua subpasta** antes de começar. Todos os caminhos deste documento são relativos a ela.

---

## A ideia do trabalho, em uma página

Você vai construir **uma única página**: a listagem pública de cursos e turmas FIC. Ela mostra, para cada turma: nome do curso, eixo, campus, turno, carga horária, datas, vagas, inscritos e vagas restantes.

Só que você vai escrever essa mesma página **cinco vezes**, cada uma um pouco mais rápida que a anterior, e vai **medir** cada uma:

| Versão | Endereço | O que muda em relação à anterior |
|---|---|---|
| V0 | `/cursos/v0/` | Versão "ingênua", escrita sem pensar em desempenho. É o ponto de partida |
| V1 | `/cursos/v1/` | Usa `select_related` para buscar os dados relacionados de uma vez |
| V2 | `/cursos/v2/` | Cria índices no banco de dados |
| V3 | `/cursos/v3/` | Manda o banco contar os inscritos, em vez de contar no Python |
| V4 | `/cursos/v4/` | Guarda o resultado pronto no Redis (cache) |

**Por que as cinco ficam no ar ao mesmo tempo, em endereços diferentes?**

Porque assim você mede todas **no mesmo dia, na mesma máquina, com os mesmos dados**. Se medisse cada versão em um dia, qualquer diferença (computador mais quente, outro programa aberto, banco em outro estado) entraria no resultado e você não saberia o que foi otimização e o que foi acaso. É uma decisão simples, mas é a que faz a comparação valer alguma coisa — e você vai escrever sobre ela no artigo.

### Modelo de dados

Seis tabelas, nada complicado:

```
Campus            (nome, cidade)
EixoTecnologico   (nome)
CursoFIC          (codigo, nome, carga_horaria, eixo → EixoTecnologico)
Turma             (curso → CursoFIC, campus → Campus, turno, vagas,
                   data_inicio, data_fim, situacao)
Candidato         (nome, email, cidade)
Inscricao         (turma → Turma, candidato → Candidato, data_inscricao)
```

### Volumes da base de dados

Só dois tamanhos, para não complicar:

| Base | Cursos | Turmas | Candidatos | Inscrições |
|---|---|---|---|---|
| Pequena (para testes) | 30 | 100 | 1.000 | 2.000 |
| Grande (para medições) | 150 | 1.000 | 20.000 | 50.000 |

> **Regra do projeto:** nenhum dado real de pessoas. Tudo é inventado por script, com a biblioteca `Faker` em português (LGPD, Lei nº 13.709/2018). Como não há pessoas envolvidas, não é preciso submeter nada ao Comitê de Ética em Pesquisa.

### Ferramentas (sem Docker)

Tudo instalado direto na máquina:

| Ferramenta | Para quê |
|---|---|
| Python 3.12 + Django 5 | A aplicação |
| MySQL 8 | O banco de dados |
| Redis | O cache (Sprint 7) |
| `django-debug-toolbar` | Ver quantas consultas SQL cada página faz |
| `Locust` | Simular vários usuários acessando ao mesmo tempo |
| `Faker` | Gerar os dados fictícios |
| Google Sheets ou Excel | Guardar as medições e fazer os gráficos |

**Por que MySQL e não SQLite?** Porque este trabalho mede o que acontece quando **muita gente acessa ao mesmo tempo**. O SQLite guarda o banco inteiro em um arquivo só e trava esse arquivo a cada escrita — o que você mediria seria a trava do arquivo, não as suas consultas. Escreva isso no artigo, é uma justificativa técnica legítima.

**O Redis não substitui o MySQL.** Os dados continuam todos no MySQL. O Redis só guarda uma cópia pronta do resultado, na memória, para não precisar refazer a consulta toda vez.

---

## Combinados gerais

- **Repositório:** já existe e é compartilhado. Trabalhe **somente dentro da sua subpasta**.
- **Commits:** pelo menos 3 por sprint, com mensagem em português dizendo o que foi feito (ex.: `Adiciona select_related na V1`).
- **Reunião semanal:** no começo de cada sprint você mostra ao orientador o que fez, **rodando na máquina**. A partir da Sprint 3, "está funcionando" não basta: tem que ter número.
- **Travou mais de 40 minutos no mesmo erro? Peça ajuda.**
- **Planilha de medições:** a partir da Sprint 3, toda medição vai para `docs/medicoes.csv` (ou uma planilha no Drive). **Nunca apague uma medição.** Se uma rodada saiu estranha, registre e escreva ao lado o que aconteceu.
- **Diário:** `docs/diario.md`, três linhas no fim de cada sprint — o que funcionou, o que deu errado, o que aprendi. Isso vai virar a Conclusão do artigo.
- **Print de tudo:** capturas de tela em `docs/evidencias/`. Elas vão para o capítulo de Resultados.

### Convivência em repositório compartilhado

1. **Só altere arquivos da sua subpasta.** Nunca edite, mova ou apague arquivo de outro aluno.
2. **Comece o dia com `git pull`.**
3. **Comite só o que é seu:** use `git add davi/`, não `git add .`. Confira com `git status` antes.
4. **Não comite** `.venv/`, `__pycache__/`, senhas, relatórios do Locust.
5. **Deu `CONFLICT`? Pare e chame o orientador.**
6. **`git push` no fim de cada dia.**

---

# Sprint 1 — 22/09 a 28/09/2026
## Preparar o ambiente e criar o projeto Django

**Objetivo:** ao final da semana, ter um projeto Django rodando na sua máquina, conectado ao MySQL, com as seis tabelas criadas e visíveis no Django Admin.

### O que você vai fazer

1. Instalar o MySQL.
2. Criar a sua subpasta no repositório.
3. Criar o ambiente virtual e instalar o Django.
4. Criar o projeto Django e conectá-lo ao MySQL.
5. Escrever os seis modelos.
6. Rodar as migrações e conferir no Admin.

### Passo a passo

**1. Instalar o MySQL (sem Docker).**

- **Windows:** baixe o *MySQL Installer for Windows* no site oficial (`dev.mysql.com/downloads/installer`). Escolha a opção **Developer Default** ou **Server only**. Durante a instalação ele pede uma senha para o usuário `root` — **anote essa senha**, você vai precisar dela. O instalador também traz o **MySQL Workbench**, que é a interface gráfica para ver o banco.
- **Linux (Ubuntu/Debian):** `sudo apt install mysql-server` e depois `sudo mysql_secure_installation`.

Depois de instalado, crie o banco. Abra o MySQL Workbench (ou o terminal `mysql -u root -p`) e execute:

```sql
CREATE DATABASE ific CHARACTER SET utf8mb4;
```

**2. Criar a subpasta.**

```
git clone <endereço-do-repositório>
cd <pasta-do-repositório>
mkdir davi
cd davi
```

**3. Ambiente virtual e Django.**

```
python -m venv .venv
.venv\Scripts\activate           (Windows)
source .venv/bin/activate        (Linux/Mac)

pip install django mysqlclient faker
pip freeze > requirements.txt
```

Se o `mysqlclient` der erro na instalação, use a alternativa:

```
pip install pymysql
```

e acrescente estas duas linhas **no topo** do arquivo `config/__init__.py`:

```python
import pymysql
pymysql.install_as_MySQLdb()
```

Anote qual das duas você usou — isso vai no capítulo de Materiais e Métodos.

**4. Criar o projeto e o app.**

```
django-admin startproject config .
python manage.py startapp catalogo
```

O ponto final no `startproject` é importante: ele cria o projeto na pasta atual, sem criar mais um nível de pasta.

Abra `config/settings.py` e faça três alterações:

```python
INSTALLED_APPS = [
    # ... o que já estava ...
    "catalogo",
]

DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.mysql",
        "NAME": "ific",
        "USER": "root",
        "PASSWORD": "SUA_SENHA_AQUI",
        "HOST": "127.0.0.1",
        "PORT": "3306",
    }
}

LANGUAGE_CODE = "pt-br"
TIME_ZONE = "America/Fortaleza"
```

**5. Tirar a senha do código.** O repositório é compartilhado — a sua senha do MySQL não pode ir para lá. Faça assim, que é o jeito mais simples:

Crie o arquivo `config/settings_local.py` (este arquivo **não** vai para o Git):

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.mysql",
        "NAME": "ific",
        "USER": "root",
        "PASSWORD": "a_sua_senha_de_verdade",
        "HOST": "127.0.0.1",
        "PORT": "3306",
    }
}
SECRET_KEY = "qualquer-coisa-para-desenvolvimento"
```

E no **final** de `config/settings.py`:

```python
try:
    from .settings_local import *
except ImportError:
    pass
```

Crie também um `config/settings_local.exemplo.py`, igual ao de cima mas **sem a senha de verdade**, e comite esse. Assim qualquer pessoa sabe o que precisa preencher.

**6. O `.gitignore` da sua subpasta** (arquivo `davi/.gitignore`):

```
.venv/
__pycache__/
*.pyc
settings_local.py
*.log
relatorios/
```

**7. Escrever os modelos** em `catalogo/models.py`:

```python
from django.db import models


class Campus(models.Model):
    nome = models.CharField(max_length=100)
    cidade = models.CharField(max_length=100)

    def __str__(self):
        return self.nome


class EixoTecnologico(models.Model):
    nome = models.CharField(max_length=100)

    def __str__(self):
        return self.nome


class CursoFIC(models.Model):
    codigo = models.CharField(max_length=20, unique=True)
    nome = models.CharField(max_length=200)
    carga_horaria = models.IntegerField()
    eixo = models.ForeignKey(EixoTecnologico, on_delete=models.PROTECT)

    def __str__(self):
        return self.nome


class Turma(models.Model):
    TURNOS = [("matutino", "Matutino"), ("vespertino", "Vespertino"),
              ("noturno", "Noturno")]
    SITUACOES = [("aberta", "Aberta"), ("encerrada", "Encerrada")]

    curso = models.ForeignKey(CursoFIC, on_delete=models.CASCADE)
    campus = models.ForeignKey(Campus, on_delete=models.PROTECT)
    turno = models.CharField(max_length=20, choices=TURNOS)
    vagas = models.IntegerField()
    data_inicio = models.DateField()
    data_fim = models.DateField()
    situacao = models.CharField(max_length=20, choices=SITUACOES)

    def __str__(self):
        return f"{self.curso.nome} - {self.campus.nome}"


class Candidato(models.Model):
    nome = models.CharField(max_length=200)
    email = models.EmailField()
    cidade = models.CharField(max_length=100)

    def __str__(self):
        return self.nome


class Inscricao(models.Model):
    turma = models.ForeignKey(Turma, on_delete=models.CASCADE)
    candidato = models.ForeignKey(Candidato, on_delete=models.CASCADE)
    data_inscricao = models.DateField()
```

> **Importante:** não coloque `db_index=True` em nenhum campo agora. Os índices são o assunto da Sprint 5, e eles só fazem sentido se existir um "antes" para comparar.

**8. Migrar e conferir.**

```
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

Registre os modelos em `catalogo/admin.py`:

```python
from django.contrib import admin
from .models import Campus, EixoTecnologico, CursoFIC, Turma, Candidato, Inscricao

admin.site.register([Campus, EixoTecnologico, CursoFIC, Turma, Candidato, Inscricao])
```

Rode `python manage.py runserver`, entre em `http://127.0.0.1:8000/admin/` e cadastre um campus, um eixo, um curso e uma turma na mão, só para ver que está tudo funcionando.

**9. Comece o `docs/ambiente.md`** anotando: versão do Python, do Django e do MySQL; processador, memória RAM e tipo de disco (SSD ou HD) da sua máquina; sistema operacional. Isso é exigido no artigo — sem essa informação, nenhum tempo que você medir significa alguma coisa.

### Como saber que deu certo

- [ ] `python manage.py migrate` roda sem erro.
- [ ] As seis tabelas aparecem no MySQL Workbench.
- [ ] Você consegue cadastrar um curso e uma turma pelo Admin.
- [ ] `settings_local.py` **não** aparece no `git status`.
- [ ] `requirements.txt` e `docs/ambiente.md` comitados.

### Erros comuns

- **`Access denied for user 'root'`:** senha errada no `settings_local.py`.
- **`Can't connect to MySQL server`:** o serviço do MySQL não está rodando. No Windows, abra "Serviços" e procure por `MySQL80`.
- **Acentos aparecendo errado:** o banco precisa ter sido criado com `CHARACTER SET utf8mb4`.

---

# Sprint 2 — 29/09 a 05/10/2026
## Gerar os dados e escrever a página V0 (a versão lenta)

**Objetivo:** ter 50.000 inscrições no banco e a primeira versão da página funcionando — de propósito, do jeito errado.

### O que você vai fazer

1. Escrever um comando que popula o banco com dados fictícios.
2. Gerar a base pequena e conferir.
3. Gerar a base grande.
4. Escrever a view e o template da V0.
5. Abrir a página no navegador.

### Passo a passo

**1. Criar a estrutura do comando.** O Django permite criar comandos próprios, que você roda com `python manage.py <nome>`. Crie estas pastas e arquivos:

```
catalogo/
└── management/
    ├── __init__.py
    └── commands/
        ├── __init__.py
        └── popular_base.py
```

Os dois `__init__.py` são arquivos **vazios**, mas precisam existir.

**2. Escrever o comando** em `popular_base.py`:

```python
import random
from datetime import date, timedelta

from django.core.management.base import BaseCommand
from django.db import transaction
from faker import Faker

from catalogo.models import (Campus, EixoTecnologico, CursoFIC,
                             Turma, Candidato, Inscricao)

VOLUMES = {
    "pequena": {"cursos": 30, "turmas": 100, "candidatos": 1000, "inscricoes": 2000},
    "grande": {"cursos": 150, "turmas": 1000, "candidatos": 20000, "inscricoes": 50000},
}


class Command(BaseCommand):
    help = "Popula o banco com dados ficticios de cursos FIC"

    def add_arguments(self, parser):
        parser.add_argument("--volume", default="pequena",
                            choices=["pequena", "grande"])

    @transaction.atomic
    def handle(self, *args, **opcoes):
        fake = Faker("pt_BR")
        Faker.seed(42)
        random.seed(42)

        config = VOLUMES[opcoes["volume"]]

        # limpa tudo antes, para o comando poder ser rodado de novo
        Inscricao.objects.all().delete()
        Turma.objects.all().delete()
        CursoFIC.objects.all().delete()
        Candidato.objects.all().delete()
        Campus.objects.all().delete()
        EixoTecnologico.objects.all().delete()

        # ... criar campi, eixos, cursos, turmas, candidatos e inscricoes ...
        self.stdout.write(self.style.SUCCESS("Base populada!"))
```

**O que é a semente (`seed`) e por que ela importa.** `Faker.seed(42)` e `random.seed(42)` fazem o sorteio sair **sempre igual**. Se outra pessoa rodar o seu comando, ela vai obter exatamente a mesma base que você usou. Sem isso, os números do seu artigo não podem ser conferidos por ninguém. Escreva sobre isso na Metodologia.

**3. Criar os registros, na ordem certa.** Primeiro o que não depende de ninguém (campi e eixos), depois cursos, turmas, candidatos e, por último, inscrições.

**Para inserir muitos registros, use `bulk_create`.** Criar 50.000 inscrições uma a uma com `.save()` levaria muitos minutos, porque cada `.save()` é uma ida ao banco. O `bulk_create` manda tudo em poucas idas:

```python
inscricoes = []
for _ in range(config["inscricoes"]):
    inscricoes.append(Inscricao(
        turma=random.choice(turmas),
        candidato=random.choice(candidatos),
        data_inscricao=date(2026, 1, 1) + timedelta(days=random.randint(0, 60)),
    ))
Inscricao.objects.bulk_create(inscricoes, batch_size=1000)
```

Repare que você acabou de sentir, na prática, exatamente o que o trabalho investiga: **a diferença entre ir ao banco 50.000 vezes e ir 50 vezes**. Anote no diário quanto tempo levou de cada jeito, se tiver curiosidade de testar — é um bom parágrafo para o artigo.

**4. Cuidados com os dados gerados** (nada muito elaborado, só coerência básica):

- a `data_fim` da turma tem de ser depois da `data_inicio`;
- a `data_inscricao` tem de ser antes da `data_inicio` da turma;
- distribua as turmas entre as situações — cerca de metade `aberta` e metade `encerrada`. Se todas ficarem `encerrada`, a listagem vai vir vazia;
- distribua as turmas entre os campi e os turnos.

**5. Rodar e conferir:**

```
python manage.py popular_base --volume pequena
```

Confira no Admin ou no Workbench se os registros apareceram. Depois rode com `--volume grande` e **anote quanto tempo demorou** em `docs/diario.md`.

**6. Escrever a view V0.** Esta é a versão ingênua — escrita como alguém escreveria sem pensar em desempenho. Em `catalogo/views.py`:

```python
from django.shortcuts import render
from .models import Turma, Inscricao


def listar_v0(request):
    """VERSAO INGENUA - ponto de partida da comparacao.
    Escrita de proposito sem nenhuma otimizacao."""
    turmas = Turma.objects.filter(situacao="aberta")

    dados = []
    for turma in turmas:
        inscritos = Inscricao.objects.filter(turma=turma).count()
        dados.append({
            "curso": turma.curso.nome,
            "eixo": turma.curso.eixo.nome,
            "campus": turma.campus.nome,
            "turno": turma.get_turno_display(),
            "carga_horaria": turma.curso.carga_horaria,
            "data_inicio": turma.data_inicio,
            "vagas": turma.vagas,
            "inscritos": inscritos,
            "restantes": turma.vagas - inscritos,
        })

    return render(request, "catalogo/listagem.html",
                  {"dados": dados, "versao": "V0"})
```

**Por que isso é lento?** Cada volta do laço vai ao banco **quatro vezes**: uma para contar as inscrições, uma para buscar o curso, uma para buscar o eixo e uma para buscar o campus. Com 500 turmas abertas, são 1 + 4×500 = **2.001 consultas** para montar uma página. Esse é o problema conhecido como **N+1**, e é o que a V1 vai resolver.

**Deixe o comentário no código** dizendo que a implementação é intencionalmente ingênua. Senão, daqui a seis meses alguém vai achar que foi descuido.

**7. O template** `catalogo/templates/catalogo/listagem.html` — simples mesmo, sem CSS:

```html
<h1>Cursos FIC abertos ({{ versao }})</h1>
<table border="1">
  <tr>
    <th>Curso</th><th>Eixo</th><th>Campus</th><th>Turno</th>
    <th>Carga</th><th>Início</th><th>Vagas</th><th>Inscritos</th><th>Restantes</th>
  </tr>
  {% for item in dados %}
  <tr>
    <td>{{ item.curso }}</td>
    <td>{{ item.eixo }}</td>
    <td>{{ item.campus }}</td>
    <td>{{ item.turno }}</td>
    <td>{{ item.carga_horaria }}</td>
    <td>{{ item.data_inicio }}</td>
    <td>{{ item.vagas }}</td>
    <td>{{ item.inscritos }}</td>
    <td>{{ item.restantes }}</td>
  </tr>
  {% endfor %}
</table>
```

O objeto do trabalho é o que acontece no servidor. Não gaste tempo com layout.

**8. As rotas.** Crie `catalogo/urls.py`:

```python
from django.urls import path
from . import views

app_name = "catalogo"

urlpatterns = [
    path("v0/", views.listar_v0, name="listar_v0"),
]
```

E em `config/urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    # ... admin ...
    path("cursos/", include("catalogo.urls")),
]
```

**9. Uma decisão para tomar agora e não mudar mais: paginação.** A listagem vai mostrar todas as turmas abertas ou só as primeiras 20? Escolha uma opção e **use a mesma nas cinco versões**. Se a V0 listar tudo e a V4 listar 20, a comparação não vale nada. A sugestão é **listar tudo**, porque assim a diferença entre as versões fica mais visível, que é o objetivo didático do trabalho.

### Como saber que deu certo

- [ ] `python manage.py popular_base --volume grande` roda e popula o banco.
- [ ] As contagens batem (confira no Workbench: `SELECT COUNT(*) FROM catalogo_inscricao;`).
- [ ] `http://127.0.0.1:8000/cursos/v0/` abre e mostra a tabela preenchida.
- [ ] A página está visivelmente lenta. **Isso é o esperado nesta sprint.**
- [ ] Print da página em `docs/evidencias/`.

### Erros comuns

- **Comando não encontrado:** faltou um dos `__init__.py`, ou a pasta está com nome errado (tem que ser exatamente `management/commands/`).
- **Página em branco:** provavelmente nenhuma turma ficou com `situacao="aberta"`. Confira no Admin.
- **A carga demora demais:** você está usando `.save()` em vez de `bulk_create`.

---

# Sprint 3 — 06/10 a 12/10/2026
## Aprender a medir (e medir a V0)

**Objetivo:** esta é a sprint mais importante do trabalho. Ao final dela você sabe responder, com número: quantas consultas a V0 faz e quanto tempo ela leva com vários usuários acessando.

Sem isso, tudo o que vier depois é achismo.

### O que você vai fazer

1. Instalar o `django-debug-toolbar` e ver as consultas da V0.
2. Escrever um teste que conta as consultas automaticamente.
3. Instalar o Locust e escrever o arquivo de teste de carga.
4. Escrever o protocolo de medição.
5. Medir a V0 e anotar tudo.

### Passo a passo

**1. Instalar o debug toolbar.**

```
pip install django-debug-toolbar
```

Em `config/settings.py`:

```python
INSTALLED_APPS = [
    # ...
    "debug_toolbar",
]

MIDDLEWARE = [
    "debug_toolbar.middleware.DebugToolbarMiddleware",   # coloque no topo
    # ... o resto ...
]

INTERNAL_IPS = ["127.0.0.1"]
```

Em `config/urls.py`:

```python
from django.conf import settings
from django.urls import include, path

urlpatterns = [
    # ... as suas rotas ...
]

if settings.DEBUG:
    urlpatterns += [path("__debug__/", include("debug_toolbar.urls"))]
```

Rode `python manage.py runserver`, abra `/cursos/v0/` e clique na aba **SQL** do painel lateral. Ele mostra quantas consultas a página fez. **Tire um print disso** — vai ser uma das melhores figuras do seu artigo.

> **Atenção:** o debug toolbar deixa a página mais lenta, porque ele mesmo mede tudo. Ele serve para **investigar**, nunca para medir tempo. Nos testes de carga, ele fica desligado.

**2. Contar as consultas de um jeito confiável.** O número que vai para a tabela do artigo tem de vir de um teste automatizado, não do toolbar. Crie `catalogo/tests.py`:

```python
from django.test import TestCase
from django.test.utils import CaptureQueriesContext
from django.db import connection
from django.urls import reverse

from catalogo.models import Campus, EixoTecnologico, CursoFIC, Turma


class ContagemConsultasTest(TestCase):

    @classmethod
    def setUpTestData(cls):
        campus = Campus.objects.create(nome="Natal-Central", cidade="Natal")
        eixo = EixoTecnologico.objects.create(nome="Informacao e Comunicacao")
        for i in range(20):
            curso = CursoFIC.objects.create(
                codigo=f"FIC-{i}", nome=f"Curso {i}",
                carga_horaria=160, eixo=eixo)
            Turma.objects.create(
                curso=curso, campus=campus, turno="noturno", vagas=30,
                data_inicio="2026-03-01", data_fim="2026-06-30",
                situacao="aberta")

    def test_contar_consultas_v0(self):
        with CaptureQueriesContext(connection) as contexto:
            self.client.get(reverse("catalogo:listar_v0"))
        print(f"\nV0 fez {len(contexto.captured_queries)} consultas")
```

Rode com:

```
python manage.py test catalogo
```

Ele vai imprimir o número de consultas. Com 20 turmas, espere algo em torno de 80. **Anote esse número.** A cada nova versão você repete esse teste e compara.

**3. Instalar o Locust e escrever o teste de carga.**

```
pip install locust
```

Crie o arquivo `locustfile.py` na raiz da sua subpasta:

```python
from locust import HttpUser, task, between


class UsuarioDoCatalogo(HttpUser):
    wait_time = between(1, 3)      # cada usuario espera de 1 a 3s entre acessos

    @task
    def abrir_listagem(self):
        self.client.get("/cursos/v0/")
```

**4. Preparar o servidor para medir.** O `runserver` é um servidor de desenvolvimento: ele atende um pedido de cada vez e não serve para medir carga. Use um servidor de verdade — a instalação é de uma linha:

**Windows:**
```
pip install waitress
waitress-serve --port=8000 --threads=4 config.wsgi:application
```

**Linux/Mac:**
```
pip install gunicorn
gunicorn config.wsgi:application --bind 127.0.0.1:8000 --workers 2
```

Antes de subir o servidor, edite `config/settings_local.py` e coloque:

```python
DEBUG = False
ALLOWED_HOSTS = ["127.0.0.1", "localhost"]
```

Com `DEBUG = False`, o debug toolbar não carrega. **Isso é obrigatório para medir.**

**5. Rodar o teste de carga.** Com o servidor de pé em um terminal, abra **outro terminal**, ative o ambiente virtual e rode:

```
locust -f locustfile.py --headless -u 10 -r 2 -t 3m -H http://127.0.0.1:8000 --csv relatorios/v0_10u
```

O que cada parte significa:

| Parâmetro | Significado |
|---|---|
| `--headless` | Sem interface gráfica (é o modo que dá para repetir igual) |
| `-u 10` | 10 usuários simultâneos |
| `-r 2` | Cria 2 usuários por segundo até chegar aos 10 |
| `-t 3m` | Roda por 3 minutos |
| `--csv relatorios/v0_10u` | Salva os relatórios em arquivos CSV com esse nome |

Ao terminar, ele imprime uma tabela com **tempo médio**, **mediana**, **percentil 95** e **requisições por segundo**. Os mesmos números ficam no arquivo `relatorios/v0_10u_stats.csv`.

> **O que é o percentil 95 (p95)?** É o tempo abaixo do qual ficaram 95% dos acessos. Se o p95 é 2 segundos, significa que 95 de cada 100 pessoas esperaram menos de 2 segundos, e 5 esperaram mais. A **média** esconde essa cauda: ela pode ser boa mesmo com algumas pessoas esperando muito. É por isso que o p95 sempre aparece junto.

**6. O protocolo de medição — escreva em `docs/protocolo.md` e siga igualzinho todas as vezes:**

1. base **grande** carregada (`popular_base --volume grande`);
2. `DEBUG = False`, debug toolbar desligado;
3. servidor Waitress/Gunicorn rodando (nunca `runserver`);
4. fechar navegador, música, jogo e tudo mais que estiver pesado na máquina;
5. rodar 1 minuto "de aquecimento" e **descartar** esse resultado — a primeira execução é sempre mais lenta, porque o banco ainda não tem nada em memória;
6. depois, rodar a medição de verdade por 3 minutos;
7. repetir **3 vezes** cada cenário;
8. cenários: **10 usuários** e **50 usuários**;
9. anotar: consultas por requisição, tempo médio, mediana, p95, requisições por segundo e número de erros.

**7. A planilha de medições.** Crie `docs/medicoes.csv` (ou uma planilha no Drive) com estas colunas:

```
data,versao,usuarios,repeticao,consultas,tempo_medio_ms,mediana_ms,p95_ms,req_por_seg,erros,observacao
```

Preencha uma linha por rodada. São 2 cenários × 3 repetições = **6 linhas** para a V0 nesta sprint.

**8. Uma limitação que você precisa declarar no artigo:** o Locust e a aplicação estão rodando na **mesma máquina** e disputam processador. Isso deixa os tempos absolutos piores do que seriam em um servidor de verdade. O que salva o trabalho é que essa limitação é **igual para todas as versões** — e o que você está comparando é V1 contra V0, não o número absoluto. Escreva exatamente isso.

### Como saber que deu certo

- [ ] `docs/protocolo.md` escrito.
- [ ] O teste imprime o número de consultas da V0.
- [ ] O Locust roda e gera os arquivos CSV.
- [ ] 6 linhas de medição da V0 na planilha.
- [ ] Print do painel SQL do debug toolbar e do resultado do Locust em `docs/evidencias/`.

### Erros comuns

- **Locust dá erro de conexão:** o servidor não está de pé, ou está em outra porta.
- **Tempos absurdamente diferentes entre as 3 repetições:** tem outro programa pesado aberto, ou você esqueceu o aquecimento. Fale com o orientador antes de seguir — resolver isso agora é mais barato do que na Sprint 8.
- **Debug toolbar aparecendo durante o teste de carga:** `DEBUG` ainda está `True`.

---

# Sprint 4 — 13/10 a 19/10/2026
## V1: buscar os dados relacionados de uma vez (`select_related`)

**Objetivo:** eliminar o problema N+1 e medir o quanto isso rendeu.

### O que você vai fazer

1. Escrever a view V1.
2. Conferir que ela mostra exatamente o mesmo que a V0.
3. Contar as consultas da V1.
4. Rodar a bateria de medições da V1.
5. Comparar com a V0.

### Passo a passo

**1. O que é `select_related`.** Quando você escreve `turma.curso.nome`, o Django vai ao banco naquele instante buscar o curso. Dentro de um laço, isso vira uma consulta por volta. O `select_related` avisa o Django, **antes** do laço, que você vai precisar desses dados — e ele traz tudo de uma vez só, com um `JOIN`.

```python
def listar_v1(request):
    """V1 - usa select_related para evitar o N+1 dos relacionamentos."""
    turmas = (Turma.objects
              .filter(situacao="aberta")
              .select_related("curso", "curso__eixo", "campus"))

    dados = []
    for turma in turmas:
        inscritos = Inscricao.objects.filter(turma=turma).count()
        dados.append({
            "curso": turma.curso.nome,
            "eixo": turma.curso.eixo.nome,
            "campus": turma.campus.nome,
            "turno": turma.get_turno_display(),
            "carga_horaria": turma.curso.carga_horaria,
            "data_inicio": turma.data_inicio,
            "vagas": turma.vagas,
            "inscritos": inscritos,
            "restantes": turma.vagas - inscritos,
        })

    return render(request, "catalogo/listagem.html",
                  {"dados": dados, "versao": "V1"})
```

Repare em três coisas:

- `"curso__eixo"` com dois sublinhados: significa "o eixo **do** curso". Sem isso, `turma.curso.eixo.nome` continuaria indo ao banco a cada volta;
- a contagem de inscritos **continua igual** por enquanto. Ela é o assunto da V3. Aqui você muda **uma coisa só**, que é o jeito certo de fazer um experimento;
- o resto do código é idêntico ao da V0. Copie e altere só a primeira linha.

**2. Registre a rota** em `catalogo/urls.py`:

```python
path("v1/", views.listar_v1, name="listar_v1"),
```

**3. Conferir que V0 e V1 mostram o mesmo.** Otimização que muda o resultado não é otimização, é defeito. O jeito mais simples de conferir: abra as duas páginas no navegador, lado a lado, e compare. Depois automatize com um teste simples:

```python
def test_v0_e_v1_mostram_o_mesmo(self):
    r0 = self.client.get(reverse("catalogo:listar_v0"))
    r1 = self.client.get(reverse("catalogo:listar_v1"))
    # remove o nome da versao, que e a unica diferenca esperada
    self.assertEqual(
        r0.content.replace(b"V0", b"X"),
        r1.content.replace(b"V1", b"X"),
    )
```

**Guarde esse teste.** Ele vai valer para a V2, a V3 e a V4 também — é só acrescentar os casos.

**4. Contar as consultas da V1.** Copie o teste de contagem da Sprint 3, trocando a URL. Com 20 turmas, a V0 fazia cerca de 80 consultas; a V1 deve fazer cerca de 21 (uma para a lista + uma por turma para contar os inscritos). **Anote os dois números.**

**5. Ver o SQL que o Django gerou.** Abra a V1 com o debug toolbar (`DEBUG = True`, `runserver`) e olhe na aba SQL: agora há uma consulta grande, com `JOIN`. Copie essa consulta e a da V0 e salve em `docs/evidencias/sql_v0.txt` e `sql_v1.txt`. O contraste entre as duas é uma figura excelente para o artigo.

**6. Medir.** Edite o `locustfile.py` para apontar para `/cursos/v1/`, volte `DEBUG = False`, suba o servidor e rode a bateria: 2 cenários × 3 repetições. Anote as 6 linhas na planilha.

**Dica para facilitar:** dá para medir as duas versões no mesmo locustfile, usando duas tarefas. Mas, se preferir, rode uma de cada vez — é mais simples de entender e de anotar.

**7. Anote a comparação** em `docs/resultados.md`: consultas de V0 e V1, tempo médio de V0 e V1, p95 de V0 e V1, e quantos por cento melhorou.

### Como saber que deu certo

- [ ] `/cursos/v1/` abre e mostra exatamente o mesmo conteúdo da V0.
- [ ] O teste de comparação V0 = V1 passa.
- [ ] O número de consultas caiu bastante.
- [ ] 6 linhas de medição da V1 na planilha.
- [ ] SQL das duas versões salvo em `docs/evidencias/`.

### Erros comuns

- **O número de consultas não caiu:** você esqueceu o `curso__eixo`, ou o template está acessando algum campo que não foi incluído no `select_related`.
- **As páginas ficaram diferentes:** provavelmente a ordem das turmas mudou. Acrescente `.order_by("data_inicio", "id")` nas duas views, para garantir ordem igual.

---

# Sprint 5 — 20/10 a 26/10/2026
## V2: criar índices no banco de dados

**Objetivo:** fazer o banco encontrar as turmas abertas sem varrer a tabela inteira, e medir.

### O que você vai fazer

1. Ver, no MySQL, como a consulta está sendo executada hoje.
2. Criar a view V2 (código igual ao da V1).
3. Criar os índices.
4. Ver a mesma consulta depois dos índices.
5. Medir de novo **todas** as versões.

### Passo a passo

**1. O que é um índice.** É como o índice remissivo no fim de um livro. Sem ele, para achar todas as turmas com `situacao = "aberta"`, o banco lê as 1.000 linhas da tabela uma por uma. Com um índice nessa coluna, ele vai direto.

**2. Ver o que o banco está fazendo hoje.** Primeiro descubra qual SQL o Django gera. No `python manage.py shell`:

```python
from catalogo.models import Turma
qs = Turma.objects.filter(situacao="aberta").order_by("data_inicio")
print(qs.query)
```

Copie o SQL que aparecer, abra o MySQL Workbench e rode com `EXPLAIN` na frente:

```sql
EXPLAIN SELECT ... ;
```

Olhe duas colunas do resultado:

- **`type`**: se estiver `ALL`, o banco está lendo a tabela inteira;
- **`key`**: se estiver `NULL`, nenhum índice está sendo usado.

**Tire um print dessa saída.** Ela é o "antes".

**3. Criar a view V2.** O código é **idêntico** ao da V1 — copie e troque só o nome e o `"versao": "V2"`. O que muda nesta sprint não é o código, é o banco. Registre a rota `v2/`.

**4. Criar os índices.** Em `catalogo/models.py`, acrescente à classe `Turma`:

```python
class Turma(models.Model):
    # ... os campos ...

    class Meta:
        indexes = [
            models.Index(fields=["situacao"], name="idx_turma_situacao"),
            models.Index(fields=["data_inicio"], name="idx_turma_data_inicio"),
        ]
```

Depois:

```
python manage.py makemigrations
python manage.py migrate
```

> **Não precisa criar índice para as chaves estrangeiras** (`curso`, `campus`, `turma`). O Django já cria automaticamente um índice para todo `ForeignKey`. Confira no Workbench antes de criar algo repetido.

**5. Ver o "depois".** Rode o mesmo `EXPLAIN` de novo. Agora a coluna `key` deve mostrar o nome do seu índice, e `type` não deve mais ser `ALL`. Tire outro print.

**6. Medir o custo do índice.** Índice não é de graça: ele ocupa espaço e deixa as escritas um pouco mais lentas. Mostre isso, porque a maioria dos trabalhos só mostra o lado bom. No Workbench:

```sql
SELECT table_name, data_length, index_length
FROM information_schema.tables
WHERE table_schema = 'ific';
```

Anote o `index_length` **antes** e **depois** de criar os índices (rode a consulta antes de aplicar a migração, se ainda der tempo; se já aplicou, anote o valor atual e compare com o tempo de carga). Anote também quanto tempo o `popular_base --volume grande` leva agora, comparado com o que você anotou na Sprint 2.

**7. Atenção metodológica — leia com calma.** O índice fica no banco, então ele acelera **todas as versões**, não só a V2. Por isso, nesta sprint você precisa **rodar a bateria de medições de novo para a V0, a V1 e a V2**.

Parece trabalho repetido, mas é só rodar o mesmo comando do Locust três vezes mais. E é o que permite você apresentar no artigo uma tabela honesta:

| Versão | Tempo médio sem índices | Tempo médio com índices |
|---|---|---|
| V0 | ... | ... |
| V1 | ... | ... |
| V2 | — | ... |

Se você simplesmente comparasse a V2 de hoje com a V1 da semana passada, estaria dando à sua otimização um crédito que não é todo dela.

### Como saber que deu certo

- [ ] Prints do `EXPLAIN` antes e depois salvos.
- [ ] Migração dos índices aplicada.
- [ ] Tabela "sem índices × com índices" montada, com V0, V1 e V2.
- [ ] Espaço ocupado pelos índices anotado.
- [ ] Teste de comparação entre as versões ainda passando.

### Erros comuns

- **O `EXPLAIN` não mudou nada:** pode ser que a tabela seja pequena demais e o MySQL tenha decidido que ler tudo é mais rápido. Confirme que você está com a base **grande** carregada.
- **Migração falha dizendo que o índice já existe:** você criou na mão pelo Workbench e depois pelo Django. Escolha um caminho só — use o Django.

---

# Sprint 6 — 27/10 a 02/11/2026
## V3: deixar o banco contar os inscritos

**Objetivo:** tirar a última consulta que ainda roda dentro do laço.

### O que você vai fazer

1. Escrever a view V3 usando `annotate`.
2. Conferir que os números continuam certos.
3. Contar as consultas.
4. Medir.

### Passo a passo

**1. O problema que ainda existe.** Na V1 e na V2, isto continua dentro do laço:

```python
inscritos = Inscricao.objects.filter(turma=turma).count()
```

São 500 consultas para 500 turmas. O banco sabe contar sozinho, e faz isso muito melhor.

**2. A solução: `annotate` com `Count`.** O `annotate` acrescenta uma coluna calculada ao resultado da consulta — como se fosse um campo extra que o banco preencheu:

```python
from django.db.models import Count


def listar_v3(request):
    """V3 - o banco conta os inscritos, com annotate."""
    turmas = (Turma.objects
              .filter(situacao="aberta")
              .select_related("curso", "curso__eixo", "campus")
              .annotate(total_inscritos=Count("inscricao"))
              .order_by("data_inicio", "id"))

    dados = []
    for turma in turmas:
        dados.append({
            "curso": turma.curso.nome,
            "eixo": turma.curso.eixo.nome,
            "campus": turma.campus.nome,
            "turno": turma.get_turno_display(),
            "carga_horaria": turma.curso.carga_horaria,
            "data_inicio": turma.data_inicio,
            "vagas": turma.vagas,
            "inscritos": turma.total_inscritos,
            "restantes": turma.vagas - turma.total_inscritos,
        })

    return render(request, "catalogo/listagem.html",
                  {"dados": dados, "versao": "V3"})
```

Agora `turma.total_inscritos` já vem pronto do banco. O laço não vai mais ao banco nenhuma vez — ele só monta o dicionário.

O cálculo de `restantes` continua em Python, mas isso **não custa nada**: é uma subtração em memória, sem ida ao banco. Não confunda "fazer no Python" com "ir ao banco" — o problema nunca foi a conta, foi a viagem.

**3. Conferir que os números batem.** Esta é a parte que exige cuidado. Escreva um teste que compara o valor anotado com a contagem feita na mão, para algumas turmas:

```python
def test_contagem_do_annotate_esta_certa(self):
    turma = Turma.objects.filter(situacao="aberta").first()
    esperado = Inscricao.objects.filter(turma=turma).count()

    anotada = (Turma.objects
               .filter(pk=turma.pk)
               .annotate(total=Count("inscricao"))
               .first())

    self.assertEqual(anotada.total, esperado)
```

**Por que esse cuidado?** Porque quando uma consulta junta mais de uma tabela "de muitos", o `Count` pode contar repetido e devolver um número maior do que o real. No seu caso provavelmente não vai acontecer, porque só há uma relação desse tipo. Mas se acontecer, a correção é `Count("inscricao", distinct=True)` — e o fato de você ter encontrado isso vira um parágrafo muito bom nos Resultados, porque é um erro silencioso: não quebra nada, só entrega número errado.

**4. Contar as consultas.** Rode o teste de contagem. A V3 deve fazer **1 ou 2 consultas, independentemente do número de turmas**. Esta é a propriedade importante: não é só ser um número menor, é ser um número que **não cresce** quando a base cresce. Destaque isso no artigo.

**5. Medir.** Mesma bateria de sempre: 2 cenários × 3 repetições, anotadas na planilha.

**6. Rode também o teste de comparação** entre V0, V1, V2 e V3. Todas têm de mostrar exatamente a mesma coisa.

### Como saber que deu certo

- [ ] `/cursos/v3/` abre e mostra o mesmo que as anteriores.
- [ ] O teste que confere a contagem passa.
- [ ] A V3 faz pouquíssimas consultas, e esse número não muda se você carregar mais turmas.
- [ ] 6 linhas de medição da V3 na planilha.
- [ ] Tabela acumulada V0 → V3 em `docs/resultados.md`.

### Erros comuns

- **Número de inscritos veio maior do que o real:** é o caso da contagem repetida. Use `distinct=True` e **registre o achado**.
- **`Count("inscricao")` dá erro:** o nome é o do modelo em minúsculas. Se você deu um `related_name` ao `ForeignKey`, use o `related_name`.

---

# Sprint 7 — 03/11 a 09/11/2026
## V4: guardar o resultado pronto no Redis (cache)

**Objetivo:** não refazer a consulta a cada acesso, e garantir que o dado guardado nunca fique desatualizado.

### O que você vai fazer

1. Instalar o Redis.
2. Configurar o cache no Django.
3. Escrever a V4 guardando o resultado no cache.
4. Fazer o cache se limpar quando algo mudar.
5. Medir com cache vazio e com cache cheio.

### Passo a passo

**1. Instalar o Redis (sem Docker).** O Redis não tem instalador oficial para Windows. As duas opções, escolha uma **com o orientador**:

- **Linux (ou WSL2 no Windows):** `sudo apt install redis-server`. Para conferir: `redis-cli ping` deve responder `PONG`. No Windows, o WSL2 se instala com `wsl --install` no PowerShell como administrador, e depois você usa o terminal do Ubuntu;
- **Windows direto:** instale o **Memurai**, que é compatível com o Redis e roda como serviço do Windows (tem edição gratuita para desenvolvedores). O Django enxerga como se fosse Redis.

Anote qual você usou — vai para Materiais e Métodos.

**2. Configurar no Django.**

```
pip install django-redis
```

Em `config/settings.py`:

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
    }
}
```

Teste se está funcionando, no `python manage.py shell`:

```python
from django.core.cache import cache
cache.set("teste", "funcionou", 60)
cache.get("teste")      # tem que imprimir 'funcionou'
```

Se isso funcionar, a parte difícil acabou.

**3. Escrever a V4.** A ideia é simples: antes de fazer a consulta, olhe se o resultado já está guardado. Se estiver, use. Se não estiver, calcule e guarde.

```python
from django.core.cache import cache

CHAVE_CACHE = "listagem_cursos_abertos"


def listar_v4(request):
    """V4 - guarda o resultado pronto no Redis."""
    dados = cache.get(CHAVE_CACHE)

    if dados is None:
        # nao estava no cache: calcula (igual a V3) e guarda
        turmas = (Turma.objects
                  .filter(situacao="aberta")
                  .select_related("curso", "curso__eixo", "campus")
                  .annotate(total_inscritos=Count("inscricao"))
                  .order_by("data_inicio", "id"))

        dados = []
        for turma in turmas:
            dados.append({
                "curso": turma.curso.nome,
                # ... os mesmos campos da V3 ...
            })

        cache.set(CHAVE_CACHE, dados, timeout=300)   # guarda por 5 minutos

    return render(request, "catalogo/listagem.html",
                  {"dados": dados, "versao": "V4"})
```

Guarde **listas de dicionários** no cache, não objetos do Django. É mais simples e evita problemas.

**4. Limpar o cache quando algo mudar — esta é a parte séria.**

O cache guarda uma **cópia** do resultado. Se alguém cadastrar uma inscrição nova e a cópia não for atualizada, o candidato vai ver "10 vagas restantes" em uma turma que já lotou. Isso não é um detalhe técnico: é informação errada para uma pessoa real.

A solução mais simples é usar *signals*: o Django avisa quando um registro é salvo ou apagado, e você aproveita para limpar o cache. Crie `catalogo/signals.py`:

```python
from django.db.models.signals import post_save, post_delete
from django.dispatch import receiver
from django.core.cache import cache

from .models import Turma, CursoFIC, Inscricao


@receiver([post_save, post_delete], sender=Turma)
@receiver([post_save, post_delete], sender=CursoFIC)
@receiver([post_save, post_delete], sender=Inscricao)
def limpar_cache_da_listagem(sender, **kwargs):
    cache.delete("listagem_cursos_abertos")
```

E registre em `catalogo/apps.py`:

```python
class CatalogoConfig(AppConfig):
    name = "catalogo"

    def ready(self):
        from . import signals      # noqa
```

Repare que são **três** modelos, não um só: mudar o nome do curso muda a listagem; criar uma inscrição muda as vagas restantes. Pensar em quais mudanças afetam a página é parte do trabalho.

**5. Medir com cache vazio e com cache cheio — os dois números.**

- **Cache vazio (frio):** limpe o Redis antes (`redis-cli FLUSHDB`, ou `cache.clear()` no shell) e meça. A primeira requisição paga o custo cheio **mais** o custo de gravar no cache;
- **Cache cheio (quente):** acesse a página uma vez para preencher, e só então rode o Locust.

Apresentar só o número quente seria enganoso. Registre os dois e explique a diferença no artigo.

**6. Opcional, se sobrar tempo:** existe um jeito ainda mais simples de cachear, que é guardar a página HTML inteira:

```python
from django.views.decorators.cache import cache_page

@cache_page(300)
def listar_v4b(request):
    ...
```

Se der tempo, faça e compare com a V4. É uma comparação interessante: mais simples de escrever, mais rápido ainda, mas menos controlável. Se não der tempo, deixe como trabalho futuro no artigo.

### Como saber que deu certo

- [ ] `redis-cli ping` responde `PONG`.
- [ ] `/cursos/v4/` abre e mostra o mesmo conteúdo das outras versões.
- [ ] O segundo acesso é visivelmente mais rápido que o primeiro.
- [ ] Alterar as vagas de uma turma pelo Admin e recarregar a página mostra o valor novo.
- [ ] Medições com cache frio e quente anotadas na planilha.

### Erros comuns

- **`ConnectionError` ao acessar a página:** o Redis não está rodando.
- **A página não atualiza depois de mudar algo no Admin:** o `signals.py` não está sendo carregado. Confira o `ready()` no `apps.py`.
- **`TypeError: Object of type Turma is not JSON serializable`:** você está tentando guardar objetos do Django no cache. Guarde dicionários.

---

# Sprint 8 — 10/11 a 16/11/2026
## Bateria final, conferência e documentação

**Objetivo:** rodar tudo de novo, do zero, de uma vez só; conferir que o cache não entrega dado velho; e deixar tudo documentado.

### O que você vai fazer

1. Testar os casos de atualização do cache.
2. Rodar a bateria final completa.
3. Montar as tabelas e os gráficos.
4. Escrever o `README.md`.
5. Montar a apresentação.

### Passo a passo

**1. Testar se o cache se atualiza.** Escreva um teste para cada situação:

```python
from django.test import TestCase, override_settings
from django.core.cache import cache

@override_settings(CACHES={"default": {
    "BACKEND": "django.core.cache.backends.locmem.LocMemCache"}})
class CacheTest(TestCase):

    def setUp(self):
        cache.clear()

    def test_mudar_vagas_aparece_na_pagina(self):
        self.client.get(reverse("catalogo:listar_v4"))   # enche o cache
        turma = Turma.objects.first()
        turma.vagas = 999
        turma.save()
        resposta = self.client.get(reverse("catalogo:listar_v4"))
        self.assertContains(resposta, "999")
```

Cubra, no mínimo, estes quatro casos:

| Caso | O que fazer no teste |
|---|---|
| Alterar uma turma | mudar `vagas` e conferir que a página mostra o novo valor |
| Alterar um curso | mudar o `nome` do curso e conferir que aparece |
| Criar uma inscrição | criar e conferir que "restantes" diminuiu |
| Apagar uma turma | apagar e conferir que sumiu da listagem |

**Se algum falhar, não esconda.** Corrija se der tempo e, de toda forma, **relate no artigo**. Um trabalho que mostra onde o cache falha é mais útil do que um que finge que ele é perfeito.

> Repare no `@override_settings` acima: ele faz o teste usar um cache em memória, em vez do Redis de verdade. Isso evita que o teste bagunce o cache da aplicação. E o `cache.clear()` no `setUp` garante que um teste não interfira no outro.

**2. A bateria final.** Agora você roda tudo de novo, na mesma tarde, na mesma máquina:

- base grande recarregada (`popular_base --volume grande`);
- 5 versões × 2 cenários (10 e 50 usuários) × 3 repetições = **30 rodadas** de 3 minutos.

Parece muito, mas é o mesmo comando repetido, trocando a URL e o número de usuários. Reserve uma tarde inteira e deixe rodando. **É esta bateria que vai para o artigo**; as medições anteriores ficam como histórico.

Uma dica que economiza tempo: escreva um arquivo `.bat` (Windows) ou `.sh` (Linux) com os 30 comandos em sequência, e deixe rodando sozinho.

**3. Montar as tabelas.** A tabela principal do artigo é esta, uma para cada cenário de usuários:

| Versão | Consultas | Tempo médio (ms) | p95 (ms) | Req/s | Melhora sobre a V0 |
|---|---|---|---|---|---|
| V0 | | | | | — |
| V1 | | | | | |
| V2 | | | | | |
| V3 | | | | | |
| V4 | | | | | |

Preencha com a **média das 3 repetições** e anote também o desvio padrão, para mostrar que as medições foram estáveis.

**4. Montar os gráficos.** Use o Google Sheets ou o Excel mesmo — não precisa de script. Faça três:

- barras: tempo médio por versão;
- barras: p95 por versão;
- barras: consultas por requisição por versão.

Cuidados: coloque a unidade no eixo (ms, req/s); se o eixo vertical não começar no zero, avise na legenda; e use o mesmo padrão de cores nos três.

**5. Escrever o `README.md` da sua subpasta.** Ele tem de permitir que outra pessoa repita tudo. Precisa conter:

- o que é o projeto e a que trabalho ele pertence;
- o que instalar (Python, MySQL, Redis, com as versões);
- como criar o banco (`CREATE DATABASE ific ...`);
- como configurar o `settings_local.py` a partir do arquivo de exemplo;
- como instalar as dependências (`pip install -r requirements.txt`);
- como popular a base (`python manage.py popular_base --volume grande`);
- o que é cada uma das cinco URLs;
- como rodar os testes;
- como subir o servidor no modo de medição (o comando do Waitress/Gunicorn);
- como rodar o Locust;
- onde estão as medições e os resultados.

**6. Revisar o código.** Confira que as cinco views estão com nomes padronizados, que cada uma tem o comentário dizendo qual otimização ela representa, e que não sobrou código morto.

**7. Montar a apresentação** (8 a 10 slides): o problema, o que foi construído, como foi medido, a tabela principal, os gráficos, o que deu certo, o que deu errado.

### Como saber que deu certo

- [ ] Os quatro testes de atualização do cache rodaram, com o resultado de cada um documentado.
- [ ] Bateria final completa rodada e anotada.
- [ ] Tabelas e gráficos prontos.
- [ ] `README.md` permite que outra pessoa repita o trabalho.
- [ ] Subpasta limpa: sem `.venv`, sem `settings_local.py`, sem relatórios pesados.
- [ ] `git log --stat` não mostra nenhum arquivo fora da sua subpasta.
- [ ] Apresentação montada.

---

## Quadro-resumo das sprints

| Sprint | Período | O que entrega | O que aprende |
|---|---|---|---|
| 1 | 22/09 a 28/09 | Projeto Django com MySQL e os modelos | instalação, configuração, modelagem |
| 2 | 29/09 a 05/10 | Base de dados e a página V0 (lenta) | `Faker`, `bulk_create`, o problema N+1 |
| 3 | 06/10 a 12/10 | **Saber medir** e os números da V0 | debug toolbar, Locust, p95, protocolo |
| 4 | 13/10 a 19/10 | V1 – `select_related` | carregar relacionamentos de uma vez |
| 5 | 20/10 a 26/10 | V2 – índices | `EXPLAIN`, índice e seu custo |
| 6 | 27/10 a 02/11 | V3 – `annotate` | deixar o banco fazer a conta |
| 7 | 03/11 a 09/11 | V4 – cache com Redis | cache e atualização do cache |
| 8 | 10/11 a 16/11 | Bateria final e documentação | análise dos dados, reprodutibilidade |

---

## Se algo der errado no cronograma

| Problema | O que fazer |
|---|---|
| MySQL não instala ou não conecta | Chame o orientador **na primeira semana**. Não empurre para a semana seguinte |
| Carga da base grande demora demais | Desenvolva com a base pequena e use a grande só nas medições |
| Medições muito diferentes entre as repetições | Feche todos os outros programas e refaça. Se continuar, fale com o orientador **na Sprint 3** |
| Redis não instala de jeito nenhum | Use o cache em memória do Django (`LocMemCache`) para desenvolver e **declare no artigo** que a medição do cache não pôde ser feita com Redis |
| A Sprint 7 atrasou | Entregue a V4 com uma estratégia só de cache e coloque as outras como trabalho futuro |

**Se precisar cortar algo, corte quantidade, não qualidade.** Três otimizações bem medidas valem mais do que quatro medidas de qualquer jeito. O que **não** pode faltar é o protocolo de medição e a comparação honesta entre as versões.

---

## Se sobrar tempo (opcional)

- **E1.** Testar também o cache de página inteira (`cache_page`) e comparar com a V4.
- **E2.** Medir com 100 usuários simultâneos, além de 10 e 50.
- **E3.** Testar um índice composto `(situacao, data_inicio)` e comparar com os dois índices separados.
- **E4.** Medir também o tempo de resposta com a base pequena, para mostrar que o problema **não aparece** quando há poucos dados — o que é exatamente o motivo de ele passar despercebido em desenvolvimento.

---

## Relação com o artigo

O desenvolvimento e a escrita andam juntos (ver `01_davi_ific_tarefas_escrita.md`):

| Seção do artigo | De onde vem o conteúdo |
|---|---|
| Referencial Teórico | as leituras que você faz nas Sprints 3 a 7 |
| Metodologia | o protocolo da Sprint 3 e a ideia das cinco versões |
| Materiais e Métodos | Sprints 1, 2 e 3 (ferramentas, versões, base, máquina) |
| Resultados | Sprints 4 a 7 (cada otimização) e 8 (bateria final) |
| Conclusão | o `docs/diario.md` das oito sprints |

**Nunca apague uma medição da planilha.** Rodada estranha vira observação no artigo, não lixo. A confiabilidade do seu trabalho está inteira nesse arquivo.
