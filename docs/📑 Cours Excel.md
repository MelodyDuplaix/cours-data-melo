---  
number headings: first-level 2, max 6, start-at 1, 1.1)  
aliases:  
  - Excel  
nature: note  
tags:  
  - logiciel  
  - formation  
  - data  
  - cours  
cssclasses:  
  - banner-image  
share: true  
---  
  
![banner](./image/image%20-%20%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel.png#)  
  
[Cefim note principale](../CEFIM%20note%20principale.md#)  
  
---  
[Cours sur internet](https://linen-safflower-595.notion.site/Formation-Tableurs-7bc273c2e2ce482ca4b4f73ab94e85de) ^01489d  
>[!SUMMARY]+  
>```toc  
>```  
## 1) Principes de bases  
  
### 1.1) Plages de valeurs  
**vecteur**: liste de valeurs(ligne ou colonne), l'adresse est définie par ses 2 cellules extrêmes séparées de deux points[:]  
**matrice**: table de valeurs, caractérisée par les deux cellules extrêmes (haut-gauche et bas-droite)  
  
### 1.2) Adressage  
**adressage relatif**: adressage par défaut, `C5*D5` <br>**adressage absolu**: bloque le décalage d'une ou plusieurs cellules, précédé d'un dollar,  `$C$5*$D$5`<br>**adressage mixte**: seule une partie de la référence est fixe, `C$5`  
**<span style="background:#fff88f">raccourci</span>**:  F4 quand on sélectionne une cellule pour rapidement changer l'adressage  
  
## 2) Calcul et fonctions  
  
### 2.1) Fonctions statistiques  
**somme**  
**moyenne**  
**min**  
**max**  
**médiane**  
 **nb**, nombre de nombre  
 **nbval**, nombre de cellules non vides  
 **ecartype**  
 **nb.vide**, nombre de cellules vides  
  
### 2.2) Fonctions de recherche  
**recherchev** et **rechercheh** s'utilisent de la même manière  
  
#### 2.2.1) Recherche avec un intervalle  
 syntaxe: =recherchev(valeur que l'on cherche; matrice ou l'on cherche; numéro de colonne dans la matrice de la valeur à renvoyer; VRAI )  
 Exemple:  
![📑 Aide mémoire Excel - image - 1.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%201.png#)  
 Commentaire=`RECHERCHEV(D8; $J$8:$K$12; 2; VRAI)`  
  
#### 2.2.2) Recherche précise  
syntaxe: =recherchev(valeur que l'on cherche; matrice ou l'on cherche; numéro de colonne dans la matrice de la valeur à renvoyer; FAUX )  
Exemple:  
![📑 Aide mémoire Excel - image - 2.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%202.png#)  
Prénom=`RECHERCHEV(H7; B3:D6; 3; FAUX)`  
Exemple avec If:  
![600](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%203.png#)  
  
#### 2.2.3) EQUIV  
Permet de recherche un élément spécifique dans une plage de cellule puis renvoie la position relative de l'élement dans la plage.  
syntaxe: `MATCH(valeur que l'on cherche; matrice où l'on cherche; type(0 en cas normal, -1 ou +1 pour des cas particuliers))`  
  
Exemple:  
![📑 Aide mémoire Excel - image - 4.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%204.png#)  
Rang=`MATCH(G3; C4:C10; 0`  
  
#### 2.2.4) Index  
renvoie une valeur d'un tableau avec les numéros de lignes et de colonnes  
syntaxe:`INDEX(matrice où l'on cherche; numéro de ligne; numéro de colonne)`  
Exemple:  
![📑 Aide mémoire Excel - image - 5.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%205.png#)  
  
### 2.3) Fonctions logiques  
  
#### 2.3.1) Si  
La fonction si simple permet d'avoir 2 résultats, le premier est appliqué si la comparaison est vérifié, sinon c'est le deuxième.  
syntaxe:=`SI(test logique; resultat si vrai; resultat si faux`  
  
opérateur de comparaisons disponibles: =, >, <, >=, <=, <>  
  
#### 2.3.2) Et/Ou/Non  
On ne peut pas écrire plusieurs comparaison dans un test logique. Pour écrire 12 < A2 < 16 , on doit donc écrire `ET(12<A2; A2<16)`.  
  
### 2.4) Fonctions d'information  
  
#### 2.4.1) EstErreur  
Renvoie True si une valeur renvoie une erreur( /#NA, /#Value, /#REF, /#DIV/0, /#NUM, /#NAME?, /#NULL!)  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%206.png#)  
#### 2.4.2) SiErreur  
Renvoie le résultat de la formule s'il n'y a pas d'erreur, ou une autre valeur s'il y a un problème  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%207.png#)  
  
### 2.5) Fonctions d'agrégations  
  
#### 2.5.1) NbSi/SommeSi/MoyenneSi  
Permet de compter les cellules, la moyenne ou la somme des cellules qui correspondent à un critère.  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%208.png#)  
  
> [!hint|c-yellow c-p-sm]-  
> quand on souhaite faire intervenir la valeur d’une cellule dans le critère il faut réaliser une concaténation avec & entre le signe et la référence.  
> ![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%209.png#)  
  
#### 2.5.2) NbSiEns/SommeSiEns  
Fonction similaire mais avec plusieurs conditions  
  
#### 2.5.3) SommeProd  
renvoie la somme des produits de 2 matrices de même forme  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2010.png#)  
#### 2.5.4) Rang  
renvoie le rang d'une valeur numérique dans une liste de valeur données  
  
> [!hint|c-yellow c-p-sm]-  
> Si on imbrique beaucoup de fonctions les unes dans les autres, on peut étirer la zone d'écriture pour gagner en lisibilité  
>![400](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2011.png#)  
>![400](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2012.png#)  
  
## 3) Formatage  
  
le **format** fait référence à la police, au remplissage, à l'alignement, au bordures et au nombre  
  
#### 3.1.1) Formatage personnalisé  
On peut créer ses propres format de données. Quelques exemples utiles:  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2013.png#)  
> [!attention] Penser à mettre les espaces entre " " sinon Excel les interprète comme division par 1000  
  
### 3.2) Mise en forme conditionnelle  
  
Permet de mettre en évidence les éléments dans vos données à partir de règles qui déterminent le format des cellules en fonctions de leurs valeurs  
- format par contenu de cellules  
- échelle de couleurs par échelle de valeurs  
- règles personnalisés, avec notre propre formule  
  
>[!TIP] On peut copier un formatage conditionnel avec le pinceau de format  
  
## 4) Faciliter l'usage du classeur  
  
Le classeur doit être pensé pour deux types de personnes:  
- Utilisateurs: minimiser le risque d'erreurs, on fait en sorte que l'utilisateur utilise le tableau comme on le souhaite (data validation)  
- Développeur: de façon à ce qu'un autre développeur puisse le reprendre et comprendre sa construction, ses fonctions  
  
### 4.1) Limiter les choix de l'utilisateur  
  
Grâce à la validation de données, l'utilisateur ne peut pas rentrer de données qui marquerait des erreurs.  
On peut utiliser une liste prédéterminée, ou une échelle de valeur  
  
### 4.2) Nommer une cellule ou une plage de valeur  
En remplaçant en haut à gauche la référence de cellule par un nom, pour pouvoir l'utiliser de façon plus naturel  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2014.png#)  
Il vaut mieux limiter l'usage des plages de données le plus possible  
  
## 5) Les Tableaux croisés dynamiques  
  
Un tableau croisé dynamique est un tableau de valeurs groupées qui regroupe les éléments individuels d'un tableau plus étendu ( ex: d'une base de données ) dans une ou plusieurs catégories distinctes. Ce résumé peut inclure des sommes, des moyennes ou d'autres statistiques, que le tableau croisé dynamique regroupe à l'aide d'une fonction d'agrégation choisie appliquée aux valeurs groupées.  
Il ne se met pas automatiquement à jour à chaque changement de la base de données.  
  
### 5.1) Prérequis  
Il faut une base de données relationnelle: lignes représentant un enregistrement et colonnes représentant un champs de données avec des en-têtes de colonnes dans la première ligne.  
  
### 5.2) Champs calculés  
Cela permet d'ajouter un champ directement dans le TCD avec une formule, faite avec des champs qui existent déjà. Il est toujours calculé au niveau de détail du TCD  
  
## 6) Analyse des données  
  
### 6.1) Trier  
On peut trier du texte, des nombres et des dates, il faut avant vérifier que les valeurs sont au bon format.  
  
### 6.2) Filtrer  
Permet d'afficher ou de masquer des valeurs dans une ou plusieurs colonnes. On peut utiliser diverses conditions préconfigurés ou en créer une.  
  
## 7) Visualisations  
  
pivot chart: issu d'un TCD  
  
### 7.1) Changement dans la durée  
avec une courbe  
exemple:  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2015.png#)  
Ce graphique répond aux questions:  
- Comment cette mesure a-t-elle évolué au cours de l'année passé ?  
- Quand cette mesure a-t-elle changé ?  
- Avec quelle rapidité cette mesure a-t-elle changé ?  
  
### 7.2) Comparer et classer des données  
avec des barres/histogrammes  
exemple:  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2016.png#)  
Ce graphique répond aux questions:  
- Quel membre de cette dimension présente la mesure la plus élevée ?  
- Y a-t-til des dimensions exceptionnelles ?  
- Quelle est l'étendue de l'écart entre la mesure la plus basse et la plus élevée entre ces deux dimensions ?  
  
On peut aussi choisir entre utiliser un graphique en barre groupé ou un graphique en barre superposé.  
  
### 7.3) Visualiser une représentation en pourcentage  
avec un camembert ou donut, pour montrer ce qu'un élément individuel représente dans un tout  
exemple:  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2017.png#)  
Ce graphique répond aux questions:  
- Quelle est la contribution de cette valeur au total ?  
- Comment la répartition des frais change-t-elle chaque année ?  
- Les différents articles apportent ils différents montants de ventes par région ?   
  
### 7.4) Autres graphiques utiles  
qui ne sont pas accessibles directement avec les TCD  
  
Pour cela, on peut recopier le TCD a coté, en mettant `\=première cellule` dans une cellule, puis en continuant avec la poignée de recopie.  
  
#### 7.4.1) Graphiques avec hiérarchie/rayons de soleils  
pour mettre en avant un rapport hiérarchique  
exemple:  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2018.png#)  
  
#### 7.4.2) Combinaison de graphiques  
pour montrer comment évoluent différentes mesures ensembles  
exemple:  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2019.png#)  
  
#### 7.4.3) Visualisation géographique  
pour les intégrer dans une carte  
exemple:  
![300](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2020.png#)  
  
## 8) Dashboard  
  
### 8.1) Slicers et timeline  
Ce sont des filtres simplifiés pour les dashboards  
>[!WARNING] Attention, tous les TCD et éléments que l'ont veut filtrer doivent être exactement sur les mêmes plages de la base de données, donc faire attention à ce que la base de données soit un tableau avant de réaliser des TCD  
  
### 8.2) Bonnes pratiques  
Un tableau de bord bien conçu peut harmoniser les efforts de votre organisation, contribuer à  
révéler des informations majeures et accélérer le processus décisionnaire.  
  
- Connaître votre objectif et votre public  
	- Quel message veut-on transmettre ?  
	- Conclusion ou question clé ?  
	- Public novice ou qui maîtrise le sujet ?  
	- De quel type de repère a-t-il besoin ?  
- Exploiter l'endroit le plus visité  
	- partie supérieur gauche  
- Limiter le nombre de graphique  
	- 2 ou 3 max  
- Désencombrer la vue  
	- 1 ou 2 palette de couleurs max  
	- supprimer les textes, lignes, trames de fond, légendes, qui ne fournissent pas d'informations  
- Limiter les couleurs  
  
### 8.3) Construire la structure du dashboard  
exemple:  
![400](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2021.png#)  
  
Pour obtenir ceci, on peut commencer par créer les formes avec des rectangles, et bien les aligner  
  
### 8.4) KPI  
Une KPI est un chiffre clé qui sera dynamique  
exemple:  
![200](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2022.png#)  
On peut utiliser 2 formes, et rajouter la référence à la formule dans la 2ème forme avec la barre de formule  
On peut ensuite grouper les 2 boites et les dupliquer  
  
### 8.5) Ajouter les graphiques  
Il ne reste alors plus qu'a ajouter les graphiques en les copiant-collant  
  
Avec Google Sheets, tous les éléments doivent être sur la même feuille et l'on ne pourra pas faire des copier-coller. Les TCD seront sur la même feuille que le dashboard et il faudra donc les cacher en cachant des lignes.  
  
Enfin, pour bien terminer un dashboard, on peut enlever les barres de formules et références; cacher les onglets inutiles voir les verrouiller, et grouper tous le dashboard  
  
## 9) Ressource  
<iframe title="Excel Pivot Tables EXPLAINED in 10 Minutes (Productivity tips included!)" src="https://www.youtube.com/embed/UsdedFoTA68?feature=oembed" height="113" width="200" style="aspect-ratio: 1.76991 / 1; width: 80%; height: 80%;" allowfullscreen="" allow="fullscreen"></iframe>  
  
  
%%  
parent:: [Cefim note principale](../CEFIM%20note%20principale.md#)  
image:: [📑 Aide mémoire Excel - image - 1.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%201.png#), [📑 Aide mémoire Excel - image - 2.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%202.png#), [📑 Aide mémoire Excel - image - 3.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%203.png#), [📑 Aide mémoire Excel - image - 4.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%204.png#), [📑 Aide mémoire Excel - image - 5.png, 📑 Aide mémoire Excel - image - 6.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%205.png,%20%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%206.png#), [📑 Aide mémoire Excel - image - 7.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%207.png#), [📑 Aide mémoire Excel - image - 8.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%208.png#), [📑 Aide mémoire Excel - image - 9.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%209.png#), [📑 Aide mémoire Excel - image - 10.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2010.png#), [📑 Aide mémoire Excel - image - 11.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2011.png#), [📑 Aide mémoire Excel - image - 12.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2012.png#), [📑 Aide mémoire Excel - image - 13.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2013.png#), [📑 Aide mémoire Excel - image - 14.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2014.png#), [📑 Aide mémoire Excel - image - 15.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2015.png#), [📑 Aide mémoire Excel - image - 16.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2016.png#), [📑 Aide mémoire Excel - image - 17.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2017.png#), [📑 Aide mémoire Excel - image - 18.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2018.png#), [📑 Aide mémoire Excel - image - 19.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2019.png#), [📑 Aide mémoire Excel - image - 20.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2020.png#), [📑 Aide mémoire Excel - image - 21.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2021.png#), [📑 Aide mémoire Excel - image - 22.png](%F0%9F%93%91%20Aide%20m%C3%A9moire%20Excel%20-%20image%20-%2022.png#),   
%%  
  
  
  
---  
[Cefim note principale](../CEFIM%20note%20principale.md#)