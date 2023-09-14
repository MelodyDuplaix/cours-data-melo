---  
url: https://docs.streamlit.io/library/advanced-features/button-behavior-and-examples  
date: 2023-09-14  
nature: article  
aliases:  
  - boutons streamlit  
fileClass: articles  
tags:  
  - logiciel  
  - data  
  - python  
  - idée  
share: true  
---  
  
[Button behavior and examples - Streamlit Docs](https://docs.streamlit.io/library/advanced-features/button-behavior-and-examples)  
  
Les boutons créés avec [`st.button`](https://docs.streamlit.io/library/api-reference/widgets/st.button) ne conservent pas d'état. Ils renvoient `True` lors de la ré-exécution du script résultant de leur clic et retournent immédiatement à `False` lors de la ré-exécution suivante du script. Si un élément affiché est imbriqué dans `if st.button('Click me'):`, l'élément sera visible lorsque le bouton sera cliqué et disparaîtra dès que l'utilisateur effectuera son action suivante. Ceci est dû au fait que le script est réexécuté et que la valeur de retour du bouton devient `False`.  
  
Dans ce guide, nous allons illustrer l'utilisation des boutons et expliquer les idées fausses les plus courantes. Lisez la suite pour voir une variété d'exemples qui développent `st.button` en utilisant [`st.session_state`](https://docs.streamlit.io/library/api-reference/session-state). Des [Anti-patterns] (https://docs.streamlit.io/library/advanced-features/button-behavior-and-examples#anti-patterns) sont inclus à la fin. Allez-y et ouvrez votre éditeur de code favori pour pouvoir exécuter les exemples pendant que vous lisez. Si vous n'avez pas encore exécuté vos propres scripts Streamlit, consultez la page [Concepts principaux] de Streamlit (https://docs.streamlit.io/library/get-started/main-concepts).  
  
Lorsqu'un code est conditionné par la valeur d'un bouton, il s'exécute une fois en réponse au clic sur le bouton et ne s'exécute plus (jusqu'à ce que le bouton soit cliqué à nouveau).  
  
Bon à placer à l'intérieur des boutons :  
  
- Messages transitoires qui disparaissent immédiatement.  
- Processus unique par clic qui enregistre des données dans l'état de la session, dans un fichier ou dans une base de données.  
  
Il n'est pas souhaitable de placer des boutons à l'intérieur :  
  
- Les éléments affichés qui doivent persister pendant que l'utilisateur continue.  
- Autres widgets qui entraînent la ré-exécution du script lorsqu'ils sont utilisés.  
- Processus qui ne modifient pas l'état de la session et n'écrivent pas dans un fichier ou une base de données.\*  
  
\* Cela peut s'avérer utile lorsque des résultats jetables sont souhaités. Si vous avez un bouton "Valider", il pourrait s'agir d'un processus conditionné directement par un bouton. Il pourrait être utilisé pour créer une alerte indiquant "Valide" ou "Invalide" sans qu'il soit nécessaire de conserver cette information.  
  
Si vous voulez donner à l'utilisateur un bouton rapide pour vérifier si une entrée est valide, mais ne pas garder cette vérification affichée au fur et à mesure que l'utilisateur continue.  
  
Dans cet exemple, un utilisateur peut cliquer sur un bouton pour vérifier si sa chaîne `animal` se trouve dans la liste `animal_shelter`. Lorsque l'utilisateur clique sur "**Vérifier la disponibilité**", il verra "Nous avons cet animal !" ou "Nous n'avons pas cet animal." S'il change l'animal dans [st.text_input](https://docs.streamlit.io/library/api-reference/widgets/st.text_input), le script est réexécuté et le message disparaît jusqu'à ce qu'il clique à nouveau sur "**Vérifier la disponibilité**".  
  
```  
import streamlit as st  
  
animal_shelter = ['cat', 'dog', 'rabbit', 'bird']  
  
animal = st.text_input('Type an animal')  
  
if st.button('Check availability'):  
    have_it = animal.lower() in animal_shelter  
    'We have that animal!' if have_it else 'We don\'t have that animal.'  
```  
  
Note : L'exemple ci-dessus utilise [magic](https://docs.streamlit.io/library/api-reference/write-magic/magic) pour rendre le message sur le frontend.  
  
Si vous voulez qu'un bouton cliqué continue à être `True`, créez une valeur dans `st.session_state` et utilisez le bouton pour fixer cette valeur à `True` dans un callback.  
  
```  
import streamlit as st  
  
if 'clicked' not in st.session_state:  
    st.session_state.clicked = False  
  
def click_button():  
    st.session_state.clicked = True  
  
st.button('Click me', on_click=click_button)  
  
if st.session_state.clicked:  
    # The message and nested widget will remain on the page  
    st.write('Button clicked!')  
    st.slider('Select a value')  
```  
  
Si vous voulez qu'un bouton fonctionne comme un interrupteur à bascule, envisagez d'utiliser [st.checkbox](https://docs.streamlit.io/library/api-reference/widgets/st.checkbox). Sinon, vous pouvez utiliser un bouton avec une fonction de rappel pour inverser une valeur booléenne sauvegardée dans `st.session_state`.  
  
Dans cet exemple, nous utilisons `st.button` pour activer et désactiver un autre widget. En affichant [`st.slider`](https://docs.streamlit.io/library/api-reference/widgets/st.slider) conditionnellement à une valeur dans `st.session_state`, l'utilisateur peut interagir avec le slider sans qu'il ne disparaisse.  
  
```  
import streamlit as st  
  
if 'button' not in st.session_state:  
    st.session_state.button = False  
  
def click_button():  
    st.session_state.button = not st.session_state.button  
  
st.button('Click me', on_click=click_button)  
  
if st.session_state.button:  
    # The message and nested widget will remain on the page  
    st.write('Button is on!')  
    st.slider('Select a value')  
else:  
    st.write('Button is off!')  
```  
  
Alternativement, vous pouvez utiliser la valeur de `st.session_state` sur le paramètre `disabled` du slider.  
  
```  
import streamlit as st  
  
if 'button' not in st.session_state:  
    st.session_state.button = False  
  
def click_button():  
    st.session_state.button = not st.session_state.button  
  
st.button('Click me', on_click=click_button)  
  
st.slider('Select a value', disabled=st.session_state.button)  
```  
  
Une autre alternative à l'imbrication du contenu dans un bouton est d'utiliser une valeur dans `st.session_state` qui désigne le "step" ou "stage" d'un processus. Dans cet exemple, nous avons quatre étapes dans notre script :  
  
0.  Avant que l'utilisateur ne commence.  
1.  L'utilisateur entre son nom.  
2.  L'utilisateur choisit une couleur.  
3.  L'utilisateur reçoit un message de remerciement.  
  
Un bouton au début fait avancer l'étape de 0 à 1, et un bouton à la fin réinitialise l'étape de 3 à 0. Les autres widgets utilisés dans les étapes 1 et 2 ont des rappels pour définir l'étape. Si vous avez un processus avec des étapes dépendantes et que vous voulez garder les étapes précédentes visibles, un tel rappel oblige l'utilisateur à retracer les étapes suivantes s'il modifie un widget antérieur.  
  
```  
import streamlit as st  
  
if 'stage' not in st.session_state:  
    st.session_state.stage = 0  
  
def set_state(i):  
    st.session_state.stage = i  
  
if st.session_state.stage == 0:  
    st.button('Begin', on_click=set_state, args=[1])  
  
if st.session_state.stage >= 1:  
    name = st.text_input('Name', on_change=set_state, args=[2])  
  
if st.session_state.stage >= 2:  
    st.write(f'Hello {name}!')  
    color = st.selectbox(  
        'Pick a Color',  
        [None, 'red', 'orange', 'green', 'blue', 'violet'],  
        on_change=set_state, args=[3]  
    )  
    if color is None:  
        set_state(2)  
  
if st.session_state.stage >= 3:  
    st.write(f':{color}[Thank you!]')  
    st.button('Start Over', on_click=set_state, args=[0])  
```  
  
If you modify `st.session_state` inside of a button, you must consider where that button is within the script.  
  
#### Un petit problème  
  
Dans cet exemple, nous accédons à `st.session_state.name` avant et après les boutons qui le modifient. Lorsqu'un bouton ("**Jane**" ou "**John**") est cliqué, le script est réexécuté. L'information affichée avant les boutons est en retard par rapport à l'information écrite après le bouton. Les données contenues dans `st.session_state` avant le bouton ne sont pas mises à jour. Lorsque le script exécute la fonction du bouton, c'est à ce moment que le code conditionnel de mise à jour de `st.session_state` crée le changement. Cette modification est donc répercutée après le bouton.  
  
```  
import streamlit as st  
import pandas as pd  
  
if 'name' not in st.session_state:  
    st.session_state['name'] = 'John Doe'  
  
st.header(st.session_state['name'])  
  
if st.button('Jane'):  
    st.session_state['name'] = 'Jane Doe'  
  
if st.button('John'):  
    st.session_state['name'] = 'John Doe'  
  
st.header(st.session_state['name'])  
```  
  
#### Logique utilisée dans un callback  
  
Les callbacks sont un moyen propre de modifier `st.session_state`. Les callbacks sont exécutés avant la ré-exécution du script, de sorte que la position du bouton par rapport à l'accès aux données n'est pas importante.  
  
```  
import streamlit as st  
import pandas as pd  
  
if 'name' not in st.session_state:  
    st.session_state['name'] = 'John Doe'  
  
def change_name(name):  
    st.session_state['name'] = name  
  
st.header(st.session_state['name'])  
  
st.button('Jane', on_click=change_name, args=['Jane Doe'])  
st.button('John', on_click=change_name, args=['John Doe'])  
  
st.header(st.session_state['name'])  
```  
  
#### Logique imbriquée dans un bouton avec une relance  
  
Bien que les callbacks soient souvent préférés pour éviter des réexécutions supplémentaires, notre premier exemple 'John Doe'/'Jane Doe' peut être modifié en ajoutant [`st.experimental_rerun`](https://docs.streamlit.io/library/api-reference/control-flow/st.experimental_rerun) à la place. Si vous avez besoin d'accéder aux données de `st.session_state` avant le bouton qui les modifie, vous pouvez inclure `st.experimental_rerun` pour réexécuter le script après que la modification ait été validée. Cela signifie que le script sera réexécuté deux fois lorsqu'un bouton est cliqué.  
  
```  
import streamlit as st  
import pandas as pd  
  
if 'name' not in st.session_state:  
    st.session_state['name'] = 'John Doe'  
  
st.header(st.session_state['name'])  
  
if st.button('Jane'):  
    st.session_state['name'] = 'Jane Doe'  
    st.experimental_rerun()  
  
if st.button('John'):  
    st.session_state['name'] = 'John Doe'  
    st.experimental_rerun()  
  
st.header(st.session_state['name'])  
```  
  
Lorsqu'un bouton est utilisé pour modifier ou réinitialiser un autre widget, il est identique aux exemples précédents pour modifier `st.session_state`. Cependant, une considération supplémentaire existe : vous ne pouvez pas modifier une paire clé-valeur dans `st.session_state` si le widget avec cette clé a déjà été rendu sur la page pour l'exécution du script en cours.  
  
Ne faites pas cela !  
  
```  
import streamlit as st  
  
st.text_input('Name', key='name')  
  
# These buttons will error because their nested code changes  
# a widget's state after that widget within the script.  
if st.button('Clear name'):  
    st.session_state.name = ''  
if st.button('Streamlit!'):  
    set_name('Streamlit')  
```  
  
#### Option 1 : Utiliser une clé pour le bouton et placer la logique avant le widget  
  
Si vous assignez une clé à un bouton, vous pouvez conditionner le code à l'état du bouton en utilisant sa valeur dans `st.session_state`. Cela signifie que la logique dépendant de votre bouton peut se trouver dans votre script avant ce bouton. Dans l'exemple suivant, nous utilisons la méthode `.get()` sur `st.session_state` parce que les clés des boutons n'existeront pas lorsque le script s'exécutera pour la première fois. La méthode `.get()` retournera `False` si elle ne trouve pas la clé. Sinon, elle retournera la valeur de la clé.  
  
```  
import streamlit as st  
  
# Use the get method since the keys won't be in session_state  
# on the first script run  
if st.session_state.get('clear'):  
    st.session_state['name'] = ''  
if st.session_state.get('streamlit'):  
    st.session_state['name'] = 'Streamlit'  
  
st.text_input('Name', key='name')  
  
st.button('Clear name', key='clear')  
st.button('Streamlit!', key='streamlit')  
```  
  
#### Option 2 : utiliser un système de rappel  
  
```  
import streamlit as st  
  
st.text_input('Name', key='name')  
  
def set_name(name):  
    st.session_state.name = name  
  
st.button('Clear name', on_click=set_name, args=[''])  
st.button('Streamlit!', on_click=set_name, args=['Streamlit'])  
```  
  
#### Option 3 : Utiliser des conteneurs  
  
En utilisant [`st.container`](https://docs.streamlit.io/library/api-reference/layout/st.container) vous pouvez faire apparaître les widgets dans des ordres différents dans votre script et dans la vue frontale (page web).  
  
```  
import streamlit as st  
  
begin = st.container()  
  
if st.button('Clear name'):  
    st.session_state.name = ''  
if st.button('Streamlit!'):  
    st.session_state.name = ('Streamlit')  
  
# The widget is second in logic, but first in display  
begin.text_input('Name', key='name')  
```  
  
Lorsque vous ajoutez dynamiquement des widgets à la page, assurez-vous d'utiliser un index pour garder les clés uniques et éviter une erreur `DuplicateWidgetID`. Dans cet exemple, nous définissons une fonction `display_input_row` qui rend une rangée de widgets. Cette fonction accepte un `index` comme paramètre. Les widgets rendus par `display_input_row` utilisent `index` dans leurs clés afin que `dispaly_input_row` puisse être exécuté plusieurs fois sur un seul script sans répéter les clés des widgets.  
  
```  
import streamlit as st  
  
def display_input_row(index):  
    left, middle, right = st.columns(3)  
    left.text_input('First', key=f'first_{index}')  
    middle.text_input('Middle', key=f'middle_{index}')  
    right.text_input('Last', key=f'last_{index}')  
  
if 'rows' not in st.session_state:  
    st.session_state['rows'] = 0  
  
def increase_rows():  
    st.session_state['rows'] += 1  
  
st.button('Add person', on_click=increase_rows)  
  
for i in range(st.session_state['rows']):  
    display_input_row(i)  
  
# Show the results  
st.subheader('People')  
for i in range(st.session_state['rows']):  
    st.write(  
        f'Person {i+1}:',  
        st.session_state[f'first_{i}'],  
        st.session_state[f'middle_{i}'],  
        st.session_state[f'last_{i}']  
    )  
```  
  
Lorsque vous avez des processus coûteux, configurez-les pour qu'ils s'exécutent lorsque vous cliquez sur un bouton et sauvegardez les résultats dans `st.session_state`. Cela vous permet de continuer à accéder aux résultats du processus sans le ré-exécuter inutilement. Ceci est particulièrement utile pour les processus qui sauvegardent sur le disque ou écrivent dans une base de données. Dans cet exemple, nous avons un `expensive_process` qui dépend de deux paramètres : `option` et `add`. Fonctionnellement, `add` change la sortie, mais `option` ne le fait pas - `option` est là pour fournir un paramètre  
  
```  
import streamlit as st  
import pandas as pd  
import time  
  
def expensive_process(option, add):  
    with st.spinner('Processing...'):  
        time.sleep(5)  
    df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'C':[7, 8, 9]}) + add  
    return (df, add)  
  
cols = st.columns(2)  
option = cols[0].selectbox('Select a number', options=['1', '2', '3'])  
add = cols[1].number_input('Add a number', min_value=0, max_value=10)  
  
if 'processed' not in st.session_state:  
    st.session_state.processed = {}  
  
# Process and save results  
if st.button('Process'):  
    result = expensive_process(option, add)  
    st.session_state.processed[option] = result  
  
if option in st.session_state.processed:  
    st.write(f'Option {option} processed with add {add}')  
    st.write(st.session_state.processed[option][0])  
```  
  
Les observateurs avisés penseront peut-être : "Cela ressemble un peu à la mise en cache". Nous ne sauvegardons que les résultats relatifs à un paramètre, mais le modèle pourrait facilement être étendu pour sauvegarder les résultats relatifs aux deux paramètres. Dans ce sens, oui, il y a des similitudes avec la mise en cache, mais aussi des différences importantes. Lorsque vous sauvegardez des résultats dans `st.session_state`, les résultats ne sont disponibles que pour l'utilisateur actuel dans sa session actuelle. Si vous utilisez [`st.cache_data`](https://docs.streamlit.io/library/api-reference/performance/st.cache_data) à la place, les résultats sont disponibles pour tous les utilisateurs à travers toutes les sessions. De plus, si vous souhaitez mettre à jour un résultat sauvegardé, vous devez effacer tous les résultats sauvegardés pour cette fonction.  
  
Voici quelques exemples simplifiés de la manière dont les boutons peuvent mal tourner. Soyez attentif à ces erreurs courantes.  
  
```  
import streamlit as st  
  
if st.button('Button 1'):  
    st.write('Button 1 was clicked')  
    if st.button('Button 2'):  
        # This will never be executed.  
        st.write('Button 2 was clicked')  
```  
  
```  
import streamlit as st  
  
if st.button('Sign up'):  
    name = st.text_input('Name')  
  
    if name:  
        # This will never be executed.  
        st.success(f'Welcome {name}')  
```  
  
```  
import streamlit as st  
import pandas as pd  
  
file = st.file_uploader("Upload a file", type="csv")  
  
if st.button('Get data'):  
    df = pd.read_csv(file)  
    # This display will go away with the user's next action.  
    st.write(df)  
  
if st.button('Save'):  
    # This will always error.  
    df.to_csv('data.csv')  
```  
  
## Formulaire qui s'efface quand on appui sur un bouton  
  
```  
  
if 'clicked' not in st.session_state:  
    st.session_state.clicked = False  
  
def click_button(prenom, nom, block):  
    st.session_state.clicked = True  
    block.write(f"Bienvenue {prenom} {nom}")  
  
prenom =""  
nom=""  
  
if not st.session_state.clicked:  
    prenom = st.text_area("Prénom", max_chars=25, placeholder="Pas de prénom", height=1, key="prenom")  
    st.write("hello world")  
    nom = st.text_area("Nom", max_chars=25, placeholder="Pas de nom", height=1, key="nom")  
  
    mail = st.text_area("Mail", max_chars=50, placeholder="Pas de mail", height=1, key="mail")  
    # if mail and( not "@" in mail or " " in mail):  
    #     st.write(":red[Le mail n'est pas valide !]")  
          
    today = datetime.datetime.now()  
    date_de_naissance = st.date_input(  
        "Date de naissance", max_value=datetime.date((today.year-18), 1, 1), min_value= datetime.date((today.year-100), 1, 1),  
        format="DD/MM/YYYY", value= datetime.date((today.year-30), 1, 1), key="date_naissance"  
    )  
  
    genre = st.selectbox("Genre", ("F","M"), help="Homme : H Femme : F", key="genre")  
    date_arrive = st.date_input(  
        "Date d'entrée dans l'entreprise", min_value= datetime.date((today.year-60), 1, 1),  
        format="DD/MM/YYYY", key="date_arrive"  
    )  
  
block = st.container()  
block.write("")  
  
if not st.session_state.clicked:  
    submitted = st.button("Envoyer", on_click=click_button, args=[prenom, nom, block])  
  
  
```