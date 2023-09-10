---  
aliases: []  
nature: cours  
tags:  
  - cours  
  - python  
  - formation  
  - dataviz  
  - data  
cssclasses:  
  - banner-image  
share: true  
---  
  
[Cours python](./Cours%20python.md#)  
  
---  
> [!summary]+  
><pre class="dataview dataview-error">Evaluation Error: SyntaxError: Unexpected end of input  
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
>   
  
## 1) Base des diagrammes  
  
### 1.1) Import des bibliothèques  
```python  
from plotly.offline import iplot  
import plotly.graph_objs as go  
```  
  
### 1.2) Barres  
  
> [!Attention] **Infos**  
> <font color="#974806">**variable\_graphique = go.Bar(x=, y=, ( marker=Dictionnaire, text=liste, name=string)**</font>  
> <font color="#974806">**variable\_affichage\_graphique = go.Figure(data=_Dataframe_, layout=_Dictionnaire_)**</font>  
  
Je définis mes données  
```python  
eleves = ["Amour","Gloire","Beauté"]  
moyennes = [15,20,8]  
```  
  
Je crée une variable qui contient le graphique  
```python  
graphique = go.Bar(x=eleves, y=moyennes)  
```  
  
Je crée un emplacement qui contient mon graphique  
```python  
mon_premier_graphique = go.Figure(data=graphique)  
```  
  
J'affiche le graphique  
```python  
iplot(mon_premier_graphique)  
```  
![image - Plotly-1.png](./image/image%20-%20Plotly-1.png#)  
  
#### 1.2.1) Pour rajouter un titre au graphique  
```python  
# Je définis un titre sous forme de dictionnaire.  
# ATTENTION : la clé doit être title !  
  
titre_graphique = {"title" : "Note des 3 élèves de la promotion D2SM", "title_x" : 0.5}  
representation = go.Figure(data = graph, layout = titre_graphique)  
iplot(representation)  
```  
  
#### 1.2.2) Pour rajouter les titres des axes au graphique  
```python  
# Je complète le graphique avec les intitulés des axes :   
titre_graphique = {"title" : "Note des 3 élèves de la promotion D2SM",  
                   "xaxis" : {"title" : "Prénom"},  
                   "yaxis" : {"title" : "Note"}}  
  
representation = go.Figure(data = graph, layout = titre_graphique)  
iplot(representation)  
```  
  
#### 1.2.3) Pour modifier les couleurs  
```python  
# Je peux modifier la couleur, directement dans le jeu de données.  
# ATTENTION : marker et color sont des mots-clés  
graph = go.Bar(x = ["Tom", "Albert", "Georges"], y = [10, 12, 15],  
               marker = dict(color = ["red", "blue", "green"]))  
  
  
titre_graphique = {"title" : "Note des 3 élèves de la promotion D2SM",  
                   "xaxis" : {"title" : "Prénom", "tickangle":-30},  
                   "yaxis" : {"title" : "Note"}}  
  
representation = go.Figure(data = graph, layout = titre_graphique)  
iplot(representation)  
```  
  
#### 1.2.4) Pour rajouter des étiquettes  
```python  
# Je peux aussi rajouter des textes dans les barres.  
# ATTENTION : marker et color sont des mots-clés  
graph = go.Bar(x = ["Tom", "Albert", "Georges"], y = [10, 12, 15],  
               marker = dict(color = ["red", "blue", "green"]),  
               text = ["Moyen", "Bon", "Très bon"])  
  
  
titre_graphique = {"title" : "Note des 3 élèves de la promotion D2SM",  
                   "xaxis" : {"title" : "Prénom", "tickangle":-30},  
                   "yaxis" : {"title" : "Note"}}  
  
representation = go.Figure(data = graph, layout = titre_graphique)  
iplot(representation)  
```  
  
#### 1.2.5) Pour comparer plusieurs séries de données  
```python  
prenoms = ["Tom", "Albert", "Georges"]  
moyennes = [10, 12, 15]  
avis = ["Moyen", "Bon", "Très bon"]  
  
# Je créé les 2 graphes.  
# Je leur donne un nom. Ce nom apparaîtra comme légende cliquable.  
# Je retire les couleurs, car elles seront peut pertinentes en termes de représentation.  
graph_1 = go.Bar(x = prenoms, y = moyennes,  
               text = avis,  
               name = "2021")  
graph_2 = go.Bar(x = prenoms, y = moyennes,  
               text = avis,  
               name = "2022")  
  
# L'argument barmode indique le mode de représentation : group, stack  
titre_graphique = {"title" : "Note des 3 élèves de la promotion D2SM",  
                   "xaxis" : {"title" : "Prénom", "tickangle":-30},  
                   "yaxis" : {"title" : "Note"},  
                   "barmode" : "group"}  
  
  
representation = go.Figure(data = [graph_1, graph_2], layout = titre_graphique)  
  
iplot(representation)  
```  
  
  
### 1.3) Histogramme  
  
> [!Attention] **Infos**  
> <font color="#974806">**variable\_graphique = go.Histogram(x=, (name=string, opacity=nombre, xbins=Dictionnaire))**</font>  
> <font color="#974806">**variable\_affichage\_graphique = go.Figure(data=_Dataframe_, layout=_Dictionnaire_)**</font>  
  
avec ces dataframe:  
```python  
import random  
import numpy as np  
import pandas as pd  
from plotly.offline import iplot  
import plotly.graph_objs as go  
  
pays = random.choices(["France", "Allemagne", "Italie"], k = 100)  
age = np.random.randint(low = 20, high = 65, size = 100)  
salaire = np.random.randint(low = 2300, high = 10000, size = 100)  
  
df = pd.DataFrame({"Pays" : pays, "Age" : age, "Salaire" : salaire})  
  
allemagne = df[df.Pays == "Allemagne"]  
italie = df[df.Pays == "Italie"]  
france = df[df.Pays == "France"]  
```  
  
```python  
histogramme = go.Histogram(x = df.Pays)  
  
#donnees = [histogramme]  
  
titre_graphique = {"title" : "Répartition par pays",  
                   "xaxis" : {"title" : "Pays des personnes de l'échantillon"}}  
  
representation = go.Figure(data = histogramme, layout = titre_graphique)  
  
iplot(representation)  
```  
![image - Plotly2-1.png](./image/image%20-%20Plotly2-1.png#)  
  
#### 1.3.1) Pour comparer plusieurs séries de données  
```python  
histogramme_allemagne = go.Histogram(x = allemagne.Salaire,  
                                     name = "Allemagne",  
                                     opacity = 0.5)  
histogramme_italie = go.Histogram(x = italie.Salaire,  
                                     name = "Italie")  
histogramme_france = go.Histogram(x = france.Salaire,  
                                     name = "France",  
                                     opacity = 0.5)  
  
donnees = [histogramme_allemagne, histogramme_italie, histogramme_france]  
  
titre_graphique = {"title" : "Répartition par pays",  
                   "xaxis" : {"title" : "Pays des personnes de l'échantillon"},  
                   "barmode" : "overlay"}  
  
# IL est aussi possible de ne pas créer de variable pour le graphique et de tout intégrer dans iplot.  
iplot({"data" : donnees, "layout" : titre_graphique})  
```  
  
#### 1.3.2) Pour modifier l'échelle des axes  
```python  
histogramme_allemagne = go.Histogram(x = allemagne.Salaire,  
                                     name = "Allemagne",  
                                     opacity = 0.5,  
                                    xbins = dict(start = 2000, end = 10000, size = 500))  
histogramme_italie = go.Histogram(x = italie.Salaire,  
                                     name = "Italie",  
                                     opacity = 0.5, xbins = dict(start = 2000, end = 10000, size = 500))  
histogramme_france = go.Histogram(x = france.Salaire,  
                                     name = "France",  
                                     opacity = 0.5,  
                                 xbins = dict(start = 2000, end = 10000, size = 500))  
  
donnees = [histogramme_allemagne, histogramme_italie, histogramme_france]  
  
titre_graphique = {"title" : "Répartition par pays",  
                   "xaxis" : {"title" : "Pays des personnes de l'échantillon"},  
                   "barmode" : "overlay"}  
  
iplot({"data" : donnees, "layout" : titre_graphique})  
```  
  
  
  
  
### 1.4) Distribution  
  
> [!Attention] **Infos**  
>  
  
avec ces dataframes:  
```python  
import random  
import numpy as np  
import pandas as pd  
  
from plotly.offline import iplot  
import plotly.graph_objs as go  
  
# figure_factury ajoute des méthodes pour construire des visualisations plus complexes.  
import plotly.figure_factory as ff  
  
pays = random.choices(["France", "Allemagne", "Italie"], k = 100)  
age = np.random.randint(low = 20, high = 65, size = 100)  
salaire = np.random.randint(low = 2300, high = 10000, size = 100)  
  
df = pd.DataFrame({"Pays" : pays, "Age" : age, "Salaire" : salaire})  
  
allemagne = df[df.Pays == "Allemagne"]  
italie = df[df.Pays == "Italie"]  
france = df[df.Pays == "France"]  
```  
  
```python  
# donnees = [df.Salaire.values.tolist()]  
  
representation = ff.create_distplot(hist_data=[df.Salaire.values.tolist()],  
                                    group_labels=["Dispersion des salaires"],  
                                    bin_size=[100])  
  
representation["layout"].update(title = "Répartition des salaires", title_x=0.5)  
  
iplot(representation)  
```  
![image - Plotly-2.png](./image/image%20-%20Plotly-2.png#)  
  
#### 1.4.1) Pour comparer plusieurs séries de données  
```python  
representation = ff.create_distplot(hist_data=[allemagne.Salaire.values.tolist(), italie.Salaire.values.tolist(), france.Salaire.values.tolist()],  
                                    group_labels=["Alemagne","Italie","France"],  
                                    bin_size=200,  
                                    colors = ["blue", "green", "red"])  
  
representation["layout"].update(title = "Répartition des salaires par pays", title_x=0.5)  
  
iplot(representation)  
```  
  
#### 1.4.2) Pour retirer une partie des graphiques  
```python  
donnees_pays = [allemagne.Salaire.values.tolist(), france.Salaire.values.tolist(), italie.Salaire.values.tolist()]  
etiquettes = ["Allemagne", "France", "Italie"]  
  
representation = ff.create_distplot(donnees_pays, etiquettes,   
                                    bin_size=[200, 200, 200],  
                                    colors = ["blue", "green", "red"],  
                                    show_hist=False,  
                                    show_rug=False)  
  
iplot(representation)  
```  
  
### 1.5) Nuage de points  
  
avec ces dataframes:  
```python  
import random  
import numpy as np  
import pandas as pd  
  
from plotly.offline import iplot  
import plotly.graph_objs as go  
  
pays = random.choices(["France", "Allemagne", "Italie"], k = 100)  
age = np.random.randint(low = 20, high = 65, size = 100)  
salaire = np.random.randint(low = 2300, high = 10000, size = 100)  
  
df = pd.DataFrame({"Pays" : pays, "Age" : age, "Salaire" : salaire})  
  
allemagne = df[df.Pays == "Allemagne"]  
italie = df[df.Pays == "Italie"]  
france = df[df.Pays == "France"]  
```  
  
```python  
nuage_de_points = go.Scatter(x = allemagne.Salaire,  
                             y = allemagne.Age,  
                             mode = "markers",  
                             marker = dict(size = allemagne.Age,   
                                           color = allemagne.Salaire,  
                                           colorscale = "rainbow",  
                                           showscale = True))  
  
donnees = [nuage_de_points]  
  
titre_graphique = {"title" : "Répartition des salaires en Allemagne",  
                   "xaxis" : {"title" : "Salaires"},  
                   "yaxis" : {"title" : "Ages"}}  
  
iplot({"data" : donnees, "layout" : titre_graphique})  
```  
![image - Plotly-3.png](./image/image%20-%20Plotly-3.png#)]  
  
#### 1.5.1) Pour comparer plusieurs séries de données  
```python  
nuage_de_points_allemagne = go.Scatter(x = allemagne.Salaire,  
                             y = allemagne.Age,  
                             mode = "markers",  
                             name = "Allemagne")  
nuage_de_points_france = go.Scatter(x = france.Salaire,  
                             y = france.Age,  
                             mode = "markers",  
                             name = "France")  
  
donnees = [nuage_de_points_allemagne, nuage_de_points_france]  
  
iplot({"data" : donnees})  
```  
  
### 1.6) Courbes  
  
avec ces données:  
```python  
from plotly.offline import iplot  
import plotly.graph_objs as go  
  
mois = ["Janvier", "Février", "Mars", "Avril", "Mai", "Juin"]  
nb_etudiants = [5, 12, 27, 23, 15, 3]  
```  
  
```python  
ligne = go.Scatter(x = mois,  
                   y = nb_etudiants,  
                   mode = "lines")  
  
donnees = [ligne]  
  
iplot({"data" : donnees})  
```  
![image - Plotly-4.png](./image/image%20-%20Plotly-4.png#)  
#### 1.6.1) Pour rajouter des arguments  
```python  
ligne = go.Scatter(x = mois,  
                   y = nb_etudiants,  
                   fill = "tozerox",  
                   fillcolor = "green",  
                   mode = "lines+markers",  
                   marker = dict(size = 20, color="red"),  
                   line = dict(color = "black",  
                               width = 5,  
                               dash = "dash",  
                               shape = "spline"))  
  
donnees = [ligne]  
  
titre = {"title" : "Vente sur le <b>dernier trimestre<b>"}  
  
iplot({"data" : donnees, "layout" : titre})  
```  
  
### 1.7) Boite à moustache  
  
avec ces données:  
```python  
import random  
import numpy as np  
import pandas as pd  
  
from plotly.offline import iplot  
import plotly.graph_objs as go  
  
pays = random.choices(["France", "Allemagne", "Italie"], k = 100)  
age = np.random.randint(low = 20, high = 65, size = 100)  
salaire = np.random.randint(low = 2300, high = 10000, size = 100)  
  
df = pd.DataFrame({"Pays" : pays, "Age" : age, "Salaire" : salaire})  
  
allemagne = df[df.Pays == "Allemagne"]  
italie = df[df.Pays == "Italie"]  
france = df[df.Pays == "France"]  
```  
  
```python  
donnees = go.Box(y = allemagne.Salaire,  
                 boxmean = True)  
  
iplot([donnees])  
```  
![image - Plotly-1 1.png](./image/image%20-%20Plotly-1%201.png#)  
  
  
### 1.8) Séparer les graphiques  
  
  
```python  
import random  
import numpy as np  
import pandas as pd  
  
from plotly.offline import iplot  
import plotly.graph_objs as go  
  
from plotly import subplots  
```  
  
  
```python  
pays = random.choices(["France", "Allemagne", "Italie"], k = 100)  
age = np.random.randint(low = 20, high = 65, size = 100)  
salaire = np.random.randint(low = 2300, high = 10000, size = 100)  
  
df = pd.DataFrame({"Pays" : pays, "Age" : age, "Salaire" : salaire})  
  
allemagne = df[df.Pays == "Allemagne"]  
italie = df[df.Pays == "Italie"]  
france = df[df.Pays == "France"]  
```  
  
  
```python  
nuage_de_points_allemagne = go.Scatter(x = allemagne.Salaire,  
                             y = allemagne.Age,  
                             mode = "markers",  
                             name = "Allemagne")  
nuage_de_points_france = go.Scatter(x = france.Salaire,  
                             y = france.Age,  
                             mode = "markers",  
                             name = "France")  
  
# Je créé ma figure avec 1 ligne et 2 colonnes  
separation_graphique = subplots.make_subplots(rows = 1,  
                                           cols = 2,  
                                           subplot_titles = ("Allemagne", "France"))  
# Je définis quel graphique est dans quelle colonne  
separation_graphique.append_trace(nuage_de_points_allemagne, 1, 1)  
separation_graphique.append_trace(nuage_de_points_france, 1, 2)  
  
donnees = [nuage_de_points_allemagne, nuage_de_points_france]  
  
iplot({"data" : separation_graphique})  
```  
  
![image - Plotly-2 1.png](./image/image%20-%20Plotly-2%201.png#)  
  
#### Pour combiner les axes des graphiques  
  
```python  
nuage_de_points_allemagne = go.Scatter(x = allemagne.Salaire,  
                             y = allemagne.Age,  
                             mode = "markers",  
                             name = "Allemagne")  
nuage_de_points_france = go.Scatter(x = france.Salaire,  
                             y = france.Age,  
                             mode = "markers",  
                             name = "France")  
  
# Je créé ma figure avec 1 ligne et 2 colonnes  
# Dans ce cas, les 2 représentations partagent l'axe des y  
separation_graphique = subplots.make_subplots(rows = 1,  
                                           cols = 2,  
                                           subplot_titles = ("Allemagne", "France"),  
                                            shared_yaxes = True)  
# Je définis quel graphique est dans quelle colonne  
separation_graphique.append_trace(nuage_de_points_allemagne, 1, 1)  
separation_graphique.append_trace(nuage_de_points_france, 1, 2)  
  
donnees = [nuage_de_points_allemagne, nuage_de_points_france]  
  
iplot({"data" : separation_graphique})  
```  
  
![image - Plotly-1 2.png](./image/image%20-%20Plotly-1%202.png#)