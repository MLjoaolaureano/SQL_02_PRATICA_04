# SQL 02
# PRÁTICA INTEGRADORA 04
## Adicione um filme à tabela de filmes.
    INSERT INTO `movies_db`.`movies`
    (`created_at`,`updated_at`,`title`,`rating`,`awards`,`release_date`,`length`,`genre_id`)
    VALUES
    (null,null,'RED: CRESCER É UMA FERA',7,0,'2022-04-11',100,7);

## Adicione um gênero à tabela de gêneros.
    INSERT INTO `movies_db`.`genres`
    (`created_at`,`updated_at`,`name`,`ranking`)
    VALUES
    (null,null,'spaghetti western',13);

## Associe o filme do ponto 1. com o gênero criado no ponto 2.
    UPDATE `movies_db`.`movies`
    SET `genre_id` = 2
    WHERE `id` = 1;

## Modifique a tabela de atores para que pelo menos um ator tenha o filme adicionado no ponto 1 como favorito.
    UPDATE `movies_db`.`actors`
    SET
    `favorite_movie_id` = 1
    WHERE `id` = 12;

    SELECT * FROM movies_db.actors;
## Crie uma tabela temporária da tabela filmes.
    create temporary table movies_temp
    select * from movies;
## Elimine dessa tabela temporária todos os filmes que ganharam menos de 5 prêmios.
    DELETE FROM `movies_db`.`movies_temp`
    WHERE awards < 5;
## Obtenha a lista de todos os gêneros que possuem pelo menos um filme.
    SELECT genres.name, count(*) FROM movies_db.genres
    join Movies movies on movies.genre_id = genres.id
    group by movies.genre_id
    having count(*) >= 1;
## Obtenha a lista de atores cujo filme favorito ganhou mais de 3 prêmios.
    SELECT * FROM movies_db.actors
    join Movies movies on movies.id = actors.favorite_movie_id
    where movies.awards > 3;
## Crie um índice no nome na tabela de filmes.
    create unique index idx_movies_title
    on movies (title);
## Verifique se o índice foi criado corretamente.
    show index from movies where key_name = 'idx_movies_title';
## No banco de dados movies, haveria uma melhoria notável na criação de índices? Analise e justifique a resposta.
    Caso essa tabela seja muito referenciada nas procuras com JOIN, como no caso de actor_movie, sim, o índice seria interessante para otimizar a pesquisa
## Em que outra tabela você criaria um índice e por quê? Justifique a resposta
    Na tabela de series.
    Ela é utilizada frequentemente em conjunto com uma tabela chamada seasons, e, considerando que o usuário vá usar a tabela seasons ou outras relacionadas, como episodes, os dados de series poderiam ser carregados de maneira mais otimizado.