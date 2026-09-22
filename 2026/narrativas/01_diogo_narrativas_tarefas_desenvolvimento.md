# Plano de tarefas de desenvolvimento – Diogo (Tecnologia em Sistemas para Internet)

**Projeto pai:** Narrativas – plataforma digital para registro, organização e difusão das narrativas populares do Rio Grande do Norte (ver [projeto.md](../projeto.md)).

**Temática escolhida:** 4.3 – Narração automática das narrativas: conversão de texto em áudio (ver [tematicas.md](../tematicas.md)).

**Perfil do aluno:** 1 aluno do Curso Superior de Tecnologia em Sistemas para Internet, com conhecimentos básicos/intermediários em Python, em treinamento. As tarefas são pequenas e detalhadas de propósito: quase todo o código deste trabalho é script curto, e o esforço principal está na **coleta e na análise dos dados**, não na programação.

**Duração:** 8 sprints de 1 semana (22/09/2026 a 16/11/2026).

---

## A ideia do trabalho, em uma página

O protótipo da página de detalhes da plataforma Narrativas já prevê um botão de **"Narração em Áudio"**. Gravar narração humana para um acervo inteiro é inviável: exige estúdio, locutor e horas de trabalho por narrativa. A pergunta que a equipe do projeto vai precisar responder é:

> **A síntese de voz por computador dá conta de narrar narrativas populares em português brasileiro, com termos regionais do sertão potiguar?**

O seu trabalho responde a essa pergunta **com medição**, e não com opinião. Para isso você vai:

1. montar um conjunto de narrativas populares de domínio público (o *corpus*);
2. gerar o áudio de **todas elas em todas as ferramentas** de síntese de voz testadas;
3. medir cada ferramenta em critérios objetivos;
4. entregar um quadro comparativo e uma recomendação para o projeto.

### As ferramentas comparadas

| Ferramenta | Funciona sem internet? | Instalação | Tipo de voz |
|---|---|---|---|
| **gTTS** | Não | `pip install` | Voz do tradutor do Google |
| **pyttsx3** | **Sim** | `pip install` + voz do sistema | Voz do próprio sistema operacional |
| **edge-tts** | Não | `pip install` | Voz neural da Microsoft |
| **Piper** *(opcional)* | **Sim** | download de programa e de modelo | Voz neural, rodando na sua máquina |

As três primeiras são obrigatórias. **O Piper é tarefa extra da Sprint 3**: só comece se as outras três já estiverem gerando áudio. Ele é o mais interessante para o projeto (é o único que junta "sem internet" com "voz neural"), mas exige baixar um executável e um modelo de voz, e não pode atrasar o resto.

### O que vai ser medido

**Medições objetivas — esta é a espinha dorsal do trabalho:**

| O que | Como |
|---|---|
| **Inteligibilidade** | O áudio gerado é transcrito de volta para texto por um programa de reconhecimento de fala, e o texto transcrito é comparado com o original. Quanto mais parecido, mais inteligível foi a fala |
| **Pronúncia de termos regionais** | Lista de 30 palavras ("Boitatá", "Mossoró", "açude", "jerimum"...) — quantas cada ferramenta pronunciou de forma reconhecível |
| **Tempo de geração** | Quantos segundos para gerar o áudio de cada narrativa |
| **Tamanho do arquivo** | Quantos KB por minuto de áudio |
| **Funciona sem internet?** | Testado com a rede desligada |
| **Custo** | Gratuito, limitado ou pago |

**Avaliação com ouvintes — complemento, só se for liberada:** um questionário de 1 a 5 sobre naturalidade e inteligibilidade. Isso envolve pessoas respondendo, e por isso depende de uma definição sobre ética em pesquisa, tratada na Sprint 1. **O trabalho não depende dela para ficar completo** — se ela sair, é um capítulo a mais; se não sair, o TCC se sustenta inteiro nas medições objetivas.

### O que este trabalho **não** é

Não é "fazer a narração do site Narrativas". A plataforma é o **contexto** que justifica a pergunta. O objeto do TCC é a **comparação medida** entre as ferramentas. Escreva isso na Introdução — é o que separa um TCC de um manual de programa.

---

## Decisões técnicas já fechadas

**Você vai criar o seu próprio repositório, público, no GitHub.** Ele é separado do repositório da plataforma Narrativas — nenhuma tarefa deste plano altera o sistema. O endereço vai no seu TCC.

**Não vamos usar Docker.** Tudo é instalado direto na máquina, com `pip` ou download.

**Não precisa de banco de dados.** Este trabalho gera algumas centenas de linhas de medição, e planilha (CSV) resolve melhor do que banco: é mais fácil de conferir, de ordenar e de virar gráfico. A orientação do projeto é usar MySQL **se precisar** — aqui não precisa, e escolher a ferramenta certa para o tamanho do problema também é uma decisão técnica que você pode justificar no TCC.

**Não precisa de Django.** O trabalho é feito com scripts Python de linha de comando.

**Nada de dados pessoais.** As narrativas são de domínio público. Se houver questionário, as respostas são anônimas.

---

## Combinados gerais

- **Commits:** pelo menos 3 por sprint, com mensagem em português dizendo o que foi feito (ex.: `Adiciona script de geracao com edge-tts`).
- **Reunião semanal:** no começo de cada sprint você mostra ao orientador o que fez, **rodando na máquina**. A partir da Sprint 4, é preciso mostrar número.
- **Travou mais de 40 minutos no mesmo erro? Peça ajuda.**
- **Planilha de medições:** a partir da Sprint 4, toda medição vai para `dados/medicoes.csv`. **Nunca apague uma medição.** Se uma rodada saiu estranha, registre e anote o motivo ao lado.
- **Diário:** `docs/diario.md`, três linhas no fim de cada sprint — o que funcionou, o que deu errado, o que aprendi. Isso vira a Conclusão do TCC.
- **Prints:** capturas de tela em `docs/evidencias/`. Vão para o capítulo de Resultados.
- **Os áudios gerados são entregável.** Guarde todos, organizados por ferramenta. Eles são a prova do que você mediu.

---

# Sprint 1 — 22/09 a 28/09/2026
## Repositório, ambiente e o primeiro áudio

**Objetivo:** ao final da semana, ter um repositório público no GitHub e um script Python que transforma um texto em um arquivo de áudio que você consegue ouvir.

E, em paralelo, **destravar a questão da pesquisa com pessoas** — que é o único item deste plano que não depende só de você.

### O que você vai fazer

1. Criar o repositório público no GitHub.
2. Preparar o ambiente Python.
3. Gerar o primeiro áudio com o gTTS.
4. Levar ao orientador a questão do questionário com ouvintes.

### Passo a passo

**1. Criar o repositório.** No GitHub, crie um repositório **público** chamado `narracao-automatica-narrativas` (ou outro nome que combine com o orientador). Marque a opção de criar com um `README.md`. Depois:

```
git clone https://github.com/<seu-usuario>/narracao-automatica-narrativas.git
cd narracao-automatica-narrativas
```

Estrutura de pastas para criar:

```
narracao-automatica-narrativas/
├── corpus/              ← os textos das narrativas e a lista de termos regionais
├── audios/              ← os áudios gerados (uma subpasta por ferramenta)
├── src/                 ← os scripts Python
├── dados/               ← as planilhas de medição
├── docs/
│   ├── diario.md
│   ├── ambiente.md
│   └── evidencias/
├── .gitignore
├── requirements.txt
└── README.md
```

**2. Ambiente virtual.**

```
python -m venv .venv
.venv\Scripts\activate           (Windows)
source .venv/bin/activate        (Linux/Mac)

pip install gtts
pip freeze > requirements.txt
```

**3. O `.gitignore`:**

```
.venv/
__pycache__/
*.pyc
```

> **Atenção:** os áudios **devem** ser comitados — eles são entregável do trabalho e precisam estar no repositório público para que outra pessoa possa ouvi-los. Só cuide para que sejam arquivos de poucos MB cada. Se o total passar de uns 200 MB, fale com o orientador.

**4. O primeiro áudio.** Crie `src/teste_gtts.py`:

```python
from gtts import gTTS

texto = ("Conta-se que, nas noites escuras do sertao, a Boitata aparece "
         "como uma cobra de fogo correndo pelos campos de Mossoro.")

tts = gTTS(text=texto, lang="pt", tld="com.br")
tts.save("audios/teste.mp3")

print("Audio gerado em audios/teste.mp3")
```

Rode com `python src/teste_gtts.py` e **ouça o arquivo**. Preste atenção em como ele pronunciou "Boitatá" e "Mossoró" — é exatamente disso que o seu trabalho trata.

O parâmetro `tld="com.br"` pede o sotaque brasileiro. Teste também sem ele e ouça a diferença: é um detalhe pequeno que já rende observação para o TCC.

**5. Comece o `docs/ambiente.md`** anotando: versão do Python, sistema operacional, processador, memória RAM e tipo de disco da sua máquina, e a velocidade da sua internet (você vai medir ferramentas que dependem de rede — isso vai ter que ser declarado no TCC).

**6. A questão da pesquisa com pessoas — leve isso ao orientador nesta semana.**

O questionário com ouvintes envolve pessoas respondendo, e pesquisas com seres humanos no Brasil podem exigir aprovação de Comitê de Ética em Pesquisa (CEP) e Termo de Consentimento Livre e Esclarecido (TCLE). Aprovação de CEP costuma levar mais tempo do que os dois meses deste trabalho.

Há uma previsão na **Resolução CNS nº 510/2016** que pode dispensar a submissão no caso de pesquisa de opinião pública com participantes não identificados — mas **quem decide isso é o orientador, junto ao CEP da instituição**, e não você nem este documento.

O que você faz nesta sprint: leva a pergunta ao orientador, por escrito, explicando que o questionário seria anônimo, com escala de 1 a 5 sobre a qualidade de áudios gerados por computador, sem coletar nome, e-mail ou qualquer dado que identifique quem responde. Anote a resposta em `docs/diario.md`.

**Enquanto isso, siga o plano normalmente.** As sprints 2 a 5 e 7 não dependem dessa resposta. O questionário está na Sprint 6, e existe plano B caso ele não possa ser aplicado.

### Como saber que deu certo

- [ ] Repositório público criado e clonado, com a estrutura de pastas.
- [ ] `audios/teste.mp3` existe e você conseguiu ouvir.
- [ ] `requirements.txt` e `docs/ambiente.md` comitados.
- [ ] A pergunta sobre ética foi levada ao orientador e a resposta está anotada no diário.
- [ ] Pelo menos 1 commit no GitHub.

### Erros comuns

- **`gTTS` dá erro de conexão:** ele precisa de internet. Confira a rede e o *proxy* do IFRN, se houver.
- **O áudio não abre:** confira se a pasta `audios/` existe antes de rodar o script. O Python não cria a pasta sozinho.

---

# Sprint 2 — 29/09 a 05/10/2026
## Montar o corpus: as narrativas e os termos regionais

**Objetivo:** ter 10 narrativas populares em arquivos de texto e uma lista de 30 termos regionais — tudo com a origem registrada.

Esta sprint tem pouca programação e muita organização. **Não a subestime:** todo o resto do trabalho vai ser feito em cima desses arquivos, e corpus mal montado contamina todos os resultados.

### O que você vai fazer

1. Escolher 10 narrativas de domínio público.
2. Salvar cada uma em um arquivo de texto limpo.
3. Registrar a origem e a licença de cada uma em uma planilha.
4. Montar a lista de 30 termos e nomes regionais.

### Passo a passo

**1. Onde achar narrativas de domínio público.**

Obra no **domínio público** é aquela cujo prazo de proteção já acabou. No Brasil, pela Lei nº 9.610/1998, isso acontece 70 anos depois do primeiro dia do ano seguinte ao da morte do autor.

Fontes recomendadas:

- **Sílvio Romero, *Contos Populares do Brasil* (1883)** — o autor morreu em 1914, então a obra está em domínio público. É a fonte mais indicada para este trabalho;
- **Lindolfo Gomes, *Contos Populares Brasileiros* (1918)** — autor falecido em 1953, também em domínio público;
- **Portal Domínio Público** (`dominiopublico.gov.br`), **Wikisource** e **Projeto Gutenberg**.

> **Cuidado importante:** as obras de **Luís da Câmara Cascudo** ainda **não** estão em domínio público — ele faleceu em 1986. Por mais que sejam a referência natural quando se fala em folclore potiguar, você não pode reproduzir os textos dele no corpus. Cite-o no Referencial Teórico como autor, o que é perfeitamente normal e recomendável, mas não use os textos como material de teste.

**Outra opção, que vale conversar com o orientador:** narrativas coletadas ou escritas pela própria equipe do projeto Narrativas, com autorização registrada.

**2. O que escolher.** Dez narrativas, com estas características:

- entre **200 e 400 palavras** cada (áudio de 1 a 3 minutos — suficiente para avaliar e curto o bastante para alguém ouvir no questionário);
- variadas: escolha algumas com muitos nomes próprios e termos regionais, e outras mais "neutras". Assim dá para ver se a ferramenta se sai pior justamente nas que têm mais vocabulário local — e essa comparação é um resultado;
- se possível, com ligação ao Nordeste ou ao Rio Grande do Norte, para casar com o projeto.

**3. Limpar e salvar os textos.** Salve cada narrativa em `corpus/narrativa_01.txt` até `narrativa_10.txt`, em **UTF-8**, e limpe antes de salvar:

- tire números de página, notas de rodapé e cabeçalhos que vieram junto na cópia;
- tire quebras de linha no meio das frases (texto copiado de PDF vem cheio delas);
- confira a acentuação: textos digitalizados antigos costumam vir com erro de reconhecimento de caracteres;
- **mantenha a pontuação.** A vírgula e o ponto são o que dizem ao sintetizador onde pausar. Tirar a pontuação mudaria o resultado.

Anote quantas palavras tem cada texto — você vai precisar desse número para calcular tempo por palavra.

**4. A planilha de origem.** Crie `corpus/origem.csv`, com uma linha por narrativa:

```
arquivo,titulo,autor_ou_coletor,obra,ano,fonte_url,situacao_direitos,palavras
narrativa_01.txt,...,Silvio Romero,Contos Populares do Brasil,1883,...,dominio publico,312
```

**Esta planilha vai direto para o capítulo de Materiais e Métodos do TCC.** Sem ela, você não tem como provar que usou material que podia usar.

**5. A lista de termos regionais.** Crie `corpus/termos_regionais.csv`. São 30 palavras que serão faladas isoladamente por cada ferramenta, para testar a pronúncia. Sugestão de categorias:

| Categoria | Exemplos |
|---|---|
| Seres do folclore | Boitatá, Caipora, Curupira, Saci-Pererê, Mula sem cabeça, Cuca |
| Cidades do RN | Mossoró, Caicó, Açu, Apodi, Ceará-Mirim, Currais Novos, Pau dos Ferros |
| Regiões e natureza | Seridó, sertão, agreste, caatinga, açude, mandacaru, xique-xique, juazeiro |
| Cultura e história | cangaço, Lampião, forró, xaxado, aboio, vaquejada, repente |
| Comida e dia a dia | rapadura, jerimum, macaxeira, tapioca, buchada |

O arquivo fica assim:

```
termo,categoria
Boitata,folclore
Mossoro,cidade
```

> **Detalhe que importa:** no CSV, escreva os termos **com acento** (`Boitatá`, `Mossoró`). O acento é parte do problema que você está estudando — é ele que diz ao sintetizador onde fica a sílaba tônica. O exemplo acima está sem acento só por limitação desta página.

**6. Escreva também, ao lado de cada termo, como ele deve soar.** Isso vai ser útil na Sprint 6, quando você for julgar se a pronúncia saiu certa. Pode ser uma coluna a mais, bem informal: `Boitatá → boi-ta-TÁ`.

### Como saber que deu certo

- [ ] 10 arquivos `.txt` em `corpus/`, em UTF-8, limpos e com pontuação preservada.
- [ ] `corpus/origem.csv` preenchido, com a situação de direitos de cada texto.
- [ ] `corpus/termos_regionais.csv` com 30 termos.
- [ ] Nenhum texto de autor ainda protegido por direitos autorais.

### Erros comuns

- **Acentos quebrados (`Mossor├│`):** o arquivo não foi salvo em UTF-8. No VS Code, o canto inferior direito mostra a codificação; clique nela e escolha "Salvar com codificação → UTF-8".
- **Texto com quebras de linha no meio das frases:** veio de PDF. Use Localizar e Substituir para juntar.
- **Escolher textos longos demais:** um texto de 2.000 palavras vira um áudio de 15 minutos que ninguém vai ouvir no questionário.

---

# Sprint 3 — 06/10 a 12/10/2026
## Fazer as três ferramentas gerarem áudio

**Objetivo:** ter as três ferramentas instaladas e funcionando, cada uma gerando o áudio das mesmas 10 narrativas.

### O que você vai fazer

1. Instalar e testar o pyttsx3 (o que funciona sem internet).
2. Instalar e testar o edge-tts.
3. Escrever um script que gera tudo de uma vez, para as três.
4. **Tarefa extra, só se sobrar tempo:** instalar o Piper.

### Passo a passo

**1. pyttsx3 — a voz do próprio sistema operacional.**

```
pip install pyttsx3
```

Este é o único que funciona **sem internet**, porque usa as vozes instaladas no seu computador. O problema é justamente esse: se não houver voz em português instalada, ele vai ler o texto português com sotaque inglês, e o resultado fica impossível de entender.

Primeiro descubra quais vozes existem na sua máquina:

```python
import pyttsx3

motor = pyttsx3.init()
for voz in motor.getProperty("voices"):
    print(voz.id)
    print("   nome:", voz.name)
```

Procure uma que tenha `pt` ou `Brazil` no nome. **Se não existir nenhuma**, no Windows você instala assim: *Configurações → Hora e Idioma → Idioma e Região → Adicionar idioma → Português (Brasil)* e, nas opções desse idioma, instale o pacote de **Fala**. Depois reinicie o computador e rode o script de novo.

Com a voz encontrada, gere o áudio:

```python
import pyttsx3

motor = pyttsx3.init()
motor.setProperty("voice", "COLE_AQUI_O_ID_DA_VOZ")
motor.setProperty("rate", 170)      # velocidade da fala

motor.save_to_file("A Boitata apareceu no acude de Mossoro.", "audios/pyttsx3/teste.wav")
motor.runAndWait()
```

**Anote no diário** qual voz você usou e se precisou instalar. Isso vai para o TCC: é uma **limitação importante** dessa ferramenta, porque significa que o resultado depende da máquina onde ela roda.

**2. edge-tts — voz neural da Microsoft.**

```
pip install edge-tts
```

Teste primeiro pelo terminal, que é mais fácil:

```
edge-tts --voice pt-BR-FranciscaNeural --text "A Boitata apareceu no acude de Mossoro." --write-media audios/edgetts/teste.mp3
```

Para ver todas as vozes em português disponíveis:

```
edge-tts --list-voices
```

Procure as que começam com `pt-BR`. As duas principais são `pt-BR-FranciscaNeural` (feminina) e `pt-BR-AntonioNeural` (masculina). **Escolha uma e use a mesma em todas as narrativas** — trocar de voz no meio invalidaria a comparação.

Em Python, o edge-tts usa programação assíncrona, que talvez você ainda não tenha visto. Não precisa entender agora; use o modelo pronto:

```python
import asyncio
import edge_tts


async def gerar(texto, caminho):
    comunicador = edge_tts.Communicate(texto, "pt-BR-FranciscaNeural")
    await comunicador.save(caminho)


asyncio.run(gerar("A Boitata apareceu no acude de Mossoro.",
                  "audios/edgetts/teste.mp3"))
```

**3. O script que gera tudo.** Agora junte as três em `src/gerar_audios.py`. A ideia é: para cada uma das 10 narrativas, gerar o áudio nas três ferramentas, salvando em pastas separadas com o mesmo nome de arquivo.

```python
import os
import time
import csv

CORPUS = "corpus"
FERRAMENTAS = ["gtts", "pyttsx3", "edgetts"]


def ler_texto(caminho):
    with open(caminho, encoding="utf-8") as arquivo:
        return arquivo.read()


def gerar_com_gtts(texto, saida):
    from gtts import gTTS
    gTTS(text=texto, lang="pt", tld="com.br").save(saida)


# ... uma funcao por ferramenta ...


def main():
    for ferramenta in FERRAMENTAS:
        os.makedirs(f"audios/{ferramenta}", exist_ok=True)

    for numero in range(1, 11):
        nome = f"narrativa_{numero:02d}"
        texto = ler_texto(f"{CORPUS}/{nome}.txt")

        for ferramenta in FERRAMENTAS:
            extensao = "wav" if ferramenta == "pyttsx3" else "mp3"
            saida = f"audios/{ferramenta}/{nome}.{extensao}"
            print(f"Gerando {saida} ...")
            # chama a funcao da ferramenta


if __name__ == "__main__":
    main()
```

Organize os áudios exatamente assim, porque as próximas sprints dependem desses caminhos:

```
audios/
├── gtts/narrativa_01.mp3 ... narrativa_10.mp3
├── pyttsx3/narrativa_01.wav ... narrativa_10.wav
└── edgetts/narrativa_01.mp3 ... narrativa_10.mp3
```

**4. Ouça pelo menos três áudios de cada ferramenta.** Não passe para a próxima sprint sem ouvir. Se algum ficou mudo, cortado ou com a voz errada, é melhor descobrir agora. Anote no diário a sua primeira impressão de cada ferramenta — ela vai ser interessante de comparar com o que os números disserem depois.

**5. Tarefa extra: Piper — só se as três anteriores já estiverem prontas.**

O Piper roda **sem internet** e com **voz neural**, o que o torna o mais interessante dos quatro para o projeto. Em compensação, ele não se instala só com `pip`: é preciso baixar o programa e um modelo de voz.

- baixe o executável do Piper na página de *releases* do projeto `rhasspy/piper` no GitHub, escolhendo a versão do seu sistema operacional;
- baixe um modelo de voz em português do Brasil. São dois arquivos que andam juntos: um `.onnx` e um `.onnx.json`. Procure por vozes `pt_BR` na página de vozes do projeto;
- descompacte tudo em uma pasta `piper/` dentro do repositório, e **acrescente essa pasta ao `.gitignore`** (são arquivos grandes demais para o Git).

Uso pelo terminal:

```
echo "A Boitata apareceu no acude de Mossoro." | piper --model pt_BR-faber-medium.onnx --output_file audios/piper/teste.wav
```

**Se travar em qualquer ponto, pare e siga sem o Piper.** Ele é um item a mais, não um requisito. Se você o deixar de fora, escreva no TCC que ele foi identificado como alternativa promissora e ficou como trabalho futuro — isso é uma limitação declarada, e limitação declarada não tira valor do trabalho.

### Como saber que deu certo

- [ ] As três ferramentas geram áudio em português.
- [ ] 30 arquivos de áudio gerados (10 narrativas × 3 ferramentas).
- [ ] Você ouviu pelo menos 3 de cada e eles estão inteiros.
- [ ] A voz usada em cada ferramenta está anotada em `docs/ambiente.md`.
- [ ] Áudios comitados no repositório.

### Erros comuns

- **pyttsx3 lendo português com sotaque inglês:** não há voz em português instalada no sistema. Veja o passo 1.
- **pyttsx3 gerando arquivo vazio:** faltou o `motor.runAndWait()` depois do `save_to_file`.
- **edge-tts dando erro de conexão:** ele precisa de internet, como o gTTS.
- **Erro de "arquivo ou diretório não encontrado":** a pasta de saída não existe. Use `os.makedirs(..., exist_ok=True)`.

---

# Sprint 4 — 13/10 a 19/10/2026
## Medir tempo, tamanho e funcionamento sem internet

**Objetivo:** ter a primeira tabela de resultados do seu TCC.

### O que você vai fazer

1. Definir e escrever o protocolo de medição.
2. Medir o tempo de geração de cada ferramenta, com repetições.
3. Medir o tamanho e a duração dos áudios.
4. Testar o funcionamento com a internet desligada.
5. Levantar o custo e os limites de uso de cada ferramenta.

### Passo a passo

**1. O protocolo de medição.** Antes de medir, escreva em `docs/protocolo.md` como você vai medir — e depois siga igual todas as vezes. Sugestão:

1. computador ligado na tomada, não na bateria (no modo bateria o processador reduz a velocidade);
2. fechar navegador e tudo mais que estiver pesado;
3. usar a mesma conexão de internet em todas as medições, e anotar qual é;
4. gerar cada áudio **3 vezes** e usar a média dos três tempos;
5. rodar uma vez antes "para aquecer" e descartar esse resultado;
6. anotar a data e a hora de cada rodada.

**Por que 3 repetições?** Porque uma medição sozinha pode sair distorcida: o antivírus rodou, a internet oscilou, o sistema resolveu atualizar. Média de três é o mínimo razoável, e apresentar isso no TCC é o que separa medição de chute.

**2. Medir o tempo.** Use `time.perf_counter()`, que é mais preciso que `time.time()` para medir duração:

```python
import time

inicio = time.perf_counter()
gerar_com_gtts(texto, saida)
duracao = time.perf_counter() - inicio

print(f"Levou {duracao:.2f} segundos")
```

**Cuidado com uma comparação injusta:** gTTS e edge-tts dependem da internet, e o pyttsx3 não. Parte do tempo dos dois primeiros é tempo de rede, não de processamento. **Isso não é um problema do seu trabalho — é um dos resultados dele.** Mas precisa estar escrito com todas as letras no TCC, porque é a explicação de por que os números são o que são.

**3. Medir tamanho e duração.** O tamanho do arquivo vem direto do sistema:

```python
import os

tamanho_kb = os.path.getsize(caminho) / 1024
```

Para a duração do áudio em segundos, instale:

```
pip install mutagen
```

```python
from mutagen import File

audio = File(caminho)
duracao_segundos = audio.info.length
```

**Uma ressalva que você precisa registrar:** as ferramentas geram em formatos diferentes — o pyttsx3 salva em WAV (sem compressão, arquivos grandes) e as outras em MP3 (comprimido). Comparar o tamanho bruto entre elas é comparar coisas diferentes. Por isso, apresente no TCC **duas colunas**: o tamanho no formato nativo e o tamanho **por minuto de áudio** (KB/min), que é a comparação mais justa. E explique a diferença de formato no texto.

**4. Testar sem internet.** Desligue o Wi-Fi (ou tire o cabo) e rode o script de geração de novo. Anote, para cada ferramenta: funcionou, funcionou parcialmente ou deu erro — e **qual erro apareceu**. Tire print da mensagem de erro; ela vira figura no capítulo de Resultados.

Este é um critério decisivo para o projeto Narrativas: se a plataforma for gerar narração no servidor, depender de um serviço externo significa que a funcionalidade cai quando o serviço cai.

**5. Levantar custo e limites.** Consulte a documentação oficial de cada ferramenta e anote: é gratuita? tem limite de uso por dia ou por requisição? os termos de uso permitem uso institucional? **Guarde o endereço e a data de consulta** — você vai precisar citar isso no TCC, e termos de serviço mudam.

**6. A planilha de medições.** Crie `dados/medicoes.csv`:

```
data,ferramenta,narrativa,repeticao,palavras,tempo_seg,tamanho_kb,duracao_seg,formato,observacao
```

São 10 narrativas × 3 ferramentas × 3 repetições = **90 linhas**. Deixe o script preencher sozinho: escrever 90 linhas à mão é onde o erro entra.

### Como saber que deu certo

- [ ] `docs/protocolo.md` escrito.
- [ ] `dados/medicoes.csv` com as 90 linhas.
- [ ] Teste sem internet feito, com print dos erros.
- [ ] Tabela de custo e limites preenchida, com data de consulta.
- [ ] Primeira tabela de resultados montada: tempo médio, tamanho por minuto e funcionamento offline, por ferramenta.

### Erros comuns

- **Tempos muito diferentes entre as 3 repetições:** provavelmente a internet oscilou. Refaça, e se continuar, registre a variação — ela também é um resultado (significa que a ferramenta é instável).
- **`mutagen` não lê o WAV:** para WAV, dá para calcular a duração com o módulo `wave`, que já vem com o Python.

---

# Sprint 5 — 20/10 a 26/10/2026
## Medir a inteligibilidade automaticamente

**Objetivo:** medir, sem depender de ninguém responder questionário, o quanto cada ferramenta foi compreensível.

### A ideia, explicada

Você não tem como perguntar a um computador "essa voz está boa?". Mas tem como fazer o seguinte, que é o método central deste trabalho:

```
texto original  →  [ferramenta de voz]  →  áudio  →  [reconhecimento de fala]  →  texto transcrito
```

Se o texto transcrito no fim for igual ao original, é sinal de que a fala saiu clara o suficiente para ser reconhecida. Se vier cheio de palavra trocada, é sinal de que a pronúncia ficou ruim. A medida disso chama-se **taxa de erro de palavras** (*Word Error Rate*, WER): quanto menor, melhor.

**Isso é um indício, não uma prova.** O programa de reconhecimento de fala tem os erros dele, e foi treinado com voz humana. Essa limitação precisa estar escrita no TCC — e é justamente ela que justifica o questionário com pessoas como complemento.

### O que você vai fazer

1. Instalar o programa de reconhecimento de fala.
2. Transcrever os 30 áudios.
3. Comparar cada transcrição com o texto original e calcular a taxa de erro.
4. Montar a tabela.

### Passo a passo

**1. Instalar.**

```
pip install faster-whisper jiwer
```

O `faster-whisper` transcreve áudio em texto e roda na sua máquina, sem internet depois de baixar o modelo. O `jiwer` calcula a taxa de erro.

**2. Transcrever.**

```python
from faster_whisper import WhisperModel

modelo = WhisperModel("small", device="cpu", compute_type="int8")

segmentos, info = modelo.transcribe("audios/gtts/narrativa_01.mp3", language="pt")
transcricao = " ".join(s.text for s in segmentos)
print(transcricao)
```

Na primeira execução ele baixa o modelo (algumas centenas de MB) — isso é normal e acontece uma vez só. Se a sua máquina for lenta, troque `"small"` por `"base"`. **Use o mesmo modelo para todas as ferramentas**, senão a comparação não vale; anote qual usou em `docs/ambiente.md`.

**3. Normalizar antes de comparar.** O programa de transcrição escreve "Boitatá" e o texto original pode ter "boitatá"; a pontuação também não vai bater. Comparar sem normalizar contaria como erro coisa que não é erro. Então, antes de comparar, passe os dois textos por uma função simples:

```python
import re
import unicodedata


def normalizar(texto):
    texto = texto.lower()
    texto = re.sub(r"[^\w\s]", " ", texto)      # tira pontuacao
    texto = re.sub(r"\s+", " ", texto)          # espacos sobrando
    return texto.strip()
```

**Decisão a tomar e registrar:** você vai comparar **com** ou **sem** acento? As duas opções se defendem. Comparar sem acento é mais generoso com as ferramentas; comparar com acento é mais rigoroso. Escolha uma, use a mesma para todas as ferramentas e **escreva a escolha na Metodologia**, com a justificativa. Se quiser, apresente os dois números — dá uma discussão boa.

**4. Calcular a taxa de erro.**

```python
import jiwer

taxa_palavras = jiwer.wer(texto_original_normalizado, transcricao_normalizada)
taxa_caracteres = jiwer.cer(texto_original_normalizado, transcricao_normalizada)

print(f"WER: {taxa_palavras:.2%}   CER: {taxa_caracteres:.2%}")
```

O **WER** conta palavras erradas; o **CER** conta caracteres errados. Apresente os dois: às vezes a ferramenta erra só um pedaço da palavra, e o CER mostra isso melhor.

**5. Rodar para tudo e salvar.** Crie `src/medir_inteligibilidade.py`, que percorre as 30 combinações e grava `dados/inteligibilidade.csv`:

```
ferramenta,narrativa,palavras,wer,cer,transcricao
```

**Guarde a transcrição inteira na planilha.** Ela é ouro para o TCC: dá para mostrar exemplos concretos de erro ("o sintetizador falou *Mossoro* e a transcrição entendeu *Mossoró*" ou "*boi tatá*" virou "*boi ta tá*"). Exemplo concreto vale mais que qualquer tabela.

### Como saber que deu certo

- [ ] `dados/inteligibilidade.csv` com 30 linhas.
- [ ] Tabela com WER e CER médios por ferramenta.
- [ ] Pelo menos 5 exemplos concretos de erro anotados para usar no texto.
- [ ] A decisão sobre acentos está registrada e foi aplicada igualmente a todas.

### Erros comuns

- **A transcrição sai em outra língua:** faltou `language="pt"`.
- **Taxa de erro altíssima em todas as ferramentas:** quase sempre é falta de normalização. Confira imprimindo os dois textos lado a lado antes de comparar.
- **Demora demais:** use o modelo `"base"` em vez de `"small"` — mas então refaça **todas** as transcrições com ele.

---

# Sprint 6 — 27/10 a 02/11/2026
## Pronúncia dos termos regionais (e o questionário, se liberado)

**Objetivo:** responder à pergunta mais interessante do trabalho — as ferramentas dão conta do vocabulário do sertão?

### O que você vai fazer

1. Gerar o áudio dos 30 termos regionais em cada ferramenta.
2. Verificar a pronúncia de dois jeitos: automático e ouvindo.
3. Montar a tabela de acertos por ferramenta e por categoria.
4. **Se a questão ética foi resolvida:** montar e aplicar o questionário.

### Passo a passo

**1. Gerar os termos.** Escreva `src/gerar_termos.py`, que lê `corpus/termos_regionais.csv` e gera um áudio por termo, por ferramenta:

```
audios/termos/gtts/boitata.mp3
audios/termos/pyttsx3/boitata.wav
audios/termos/edgetts/boitata.mp3
```

São 30 × 3 = **90 áudios curtos**.

**Dica prática:** gerar a palavra sozinha pode dar resultado diferente de gerá-la dentro de uma frase, porque o sintetizador usa o contexto. O ideal é gerar as duas formas — a palavra isolada e uma frase curta que a contenha ("A Boitatá apareceu no açude."). Se o tempo apertar, fique só com a frase, que é a situação mais parecida com o uso real.

**2. Verificação automática.** Transcreva cada áudio de termo com o `faster-whisper`, igual à sprint passada, e veja se o termo apareceu corretamente na transcrição. Isso dá uma medida objetiva e rápida dos 90 áudios.

**3. Verificação ouvindo — e esta você faz pessoalmente.** Ouça os 90 áudios e classifique cada um em três níveis:

| Nota | Significado |
|---|---|
| 2 | Pronúncia correta |
| 1 | Reconhecível, mas com erro (sílaba tônica errada, som trocado) |
| 0 | Irreconhecível ou lido letra por letra |

Registre em `dados/pronuncia.csv`:

```
termo,categoria,ferramenta,nota_ouvindo,transcricao_automatica,acertou_automatico,observacao
```

Na coluna de observação, descreva o erro: "leu 'Mossoró' como 'Mossôro'", "leu 'xique-xique' letra por letra", "acentuou 'Boitatá' na sílaba errada". **São essas observações que vão fazer o seu capítulo de Resultados ser interessante**, porque mostram *que tipo* de erro cada ferramenta comete, não só quantos.

> **Sobre você mesmo avaliar:** isso se chama avaliação do próprio pesquisador, e precisa ser declarado no TCC como uma limitação — você sabe qual ferramenta gerou cada áudio, e isso pode influenciar o julgamento. Duas coisas reduzem o problema e valem a pena: **embaralhe os arquivos** e avalie sem olhar de qual pasta vieram (renomeie para `audio_001`, `audio_002`... com uma tabela de correspondência guardada à parte), e **apresente junto a verificação automática**, que não tem esse viés.

**4. A tabela de resultados.** Monte duas:

- acertos por **ferramenta**: quantos dos 30 termos cada uma pronunciou bem;
- acertos por **categoria**: as ferramentas erram mais em nomes de cidade, em seres do folclore ou em comida? Essa quebra costuma revelar padrão interessante.

**5. O questionário — só se o orientador liberou.**

Se a questão ética da Sprint 1 foi resolvida favoravelmente, monte o questionário no Google Forms:

- **anônimo**: nada de nome, e-mail ou matrícula. Se o Forms estiver configurado para coletar e-mail, desligue essa opção;
- texto de abertura explicando o que é a pesquisa, que é voluntária, anônima, e que a pessoa pode desistir a qualquer momento — conforme o que o orientador orientar;
- **3 narrativas**, cada uma nas 3 ferramentas = 9 áudios. Não coloque as 10 narrativas: ninguém termina um questionário de 30 áudios;
- **não diga qual ferramenta gerou qual áudio.** Chame de "Áudio A", "Áudio B", "Áudio C", e **embaralhe a ordem** entre as narrativas;
- para cada áudio, duas perguntas em escala de 1 a 5: **naturalidade** ("o quanto soou como uma pessoa falando") e **inteligibilidade** ("o quanto foi fácil entender");
- uma pergunta aberta ao final: "alguma palavra você não entendeu ou achou mal pronunciada?";
- hospede os áudios no Google Drive e coloque os links no formulário, ou use a opção de anexar arquivo de áudio;
- **meta: 20 a 30 respostas.** Colegas de turma, professores e pessoas do projeto. Menos que isso não sustenta média.

Essa escala de 1 a 5 é o método padrão de avaliação de qualidade de voz, chamado de **MOS** (*Mean Opinion Score*) — cite isso na Metodologia, com a referência da recomendação ITU-T P.800.

**Se o questionário não puder ser aplicado:** siga sem ele. Escreva no TCC, na Metodologia e nas Limitações, que a avaliação subjetiva não foi realizada por questões de prazo e de procedimento ético, e que fica como trabalho futuro. **O trabalho continua completo** — ele tem WER, CER, pronúncia, tempo, tamanho e funcionamento offline. Muitos artigos publicados se sustentam com menos do que isso.

### Como saber que deu certo

- [ ] 90 áudios de termos gerados.
- [ ] `dados/pronuncia.csv` preenchido, com verificação automática e ouvindo.
- [ ] Pelo menos 10 observações descrevendo erros concretos de pronúncia.
- [ ] Tabela de acertos por ferramenta e por categoria.
- [ ] Questionário aplicado **ou** decisão registrada de não aplicá-lo.

---

# Sprint 7 — 03/11 a 09/11/2026
## Juntar tudo, fazer os gráficos e analisar

**Objetivo:** transformar quatro planilhas em tabelas e gráficos que respondem à pergunta do trabalho.

### O que você vai fazer

1. Tabular as respostas do questionário, se houver.
2. Consolidar todas as medições em uma tabela única.
3. Fazer os gráficos.
4. Procurar os cruzamentos interessantes.

### Passo a passo

**1. Tabular o questionário, se houve.** O Google Forms exporta as respostas para planilha. Para cada ferramenta, calcule a **média** e o **desvio padrão** das notas de naturalidade e de inteligibilidade. Informe também quantas pessoas responderam.

Leia as respostas da pergunta aberta uma a uma e agrupe por assunto ("acharam a voz robótica", "não entenderam o nome da cidade"). Duas ou três frases de participantes, citadas no TCC, valem muito — desde que sem qualquer identificação.

**2. A tabela consolidada.** Esta é a tabela principal do seu trabalho:

| Ferramenta | WER médio | CER médio | Termos corretos (de 30) | Tempo médio (s) | KB por minuto | Funciona offline | Custo | MOS naturalidade | MOS inteligibilidade |
|---|---|---|---|---|---|---|---|---|---|
| gTTS | | | | | | Não | | | |
| pyttsx3 | | | | | | Sim | | | |
| edge-tts | | | | | | Não | | | |
| Piper | | | | | | Sim | | | |

As duas últimas colunas só existem se o questionário tiver sido aplicado; a linha do Piper, só se ele tiver sido feito.

**3. Os gráficos.** Use o Google Sheets ou o Excel — não precisa de programação. Faça três ou quatro:

- barras: WER médio por ferramenta (quanto menor, melhor — diga isso na legenda);
- barras: termos regionais corretos por ferramenta;
- barras agrupadas: acerto por categoria de termo (folclore, cidade, natureza...), uma cor por ferramenta;
- barras: tempo médio de geração por ferramenta;
- se houve questionário: barras com a média MOS e a barra de erro do desvio padrão.

Cuidados: unidade no eixo; se o eixo vertical não começar em zero, avise na legenda; mesma cor para a mesma ferramenta em todos os gráficos.

**4. Procure os cruzamentos — é aqui que o trabalho fica bom.** Não basta apresentar as tabelas; é preciso perguntar coisas a elas:

- **a ferramenta mais rápida é a mais compreensível?** Quase certamente não. Se houver um compromisso entre velocidade e qualidade, isso é um resultado;
- **a ferramenta offline perde muito?** Esta é a pergunta que mais interessa ao projeto Narrativas. Se o pyttsx3 for muito pior, a conclusão prática é que a plataforma vai depender de serviço externo — ou do Piper;
- **os erros se concentram nos termos regionais?** Compare o WER das narrativas com mais termos locais com o das mais neutras. Se a diferença existir, você acabou de confirmar a hipótese central da temática;
- **em que categoria todas erram?** Se as três ferramentas erram nos mesmos termos, o problema não é da ferramenta, é do vocabulário — e a recomendação para o projeto muda: seria preciso um dicionário de pronúncia, não trocar de ferramenta;
- **o que os números dizem que os ouvintes não disseram, e vice-versa?** Se o WER de uma ferramenta é ótimo mas as pessoas acharam a voz desagradável, os dois métodos estão medindo coisas diferentes — e explicar isso é uma discussão de alto nível.

**5. Anote cada achado em `docs/resultados.md`**, em uma frase, com o número que o sustenta. Esse arquivo vira o rascunho do capítulo de Resultados.

### Como saber que deu certo

- [ ] Tabela consolidada preenchida.
- [ ] 3 a 5 gráficos prontos.
- [ ] Questionário tabulado (se houve), com média, desvio padrão e número de respondentes.
- [ ] Pelo menos 5 achados escritos em `docs/resultados.md`, cada um com o número que o comprova.

---

# Sprint 8 — 10/11 a 16/11/2026
## Recomendação, documentação e fechamento

**Objetivo:** transformar os números em uma resposta para o projeto Narrativas, e deixar tudo reproduzível.

### O que você vai fazer

1. Escrever o quadro comparativo final e a recomendação.
2. Escrever o `README.md` do repositório.
3. Organizar os entregáveis.
4. Montar a apresentação.

### Passo a passo

**1. O quadro comparativo e a recomendação.** Esta é a contribuição prática do seu trabalho. Monte um quadro com uma linha por ferramenta e colunas de **pontos fortes**, **pontos fracos**, **quando usar** e **quando não usar**.

E então responda, em um parágrafo direto, à pergunta do projeto:

- a narração automática é viável para o acervo Narrativas? Em que condições?
- qual ferramenta você recomenda, e por quê?
- o que ainda precisaria ser resolvido antes de usar em produção? (Provavelmente a pronúncia de nomes regionais — e aí cabe sugerir um dicionário de pronúncia para os termos que todas erraram.)
- ou a conclusão é que, para este acervo, a narração precisa ser humana?

**Qualquer uma dessas respostas é um bom resultado, inclusive a última.** Um trabalho que conclui "não dá, e aqui está a medição que mostra por quê" é tão útil para o projeto quanto um que conclui o contrário. Não force um resultado positivo.

**2. O `README.md` do repositório.** Como o repositório é público e vai ser citado no TCC, ele precisa permitir que outra pessoa repita o trabalho:

- o que é o projeto e a que trabalho pertence (com o vínculo ao projeto Narrativas);
- o que instalar, com as versões;
- como preparar o ambiente (`pip install -r requirements.txt`);
- de onde vieram os textos do corpus e qual a situação de direitos autorais;
- como rodar cada script, na ordem;
- o que tem em cada pasta;
- onde estão as medições e os resultados;
- a licença do repositório (combine com o orientador; para trabalho acadêmico, MIT ou Creative Commons são escolhas comuns).

**3. Organizar os entregáveis.** A temática pede quatro coisas — confira se todas estão no repositório:

| Entregável | Onde está |
|---|---|
| Os áudios gerados | `audios/` |
| O questionário e as respostas tabuladas | `dados/` (ou a declaração de que não foi aplicado) |
| O quadro comparativo | `docs/resultados.md` e o TCC |
| A recomendação | `docs/resultados.md` e o TCC |

**4. Revisar o código.** Confira que os scripts têm nomes claros, que cada um tem um comentário no topo dizendo o que faz e em que ordem deve ser rodado, e que não sobrou código morto nem caminho fixo da sua máquina (`C:\Users\...`) dentro do código.

**5. A apresentação** (8 a 10 slides): o problema, o corpus, as ferramentas, como você mediu, a tabela principal, dois ou três gráficos, exemplos de erro de pronúncia (**com o áudio, se der para tocar** — é o que mais impressiona em apresentação deste tema), e a recomendação.

### Como saber que deu certo

- [ ] Quadro comparativo e recomendação escritos.
- [ ] `README.md` permite que outra pessoa repita o trabalho.
- [ ] Repositório público, organizado, com os áudios dentro.
- [ ] Os quatro entregáveis da temática estão no lugar.
- [ ] Apresentação montada.

---

## Quadro-resumo das sprints

| Sprint | Período | O que entrega | O que aprende |
|---|---|---|---|
| 1 | 22/09 a 28/09 | Repositório público e o primeiro áudio | ambiente, Git, gTTS, a questão ética |
| 2 | 29/09 a 05/10 | Corpus de 10 narrativas e 30 termos | domínio público, licença, preparo de dados |
| 3 | 06/10 a 12/10 | As 3 ferramentas gerando áudio | pyttsx3, edge-tts, vozes do sistema |
| 4 | 13/10 a 19/10 | Tempo, tamanho, offline e custo | protocolo de medição, repetições |
| 5 | 20/10 a 26/10 | Inteligibilidade medida (WER e CER) | reconhecimento de fala, normalização de texto |
| 6 | 27/10 a 02/11 | Pronúncia dos termos (e questionário) | avaliação cega, escala MOS |
| 7 | 03/11 a 09/11 | Tabelas, gráficos e análise | cruzamento de dados |
| 8 | 10/11 a 16/11 | Recomendação e documentação | síntese e reprodutibilidade |

---

## Se algo der errado no cronograma

| Problema | O que fazer |
|---|---|
| Não há voz em português no sistema para o pyttsx3 | Veja o passo da Sprint 3. Se não resolver, registre como limitação e teste em outra máquina |
| Questão ética não resolvida | Siga sem questionário. O plano já foi montado para isso |
| Piper não instala | Deixe de fora. Ele é tarefa extra, e vira trabalho futuro no TCC |
| `faster-whisper` roda lento demais | Use o modelo `base` em vez de `small`, e refaça **todas** as transcrições com ele |
| Poucas respostas no questionário | Reporte o número real e trate como limitação. Não invente resposta, em nenhuma hipótese |
| Atraso geral | Corte o Piper e a geração dos termos isolados (fique só com os termos dentro de frase). Não corte as repetições das medições |

**Se precisar cortar, corte quantidade, não qualidade.** Três ferramentas bem medidas valem mais que quatro medidas de qualquer jeito.

---

## Se sobrar tempo (opcional)

- **E1.** Testar mais de uma voz da mesma ferramenta (masculina e feminina do edge-tts) e ver se a pronúncia dos termos muda.
- **E2.** Testar se "ensinar" a pronúncia resolve: escrever `Boitatá` como `Boi-ta-tá` no texto de entrada e ver se o áudio melhora. Se funcionar, isso vira uma recomendação muito concreta para o projeto.
- **E3.** Medir quanto tempo levaria para narrar o acervo inteiro, projetando a partir do tempo médio por palavra.
- **E4.** Comparar o áudio sintetizado com uma gravação humana da mesma narrativa (você mesmo lendo), para ter uma referência de quanto as ferramentas ainda estão distantes.

---

## Relação com o TCC

O desenvolvimento e a escrita andam juntos (ver `01_diogo_narrativas_tarefas_escrita.md`):

| Capítulo do TCC | De onde vem o conteúdo |
|---|---|
| Referencial Teórico | as leituras das Sprints 2 a 6 (tradição oral, síntese de voz, acessibilidade, MOS) |
| Metodologia | o protocolo da Sprint 4 e o método de medição da Sprint 5 |
| Materiais e Métodos | Sprints 1, 2 e 3 (ferramentas, versões, corpus, máquina) |
| Resultados | Sprints 4, 5, 6 e 7 |
| Conclusão | o `docs/diario.md` e a recomendação da Sprint 8 |

**Nunca apague uma medição das planilhas.** Rodada estranha vira observação no TCC, não lixo.
