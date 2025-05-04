Requêtes SQL
Exo 1 : Nom et année de naissance des artistes nés avant 1950
Requête :
SELECT nom, annéeNaiss 
FROM artiste 
WHERE annéeNaiss < 1950;

Mots-clés utilisés :

SELECT : Sélectionne les colonnes nom et annéeNaiss pour l'affichage.
FROM : Indique que les données proviennent de la table artiste.
WHERE : Filtre les lignes pour ne garder que celles où annéeNaiss est inférieur à 1950.


Exo 2 : Titre de tous les drames
Requête :
SELECT genre from film WHERE genre LIKE 'Drame%';

Mots-clés utilisés :

SELECT : Sélectionne la colonne genre (bien que l'énoncé demande les titres, il s'agit probablement d'une erreur dans la requête).
FROM : Indique que les données proviennent de la table film.
WHERE : Filtre les lignes où la condition suivante est vraie.
LIKE : Recherche les valeurs de genre commençant par "Drame" (% représente n'importe quelle séquence de caractères).


Exo 3 : Quels rôles a joué Bruce Willis
Requête :
SELECT r.nomRôle
FROM role r, artiste a
WHERE r.idActeur = a.idArtiste
AND a.nom = 'Willis'
AND a.prénom = 'Bruce';

Mots-clés utilisés :

SELECT : Sélectionne la colonne nomRôle de la table role.
FROM : Indique les tables role (alias r) et artiste (alias a).
WHERE : Filtre les lignes selon les conditions suivantes.
AND : Combine plusieurs conditions : r.idActeur = a.idArtiste (jointure implicite), a.nom = 'Willis', et a.prénom = 'Bruce'.


Exo 4 : Qui est le réalisateur de Memento
Requête :
SELECT artiste.nom, artiste.prénom
FROM film
JOIN artiste ON film.idRéalisateur = artiste.idArtiste
WHERE film.titre = 'Memento';

Mots-clés utilisés :

SELECT : Sélectionne les colonnes nom et prénom de la table artiste.
FROM : Indique que les données proviennent initialement de la table film.
JOIN : Effectue une jointure (INNER JOIN implicite) avec la table artiste.
ON : Spécifie la condition de jointure : film.idRéalisateur = artiste.idArtiste.
WHERE : Filtre pour ne garder que le film dont le titre est "Memento".


Exo 5 : Quelles sont les notes obtenues par le film Fargo
Requête :
SELECT notation.note
FROM notation
JOIN film ON notation.idFilm = film.idFilm
WHERE film.titre = 'Fargo';

Mots-clés utilisés :

SELECT : Sélectionne la colonne note de la table notation.
FROM : Indique que les données proviennent initialement de la table notation.
JOIN : Joint la table film à notation.
ON : Spécifie la condition de jointure : notation.idFilm = film.idFilm.
WHERE : Filtre pour ne garder que les notes du film dont le titre est "Fargo".


Exo 6 : Qui a joué le rôle de Chewbacca ?
Requête :
SELECT a.nom, a.prénom
FROM role r, artiste a
WHERE r.nomRôle = 'Chewbacca' AND r.idActeur = a.idArtiste;

Mots-clés utilisés :

SELECT : Sélectionne les colonnes nom et prénom de la table artiste (alias a).
FROM : Indique les tables role (alias r) et artiste (alias a).
WHERE : Filtre les lignes où nomRôle = 'Chewbacca' et où r.idActeur = a.idArtiste (jointure implicite).
AND : Combine les deux conditions du WHERE.


Exo 7 : Dans quels films Bruce Willis a-t-il joué le rôle de John McClane ?
Requête :
SELECT film.titre
FROM role
JOIN film ON role.idFilm = film.idFilm
JOIN artiste ON role.idActeur = artiste.idArtiste
WHERE artiste.nom = 'Willis' AND artiste.prénom = 'Bruce' AND role.nomRôle = 'John McClane';

Mots-clés utilisés :

SELECT : Sélectionne la colonne titre de la table film.
FROM : Indique que les données proviennent initialement de la table role.
JOIN : Joint les tables film et artiste à role.
ON : Spécifie les conditions de jointure : role.idFilm = film.idFilm et role.idActeur = artiste.idArtiste.
WHERE : Filtre selon artiste.nom = 'Willis', artiste.prénom = 'Bruce', et role.nomRôle = 'John McClane'.
AND : Combine les trois conditions du WHERE.


Exo 8 : Nom des acteurs de 'Sueurs froides'
Requête :
SELECT a.nom, a.prénom
FROM role r
JOIN artiste a ON r.idActeur = a.idArtiste
JOIN film f ON r.idFilm = f.idFilm
WHERE f.titre = 'Sueurs froides';

Mots-clés utilisés :

SELECT : Sélectionne les colonnes nom et prénom de la table artiste (alias a).
FROM : Indique que les données proviennent initialement de la table role (alias r).
JOIN : Joint les tables artiste (alias a) et film (alias f) à role.
ON : Spécifie les conditions de jointure : r.idActeur = a.idArtiste et r.idFilm = f.idFilm.
WHERE : Filtre pour ne garder que le film dont le titre est "Sueurs froides".


Exo 9 : Quelles sont les films notés par l'internaute Prénom0 Nom0
Requête :
SELECT f.titre
FROM notation n
JOIN film f ON n.idFilm = f.idFilm
JOIN internaute i ON n.email = i.email
WHERE i.prénom = 'Prénom0' AND i.nom = 'Nom0';

Mots-clés utilisés :

SELECT : Sélectionne la colonne titre de la table film (alias f).
FROM : Indique que les données proviennent initialement de la table notation (alias n).
JOIN : Joint les tables film (alias f) et internaute (alias i) à notation.
ON : Spécifie les conditions de jointure : n.idFilm = f.idFilm et n.email = i.email.
WHERE : Filtre selon i.prénom = 'Prénom0' et i.nom = 'Nom0'.
AND : Combine les deux conditions du WHERE.


Exo 10 : Films dont le réalisateur est Tim Burton et l’un des acteurs Johnny Depp
Requête :
SELECT f.titre
FROM film f
JOIN role r ON f.idFilm = r.idFilm
JOIN artiste a1 ON r.idActeur = a1.idArtiste
JOIN artiste a2 ON f.idRéalisateur = a2.idArtiste
WHERE a2.nom = 'Burton' AND a2.prénom = 'Tim'
AND a1.nom = 'Depp' AND a1.prénom = 'Johnny';

Mots-clés utilisés :

SELECT : Sélectionne la colonne titre de la table film (alias f).
FROM : Indique que les données proviennent initialement de la table film (alias f).
JOIN : Joint les tables role (alias r), artiste (alias a1 pour les acteurs), et artiste (alias a2 pour le réalisateur).
ON : Spécifie les conditions de jointure : f.idFilm = r.idFilm, r.idActeur = a1.idArtiste, et f.idRéalisateur = a2.idArtiste.
WHERE : Filtre selon a2.nom = 'Burton', a2.prénom = 'Tim', a1.nom = 'Depp', et a1.prénom = 'Johnny'.
AND : Combine les quatre conditions du WHERE.


Exo 11 : Titre des films dans lesquels a joué Woody Allen, avec le rôle
Requête :
SELECT film.titre, role.nomRôle
FROM role, film, artiste
WHERE role.idFilm = film.idFilm
AND role.idActeur = artiste.idArtiste
AND artiste.nom = 'Allen'
AND artiste.prénom = 'Woody';

Mots-clés utilisés :

SELECT : Sélectionne les colonnes titre (de film) et nomRôle (de role).
FROM : Indique les tables role, film, et artiste.
WHERE : Filtre selon role.idFilm = film.idFilm (jointure implicite), role.idActeur = artiste.idArtiste (jointure implicite), artiste.nom = 'Allen', et artiste.prénom = 'Woody'.
AND : Combine les quatre conditions du WHERE.


Exo 12 : Quel metteur en scène a tourné dans ses propres films ? Donner le nom, le rôle et le titre des films
Requête :
SELECT a.nom, a.prénom, r.nomRôle, f.titre
FROM film f
JOIN role r ON f.idFilm = r.idFilm
JOIN artiste a ON r.idActeur = a.idArtiste
WHERE f.idRéalisateur = a.idArtiste;

Mots-clés utilisés :

SELECT : Sélectionne les colonnes nom, prénom (de artiste), nomRôle (de role), et titre (de film).
FROM : Indique que les données proviennent initialement de la table film (alias f).
JOIN : Joint les tables role (alias r) et artiste (alias a) à film.
ON : Spécifie les conditions de jointure : f.idFilm = r.idFilm et r.idActeur = a.idArtiste.
WHERE : Filtre pour que l’acteur (a.idArtiste) soit aussi le réalisateur (f.idRéalisateur).


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

Mots-clés utilisés :

SELECT : Sélectionne la colonne titre de la table film (alias f).
FROM : Indique que les données proviennent initialement de la table film (alias f).
JOIN : Joint la table artiste (alias a) à film.
ON : Spécifie la condition de jointure : f.idRéalisateur = a.idArtiste.
WHERE : Filtre selon a.nom = 'Tarantino', a.prénom = 'Quentin', et la sous-requête.
AND : Combine les trois conditions du WHERE.
NOT IN : Exclut les films où f.idFilm apparaît dans la sous-requête (films où Tarantino a joué).
(Sous-requête) : SELECT r.idFilm FROM role r WHERE r.idActeur = a.idArtiste identifie les films où Tarantino est acteur.


Exo 14 : Quel metteur en scène a tourné en tant qu’acteur ? Donner le nom, le rôle et le titre des films
Requête :
SELECT DISTINCT a.nom, a.prénom, r.nomRôle, f.titre
FROM role r
JOIN artiste a ON r.idActeur = a.idArtiste
JOIN film f ON r.idFilm = f.idFilm
WHERE EXISTS (
  SELECT * FROM film f2 WHERE f2.idRéalisateur = a.idArtiste
);

Mots-clés utilisés :

SELECT : Sélectionne les colonnes nom, prénom (de artiste), nomRôle (de role), et titre (de film).
DISTINCT : Évite les doublons dans les résultats.
FROM : Indique que les données proviennent initialement de la table role (alias r).
JOIN : Joint les tables artiste (alias a) et film (alias f) à role.
ON : Spécifie les conditions de jointure : r.idActeur = a.idArtiste et r.idFilm = f.idFilm.
WHERE : Filtre selon la sous-requête.
EXISTS : Vérifie si l’artiste (a.idArtiste) est aussi réalisateur dans au moins un film.
(Sous-requête) : SELECT * FROM film f2 WHERE f2.idRéalisateur = a.idArtiste vérifie si l’artiste est réalisateur.
* : Sélectionne toutes les colonnes dans la sous-requête (optimisation possible avec SELECT 1).


Exo 15 : Donnez les films de Hitchcock sans James Stewart
Requête :
SELECT f.titre
FROM film f
JOIN artiste a ON f.idRéalisateur = a.idArtiste
WHERE a.nom = 'Hitchcock' AND a.prénom = 'Alfred'
AND f.idFilm NOT IN (
  SELECT r.idFilm
  FROM role r
  JOIN artiste a2 ON r.idActeur = a2.idArtiste
  WHERE a2.nom = 'Stewart' AND a2.prénom = 'James'
);

Mots-clés utilisés :

SELECT : Sélectionne la colonne titre de la table film (alias f).
FROM : Indique que les données proviennent initialement de la table film (alias f).
JOIN : Joint la table artiste (alias a) à film.
ON : Spécifie la condition de jointure : f.idRéalisateur = a.idArtiste.
WHERE : Filtre selon a.nom = 'Hitchcock', a.prénom = 'Alfred', et la sous-requête.
AND : Combine les trois conditions du WHERE.
NOT IN : Exclut les films où f.idFilm apparaît dans la sous-requête (films avec James Stewart).
(Sous-requête) : SELECT r.idFilm FROM role r JOIN artiste a2 ON r.idActeur = a2.idArtiste WHERE a2.nom = 'Stewart' AND a2.prénom = 'James' identifie les films où Stewart a joué.


Exo 16 : Dans quels films le réalisateur a-t-il le même prénom que l’un des interprètes ?
Requête :
SELECT f.titre, a1.nom AS nomRéalisateur, a1.prénom AS prénomRéalisateur, a2.nom AS nomActeur, a2.prénom AS prénomActeur
FROM film f
JOIN artiste a1 ON f.idRéalisateur = a1.idArtiste
JOIN role r ON f.idFilm = r.idFilm
JOIN artiste a2 ON r.idActeur = a2.idArtiste
WHERE a1.prénom = a2.prénom AND a1.idArtiste != a2.idArtiste;

Mots-clés utilisés :

SELECT : Sélectionne titre (de film), nom et prénom de a1 (réalisateur), nom et prénom de a2 (acteur).
AS : Renomme les colonnes pour clarifier : nomRéalisateur, prénomRéalisateur, nomActeur, prénomActeur.
FROM : Indique que les données proviennent initialement de la table film (alias f).
JOIN : Joint les tables artiste (alias a1 pour le réalisateur), role (alias r), et artiste (alias a2 pour l’acteur).
ON : Spécifie les conditions de jointure : f.idRéalisateur = a1.idArtiste, f.idFilm = r.idFilm, et r.idActeur = a2.idArtiste.
WHERE : Filtre pour que les prénoms soient identiques (a1.prénom = a2.prénom) et que les artistes soient différents (a1.idArtiste != a2.idArtiste).
AND : Combine les deux conditions du WHERE.


Exo 17 : Les films sans rôle
Requête :
SELECT titre
FROM film
WHERE idFilm NOT IN (
  SELECT idFilm FROM role
);

Mots-clés utilisés :

SELECT : Sélectionne la colonne titre de la table film.
FROM : Indique que les données proviennent de la table film.
WHERE : Filtre selon la sous-requête.
NOT IN : Exclut les films dont l’idFilm apparaît dans la sous-requête (films avec des rôles).
(Sous-requête) : SELECT idFilm FROM role liste tous les idFilm ayant des rôles.


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

Mots-clés utilisés :

SELECT : Sélectionne la colonne titre de la table film (alias f).
FROM : Indique que les données proviennent de la table film (alias f).
WHERE : Filtre selon la sous-requête.
NOT EXISTS : Vérifie l’absence de lignes dans la sous-requête (films notés par Prénom1 Nom1).
(Sous-requête) : SELECT 1 FROM notation n, internaute i WHERE n.email = i.email AND n.idFilm = f.idFilm AND i.prénom = 'Prénom1' AND i.nom = 'Nom1' identifie les films notés par l’internaute.
AND : Combine les conditions dans la sous-requête.
1 : Constante utilisée pour optimiser la sous-requête (seule l’existence compte).


Exo 19 : Quels acteurs n’ont jamais réalisé de film ?
Requête :
SELECT DISTINCT nom, prénom
FROM artiste
WHERE NOT EXISTS (
  SELECT 1 FROM film WHERE film.idRéalisateur = artiste.idArtiste
);

Mots-clés utilisés :

SELECT : Sélectionne les colonnes nom et prénom de la table artiste.
DISTINCT : Évite les doublons dans les résultats.
FROM : Indique que les données proviennent de la table artiste.
WHERE : Filtre selon la sous-requête.
NOT EXISTS : Vérifie l’absence de films où l’artiste est réalisateur.
(Sous-requête) : SELECT 1 FROM film WHERE film.idRéalisateur = artiste.idArtiste vérifie si l’artiste est réalisateur.
1 : Constante pour optimiser la sous-requête.


Exo 20 : Quelle est la moyenne des notes de Memento
Requête :
SELECT AVG(note) AS moyenne
FROM notation
WHERE idFilm = (
  SELECT idFilm FROM film WHERE titre = 'Memento'
);

Mots-clés utilisés :

SELECT : Sélectionne la moyenne des notes (AVG(note)).
AVG : Calcule la moyenne des valeurs de la colonne note.
AS : Renomme le résultat de AVG(note) en moyenne.
FROM : Indique que les données proviennent de la table notation.
WHERE : Filtre pour ne garder que les notes du film spécifié par la sous-requête.
(Sous-requête) : `SELECT idFilm FROM film WHERE titre
SELECT : Sélectionne la colonne idFilm dans la sous-requête.
FROM : Indique que les données de la sous-requête proviennent de la table film.
WHERE : Filtre pour ne garder que le film dont le titre est "Memento".


Exo 21 : ID, nom et prénom des réalisateurs, et nombre de films qu’ils ont tournés
Requête :
SELECT a.idArtiste, a.nom, a.prénom, COUNT(f.idFilm) AS nombreFilms
FROM artiste a
LEFT JOIN film f ON a.idArtiste = f.idRéalisateur
GROUP BY a.idArtiste, a.nom, a.prénom;

Mots-clés utilisés :

SELECT : Sélectionne idArtiste, nom, prénom (de artiste), et le compte des films (COUNT(f.idFilm)).
COUNT : Compte le nombre de idFilm pour chaque groupe.
AS : Renomme le résultat de COUNT(f.idFilm) en nombreFilms.
FROM : Indique que les données proviennent initialement de la table artiste (alias a).
LEFT JOIN : Joint la table film (alias f) à artiste, incluant tous les artistes même sans films.
ON : Spécifie la condition de jointure : a.idArtiste = f.idRéalisateur.
GROUP BY : Regroupe les résultats par a.idArtiste, a.nom, et a.prénom pour compter les films par artiste.


Exo 22 : Nom et prénom des réalisateurs qui ont tourné au moins deux films
Requête :
SELECT a.nom, a.prénom
FROM artiste a
JOIN film f ON a.idArtiste = f.idRéalisateur
GROUP BY a.idArtiste, a.nom, a.prénom
HAVING COUNT(f.idFilm) >= 2;

Mots-clés utilisés :

SELECT : Sélectionne les colonnes nom et prénom de la table artiste (alias a).
FROM : Indique que les données proviennent initialement de la table artiste (alias a).
JOIN : Joint la table film (alias f) à artiste.
ON : Spécifie la condition de jointure : a.idArtiste = f.idRéalisateur.
GROUP BY : Regroupe les résultats par a.idArtiste, a.nom, et a.prénom.
HAVING : Filtre les groupes ayant au moins deux films (COUNT(f.idFilm) >= 2).
COUNT : Compte le nombre de idFilm dans chaque groupe.


Exo 23 : Quels films ont une moyenne des notes supérieure à 7
Requête :
SELECT titre FROM notemoyenne WHERE moyenne > 7;

Mots-clés utilisés :

SELECT : Sélectionne la colonne titre de la table notemoyenne.
FROM : Indique que les données proviennent de la table notemoyenne.
WHERE : Filtre pour ne garder que les films dont la moyenne est supérieure à 7.

