# examen-requete
Exo 1 Nom et année de naissance des artistes nés avant 1950.

SELECT nom, annéeNaiss 
FROM artiste 
WHERE annéeNaiss < 1950;


Exo 2 Titre de tous les drames.

SELECT genre from film WHERE genre LIKE 'Drame%';

Exo 3 Quels rôles a joué Bruce Willis.

SELECT r.nomRôle
FROM role r, artiste a
WHERE r.idActeur = a.idArtiste
AND a.nom = 'Willis'
AND a.prénom = 'Bruce';


Exo 4 Qui est le réalisateur de Memento.

SELECT artiste.nom, artiste.prénom
FROM film
JOIN artiste ON film.idRéalisateur = artiste.idArtiste
WHERE film.titre = 'Memento';


Exo 5 Quelles sont les notes obtenues par le film Fargo

SELECT notation.note
FROM notation
JOIN film ON notation.idFilm = film.idFilm
WHERE film.titre = 'Fargo';


Exo 6 Qui a joué le rôle de Chewbacca?

SELECT a.nom, a.prénom
FROM role r, artiste a
WHERE r.nomRôle = 'Chewbacca' AND r.idActeur = a.idArtiste;



Exo 7 Dans quels films Bruce Willis a-t-il joué le rôle de John McClane?

SELECT film.titre
FROM role
JOIN film ON role.idFilm = film.idFilm
JOIN artiste ON role.idActeur = artiste.idArtiste
WHERE artiste.nom = 'Willis' AND artiste.prénom = 'Bruce' AND role.nomRôle = 'John McClane';



Exo 8 Nom des acteurs de 'Sueurs froides'

SELECT a.nom, a.prénom
FROM role r
JOIN artiste a ON r.idActeur = a.idArtiste
JOIN film f ON r.idFilm = f.idFilm
WHERE f.titre = 'Sueurs froides';



Exo 9 Quelles sont les films notés par l'internaute Prénom 0 Nom0

SELECT f.titre
FROM notation n
JOIN film f ON n.idFilm = f.idFilm
JOIN internaute i ON n.email = i.email
WHERE i.prénom = 'Prénom0' AND i.nom = 'Nom0';




Exo 10 Films dont le réalisateur est Tim Burton, et l’un des acteursJohnny Depp.

SELECT f.titre
FROM film f
JOIN role r ON f.idFilm = r.idFilm
JOIN artiste a1 ON r.idActeur = a1.idArtiste
JOIN artiste a2 ON f.idRéalisateur = a2.idArtiste
WHERE a2.nom = 'Burton' AND a2.prénom = 'Tim'
AND a1.nom = 'Depp' AND a1.prénom = 'Johnny';


Exo 11 Titre des films dans lesquels a joué ́Woody Allen. Donner aussi le rôle.


SELECT film.titre, role.nomRôle
FROM role, film, artiste
WHERE role.idFilm = film.idFilm
AND role.idActeur = artiste.idArtiste
AND artiste.nom = 'Allen'
AND artiste.prénom = 'Woody';



Exo 12 Quel metteur en scène a tourné dans ses propres films ? Donner
le nom, le rôle et le titre des films.

SELECT a.nom, a.prénom, r.nomRôle, f.titre
FROM film f
JOIN role r ON f.idFilm = r.idFilm
JOIN artiste a ON r.idActeur = a.idArtiste
WHERE f.idRéalisateur = a.idArtiste;




 Exo 13 Titre des films de Quentin Tarantino dans lesquels il n’a pas
joué
SELECT f.titre
FROM film f
JOIN artiste a ON f.idRéalisateur = a.idArtiste
WHERE a.nom = 'Tarantino'
AND a.prénom = 'Quentin'
AND f.idFilm NOT IN (
  SELECT r.idFilm FROM role r WHERE r.idActeur = a.idArtiste
);




Exo 14 Quel metteur en scène a tourné ́en tant qu’acteur ? Donner le
nom, le rôle et le titre des films dans lesquels cet artiste a joué.

SELECT DISTINCT a.nom, a.prénom, r.nomRôle, f.titre
FROM role r
JOIN artiste a ON r.idActeur = a.idArtiste
JOIN film f ON r.idFilm = f.idFilm
WHERE EXISTS (
  SELECT * FROM film f2 WHERE f2.idRéalisateur = a.idArtiste
);


Exo 15 Donnez les films de Hitchcock sans James Stewart
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




Exo 16 Dans quels films le réalisateur a-t-il le même prénom que l’un
des interprètes ? (titre, nom du réalisateur, nom de l’interprète). Le
réalisateur et l’interprète ne doivent pas être la même personne.


SELECT f.titre, a1.nom AS nomRéalisateur, a1.prénom AS prénomRéalisateur, a2.nom AS nomActeur, a2.prénom AS prénomActeur
FROM film f
JOIN artiste a1 ON f.idRéalisateur = a1.idArtiste
JOIN role r ON f.idFilm = r.idFilm
JOIN artiste a2 ON r.idActeur = a2.idArtiste
WHERE a1.prénom = a2.prénom AND a1.idArtiste != a2.idArtiste;






Exo 17 Les films sans rôlSELECT titre

SELECT titre
FROM film
WHERE idFilm NOT IN (
  SELECT idFilm FROM role
);




Exo 18 Quelles sont les films non notés par l'internaute Prénom1 Nom1

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





Exo 19 Quels acteurs n’ont jamais réalisé de film ?

SELECT DISTINCT nom, prénom
FROM artiste
WHERE NOT EXISTS (
  SELECT 1 FROM film WHERE film.idRéalisateur = artiste.idArtiste
);




Exo 20 Quelle est la moyenne des notes de Memento

SELECT AVG(note) AS moyenne
FROM notation
WHERE idFilm = (
  SELECT idFilm FROM film WHERE titre = 'Memento'
);




Exo 21 id, nom et prénom des réalisateurs, et nombre de films qu’ils
ont tournés.

SELECT a.idArtiste, a.nom, a.prénom, COUNT(f.idFilm) AS nombreFilms
FROM artiste a
LEFT JOIN film f ON a.idArtiste = f.idRéalisateur
GROUP BY a.idArtiste, a.nom, a.prénom;



Exo 22 Nom et prénom des réalisateurs qui ont tourné au moins deux
films.

SELECT a.nom, a.prénom
FROM artiste a
JOIN film f ON a.idArtiste = f.idRéalisateur
GROUP BY a.idArtiste, a.nom, a.prénom
HAVING COUNT(f.idFilm) >= 2;



Exo 23 Quels films ont une moyenne des notes supérieure à 7
SELECT titre FROM notemoyenne WHERE moyenne > 7;





