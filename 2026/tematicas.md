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