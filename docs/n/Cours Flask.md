---  
nature: cours  
aliases:  
  - Flask  
tags:  
  - cours  
  - formation  
  - data  
  - python  
number headings: auto, first-level 2, max 6, start-at 1, 1.1)  
share_link: https://file.obsidianshare.com/37/247ced0836cad48b977637867e82db8f.html#OB9qBT2CS3AvOgO22aGZitMvXh96xa0WxnjeJ6Een84  
share_updated: 2023-10-01T16:11:36+02:00  
share: true  
---  
  
<a href="https://file.obsidianshare.com/3f/11facbe7124c27d45b5c3fe1cc49e97a.html#EBHLEzO5BZnetq/DlTd/a5tielrVWDcpJwuMwcpx3Kk" target="_self" class="external-link" ><button class="image-button" style="position: fixed;top: 100px;left: 70px;box-shadow: none !important;"><img height=100 src="https://png.pngtree.com/png-vector/20190223/ourlarge/pngtree-vector-house-icon-png-image_695369.jpg"/></button></a>  
  
> [!sommaire]- Sommaire  
> <pre class="dataview dataview-error">Evaluation Error: SyntaxError: Unexpected token '&gt;'  
    at DataviewInlineApi.eval (plugin:dataview:18618:21)  
    at evalInContext (plugin:dataview:18619:7)  
    at asyncEvalInContext (plugin:dataview:18629:32)  
    at DataviewJSRenderer.render (plugin:dataview:18650:19)  
    at DataviewJSRenderer.onload (plugin:dataview:18240:14)  
    at e.load (app://obsidian.md/app.js:1:715707)  
    at DataviewApi.executeJs (plugin:dataview:19171:18)  
    at eval (plugin:obsidian-mkdocs-publisher:28:2026)  
    at Generator.next (&lt;anonymous&gt;)  
    at eval (plugin:obsidian-mkdocs-publisher:2:871)  
    at new Promise (&lt;anonymous&gt;)  
    at m (plugin:obsidian-mkdocs-publisher:2:691)  
    at Kf (plugin:obsidian-mkdocs-publisher:28:1256)  
    at eval (plugin:obsidian-mkdocs-publisher:28:3257)  
    at Generator.next (&lt;anonymous&gt;)  
    at r (plugin:obsidian-mkdocs-publisher:2:729)</pre>  
  
[dossier de travail](file:///D:\Projets\Projets%20CEFIM\Projet%20Flask)  
  
> [!info]- [Diaporama du cours](../image/Flask%20_%20pr%C3%A9sentation%20-%20Avec%20correction.pdf#)  
> ![Diaporama du cours](../image/Flask%20_%20pr%C3%A9sentation%20-%20Avec%20correction.pdf#)  
  
ORM : object relation ship management  
  
> [!info]- [Fichier explication du projet](../image/Flask%20-%20Projet%20_%20soci%C3%A9t%C3%A9%20Tout%E2%80%99roule%20.pdf#)  
> ![Fichier explication du projet](../image/Flask%20-%20Projet%20_%20soci%C3%A9t%C3%A9%20Tout%E2%80%99roule%20.pdf#)  
  
## 1) Bases des applis  
  
### 1.1) Squelette de base  
  
```python  
from flask import Flask   
  
app = Flask(__name__) # app est le nom du fichier obligatoirement, on lui attribuel l'objet Flask du nom du fichier  
  
@app.route("/") # méthode qui permet de créer des pages web  
def f_index():   
    return "Bonjour !"   
```  
  
puis pour lancer l'appli:  
```shell  
set FLASK_ENV=development  
 set FLASK_APP=app.py  
 flask run # ou flask --app app run --debug pour le mode debug  
```  
  
on peut aussi écrire, qui est la seule facon possible de lancer si l'on veut mettre notre appli sur un hébergeur :   
```python  
if __name__ == "__main__": # si le nom du fichier est le nom du fichier principal  
	app.run(debug=True)  
```  
  
et lancer `{python} python app.py` sur le terminal  
  
### 1.2) Créer plusieurs pages  
  
On répète:  
```python  
# Créer une nouelle page qui s'appelle qui-suis-je  
@app.route("/qui-suis-je") # nom de la page a mettre à la fin de l'url pour y accéder  
def f_qui_suis_je():  
    return "Melody Duplaix"  
```  
  
Si la variable a retourner est définie avant :  
```python  
@app.route("/qui-suis-je")  
def f_qui_suis_je():  
    nom = "Melody Duplaix"  
    return f"{nom}"  
```  
  
On peut aussi utiliser des balises HTML dans le return:  
```python  
@app.route("/qui-suis-je" )   
def f_qui_suis_je ():   
    return "<H1>Jean-Lou Le Bars</H1>"  
```  
  
### 1.3) Faciliter le run de l'appli  
  
avec la bibliothèque python-dotenv:  
utiliser ces lignes dans un fichier .env pour paramétrer flask:  
```  
FLASK_DEBUG=1  
FLASK_ENV=development   
FLASK_APP=app.py  
```  
puis rajouter ceci dans le main py :  
```python  
from dotenv import load_dotenv   
load_dotenv()  
```  
  
Pour ne pas activer le cache sur le Flask:  
```python  
app.config["CACHE_TYPE"] = "null"  
```  
  
### 1.4) Utiliser un template  
  
```python  
from flask import Flask, render_template  
@app.route("/code")   
def f_code():   
    ma_liste = [10,12,11](10,12,11.md#)   
    df = pd.DataFrame(ma_liste, columns= ['Tom','Tim','Tam'])   
    return render_template("t_code.html", t_df = df["Tom"].sum())  
```  
ne pas oublier de faire un dossier templates  
et un exemple de template en html:  
```html  
<!DOCTYPE html>  
<html lang="fr">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>Document</title>  
</head>  
<body>  
    {{t_df}}  
</body>  
</html>  
```  
ou  
```python  
<!doctype html>  
<title>Hello from Flask</title>  
{% if name %}  
  <h1>Hello {{ name }}!</h1>  
{% else %}  
  <h1>Hello, World!</h1>  
{% endif %}  
```  
  
#### 1.4.1) Utiliser plusieurs variables dans un template  
```python  
@app.route("/") # méthode qui permet de créer des pages web  
def f_index():   
    v_texte = "Bonjour et bienvenue sur mon mega super hype top site"  
    v_titre = "Page d'acceuil"  
    return render_template("t_index.html",   
                           t_texte = v_texte,   
                           t_titre=v_titre)  
```  
  
  
#### 1.4.2) Utiliser un dictionnaire pour stocker les variables  
```python title:python  
@app.route("/qui-suis-je" )   
def f_qui_suis_je ():   
    prenom = "Melody"  
    nom = "Duplaix"  
    v_identite = {  
        "prenom":prenom,  
        "nom":nom,  
        "test":"test"  
    }  
    return render_template("t_qui_suis_je.html", t_identite=v_identite )  
```  
```html title:html  
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>Qui suis je</title>  
</head>  
<body>  
    <p>  
    Je m'appelle {{t_identite.prenom|capitalize}} {{t_identite.nom|upper}}.  
    </p>  
    <p>  
    Code de test: {{t_identite.test|striptags}}  
    </p>      
</body>  
</html>  
```  
  
#### 1.4.3) Utiliser les boucles et conditions dans les templates  
  
```python title:python  
@app.route("/qui-suis-je" )  
def f_qui_suis_je():   
    v_prenom = "Jean-Lou"   
    v_competences = ["Gestion de projet" , "Python", "Data"]   
    return render_template("t_qui_suis_je.html", t_prenom = v_prenom, t_competences = v_competences)  
```  
```html title:html  
<h1> {{ t_prenom }} </h1> <br>   
    {% for competence in t_competences %}   
        <li>{{ competence }}</li>   
    {% endfor %}  
```  
autre exemple:  
```html title:html  
<ul>  
        {% for competence in t_competences %}   
            {% if competence == "Python" %}   
                Il connaît très bien le langage <strong>{{competence | upper }}</strong>.   
            {% endif %}   
        {% endfor %}  
    </ul>  
```  
  
  
### 1.5) Utiliser un url dynamique  
  
```python  
@app.route("/<v_nom>")   
def f_nom(v_nom):   
    return f"Bonjour {v_nom}"  
```  
  
> [!warning] Les pages statiques sont supérieurs aux pages dynamique de base  
  
### 1.6) Gérer les pages d'erreurs  
  
```python  
@app.errorhandler (404)   
def page_introuvable(e):   
	return render_template ("t_404.html" ), 404  
```  
  
### 1.7) Faire un formulaire  
  
#### 1.7.1) Méthode classique  
  
```python  
@app.route('/formulaire', methods=['GET', 'POST'])   
def formulaire():   
    if request.method == 'POST':   
        f_nom = request.form.get('nom')   
        f_prenom = request.form.get('prenom')   
        return f'''   
        <h1>Votre nom : {f_nom}</h1>   
        <h2>Votre prénom : {f_prenom}</h2> '''   
    return '''   
        <form method="POST">   
        <div>  
            <label>Votre nom :   
                <input type="text" name="nom">  
            </label>  
        </div>  
        <div>  
            <label>Votre prénom :   
                <input type="text" name="prenom">  
            </label>  
        </div>   
            <input type="submit" value="Envoyer">   
        </form>'''  
```  
  
  
#### 1.7.2) Avec la bibliothèque WTF (What the form)  
  
[site de la librairie](https://flask-wtf.readthedocs.io/en/1.0.x/)  
mvc : model vue controller   
  
```python title:imports  
from flask_wtf import FlaskForm   
from wtforms import StringField, SubmitField  
from wtforms.validators import DataRequired  
```  
  
```python title:"config de la clé secrète"  
app.config['SECRET_KEY'] = "Ma super clé !"  
```  
  
```python title:"code python"  
class c_Formulaire_enregistrement_informations(FlaskForm):   
    wtf_nom = StringField( "Nom", validators =[DataRequired()])   
    wtf_envoyer = SubmitField( "Envoyer" )  
  
@app.route("/formulaire")   
def f_formulaire():   
    f_formulaire = c_Formulaire_enregistrement_informations()   
    print(f"Formulaire créé ! {f_formulaire}.")   
    return "Formulaire bien créé"   
```  
  
puis:  
```python title:"envoi forumaire"  
class t_Formulaire_enregistrement_informations(FlaskForm):   
    wtf_nom = StringField( "Nom", validators =[DataRequired()])   
    wtf_envoyer = SubmitField( "Envoyer" )  
  
  
@app.route("/formulaire", methods=["GET", "POST"])  
def f_enregistrer_informations():  
 f_formulaire = t_Formulaire_enregistrement_informations()  
 if f_formulaire.validate_on_submit():  
    f_nom = f_formulaire.wtf_nom.data  
    f_formulaire.wtf_nom.data = ""  
 return render_template("t_formulaire.html" ,  
                          t_titre = "Formulaire d'inscription",  
                          html_formulaire = f_formulaire)  
```  
  
```html title:html  
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>formulaire d'inscription</title>  
</head>  
<body>  
    <H1>Formulaire d'enregistrement d'un intervenant</H1>   
    <form method="POST">   
        {{ html_formulaire.hidden_tag()}}   
        {{ html_formulaire.wtf_nom.label }}   
        {{ html_formulaire.wtf_nom() }}   
        <br/>   
        {{ html_formulaire.wtf_envoyer()}}   
    </form>  
</body>  
</html>  
```  
  
  
### 1.8) Insérer des images  
  
les images doivent être dans un dossier images dans un dossier static  
```html  
<img src="{{url_for('static', filename='images/photo_profil_linkedIn.excalidraw.png')}}" class="photo" width=50 heigth=50 >  
```  
  
### 1.9) Utiliser boostrap  
  
Dans le head, rajouter ces lignes  pour lier aux css de bootstrap:  
```html  
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">  
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>  
```  
  
puis regarder dans les docs de boostrap les class et attributs à utiliser pour obtenir tel forme d'élément  
  
### 1.10) Utiliser un template de base pour tous les templates  
```html title:"template de base (base.html)"  
<!DOCTYPE html>   
<html lang="en">   
    <head>   
        <meta charset="UTF-8">   
        <meta http-equiv="X-UA-Compatible" content="IE=edge">   
        <meta name="viewport" content="width=device-width, initial-scale=1.0">   
        <title>Document</title>   
    </head>   
    <body> EN-TETE<br/>   
        {% block content %}   
        {% endblock %}   
        <p></p> PIED DE PAGE<br/>   
    </body>   
</html>  
```  
  
```python title:"contenu de chaque fichier utilisant ce template"  
{% extends "base.html" %}   
{% block content %}   
	<h1>{{ t_texte.upper() }}</h1>   
{% endblock %}  
```  
  
### 1.11) Afficher des graphiques  
  
Mettre toutes nos analyses dans un fichier analyses.py  
On convertir les graphiques en json:  
```python title:"analyses.py"  
def analyse_kpi():   
	donnees = go.Bar(x = ["Tom", "Albert", "Georges"], y = [10, 12, 15])   
	graph = go.Figure(data = donnees)   
	graph_JSON = json.dumps(graph, cls=plotly.utils.PlotlyJSONEncoder)   
	return graph_JSON  
```  
  
puis pour afficher le graph:  
```python title:"app.py"  
@app.route("/graphique")   
def f_graphiques():   
	f_analyse_graphique = analyse_kpi()   
	return render_template('t_graphiques.html', t_graphique=f_analyse_graphique)  
```  
  
et on l'insère dans le template:  
```html title:"template html"  
<script src='https://cdn.plot.ly/plotly-latest.min.js'></script>   
<div id ="chart">   
	<script type='text/javascript'>   
		var graphs = {{ t_graphique | safe }};   
		Plotly.plot("chart",graphs,{})   
	</script>   
</div>  
```  
  
  
### 1.12) Schéma de fonctionnement  
  
![1000](../../Cours%20Flask%20sch%C3%A9ma%20du%20fonctionnement.excalidraw.md#)  
  
## 2) Projet en groupe  
  
[dossier de travail](file:///D:\Projets\Projets%20CEFIM\projet_flask_asso)  
[dossier de travail dans vscode](vscode://file/D:\Projets\Projets%20CEFIM\projet_flask_asso)  
[dossier google drive](https://drive.google.com/drive/folders/1YVRCp_JS0YSynAyC5yk9ozHMueVXBrDQ)  
[repo github](https://github.com/MelodyDuplaix/projet_flask)  
[excalidraw du projet](https://excalidraw.com/#room=1ea4f5cdfadf1386bbe0,sgZwUA6XETmNKcY8N0J6Iw)  
  
code de création des tables de données:  
```sql  
CREATE TABLE vehicule(  
   id_vehicule INTEGER PRIMARY KEY,  
   type VARCHAR(50) NOT NULL  
);  
  
CREATE TABLE chauffeurs(  
   id_chauffeur INTEGER PRIMARY KEY,  
   nom VARCHAR(50) NOT NULL,  
   prenom VARCHAR(50) NOT NULL,  
   genre VARCHAR(2) NOT NULL  
);  
  
CREATE TABLE trajets(  
   id_trajet INTEGER PRIMARY KEY,  
   km_fin INT NOT NULL,  
   km_debut INT NOT NULL,  
   commentaire VARCHAR(250),  
   id_vehicule CHAR(50) NOT NULL,  
   id_chauffeur INT NOT NULL,  
   FOREIGN KEY(id_vehicule) REFERENCES vehicule(id_vehicule),  
   FOREIGN KEY(id_chauffeur) REFERENCES chauffeurs(id_chauffeur)  
);  
  
```  
  
  
### 2.1) Daily scrum 28-09  
  
envoie des données des trajets à la base  
mise en page du formulaire  
essai de validation des noms et prénoms avant envoie ->  non marché difficulté  
commencé page de visualisation des tables avec table des chauffeurs et table des véhicules  
je vais finir la visualisation des des tables avec la table des trajets