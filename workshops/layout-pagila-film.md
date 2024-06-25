# Schéma `pagila` (vue partielle restreinte au catalogue des films)

Créé par [DbSchema](https://dbschema.com)

`pagila` est un schéma d'entrainement dérivé du schéma `sakila`  de `MySQL`.  C'est une base de donnée fictive destinée à gérer le catalogue et les stocks d'une chaine de magasins de location de DVD (début du XXIème siècle). 

### Vue d'ensemble des tables portants sur les films

![Vue partielle de `pagila`](../images/layout-pagila-film.svg)

<!-- Voir aussi [Vue partielle restreinte au catalogue des films](./layout-pagila-film.html) -->

### Table pagila.actor 
| | | |
|---|---|---|
| * &#128273;  &#11019; | actor\_id| integer  DEFAULT nextval('pagila.actor_actor_id_seq'::regclass) |
| * | first\_name| varchar(45)  |
| * &#128270; | last\_name| varchar(45)  |
| * | last\_update| timestamp  DEFAULT now() |

Les lignes de la able `actor` sont identifiées par la colonne `actor_id`. Deux lignes différentes peuvent coïncider sur les colonnes `first_name`  et `last_name` mais elles doivent se distinguer sur la colonne `actor_id`. La colonne `actor_id`  est la *clé primaire*  de la table `actor`.


### Table pagila.category 
| | | |
|---|---|---|
| * &#128273;  &#11019; | category\_id| integer  DEFAULT nextval('pagila.category_category_id_seq'::regclass) |
| * | name| varchar(25)  |
| * | last\_update| timestamp  DEFAULT now() |

Un film relève d'une ou plusieurs catégories (`horror`, `children`, ...). 
La table `category` liste les catégories utilisées dans `pagila`.
Les lignes de cette table sont disinguées par la colonne `category_id`.



### Table pagila.country 
| | | |
|---|---|---|
| * &#128273;  &#11019; | country\_id| integer  DEFAULT nextval('pagila.country_country_id_seq'::regclass) |
| * | country| varchar(50)  |
| * | last\_update| timestamp  DEFAULT now() |




### Table pagila.film 
| | | |
|---|---|---|
| * &#128273;  &#11019; | film\_id| integer  DEFAULT nextval('pagila.film_film_id_seq'::regclass) |
| * &#128270; | title| varchar(255)  |
|  | description| text  |
|  | release\_year| integer  |
| * &#128270; &#11016; | language\_id| smallint  |
| &#128270; &#11016; | original\_language\_id| smallint  |
| * | rental\_duration| smallint  DEFAULT 3 |
| * | rental\_rate| varchar(4)  DEFAULT 4.99 |
|  | length| smallint  |
| * | replacement\_cost| varchar(5)  DEFAULT 19.99 |
|  | rating| mpaa\_rating  DEFAULT 'G'::pagila.mpaa_rating |
| * | last\_update| timestamp  DEFAULT now() |
|  | special\_features| text[]  |


La table `film` contient le catalogue de la chaine de magasins de `DVD`.  Les lignes de cette table sont distinguées par la colonne `film_id`. Deux lignes distinctes peuvent coïncider sur la colonne `title`. 

La colonne `original_language_id` permet de repérer la langue de la version originale du film. La colonne `language_id` permet de repérer la langue dans laquelle le DVD est éditée. Ces informations doivent être recollées à l'aide de la table `language`. Les valeurs prises par les colonnes `language_id` et `original_language_id` doivent obligatoirement réferrer à des valeurs recontrées dans la colonne `language_id`  de la table `language`. On parle de *contraintes référentielles*.

##### Foreign Keys
| | | |
|---|---|---|
|  | film_original_language_id_fkey | ( original\_language\_id ) ref [pagila.language](#language) (language\_id) |
|  | film_language_id_fkey | ( language\_id ) ref [pagila.language](#language) (language\_id) |




### Table pagila.film_actor 
| | | |
|---|---|---|
| * &#128273;  &#11016; | actor\_id| smallint  |
| * &#128273;  &#11016; | film\_id| smallint  |
| * | last\_update| timestamp  DEFAULT now() |


##### Foreign Keys
| | | |
|---|---|---|
|  | film_actor_film_id_fkey | ( film\_id ) ref [pagila.film](#film) (film\_id) |
|  | film_actor_actor_id_fkey | ( actor\_id ) ref [pagila.actor](#actor) (actor\_id) |


La table `film_actor` est une table intermédiaire qui permet de savoir quels acteurs jouent dans quels films.



### Table pagila.film_category 
| | | |
|---|---|---|
| * &#128273;  &#11016; | film\_id| smallint  |
| * &#128273;  &#11016; | category\_id| smallint  |
| * | last\_update| timestamp  DEFAULT now() |


La table `film_category` est une table intermédiaire qui permet de savoir de quelles catégories relève un film.


##### Foreign Keys
| | | |
|---|---|---|
|  | film_category_film_id_fkey | ( film\_id ) ref [pagila.film](#film) (film\_id) |
|  | film_category_category_id_fkey | ( category\_id ) ref [pagila.category](#category) (category\_id) |




### Table pagila.language 
| | | |
|---|---|---|
| * &#128273;  &#11019; | language\_id| integer  DEFAULT nextval('pagila.language_language_id_seq'::regclass) |
| * | name| char(20)  |
| * | last\_update| timestamp  DEFAULT now() |





