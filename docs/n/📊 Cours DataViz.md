---  
cssclasses:  
  - banner-image  
number headings: first-level 2, max 6, start-at 1, 1.1)  
aliases:  
  - dataviz  
nature: cours  
tags:  
  - cours  
  - logiciel  
  - data  
  - dataviz  
share: true  
---  
  
![banner higher](../image/image%20-%20%20Cours%20DataViz%20-%20banniere.png#)  
  
[Cefim note principale](../../CEFIM%20note%20principale.md#)  
  
---  
 > [!summary]+  
><pre class="dataview dataview-error">Evaluation Error: SyntaxError: Unexpected token '&gt;'  
    at DataviewInlineApi.eval (plugin:dataview:18404:21)  
    at evalInContext (plugin:dataview:18405:7)  
    at asyncEvalInContext (plugin:dataview:18415:32)  
    at DataviewJSRenderer.render (plugin:dataview:18436:19)  
    at DataviewJSRenderer.onload (plugin:dataview:18020:14)  
    at e.load (app://obsidian.md/app.js:1:720327)  
    at DataviewApi.executeJs (plugin:dataview:18954:18)  
    at eval (plugin:obsidian-mkdocs-publisher:28:2026)  
    at Generator.next (&lt;anonymous&gt;)  
    at eval (plugin:obsidian-mkdocs-publisher:2:871)  
    at new Promise (&lt;anonymous&gt;)  
    at m (plugin:obsidian-mkdocs-publisher:2:691)  
    at Gf (plugin:obsidian-mkdocs-publisher:28:1256)  
    at eval (plugin:obsidian-mkdocs-publisher:28:3257)  
    at Generator.next (&lt;anonymous&gt;)  
    at r (plugin:obsidian-mkdocs-publisher:2:729)</pre>  
  
![image - 📊 Cours DataViz  - 1.png](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%201.png#)  
  
- [x] à reprendre avec le diapo , les éléments avec un x italique ✅ 2023-05-09  
  
L'enjeu n'est pas la donnée, qui augmente de façon exponentielle, mais de les exploiter et de leur donnée du sens.  
Comment faire sens des données, les utiliser dans les processus de décision, ne pas être surchargé.  
  
## 1) Apprendre à décomposer une visualisation  
  
### 1.1) Sémiologie graphique  
Mettre des règles communes, établit un language commun sur la façon sont on construit une visualisation  
L'ensembles des règles permettant l'utilisation d'un système graphique de signes pour la transmission d'une information correcte et accessible au lecteur.  
Comment définir ces variables graphiques ? Quels sont les éléments modifiables dans une visualisation ? Quels sont ceux qui rendent une visualisation efficace et pertinente ?  
- visuel: obéir aux règles générales de la perception  
- Universel: compréhensible par tous  
- Clair et cohérent: éviter les redondances et la surcharge d'informations  
  
#### 1.1.1) Composants  
- données(que veut on montrer)  
- esthétique(comment va t-on le montrer)  
- echelle(comment passe-t-on des données à la visualisation)  
- objets géométriques(sortes de marqueurs visuels): aires, barres, lignes, pictogrammes  
- statistiques(statistiques)  
- facettes(comment on divises les données en multiples représentations)  
- système de coordonnées(comment positionner les différentes données sur l'écran): polaires, logarithmiques, tridimensionnels  
  
<font color="#05b305">Exemple avec les graphiques du diapo:</font>  
**données**: 4 graphiques de 11 points  
**esthétiques:** grille, 4\*4, 2 axes chacun, utilisation de couleurs différentes pour chaque jeu de données  
**echelle:** points mappées linéaires sur un axe allant de 0-21 et 0-13  
**objets géométriques:** des points, pareille pour tous les nuages de points  
**statistiques:** dispersion des points en comparaison avec une régression linéaire  
**facettes**: graphes séparées et non un seul, donc 4 facettes  
**système de coordonnées**: valeurs brute représentées sur des axes dons  l'espace x/y(coordonnées cartésiennes)  
  
<font color="#05b305">Exercice avec le graphique du diapo:</font>  
**données**: 1 graphique de 5 secteurs, inflation en pourcentage de 5 produits au cours du temps  
**esthétiques**: grille, 30\*9, graphique en baton  et courbe de tendance, évolution, et couleurs  
**l'échelle:** axe linéaire allant de -1 à 7, axe de abscisse de 2021 à 2023  
**objets géométriques:** barres combinées par secteurs, et lignes  
**statistiques:** evolution des prix en fonction du temps, données brutes  
**facettes:** 1 graphe reprenant tous les secteurs -> 1 facette  
**système de coordonnées:** représentées dans des axes x/y(coordonnées cartésiennes)  
ici, le fait de réunir en un seul graphique n'était pas forcément adéquat si l'on veut montrer les tendances individuelles des secteurs  
  
## 2) Vocabulaire  
![image - 📊 Cours DataViz  - 2.png](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%202.png#)  
**attribut**: mesure ou observation d'une grandeur (couleur, forme, taille)  
**classe**: catégorie  
**élément item ou individu**: entité individuelle avec toutes ses caractéristiques  
**lien**: relation entre 2 éléments  
  
#### 2.1.1) Le Mapping  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%203.png#)  
on passe d'unespace de données à un espace de visualisation  
  
Quel encodage visuel dois-je utiliser ?  
Comment élaborer une représentation visuelle à partir des données brutes ?  
Quels sont les motifs que l'ont va utiliser pour faire ressortir nos données et les rendre compréhensibles ?  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%204.png#)  
  
## 3) propriétés graphiques  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%205.png#)  
permet d'exprimer visuellement l'inportance des données, on choisit avec le type de données  
  
**forme**  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%206.png#)  
  
Nous pouvons utiliser la façon dont nous percevons les éléments et notre intuition des différents canaux visuels (formes, couleurs…) pour choisir ceux adéquats par rapport à la façon dont les données changent  
**expressivité**: l'encodage visuel doit exprimer uniquement l'information de l'attribut visuel  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%207.png#)  
**efficacité:** l'importance de l'attribut doit transparaître dans le choix du canal utilisé  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%208.png#)  
  
Exercice dataviz avec 3 jeux de données:  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%209.png#)  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2010.png#)  
  
  
Les couleurs peuvent conduire à une mauvaise interprétations. Il faut essaye d'aligner le sens sémantique des données avec les couleurs que l'on va utiliser pour les représenter.  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2011.png#)  
  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2012.png#)  
  
Plus les marqueurs sont petits, plus les couleurs doivent être distinguables  
  
Recap :  
![image - 📊 Cours DataViz  - 13.png](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2013.png#)  
![image - 📊 Cours DataViz  - 14.png](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2014.png#)  
  
  
### 3.1) types de données :  
  
[listroot(root((types de données)))|list2mindmap]  
- variables qualitatives  
	- variables ordinales  
	- variables catégoriques  
- variables quantitatives  
	- variables disrètes  
	- variables continues  
  
couleur des yeux: qualitative catégorique  
sexe d'une personne: qualitative catégorique  
nombre d'articles dans un magasin: qualitative discrète  
taille d'une personne: quantitative continue  
taille d'un vêtement: quantitative discrète  
note: quantitative discrète ou qualitative ordinale  
température:  quantitative continue  
nombre d'enfant: quantitative discrète  
  
## 4) Types de graphiques  
ressources pour des types variées:  
https://datavizproject.com/  
https://www.data-to-viz.com/  
  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2015.png#)  
pour montrer des comparaisons entre des catégories  
  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2016.png#)  
généralement pour montrer comment une information en deux dimensions change à travers le temps  
  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2017.png#)  
pour rapidement voir les termes les plus importants  
  
![hs-med](image%20data%2018.md#)  
pour montrer une comparaison  
  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2019.png#)  
pour montrer comment une valeur initiale est affecté par une série de valeurs positives ou négatives  
  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2019.png#)  
pour montrer comment une variable change selon 3 composants  
  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2020.png#)  
pour montrer la composition en 3 éléments de plusieurs éléments  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2021.png#)]  
pour montrer rapidement une évolution  
  
SCATTER WITH MARGINAL POINT  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2022.png#)  
pour montrer la relation entre 2 variables et leur distribution  
  
Graphique tige et feuille  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2023.png#)  
pour voir la répartition d'une variable  
  
  
## 5) Règles de bases  
  
**digrammes en barres ou histogrammes:** variables quantitatives, si continues on peut les regrouper en classe  
**digramme en secteur:** variables qualitatives si pas beaucoup de classes  
**nuage de points**(+bloxplot): variables quantitatives continues, idée simple de la façon dont les données sont dispersées, boite à mouche: valeurs aberrantes et extrêmes  
  
| données                           | type de données                               | type de diagramme                 |  
|:--------------------------------- |:--------------------------------------------- |:--------------------------------- |  
| couleur des yeux                  | qualitative catégorique                       | secteur                           |  
| sexe d'une personne               | qualitative catégorique                       | secteur                           |  
| nombre d'articles dans un magasin | qualitative discrète                          | histogramme                       |  
| taille d'une personne             | quantitative continue                         | nuage de points, boit à moustache |  
| taille d'un vêtement              | qualitative catégorique                       | secteur                           |  
| note                              | quantitative discrète ou qualitative ordinale | histogramme                       |  
| température                       | quantitative continue                         | nuage de point ou courbe          |  
| nombre d'enfant                   | quantitative discrète                         | histogramme ou secteur            |  
  
![hs-med](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2024.png#)  
  
  
### 5.1) Exercice pratique  
  
#### 5.1.1) Critiques et points positives  
\- beaucoup d'informations donc perdue visuellement  
\- on ne voit pas bien les différences entre les pays qui sont minimes  
\- manque de différences de couleur entre l'espérance de vie et l'âge moyen de départ à la retraite  
  
\+ titre clair, tous les éléments du graphiques et source  
\+ la moyenne générale se voit assez vite visuellement  
\+ les différences de couleurs selon le sexe  
\+ les histogrammes sont un bon choix  
  
#### 5.1.2) Quel est le message  
On cherche à montrer l'âge moyen de départ à la retraite, selon les pays de l'OCDE, et en particulier celui de la France, pour le comparer par rapport aux autres pays. On cherche aussi à montrer que l'espérance de vie après le départ à la retraite est plus élevé chez les Français que dans les autres pays de l'OCDE.  
  
#### 5.1.3) A qui est-elle destinée ?  
Elle est destinée à l'ensemble de la population qui chercheraient à comprendre l'âge de la retraite en France par rapport à d'autres pays.  
  
#### 5.1.4) Les différents composants  
- données: âge moyen d'espérance de vie et de départ à la retraite pour les 12 pays de l'OCDE, 4 jeux de données de 12 pays  
- esthétique: barre coloré selon le sexe et selon les 2 variables départ à la retraite et espérance de vie  
- echelle: barre mappée de 0 à 90  
- objets géométriques: barres de couleurs  
- statistiques: données brutes de moyennes  
- facettes: 1 seul facette représentant 4 ensemble de données  
- système de coordonnées: valeurs brutes représenté dans un seul axe en ordonnées  
  
#### 5.1.5) Alternative au graphique  
![600](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2025.png#)  
et un autre idem pour les hommes  
  
> [!TIP| background-red]  
> - jouer sur les contrastes  
> - jouer sur les couleurs  
> - l'oeil doit être attiré par le message  
> - respecter les conventions (temps en x)  
> - ne jamais présenter un chiffre seul sans comparaison, ou en comparaison avec des chiffres qui ne représentent pas la même chose  
> - ne pas introduire plusieurs éléments en même temps, ou les afficher les uns après les autres  
> - Expliquer le contexte  
  
![300](../image/image%20-%20%F0%9F%93%8A%20Cours%20DataViz%20%20-%2026.png#)  
  
## 6) Construire une dataviz pertinente  
  
### 6.1) Méthodologie d'une dataviz  
- cadrer le projet  
- nettoyer et explorer (repérer les infos manquantes et les erreurs, s'ouvrir à pleins de pistes)  
- co-construire (échange avec les métiers, trouver les bons indicateurs)  
- simplifier et épurer (pour présenter, message clair, compréhensible et sans ambiguïté, retire les fioritures, effacer ce qui est redondant, montrer la donnée, gagner en visibilité sans perdre l'information)  
- publier ou déployer et itérer (demander un feedback)  
  
#### 6.1.1) Cadrer  
**pourquoi**: quel est l'objet de la visualisation ? Objectifs opérationnels A quels besoins la visualisation doit-elle répondre  
savoir déterminer quels sont les objectifs des utilisateurs finaux (explorer, comparer, confirmer, présenter)  
**comment**: Quels éléments vont me permettre de servir les objectifs ? Quel support doit-on fournir ?  
comment l'utilisateur compte interagir avec la données -> support adéquat (navigation: dashboard, organisation: synthèse ou dashboard statique, établir des relations)  
**qui**: A qui est elle destinée ?(profil-nb d'utilisateurs) Qui sont les parties prenantes ? Qui sont ceux qui disposent des informations dont je dispose ?  
**quoi**: Que souhaite-on montrer , mettre en évidence, alerter ? Quelles sont les données en entrées et quelles statistiques ?  
évaluer la qualité, la nature et le sens de la donnée (type, complète ?, qualité ?, analyse)  
**quand**: Dans quel délai ? Prendre en compte la date de mise à disposition/contraintes métiers/rafraichissement des données…  
**où**: Où sont les données ?  
  
Analyse:  
- Pour chacune des variables à considerer:  
	- au niveau micro: points individuels, cas particulier, valeurs spécifiques  
	- au niveau macro: tendances générales, statistiques classiques, moyenne, médianes  
- Pour plusieurs variables à considérer, on cherche les liens et les corrélations entre elles  
  
### 6.2) L'approche Five design Sheet  
  
>[!WARNING] Long, se fixer des horaires  
  
source:  
[https://towardsdatascience.com/five-design-sheet-methodology-approach-to-data-visualisation-603d760f2418](https://towardsdatascience.com/five-design-sheet-methodology-approach-to-data-visualisation-603d760f2418)  
![no-h](../../M%C3%A9thode%20Five%20design%20sheet.md#highlights)  
[The Five Design Sheet Methodology](../../The%20Five%20Design%20Sheet%20Methodology.md#)  
### 6.3) Application  
#### 6.3.1) Identifier un problème  
Identifier les compagnies par prix moins cher ou par temps de trajet ou par nombre d'escales pour un trajet  
Identifier les destinations les moins chers  
  
#### 6.3.2) Imaginer  un cas d'applications avec les 5 W  
pourquoi: permettre au voyageur de choisir son vol avec son prix ou son temps de trajet, explorer et comparer  
comment: dashboard dynamique  
quoi: données: informations et prix des vols proposées par les compagnies aériennes, données complètes sauf une ligne non remplies qui sera écarté, de qualité  
quand: délai 1h15, non connaissance de la date de rafraichissement des données, besoin de rafraichissement  
qui: demande de la part de particuliers ou d'une compagnie de voyage  
  
#### 6.3.3) Elaborer une maquette avec la méthode des FDS  
https://onedrive.live.com/edit.aspx?resid=D91836E916F7A72C!437&ithint=file%2cpptx&authkey=!AEYW5QtqpOTPOxE  
  
A rajouter comme idée problématique ? Est-ce que toutes les régions sont desservies de manière égale ou l'une est favorisé ?  
  
  
## 7) Manipuler son auditoire ou ne pas commettre des erreurs  
  
Notre cerveau fait un test visuel lorsque l'on voit une image, il formule des hypothèses.  
La datavisualisation s'appui sur des méthodes de comparaisons implicites et explicites  
explicite: couleur, forme, orientation  
  
Les données ne mentent pas, mais on peut facilement de faire mentir des graphiques ou stats par erreur, ignorance, ou tromperie.   
  
L'agencement de la visualisation est toujours porteuses d'un message et peut parfois véhiculer certains biais.  
  
### 7.1) Les erreurs les plus courantes  
- Faire des erreurs mathématiques (moyennes et médiane confuses par exemple)  
- Omettre une partie des données (ex: courbe où l'on met 1 année sur 2 pour cacher les baisses )  
- Jouer sur les axes et échelles (ex: mettre des doubles axes avec des 2 échelles totalement différentes, distordre les axes, échelle qui ne commence pas à 0)  
- Jouer sur la taille des éléments graphiques (ex: éléments plus gros pour mettre en avant un certain élément)  
- Jouer sur les couleurs (ex: ne pas répartir les couleurs comme les chiffres le montrent, mettre les mauvaises couleurs)  
- Préférer l'esthétique à l'information (ex: graphique où l'on ne comprend rien, esthétique qui n'a aucun sens)  
- Surcharger la visualisation  
- Utiliser une représentation visuelle non adéquate ou non conforme aux données (ex: corrélations qui n'ont aucun sens, faux calculs de pourcentage, évolution cumulative, échelle non conforme, évolution en pourcentage par rapport à quoi ?, diagramme en secteur en 3D)  
  
  
  
%%  
parent:: [Cefim note principale](../../CEFIM%20note%20principale.md#)  
enfant:: [Méthode Five design sheet](../../M%C3%A9thode%20Five%20design%20sheet.md#), [The Five Design Sheet Methodology](../../The%20Five%20Design%20Sheet%20Methodology.md#), [Méthode Five design sheet](../../M%C3%A9thode%20Five%20design%20sheet.md#)  
%%  
  
  
---  
[Cefim note principale](../../CEFIM%20note%20principale.md#)