---  
aliases: []  
nature: cours  
tags:  
  - cours  
  - python  
  - formation  
  - data  
  - SQL  
cssclasses: []  
share: true  
---  
  
[📑 Cours python](./%F0%9F%93%91%20Cours%20python.md#)  
  
---  
diaporama du cours : [Python et base de données.pdf](./image/Python%20et%20base%20de%20donn%C3%A9es.pdf#)  
  
```toc  
```  
  
## 1) Les manières de stocker des données  
  
- Fichiers  
	- fichiers tableurs  
	- fichiers textes  
	- fichiers binaire (SQLite)  
- Base de données ( propriétaires: SQLServer, Oracle, DB2; ou libres de droits: MySQL, PostGreSQL, Maria DB)  
	- SGBDR (relationnels)  
	- NoSQL (non relationnelles)  
- BDD Online  
	- Microsoft Azure / dataverse  
	- Amazon : AWS  
	- Facebook : Cassandra  
	- Google : Firebase  
  
Pour gérer des bases de données que l'on ne connaît pas et créer les schémas des tables: DBeaver et DBschema  
  
## 2) Etude de cas conception base de données  
  
objectif : [concevoir un modèle conceptuel de données](https://fr.wikipedia.org/wiki/Mod%C3%A8le_entit%C3%A9-association) + un dictionnaire des données  
méthode : [MERISE](https://fr.wikipedia.org/wiki/Merise_(informatique))  
logiciel : [Looping](https://www.looping-mcd.fr/)  
  
### 2.1) Vocabulaire  
  
- **UML** : formalisme permettant notamment de formaliser un SGBD (Système de Gestion de base de données)  
- **MERISE** : méthode pour formaliser un système d'information. notamment les données à travers plusieurs schémas dont les MCO. MLO. MP O. Le vocabulaire pour un MCD est suivant est utilisé :  
	- **entité** : composant d'une base de données. Une entité est un nom commun. elle est unique, écrit en minuscule. au pluriel. sans signe diacritique et sans espace.  
	- **association** : relation entre 2 entités. une association est un verbe à l'infinitif écrit en minuscule.  
	- **schéma entité association** : représentation graphique  
	- **attribut** : propriétés d'une entité.  
		- Exemple : entité personne peut avoir comme attribut : nom. prenom  
	- **clé** : attribut particulier identifiant de façon unique les propriété d'une entité une clé peut etre unique (une seule propriété) ou composée (plusieurs propriétés).  
	- **occurrence** : données contenues dans une entité.  
	- **cardinalité** : nombre d'entités reliées entre elles par une association.  
		- Exemple :  
			- une personne (entité)  
			- possède (association)  
			- aucun ou plusieurs (cardinalité)  
			- animaux (entité)  
- **Dépendance fonctionnelle** : à partir d'une valeur ou plusieurs valeurs, j'ai accès à une et une seule valeur.  
	- Exemple :  
		- dépendance élémentaire : à partir d'un no de sécurité sociale, j'ai accès à un seul individu  
		- dépendance non élémentaire : à partir d'un code produit et d'une quantité, j'ai accès au montant  
	- Il est possible de représenter ces dépendances avec un **graphe de couverture** minimum.  
  
### 2.2) Utilisation de looping  
  
- Création d'un nouveau fichier  
- Création d'entités  
	- nom : en minuscule, au pluriel  
	- création de champs/variable  
		- nom  
		- type  
		- clé primaire (1) : généralement id\__nomd'identifiant_   
- On peut cliquer sur scripts SQL tout à droite pour afficher le code correspondant  
	- attention, il ne doit pas y avoir d'entité vides  
- Création d'associations, en cliquant sur lien et en faisant glisser  
- double-cliquer pour modifier l'association  
	- nom = verbe d'action  
	- cardinalité (règles)  
		- de l'entité vers l'autre entité en passant vers le verbe d'action, avec la cardinalité la plus proche de l'entité d'origine  
		- 0,1 : un apprenant peut suivre 0 ou 1 formation  
		- 1,1 : un apprenant peut suivre 1 seule formation  
		- 0,n : un apprenant peut suivre 0 ou plusieurs formations  
		- 1,n : un apprenant peut suivre 1 ou plusieurs formations  
- Création de règles possible pour completer les liens, mais alourdit la lecture  
- Affichage du Scripts SQL, du MLD textuel  
  
### 2.3) La normalisation des données  
<u>objectifs : </u>  
- eviter les redondances  
- avoir une base de connaissance cohérentes  
- faciliter les mises à jour  
  
2 entités qui ont les mêmes attributs doivent être fusionné -> association réflexive  
![image - Bases de données avec python-1.png](./image/image%20-%20Bases%20de%20donn%C3%A9es%20avec%20python-1.png#)  
![image - Bases de données avec python-2.png](./image/image%20-%20Bases%20de%20donn%C3%A9es%20avec%20python-2.png#)  
  
  
  
## 3) SQLite  
- intégré de base à Python  
- système de base de données open source léger  
- librairie  
- système de commande en ligne  
- 5 type de données + sous-types  
	- null  
	- int  
	- real  
	- text  
	- blob  
  
### 3.1) Création d'une base de données avec SQLite  
1. connexion si elle existe, creation sinon  
2. création table et champs  
3. transmet ces informations (commit)  
4. ferme la table  
  
tutoriel : [SQLite Tutorial - An Easy Way to Master SQLite Fast](https://www.sqlitetutorial.net/)  
  
### 3.2) Sur l'étude de cas  
  
Avec DB browser:  
1. creation d'une base  
2. copier-coller le code depuis looping  
3. modifier certains champs : clés, bytes  
	- bien vérifier 1 table = 1 clé primaire sauf les tables de liaison verbe  
4. écrire des données en faisant attention au sens d'écriture (sans clés étrangères en premier)  
5. écrire des déclencheurs (triggers) pour les mails  
  
### 3.3) Utilisation sous python  
  
![500|center](./image/Sch%C3%A9ma%20SQLite%20sous%20python.excalidraw.svg#)  
  
  
#### 3.3.1) Création d'une base de données  
  
Import SQLite3:  
```python  
import sqlite3  
```  
  
Sous forme de fichier:  
```python  
connexion = sqlite3.connect("mabase.db")  
```  
  
Sous forme de base de donnée en mémoire:  
```python  
connexion = sqlite3.connect(":memory:")  
```  
  
Les deux permettent à la fois de se connecter ou de créer une base.  
La base est crée au même niveau que le fichier de code.  
  
Pour réaliser des actions, il faut un curseur, un objet qui me permettre de réaliser des actions:  
```python  
curseur = connexion.cursor()  
```  
  
On peut ensuite créer des tables et des champs avec:  
```python  
curseur.execute("""  
	CREATE TABLE intervenants (  
	prenom_bdd text,  
	nom_bdd text,  
	mail_bdd text  
	)  
	""")  
```  
_les docstrings servent à plus de lisibilité en étendant sur plusieurs lignes_  
  
**<font color="#76923c"> Bonne pratique </font>** : créer une variables pour toute requête  
```python  
table_intervenants = """  
                CREATE TABLE intervenants (  
                    prenom_bdd text,  
                    nom_bdd text,  
                    mail_bdd text  
                )  
                """  
curseur.execute(table_intervenants)  
```  
  
On peut ensuite envoyer les infos à la base et la fermer:  
```python  
connexion.commit()  
connexion.close()  
```  
  
Pour éviter d'écraser une base, on ajoute une instruction qui ne crée la base que si elle n'existe pas déja:  
```python  
import os  
import sqlite3  
def f_creerLaBaseDeDonnees():  
   if os.path.isfile('base_intervenants.db'):  
       print("la base existe déjà.")  
   else :  
       connexion = sqlite3.connect("base_intervenants.db")  
       curseur = connexion.cursor()  
       curseur.execute("""  
               …….  
```  
  
#### 3.3.2) Insérer des données dans la base  
  
On utilise aussi le curseur:  
```python  
curseur.execute("""  
      INSERT INTO intervenants VALUES (  
      'Jean-Lou', 'Le Bars', 'jllebars@gmail.com'  
)  
""")  
```  
ceci est sous forme de tupple  
  
Pour le faire sous forme de liste:  
```python  
liste_intervenants = [  
     ('Harris', 'Tote', 'h.tote@hotmail.com'),  
     ('Eva', 'Nouie', 'e.nouie@gmail.com'),  
     ('Tugudule', 'Niguedouille', 't.niguedouille@wanadoo.fr')  
               ]  
curseur.executemany("INSERT INTO intervenants VALUES(?,?,?)", liste_intervenants)  
```  
  
#### 3.3.3) Afficher des données  
  
On sélectionne les données puis on les affiche:  
```python  
curseur.execute("SELECT * FROM intervenants")  
print(curseur.fetchall())  
```  
  
On peut stocker la selection dans une variable:  
```python  
liste_intervenants = curseur.execute("SELECT * FROM intervenants")  
  for intervenant in liste_intervenants:  
     print(intervenant)  
```  
  
  
#### 3.3.4) Création de triggers  
  
Instruction SQL qui permet de vérifier des données ou de manipuler des données  
  
exemple de trigger:  
```python  
trigger_forme = """  
                CREATE TRIGGER IF NOT EXISTS verification_forme  
                BEFORE INSERT ON casseroles  
                FOR EACH ROW  
                    WHEN NEW.forme NOT IN ('russe', 'sauteuse')  
                    BEGIN  
                        SELECT RAISE(ABORT, 'Seules les valeurs russe et sauteuse sont acceptées pour le champ forme');  
                    END;  
                """  
curseur.execute(trigger_forme)  
```  
  
Pour avoir une saisie de données avec erreur bien formaté:  
```python  
def inserer_produits_avec_verification() :  
      
    marque = input("Quelle est la marque : ")  
    taille = input("Quelle est la taille : ")  
    forme =input("Quelle est la forme : ")  
    induction =int(input("Est-elle à induction (0 = non ; 1 = oui) : "))  
    materiau =input("Quelle est son matériau : ")  
    manche =input("Quelle est la matière de son manche : ")  
    four =int(input("Peut-on la mettre au four (0 = non ; 1 = oui) : "))  
    revetement =input("Quel est son revetement : ")  
      
    reponse = [marque, taille, forme, induction, materiau, manche, four, revetement]  
      
    return reponse  
  
encore_une_saisie = "o"  
  
while encore_une_saisie != "n":   
  
    saisie_produits = inserer_produits_avec_verification()  
    print(saisie_produits)  
      
    try :   
        curseur.execute("INSERT INTO casseroles VALUES(?,?,?,?,?,?,?,?)", saisie_produits)  
    except sqlite3.IntegrityError as e:  
        print(e)  
          
    encore_une_saisie = input("Voulez-vous continuer (o/n)")  
```  
  
#### 3.3.5) Code qui créer la base, la table et les données par des inputs  
  
```python  
import sqlite3  
import os  
  
def creer_bdd(bdd) -> "str":  
    """  
    :name : creer_bdd  
    :param : nom de la base de données sans extension  
    :return : soit la base de données, soit un message d'erreur.  
    :desc : création du nom de la base de données puis tests la création / l'existence de la base de données.  
    """  
    nom_bdd = bdd + ".db"  
  
    print("============== REQUETE POUR LA CREATION DE LA BASE =======================")  
    print(f"Le nom de la base de données est :  {nom_bdd}.")  
    print("==========================================================================")  
      
    if os.path.isfile(nom_bdd):  
        print(f"La base de données {nom_bdd} existe DEJA.")  
        return nom_bdd  
    else :   
        try :  
            connexion = sqlite3.connect(nom_bdd)  
            print(f"La base de donnée '{nom_bdd}' a BIEN été créée.")  
            connexion.close()  
            return nom_bdd  
        except sqlite3.Error as e:  
            print(f"Il y a eu un souci : {e}")  
  
def se_connecter(bdd, requete):  
    connexion = sqlite3.connect(bdd)  
    curseur = connexion.cursor()  
    curseur.execute(requete)  
    connexion.commit()  
    curseur.close()  
    connexion.close()  
              
def creer_table(bdd, name_table) -> "message":  
    """  
    :name : creer_table  
    :param : la base de données, la table  
    :return : un message indiquant si la table a bien été créée ou pas.  
    :desc : je créé la requête de création d'une table. J'y intègre aussi un chmp id et date  
    """  
    requete_creation_table = f"CREATE TABLE {name_table} \  
                (id INTEGER PRIMARY KEY AUTOINCREMENT, \  
                 date DATETIME NOT NULL DEFAULT (strftime('%Y-%m-%d %H:%M:%S', 'now', 'localtime')));"  
    print("============== REQUETE POUR LA CREATION DE LA TABLE =======================")  
    print("===========================================================================")  
    try:  
        se_connecter(bdd, requete_creation_table)  
        print(f"La table '{name_table}' a bien été créée.")  
    except sqlite3.Error as e:  
            print(f"ERREUR: {e}")  
  
def creer_champs(bdd, table, champs) -> "Affichage des champs de la table":  
    """  
    :name : creer_champs  
    :param : la base de données, la table, le/les champs sous forme de liste  
    :return : un message indiquant si la / les champs ont bien été créés.  
    :desc : je modifie les colonnes de la base de données avec le / les intitulés de la liste  
    """  
      
    print("============== REQUETE POUR LA CREATION DES CHAMPS =======================")  
    print("==========================================================================")  
      
    for champ in champs:  
        requete_creation_champs = f"ALTER TABLE {table} ADD COLUMN {champ};"  
        try:  
            se_connecter(bdd, requete_creation_champs)  
        except sqlite3.Error as e:  
            raise(f"ERREUR: {e}")  
      
    print(f"Les champs {champs} de la base de données ont bien été ajoutés.")  
  
def enregistrer_donnees(bdd, table, champs, donnees) -> "Enregistrer les données la base de données":  
    """  
    :name : enregistrer_donnees  
    :param : la base de données, la table, le/les champs, les données  
    :return : un message indiquant si les données ont bien été enregistrées.  
    :desc : les données des listes champs et table sont converties en chaîne de caractères séparées par des virgules.  
            Les données doivent être entourées de ' '.  
    """  
      
    print("============== REQUETE L'AJOUT D'UNE DONNE ===============================")  
    print("==========================================================================")  
    # Je convertis les champs qui sont sous forme de liste en suite de caractères séparés par des ,  
    liste_des_champs = ",".join(champs)  
      
    # Je convertis les données qui sont sous forme de liste en suite de caractère.  
    # ATTENTION : les valeurs de VALUES sont de la forme ('val1', 'Val2'). Je dois donc rajouter des '  
    for donnee in donnees :  
        liste_des_valeurs = "'" + "','".join(donnee) + "'"  
      
    requete_enregistrement_donnees = f"INSERT INTO {table} ({liste_des_champs}) VALUES ({liste_des_valeurs})"  
    print(requete_enregistrement_donnees)  
      
    try:  
        se_connecter(bdd, requete_enregistrement_donnees)  
        print(f"Les données ont été enregistrées.")  
    except sqlite3.Error as e:  
            print(f"ERREUR: {e}")  
  
if __name__ == '__main__':  
      
    # CREATION DE LA BASE DE DONNEES  
    nom_bdd = input("Quel est le NOM de la BASE DE DONNEES : ")  
    BASE_DE_DONNEES = creer_bdd(nom_bdd)  
  
    # CREATION DE LA TABLE  
    nom_table = input("Quel est le NOM de la TABLE : ")  
      
    creer_table(BASE_DE_DONNEES, nom_table)  
      
    # CREATION DES CHAMPS  
    liste_des_champs = []  
    encore_champs = True  
  
    print("Vous allez créer les CHAMPS de la base de données.")  
    print("Pour arrêter de saisir les champs, appuyer sur  >> Entrée << sans entrer de données.")  
    numero = 1  
    while encore_champs :  
        champ_nom = input(f"=====>   CHAMP n°{numero} : ")  
        if champ_nom == "":  
            encore_champs = False  
        else:  
            if " " in champ_nom :  
                champ_nom = champ_nom.replace(" ", "_")  
            liste_des_champs.append(champ_nom)  
            numero += 1  
  
    creer_champs(BASE_DE_DONNEES, nom_table, liste_des_champs)  
      
    # INSERTION DES DONNEES  
    encore_donnees = True  
    liste_des_donnees = []  
      
    while encore_donnees:  
        ajouter_des_donnees = input(f"Prêt à ajouter les DONNEES (o/n) : ").lower()  
  
        if ajouter_des_donnees == "o":  
            ligne = []  
            for champ in liste_des_champs :  
                information = input(f"Quelle est votre DONNEE pour le champ {champ.upper()} : ")  
                ligne.append(information)  
            if ligne:  
                liste_des_donnees.append(ligne)  
            enregistrer_donnees(BASE_DE_DONNEES, nom_table, liste_des_champs, liste_des_donnees)  
        else :  
            print("Fin de la saisie des données.")  
            encore_donnees = False  
```  
  
  
  
  
  
  
  
  
%%  
parent:: [Python et base de données.pdf](./image/Python%20et%20base%20de%20donn%C3%A9es.pdf#)  
exemple:: [Bases de données avec python-1.png](Bases%20de%20donn%C3%A9es%20avec%20python-1.png#), [Bases de données avec python-2.png](Bases%20de%20donn%C3%A9es%20avec%20python-2.png#), [Schéma SQLite sous python.excalidraw](../Sch%C3%A9ma%20SQLite%20sous%20python.excalidraw.md#)  
précédent:: [📑 Cours python](./%F0%9F%93%91%20Cours%20python.md#)  
%%