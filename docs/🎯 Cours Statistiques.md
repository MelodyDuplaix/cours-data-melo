---  
number headings: first-level 2, max 6, start-at 1, 1.1), auto  
aliases:  
  - statistiques  
nature: cours  
tags:  
  - cours  
  - data  
  - formation  
cssclasses:  
  - banner-image  
share: true  
---  
  
![banner](./image/image%20-%20%20Cours%20Statistiques%20-%20banniere.png#)  
  
> [!summary]- Sommaire  
> <pre class="dataview dataview-error">Evaluation Error: SyntaxError: Unexpected token '&gt;'  
    at DataviewInlineApi.eval (plugin:dataview:18404:21)  
    at evalInContext (plugin:dataview:18405:7)  
    at asyncEvalInContext (plugin:dataview:18415:32)  
    at DataviewJSRenderer.render (plugin:dataview:18436:19)  
    at DataviewJSRenderer.onload (plugin:dataview:18020:14)  
    at e.load (app://obsidian.md/app.js:1:720143)  
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
  
## 1) A quoi sert les statistiques ?  
   - A les comprendre  
   - A les "analyser"  
   - A les organiser  
      <font color="#05b305">C'est la science qui permet de prendre des notes de toutes les données et d'expliquer les évènements ou de comprendre les phénomènes mis en jeu en apportant une objectivité dans l'interpretation. Elle permet ainsi de prendre des décisions fondées dur la connaissance des fait et d'établir des relations.</font>  
### 1.1) Etapes  
- <font color="#974806">Collecter les données utiles (achats, avis clients, ventes, données clients</font> :  
  - comprendre la problématiques métiers, a quoi mes données vont-elles servir ?  
  - sélectionner un échantillon représentatif de la population que l''on cherche à étudier  
  - Comprendre les enjeux du pronlème  
  - Interroger les parties prenantes  
  - Faires l'inventaire des ressources  
  - Collecter les données nécessaires manquantes  
- <font color="#974806">Trier, ordonner, calculer, analyser</font>  
- <font color="#974806">Visualiser les indicateurs pertinents</font>  
  - voir les tendances et les valeurs aberrantes, visualisation plus rapide  
- <font color="#974806">Interprétez les résultats pour prendre les décisions adéquates</font>  
  - alerter les services concernés  
### 1.2) Pourquoi ne pourrait-on pas se suffire d'une analyse purement humaine ? ([Gapminder](https://www.gapminder.org/))  
- Le cerveau n'est pas capable de traiter une quantité volumineuse d'informations  
- L'analyse humaine induit des biais psychologiques comme le biais de confirmations  
  
## 2) Définition du cadre de travail  
- Statistique descriptive  
  - décrire ce que contiennent les données  
  - représentations graphiques  
  - caractéristiques numériques  
  - les résultats ne sont que sur les résultats que l'on a  
  - objectif: repérez les valeurs atypiques, les valeurs extrêmes, visualiser les tendances  
- Statistique inférentielle  
  - analyses et tests  
  - objectif: prédire, estimer, les comportement d'une population et expliquer les chances d'occurence d'un évènement à partir d'une échantillon aléatoire  
  
### 2.1) Vocabulaire  
- <font color="#ff0000">population</font>: ensemble concerné par une étude statistique  
- <font color="#ff0000">individu</font>: un élément d'une population concerné = observation  
- <font color="#ff0000">échantillon</font>: sous-ensemble de la population sur lequel sont réalisé des tests  
- <font color="#ff0000">variable</font>: information ou caractéristique dont on va recueillir la valeur pour chaque individu d'une population  
- <font color="#ff0000">variable aléatoire</font>: variable qui peut prendre plusieurs valeurs possible pour une experience aléatoire donnée  
- <font color="#ff0000">variable explicative</font>: celle ci permet d'expliquer les valeurs obtenues par une autre variable  
- <font color="#ff0000">variable cible, expliquée</font>: celle que l'on veut expliquer  
  
### 2.2) Types de variables  
  
![500](./image/Drawing%20Types%20de%20variables.excalidraw.svg#)  
```mermaid  
flowchart TB  
    A([types de données]) --> B([quantitatives]) & C([qualitatives])  
    B(["fas:fa-sort-numeric-up-alt quantitatives"]) --> D([continues]) & E([discrètes])  
   C(["fa:fa-font qualitatives"]) --> F([nominales]) & G([ordinales])  
	style A fill:#b425c700,stroke:#ffc04d,stroke-width:2px,color:#f08c00  
	style B fill:#ffffff00,stroke:#171717,stroke-width:1.5px  
	style C fill:#ffffff00,stroke:#171717,stroke-width:1px  
	class D,E,F,G child  
	classDef child fill:#ffffff00, stroke:#171717  
```  
  
### 2.3) Notions de variabilité  
- Quelle que soit sa nature, des fluctuations ou variabilités sont présentes dans un phénomène  
- On peut décrire cette variabilité avec des lois statistiques  
	- exemple: loi normale  
  
### 2.4) La loi normale  
- sous la forme d'une courbe en forme de cloche  
- les valeurs sont continues et symétriques  
- cette courbe est caractérisée par son espérance et son écart-type  
- On peut calculer les probabilités d'une valeur facilement  
  
## 3) La statistique descriptive  
  
### 3.1) Définition  
- permet de décrire la donnée spar des représentations graphiques et des caractéristiques numériques  
- propriétés  
   - caractéristiques de position: moyenne, médiane, mode  
   - de forme: coefficient de symétrie, coef d'aplatissement  
   - de dispersion: variance, écart-type, étendues, quartiles  
- graphiques et tableaux  
- décrire une situation en se basant uniquement sur les résultats des échantillons  
  
### 3.2) Caractéristiques de position  
- Moyenne  
   - Pour une variable quantitative, la moyenne est la valeur uniforme que devrait présenter chaque individu d’une population ou d’un échantillon pour que le total de l’ensemble reste inchangé. La moyenne arithmétique s’obtient en divisant la somme des valeurs par l’effectif : la moyenne de la somme des 10 premiers nombres est 55/10, autrement dit 5,5.  
- Médiane  
   - Si on ordonne une distribution, la médiane  partage cette distribution en deux parties d’effectifs égaux.  
      Ainsi, pour une distribution de salaires, 50 % des salaires se situent sous la médiane et 50 % au-dessus.  
- Mode  
   - En statistique, le mode, ou valeur dominante, est la valeur la plus représentée d'une variable quelconque dans une population donnée.  
- Fréquence  
   - La fréquence d’une valeur donnée, c’est le quotient (la division) de l’effectif de la valeur par l’effectif total. Intuitivement, elle indique la proportion de la présence de la valeur dans la liste.  
- Effectif  
   - L'EFFECTIF d'une valeur est le nombre de données qui ont cette valeur (nombre de fois où cette valeur apparaît). L'EFFECTIF TOTAL est le nombre d'individus de la population étudiée, c'est-à-dire le nombre de données collectées.  
  
### 3.3) Caractéristiques de forme  
- coefficient d'aplattisement  
- coefficient de symétrie  
  
### 3.4) Caractéristiques de dispersion  
- L'étendue  
   - L’étendue d’une série statistique est la différence entre la valeur la plus grande et la valeur la plus petite de cette série.  
- La variance  
   - La variance  est définie comme la moyenne du carré des écarts à la moyenne des valeurs de la distribution.  
   - Le calcul de la variance est nécessaire pour calculer l'écart type.  
- L'écart-type  
   - L'écart-type sert à mesurer la dispersion, ou l'étalement, d'un ensemble de valeurs autour de leur moyenne. Plus l'écart-type est faible, plus la population est homogène.  
- Le quartile  
   - Si on ordonne une distribution de salaires, de revenus, de chiffre d'affaires…, les quartiles sont les valeurs qui partagent cette distribution en quatre parties égales.  
  
### 3.5) Exercice  
- 1. De quelle population s’agit-il ? Il s'agit d'une population de 80 étudiants  
- 2. Quelle est la variable statistique mise en jeu ? C'est une note à un test  
- 3. Cette variable est -elle discrète ou continue ? Discrète  
- 4. Construisez une visualisation adéquate pour représenter les effectifs  
  ![300](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%203.png#)  
- 5. Mettez en évidence le nombre d’étudiants ayant répondu plus de 6 fois correctement  
  ![300](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%204.png#)  
- 6. Quel est le nombre de réponses correctes qui apparaît le plus souvent ? Comment appelle-ton cette valeur ? 7 , c'est le mode  
- 7. Quelle est la moyenne obtenue pour ce test ? 6,475  
- 8. Quel est le nombre de réponses correctes pour lequel 50% des élèves se situent en dessous et 50% en dessus ? Comment appelle-t-on cette valeur ? 7 , c'est la médiane  
- 9. Construisez une boîte à moustache et retrouver les valeurs précédentes.  
  ![300](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%205.png#)  
- 10. Calculer la variance et l’écart type ? variance = 3,949375 écart-type = 1,99984177  
  
## 4) Analyse de plusieurs valeurs  
- Après avoir visualiser les variables une à une , il reste encore à savoir si les variables explicatives entretiennent un lien entre elles, est-ce qu'elles sont corrélées ?  
- rôle de l'analyse bivariée, objectif : relation qui existe entre 2 variable  
  
### 4.1) Les corrélations entre les variables  
- le fait que 2 variables varient simultanément ne certifie pas qu'ils sont corrélés  
- Il faut utiliser le coefficient de corrélation ou de Pearson, indicateur numérique  
- le signe de coefficient indique le sens de la liaison  
   - positif: même sens  
   - négatif: sens opposées  
- la valeur absolue indique l'intensité de la liaison (entre 0 et 1)  
   - proche de 1: liaison forte  
   - proche de 0: liaison faible  
- On peut s'aider de la visualisation en point de nuage pour voir une corrélation, sans en être sûr  
- Si l'on a plusieurs valeurs, on peut calculer la corrélation une à une et les rassembler sous forme d'une <font color="#ff0000">matrice de corrélation</font>.  
  ![400](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%206.png#)  
- Pour le cas de variables qualitatives  
   - On se focalise sur les effectifs, la question est donc de savoir si les effectifs sont reliées.  
   - On utilise un tableau de contingence que l'on calcule avec un test de Khi2  
  
### 4.2) Etapes d'une analyse statistique exhaustive univariée  
- dimension de nos données  
- nom et signification des variables  
- types de variables  
- présence de valeurs manquantes ou nulles  
- caractéristiques de forme/position/distribution avec les visualisation adéquates  
  
### 4.3) Exercice 2  
- [EXO2_clients_marketing.xlsx](./image/EXO2_clients_marketing.xlsx.md#)  
  
## 5) Test du Khi2  
- Quand l'on travaille avec des variables qualitatives, on ne peut plus calculer le coefficient de corrélation  
- On utiliser donc le test du Khi2, et un tableau de contingence  
  
- On pose 2 hypothèses:  
	- H0: les deux variables sont indépendantes  
	- H1: les variables sont dépendantes  
- l'hypuyhèse nulle est considéré comme vrai tout au long du test, on le rejette si l'on a suffisamment de preuve  
  
- On commence par calculer les totaux de chaque lignes et colonnes;  
- ![800](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%207.png#)  
- Si les variables sont indépendantes, on devrait retrouver les même proportion des lignes et des colonnes entre elles  
- Ensuite on calcule combien on devrait en avoir si cela était respecté  
- ![800](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%208.png#)  
- ![800](Revision%20des%20cours%20data%20-%20image%20-%201.png#)  
- On compare ensuite les fréquences théoriques et comparées  
- On calcule ensuite le lien avec le Khi2, qui calcule l'écart global entre les fréquences observées et celles attendues  
- ![600](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%2010.png#)  
- Les loi du Khi2 possède 2 paramètres:  
	- degré de liberté = nombre de ligne - 1 * nombre de colonne - 1  
	- seuil de significativité: probabilité du risque que l'on est prêt à assumer en rejetant l'hypothqèse nulle = ɑ  
		- souvent fixé à 5%  
- On compare ensuite la statistique Khi2 à la critique de distribution du Khi2 de référence , avec la table de référence  
	- Si <font color="#ff0000">Khi2</font> > <font color="#ff0000">Khi2</font> <font color="#ff0000">critique</font> : <font color="#ff0000">on rejette l'hypthèse H0</font>  
	- Si <font color="#ff0000">Khi2</font> < <font color="#ff0000">Khi2</font> <font color="#ff0000">critique</font> : <font color="#ff0000">on accepte l'hypothèse H1</font>  
  
  
- Template: [Template Test Khi2.xlsx](./image/Template%20Test%20Khi2.xlsx.md#)  
  
## 6) Exercice 4  
[EXO4_donnees_bancaires.xlsx](./image/EXO4_donnees_bancaires.xlsx.md#)  
[exercice_stat.pdf](./image/exercice_stat.pdf#)  
  
## 7) Exercice méthode Kmeans et CAH  
- [x] a rendre au format word + rajouter les autres travail , sur le campus CEFIM 📅 2023-06-01 ✅ 2023-06-04  
mail barbara: barbarafraenckel@gmail.com  
  
%%  
parent:: [Cefim note principale](../CEFIM%20note%20principale.md#)  
image:: [image - 🎯 Cours Statistiques  - 1.jpg](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%201.jpg#), [image - 🎯 Cours Statistiques  - 2.png](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%202.png#), [image - 🎯 Cours Statistiques  - 3.png](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%203.png#), [image - 🎯 Cours Statistiques  - 4.png](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%204.png#), [image - 🎯 Cours Statistiques  - 5.png](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%205.png#), [image - 🎯 Cours Statistiques  - 6.png](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%206.png#), [image - 🎯 Cours Statistiques  - 7.png](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%207.png#), [image - 🎯 Cours Statistiques  - 8.png](./image/image%20-%20%F0%9F%8E%AF%20Cours%20Statistiques%20%20-%208.png#), [Drawing Types de variables.excalidraw](../Drawing%20Types%20de%20variables.excalidraw.md#), [Revision des cours data - image - 1.png](Revision%20des%20cours%20data%20-%20image%20-%201.png#)  
exemple:: [EXO2_clients_marketing.xlsx](./image/EXO2_clients_marketing.xlsx.md#), [EXO4_donnees_bancaires.xlsx](./image/EXO4_donnees_bancaires.xlsx.md#), [exercice_stat.pdf](./image/exercice_stat.pdf#)  
%%  
  
---  
[Cefim note principale](../CEFIM%20note%20principale.md#)  
  
