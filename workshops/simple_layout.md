

### Table public.region 
Region(nom, population, prefecture)

| | | |
|---|---|---|
| * &#128273;  &#11019; | nom| text  |
|  | population| integer  |
| &#11016; | prefecture| char(5)  |


##### Foreign Keys
| | | |
|---|---|---|
|  | fk_region_ville | ( prefecture ) ref [public.ville](#ville) (code\_postal) |




### Table public.ville 
`Ville(nom, nom\_gare, code\_postal, region)`

| | | | |
|---|---|---|---|
| * | nom| text  |  |
|  | nom\_gare| text  |  |
| * &#128273;  &#11019; | code\_postal| char(5)  | 5 caractères reprèsentant des entiers |
| * &#11016; | region| text  |  |


##### Foreign Keys
| | | |
|---|---|---|
|  | fk_ville_region | ( region ) ref [public.region](#region) (nom) |





