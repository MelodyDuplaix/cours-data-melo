---
number headings: first-level 2, max 6, start-at 1, 1.1), auto
cssclasses:
  - banner-image
aliases:
  - python
nature: cours
tags:
  - data
  - python
  - formation
  - cours
share: true
---
![[image -  Cours python - banniere.png|banner]]

[[Cefim note principale]]

---
- [[Cours python#1) Premières étapes lorsque l'on souhaite travailler sur des données avec Python|1) Premières étapes lorsque l'on souhaite travailler sur des données avec Python]]
- [[Cours python#3) Pandas|3) Pandas]]
- [[Cours python#4) Créer un échantillon de données en csv depuis un csv|4) Créer un échantillon de données en csv depuis un csv]]
	- [[Cours python#4.1) Créer une liste de nombre aléatoire|4.1) Créer une liste de nombre aléatoire]]
	- [[Cours python#4.2) Créer l'échantillon|4.2) Créer l'échantillon]]
	- [[Cours python#4.3) Exporter l'échantillon dans un fichier csv|4.3) Exporter l'échantillon dans un fichier csv]]
	- [[Cours python#4.4) Autre facon de faire|4.4) Autre facon de faire]]
- [[Cours python#6) Seaborn|6) Seaborn]]
- [[Cours python#7) Bases de données et SQLite|7) Bases de données et SQLite]]
- [[Cours python#8) Exercices autres possibles|8) Exercices autres possibles]]
- [[Cours python#9) Projet Python|9) Projet Python]]
- [[#10) Streamlit|10) Streamlit]]
- [[#11) Bonnes pratiques]]
	- [[#11.1) Créer des fonctions]]
	- [[#11.2) Gestion de projet]]
		- [[#11.2.1) User-stories]]



## 1) Premières étapes lorsque l'on souhaite travailler sur des données avec Python
- Créer un environnement virtuel (pour pouvoir travailler sur plusieurs projet avec des versions différentes, sur un même poste)
>[!WARNING] Ne pas changer les versions de bibliothèque dans un environnement virtuel, le faire avant dans un nouvel environnement d'abord, pour vérifier que le code fonctionne toujours.
- créer le dossier de travail
- définir un plan de classement
- collecter/créer des fichiers
- créer un programme python
	- expliquer le programme avec du markdown
	- programmer en python
		- définir la nomenclature des variables

Sur jupyter, tabulation pour afficher toutes les méthodes après avoir écris [méthode].
enumerate() permet d'énumérer les éléments d'une liste, ou un élément précis d'une liste
dir([bibliothèque]): affiche touts les méthodes que l'on peux utiliser

Pour accéder à un environnement virtuel sur VSCode: .\.venv\Scripts\activate

Il est préférable de travailler sur une copie du tableau avec:
```python
import copy
new_tableau = copy.deepcopy(matrice_nombres_entiers)
```
## 2) Numpy
[[Numpy]]

## 3) Pandas
[[Pandas]]

## 4) Créer un échantillon de données en csv depuis un csv

### 4.1) Créer une liste de nombre aléatoire
```python fold title:"liste de nombre"
listeNombreHasard = []

while len(listeNombreHasard) < (df.shape[0]*0.2):
    nombreHasard = randint(1,540)
    # print(nombreHasard)
    if nombreHasard in listeNombreHasard :
        print('Nb en doublon.')
    else :
        listeNombreHasard.append(nombreHasard)

print(listeNombreHasard)
```

### 4.2) Créer l'échantillon
```python
echantillon = []
with open("data/RNCP-Nettoyage.csv", encoding="utf-8") as fichier:
    contenu = list(csv.reader(fichier))
    
    for nombre in listeNombreHasard:
        print(contenu[nombre])
        echantillon.append(contenu[nombre])
```

### 4.3) Exporter l'échantillon dans un fichier csv
```python
nom_fichier_sortie = "echantillon.csv"
with open(nom_fichier_sortie, mode="w", newline="", encoding="utf-8") as fichier_sortie:
    ecrivain_csv = csv.writer(fichier_sortie)
    for ligne in echantillon:
        ecrivain_csv.writerow(ligne)
```

### 4.4) Autre facon de faire
```python
# Créer une liste au hasard
nb_echantillons=round(df.shape[0] * 0.25, 0)
print(f"Nous devons tirer {nb_echantillons} lignes au hasard")

liste_tirage =[]
while len(liste_tirage) < nb_echantillons:
    nombre_hasard = np.random.randint(0,df.shape[0]+1)
    if nombre_hasard not in liste_tirage:
        liste_tirage.append(nombre_hasard)
        
# Créer un nouveau DF contenant cette sélection
colonnes_df = list(df.columns.values)
df_selection = pd.DataFrame(columns = colonnes_df) # df vide avec les mêmes intitulés de colonne
for index,ligne in df.iterrows():
    if index in liste_tirage:
        df_selection = pd.concat([df_selection, ligne.to_frame().T])#, ignore_index = True)

        
df_selection.to_csv("Echantillon.csv")

df_selection
```
## 5) Plotly
[[Plotly]]

voir aussi [[plotly_cheat_sheet.pdf]] pour la réalisation
et [[plotly_cours.ipynb]]
aide avec [Online Graph Maker · Plotly Chart Studio](https://chart-studio.plotly.com/create/#/)

## 6) Seaborn
[[Seaborn]]

## 7) Bases de données et SQLite
[[📇 Cours python - Bases de données]]

## 8) Exercices autres possibles
Sphinx pour la documentation: [google doc](https://docs.google.com/document/d/1kxkZ7fKTJ2UUiYAPIJf0XL_aVBrlSY47JP_BIDe3T8c/edit?usp=sharing)
MongoDB: [google slide](https://docs.google.com/presentation/d/1caoP2hgen8Bl4DlIxz20TuUHAKz4i66BjJCPdtbJrxM/edit?usp=sharing)

## 9) Projet Python
[[🐍 Projet python]]

## 10) Streamlit
[[Projet Streamlit]]

## 11) Autres projets

[[Petits projets python pour apprendre]]

## 12) Bonnes pratiques

### 12.1) Créer des fonctions

avantage: 
- ne pas avoir à stopper/arrêter le service pour faires des modification
- les réutiliser facilement dans d'autres codes 

> [!tip] Important
> - D'abord écrire le code en entier sans fonctions
> - Puis écrire toutes les fonctions juste avec pass pour avoir le squelette
> - Vérifier les choix de fonction avec équipe si nécessaire
> - Finir par écrire les instructions des fonctions
> - nommer les variables des fonctions avec f_ en premier
> - ne pas oublier les docstrings
> 	- exemple de forme:
> ````
> """
> Nom :
> Paramètres :
> Traitement :
> Retour :
> """
> ````


### 12.2) Créer une bibliothèque de fonction
Dans un dossier "bibliotheque" par exemple, on crée un fichier python, souvent lib.py, on y place toutes nos fonctions, et les imports de bibliothèques nécessaires pour les fonctions.
Puis pour importer nos fonctions, on ajoute cet import dans le fichier de code principal : ` from bibliotheque.lib import  * ` 
Le dossier \_pycahcache_ est automatiquement crée.

### 12.3) Gestion de projet

#### 12.3.1) User-stories

Origine des méthodes Agiles / XP(eXtrem Programming)
Idée: si une fonctionnalité doit être intégré , c'est qu'elle est réellement utilisée

**Syntaxe** : (Gerkhin syntax, cucumber)

**En tant que**... rôle de l'acteur, exemples: 
- *utilisateur*
- *administrateur*
- *commercial*
- *directeur*

**Je veux**... fonctionnalité/accès à la fonctionnalité, exemples: 
- *appuyer sur un bouton pour imprimer une page au format pdf*
- *afficher le nombre d'associations dans le 37 en tapant dans un champs de recherche un code postal*
- *afficher le nombre d'associations dans le 37 dès que la page se charge*
- *voir un graphique représentant le nombre d'associations dissoutes en choisissant avec un calendrier une date de début et une date de fin*

**Afin de**.. Pourquoi l'utilisateur a besoin de cette information/service, exemples: 
- *d'évaluer si il y a beaucoup d'associations ou pas*
- *pouvoir compléter visuellement le rapport mensuel*



%%
parent:: [[Cefim note principale]], [[Cours Data]]
enfant:: [[Numpy]], [[Pandas]], [[Plotly]], [[plotly_cheat_sheet.pdf]], ,[[Seaborn]], [[📇 Cours python - Bases de données]], [[🐍 Projet python]]
exemple:: [[plotly_cours.ipynb]]
%%