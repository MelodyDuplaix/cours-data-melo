---  
number headings: first-level 2, max 6, start-at 1, 1.1), auto  
aliases:  
  - streamlit  
nature: cours  
tags:  
  - cours  
share: true  
---  
  
> [!sommaire|outlined]-   
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
    at eval (plugin:obsidian-mkdocs-publisher:2:871)</pre>  
  
## 1) Explication du projet  
  
> [!info]- [Fiche Projet Streamlit](https://docs.google.com/document/d/13sPOAO5Wy9ln6N1wxK6xBytp88l5QO1j-emM3RTN6V0/edit)  
> <iframe src='https://docs.google.com/document/d/13sPOAO5Wy9ln6N1wxK6xBytp88l5QO1j-emM3RTN6V0/edit' allow='fullscreen' allowfullscreen='' style='height: 100%; width: 100%; aspect-ratio: 1/1;'></iframe>  
  
[lien du dossier partagé](https://drive.google.com/drive/u/0/folders/1tXTroYIkZ2Uj0DgUIpj-hCEv9enJHXRQ)  
  
> [!info]- [Document de travail](https://docs.google.com/document/d/1rAKMMQIoGxYt144rZRtNZNDUcj0u2gVJidd2O-J2xZY/edit)  
> <iframe src='https://docs.google.com/document/d/1rAKMMQIoGxYt144rZRtNZNDUcj0u2gVJidd2O-J2xZY/edit' allow='fullscreen' allowfullscreen='' style='height: 100%; width: 100%; aspect-ratio: 1/1;'></iframe>  
  
> [!info]- [Matrice RACI](https://docs.google.com/spreadsheets/d/1djTlcbTI7zHcHMqN_YDB4gWvGhkTDM9okXPorAf6AHQ/edit#gid=0)  
> <iframe src='https://docs.google.com/spreadsheets/d/1djTlcbTI7zHcHMqN_YDB4gWvGhkTDM9okXPorAf6AHQ/edit#gid=0' allow='fullscreen' allowfullscreen='' style='height: 100%; width: 100%; aspect-ratio: 1/1;'>/</iframe>  
  
[Diagramme d'activité des algorithmes](https://app.diagrams.net/#G1Hxjhkzcq-aXdlMnRjHgt8ihwiPje2UQ3)  
  
![500](../image/Projet%20Streamlit%202023-08-29%20maquette.excalidraw.svg#)  
## 2) Composition d'une appli streamlit  
  
> [!info]- [cheatsheet streamlit](https://cheat-sheet.streamlit.app/)  
> <iframe src="https://cheat-sheet.streamlit.app/" allow="fullscreen" allowfullscreen="" style="height: 100%; width: 100%; aspect-ratio: 1/1;"></iframe>  
### 2.1) Titre  
  
#### 2.1.1) Création d'un titre  
  
```python  
st.title("")  
```  
  
On peut modifier le style avec du markdown, et des emojis via ces codes: https://share.streamlit.io/streamlit/emoji-shortcodes  
#### 2.1.2) Afficher un élément  
équivalent du print  
  
```python  
st.write()  
```  
  
#### 2.1.3) Rajouter une image   
avec la méthode `Image` de la bibliothèque `PIL`  
```python  
logo = Image.open("chemin image")  
st.image(logo)  
```  
  
pour réduire une image:  
```python  
logo_reduit = logo.resize([largeur,longueur])  
```  
  
#### 2.1.4) Faire des colonnes  
```python  
colonne1, colonne2 = st.columns((2))  
with colonne1  
	contenu  
with colonne2  
	contenu  
```  
  
#### 2.1.5) Pour modifier favicon ,nom d'onglet et liens du menu  
```python  
st.set_page_config(  
    page_title="Analyse associations",  
    page_icon="📊",  
    menu_items={  
        "Get Help": "https://www.cefim.eu/",  
        "About" : "https://www.linkedin.com/in/melody-duplaix-391672265"  
    }  
)  
```  
  
#### 2.1.6) Afficher un chargeur de fichier   
```python  
fichier_charge = st.file_uploader("Choisissez un fichier csv", type=["csv"])  
```  
  
et l'utiliser:  
```python  
fichier_charge = st.file_uploader("Choisissez un fichier csv", type=["csv"])  
  
if fichier_charge :  
    dataset = pd.read_csv(fichier_charge,encoding="latin",sep=";")  
    st.write(dataset["siteweb"].unique())  
```  
  
exploiter le nom du fichier:  
```python  
    st.write("Le fichier chargé est : ", fichier_charge.name)  
```  
#### 2.1.7) Afficher un tableau  
```python  
dataset = pd.read_csv("data/rna_waldec_20230801_dpt_37.csv",encoding="latin",sep=";")  
st.write(dataset)  
```  
  
#### 2.1.8) Utiliser streamlit en utilisant des fonctions  
```python  
# Import des bibliothèques  
import streamlit as st  
from PIL import Image  
import pandas as pd  
import re  
  
# Définitions des fonctions  
def charger_le_fichier():  
    """  
    Nom : charger_le_fichier  
    Paramètres : 0  
    Traitement : charger un fichier au format csv grâce à file_uploader  
    Retour : retourne le fichier csv dans la variable fichier_charge  
    """  
    fichier_charge = st.file_uploader("Choisissez un fichier csv", type=["csv"])  
    return(fichier_charge)  
  
def creer_le_jeu_de_donnes(f_fichier_donnee):  
    """  
    Nom : creer_le_jeu_de_donnes  
    Paramètres : 1 - Type : chaine de caractère  
    Traitement : charger un dataset à partir d'un fichier csv  
    Retour : retourne le dataset dans la variable dataset  
    """  
    dataset = pd.read_csv(f_fichier_donnee,encoding="latin", sep=";", decimal=",", thousands=" ")  
    return(dataset)  
  
def rechercher_par_code_postal(f_dataset):  
    pattern = re.compile(r'\d{5}')  
    text_input = st.text_input("Taper le code postal :", placeholder="Code Postal", max_chars=5, help="Veuillez entrer le code postal pour filtrer les associations dans ce code postal.")  
    if text_input and not pattern.search(text_input):  
        st.write("Ce code postal n'est pas valide.")  
          
    f_dataset["adrs_codepostal"] = f_dataset["adrs_codepostal"].apply(str)  
    if text_input and pattern.search(text_input):  
        st.write("Liste des associations du : " + text_input)  
        dataset_codepostal = f_dataset[f_dataset["adrs_codepostal"]==text_input]  
        return(dataset_codepostal)  
  
  
# config de pages  
st.set_page_config(  
    page_title="Analyse associations",  
    page_icon="📊",  
    menu_items={  
        "Get Help": "https://www.cefim.eu/",  
        "About" : "https://www.linkedin.com/in/melody-duplaix-391672265"  
    }  
)  
  
# titre, contexte et logos  
contexte = "Cette application a pour objectif d'analyser les associations au sein des départements 37 et 45."  
colonne_logo, colonne_titre = st.columns([1,5])  
with colonne_logo:  
    logo = Image.open("images/photoprofillinkedIn.excalidraw.png")  
    logo_reduit = logo.resize([60,40])  
    st.image(logo_reduit)  
with colonne_titre:  
    st.title(":red[Application d'analyse des associations du 37 et du 45] :bar_chart:")  
st.write(contexte)  
  
# Code principal  
fichier_charge = charger_le_fichier()  
if fichier_charge:  
    st.write(f"Vous venez de charger le fichier : {fichier_charge.name}")  
  
dataset_charge = creer_le_jeu_de_donnes(fichier_charge)  
if fichier_charge:  
    st.write(dataset_charge)  
  
st.write(rechercher_par_code_postal(dataset_charge))  
```  
  
> [!example]- Exemple autre possibilité par Jean Lou  
> ```python  
>   
> # Autre possibilités  
> # import streamlit as st  
> # from PIL import Image   
> # import pandas as pd  
>   
> # st.set_page_config(  
> #     page_title="AssoApp",  
> #     page_icon="🧊",  
> #     menu_items={  
> #         'Get Help': 'https://www.cefim.eu',  
> #         'About' : 'https://campus.cefim.eu'}  
> #         )  
>   
> # contexte = "Cette application a pour objectifs ......"  
>   
>   
> # st.title("Application d'analyse des associations du 37 	:sparkles:")  
>   
> # st.write(contexte)  
>   
> # fichier_charge = st.file_uploader("Choisissez un fichier csv", type=["csv","xls","xlsx"])  
>   
> # if fichier_charge:  
> #     dataset = pd.read_csv(fichier_charge,   
> #                       encoding="latin", sep=";")  
> #     st.write(f"Vous venez de charger le fichier : {fichier_charge.name}.")  
> #     # st.write(fichier_charge)  
> #     dataset['adrs_codepostal'] = dataset['adrs_codepostal'].apply(str)  
> #     recherche_code_postal = st.text_input("Tapez un code postal 👇",   
> #                                       max_chars=5,  
> #                                       help="Tapez un code postal commençant par 37",   
> #                                       placeholder="Code postal en 37",  
> #                                       value="")  
>   
> #     try :  
> #         if recherche_code_postal:  
> #             st.write(dataset[dataset["adrs_codepostal"] == recherche_code_postal])  
> #     except:  
> #         st.write("La recherche tapée n'est pas correcte.")   
> ```  
  
## 3) Lancer l'application  
  
```powershell  
streamlit run [nom fichier avec extension]  
```  
## 4) Styliser l'application avec du css  
On créer un fichier style.css à la racine du fichier de l'application, dans lequel on met notre code css.  
Puis dans le code, on  ajoute une fonction qui lie le fichier css:  
```python  
def formatage_de_la_page(fichier_css):  
    with open(fichier_css) as f:  
        st.markdown(f"<style>{f.read()}</style>", unsafe_allow_html=True)  
```  
  
Puis on appelle la fonction après les configs de la page  
  
### 4.1) Appliquer du style à un paragraphe  
code:  
```python  
st.markdown(f"<style>{f.read()}</<style>   
			{contexte}")  
```  
avec dans le css:  
p.contexte {}  
  
  
## 5) Modifier le layout  
  
### 5.1) Ajouter un sidebar  
  
Avant tout contenue de la page, pour rajouter un titre de sidebar:  
```python  
st.sidebar.header("filtre")  
```  
Et pour rajouter n'importe quel contenue à la sidebar, on met st.sidebar. à la place de st.  
  
### 5.2) Faire plusieurs pages  
  
> [!warning] Important : D'abord s'assurer que l'application marche sur une seule page  
  
Créer un dossier pages, avec les différentes pages en fichier python dedans, commençant par un numéro qui sera l'ordre des pages.  
Les différentes pages seront présentes dans la sidebar.  
  
Pour renommer les pages et ajouter des sections, il faut utiliser l'extension st-pages ([New package st-pages: change page names and icons](https://discuss.streamlit.io/t/new-package-st-pages-change-page-names-and-icons-in-sidebar-without-changing-filenames/33969))  
  
> [!tip] Penser à faire l'en-tête et bas-de-page avec une fonction pour les appeler directement sur chaque page  
  
  
## 6) Code finale  
  
  
```python  
```