# FIND - Plano de Desenvolvimento (Ciclo 1) - Alan Bezerra

- **Estudante:** Alan Bezerra - Curso Superior de Tecnologia em Sistemas para Internet 
- **Orientação:** Prof. Bruno Gomes - NIC
- **Período:** 28/09/2026 a 13/11/2026 - 7 *sprints* de 1 semana (segunda a sexta)
- **Projeto:** FIND - plataforma web (Django) em https://github.com/gabryellgs/projeto-find
- **Temática:** avaliação e correção da acessibilidade da plataforma web do FIND segundo a WCAG 2.2 e o eMAG.

> **Leia este documento inteiro antes de começar a Sprint 1.** Ele diz *o que* fazer, *como* fazer e *o que precisa estar pronto* ao final de cada semana. O documento complementar, com as orientações de escrita do TCC, é `01_alan_Find_tarefas_escrita.md`.

---

## Sumário

- [1. A ideia do trabalho](#1-a-ideia-do-trabalho)
- [2. O que será entregue](#2-o-que-será-entregue)
- [3. Estado atual do código](#3-estado-atual-do-código)
- [4. Fluxo de trabalho no repositório](#4-fluxo-de-trabalho-no-repositório)
- [5. Ambiente de trabalho](#5-ambiente-de-trabalho)
- [6. Rotina das sprints](#6-rotina-das-sprints)
- [7. Sprints](#7-sprints)
- [8. Definição de pronto](#8-definição-de-pronto-vale-para-todas-as-sprints)
- [9. Riscos e planos B](#9-riscos-e-planos-b)
- [10. Trabalhos futuros (Ciclo 2)](#10-trabalhos-futuros-ciclo-2)
- [11. Checklist de encerramento](#11-checklist-de-encerramento)

---

## 1. A ideia do trabalho

Acessibilidade digital é garantir que **pessoas com deficiência consigam usar um sistema** - quem navega só pelo teclado, quem usa leitor de tela, quem tem baixa visão ou daltonismo, quem precisa ampliar a tela. No Brasil, isso não é só boa prática: a **Lei Brasileira de Inclusão (Lei nº 13.146/2015, art. 63)** torna obrigatória a acessibilidade dos sítios mantidos por órgãos de governo e por empresas com sede no País, e o **eMAG** (Modelo de Acessibilidade em Governo Eletrônico) é a referência para sistemas de instituições públicas - como o IFRN, onde o FIND nasceu.

**A ideia em uma frase:**

> Avaliar a conformidade da plataforma web do FIND com a WCAG 2.2 (níveis A e AA) e com o eMAG, usando ferramentas automáticas e uma inspeção por teclado, corrigir as barreiras encontradas e medir a diferença entre o antes e o depois.

**Por que isso é um bom trabalho:**

- **Tem método claro e repetível.** Mesma amostra de páginas, mesmas ferramentas, mesmo protocolo, aplicados duas vezes: antes e depois das correções;
- **Produz números.** Violações por página, por critério e por ferramenta; pontuação do Lighthouse; índice do ASES; itens aprovados no *checklist* de teclado;
- **É trabalho de desenvolvimento web que você já sabe fazer:** HTML, CSS e *templates* Django. A diferença é que cada alteração tem uma justificativa normativa (o critério da WCAG que ela atende);
- **Deixa o FIND melhor de verdade**, e as correções entram direto no repositório principal.

**Recorte deste ciclo:** a **plataforma web**, nas páginas públicas e nas páginas do **usuário comum** (ver amostra na Tarefa 1.4). Os painéis de bolsista, de administrador e de IoT e o aplicativo móvel ficam para o Ciclo 2 (seção 10).

**Perguntas de pesquisa:**

- **QP1:** qual é o nível de conformidade da plataforma web do FIND com os critérios A e AA da WCAG 2.2 e com as recomendações do eMAG, e quais são as barreiras mais frequentes?
- **QP2:** quais barreiras cada ferramenta automática detecta, e quais só aparecem na inspeção por teclado?
- **QP3:** qual foi o efeito das correções aplicadas sobre os indicadores de acessibilidade?

> **A QP2 é a que tem maior potencial de achado original.** A literatura já mostra que as ferramentas automáticas detectam só uma parte das barreiras e que elas discordam entre si. Mostrar isso com dados de um sistema real, com uma tabela de "quem encontrou o quê", é exatamente o tipo de resultado que interessa a um congresso da área.

---

## 2. O que será entregue

1. **Protocolo de avaliação** escrito (amostra de páginas, ferramentas, versões, configurações e *checklist* de teclado), fixado **antes** da primeira avaliação.
2. **Comando de dados fictícios** (`popular_dados_avaliacao`), para que a avaliação rode sempre sobre o mesmo conteúdo, sem dados reais de usuários.
3. **Script de avaliação automática** com o axe-core (`acessibilidade/avaliar_axe.py`), que avalia todas as páginas da amostra e grava os resultados em JSON e CSV.
4. **Planilha de barreiras** - cada barreira com página, critério WCAG, recomendação eMAG, ferramenta que a detectou, impacto, evidência e situação (corrigida ou não).
5. **Correções aplicadas** nos *templates* e no CSS do FIND, com commits identificados pelo código da barreira.
6. **Avaliação "depois"** com o mesmo protocolo, **tabela comparativa** e **gráficos**.
7. **README da pasta `acessibilidade/`**, explicando como reproduzir cada tabela e cada gráfico.
8. **TCC completo** (ver documento de escrita).

---

## 3. Estado atual do código

Pontos levantados na leitura do repositório em 25/09/2026 (último commit analisado: `e2f364a`, de 11/09/2026). **Eles não são o seu diagnóstico:** servem para você saber onde olhar. O diagnóstico oficial do TCC é o que as ferramentas e o *checklist* encontrarem na Sprint 3, com o protocolo aplicado.

**O que já está bom** (e deve ser citado no TCC - avaliação honesta mostra também o que já atende):

| Fato | Onde |
|---|---|
| Idioma da página declarado (`lang="pt-br"`) | `templates/base.html:3`, `index.html`, `login.html`, `register.html` |
| Todas as imagens (`<img>`) dos *templates* têm atributo `alt` | todos os *templates* |
| Há um `<main>` envolvendo o conteúdo das páginas que herdam de `base.html` | `templates/base.html:397` |
| O botão de mostrar senha já tem `aria-label` e `aria-pressed` | `login.html:108` |
| Abas dos painéis já usam `role="tab"`, `aria-selected` e `aria-controls` | `bolsista_dashboard.html`, `admin_dashboard.html` |
| Houve ajustes de contraste anteriores na barra de navegação e nas cores | commits `b6754bd` (15/06/2026) e `d8ea5d1` (06/07/2026) |

**Onde provavelmente estão as barreiras:**

| Ponto de atenção | Critério WCAG relacionado | Onde |
|---|---|---|
| Regra `*:focus { outline: none; }` remove o indicador de foco de **todos** os elementos (existe uma exceção `.keyboard-nav`; verifique se ela funciona) | 2.4.7 Foco visível | `login.css:614`, `register.css:588` |
| `outline: none` em campos e botões de várias telas | 2.4.7 Foco visível | `navbar.css:171`, `menu.css`, `chats.css`, `item_list.css`, `item_edit.css`, `modal-item.css`, entre outros |
| Não existe link "Pular para o conteúdo" | 2.4.1 Ignorar blocos | `templates/base.html` |
| A barra de navegação é fixa no topo (`position: sticky`) e pode cobrir o elemento que recebe foco ao navegar por Tab | 2.4.11 Foco não encoberto (novo na 2.2) | `navbar.css:32` |
| 17 *templates* de página não têm nenhum `<h1>` | 1.3.1 Informações e relações; 2.4.6 Cabeçalhos e rótulos | `item_detail.html`, `register_item.html`, `chats_list.html`, `chat_detail.html`, `user.html`, `visual_search.html`, entre outros |
| Campos de formulário sem `<label for>` associado (confira se há rótulo envolvendo o campo ou `aria-label`) | 1.3.1; 3.3.2 Rótulos ou instruções; 4.1.2 Nome, função, valor | `register_item.html`, `edit_profile.html`, `menu.html`, `chats_list.html`, `chat_detail.html` |
| Campo de busca identificado apenas pelo `placeholder` | 3.3.2; 4.1.2 | `menu.html:118` |
| Ícones SVG decorativos nos links da navegação sem `aria-hidden="true"` | 1.1.1 Conteúdo não textual | `templates/base.html` (menu) |
| Muitas cores definidas em `style="..."` direto no HTML - atenção: corrigir contraste nesses pontos exige editar o *template*, e não só o CSS | 1.4.3 Contraste mínimo | `menu.html` (59 ocorrências), `user.html` (54), entre outros |
| Área de envio de imagem com arrastar e soltar | 2.5.7 Movimentos de arrastar (novo na 2.2) - verifique se há alternativa por clique | `visual_search.html`, `register_item.html` |
| Mensagens do chat chegam sem recarregar a página | 4.1.3 Mensagens de status | `chat_detail.html` |

---

## 4. Fluxo de trabalho no repositório

Você trabalha **direto na *branch* `main`** do `projeto-find`. Como outras pessoas também fazem commits nela, siga estas regras:

1. **Sempre atualize antes de começar e antes de enviar:**
   ```
   git pull
   ```
2. **Commits pequenos**, um por correção (ou por grupo pequeno de correções da mesma barreira). Isso permite desfazer uma correção sem perder as outras.
3. **Mensagens no padrão *Conventional Commits*, com o código da barreira** entre colchetes (os códigos saem da planilha de barreiras, Tarefa 3.4):
   ```
   feat(a11y): adiciona link "Pular para o conteúdo" no base.html [B01]
   fix(a11y): restaura indicador de foco visível no login e no cadastro [B02]
   fix(a11y): associa rótulos aos campos do cadastro de item [B07]
   test(a11y): adiciona script de avaliação com axe-core
   docs(a11y): documenta o protocolo de avaliação
   ```
4. **Antes de cada `git push`:** rode `pytest` (os testes existentes precisam continuar passando) e abra no navegador as páginas que você alterou.
5. **Nunca use `git push --force`.** Se algo der errado, desfaça com `git revert <hash>`.
6. **Marque os dois momentos da avaliação com *tags*.** Elas são a evidência de qual versão foi avaliada em cada rodada:
   ```
   git tag -a a11y-antes -m "Versão avaliada antes das correções"
   git push origin a11y-antes
   ```
   (a `a11y-depois` é criada na Sprint 7).

---

## 5. Ambiente de trabalho

**Sistema:** Windows, sem Docker. Tudo o que for biblioteca é instalado via `pip`, dentro do ambiente virtual.

**Projeto rodando localmente** (segue o README do FIND). Em desenvolvimento local o FIND usa **SQLite** automaticamente e dispensa o Redis:

```
git clone https://github.com/gabryellgs/projeto-find
cd projeto-find
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
pip install python-magic-bin
```

Crie o arquivo `.env` na raiz:

```
SECRET_KEY=chave-local-qualquer
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
```

```
python manage.py migrate
python manage.py criar_categorias
python manage.py collectstatic --noinput
python manage.py runserver
```

**Bibliotecas da avaliação** - ficam em um arquivo **separado**, `acessibilidade/requirements-avaliacao.txt`, para **não** entrarem no `requirements.txt` que o servidor de produção instala:

```
faker
playwright
axe-playwright-python
pandas
matplotlib
openpyxl
```

```
pip install -r acessibilidade/requirements-avaliacao.txt
```

O Playwright vai usar o **Edge ou o Chrome já instalados** no computador (parâmetro `channel`), então não é preciso baixar outro navegador.

**Ferramentas no navegador** (todas gratuitas):

| Ferramenta | O que é | Como usar |
|---|---|---|
| **axe DevTools** | Extensão do Chrome/Edge (versão gratuita), da Deque, baseada no axe-core | Aba "axe DevTools" no DevTools (F12) → *Scan all of my page* |
| **WAVE** | Extensão do Chrome/Edge, da WebAIM | Ícone da extensão na página aberta |
| **Lighthouse** | Já vem no Chrome e no Edge | DevTools (F12) → aba *Lighthouse* → marcar só "Acessibilidade" |
| **ASES Web** | Avaliador do governo brasileiro, baseado no **eMAG** | Site do ASES Web; para páginas que exigem login, use a avaliação por **código-fonte** (Ctrl+U na página, copiar e colar) |
| **Contrast Checker** (WebAIM) | Página web que calcula a razão de contraste entre duas cores | Para conferir cada cor que você for trocar |

---

## 6. Rotina das sprints

- **Segunda-feira:** leia as tarefas da *sprint* neste documento e anote as dúvidas.
- **Durante a semana:** trabalhe nas tarefas e faça commits pequenos.
- **Sexta-feira:** entrega da *sprint* - mensagem ao orientador com: o que foi feito, *links* dos commits, prints (antes e depois, quando houver correção) e o que ficou pendente.
- **Toda semana:** atualize a planilha de barreiras. Ela é a base dos Resultados do TCC; se ficar desatualizada, você vai reconstruí-la de memória na hora de escrever.

---

## 7. Sprints

| *Sprint* | Período | Foco |
|---|---|---|
| 1 | 28/09 a 02/10 | Ambiente, estudo das normas, ferramentas e amostra de páginas |
| 2 | 05/10 a 09/10 | Dados fictícios, script do axe e protocolo de avaliação |
| 3 | 12/10 a 16/10 | Avaliação "antes" e planilha de barreiras |
| 4 | 19/10 a 23/10 | Priorização e correções globais (`base.html` e CSS comum) |
| 5 | 26/10 a 30/10 | Correções de formulários, rótulos e imagens |
| 6 | 02/11 a 06/11 | Correções de contraste, títulos, alvos de toque e mensagens dinâmicas |
| 7 | 09/11 a 13/11 | Avaliação "depois", comparação, gráficos e documentação |

---

### Sprint 1 - Ambiente, normas, ferramentas e amostra (28/09 a 02/10/2026)

**Objetivo:** ter o FIND rodando, conhecer as normas e as ferramentas, e definir quais páginas serão avaliadas.

#### Tarefa 1.1 - FIND rodando localmente

Siga a seção 5. Crie um superusuário (`python manage.py createsuperuser`) e cadastre um item pela interface para confirmar que tudo funciona.

**Pronto quando:** você consegue entrar, cadastrar um item, vê-lo na lista e abrir o detalhe.

#### Tarefa 1.2 - Estudar a WCAG 2.2 e o eMAG

Não é para ler tudo de ponta a ponta. Faça assim:

1. Leia a **visão geral da WCAG** no site da W3C/WAI e entenda os **quatro princípios** (perceptível, operável, compreensível e robusto), os **níveis** (A, AA e AAA) e o que é um **critério de sucesso**;
2. Abra a **referência rápida da WCAG 2.2** (*How to Meet WCAG - Quick Reference*), filtre pelos níveis **A e AA** e leia o enunciado de cada critério. Para os que parecerem obscuros, abra o documento *Understanding WCAG 2.2* do critério;
3. Dê atenção especial aos **critérios novos da versão 2.2** nos níveis A e AA: 2.4.11 (Foco não encoberto), 2.5.7 (Movimentos de arrastar), 2.5.8 (Tamanho do alvo - mínimo), 3.2.6 (Ajuda consistente), 3.3.7 (Entrada redundante) e 3.3.8 (Autenticação acessível - mínimo). Eles são pouco estudados em trabalhos brasileiros, e o FIND tem pelo menos três deles em jogo (barra fixa, arrastar imagem e tela de login);
4. Leia o **eMAG 3.1** - são 45 recomendações em seis seções (Marcação, Comportamento, Conteúdo/Informação, Apresentação/Design, Multimídia e Formulário). Perceba que ele é baseado na WCAG 2.0: boa parte das recomendações tem um critério WCAG correspondente.

**Entrega:** uma tabela (planilha) com os critérios A e AA da WCAG 2.2 - número, nome, nível e, quando houver, a recomendação eMAG correspondente. Ela será usada para classificar cada barreira e vai virar um quadro do Referencial.

#### Tarefa 1.3 - Conhecer as ferramentas

Instale as extensões **axe DevTools** e **WAVE** e rode as quatro ferramentas (axe, WAVE, Lighthouse e ASES Web) na **página inicial** do FIND. Para cada uma, anote:

- o nome e a **versão** (aparece nas configurações da extensão ou no rodapé do relatório);
- o que ela informa (quantidade de erros? alertas? pontuação? percentual?);
- como ela agrupa os problemas (por regra, por critério WCAG, por recomendação eMAG).

> **Atenção com o Lighthouse:** rode-o em uma **janela anônima**, sem extensões ativas (as extensões interferem no resultado), no modo "Navegação", dispositivo **Desktop** e somente a categoria **Acessibilidade**.

**Entrega:** um quadro "ferramenta × o que mede × unidade × versão". Ele entra em Materiais e Métodos.

#### Tarefa 1.4 - Definir a amostra de páginas

A amostra são as páginas que serão avaliadas **antes e depois**. Ela precisa cobrir os principais fluxos do usuário comum e todos os tipos de componente (formulário, lista, detalhe, chat, *upload*). Use esta:

| ID | Página | URL | Exige login |
|---|---|---|---|
| P01 | Página inicial | `/` | não |
| P02 | Entrar | `/login/` | não |
| P03 | Cadastro de usuário | `/register/` | não |
| P04 | Redefinir senha | `/redefinir-senha/` | não |
| P05 | Início (menu) | `/menu/` | sim |
| P06 | Itens perdidos | `/itens/perdidos/` | sim |
| P07 | Detalhe do item | `/item/<slug>/` | sim |
| P08 | Cadastrar item | `/perfil/item/novo/` | sim |
| P09 | Meus chats | `/chats/` | sim |
| P10 | Conversa | `/chats/<id>/` | sim |
| P11 | Perfil do usuário | `/tela/` | sim |
| P12 | Busca visual | `/itens/busca-visual/` | sim |

A escolha segue a ideia da **WCAG-EM** (a metodologia de avaliação de conformidade da W3C): uma **amostra estruturada**, com as páginas mais usadas e com pelo menos uma página de cada tipo. Leia a etapa 3 da WCAG-EM ("Select a Representative Sample") - você vai citar isso na Metodologia.

**Entrega:** o arquivo `acessibilidade/paginas.csv` (as URLs da P07 e da P10 são preenchidas na Sprint 2, depois de gerar os dados fictícios):

```
id,nome,url,requer_login
P01,Página inicial,/,nao
P02,Entrar,/login/,nao
...
```

---

### Sprint 2 - Dados fictícios, script do axe e protocolo (05/10 a 09/10/2026)

**Objetivo:** deixar a avaliação **automática e repetível**, para que a rodada "depois" seja feita exatamente como a rodada "antes".

#### Tarefa 2.1 - Comando de dados fictícios

A avaliação não pode depender do que você cadastrou à mão: as páginas precisam ter **o mesmo conteúdo** nas duas rodadas (itens com e sem foto, uma conversa com mensagens). E **nunca** use dados reais de usuários do FIND (LGPD).

Crie `items/management/commands/popular_dados_avaliacao.py`. Ponto de partida:

```python
import io
import random
from datetime import date, timedelta

from django.conf import settings
from django.contrib.auth import get_user_model
from django.core.files.base import ContentFile
from django.core.management.base import BaseCommand, CommandError
from faker import Faker
from PIL import Image, ImageDraw

from chats.models import Chat, Mensagem
from items.models import Categoria, Item

OBJETOS = [
    "Garrafa térmica azul", "Carregador de celular", "Óculos de grau",
    "Mochila preta", "Chaveiro com três chaves", "Casaco cinza",
    "Fone de ouvido sem fio", "Carteira marrom", "Calculadora científica",
    "Guarda-chuva", "Caderno de anotações", "Crachá de estudante",
]
LOCAIS = ["Biblioteca", "Bloco A - Sala 3", "Cantina", "Laboratório 2", "Quadra", "Auditório"]
SENHA = "Avaliacao@2026"


def gerar_imagem(texto):
    """Cria uma imagem simples com o nome do objeto, para testar o texto alternativo."""
    imagem = Image.new("RGB", (640, 480), (random.randint(40, 200), 120, 160))
    ImageDraw.Draw(imagem).text((40, 220), texto, fill="white")
    buffer = io.BytesIO()
    imagem.save(buffer, format="JPEG")
    return ContentFile(buffer.getvalue())


class Command(BaseCommand):
    help = "Cria usuários, itens e uma conversa fictícios para a avaliação de acessibilidade."

    def handle(self, *args, **options):
        if not settings.DEBUG:
            raise CommandError("Use este comando apenas no ambiente local (DEBUG=True).")

        fake = Faker("pt_BR")
        Faker.seed(2026)
        random.seed(2026)
        User = get_user_model()

        usuarios = []
        for nome in ["avaliadora", "visitante"]:
            usuario, _ = User.objects.get_or_create(
                username=nome, defaults={"email": f"{nome}@example.com"}
            )
            usuario.set_password(SENHA)
            usuario.save()
            usuarios.append(usuario)
        avaliadora, visitante = usuarios

        categorias = list(Categoria.objects.all())
        data_base = date(2026, 10, 1)  # data fixa: o conteúdo não muda de uma rodada para outra

        for indice, objeto in enumerate(OBJETOS, start=1):
            # O slug é informado aqui porque o save() do Item gera um slug
            # com sufixo aleatório - e a URL da página P07 precisa ser sempre a mesma.
            item, _ = Item.objects.update_or_create(
                slug=f"avaliacao-{indice:02d}",
                defaults={
                    "titulo": objeto,
                    "descricao": fake.text(max_nb_chars=150),
                    "status": "perdido" if indice % 2 else "achado",
                    "local": random.choice(LOCAIS),
                    "data": data_base - timedelta(days=indice),
                    "usuario": avaliadora,
                    "categoria": random.choice(categorias) if categorias else None,
                },
            )
            if indice % 3 and not item.imagem:  # dois terços dos itens com foto
                item.imagem.save(f"avaliacao_{indice:02d}.jpg", gerar_imagem(objeto), save=True)

        # TODO: com Chat.objects.get_or_create, criar (ou reaproveitar) uma conversa
        #       entre "visitante" (criado_por) e "avaliadora" (dono_item) sobre o item
        #       "avaliacao-01"; apagar as mensagens dela e recriar 4 mensagens,
        #       alternando o remetente. Assim o id da conversa não muda entre rodadas.

        # TODO: imprimir o id da conversa, para preencher o paginas.csv.
        self.stdout.write(self.style.SUCCESS("Dados fictícios criados."))
```

Complete os dois `TODO` (os campos de `Chat` e `Mensagem` estão em `chats/models.py`). Rode `python manage.py criar_categorias` antes. Depois, preencha o `paginas.csv`: a URL da P07 é `/item/avaliacao-01/`, e a da P10 usa o id que o comando imprimir.

**Pronto quando:** rodar o comando duas vezes seguidas deixa o banco no **mesmo estado** (mesmos itens, mesma conversa), e as 12 páginas da amostra abrem com conteúdo.

#### Tarefa 2.2 - Script de avaliação com o axe-core

As extensões são ótimas para **investigar** um problema, mas anotar resultados de 12 páginas à mão, duas vezes, gera erro de digitação. O script faz a parte repetitiva: abre cada página, roda o axe-core e grava o resultado.

Crie `acessibilidade/avaliar_axe.py`:

```python
"""Avalia as páginas da amostra com o axe-core e grava os resultados.

Uso (com o servidor rodando em outro terminal):
    python acessibilidade/avaliar_axe.py --rotulo antes
"""
import argparse
import csv
import json
from pathlib import Path

from axe_playwright_python.sync_playwright import Axe
from playwright.sync_api import sync_playwright

BASE_URL = "http://127.0.0.1:8000"
USUARIO = "avaliadora@example.com"
SENHA = "Avaliacao@2026"
TAGS_WCAG = ["wcag2a", "wcag2aa", "wcag21a", "wcag21aa", "wcag22aa"]
PASTA = Path(__file__).parent


def ler_paginas():
    with open(PASTA / "paginas.csv", encoding="utf-8") as arquivo:
        return list(csv.DictReader(arquivo))


def fazer_login(page):
    page.goto(f"{BASE_URL}/login/")
    page.fill('input[name="username"]', USUARIO)
    page.fill('input[name="password"]', SENHA)
    with page.expect_navigation():
        page.click("#btn-submit")


def criterios_wcag(tags):
    """Converte tags do axe como 'wcag143' em '1.4.3'."""
    return [".".join(t[4:]) for t in tags if t.startswith("wcag") and t[4:].isdigit()]


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument("--rotulo", required=True, help="antes ou depois")
    args = parser.parse_args()

    destino = PASTA / "resultados" / args.rotulo
    destino.mkdir(parents=True, exist_ok=True)
    axe = Axe()
    linhas = []

    with sync_playwright() as p:
        navegador = p.chromium.launch(channel="msedge")  # ou channel="chrome"
        for pagina in ler_paginas():
            # Contexto novo por página: mesmo estado inicial (banner de cookies visível)
            contexto = navegador.new_context(
                bypass_csp=True, viewport={"width": 1366, "height": 768}
            )
            page = contexto.new_page()
            if pagina["requer_login"] == "sim":
                fazer_login(page)
            page.goto(BASE_URL + pagina["url"], wait_until="load")
            page.wait_for_timeout(1500)  # tempo para o JavaScript da página terminar

            resultado = axe.run(page, options={"runOnly": {"type": "tag", "values": TAGS_WCAG}})
            dados = resultado.response
            (destino / f"{pagina['id']}.json").write_text(
                json.dumps(dados, ensure_ascii=False, indent=2), encoding="utf-8"
            )
            for violacao in dados["violations"]:
                linhas.append({
                    "pagina": pagina["id"],
                    "regra": violacao["id"],
                    "impacto": violacao["impact"],
                    "criterios": " ".join(criterios_wcag(violacao["tags"])),
                    "ocorrencias": len(violacao["nodes"]),
                    "descricao": violacao["help"],
                })
            print(f"{pagina['id']}: {len(dados['violations'])} regras violadas")
            contexto.close()
        navegador.close()

    with open(destino / "resumo.csv", "w", newline="", encoding="utf-8") as arquivo:
        escritor = csv.DictWriter(arquivo, fieldnames=linhas[0].keys())
        escritor.writeheader()
        escritor.writerows(linhas)
    print(f"Versão do axe-core: {dados['testEngine']['version']}")


if __name__ == "__main__":
    main()
```

Entenda **duas unidades de contagem** do axe, porque elas vão aparecer no TCC:

- **regra violada** (`violations`): por exemplo, "`color-contrast`" - conta uma vez por página;
- **ocorrências** (`nodes`): quantos elementos da página violam aquela regra - um botão com contraste ruim repetido em 20 cartões dá 20 ocorrências.

As duas medidas contam histórias diferentes, e o TCC apresenta as duas.

> Se a biblioteca mudar algum nome (por exemplo, o atributo `response`), consulte a documentação da versão instalada (`pip show axe-playwright-python`). Anote a versão da biblioteca e a do axe-core que o script imprime: as duas vão para Materiais e Métodos.

**Pronto quando:** `python acessibilidade/avaliar_axe.py --rotulo teste` gera os 12 JSON e o `resumo.csv`. Apague a pasta `resultados/teste` depois.

#### Tarefa 2.3 - *Checklist* de inspeção por teclado

As ferramentas automáticas **não conseguem** verificar boa parte do que envolve interação: se o foco aparece, se a ordem faz sentido, se dá para sair de um menu. Isso você verifica **usando só o teclado** (Tab, Shift+Tab, Enter, Espaço, setas e Esc), sem tocar no mouse.

Monte o *checklist* em planilha, com uma coluna por página e uma linha por item, marcando **Atende / Não atende / Não se aplica**:

| # | Verificação | Critério WCAG |
|---|---|---|
| K1 | Todos os links, botões e campos são alcançados com Tab | 2.1.1 Teclado |
| K2 | Nenhum componente "prende" o foco (menus, modais, banner de cookies) | 2.1.2 Sem bloqueio do teclado |
| K3 | A ordem do foco segue a ordem visual e lógica da página | 2.4.3 Ordem do foco |
| K4 | O elemento com foco tem um indicador visível | 2.4.7 Foco visível |
| K5 | O elemento com foco não fica escondido atrás da barra de navegação fixa ou do banner | 2.4.11 Foco não encoberto |
| K6 | Existe um mecanismo para pular direto ao conteúdo principal | 2.4.1 Ignorar blocos |
| K7 | Menus suspensos e modais abrem com Enter/Espaço e fecham com Esc | 2.1.1 Teclado |
| K8 | Componentes próprios (mostrar senha, abas, *upload*, filtros) funcionam pelo teclado | 2.1.1 Teclado; 2.5.7 Movimentos de arrastar |
| K9 | Com *zoom* de 200% no navegador, nada fica cortado ou sobreposto | 1.4.4 Redimensionar texto |
| K10 | Com a janela em 320 px de largura (DevTools, modo dispositivo), não há rolagem horizontal | 1.4.10 Refluxo |
| K11 | O título da aba do navegador identifica a página | 2.4.2 Página com título |

Escreva também **como** cada item é verificado (por exemplo, K5: "navegar com Tab até o fim da página e observar se algum elemento focado fica sob a barra superior").

#### Tarefa 2.4 - Protocolo de avaliação

Um documento curto, `acessibilidade/PROTOCOLO.md`, que **congela** as regras antes da primeira avaliação:

- a amostra (`paginas.csv`) e os dados (`popular_dados_avaliacao`);
- as ferramentas, com versões e configurações (Tarefa 1.3);
- a ordem de execução em cada página: script do axe (todas as páginas de uma vez) → WAVE → Lighthouse → ASES Web → *checklist* de teclado;
- o navegador e a resolução (Edge ou Chrome, 1366 × 768);
- **o que conta como uma barreira** (ver Tarefa 3.4) e como resultados repetidos de ferramentas diferentes são unificados.

> **Por que isso importa:** se o protocolo mudar entre o "antes" e o "depois", a comparação perde o valor. Escrever antes é o que permite afirmar, no TCC, que a diferença medida vem das correções.

**Entrega da Sprint 2:** comando de dados, script do axe, `paginas.csv` completo, *checklist* e protocolo commitados em `acessibilidade/`.

---

### Sprint 3 - Avaliação "antes" e planilha de barreiras (12/10 a 16/10/2026)

**Objetivo:** aplicar o protocolo completo e transformar os resultados em uma lista única de barreiras.

#### Tarefa 3.1 - Congelar a versão avaliada

```
git pull
git tag -a a11y-antes -m "Versão avaliada antes das correções"
git push origin a11y-antes
```

Recrie o banco de avaliação (`python manage.py popular_dados_avaliacao`) e não mexa mais nele até o fim da rodada.

#### Tarefa 3.2 - Rodar as ferramentas

1. `python acessibilidade/avaliar_axe.py --rotulo antes`;
2. **WAVE** em cada página: anote *Errors*, *Contrast Errors* e *Alerts*, e salve um print do painel;
3. **Lighthouse** em cada página (janela anônima, Desktop, só Acessibilidade): anote a pontuação (0 a 100) e os itens reprovados; salve o relatório em HTML (menu ⋮ do relatório → *Save as HTML*) em `acessibilidade/resultados/antes/lighthouse/`;
4. **ASES Web** em cada página: páginas públicas pela URL do Render ou pelo código-fonte; páginas com login, sempre pelo código-fonte. Anote o **percentual** e os erros e avisos por seção do eMAG;
5. **Checklist de teclado** em cada página.

Organize tudo em uma planilha `acessibilidade/resultados/antes/indicadores.xlsx`, com uma linha por página e uma coluna por indicador.

#### Tarefa 3.3 - Investigar com o axe DevTools

Para cada regra que o script apontou, abra a página, rode o **axe DevTools** e clique em *Highlight* para ver **qual elemento** tem o problema. Localize o elemento no *template* (`Ctrl+Shift+F` no VS Code, procurando pela classe ou pelo texto) e anote **arquivo e linha**. Sem isso, você não sabe o que corrigir.

#### Tarefa 3.4 - Planilha de barreiras

Ferramentas diferentes apontam o mesmo problema com nomes diferentes (o axe diz `color-contrast`, o WAVE diz *Very low contrast*, o ASES cita a recomendação 4.1 do eMAG). A planilha **unifica** tudo em barreiras:

| Coluna | Exemplo |
|---|---|
| ID | B02 |
| Descrição | Indicador de foco removido em todos os elementos |
| Critério WCAG (nº, nome, nível) | 2.4.7 Foco visível (AA) |
| Recomendação eMAG | 4.4 - Possibilitar que o elemento com foco seja visualmente evidente |
| Páginas afetadas | P02, P03 |
| Escopo | Local (CSS da página) / Global (`base.html` ou CSS comum) |
| Arquivo e linha | `login.css:614`, `register.css:588` |
| Detectada por | axe / WAVE / Lighthouse / ASES / Teclado (marque todas que detectaram) |
| Impacto (axe) | crítico / sério / moderado / menor - ou "não se aplica" se só o teclado detectou |
| Evidência | nome do print |
| Situação | Aberta / Corrigida (commit) / Não corrigida (justificativa) |

**Regra de unificação:** uma barreira = **um problema de um mesmo componente, em um mesmo critério**. Se o mesmo problema vem do `base.html` e aparece nas 12 páginas, é **uma** barreira global, que afeta 12 páginas - e não 12 barreiras.

> A coluna "Detectada por" é o que responde à **QP2**. Preencha com cuidado: ela vai virar a tabela mais interessante do seu TCC.

**Entrega da Sprint 3:** *tag* `a11y-antes`, resultados em `acessibilidade/resultados/antes/` e planilha de barreiras preenchida.

---

### Sprint 4 - Priorização e correções globais (19/10 a 23/10/2026)

**Objetivo:** corrigir primeiro o que está no `base.html` e no CSS comum, porque cada correção ali melhora **todas** as páginas de uma vez.

#### Tarefa 4.1 - Priorizar

Ordene a planilha por: (1) barreiras que **impedem** o uso (impacto crítico ou "não atende" em K1, K2 ou K4); (2) barreiras **globais**; (3) número de páginas afetadas; (4) impacto do axe. Registre a ordem - ela vira um parágrafo da Metodologia ("critério de priorização").

#### Tarefa 4.2 - Link "Pular para o conteúdo"

No `base.html`, como **primeiro** elemento dentro do `<body>`:

```html
<a href="#conteudo-principal" class="pular-conteudo">Pular para o conteúdo</a>
```

E no `<main>`: `<main id="conteudo-principal" tabindex="-1">`. No `base.css`, deixe o link invisível até receber foco:

```css
.pular-conteudo {
  position: absolute;
  left: -9999px;
}
.pular-conteudo:focus {
  left: 1rem;
  top: 1rem;
  z-index: 10000;
  padding: .75rem 1rem;
  background: #0B0F1A;
  color: #fff;
}
```

Faça o mesmo nas páginas que **não** herdam do `base.html` (`index.html`, `login.html`, `register.html`).

#### Tarefa 4.3 - Foco visível em todo o site

1. Remova as regras `*:focus { outline: none; }` (`login.css`, `register.css`);
2. Em cada `outline: none` restante, verifique se existe **outro** indicador de foco no lugar (borda, sombra). Se não existir, crie;
3. Defina um estilo de foco comum no `base.css`, usando `:focus-visible` (aparece na navegação por teclado, e não no clique do mouse):

```css
:focus-visible {
  outline: 3px solid #0B5FFF;
  outline-offset: 2px;
}
```

Confira o contraste da cor do contorno com o fundo (mínimo 3:1, critério 1.4.11).

#### Tarefa 4.4 - Foco não encoberto pela barra fixa

Com a barra `sticky` no topo, um elemento que recebe foco pode ficar embaixo dela. No `base.css`:

```css
html {
  scroll-padding-top: 90px; /* ajuste para a altura real da barra */
}
```

Teste com o item K5 do *checklist*.

#### Tarefa 4.5 - Navegação e títulos das páginas

- Ícones decorativos dos links da navegação: `aria-hidden="true"` no `<svg>` e no `<i class="bi ...">`;
- Marque o link da página atual com `aria-current="page"` (onde hoje existe a classe `active`);
- Confira se todas as páginas da amostra têm um `{% block title %}` que identifique a página (critério 2.4.2).

**Entrega da Sprint 4:** commits das correções globais, cada um com o código da barreira, e a planilha atualizada.

---

### Sprint 5 - Formulários, rótulos e imagens (26/10 a 30/10/2026)

**Objetivo:** fazer cada campo, botão e imagem ter um **nome acessível** - é o que o leitor de tela anuncia.

#### Tarefa 5.1 - Rótulos dos campos

Todo campo visível precisa de um rótulo associado. A forma preferida é o `<label for>`:

```html
<label for="id_titulo">Nome do objeto</label>
<input id="id_titulo" name="titulo" type="text" required>
```

Quando o desenho da tela não tiver um rótulo visível (como a busca do menu), use um rótulo **visualmente oculto**, com a classe `visually-hidden` do Bootstrap:

```html
<label for="menuSearchInputMobile" class="visually-hidden">Buscar itens</label>
```

`placeholder` **não** é rótulo: ele desaparece quando a pessoa começa a digitar.

Arquivos prioritários: `register_item.html`, `edit_profile.html`, `menu.html`, `chats_list.html`, `chat_detail.html`, `item_list.html`, `my_itens.html`.

#### Tarefa 5.2 - Mensagens de erro e campos obrigatórios

- Campos obrigatórios: atributo `required` (ou `aria-required="true"`) **e** indicação visual que não dependa só de cor;
- Mensagens de erro ligadas ao campo com `aria-describedby`, para o leitor de tela ler o erro junto com o rótulo:

```html
<input id="id_email" aria-describedby="erro-email" aria-invalid="true">
<p id="erro-email" class="texto-erro">Informe um e-mail válido.</p>
```

- Nos campos de dados pessoais do cadastro e do perfil, use `autocomplete` (`name`, `email`, `tel`, `new-password`, `current-password`) - critério 1.3.5;
- Na tela de login, confirme que **colar a senha** e usar o **gerenciador de senhas** do navegador funcionam (critério 3.3.8, novo na 2.2).

#### Tarefa 5.3 - Botões só com ícone

Todo botão que mostra apenas um ícone precisa de `aria-label` descrevendo a **ação**:

```html
<button type="button" class="btn-search-filter" aria-label="Filtrar itens" ...>
  <i class="bi bi-funnel-fill" aria-hidden="true"></i>
</button>
```

O atributo `title` sozinho não basta. Procure nos *templates* por `<button` seguido de apenas `<i` ou `<svg`.

#### Tarefa 5.4 - Texto alternativo das imagens

Todas as imagens já têm `alt`; agora confira a **qualidade** do texto:

- foto do item: `alt="{{ item.titulo }}"` (e não "imagem" ou "foto");
- logotipo que é link para a página inicial: `alt="FIND - página inicial"`;
- imagem puramente decorativa: `alt=""`.

#### Tarefa 5.5 - Arrastar e soltar

Nas áreas de *upload* (`visual_search.html`, `register_item.html`), confirme que existe um **botão** que abre a seleção de arquivo pelo teclado, além do arrastar. Se não existir, crie (critério 2.5.7).

**Entrega da Sprint 5:** commits e planilha atualizada. Rode o script do axe com `--rotulo parcial` para ver o progresso (não é resultado oficial; apague a pasta depois).

---

### Sprint 6 - Contraste, estrutura, alvos e mensagens dinâmicas (02/11 a 06/11/2026)

#### Tarefa 6.1 - Contraste de cores

Para cada barreira de contraste, meça as duas cores no **WebAIM Contrast Checker**. O mínimo é **4,5:1** para texto normal e **3:1** para texto grande e para componentes de interface. Troque a cor pela mais próxima que atinja o mínimo, mantendo a identidade visual.

- Se a cor está no CSS, crie uma **variável** (`--texto-secundario`) e use-a em todos os lugares;
- se está em `style="..."` no *template*, mova para uma classe CSS enquanto corrige - assim a cor não fica espalhada de novo.

Registre na planilha a cor antiga, a nova e as duas razões de contraste. Isso vira um quadro dos Resultados.

#### Tarefa 6.2 - Estrutura de títulos

Cada página precisa de **um** `<h1>` que diga do que ela trata e de uma hierarquia sem saltos (`h1` → `h2` → `h3`). Onde o texto é visualmente um título mas está em `<div>` ou `<p>`, troque pela *tag* correta e ajuste o CSS para manter a aparência. Use o painel *Structure* do WAVE para conferir.

#### Tarefa 6.3 - Tamanho dos alvos

Botões e links pequenos (ícones de ação, paginação, fechar) devem ter no mínimo **24 × 24 px** de área clicável (critério 2.5.8, novo na 2.2). O axe verifica isso na regra `target-size`. Ajuste com `min-width`, `min-height` ou `padding`.

#### Tarefa 6.4 - Mensagens dinâmicas

- **Chat:** a área onde as mensagens novas aparecem recebe `aria-live="polite"`, para que o leitor de tela anuncie a mensagem nova;
- **Mensagens do Django** (sucesso, erro): confira se o contêiner delas usa `role="status"` (sucesso) ou `role="alert"` (erro);
- **Banner de cookies:** confira K2 e K5 - ele não pode prender o foco nem encobrir o elemento focado.

#### Tarefa 6.5 - Barreiras que não serão corrigidas

Algumas barreiras podem ficar sem correção (por exemplo, dependem de biblioteca externa ou exigiriam refazer uma tela inteira). Para cada uma, escreva na planilha **por que** ficou e **o que seria preciso** para corrigi-la. Barreira remanescente justificada é resultado, e não falha.

**Entrega da Sprint 6:** todas as barreiras com situação "Corrigida" ou "Não corrigida (justificativa)".

---

### Sprint 7 - Avaliação "depois", comparação e documentação (09/11 a 13/11/2026)

#### Tarefa 7.1 - Avaliação "depois" (até quarta-feira, 11/11)

```
git pull
git tag -a a11y-depois -m "Versão avaliada depois das correções"
git push origin a11y-depois
python manage.py popular_dados_avaliacao
python acessibilidade/avaliar_axe.py --rotulo depois
```

Repita WAVE, Lighthouse, ASES Web e *checklist* de teclado **exatamente como no protocolo**, gravando em `acessibilidade/resultados/depois/`.

#### Tarefa 7.2 - Script de comparação e gráficos

Crie `acessibilidade/comparar.py` para ler os dois `resumo.csv` e gerar a tabela e os gráficos do TCC:

```python
import matplotlib.pyplot as plt
import pandas as pd
from pathlib import Path

PASTA = Path(__file__).parent / "resultados"

antes = pd.read_csv(PASTA / "antes" / "resumo.csv")
depois = pd.read_csv(PASTA / "depois" / "resumo.csv")


def por_pagina(dados, rotulo):
    return dados.groupby("pagina").agg(
        **{f"regras_{rotulo}": ("regra", "count"),
           f"ocorrencias_{rotulo}": ("ocorrencias", "sum")}
    )


tabela = por_pagina(antes, "antes").join(por_pagina(depois, "depois"), how="outer").fillna(0)
tabela.to_csv(PASTA / "comparacao_por_pagina.csv")
print(tabela)

tabela[["ocorrencias_antes", "ocorrencias_depois"]].plot(kind="bar", figsize=(10, 5))
plt.ylabel("Ocorrências de violação (axe-core)")
plt.xlabel("Página")
plt.tight_layout()
plt.savefig(PASTA / "grafico_ocorrencias_por_pagina.png", dpi=200)
```

Acrescente, no mesmo estilo: violações por **critério WCAG** (antes e depois), por **impacto** e a comparação das pontuações do Lighthouse e do ASES (a partir das planilhas `indicadores.xlsx`, com `pd.read_excel`).

> Uma página que não aparece no `resumo.csv` "depois" teve **zero** violações. O `fillna(0)` cuida disso - confira se a tabela mostra zero, e não "página sumida".

#### Tarefa 7.3 - README da avaliação

`acessibilidade/README.md` com: o que é a pasta; como instalar (`requirements-avaliacao.txt`); como gerar os dados; como rodar o script do axe; onde estão os resultados de cada rodada; e como gerar cada tabela e cada gráfico do TCC. Outra pessoa tem de conseguir refazer tudo só com ele.

**Entrega da Sprint 7:** *tag* `a11y-depois`, resultados, comparação, gráficos e README.

---

## 8. Definição de pronto (vale para todas as sprints)

- [ ] `pytest` passando;
- [ ] páginas alteradas abertas no navegador e conferidas com o mouse **e** com o teclado;
- [ ] commits pequenos, com mensagem no padrão e código da barreira;
- [ ] planilha de barreiras atualizada;
- [ ] prints de antes e depois de cada correção visível, salvos com o código da barreira no nome (`B02_antes.png`, `B02_depois.png`);
- [ ] mensagem de entrega enviada ao orientador na sexta-feira.

---

## 9. Riscos e planos B

| Risco | Plano B |
|---|---|
| O ASES Web está fora do ar no dia da avaliação | Registre a data e a tentativa, avalie no dia seguinte; se continuar fora do ar, siga com as outras três ferramentas e registre isso como limitação |
| O Playwright não abre o Edge | Troque para `channel="chrome"`; se nenhum funcionar, rode `python -m playwright install chromium` e remova o parâmetro `channel` |
| O script dá erro de *Content Security Policy* ao injetar o axe | Confira se o contexto foi criado com `bypass_csp=True` |
| Uma correção quebra o *layout* de outra tela | `git revert <hash>` do commit da correção, e refaça com mais cuidado |
| Outra pessoa altera um *template* da amostra entre o "antes" e o "depois" | Anote o commit na planilha. Na comparação, separe o que mudou por causa das suas correções. As *tags* permitem ver exatamente o que mudou (`git diff a11y-antes a11y-depois -- mainpage/templates`) |
| Barreiras demais para corrigir no prazo | Siga a priorização da Tarefa 4.1. As que sobrarem entram como "não corrigidas", com justificativa |

---

## 10. Trabalhos futuros (Ciclo 2)

- avaliação com **leitor de tela** (NVDA) em roteiros de tarefas completas (cadastrar item, iniciar conversa);
- **avaliação com usuários** que usam tecnologia assistiva;
- estender a avaliação aos **painéis** de bolsista, de administrador e de IoT;
- avaliar a acessibilidade do **aplicativo móvel** (React Native), com as diretrizes de acessibilidade para dispositivos móveis;
- colocar o script do axe em **integração contínua**, para impedir que novas barreiras entrem no código.

---

## 11. Checklist de encerramento

- [ ] *Tags* `a11y-antes` e `a11y-depois` publicadas no GitHub;
- [ ] pasta `acessibilidade/` com protocolo, *checklist*, `paginas.csv`, scripts, resultados das duas rodadas, comparação, gráficos e README;
- [ ] comando `popular_dados_avaliacao` funcionando;
- [ ] planilha de barreiras completa, sem nenhuma barreira com situação "Aberta";
- [ ] versões de todas as ferramentas anotadas;
- [ ] `pytest` passando na `main`;
- [ ] figuras do TCC (gráficos e prints) exportadas em boa resolução e guardadas na pasta `figuras/` do Drive.
