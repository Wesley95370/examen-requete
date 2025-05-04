Requêtes SQL avec explications simples des mots-clés et conditions
Exo 1 : Nom et année de naissance des artistes nés avant 1950
Requête :
SELECT nom, annéeNaiss 
FROM artiste 
WHERE annéeNaiss < 1950;

Mots-clés utilisés :La requête utilise SELECT pour choisir les colonnes nom et annéeNaiss à afficher. FROM indique que les données viennent de la table artiste. WHERE garde seulement les artistes nés avant 1950, grâce à la condition simple annéeNaiss < 1950.

Exo 2 : Titre de tous les drames
Requête (corrigée) :
SELECT titre 
FROM film 
WHERE genre LIKE 'Drame%';

Mots-clés utilisés :La requête utilise SELECT pour choisir la colonne titre à afficher. FROM indique que les données viennent de la table film. WHERE filtre les films en utilisant LIKE, qui garde ceux dont le genre commence par "Drame" (% signifie "n’importe quoi après"). La condition genre LIKE 'Drame%' est comme dire : "trouve tous les films où le genre débute par Drame".

Exo 3 : Quels rôles a joué Bruce Willis
Requête :
SELECT r.nomRôle
FROM role r, artiste a
WHERE r.idActeur = a.idArtiste
AND a.nom = 'Willis'
AND a.prénom = 'Bruce';

Mots-clés utilisés :La requête utilise SELECT pour choisir la colonne nomRôle de la table role (alias r). FROM indique deux tables : role (alias r) et artiste (alias a). WHERE combine trois conditions avec AND :  

r.idActeur = a.idArtiste : relie les tables en disant que l’acteur dans role doit correspondre à un artiste dans artiste (comme une jointure).  
a.nom = 'Willis' : garde seulement les artistes nommés Willis.  
a.prénom = 'Bruce' : précise que le prénom doit être Bruce. Ensemble, ces conditions trouvent les rôles joués par Bruce Willis.


Exo 4 : Qui est le réalisateur de Memento
Requête :
SELECT artiste.nom, artiste.prénom
FROM film
JOIN artiste ON film.idRéalisateur = artiste.idArtiste
WHERE film.titre = 'Memento';

Mots-clés utilisés :La requête utilise SELECT pour choisir nom et prénom de la table artiste. FROM commence avec la table film. JOIN relie artiste à film. ON explique comment : film.idRéalisateur = artiste.idArtiste signifie que l’ID du réalisateur dans film doit correspondre à l’ID d’un artiste dans artiste. WHERE ajoute une condition : film.titre = 'Memento' garde seulement le film nommé "Memento". Ces conditions trouvent le nom et prénom du réalisateur de ce film.

Exo 5 : Quelles sont les notes obtenues par le film Fargo
Requête :
SELECT notation.note
FROM notation
JOIN film ON notation.idFilm = film.idFilm
WHERE film.titre = 'Fargo';

Mots-clés utilisés :La requête utilise SELECT pour choisir la colonne note de notation. FROM commence avec notation. JOIN relie film à notation. ON précise : notation.idFilm = film.idFilm signifie que l’ID du film dans notation doit correspondre à celui dans film. WHERE filtre avec film.titre = 'Fargo', pour ne garder que les notes du film "Fargo". Les conditions relient les notes au film demandé.

Exo 6 : Qui a joué le rôle de Chewbacca ?
Requête :
SELECT a.nom, a.prénom
FROM role r, artiste a
WHERE r.nomRôle = 'Chewbacca' AND r.idActeur = a.idArtiste;

Mots-clés utilisés :La requête utilise SELECT pour choisir nom et prénom de artiste (alias a). FROM indique les tables role (alias r) et artiste (alias a). WHERE combine deux conditions avec AND :  

r.nomRôle = 'Chewbacca' : garde seulement le rôle nommé Chewbacca.  
r.idActeur = a.idArtiste : relie l’acteur du rôle à un artiste (comme une jointure). Ces conditions trouvent l’artiste qui a joué Chewbacca.


Exo 7 : Dans quels films Bruce Willis a-t-il joué le rôle de John McClane ?
Requête :
SELECT film.titre
FROM role
JOIN film ON role.idFilm = film.idFilm
JOIN artiste ON role.idActeur = artiste.idArtiste
WHERE artiste.nom = 'Willis' AND artiste.prénom = 'Bruce' AND role.nomRôle = 'John McClane';

Mots-clés utilisés :La requête utilise SELECT pour choisir titre de film. FROM commence avec role. JOIN relie deux tables : film et artiste. ON explique :  

role.idFilm = film.idFilm : lie le film du rôle à un film dans film.  
role.idActeur = artiste.idArtiste : lie l’acteur du rôle à un artiste. WHERE filtre avec trois conditions combinées par AND :  
artiste.nom = 'Willis' : garde l’artiste nommé Willis.  
artiste.prénom = 'Bruce' : précise le prénom Bruce.  
role.nomRôle = 'John McClane' : garde le rôle John McClane. Ces conditions trouvent les films où Bruce Willis joue ce rôle.




Exo 8 : Nom des acteurs de 'Sueurs froides'
Requête (corrigée) :
SELECT a.nom, a.prénom
FROM role r
JOIN artiste a ON r.idActeur = a.idArtiste
JOIN film f ON r.idFilm = f.idFilm
WHERE f.titre = 'Sueurs froides';

Mots-clés utilisés :La requête utilise SELECT pour choisir nom et prénom de artiste (alias a, corrigé de a.prod). FROM commence avec role (alias r). JOIN relie artiste (alias a) et film (alias f). ON précise :  

r.idActeur = a.idArtiste : lie l’acteur du rôle à un artiste.  
r.idFilm = f.idFilm : lie le film du rôle à un film dans film. WHERE filtre avec f.titre = 'Sueurs froides', pour ne garder que les acteurs de ce film.


Exo 9 : Quelles sont les films notés par l'internaute Prénom0 Nom0
Requête :
SELECT f.titre
FROM notation n
JOIN film f ON n.idFilm = f.idFilm
JOIN internaute i ON n.email = i.email
WHERE i.prénom = 'Prénom0' AND i.nom = 'Nom0';

Mots-clés utilisés :La requête utilise SELECT pour choisir titre de film (alias f). FROM commence avec notation (alias n). JOIN relie film (alias f) et internaute (alias i). ON explique :  

n.idFilm = f.idFilm : lie le film noté à un film dans film.  
n.email = i.email : lie l’internaute qui a noté à un internaute dans internaute. WHERE filtre avec deux conditions combinées par AND :  
i.prénom = 'Prénom0' : garde l’internaute avec ce prénom.  
i.nom = 'Nom0' : précise le nom. Ces conditions trouvent les films notés par cet internaute.




Exo 10 : Films dont le réalisateur est Tim Burton et l’un des acteurs Johnny Depp
Requête :
SELECT f.titre
FROM film f
JOIN role r ON f.idFilm = r.idFilm
JOIN artiste a1 ON r.idActeur = a1.idArtiste
JOIN artiste a2 ON f.idRéalisateur = a2.idArtiste
WHERE a2.nom = 'Burton' AND a2.prénom = 'Tim'
AND a1.nom = 'Depp' AND a1.prénom = 'Johnny';

Mots-clés utilisés :La requête utilise SELECT pour choisir titre de film (alias f). FROM commence avec film (alias f). JOIN relie trois tables : role (alias r), artiste (alias a1 pour l’acteur), et artiste (alias a2 pour le réalisateur). ON précise :  

f.idFilm = r.idFilm : lie le film à un rôle.  
r.idActeur = a1.idArtiste : lie l’acteur du rôle à un artiste.  
f.idRéalisateur = a2.idArtiste : lie le réalisateur du film à un artiste. WHERE filtre avec quatre conditions combinées par AND :  
a2.nom = 'Burton' et a2.prénom = 'Tim' : garde le réalisateur Tim Burton.  
a1.nom = 'Depp' et a1.prénom = 'Johnny' : garde l’acteur Johnny Depp. Ces conditions trouvent les films où les deux sont impliqués.




Exo 11 : Titre des films dans lesquels a joué Woody Allen, avec le rôle
Requête :
SELECT film.titre, role.nomRôle
FROM role, film, artiste
WHERE role.idFilm = film.idFilm
AND role.idActeur = artiste.idArtiste
AND artiste.nom = 'Allen'
AND artiste.prénom = 'Woody';

Mots-clés utilisés :La requête utilise SELECT pour choisir titre de film et nomRôle de role. FROM indique trois tables : role, film, et artiste. WHERE combine quatre conditions avec AND :  

role.idFilm = film.idFilm : relie le rôle à un film (comme une jointure).  
role.idActeur = artiste.idArtiste : relie l’acteur du rôle à un artiste.  
artiste.nom = 'Allen' : garde l’artiste nommé Allen.  
artiste.prénom = 'Woody' : précise le prénom Woody. Ces conditions trouvent les films et rôles de Woody Allen.


Exo 12 : Quel metteur en scène a tourné dans ses propres films ?
Requête :
SELECT a.nom, a.prénom, r.nomRôle, f.titre
FROM film f
JOIN role r ON f.idFilm = r.idFilm
JOIN artiste a ON r.idActeur = a.idArtiste
WHERE f.idRéalisateur = a.idArtiste;

Mots-clés utilisés :La requête utilise SELECT pour choisir nom, prénom de artiste, nomRôle de role, et titre de film. FROM commence avec film (alias f). JOIN relie role (alias r) et artiste (alias a). ON précise :  

f.idFilm = r.idFilm : lie le film à un rôle.  
r.idActeur = a.idArtiste : lie l’acteur du rôle à un artiste. WHERE filtre avec f.idRéalisateur = a.idArtiste, ce qui signifie que l’artiste doit être à la fois acteur et réalisateur du film.


Exo 13 : Titre des films de Quentin Tarantino dans lesquels il n’a pas joué
Requête :
SELECT f.titre
FROM film f
JOIN artiste a ON f.idRéalisateur = a.idArtiste
WHERE a.nom = 'Tarantino'
AND a.prénom = 'Quentin'
AND f.idFilm NOT IN (
  SELECT r.idFilm FROM role r WHERE r.idActeur = a.idArtiste
);

Mots-clés utilisés :La requête utilise SELECT pour choisir titre de film (alias f). FROM commence avec film (alias f). JOIN relie artiste (alias a). ON précise : f.idRéalisateur = a.idArtiste lie le réalisateur du film à un artiste. WHERE combine trois conditions avec AND :  

a.nom = 'Tarantino' : garde l’artiste nommé Tarantino.  
a.prénom = 'Quentin' : précise le prénom Quentin.  
NOT IN avec une sous-requête exclut les films où Tarantino a joué. La sous-requête utilise SELECT pour lister les idFilm où r.idActeur = a.idArtiste, c’est-à-dire les films où Tarantino est acteur.


Exo 14 : Quel metteur en scène a tourné en tant qu’acteur ?
Requête :
SELECT DISTINCT a.nom, a.prénom, r.nomRôle, f.titre
FROM role r
JOIN artiste a ON r.idActeur = a.idArtiste
JOIN film f ON r.idFilm = f.idFilm
WHERE EXISTS (
  SELECT * FROM film f2 WHERE f2.idRéalisateur = a.idArtiste
);

Mots-clés utilisés :La requête utilise SELECT pour choisir nom, prénom de artiste, nomRôle de role, et titre de film. DISTINCT évite les doublons. FROM commence avec role (alias r). JOIN relie artiste (alias a) et film (alias f). ON précise :  

r.idActeur = a.idArtiste : lie l’acteur du rôle à un artiste.  
r.idFilm = f.idFilm : lie le rôle à un film. WHERE utilise EXISTS avec une sous-requête pour vérifier si l’artiste (a.idArtiste) est aussi réalisateur. La sous-requête utilise SELECT avec **** pour lister les films où f2.idRéalisateur = a.idArtiste.


Exo 15 : Donnez les films de Hitchcock sans James Stewart
Requête :
SELECT f.titre
FROM film f
JOIN artiste a ON f.idRéalisateur = a.idArtiste
WHERE a.nom = 'Hitchcock' AND a.prénom = 'Alfred'
AND f.idFilm NOT IN (
  SELECT r.idFilm FROM role r JOIN artiste a2 ON r.idActeur = a2.idArtiste
  WHERE a2.nom = 'Stewart' AND a2.prénom = 'James'
);

Mots-clés utilisés :La requête utilise SELECT pour choisir titre de film (alias f). FROM commence avec film (alias f). JOIN relie artiste (alias a). ON précise : f.idRéalisateur = a.idArtiste lie le réalisateur à un artiste. WHERE combine trois conditions avec AND :  

a.nom = 'Hitchcock' : garde le réalisateur nommé Hitchcock.  
a.prénom = 'Alfred' : précise le prénom Alfred.  
NOT IN avec une sous-requête exclut les films où James Stewart a joué. La sous-requête utilise SELECT, FROM, JOIN, ON (r.idActeur = a2.idArtiste), WHERE, et AND pour lister les idFilm où a2.nom = 'Stewart' et a2.prénom = 'James'.


Exo 16 : Dans quels films le réalisateur a-t-il le même prénom que l’un des interprètes ?
Requête :
SELECT f.titre, a1.nom AS nomRéalisateur, a1.prénom AS prénomRéalisateur, a2.nom AS nomActeur, a2.prénom AS prénomActeur
FROM film f
JOIN artiste a1 ON f.idRéalisateur = a1.idArtiste
JOIN role r ON f.idFilm = r.idFilm
JOIN artiste a2 ON r.idActeur = a2.idArtiste
WHERE a1.prénom = a2.prénom AND a1.idArtiste != a2.idArtiste;

Mots-clés utilisés :La requête utilise SELECT pour choisir titre, nom, et prénom des deux artistes. AS renomme les colonnes pour clarté. FROM commence avec film (alias f). JOIN relie artiste (alias a1 pour le réalisateur), role (alias r), et artiste (alias a2 pour l’acteur). ON précise :  

f.idRéalisateur = a1.idArtiste : lie le réalisateur à un artiste.  
f.idFilm = r.idFilm : lie le film à un rôle.  
r.idActeur = a2.idArtiste : lie l’acteur du rôle à un artiste. WHERE filtre avec deux conditions combinées par AND :  
a1.prénom = a2.prénom : garde les cas où le prénom du réalisateur et de l’acteur est identique.  
a1.idArtiste != a2.idArtiste : s’assure que ce ne sont pas la même personne.




Exo 17 : Les films sans rôle
Requête :
SELECT titre
FROM film
WHERE idFilm NOT IN (
  SELECT idFilm FROM role
);

Mots-clés utilisés :La requête utilise SELECT pour choisir titre de film. FROM indique que les données viennent de film. WHERE filtre avec NOT IN, qui exclut les films dont l’idFilm apparaît dans la sous-requête. La sous-requête utilise SELECT et FROM pour lister tous les idFilm de role, c’est-à-dire les films avec des rôles.

Exo 18 : Quelles sont les films non notés par l'internaute Prénom1 Nom1
Requête :
SELECT titre
FROM film f
WHERE NOT EXISTS (
  SELECT 1
  FROM notation n, internaute i
  WHERE n.email = i.email
  AND n.idFilm = f.idFilm
  AND i.prénom = 'Prénom1'
  AND i.nom = 'Nom1'
);

Mots-clés utilisés :La requête utilise SELECT pour choisir titre de film (alias f). FROM commence avec film (alias f). WHERE utilise NOT EXISTS pour vérifier qu’aucune ligne n’existe dans la sous-requête. La sous-requête utilise SELECT avec 1 (pour optimiser), FROM pour notation (alias n) et internaute (alias i), et WHERE avec trois conditions combinées par AND :  

n.email = i.email : lie la note à un internaute.  
n.idFilm = f.idFilm : lie la note au film.  
i.prénom = 'Prénom1' et i.nom = 'Nom1' : identifie l’internaute. Ces conditions vérifient si l’internaute a noté le film.


Exo 19 : Quels acteurs n’ont jamais réalisé de film ?
Requête :
SELECT DISTINCT nom, prénom
FROM artiste
WHERE NOT EXISTS (
  SELECT 1 FROM film WHERE film.idRéalisateur = artiste.idArtiste
);

Mots-clés utilisés :La requête utilise SELECT pour choisir nom et prénom de artiste. DISTINCT évite les doublons. FROM indique que les données viennent de artiste. WHERE utilise NOT EXISTS pour vérifier qu’aucun film n’a l’artiste comme réalisateur. La sous-requête utilise SELECT avec 1 (pour optimiser), FROM pour film, et WHERE avec film.idRéalisateur = artiste.idArtiste, qui vérifie si l’artiste a réalisé un film.

Exo 20 : Quelle est la moyenne des notes de Memento
Requête :
SELECT AVG(note) AS moyenne
FROM notation
WHERE idFilm = (
  SELECT idFilm FROM film WHERE titre = 'Memento'
);

Mots-clés utilisés :La requête utilise SELECT pour calculer la moyenne des notes avec AVG sur note. AS renomme le résultat en moyenne. FROM commence avec notation. WHERE filtre avec une sous-requête. La sous-requête utilise SELECT pour choisir idFilm de film, FROM pour film, et WHERE avec titre = 'Memento' pour trouver l’ID du film "Memento". La condition idFilm = (sous-requête) limite les notes à ce film.

Exo 21 : ID, nom et prénom des réalisateurs, et nombre de films
Requête :
SELECT a.idArtiste, a.nom, a.prénom, COUNT(f.idFilm) AS nombreFilms
FROM artiste a
LEFT JOIN film f ON a.idArtiste = f.idRéalisateur
GROUP BY a.idArtiste, a.nom, a.prénom;

Mots-clés utilisés :La requête utilise SELECT pour choisir idArtiste, nom, prénom de artiste, et COUNT pour compter les films. AS renomme le compte en nombreFilms. FROM commence avec artiste (alias a). LEFT JOIN relie film (alias f), incluant tous les artistes même sans films. ON précise : a.idArtiste = f.idRéalisateur lie l’artiste au réalisateur du film. GROUP BY regroupe par a.idArtiste, a.nom, a.prénom pour compter les films par artiste.

Exo 22 : Nom et prénom des réalisateurs avec au moins deux films
Requête :
SELECT a.nom, a.prénom
FROM artiste a
JOIN film f ON a.idArtiste = f.idRéalisateur
GROUP BY a.idArtiste, a.nom, a.prénom
HAVING COUNT(f.idFilm) >= 2;

Mots-clés utilisés :La requête utilise SELECT pour choisir nom et prénom de artiste (alias a). FROM commence avec artiste (alias a). JOIN relie film (alias f). ON précise : a.idArtiste = f.idRéalisateur lie l’artiste au réalisateur. GROUP BY regroupe par a.idArtiste, a.nom, a.prénom. HAVING filtre les groupes avec au moins deux films, en utilisant COUNT sur f.idFilm. La condition COUNT(f.idFilm) >= 2 garde les réalisateurs avec plusieurs films.

Exo 23 : Quels films ont une moyenne des notes > 7
Requête :
SELECT titre 
FROM notemoyenne 
WHERE moyenne > 7;

Mots-clés utilisés :La requête utilise SELECT pour choisir titre de notemoyenne. FROM indique que les données viennent de notemoyenne. WHERE filtre avec moyenne > 7, une condition simple qui garde les films dont la moyenne des notes est supérieure à 7.
