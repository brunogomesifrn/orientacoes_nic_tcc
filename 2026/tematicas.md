# PROJETO NARRATIVAS
## Ítalo, Gleidson e Samuel (INFO4)
### Busca textual no acervo de narrativas
- As narrativas são textos longos. Quando o acervo crescer, a busca por palavra-chave feita com LIKE '%palavra%' (a saída mais comum para quem está começando) fica lenta e traz resultados ruins, principalmente com acentuação e plurais. O aluno monta uma base de teste com centenas de narrativas e mede o comportamento de cada estratégia de busca.
- Deverá Comparar, sobre a mesma base:
    - LIKE/icontains do ORM do Django, sem índice;
    - o mesmo, com índice criado no banco;
    - busca em texto completo com o FTS5 do SQLite (já vem embutido, não exige instalação);
    - e/ou a busca em texto completo do MySQL, que é o banco de produção do projeto.
- Medidas: 
    - tempo médio de resposta com 100, 1.000 e 10.000 narrativas;
    - comportamento com acentos e com letras maiúsculas; e
    - a qualidade dos resultados, para um conjunto de buscas definidas antes ("boitatá", "lobisomem", "sertão"), quantos resultados relevantes cada estratégia trouxe e quantos deixou de fora.

# PROJETO IFIC
## Kaio (INFO1)
### Temática

## Kelly (TSI4)
### Busca de cursos: comparação entre busca textual do PostgreSQL e um motor de busca dedicado
Problema:
- Candidatos procuram cursos por palavras que nem sempre estão no título ("informática básica", "programação", "excel", "costura"). Uma busca simples com LIKE não trata acentos, plurais, erros de digitação nem ordena os resultados por relevância.
O que implementar:
- Um catálogo sintético com centenas de cursos FIC (nome, ementa, eixo tecnológico, campus). Pode-se partir dos nomes do Guia Pronatec de Cursos FIC, que é público.
- Três implementações de busca:
	- icontains (LIKE) do ORM, como linha de base;
        - busca textual completa do PostgreSQL (django.contrib.postgres.search, com dicionário em português, unaccent e similaridade por trigramas);
        - motor de busca dedicado (Meilisearch ou Elasticsearch).
Como validar:
- O próprio aluno monta uma coleção de teste: uma lista de consultas (incluindo consultas com erro de digitação e sem acento) e, para cada uma, quais cursos são relevantes.
- Métricas de recuperação da informação: precisão, revocação, precisão nos primeiros k resultados (P@5) e MRR.
- Tempo de resposta e consumo de recursos (memória, espaço em disco do índice) de cada abordagem.
Integração futura ao iFIC:
- Campo de busca do catálogo público de cursos.
Tecnologias:
- Django, PostgreSQL (pg_trgm, unaccent), Meilisearch ou Elasticsearch.

## Davi (TSI4)
### Otimização de desempenho: consultas no ORM do Django e cache com Redis
Problema:
- A página pública de listagem de cursos FIC tende a ser a mais acessada do sistema, principalmente em períodos de inscrição. Consultas mal escritas no ORM (como o problema das "N+1 consultas") e a ausência de cache podem deixar o sistema lento com muitos acessos simultâneos.

O que implementar:
- Um protótipo com a listagem de cursos e turmas (com campus, eixo, número de vagas restantes etc.) implementada inicialmente de forma "ingênua".
- Otimizações aplicadas em etapas, medindo cada uma separadamente:
	- select_related e prefetch_related;
        - índices no banco de dados;
        - anotações e agregações no banco (em vez de cálculos em Python);
        - cache com Redis (cache de página, de fragmento de template e de consultas), com invalidação quando um curso é alterado.
- Base de dados sintética grande (dezenas de milhares de inscrições).

Como validar:
- Número de consultas SQL por requisição em cada etapa (django-debug-toolbar ou assertNumQueries).
- Tempo médio de resposta, percentis (p95) e requisições por segundo em testes de carga com Locust, para diferentes quantidades de usuários simultâneos.
- Verificação automatizada de que o cache é invalidado corretamente (o dado exibido nunca fica desatualizado após uma edição).

Integração futura ao iFIC:
- Melhorias diretas nas páginas públicas e nas listagens do painel administrativo.

Tecnologias:
- Django, PostgreSQL, Redis, django-redis, django-debug-toolbar, Locust.