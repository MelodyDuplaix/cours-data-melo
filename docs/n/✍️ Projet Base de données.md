---  
nature: note  
tags:  
  - formation  
  - data  
share: true  
---  
  
  
<u>fait:</u>  
- [x] création base de données et tables ✅ 2023-07-04  
- [x] requêtes SQL ✅ 2023-07-04  
- [x] structuration base de données ✅ 2023-07-04  
- [x] insertion de données interactive ✅ 2023-07-04  
<u>à finir: </u>  
- [x] trigger lors de l'insertion des données (dates  principalement) ✅ 2023-07-08  
<u>a faire : </u>  
- [x] pdf ✅ 2023-07-14  
- [x] remodifier pour rajouter la date de sortie en non-obligatoire ✅ 2023-07-11  
  
Difficultés rencontrés / ressources utilisés:  
flux chat GPT: [Conversation chat GPT projet base de données](../../Conversation%20chat%20GPT%20projet%20base%20de%20donn%C3%A9es.md#)  
  
| Difficultés                                                                        | Ressources                                                                                                                                                                       |  
| ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |  
| création de clé primaire qui s'auto-incrémente -> tout seul si INTEGER PRIMARY KEY | chat GPT: [Conversation chat GPT projet base de données > Auto-incrémentation SQLite](../../Conversation%20chat%20GPT%20projet%20base%20de%20donn%C3%A9es.md#auto-incrementation-sqlite)                                                                                            |  
| Format des dates pour pouvoir calculer avec                                        | chat GPT : [Conversation chat GPT projet base de données > Format des dates](../../Conversation%20chat%20GPT%20projet%20base%20de%20donn%C3%A9es.md#format-des-dates)                                                                                                     |  
| Calculer la médiane avec SQLite                                                    | forum : [Median in SQLITE Online. HELP! : SQL (reddit.com)](https://www.reddit.com/r/SQL/comments/pizk0l/median_in_sqlite_online_help/)                                                                                                                                                                                 |  
| Afficher les doublons                                                              | forum : [Afficher les doublons dans une requête - Langage SQL (developpez.net)](https://www.developpez.net/forums/d1800438/bases-donnees/langage-sql/afficher-doublons-requete/) |  
  
> [!info]- [Explications](../image/Formation%20Data%20Analyst%20_%20%C3%A9valuation%20sur%20les%20bases%20de%20donn%C3%A9es.pdf#)  
> ![Explications](../image/Formation%20Data%20Analyst%20_%20%C3%A9valuation%20sur%20les%20bases%20de%20donn%C3%A9es.pdf#)  
  
  
## Création de l'application  
  
> [!info]- [Diagramme des fonctions projet base de données](../../Diagramme%20des%20fonctions%20projet%20base%20de%20donn%C3%A9es.md#)  
> ![800](../../Diagramme%20des%20fonctions%20projet%20base%20de%20donn%C3%A9es.md#)  
  
[lien vers les explications](https://app.diagrams.net/#G1IgvqDSKpCUhH_ogWS3N67wMkRwSO4xd0)  
  
> [!note]- Code finale de modification des salariés  
> ```python  
> # Code principal  
>   
> # Récupération des salariés  
> dataset = récupération_dataset_total()  
> dataset["identifiant"] = dataset["prenom"] + " " + dataset["nom_sa"]  
> liste_nom = dataset["identifiant"].to_list()  
>   
> individu = st.selectbox("Salariés à modifier", options=liste_nom)  
>   
>   
> ligne_individu = dataset[dataset["identifiant"] == individu]  
> id = ligne_individu["id"]  
> with st.form("Formulaire d'ajout", clear_on_submit=False):  
>     prenom = st.text_area("Prénom", max_chars=25, placeholder="Pas de prénom", height=1, key="prenom", value=ligne_individu["prenom"].values[0])  
>   
>     nom = st.text_area("Nom", max_chars=25, placeholder="Pas de nom", height=1, key="nom", value=ligne_individu["nom_sa"].values[0])  
>   
>     mail = st.text_area("Mail", max_chars=50, placeholder="Pas de mail", height=1, key="mail", value=ligne_individu["mail"].values[0])  
>     if mail and( not "@" in mail or " " in mail):  
>         st.write(":red[Le mail n'est pas valide !]")  
>   
>     today = datetime.datetime.now()  
>     date_de_naissance= date_obj = datetime.datetime.strptime(ligne_individu["date_naissance"].values[0], "%Y-%m-%d")  
>     date_de_naissance = st.date_input(  
>         "Date de naissance", max_value=datetime.date((today.year-18), 1, 1), min_value= datetime.date((today.year-100), 1, 1),  
>         format="YYYY.MM.DD", key="date_naissance", value=date_de_naissance  
>     )  
>     if ligne_individu["genre"].values[0] == "F":  
>         genres_possible = ("F","M")  
>     else:  
>         genres_possible = ("M","F")  
>   
>     genre = st.selectbox("Genre", genres_possible, help="Homme : H Femme : F", key="genre")  
>   
>     date_entree= date_obj = datetime.datetime.strptime(ligne_individu["date_arrivee"].values[0], "%Y-%m-%d")  
>     date_arrive = st.date_input(  
>         "Date d'entrée dans l'entreprise", min_value= datetime.date((today.year-60), 1, 1),  
>         format="YYYY.MM.DD", key="date_arrive", value=date_entree  
>     )  
>     liste_ville = récupérer_liste_ville()  
>     liste_ville_update = liste_ville.copy()  
>     liste_ville_update.remove(ligne_individu["nom_ville"].values[0])  
>     liste_ville_update.insert(0, ligne_individu["nom_ville"].values[0])  
>     localisation = st.selectbox("Ville",liste_ville_update, key="localisation")  
>     table_ville = récupérer_tableau_ville()  
>     localisation_id = table_ville[table_ville["nom"]==localisation]["id"].values  
>     envoie = st.form_submit_button("Envoyer")  
>     if envoie:  
>         connexion = sqlite3.connect("data/personnel_societe_paddle")  
>         cursor = connexion.cursor()  
>         date_de_naissance_str = date_de_naissance.strftime("%Y-%m-%d")  
>         date_arrive_str = date_arrive.strftime("%Y-%m-%d")  
>         reponse = [prenom.capitalize(), nom.upper(), mail, genre, date_de_naissance_str, date_arrive_str, int(localisation_id),  int(id)]  
>         # Exécutez la commande SQL UPDATE pour mettre à jour la ligne  
>         try:  
>             cursor.execute(""" UPDATE salariés  
>             SET prenom = ?, nom_sa = ?, mail = ?, genre = ?, date_naissance = ?, date_arrivee = ?, id_ville = ?  
>             WHERE id_salarie = ?;  
>         """, reponse)  
>         except sqlite3.IntegrityError as e:  
>             st.write(e)  
>         connexion.commit()  
>         connexion.close()  
>         st.write("Les données ont bien été mises à jour")  
>         st.write(localisation_id)  
> ```  
  
![image -  Projet Base de données - code boutons RGPD.png](../image/image%20-%20%20Projet%20Base%20de%20donn%C3%A9es%20-%20code%20boutons%20RGPD.png#)  
  
![image -  Projet Base de données - code footer.png](../image/image%20-%20%20Projet%20Base%20de%20donn%C3%A9es%20-%20code%20footer.png#)  
  
  
lien de l'application: [Analyse associations · Streamlit (applicationpaddle-kh3bz5ahsvdpecynosenia.streamlit.app)](https://applicationpaddle-kh3bz5ahsvdpecynosenia.streamlit.app/Afficher%20les%20salari%C3%A9s)  
  
%%  
source :: [📟 Cours SQL](./%F0%9F%93%9F%20Cours%20SQL.md#) , [📇 Cours python - Bases de données](./%F0%9F%93%87%20Cours%20python%20-%20Bases%20de%20donn%C3%A9es.md#)  
parent:: [Cefim note principale](../../CEFIM%20note%20principale.md#)  
enfant:: [Explications](../image/Formation%20Data%20Analyst%20_%20%C3%A9valuation%20sur%20les%20bases%20de%20donn%C3%A9es.pdf#), [Conversation chat GPT projet base de données](../../Conversation%20chat%20GPT%20projet%20base%20de%20donn%C3%A9es.md#)  
%%  
  
---  
[Cefim note principale](../../CEFIM%20note%20principale.md#)