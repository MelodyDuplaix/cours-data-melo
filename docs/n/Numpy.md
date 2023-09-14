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
  
[Cours python](./Cours%20python.md#)  
***  
  
  
## 2) Numpy  
  
### 2.1) Configuration des données  
  
#### 2.1.1) Convertir une liste en tableau ndarray Numpy  
```python  
import numpy as np  
ma_liste = [1, 2, 3, 4, 5]  
nom_tableau = np.array(ma_liste)  
print(nom_tableau)  
```  
  
### 2.2) Audit des données  
  
#### 2.2.1) Connaître le nombre de dimension d'un tableau   
```python  
nom_tableau.ndim  
```  
  
#### 2.2.2) Connaître le nombre colonnes et lignes  
```python  
nom_tableau.shape  
```  
  
#### 2.2.3) Connaître le type de données du tableau  
```python  
nom_tableau.dtype  
```  
  
#### 2.2.4) Connaître le nombre d'éléments dans le tableau  
```python  
nom_tableau.size  
```  
  
### 2.3) Créer un tableau  
#### 2.3.1) Créer un tableau de nombre au hasard  
```python  
nom_tableau = np.random.randn(6,6)  
print(nom_tableau)  
```  
pour des nombres entiers :  
```python  
nom_tableau = np.random.randint(0, 10 ,[9, 9])  
print(nom_tableau)  
```  
  
#### 2.3.2) Créer un suite de nombre  
```python  
np.arange(1, 10, 2)  
```  
  
#### 2.3.3) Créer une suite de nombre répartie  
```python  
np.linspace(0, 20, 3)  
```  
  
>[!WARNING] Important  
> <span style="background:#fff88f">Créer une copie de la matrice originale avant de faire n'importe quelle modification</span>  
  
#### Créer un tableau de nombres uniques  
```python  
mon_tableau_de_uns = np.ones((2,4))  
print(mon_tableau_de_uns)  
```  
  
  
### 2.4) Slicing  
  
```python  
nb_entiers = np.random.randint(0, 10,[9,9])  
```  
  
#### 2.4.1) Slicing simple  
```python  
nb_entiers[0:3]  
```  
  
#### 2.4.2) Slicing avec pas  
```python  
nb_entiers[0][0::2]  
```  
prend dans la première ligne, les valeurs de 0 à la fin, toutes les deux valeurs  
  
#### 2.4.3) Slicing pour prendre la première colonne  
```python  
nb_entiers[:,0 ]  
```  
- []  
- : plage - nombre debut : nombre fin  
- , élément séparateur entre  les lignes et les colonnes  
  
### 2.5) Le boolean indexing  
Une matrice booléenne permet de parcourir tous les éléments et de renvoyer un booléen selon une condition  
![600](%F0%9F%93%91%20Travail%20des%20donn%C3%A9es%20sur%20python%20fourre-tout-1.png#)  
  
- on détecte les valeurs qui répondent à la contrainte => True  
- on remplace ces valeurs par une autre valeur  
#### 2.5.1) Remplacer des valeurs selon une condition  
```python  
nb_entiers[nb_entiers > 4] = 10  
print(nb_entiers)  
```  
  
#### Assembler des tableaux  
```python  
tableau_1 = np.arange(0,10)  
print(tableau_1)  
tableau_2 = np.arange(10,20)  
print(tableau_2)  
```  
  
##### De facon verticale  
```python  
tableau_assembler_vertical = np.vstack((tableau_1, tableau_2))  
print(tableau_assembler_vertical)  
```  
  
##### De façon horizontal  
```python  
tableau_assembler_horizontal = np.hstack((tableau_1, tableau_2))  
print(tableau_assembler_horizontal)  
```  
  
##### Par l'index  
```python  
tableau_assembler_index = np.dstack((tableau_1, tableau_2))  
print(tableau_assembler_index)  
```  
  
  
  
### 2.6) Calculs arithmétiques et stats  
  
```python  
nom_tableau = np.random.randint(0,10,[9,9])  
print(nom_tableau)  
```  
  
  
#### 2.6.1) Somme des valeurs des colonnes  
```python  
nom_tableau.sum(axis=0)  
```  
  
#### 2.6.2) Sommes des valeurs des lignes  
```python  
nom_tableau.sum(axis=1)  
```  
  
#### 2.6.3) Valeurs maximum et minimum des colonnes  
```python  
print(nom_tableau.max(axis=0))  
print(nom_tableau.min(axis=0))  
```  
  
#### Produit des valeurs  
```python  
nom_tableau.prod()  
```  
  
#### 2.6.4) Index des valeurs maximum des colonnes  
```python  
nom_tableau.argmax(axis=0)  
```  
  
#### 2.6.5) Trier les valeurs  
```python  
np.sort(nom_tableau, kind='quicksort')  
```  
  
#### Calculer la moyenne des valeurs  
```python  
np.mean(nom_tableau)  
```  
  
#### 2.6.6) Calculer la médiane des valeurs  
```python  
np.median(nom_tableau, axis=1)  
```  
  
#### Calcul de la variance  
```python  
nom_tableau.var()  
```  
  
#### 2.6.7) Obtenir les valeurs uniques  
```python  
np.unique(nom_tableau)  
```  
avec l'effectif des valeurs:  
```python  
np.unique(nom_tableau, return_counts=True)  
```  
  
#### 2.6.8) Manipuler des valeurs manquantes  
  
##### 2.6.8.1) Créer des valeurs manquantes  
```python  
nom_tableau[ligne,colonne] = np.nan  
```  
  
##### 2.6.8.2) Obtenir le pourcentage de valeurs manquantes  
```python  
np.nanmean(nom_tableau)  
```  
  
##### 2.6.8.3) Obtenir le nombre de valeurs manquantes  
```python  
np.isnan(nom_tableau).sum()  
```  
