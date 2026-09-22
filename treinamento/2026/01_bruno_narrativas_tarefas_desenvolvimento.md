# Plano de tarefas de desenvolvimento – Bruno (Técnico Integrado em Informática)

**Projeto pai:** Narrativas – plataforma digital para registro, organização e difusão das narrativas populares do Rio Grande do Norte (ver [projeto.md](../projeto.md)).

**Temática escolhida:** 4.1 – Exportação de narrativas para folder em PDF (ver [tematicas.md](../tematicas.md)).

**Perfil do aluno:** 1 aluno do curso Técnico Integrado em Informática, com conhecimentos **básicos** em Python, em treinamento, **sem conhecimento de banco de dados**. Por isso este plano é detalhado de propósito, e o trabalho inteiro foi montado **sem banco de dados**: as narrativas ficam em arquivos de texto comuns.

**Duração:** 8 sprints de 1 semana (22/09/2026 a 16/11/2026).

---

## Como este documento funciona

Cada sprint tem quatro partes:

- **O que você vai entregar** — em uma frase, o que precisa estar funcionando no fim da semana;
- **Passo a passo** — a lista numerada do que fazer, na ordem. Siga na ordem, sem pular;
- **Como saber que deu certo** — o que você deve ver na tela ou no arquivo. Se não vir isso, ainda não terminou;
- **Entrega da sprint** — a lista de conferência para a reunião com o orientador.

**Regra de ouro:** cada sprint é pequena de propósito. Se terminar antes, **não comece a próxima**: use o tempo que sobrou para entender melhor o que fez e para escrever o artigo. O plano de escrita (`01_bruno_narrativas_tarefas_escrita.md`) anda em paralelo e é tão importante quanto o código.

**Travou mais de 40 minutos no mesmo erro? Pare e peça ajuda.** Isso não é desistir, é administrar o tempo. Mande a mensagem de erro **inteira**, copiada e colada, não um resumo dela.

---

## A ideia do trabalho, em uma página

Os protótipos de tela do portal Narrativas já preveem dois botões na página de cada narrativa: **"Baixar PDF"** e **"Material Didático"**. A ideia é que qualquer pessoa — um professor, um aluno, um agente cultural — consiga imprimir a narrativa em um **folder** bonito, pronto para levar para a sala de aula.

Só que **ninguém ainda decidiu como esse PDF vai ser gerado**. A plataforma não tem nenhuma biblioteca de PDF escolhida, e existem várias opções em Python, bem diferentes entre si.

A pergunta que este trabalho responde é:

> **Qual biblioteca Python é a mais adequada para gerar o folder de narrativas do projeto Narrativas?**

Para responder, você vai desenhar **um modelo de folder** e depois implementar **esse mesmo folder** em **três bibliotecas diferentes**, comparando:

| O que é comparado | Como se mede |
|---|---|
| **Fidelidade ao leiaute** | uma lista de conferência com 10 itens, comparando cada PDF com o modelo desenhado |
| **Tempo de geração** | cronometrar a criação dos folders, repetindo várias vezes |
| **Tamanho do arquivo** | o tamanho em KB de cada PDF gerado |
| **Acentuação** | verificar se "coração", "vovó" e "sertão" saem certos no PDF |
| **Imagens** | verificar se a imagem aparece, no lugar certo e sem deformar |
| **Texto pesquisável** | conseguir usar Ctrl+F no PDF e achar uma palavra — isso importa para acessibilidade |
| **Facilidade de instalação** | quantos passos foram necessários e se deu algum erro |
| **Tamanho do código** | quantas linhas de Python foram precisas para fazer o mesmo folder |

### O que este trabalho **não** é

**Não é "fazer o botão de PDF do site Narrativas".** A plataforma é o **contexto** que justifica a pergunta; o objeto do seu trabalho é a **comparação**. Escreva isso na Introdução do artigo — é o que separa um trabalho acadêmico de um manual de programa.

Também **não é** fazer o programa mais bonito possível. Os três programas precisam gerar **o mesmo folder**, para que a comparação seja justa.

---

## Decisões técnicas já fechadas

Para você não perder tempo escolhendo ferramenta:

| Item | Decisão |
|---|---|
| Linguagem | **Python 3** |
| Banco de dados | **nenhum.** As narrativas ficam em arquivos `.txt` |
| Bibliotecas comparadas | **FPDF2**, **ReportLab** e **xhtml2pdf** (mais uma quarta, a WeasyPrint, que é um caso à parte — veja a Sprint 5) |
| Leitura dos PDFs gerados | `pypdf` |
| Gráficos | `matplotlib` |
| Planilhas | módulo `csv`, que já vem com o Python |
| Editor | VS Code |
| Versionamento | Git, na sua subpasta dentro do repositório compartilhado |
| O que **não** entra | Docker, banco de dados, Django, front-end, inteligência artificial — tudo isso vira "trabalho futuro" no artigo |

**Tudo o que precisa ser instalado vem pelo `pip`**, porque as máquinas do laboratório não permitem instalar programas.

### Por que sem banco de dados?

Porque o objeto do trabalho é **gerar o PDF**, e não guardar as narrativas. Colocar um banco no meio acrescentaria semanas de trabalho e complexidade **sem mudar nenhum resultado** da comparação — as três bibliotecas receberiam exatamente os mesmos dados de qualquer forma.

**Isso não é uma falha do trabalho, é uma decisão de método**, e precisa estar escrita na Metodologia do artigo, com essa justificativa. Na plataforma de verdade os dados virão do banco; aqui eles vêm de arquivos, e para a comparação dá no mesmo.

### Três confirmações com o orientador, na primeira semana

1. **Git está instalado nas máquinas do laboratório?** Se não estiver, combine outra forma de entregar os arquivos (enviar pela página do GitHub, no navegador, funciona e não exige instalar nada).
2. **O `pip install` funciona?** Teste no primeiro dia. Se houver bloqueio ou proxy, isso precisa ser resolvido **na Sprint 1**, e não na semana em que você precisar entregar resultado.
3. **Você consegue abrir o repositório da plataforma**, mesmo que só para olhar? Vale muito a pena: os protótipos de tela em `temp/layout/` mostram como o folder deveria ser, e vão te ajudar a desenhar o modelo na Sprint 2.

---

## Onde o trabalho acontece

O **repositório de treinamento do projeto já existe** e é compartilhado com os outros alunos. Você **não cria repositório nenhum**. Todo o seu trabalho fica dentro de **uma única subpasta sua**:

```
<repositorio-de-treinamento>/
├── ...              ← pastas de outros alunos (não mexa)
└── bruno/           ← a sua subpasta: tudo o que você fizer fica aqui dentro
```

Confirme com o orientador o **endereço do repositório** e o **nome exato da sua subpasta** antes de começar. Todos os caminhos citados neste documento são **relativos à sua subpasta**.

### Regras do repositório compartilhado

1. **Só altere arquivos da sua subpasta.** Nunca edite, mova ou apague arquivo de outro aluno.
2. **Comece o dia com `git pull`.**
3. **Envie apenas o que é seu:** `git add bruno/` — nunca `git add .`. Confira com `git status` antes.
4. **Não envie** a pasta `.venv/` nem `__pycache__/`.
5. **Deu conflito (`CONFLICT`)? Pare e chame o orientador.** Conflito mal resolvido apaga o trabalho dos outros.
6. **Envie ao fim de cada dia.** Código que só existe na sua máquina não foi entregue.

---

## A estrutura de pastas que você vai construir

Você não precisa criar tudo de uma vez — cada sprint cria a sua parte. Esta é a figura final, para você saber onde está indo:

```
bruno/
├── narrativas/               ← as narrativas, um arquivo .txt cada (Sprint 2)
│   ├── 01_boitata.txt
│   ├── 02_lobisomem.txt
│   └── ...
├── imagens/                  ← as imagens de cada narrativa (Sprint 2)
├── modelo/                   ← o desenho do folder e a lista de conferência (Sprint 2)
│   ├── modelo_folder.png
│   └── checklist.md
├── geradores/
│   ├── ler_narrativas.py     ← lê os arquivos .txt (Sprint 2)
│   ├── gerar_fpdf2.py        ← Sprint 3
│   ├── gerar_reportlab.py    ← Sprint 4
│   └── gerar_xhtml2pdf.py    ← Sprint 5
├── saidas/                   ← os PDFs gerados (não vão para o Git)
├── medir.py                  ← Sprint 6
├── graficos.py               ← Sprint 7
├── resultados/
│   ├── medicoes.csv
│   └── fidelidade.csv
├── docs/
│   ├── ambiente.md
│   ├── diario.md
│   ├── instalacao.md
│   └── evidencias/           ← prints de tela
├── .gitignore
├── requirements.txt
└── README.md
```

---

## Combinados que valem para todas as sprints

- **Diário (`docs/diario.md`):** ao fim de cada sprint, escreva 3 linhas — o que funcionou, o que deu errado, o que aprendi. Leva cinco minutos e vai salvar a sua Conclusão daqui a dois meses.
- **Anote todo erro que aparecer.** Neste trabalho, **erro é resultado**. Se uma biblioteca engoliu um acento, deformou a imagem ou não instalou, isso vai para uma tabela do artigo. Guarde a mensagem de erro inteira.
- **Prints (`docs/evidencias/`):** sempre que algo funcionar (ou falhar de um jeito interessante), tire um print. Eles viram figuras do artigo.
- **Envios (*commits*):** pelo menos 2 por semana, com mensagem curta em português (`Adiciona gerador com FPDF2`). Mensagem `ajustes` não conta.
- **Reunião semanal:** no começo de cada sprint você mostra ao orientador o que fez, **rodando na tela**. A partir da Sprint 6, "está funcionando" não basta: tem que ter número.

---

# Sprint 1 — 22/09 a 28/09/2026
## Preparar o ambiente e gerar o primeiro PDF

**O que você vai entregar:** a sua subpasta criada, o Python com as bibliotecas instaladas, e um PDF de uma página que você gerou com Python e abriu na tela.

Esta sprint é curta de propósito. O objetivo é **eliminar todas as surpresas de ambiente agora**, e não na semana em que você precisar entregar resultado.

### Passo a passo

**1. Confirme o Python.** Abra o Prompt de Comando (tecle `Win`, digite `cmd`, Enter) e rode:

```
python --version
pip --version
```

Você deve ver algo como `Python 3.11.5` e uma linha do `pip`. Se aparecer "não é reconhecido como comando", chame o orientador antes de continuar. **Anote as duas versões em `docs/ambiente.md`.**

**2. Pegue o repositório.** Peça ao orientador o endereço e o acesso de escrita. Com o Git disponível:

```
git clone <endereco-do-repositorio>
cd <nome-do-repositorio>
mkdir bruno
cd bruno
```

Se o Git **não** estiver instalado, combine com o orientador a forma de entrega e siga em frente — não perca a semana nisso.

**3. Crie o ambiente virtual.** Dentro de `bruno/`:

```
python -m venv .venv
.venv\Scripts\activate
```

Depois de ativar, o começo da linha passa a mostrar `(.venv)`. **Se não mostrar, o ambiente não está ativo** e tudo o que você instalar vai para o lugar errado. Toda vez que abrir um Prompt novo, precisa ativar de novo.

> Se você estiver no PowerShell e aparecer erro de "execução de scripts desabilitada", use o Prompt de Comando (`cmd`), que não tem essa restrição.

**4. Instale as bibliotecas** — e **anote quantos segundos cada uma levou e se deu algum aviso**, porque "facilidade de instalação" é um dos itens que você vai comparar:

```
pip install fpdf2
pip install reportlab
pip install xhtml2pdf
pip install pypdf matplotlib
pip freeze > requirements.txt
```

Crie `docs/instalacao.md` e escreva, para cada biblioteca: o comando usado, se instalou de primeira, se apareceu algum aviso e quantos outros pacotes vieram junto (o `pip` mostra isso na linha `Installing collected packages:`). **Esse arquivo vira uma tabela do artigo.**

> Repare já numa diferença: a `xhtml2pdf` vai puxar vários pacotes junto (inclusive a própria ReportLab), enquanto a `fpdf2` vem quase sozinha. Anote o número — é um dado objetivo sobre o "peso" de cada opção.

**5. Crie a estrutura de pastas.** Ainda dentro de `bruno/`:

```
mkdir narrativas
mkdir imagens
mkdir modelo
mkdir geradores
mkdir saidas
mkdir resultados
mkdir docs
mkdir docs\evidencias
```

**6. Crie o `.gitignore`** dentro de `bruno/`, com este conteúdo:

```
.venv/
__pycache__/
*.pyc
saidas/
```

> Os PDFs gerados **não vão para o Git**: eles são criados de novo toda vez que você roda o programa. O que vai para o Git é o programa que os gera.

**7. Gere o seu primeiro PDF.** Crie o arquivo `teste_pdf.py`:

```python
from fpdf import FPDF

pdf = FPDF()
pdf.add_page()
pdf.set_font("Helvetica", "B", 20)
pdf.cell(0, 15, "Narrativas do Rio Grande do Norte",
         new_x="LMARGIN", new_y="NEXT", align="C")

pdf.set_font("Helvetica", size=12)
pdf.multi_cell(0, 8, "Teste de acentuação: coração, vovó, sertão, José, Iracema.")

pdf.output("saidas/teste.pdf")
print("PDF gerado em saidas/teste.pdf")
```

Rode com `python teste_pdf.py` e abra o arquivo `saidas/teste.pdf` (dê dois cliques — o Microsoft Edge abre PDF sem precisar instalar nada).

**8. Faça três verificações no PDF aberto** — elas já são um ensaio do que você vai fazer o trabalho inteiro:

- **os acentos saíram certos?** Olhe "coração", "vovó" e "sertão" com atenção;
- **dá para selecionar o texto com o mouse?** Se der, o texto é de verdade, e não uma imagem;
- **o Ctrl+F acha a palavra "sertão"?** Se achar, o PDF é pesquisável.

Anote as três respostas no diário. Tire um print e guarde em `docs/evidencias/`.

**9. Preencha `docs/ambiente.md`:** versão do Python, versão de cada biblioteca (o comando `pip list` mostra todas), e a configuração da máquina do laboratório — processador, memória RAM, sistema operacional. Isso vai para a seção Materiais e Métodos do artigo, e sem isso o trabalho não é reproduzível.

### Como saber que deu certo

- O arquivo `saidas/teste.pdf` existe e abre.
- Os acentos aparecem corretos.
- Você consegue selecionar o texto e achar "sertão" com Ctrl+F.

> **Se os acentos saírem errados ou der um erro com a palavra `UnicodeEncodeError`**, não se assuste: isso acontece quando o texto tem algum caractere fora do conjunto que a fonte padrão conhece (por exemplo, o travessão "—" ou as reticências "…"). **Anote o erro exato**, porque ele é um achado do trabalho, e veja a solução na Sprint 3.

### Entrega da sprint

- [ ] Subpasta `bruno/` criada no repositório, com as pastas.
- [ ] Ambiente virtual criado e as cinco bibliotecas instaladas.
- [ ] `requirements.txt` gerado e `.gitignore` criado.
- [ ] `docs/instalacao.md` com o registro da instalação de cada biblioteca.
- [ ] `teste_pdf.py` funcionando, com print do PDF em `docs/evidencias/`.
- [ ] `docs/ambiente.md` preenchido.
- [ ] As três confirmações (Git, `pip`, acesso aos protótipos) conversadas com o orientador.
- [ ] `docs/diario.md` criado, com as 3 linhas da semana.

---

# Sprint 2 — 29/09 a 05/10/2026
## O acervo de teste e o modelo do folder

**O que você vai entregar:** 10 narrativas em arquivos de texto, as imagens delas, o desenho do folder e um programinha em Python que lê tudo isso.

Esta é a base de todo o resto. **Comece pelas narrativas na segunda-feira.**

### Passo a passo

**1. Escolha 10 narrativas populares.** Elas precisam ser de **domínio público** ou de uso autorizado — você vai publicar um trabalho acadêmico com elas.

**Como saber se um texto é de domínio público, no Brasil:** pela Lei nº 9.610/1998, a obra entra em domínio público **70 anos depois de 1º de janeiro do ano seguinte à morte do autor**. Ou seja, autores que morreram até 1955 já estão em domínio público hoje. Bons lugares para procurar:

- o portal **Domínio Público** (`dominiopublico.gov.br`), do Ministério da Educação;
- coletâneas antigas de folclore brasileiro, como as de **Sílvio Romero** (morreu em 1914) e **Lindolfo Gomes** (morreu em 1953);
- a **Biblioteca Brasiliana** e o acervo digital da Biblioteca Nacional.

**Para cada narrativa, anote o autor, a obra, o ano e o endereço de onde você tirou.** Sem isso você não consegue escrever a Metodologia, e não pode usar o texto.

> **Converse com o orientador antes de fechar a lista.** As outras temáticas do projeto também precisam de textos de teste, e o ideal é que todos usem a mesma fonte. Isso está registrado como pendência em `tematicas.md`.

**Critérios para escolher as 10:**

- **tamanhos variados** — pelo menos duas curtas (menos de 1.000 caracteres), quatro médias e duas longas (mais de 4.000 caracteres). Isso é importante: o texto longo é o que vai fazer o folder passar de uma página, e é aí que as bibliotecas se diferenciam;
- **com bastante acentuação** — o que é fácil em português;
- se possível, **narrativas do Rio Grande do Norte ou do Nordeste**, para ficar coerente com o projeto.

**2. Salve cada narrativa em um arquivo `.txt`**, dentro de `narrativas/`, exatamente neste formato:

```
titulo: A Lenda do Boitatá
tipo: Lenda
origem: Sertão do Seridó - RN
publico: Ensino Fundamental
palavras-chave: fogo; cobra; proteção da mata
imagem: 01_boitata.jpg
fonte: ROMERO, Sílvio. Contos Populares do Brasil. Lisboa: Nova Livraria Internacional, 1885. Disponível em: <endereço>. Acesso em: 30 set. 2026.
---
Conta-se que nas noites escuras do sertão aparece uma cobra de fogo...

(o texto da narrativa vem aqui, em um ou mais parágrafos)
```

Três regras deste formato:

- **as sete primeiras linhas** são os dados da narrativa, no formato `rótulo: valor`, um por linha;
- **a linha com três traços (`---`)** separa os dados do texto;
- **tudo o que vem depois** é o texto da narrativa.

**Salve os arquivos como UTF-8.** No Bloco de Notas: *Arquivo → Salvar como → Codificação: UTF-8*. No VS Code já é o padrão. Se você errar isso, os acentos viram símbolos estranhos quando o Python for ler.

Nomeie os arquivos `01_boitata.txt`, `02_lobisomem.txt`, e assim por diante.

**3. Arrume uma imagem para cada narrativa.** Guarde em `imagens/`, com o mesmo número do arquivo da narrativa (`01_boitata.jpg`).

**A imagem também precisa ter licença livre.** Use o **Wikimedia Commons** (`commons.wikimedia.org`), que informa a licença de cada imagem, ou fotografias que você mesmo tenha tirado. **Anote a licença de cada imagem** em um arquivo `imagens/creditos.md` — isso vai para o artigo, e é uma boa prática que impressiona quem avalia.

Use imagens de tamanho parecido entre si (por exemplo, todas com cerca de 800 pixels de largura). Se forem muito diferentes, você não vai saber se a diferença no PDF foi da biblioteca ou da imagem.

**4. Escreva o programa que lê os arquivos.** Crie `geradores/ler_narrativas.py`:

```python
import os

PASTA = "narrativas"

def ler_narrativa(caminho):
    """Le um arquivo .txt e devolve um dicionario com os dados e o texto."""
    with open(caminho, encoding="utf-8") as arquivo:
        conteudo = arquivo.read()

    # separa o cabecalho do texto, na linha com tres tracos
    cabecalho, texto = conteudo.split("---", 1)

    narrativa = {}
    for linha in cabecalho.strip().split("\n"):
        if ":" in linha:
            rotulo, valor = linha.split(":", 1)
            narrativa[rotulo.strip()] = valor.strip()

    narrativa["texto"] = texto.strip()
    narrativa["arquivo"] = os.path.basename(caminho)
    return narrativa

def ler_todas():
    """Le todas as narrativas da pasta, em ordem de nome de arquivo."""
    narrativas = []
    for nome in sorted(os.listdir(PASTA)):
        if nome.endswith(".txt"):
            narrativas.append(ler_narrativa(os.path.join(PASTA, nome)))
    return narrativas

if __name__ == "__main__":
    for narrativa in ler_todas():
        print(narrativa["arquivo"], "|", narrativa["titulo"],
              "|", len(narrativa["texto"]), "caracteres")
```

Rode com `python geradores/ler_narrativas.py`. Você deve ver as 10 linhas, uma por narrativa.

> **Entenda o que o programa faz**, porque você vai usá-lo nas três bibliotecas: ele abre o arquivo, corta no `---`, transforma cada linha do cabeçalho em um par `rótulo → valor` e guarda tudo em um **dicionário**. Depois, em qualquer gerador, você escreve `narrativa["titulo"]` e tem o título.

> **Erro comum:** se aparecer `ValueError: not enough values to unpack`, é porque algum arquivo está sem a linha `---`. Se aparecer `UnicodeDecodeError`, é porque algum arquivo não foi salvo em UTF-8.

**5. Desenhe o modelo do folder.** Este é o passo mais importante da semana, e **não é programação**: é desenho.

Você precisa de **um desenho de como o folder deve ficar**, porque é contra esse desenho que as três bibliotecas vão ser comparadas. Sem ele, "fidelidade ao leiaute" vira opinião.

**Ferramentas gratuitas que funcionam no navegador, sem instalar nada:** `app.diagrams.net`, o Canva na versão gratuita, ou até o PowerPoint, se estiver instalado na máquina.

**O folder deve ser A4, retrato, e ter estes 10 elementos** — que são exatamente os itens da lista de conferência:

| # | Elemento | Detalhe |
|---|---|---|
| 1 | Faixa colorida no topo | com o nome "Narrativas do Rio Grande do Norte" em branco |
| 2 | Título da narrativa | grande, em negrito, abaixo da faixa |
| 3 | Linha de dados | tipo • origem • público-alvo, em fonte menor e cinza |
| 4 | Imagem | centralizada, largura de 10 cm, sem deformar |
| 5 | Legenda da imagem | fonte pequena, itálico, logo abaixo da imagem |
| 6 | Texto da narrativa | justificado, com espaço entre os parágrafos |
| 7 | Caixa de palavras-chave | com borda, no fim do texto |
| 8 | Rodapé com a fonte | a referência de onde a narrativa foi tirada, em fonte pequena |
| 9 | Número da página | no canto do rodapé |
| 10 | Repetição em várias páginas | se o texto for longo, a faixa do topo e o rodapé se repetem na página 2 |

Salve o desenho como `modelo/modelo_folder.png`.

**6. Escreva a lista de conferência.** Crie `modelo/checklist.md` com os 10 itens acima, e a regra de pontuação:

- **2 pontos** — saiu igual ao modelo;
- **1 ponto** — saiu parecido, mas com diferença visível (cor errada, posição deslocada, tamanho diferente);
- **0 ponto** — não saiu, ou saiu errado a ponto de atrapalhar.

Assim cada biblioteca pode fazer de 0 a 20 pontos. **Escreva essa regra agora, antes de gerar qualquer folder** — se você escrever depois de ver os resultados, acaba criando uma régua que favorece a biblioteca de que você mais gostou. Isso tem nome, chama-se **viés**, e invalida a comparação.

### Como saber que deu certo

- `python geradores/ler_narrativas.py` lista as 10 narrativas, com os títulos certos e acentos corretos na tela.
- A pasta `imagens/` tem 10 imagens, e `imagens/creditos.md` diz a licença de cada uma.
- O arquivo `modelo/modelo_folder.png` existe e mostra claramente os 10 elementos.
- `modelo/checklist.md` está escrito.

### Entrega da sprint

- [ ] 10 narrativas em `narrativas/`, com tamanhos variados e fonte anotada.
- [ ] 10 imagens em `imagens/`, com as licenças registradas.
- [ ] `geradores/ler_narrativas.py` funcionando.
- [ ] `modelo/modelo_folder.png` desenhado.
- [ ] `modelo/checklist.md` com os 10 itens e a regra de pontuação.
- [ ] Fonte das narrativas confirmada com o orientador.

---

# Sprint 3 — 06/10 a 12/10/2026
## Biblioteca 1: o folder com FPDF2

**O que você vai entregar:** um programa que gera o folder completo, para as 10 narrativas, usando a biblioteca FPDF2.

**Como essa biblioteca pensa:** você diz **onde** cada coisa vai, como se estivesse desenhando em uma folha com uma régua. É a mais direta de entender, e a que dá mais trabalho quando o leiaute é complicado.

### Passo a passo

**1. Resolva a questão da fonte antes de qualquer coisa.** A FPDF2 vem com fontes embutidas (Helvetica, Times, Courier) que cobrem os acentos do português — mas **não cobrem** caracteres como o travessão (—), as reticências (…) e as aspas curvas (" "), que aparecem muito em texto literário antigo.

Teste agora. Crie um arquivo com esta linha e rode:

```python
pdf.multi_cell(0, 8, "Travessão — reticências… aspas “curvas”")
```

- **Se der erro ou sair caractere estranho**, você tem duas saídas, e **as duas são resultado do trabalho**:
  - **(a)** limpar o texto, trocando esses caracteres por equivalentes simples (`—` vira `-`, `…` vira `...`);
  - **(b)** usar uma fonte TrueType com todos os caracteres. Baixe a fonte **DejaVu Sans** (é gratuita e de uso livre), salve em `geradores/fontes/DejaVuSans.ttf` e registre assim:

```python
pdf.add_font("DejaVu", "", "geradores/fontes/DejaVuSans.ttf")
pdf.add_font("DejaVu", "B", "geradores/fontes/DejaVuSans-Bold.ttf")
pdf.set_font("DejaVu", size=11)
```

**Faça a opção (b)**, que é a correta, mas **registre no diário que a (a) foi necessária antes** — essa dificuldade é exatamente um dos pontos da sua comparação, e as outras bibliotecas podem não ter esse problema.

**2. Escreva o gerador.** Crie `geradores/gerar_fpdf2.py`. Monte por partes, testando cada uma:

```python
import os
from fpdf import FPDF
from ler_narrativas import ler_todas

AZUL = (20, 60, 110)
CINZA = (110, 110, 110)

class Folder(FPDF):
    def header(self):
        # faixa colorida do topo (item 1 do checklist)
        self.set_fill_color(*AZUL)
        self.rect(0, 0, 210, 18, style="F")
        self.set_text_color(255, 255, 255)
        self.set_font("DejaVu", "B", 13)
        self.set_y(5)
        self.cell(0, 8, "Narrativas do Rio Grande do Norte",
                  new_x="LMARGIN", new_y="NEXT", align="C")
        self.set_text_color(0, 0, 0)
        self.set_y(26)

    def footer(self):
        # rodape com fonte e numero da pagina (itens 8 e 9)
        self.set_y(-18)
        self.set_font("DejaVu", "", 7)
        self.set_text_color(*CINZA)
        self.multi_cell(0, 4, self.fonte_bibliografica, align="L")
        self.set_font("DejaVu", "", 8)
        self.cell(0, 6, f"Página {self.page_no()}", align="R")
        self.set_text_color(0, 0, 0)
```

Depois a função que monta o corpo:

```python
def gerar_folder(narrativa, caminho_saida):
    pdf = Folder()
    pdf.fonte_bibliografica = narrativa["fonte"]
    pdf.add_font("DejaVu", "", "geradores/fontes/DejaVuSans.ttf")
    pdf.add_font("DejaVu", "B", "geradores/fontes/DejaVuSans-Bold.ttf")
    pdf.set_auto_page_break(auto=True, margin=25)
    pdf.add_page()

    # item 2: titulo
    pdf.set_font("DejaVu", "B", 18)
    pdf.multi_cell(0, 10, narrativa["titulo"], align="C")

    # item 3: linha de dados
    pdf.set_font("DejaVu", "", 9)
    pdf.set_text_color(*CINZA)
    dados = f'{narrativa["tipo"]}  •  {narrativa["origem"]}  •  {narrativa["publico"]}'
    pdf.multi_cell(0, 6, dados, align="C")
    pdf.set_text_color(0, 0, 0)
    pdf.ln(4)

    # item 4: imagem, centralizada, 10 cm de largura
    caminho_imagem = os.path.join("imagens", narrativa["imagem"])
    largura = 100
    pdf.image(caminho_imagem, x=(210 - largura) / 2, w=largura)

    # item 5: legenda
    pdf.set_font("DejaVu", "", 8)
    pdf.multi_cell(0, 5, f'Imagem: {narrativa["titulo"]}', align="C")
    pdf.ln(4)

    # item 6: texto da narrativa
    pdf.set_font("DejaVu", "", 11)
    for paragrafo in narrativa["texto"].split("\n\n"):
        pdf.multi_cell(0, 6, paragrafo.strip(), align="J")
        pdf.ln(3)

    # item 7: caixa de palavras-chave
    pdf.ln(2)
    pdf.set_font("DejaVu", "B", 9)
    pdf.multi_cell(0, 7, f'Palavras-chave: {narrativa["palavras-chave"]}',
                   border=1, align="L")

    pdf.output(caminho_saida)

if __name__ == "__main__":
    os.makedirs("saidas/fpdf2", exist_ok=True)
    for narrativa in ler_todas():
        nome = narrativa["arquivo"].replace(".txt", ".pdf")
        gerar_folder(narrativa, os.path.join("saidas/fpdf2", nome))
        print("gerado:", nome)
```

**3. Cuidados que vão te economizar horas:**

- **o `import ler_narrativas` só funciona se você rodar de dentro de `bruno/`.** Rode sempre `python geradores/gerar_fpdf2.py` a partir da pasta `bruno/`. Se der `ModuleNotFoundError`, é isso;
- **a imagem pode deformar.** O `pdf.image(..., w=100)` sem informar a altura mantém a proporção — é o comportamento correto. Se você informar `w` **e** `h`, a imagem estica. **Teste as duas formas e anote o que acontece**: é o item "imagens" da sua comparação;
- **o `multi_cell` quebra a linha sozinho**, mas se uma palavra for maior que a largura disponível, ele dá erro. Isso é raro em texto normal, mas pode acontecer com um endereço de internet longo no rodapé;
- **texto justificado** é `align="J"`. Compare visualmente com `align="L"` e veja qual fica mais parecido com o seu modelo.

**4. Gere os 10 folders e olhe todos, um por um.** Sério: abra os 10. É neste momento que você descobre que a narrativa curta ficou com muito espaço em branco, que a longa passou para a página 3, ou que uma imagem ficou desproporcional.

**Anote tudo o que estiver diferente do modelo.** Essa anotação é o rascunho da sua avaliação de fidelidade, que acontece na Sprint 7.

**5. Confira o seu folder contra a lista de conferência**, só para saber onde está. Não precisa dar a nota oficial ainda — isso é da Sprint 7. Se algum dos 10 itens estiver muito longe, use o resto da semana para melhorar.

### Como saber que deu certo

- A pasta `saidas/fpdf2/` tem 10 arquivos PDF.
- Abrindo qualquer um: a faixa azul está no topo, a imagem aparece, os acentos estão certos, há número de página.
- A narrativa longa ocupa mais de uma página, e **a faixa e o rodapé se repetem** na segunda.
- Ctrl+F acha uma palavra do texto.

### Entrega da sprint

- [ ] `geradores/gerar_fpdf2.py` gerando os 10 folders.
- [ ] Questão das fontes resolvida e registrada no diário.
- [ ] Print de um folder completo (as duas páginas) em `docs/evidencias/`.
- [ ] Lista das diferenças em relação ao modelo, anotada no diário.
- [ ] Anotado quanto tempo você levou para escrever esse programa — isso é um dado de "esforço de implementação".

---

# Sprint 4 — 13/10 a 19/10/2026
## Biblioteca 2: o mesmo folder com ReportLab

**O que você vai entregar:** o **mesmo folder**, gerado pela biblioteca ReportLab.

**Como essa biblioteca pensa:** você monta uma **lista de blocos** (um parágrafo, uma imagem, um espaço) e entrega para a biblioteca, que se encarrega de encaixar tudo nas páginas. É diferente da FPDF2, onde você diz as coordenadas. Essa diferença de pensamento é um dos assuntos mais interessantes do seu artigo.

> **Regra que vale para esta sprint e para a próxima: o folder tem que ser o MESMO.** Mesmas cores, mesmos tamanhos de fonte, mesma ordem dos elementos. Se você "caprichar" numa biblioteca e não na outra, a comparação não vale. Se descobrir uma melhoria, volte e aplique nas três.

### Passo a passo

**1. Entenda as duas peças da ReportLab que você vai usar:**

- os **blocos** (a biblioteca chama de *flowables*): `Paragraph` (um parágrafo), `Image` (uma imagem), `Spacer` (um espaço em branco), `Table` (uma tabela, que serve para fazer a caixa com borda);
- os **estilos**: em vez de chamar `set_font` antes de cada coisa, você define um estilo uma vez e aplica nos parágrafos.

**2. Escreva o gerador.** Crie `geradores/gerar_reportlab.py`:

```python
import os
from reportlab.lib.pagesizes import A4
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.lib.units import cm
from reportlab.lib import colors
from reportlab.lib.enums import TA_CENTER, TA_JUSTIFY
from reportlab.platypus import (SimpleDocTemplate, Paragraph, Spacer,
                                Image, Table, TableStyle)
from ler_narrativas import ler_todas

AZUL = colors.Color(20 / 255, 60 / 255, 110 / 255)
LARGURA, ALTURA = A4

def montar_estilos():
    estilos = getSampleStyleSheet()
    estilos.add(ParagraphStyle(name="TituloFolder", fontName="Helvetica-Bold",
                               fontSize=18, leading=22, alignment=TA_CENTER))
    estilos.add(ParagraphStyle(name="Dados", fontName="Helvetica", fontSize=9,
                               textColor=colors.grey, alignment=TA_CENTER))
    estilos.add(ParagraphStyle(name="Legenda", fontName="Helvetica-Oblique",
                               fontSize=8, alignment=TA_CENTER))
    estilos.add(ParagraphStyle(name="Corpo", fontName="Helvetica", fontSize=11,
                               leading=16, alignment=TA_JUSTIFY, spaceAfter=8))
    return estilos
```

Depois a função que desenha a faixa e o rodapé (na ReportLab isso é uma função que ela chama a cada página):

```python
def cabecalho_rodape(canvas, doc):
    canvas.saveState()
    # faixa do topo
    canvas.setFillColor(AZUL)
    canvas.rect(0, ALTURA - 1.8 * cm, LARGURA, 1.8 * cm, stroke=0, fill=1)
    canvas.setFillColor(colors.white)
    canvas.setFont("Helvetica-Bold", 13)
    canvas.drawCentredString(LARGURA / 2, ALTURA - 1.2 * cm,
                             "Narrativas do Rio Grande do Norte")
    # rodape
    canvas.setFillColor(colors.grey)
    canvas.setFont("Helvetica", 7)
    canvas.drawString(2 * cm, 1.2 * cm, doc.fonte_bibliografica[:120])
    canvas.setFont("Helvetica", 8)
    canvas.drawRightString(LARGURA - 2 * cm, 1.2 * cm, f"Página {doc.page}")
    canvas.restoreState()
```

E o corpo:

```python
def gerar_folder(narrativa, caminho_saida):
    estilos = montar_estilos()
    doc = SimpleDocTemplate(caminho_saida, pagesize=A4,
                            topMargin=2.6 * cm, bottomMargin=2.5 * cm,
                            leftMargin=2 * cm, rightMargin=2 * cm)
    doc.fonte_bibliografica = narrativa["fonte"]

    blocos = []
    blocos.append(Paragraph(narrativa["titulo"], estilos["TituloFolder"]))
    dados = f'{narrativa["tipo"]} &bull; {narrativa["origem"]} &bull; {narrativa["publico"]}'
    blocos.append(Paragraph(dados, estilos["Dados"]))
    blocos.append(Spacer(1, 0.5 * cm))

    caminho_imagem = os.path.join("imagens", narrativa["imagem"])
    blocos.append(Image(caminho_imagem, width=10 * cm, height=7 * cm,
                        kind="proportional"))
    blocos.append(Paragraph(f'Imagem: {narrativa["titulo"]}', estilos["Legenda"]))
    blocos.append(Spacer(1, 0.5 * cm))

    for paragrafo in narrativa["texto"].split("\n\n"):
        blocos.append(Paragraph(paragrafo.strip(), estilos["Corpo"]))

    caixa = Table([[Paragraph(f'<b>Palavras-chave:</b> {narrativa["palavras-chave"]}',
                              estilos["BodyText"])]], colWidths=[17 * cm])
    caixa.setStyle(TableStyle([("BOX", (0, 0), (-1, -1), 0.8, colors.black),
                               ("PADDING", (0, 0), (-1, -1), 8)]))
    blocos.append(Spacer(1, 0.4 * cm))
    blocos.append(caixa)

    doc.build(blocos, onFirstPage=cabecalho_rodape, onLaterPages=cabecalho_rodape)
```

**3. Quatro armadilhas desta biblioteca — todas viram anotação no diário:**

- **o `Paragraph` entende algumas marcações de HTML**, como `<b>` para negrito. Isso é ótimo, mas significa que um texto com `<` ou `&` **dá erro**. Se alguma narrativa tiver esses símbolos, troque `&` por `&amp;` antes. **Teste de propósito** com um texto que tenha `&` e anote o que acontece;
- **o `kind="proportional"`** na imagem faz ela caber na caixa sem deformar. Sem isso, ela estica para o tamanho exato que você pediu. Teste os dois jeitos;
- **os acentos** funcionam com as fontes padrão (Helvetica), diferente do que aconteceu na FPDF2. **Anote essa diferença — é um resultado**;
- **a caixa com borda** não existe pronta: teve que ser feita com uma tabela de uma célula só. Anote isso como "esforço de implementação".

**4. Gere os 10 folders**, coloque lado a lado com os da FPDF2 e compare. **Tire um print das duas versões do mesmo folder, lado a lado** — essa é provavelmente a melhor figura do seu artigo.

### Como saber que deu certo

- A pasta `saidas/reportlab/` tem 10 PDFs.
- O folder está **visualmente igual** ao da FPDF2 (pequenas diferenças são esperadas e são justamente o objeto do estudo).
- A narrativa longa passa de página, com faixa e rodapé repetidos.

### Entrega da sprint

- [ ] `geradores/gerar_reportlab.py` gerando os 10 folders.
- [ ] Print comparando o mesmo folder nas duas bibliotecas.
- [ ] As quatro armadilhas testadas e anotadas no diário.
- [ ] Tempo que você levou para escrever o programa, anotado.

---

# Sprint 5 — 20/10 a 26/10/2026
## Biblioteca 3 (xhtml2pdf) e a quarta biblioteca

**O que você vai entregar:** o mesmo folder feito a partir de HTML e CSS, e o registro do que aconteceu ao tentar instalar uma quarta biblioteca.

**Como essa biblioteca pensa:** você **não programa o leiaute** — você escreve uma página HTML com CSS, como se fosse um site, e a biblioteca transforma em PDF. É uma forma completamente diferente das duas anteriores, e é o contraste mais interessante do seu trabalho.

### Parte A — xhtml2pdf

**1. Escreva o modelo em HTML.** Crie `geradores/modelo_folder.html`:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <style>
    @page {
      size: a4 portrait;
      margin: 2.6cm 2cm 2.5cm 2cm;
      @frame rodape { -pdf-frame-content: rodape; bottom: 1cm; height: 1.5cm; }
    }
    body   { font-family: Helvetica; font-size: 11pt; }
    .faixa { background-color: #143c6e; color: white; text-align: center;
             font-size: 13pt; font-weight: bold; padding: 6px; }
    h1     { font-size: 18pt; text-align: center; margin: 12px 0 4px 0; }
    .dados { font-size: 9pt; color: #6e6e6e; text-align: center; }
    .imagem   { text-align: center; margin-top: 12px; }
    .legenda  { font-size: 8pt; font-style: italic; text-align: center; }
    p.corpo   { text-align: justify; line-height: 150%; margin-bottom: 8px; }
    .chaves   { border: 1px solid black; padding: 8px; font-size: 9pt;
                font-weight: bold; margin-top: 10px; }
    #rodape   { font-size: 7pt; color: #6e6e6e; }
  </style>
</head>
<body>
  <div class="faixa">Narrativas do Rio Grande do Norte</div>
  <h1>{titulo}</h1>
  <div class="dados">{tipo} &bull; {origem} &bull; {publico}</div>
  <div class="imagem"><img src="{imagem}" width="280"></div>
  <div class="legenda">Imagem: {titulo}</div>
  {paragrafos}
  <div class="chaves">Palavras-chave: {palavras}</div>
  <div id="rodape">{fonte} — página <pdf:pagenumber></div>
</body>
</html>
```

**2. Escreva o gerador.** Crie `geradores/gerar_xhtml2pdf.py`:

```python
import os
from xhtml2pdf import pisa
from ler_narrativas import ler_todas

with open("geradores/modelo_folder.html", encoding="utf-8") as arquivo:
    MODELO = arquivo.read()

def gerar_folder(narrativa, caminho_saida):
    paragrafos = "".join(
        f'<p class="corpo">{p.strip()}</p>'
        for p in narrativa["texto"].split("\n\n") if p.strip()
    )
    html = (MODELO
            .replace("{titulo}", narrativa["titulo"])
            .replace("{tipo}", narrativa["tipo"])
            .replace("{origem}", narrativa["origem"])
            .replace("{publico}", narrativa["publico"])
            .replace("{imagem}", os.path.abspath(
                os.path.join("imagens", narrativa["imagem"])))
            .replace("{paragrafos}", paragrafos)
            .replace("{palavras}", narrativa["palavras-chave"])
            .replace("{fonte}", narrativa["fonte"]))

    with open(caminho_saida, "wb") as saida:
        resultado = pisa.CreatePDF(html, dest=saida, encoding="utf-8")
    if resultado.err:
        print("ERRO ao gerar", caminho_saida)

if __name__ == "__main__":
    os.makedirs("saidas/xhtml2pdf", exist_ok=True)
    for narrativa in ler_todas():
        nome = narrativa["arquivo"].replace(".txt", ".pdf")
        gerar_folder(narrativa, os.path.join("saidas/xhtml2pdf", nome))
        print("gerado:", nome)
```

**3. Três armadilhas desta biblioteca:**

- **o caminho da imagem precisa ser absoluto.** Por isso o `os.path.abspath` no código. Se você usar caminho relativo, a imagem simplesmente não aparece — **e não dá erro**, o que é pior. Teste e anote;
- **ela entende só uma parte do CSS.** Coisas comuns em sites (flexbox, grid, sombras, cantos arredondados) **não funcionam**. Descobrir o que funciona e o que não funciona é parte do trabalho. Anote cada coisa que você tentou e não deu certo;
- **`resultado.err`** diz se deu erro. Sempre confira — é fácil gerar um PDF quebrado e não perceber.

**4. Compare com as outras duas.** Repare especialmente em: o texto justificado ficou igual? A faixa ficou da mesma cor? A caixa de palavras-chave ficou do mesmo tamanho? A imagem ficou no mesmo lugar?

**5. Anote o tempo de escrita do programa e, principalmente, a sua impressão sobre a facilidade.** Foi mais fácil ou mais difícil que as outras? Por quê? Se você já sabe HTML e CSS, isso conta — e é uma observação legítima para o artigo, desde que você diga que é a sua percepção, e não uma medida.

### Parte B — A quarta biblioteca: WeasyPrint

A temática original sugeria comparar **quatro** bibliotecas, e a quarta é a **WeasyPrint**, que também gera PDF a partir de HTML e CSS, com suporte a CSS bem mais moderno que a xhtml2pdf.

**Tente instalar:**

```
pip install weasyprint
```

E depois tente rodar qualquer exemplo simples da documentação dela.

> **O que provavelmente vai acontecer:** no Windows, a WeasyPrint precisa de programas auxiliares do sistema (as bibliotecas GTK, Pango e Cairo) que **não vêm pelo `pip`** e exigem um instalador — justamente o que as máquinas do laboratório não permitem. O `pip install` costuma terminar sem erro, mas na hora de usar aparece uma mensagem sobre biblioteca não encontrada.

**Seja qual for o resultado, ele é um achado do trabalho. Faça assim:**

- **se instalar e funcionar:** ótimo, implemente o folder nela também e inclua na comparação como quarta biblioteca;
- **se não funcionar:** **copie a mensagem de erro inteira**, tire um print e registre em `docs/instalacao.md` exatamente o que você tentou, em que ordem, e o que apareceu.

**Não esconda isso, e não trate como fracasso.** "Facilidade de instalação" é um dos critérios de comparação previstos desde o começo, e a equipe do Narrativas precisa saber que essa biblioteca não serve em um ambiente Windows sem privilégios de administração. **Esse é um dos resultados mais úteis que o seu trabalho pode entregar**, porque é o tipo de coisa que só se descobre tentando.

No artigo, apresente a WeasyPrint em uma coluna própria do quadro comparativo, com "não avaliado — não foi possível instalar no ambiente" nos critérios que dependem de rodar a biblioteca, e a explicação do motivo.

### Como saber que deu certo

- A pasta `saidas/xhtml2pdf/` tem 10 PDFs, visualmente parecidos com os das outras duas.
- A imagem aparece (se não aparecer, é o caminho relativo).
- O que aconteceu com a WeasyPrint está registrado por escrito, com print.

### Entrega da sprint

- [ ] `geradores/gerar_xhtml2pdf.py` e `geradores/modelo_folder.html` funcionando.
- [ ] Lista do que funcionou e do que não funcionou no CSS, anotada.
- [ ] Tentativa de instalar a WeasyPrint documentada em `docs/instalacao.md`, com print.
- [ ] Print comparando o mesmo folder nas três bibliotecas.
- [ ] Tempo de escrita do programa, anotado.

---

# Sprint 6 — 27/10 a 02/11/2026
## As medições objetivas

**O que você vai entregar:** um programa que mede, sozinho, tempo, tamanho, acentuação e texto pesquisável dos PDFs das três bibliotecas — e uma planilha com tudo.

Até aqui você olhou os folders. Agora você vai **medir**. É esta sprint que transforma o trabalho em pesquisa.

### Passo a passo

**1. Entenda o que vai ser medido, e por quê:**

| Medida | Como se mede | Por que importa |
|---|---|---|
| **Tempo de geração** | cronômetro em volta da chamada que gera o folder | se a plataforma gerar PDF sob demanda, o usuário espera |
| **Tamanho do arquivo** | `os.path.getsize` | arquivo grande demora para baixar e ocupa espaço no servidor |
| **Texto pesquisável** | extrair o texto do PDF com o `pypdf` | se não der para extrair, o PDF é inacessível para leitores de tela |
| **Acentuação** | procurar palavras acentuadas no texto extraído | palavra com acento quebrada é erro grave em português |
| **Número de páginas** | `len(leitor.pages)` | mostra se a biblioteca aproveitou bem o espaço |
| **Linhas de código** | contar as linhas do programa gerador | mede o esforço de implementação e de manutenção |

**2. Escreva o programa de medição.** Crie `medir.py`, na raiz de `bruno/`:

```python
import csv
import os
import statistics
import sys
import time
from pypdf import PdfReader

sys.path.insert(0, "geradores")
from ler_narrativas import ler_todas
import gerar_fpdf2
import gerar_reportlab
import gerar_xhtml2pdf

BIBLIOTECAS = {
    "fpdf2": gerar_fpdf2,
    "reportlab": gerar_reportlab,
    "xhtml2pdf": gerar_xhtml2pdf,
}

# palavras acentuadas que devem aparecer no texto extraido
PALAVRAS_TESTE = ["coração", "sertão", "vovó", "história", "três"]

def medir_tempo(modulo, narrativa, caminho, repeticoes=6):
    tempos = []
    for _ in range(repeticoes):
        inicio = time.perf_counter()
        modulo.gerar_folder(narrativa, caminho)
        tempos.append((time.perf_counter() - inicio) * 1000)
    tempos = tempos[1:]                     # descarta a primeira (aquecimento)
    return statistics.median(tempos), statistics.stdev(tempos)

def analisar_pdf(caminho):
    leitor = PdfReader(caminho)
    texto = ""
    for pagina in leitor.pages:
        texto += pagina.extract_text() or ""
    return len(leitor.pages), texto

def contar_palavras_acentuadas(texto_pdf, texto_original):
    """Conta quantas palavras acentuadas do original aparecem certas no PDF."""
    esperadas = [p for p in PALAVRAS_TESTE if p in texto_original.lower()]
    if not esperadas:
        return None
    achadas = sum(1 for p in esperadas if p in texto_pdf.lower())
    return achadas / len(esperadas)

def main():
    linhas = []
    for narrativa in ler_todas():
        for nome, modulo in BIBLIOTECAS.items():
            pasta = os.path.join("saidas", nome)
            os.makedirs(pasta, exist_ok=True)
            caminho = os.path.join(pasta, narrativa["arquivo"].replace(".txt", ".pdf"))

            mediana, desvio = medir_tempo(modulo, narrativa, caminho)
            tamanho_kb = os.path.getsize(caminho) / 1024
            paginas, texto_pdf = analisar_pdf(caminho)
            acertos = contar_palavras_acentuadas(texto_pdf, narrativa["texto"])

            linhas.append({
                "biblioteca": nome,
                "narrativa": narrativa["arquivo"],
                "caracteres": len(narrativa["texto"]),
                "tempo_ms": round(mediana, 2),
                "desvio_ms": round(desvio, 2),
                "tamanho_kb": round(tamanho_kb, 1),
                "paginas": paginas,
                "texto_extraido": len(texto_pdf),
                "acentos_ok": round(acertos, 2) if acertos is not None else "",
            })
            print(nome, narrativa["arquivo"], f"{mediana:.1f} ms", f"{tamanho_kb:.1f} KB")

    with open("resultados/medicoes.csv", "w", newline="", encoding="utf-8") as arquivo:
        escritor = csv.DictWriter(arquivo, fieldnames=list(linhas[0].keys()))
        escritor.writeheader()
        escritor.writerows(linhas)
    print("\nMedições salvas em resultados/medicoes.csv")

if __name__ == "__main__":
    main()
```

**3. Entenda duas decisões do programa** — as duas vão para a Metodologia do artigo:

- **por que repetir 6 vezes e descartar a primeira?** Porque a primeira execução ainda está carregando coisas na memória e é sempre a mais lenta. Isso se chama **aquecimento**. Uma medição de tempo feita uma vez só não vale nada;
- **por que usar a mediana, e não a média?** Porque a mediana não é estragada por uma medição esquisita, que acontece quando o Windows resolve fazer outra coisa no meio.

**Antes de rodar, feche o navegador e tudo o mais que estiver aberto.** E registre isso: faz parte do protocolo de medição.

**4. Meça o tamanho dos programas.** Conte as linhas de cada gerador, sem contar linhas vazias e comentários. Um jeito rápido:

```python
for nome in ["gerar_fpdf2.py", "gerar_reportlab.py", "gerar_xhtml2pdf.py"]:
    with open(f"geradores/{nome}", encoding="utf-8") as arquivo:
        linhas = [l for l in arquivo
                  if l.strip() and not l.strip().startswith("#")]
    print(nome, len(linhas), "linhas")
```

Para a xhtml2pdf, **some as linhas do arquivo HTML também** — senão a comparação fica injusta, porque metade do trabalho dela está lá. Anote os dois números separados e o total.

**5. Olhe a planilha e desconfie de números estranhos.** Se uma biblioteca aparecer com `texto_extraido` igual a zero, o PDF dela não é pesquisável — **isso é um resultado importante**, confirme abrindo o arquivo e tentando Ctrl+F. Se `acentos_ok` der menos que 1, algum acento se perdeu na extração — confira qual, e anote a palavra exata.

**6. Registre o protocolo.** Escreva em `docs/ambiente.md`, no fim: quantas repetições, que a primeira foi descartada, que foi usada a mediana, que a máquina estava sem outros programas abertos, e a data da medição.

### Como saber que deu certo

- `python medir.py` roda até o fim e cria `resultados/medicoes.csv` com 30 linhas (10 narrativas × 3 bibliotecas).
- Os tempos fazem sentido (alguns milissegundos a poucos segundos por folder).
- Você consegue responder, olhando a planilha: qual biblioteca é mais rápida? Qual gera arquivo menor? Alguma perdeu acento?

> **Se `medir.py` der erro ao importar os geradores**, o motivo mais comum é que eles executam código ao serem importados. Confira se o código que gera os 10 folders em cada gerador está dentro do `if __name__ == "__main__":` — ele existe justamente para isso.

### Entrega da sprint

- [ ] `medir.py` funcionando.
- [ ] `resultados/medicoes.csv` com as 30 linhas.
- [ ] Contagem de linhas de código das três bibliotecas.
- [ ] Protocolo de medição registrado em `docs/ambiente.md`.
- [ ] Qualquer número estranho investigado e explicado no diário.

---

# Sprint 7 — 03/11 a 09/11/2026
## A avaliação do leiaute e os gráficos

**O que você vai entregar:** a nota de fidelidade de cada biblioteca, conferida por uma segunda pessoa, e os gráficos do artigo.

O tempo e o tamanho o computador mediu sozinho. **A fidelidade do leiaute quem avalia é você** — e por isso ela precisa de um método, senão vira opinião.

### Passo a passo

**1. Monte a planilha de avaliação.** Crie `resultados/fidelidade.csv` com esta estrutura:

```
item,descricao,fpdf2,reportlab,xhtml2pdf
1,Faixa colorida no topo,,,
2,Titulo grande e centralizado,,,
3,Linha de dados em cinza,,,
4,Imagem centralizada sem deformar,,,
5,Legenda da imagem em italico,,,
6,Texto justificado com espaco entre paragrafos,,,
7,Caixa de palavras-chave com borda,,,
8,Rodape com a fonte bibliografica,,,
9,Numero da pagina,,,
10,Faixa e rodape repetidos na pagina 2,,,
```

**2. Avalie, item por item.** Abra, lado a lado: o `modelo/modelo_folder.png` e os três PDFs **da mesma narrativa** (escolha uma das longas, para poder avaliar o item 10). Dê a nota de cada item conforme a regra que você escreveu na Sprint 2: **2** igual, **1** parecido com diferença visível, **0** não saiu ou saiu errado.

**Duas regras para a avaliação ser honesta:**

- **avalie um item por vez, nas três bibliotecas**, em vez de avaliar uma biblioteca inteira e depois a outra. Assim você compara o mesmo detalhe de uma vez e fica mais consistente;
- **escreva uma justificativa curta para toda nota diferente de 2.** "1 — a cor da faixa ficou mais clara que no modelo" é útil; "1" sozinho não é. Guarde essas justificativas: elas viram o texto da discussão dos resultados.

**3. Peça ao orientador para avaliar também.** Mostre o modelo e os três PDFs, sem dizer qual biblioteca é qual e **sem dizer as suas notas**, e peça que ele preencha a mesma lista.

**Depois compare as duas avaliações.** Onde vocês deram notas diferentes, converse e entenda o motivo. Isso leva meia hora e dá **muita** credibilidade ao trabalho — porque mostra que a nota não é só a sua impressão pessoal. **Descreva essa conferência na Metodologia do artigo** e apresente o resultado (em quantos dos 30 itens vocês concordaram).

**4. Some as notas.** Cada biblioteca faz de 0 a 20 pontos. Escreva o total em `resultados/fidelidade.csv`.

**5. Faça os gráficos.** Crie `graficos.py`, que lê as duas planilhas e gera as figuras com `matplotlib`. **Gráfico feito por programa é reproduzível; print de planilha não é.** Faça quatro:

- **Gráfico 1 — fidelidade do leiaute:** três barras, uma por biblioteca, com a nota de 0 a 20. É a figura que resume o trabalho;
- **Gráfico 2 — tempo médio de geração:** três barras, em milissegundos, com a barra de erro do desvio;
- **Gráfico 3 — tamanho médio do arquivo:** três barras, em KB;
- **Gráfico 4 — tempo por tamanho da narrativa:** o eixo de baixo é o número de caracteres da narrativa e o de cima é o tempo; três linhas, uma por biblioteca. **Este é o gráfico mais interessante**, porque mostra se alguma biblioteca fica desproporcionalmente lenta com texto grande.

Estrutura para começar:

```python
import csv
import statistics
from collections import defaultdict
import matplotlib.pyplot as plt

with open("resultados/medicoes.csv", encoding="utf-8") as arquivo:
    linhas = list(csv.DictReader(arquivo))

tempos = defaultdict(list)
for linha in linhas:
    tempos[linha["biblioteca"]].append(float(linha["tempo_ms"]))

nomes = list(tempos.keys())
medias = [statistics.mean(tempos[n]) for n in nomes]

plt.bar(nomes, medias)
plt.ylabel("Tempo médio de geração (ms)")
plt.title("Tempo para gerar um folder, por biblioteca")
plt.savefig("docs/evidencias/grafico2_tempo.png", dpi=150, bbox_inches="tight")
```

Cuidados com todos os gráficos: escreva o que é cada eixo **e a unidade**; se o eixo vertical não começar em zero, avise na legenda.

### Como saber que deu certo

- `resultados/fidelidade.csv` está preenchido, com as justificativas das notas diferentes de 2.
- A avaliação do orientador está registrada, e você sabe dizer em quantos itens vocês concordaram.
- Os quatro gráficos estão em `docs/evidencias/`, gerados pelo `graficos.py`.

### Entrega da sprint

- [ ] `resultados/fidelidade.csv` completo, com notas e justificativas.
- [ ] Segunda avaliação feita pelo orientador e comparada com a sua.
- [ ] `graficos.py` comitado, gerando os quatro gráficos.
- [ ] Notas totais das três bibliotecas anotadas no diário.

---

# Sprint 8 — 10/11 a 16/11/2026
## O quadro comparativo, a recomendação e a documentação

**O que você vai entregar:** o quadro que responde à pergunta do trabalho, a recomendação para a equipe do Narrativas, o `README.md` e a apresentação.

É nesta semana que o trabalho deixa de ser "três programas que geram PDF" e passa a ser uma pesquisa com resposta.

### Passo a passo

**1. Rode tudo de novo, do zero, de uma vez só.** Apague a pasta `saidas/`, rode `medir.py` e depois `graficos.py`, tudo no mesmo dia e na mesma máquina. **É essa rodada que vai para o artigo.** Guarde a planilha anterior como `resultados/medicoes_anterior.csv` — nunca apague uma medição.

**2. Monte o quadro comparativo.** É a figura mais importante do seu trabalho:

| Critério | FPDF2 | ReportLab | xhtml2pdf | WeasyPrint |
|---|---|---|---|---|
| Fidelidade ao leiaute (0–20) | | | | não avaliado |
| Tempo médio de geração (ms) | | | | não avaliado |
| Tamanho médio do arquivo (KB) | | | | não avaliado |
| Acentuação correta | | | | não avaliado |
| Imagem sem deformar | | | | não avaliado |
| PDF com texto pesquisável | | | | não avaliado |
| Instalação (passos e problemas) | | | | **não foi possível instalar** |
| Linhas de código do gerador | | | | não avaliado |
| Como se programa | coordenadas | blocos | HTML e CSS | HTML e CSS |

**3. Escreva a recomendação.** Em `docs/recomendacao.md`, em meia página, responda à pergunta do trabalho: **qual biblioteca a equipe do Narrativas deve usar, e por quê**.

Três coisas que a recomendação precisa ter:

- **um número que a sustente.** "Recomendo a X porque ficou com 18 de fidelidade contra 14 da Y, gerando o folder em metade do tempo" é uma recomendação; "recomendo a X porque achei melhor" não é;
- **uma condição em que a resposta mudaria.** Por exemplo: "se a equipe precisar mudar o leiaute com frequência e tiver quem saiba CSS, a xhtml2pdf pode compensar, apesar da nota menor";
- **honestidade sobre o que você não mediu.** Você testou um folder, em uma máquina, com 10 narrativas.

**4. Escreva o `README.md` da sua subpasta.** Ele precisa permitir que outra pessoa repita tudo:

1. o que é este trabalho, em três linhas;
2. o que precisa ter instalado (Python 3.x, e só);
3. como criar o ambiente virtual e instalar (`pip install -r requirements.txt`);
4. como o arquivo de uma narrativa é organizado (mostre um exemplo);
5. como gerar os folders com cada biblioteca;
6. como rodar as medições (`python medir.py`);
7. como gerar os gráficos (`python graficos.py`);
8. o que tem em cada pasta;
9. a licença das narrativas e das imagens usadas.

**Teste o seu próprio README:** apague a pasta `.venv` e a `saidas`, siga o seu texto do zero e veja se funciona. É a única forma de saber que ele está completo.

**5. Limpe a subpasta.** Não deixe no repositório: `.venv/`, `__pycache__/`, `saidas/`, arquivos de teste soltos. Rode `git status` e confira se aparece algum arquivo fora de `bruno/` — se aparecer, **não envie** e chame o orientador.

**6. Monte a apresentação.** Dez minutos:

1. o problema — mostre o protótipo da tela com o botão "Baixar PDF";
2. o modelo do folder que você desenhou;
3. o mesmo folder feito pelas três bibliotecas, lado a lado (a melhor figura que você tem);
4. o gráfico de fidelidade e o de tempo;
5. o caso da WeasyPrint, que não instalou;
6. a recomendação.

### Como saber que deu certo

- O quadro comparativo está preenchido, sem nenhuma célula vazia.
- Você consegue responder, em uma frase e com números, qual biblioteca a equipe deve usar.
- Outra pessoa consegue seguir o seu `README.md` do zero.

### Entrega da sprint

- [ ] Rodada final feita de uma vez só.
- [ ] Quadro comparativo completo.
- [ ] `docs/recomendacao.md` escrito.
- [ ] `README.md` escrito e testado.
- [ ] Subpasta limpa e enviada.
- [ ] Apresentação montada.

---

## Quadro-resumo das sprints

| Sprint | Período | O que entrega | O que você aprende |
|---|---|---|---|
| 1 | 22/09 a 28/09 | Ambiente e o primeiro PDF | ambiente virtual, `pip`, primeiro contato com geração de PDF |
| 2 | 29/09 a 05/10 | 10 narrativas, imagens e o modelo do folder | domínio público, licença de imagem, leitura de arquivos, dicionários |
| 3 | 06/10 a 12/10 | Folder com FPDF2 | leiaute por coordenadas, fontes e acentuação |
| 4 | 13/10 a 19/10 | Folder com ReportLab | leiaute por blocos, estilos, quebra de página automática |
| 5 | 20/10 a 26/10 | Folder com xhtml2pdf + teste da WeasyPrint | leiaute por HTML e CSS, dependências do sistema |
| 6 | 27/10 a 02/11 | Medições objetivas | cronometragem, mediana, extração de texto de PDF |
| 7 | 03/11 a 09/11 | Fidelidade do leiaute e gráficos | avaliação com critério, segundo avaliador, gráficos |
| 8 | 10/11 a 16/11 | Quadro, recomendação e documentação | síntese, decisão fundamentada, reprodutibilidade |

---

## Riscos e planos B

| Risco | Sinal de alerta | O que fazer |
|---|---|---|
| `pip install` bloqueado no laboratório | Sprint 1 travada | Resolver com o orientador **na primeira semana**. Em último caso, trabalhar em máquina própria e declarar isso no artigo |
| Git não instalado | Sprint 1 | Combinar entrega pela página do GitHub, no navegador |
| Achar narrativas em domínio público demora | Sprint 2 acabando sem os textos | Reduzir para 6 narrativas, **mantendo a variedade de tamanhos**. Seis bem escolhidas valem mais que quinze no chute |
| Não achar imagens com licença livre | Sprint 2 | Usar fotos próprias, ou desenhos feitos por você. Registre a origem de qualquer jeito |
| Uma biblioteca não consegue fazer um dos 10 itens | Sprints 3 a 5 | **Não force.** Registre como nota 0 ou 1 no item e explique o motivo. É resultado, não fracasso |
| A WeasyPrint não instala | Sprint 5 | **Já é o esperado.** Documente com print e siga com três bibliotecas |
| Sobrou pouco tempo na Sprint 7 | 09/11 sem as notas | Avalie a fidelidade em **uma** narrativa por biblioteca, em vez de várias, e declare isso na Metodologia |

**Se algo tiver de ser cortado, corte largura, não profundidade.** É melhor ter três bibliotecas bem comparadas com 6 narrativas do que quatro comparadas às pressas. O que **não** pode faltar é o modelo do folder, a lista de conferência, as medições e o quadro final.

---

## Se sobrar tempo (opcional)

- **E1.** Fazer o texto da narrativa em **duas colunas**, como em folder de verdade, e comparar quanto trabalho isso dá em cada biblioteca. É um ótimo item extra, porque separa muito bem as três.
- **E2.** Acrescentar um **QR Code** no rodapé, apontando para a página da narrativa no portal (biblioteca `qrcode`, instalada por `pip`).
- **E3.** Gerar uma **segunda versão do folder**, em preto e branco, pensada para impressão econômica em escola pública, e comparar o tamanho do arquivo.
- **E4.** Testar o que acontece quando a imagem é muito grande (por exemplo, 4.000 pixels de largura): alguma biblioteca reduz a imagem sozinha? O arquivo fica enorme?
- **E5.** Verificar se os PDFs gerados têm os **metadados** preenchidos (título, autor), que ajudam na organização do acervo e na acessibilidade.

---

## Relação com o artigo

O desenvolvimento e a escrita andam juntos (ver `01_bruno_narrativas_tarefas_escrita.md`):

| Seção do artigo | Sprints que geram o conteúdo |
|---|---|
| Referencial Teórico | leituras das Sprints 2 a 5 (patrimônio, material didático, formato PDF, as bibliotecas) |
| Metodologia | 2 (acervo, modelo e lista de conferência) e 6 (protocolo de medição) |
| Materiais e Métodos | 1, 2, 3, 4 e 5 (ferramentas, acervo, como cada folder foi feito) |
| Resultados | 5 (a WeasyPrint), 6 (as medições) e 7 (fidelidade e gráficos) |
| Conclusão | `docs/diario.md` acumulado e `docs/recomendacao.md` |

**Nunca apague uma medição, e não mude a lista de conferência depois da Sprint 2.** A confiabilidade do seu trabalho inteiro está nesses dois lugares.
