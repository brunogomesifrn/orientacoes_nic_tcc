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

