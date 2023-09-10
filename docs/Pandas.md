---  
aliases: []  
nature: cours  
tags:  
  - cours  
  - formation  
  - python  
  - data  
cssclasses:  
  - banner-image  
share: true  
---  
  
[📑 Cours python](./%F0%9F%93%91%20Cours%20python.md#)  
***  
> [!summary]-  
> ```toc  
> ```   
  
## 1) Pandas  
  
```python  
import pandas as pd  
```  
  
### 1.1) Identifier la version d'une bibliothèque  
```python  
pd.__version__  
```  
  
### 1.2) Tableau de pandas  
<span style="background:rgba(240, 107, 5, 0.2)">une array Numpy est une serie pandas</span>  
une indexation est automatiquement crée  
```python  
vecteur_numpy = np.array([1,2,3])  
serie_pandas = pd.Series(data=vecteur_numpy)  
print(serie_pandas)  
```  
  
`nom_series.values` redonne les valeurs sous forme d'une array Numpy  
  
#### 1.2.1) Créer un tableau pandas avec des index spécifiques  
```python  
mon_index = ["a","b","c"]  
mes_valeurs = ["Numpy", "Pandas","Plotly"]  
  
ma_serie_pandas = pd.Series(index=mon_index, data=mes_valeurs)  
print(ma_serie_pandas)  
```  
  
#### 1.2.2) Afficher une valeur selon un index  
```python  
ma_serie_pandas["b"]  
```  
  
### 1.3) Utilisation d'un dataframe  
  
#### 1.3.1) Les bases d'un dataframe  
  
##### 1.3.1.1) Création d'un dataframe  
a partir d'un dictionnaire:   
```python  
mon_dictionnaire = {'Note_Abigael' : range(0,5),  
                    'Note_Yolande' : range(11,16)}  
mon_premier_dataframe = pd.DataFrame(mon_dictionnaire)  
print(mon_premier_dataframe)  
```  
  
##### 1.3.1.2) Afficher certaines colonnes  
```python  
mon_premier_dataframe["Note_Abigael","Note_Yolande"](%22Note_Abigael%22,%22Note_Yolande%22.md#)  
```  
avec seulement certaines lignes:  
```python  
mon_premier_dataframe["Note_Abigael","Note_Yolande"](%22Note_Abigael%22,%22Note_Yolande%22.md#)[:2]  
```  
  
  
##### 1.3.1.3) Renommer des index  
au moment de créer le dataframe:  
```python  
mon_premier_dataframe = pd.DataFrame(mon_dictionnaire, index = ["Math","Physique","Sport","Français","Anglais"])  
print(mon_premier_dataframe)  
```  
  
ce qui permet d'afficher une valeur selon:  
`nom_dataframe["nom_colonne"]["index"]`  
  
### 1.4) Manipulations sur les dataframes  
  
##### 1.4.1.1) Rajouter une colonne  
```python  
mon_premier_dataframe["Note_Hector"] = range(21,26)  
print(mon_premier_dataframe)  
```  
liste_valeurs peut être un range()  
  
  
##### 1.4.1.2) Afficher les valeurs selon une condition  
```python  
print(mon_premier_dataframe[mon_premier_dataframe < 15])  
```  
  
  
##### 1.4.1.3) Changer les valeurs d'une colonne  
avec une liste:  
```python  
mon_premier_dataframe["Note_Hector"] = range(9, 14)  
print(mon_premier_dataframe)  
```  
avec une chaine de caractère splité:  
```python  
mon_premier_dataframe["Note_Abigael"] = "7 8 12 14 9".split()  
print(mon_premier_dataframe)  
```  
  
##### 1.4.1.4) Enlever une colonne directement sur le tableau  
```python  
del nom_dataframe["nom_colonne"]  
```  
ou  
```python  
nom_dataframe = nom_dataframe.drop('nom_colonne', axis=1)  
```  
ou  
```python  
mon_premier_dataframe.drop("Note_Yolande", axis=1, inplace=True)  
print(mon_premier_dataframe)  
```  
  
##### 1.4.1.5) Convertir un type object en type datetime  
```python  
df['date_fin_certification']= pd.to_datetime(df['date_fin_certification'])  
```  
  
#### 1.4.2) Bases des méthodes sur les dataframe  
  
##### 1.4.2.1) Moyenne d'une série  
```python  
mon_premier_dataframe["Note_Abigael"].mean()  
```  
  
##### 1.4.2.2) Trier les valeurs en descendantes  
```python  
mon_premier_dataframe["Note_Abigael"].sort_values(ascending=False)  
```  
ou  
```python  
mon_premier_dataframe.sort_values("Note_Abigael", ascending=False)  
```  
  
##### 1.4.2.3) Remplacer les index avec les valeurs d'une colonne  
```python  
  
nom_dataframe.set_index("nom_colonne", inplace=True)  
```  
  
##### 1.4.2.4) Programmer un méthode que l'on applique sur des lignes d'une dataframe  
```python  
# Programmer un fonction qui additione chaque valeurs d'une ligne  
def somme(ligne):  
    return ligne.sum()  
  
mon_premier_dataframe["note_finale_complexe"] = mon_premier_dataframe.apply(somme, axis=1)  
mon_premier_dataframe  
```  
créé une colonne additionnant les valeurs pour chaque ligne  
  
On peut aussi utiliser une lambda fonction:  
```python  
dataframe_exercice["note_finale_complexe"] = dataframe_exercice.apply(lambda valeur:valeur.sum(), axis=1)  
```  
  
##### 1.4.2.5) Afficher des lignes selon plusieurs conditions  
On ne peut pas utiliser des and, or et not dans les conditions de dataframe, il faut utiliser des conditions booléennes & (and) , | (ou inclusif) ou ^ (ou exclusif)  
exemple:  
```python  
dataframe_exercice[(dataframe_exercice["note_math"] > 12) & (dataframe_exercice["note_francais"] > 12)]  
```  
  
##### 1.4.2.6) Conditions booléennes  
> [!important]   
> -     & : ET - Toutes les conditions sont vraies  
>-    | : OU inclusif - Au moins une condition est vraie, voir toutes sont vraies  
>-     ^ : OU exclusif - Au moins est une condition est vraie, mais pas toutes ensemble   
  
##### 1.4.2.7) Afficher le nombre d'occurences d'une valeur  
```python  
nom_dataframe["nom_colonne"].value_counts().get(valeur)  
```  
  
  
#### 1.4.3) Première lecture des données d'un fichier  
  
##### 1.4.3.1) Afficher les infos globales   
```python  
nom_dataframe.info()  
```  
##### 1.4.3.2) Affiches le nombre de colonnes et de lignes  
```python  
nom_dataframe.shape  
```  
##### 1.4.3.3) Afficher l'ordre des index  
```python  
nom_dataframe.index  
```  
##### 1.4.3.4) Afficher le type de données de chaque colonnes  
```python  
nom_dataframe.dtype  
```  
##### 1.4.3.5) Afficher l'intitulé des colonnes   
```python  
nom_dataframe.columns  
```  
pour n'obtenir que les valeurs: on rajoute .value  
##### 1.4.3.6) Afficher une colonne spécifique  
```python  
nom_dataframe["nom_colonne"]  
```  
ou  
```python  
nom_dataframe.nom_colonne  
```  
pour plusieurs colonnes:  
```python  
nom_dataframe["nom_colonne"](%22nom_colonne%22.md#)  
```  
##### 1.4.3.7) Afficher le nombre d'occurence des valeurs  
```python  
nom_dataframe['nom_colonne'].value_count()  
```  
##### 1.4.3.8) Afficher des valeurs spécifiques avec iloc  
pour afficher une ligne:    
```python  
nom_dataframe.iloc[index_ligne]  
```  
pour afficher une valeur:  
```python  
nom_dataframe.iloc[index_ligne, numéro_colonne]  
```  
ou  
```python  
df.loc[df["titre"] == "valeur"]  
```  
  
##### 1.4.3.9) Afficher valeurs selon des critères  
avec isin:  
```python  
df.loc[df['position'].isin(["A","D"])]  
```  
avec query:  
```python  
df.query("position == 'A'")  
```  
Pour identifier plusieurs valeurs possibles  
```python  
df.query("position in ('A', 'S')")  
# ou  
requete = ["A", "S"]  
df.query("position in @requete")  
```  
pour des critères basés sur des chaînes de caractères:  
```python  
df["titre"].str.startswith("SO")  
```  
ou  
```python  
df["titre"].str.contains("SO")  
```  
Il est possible d'utiliser des chaînes regex  
```python  
df["titre"].str.contains("^SO|^AM", regex=True)  
```  
  
## 2) Nettoyer les données  
  
### 2.1) Identifier les valeurs nulles  
```python  
df["titre"].isna().sum()  
print(f"Il y a {valeurs_nulles} valeurs non-renseignées dans la colonne.")  
```  
  
### 2.2) Supprimer les colonnes avec plus de 50% de valeurs nulles  
```python  
pourcentage_de_suppression = 50  
  
for colonne in df.columns:  
    valeurs_nulles_par_colonne = df[colonne].isna().sum()  
    if valeurs_nulles_par_colonne > 0 :  
        pourcentage_valeur_vide = valeurs_nulles_par_colonne/df.shape[0]*100  
        print(f"Il y a {valeurs_nulles_par_colonne} dans la colonne {colonne}.")  
        print(f"Cela correspond à =============> {pourcentage_valeur_vide:.2f}%.")  
        if pourcentage_valeur_vide > pourcentage_de_suppression :  
            df.drop(columns=colonne, inplace=True)  
  
print(df)  
```  
  
### 2.3) Remplacer les valeurs manquantes par une autre valeur  
```python  
df['observation'].fillna("None", inplace=True)  
df["observation"]  
```  
  
### 2.4) Convertir des types de données  
convertir une colonne:  
```python  
df["titre"].astype(type)  
```  
  
pour plusieurs colonnes en même temps:  
```python  
df.astype({"colonne1": type, "colonne2":type})  
```  
  
pour les dates:  
```python  
to_datetime(dataframe['titre'], error='coerce')  
```  
  
### 2.5) Modifier des valeurs spécifiques  
```python  
df.loc[df['titre'] == 'valeur', 'titre'] = 'nouvelle_valeur'  
```  
pour plusieurs variables:  
```python  
df.loc[(df['date_publi'] == '0001-01-01') | (df['objet'] == 'O') , ['date_publi', 'objet']] = ['0', 'Neant']  
```  
  
## 3) Manipulations avancées sur les DataFrames  
  
### 3.1) Parcourir les lignes des données  
```python  
df.iterrows()  
```  
Cette méthode renvois 2 arguments: l'index et l'enregistrement de la ligne  
Elle est généralement encapsulé dans une boucle for  
  
### 3.2) Grouper des valeurs pour des calculs avancé   
```python  
df.groupby["colonne1", "colonne2"]  
```  
à utiliser avec .mean(), .sum(), .count()  ou .sort_values("colonne", ascending=False)  
  
## 4) Convertir un fichier ipynb en diapo  
On peut convertir une cellule en cellule de diapo  
- diapo: navigation horizontale  
- sous-diapo: navigation verticale en dessous de chaque diapo  
- extrait: s'affiche juste en dessous de la diapo juste avant  
  
On peut ensuite les convertir en slide avec "reveal js slides" dans Download as, dans fichier  
  
## 5) Créer et executer un fichier python en ligne de commande  
créer un fichier:  
```  
copy con instruction nom_fichier.py  
```  
  
executer un fichier:  
```  
python nom_fichier.py  
```  
  
#### 5.1.1) Comparer des dates et nombre de jours  
```python  
(datetime.date.today()-df["date_creation_JO"][1].date()).days <= 180  
```  
  
