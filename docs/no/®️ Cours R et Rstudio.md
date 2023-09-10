---  
number headings: auto, first-level 2, max 6, contents %% toc %%, start-at 1, 1.1)  
aliases: []  
nature: cours  
tags:  
  - cours  
  - data  
  - dataviz  
  - formation  
share: true  
---  
  
carte mentale: [Carte mentale R.excalidraw](../../Carte%20mentale%20R.excalidraw.md#)  
  
> [!sommaire]-  
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
  
  
![780](../image/image%20-%20%C2%AE%EF%B8%8F%20Cours%20R%20et%20Rstudio-1.png#)  
  
  
Possibilité d'utiliser des quarto documents plutôt que des Rmarkdown:  
  
## 1) Initiation  
[Formation Tidyverse.qmd](Formation%20Tidyverse.qmd.md#) et [Formation_Tidyverse_CEFIM_PARTICIPANTS.html](Formation_Tidyverse_CEFIM_PARTICIPANTS.html.md#)  
  
### 1.1) Assignation d'une valeur à un objet  
vecteur : c()  
tableau: tibble()  
  
### 1.2) Raccourcis  
<ou Alt+pour en insérer une rapidement  
commenter rapidement : Ctrl+Shift+c  
  
### 1.3) Variables d'environnement  
dans environnement, liste puis en cocher certains pour nettoyer des variables  
  
  
### 1.4) Faire un graphique  
  
#### 1.4.1) Graphique simple  
plot() pour un basique  
ggplot(nom_tableau)+aes(x=nom_vecteur, y=nom_vecteur)+geom_point() pour un avec ggplot2, plus graphique (aes=estéthique)  
  
pour avoir des facteurs et donc des catégories numériques au lieu d'une échelle de couleur:  
as.factor(nom_vecteur)  
  
exemple:  
```r  
ggplot(genre_hauteur_date)+  
  aes(x=date,  
      y=hauteur,  
      colour= as.factor(genre))+  
  geom_point()  
```  
![517](../image/image%20-%20%C2%AE%EF%B8%8F%20Cours%20R%20et%20Rstudio-2.png#)  
  
#### 1.4.2) Diviser le graphique en sous-graphique  
```r  
ggplot(seq_intro4_dem1_stats)+  
  aes(x=date,  
      y=longueur_moy,  
      colour=traitement)+  
  geom_point()+  
  facet_grid(ordre~annee, scales = "free_x")  
```  
  
#### 1.4.3) Rajouter des barres d'erreurs (écart-type)  
avec geom_errorbar  
```r  
ggplot(seq_intro4_dem1_stats)+  
  aes(x=date,  
      y=longueur_moy,  
      colour=traitement)+  
  geom_point()+  
  geom_line()+  
  geom_errorbar(aes(ymax=longueur_moy+longueur_ect,  
                    ymin=longueur_moy-longueur_ect))+  
  facet_grid(ordre~annee, scales = "free_x")  
```  
![517](../image/image%20-%20%20Cours%20R%20et%20Rstudio-4.png#)  
#### 1.4.4) Modifier l'estéthique  
  
##### 1.4.4.1) type de ligne selon une variable:  
```r  
aes(date,longueur_moy,colour=traitement,linetype=traitement)  
```  
  
##### 1.4.4.2) changer l'échelle d'un axe:  
```r  
ggplot(seq_intro5_dem1_stats)+  
  aes(x=date,y=longueur_moy,colour=traitement,linetype=traitement)+  
  geom_point(size=1)+  
  geom_line()+  
  facet_grid(ordre~annee,scales="free_x") +  
  scale_y_continuous(breaks=seq(0, 125, 10))  
```  
  
##### 1.4.4.3) modifier le format de date:  
```r  
scale_x_date(date_labels = "%d/%m",  
               date_breaks = "4 weeks")  
```  
  
##### 1.4.4.4) appliquer les dates uniques du tableau:  
```r  
scale_x_date(breaks = unique(seq_intro5_dem1_stats$date), date_labels = "%d/%m")  
```  
  
##### 1.4.4.5) changer les couleurs:  
```r  
scale_color_manual(values=c("royalblue4", "salmon1", "#66cc33"))  
```  
  
##### 1.4.4.6) Changer la légende  
```r  
labs(y="Longueur moyenne (cm)")  
```  
  
##### 1.4.4.7) Mettre en forme un élément individuel (orientation et taille du texte d'un axe)  
```r  
theme(axis.text.x = element_text(size = 8, angle = 45, hjust = 1, vjust = 1, face="bold"))  
```  
  
##### 1.4.4.8) Changer position légende et couleur d'un texte de sous-graphique  
```r  
theme(axis.text.x = element_text(size = 8, angle = 45, hjust = 1, vjust = 1, face="bold"),  
        strip.text.y = element_text(colour = "purple"),  
        legend.position = c(0.3, 0.4))  
```  
  
#### 1.4.5) Graphique en camembert  
```r  
ggplot(seq_PLOT1_dem3)+  
  aes(x="",  
      y = appreciation_pourcent,  
      fill = appreciation)+  
  geom_col()+  
  coord_polar(theta = "y")+  
  theme_void()+  
  geom_text(aes(label = appreciation_pourcent),  
            position = position_stack(vjust = 0.5))  
```  
  
#### 1.4.6) Créer un thème personnalisé  
  
```r  
theme_sans_grilles<theme(panel.border = element_blank(),  
                           panel.grid.major = element_blank(),  
                           panel.grid.minor = element_blank(),  
                           panel.background = element_blank(),  
                           axis.line = element_line(colour = "black"),  
                           strip.background=element_rect(colour="grey",  
                                                         fill="white"))  
```  
  
pour l'utiliser:  
```r  
ggplot(seq_PLOT1_dem2)+  
  aes(country,pourcentage,fill=type_ENR)+  
  geom_col()+  
  coord_flip()+  
  theme_sans_grilles  
```  
  
#### 1.4.7) Rajouter du texte dans le graphique  
```r  
ggplot(manchot_label)+  
  aes(x=bill_length_mm,  
      y=flipper_length_mm,  
      colour=sex)+  
  geom_point()+  
  facet_grid(species~island~year)+  
  geom_label(aes(label=nb_manchots,  
                 x=40,  
                 y=220),  
             inherit.aes = FALSE)  
```  
  
#### 1.4.8) Encercler des points selon des conditions  
selon une variable:  
```r  
library(ggalt)  
  
ggplot(manchot_label)+  
  aes(x=bill_length_mm,  
      y=flipper_length_mm,  
      colour=sex)+  
  geom_point()+  
  geom_encircle(aes(colour=island))  
```  
  
selon un filtre:  
```r  
ggplot(manchot_label)+  
  aes(x=bill_length_mm,  
      y=flipper_length_mm,  
      colour=sex)+  
  geom_point()+  
  geom_encircle(data=penguins |> filter(bill_length_mm>55),  
                colour="salmon")  
```  
  
#### 1.4.9) Changer la taille des points selon une variable  
```r  
ggplot(manchot_label)+  
  aes(x=bill_length_mm,  
      y=flipper_length_mm,  
      colour=sex,  
      size=species)+  
  geom_point()+  
  facet_grid(~year)  
```  
  
#### 1.4.10) Assigner des couleurs à des groupes de valeurs continues  
```r  
ggplot(manchot_label)+  
  aes(x=bill_length_mm,  
      y=flipper_length_mm,  
      colour=cut_interval(x=flipper_length_mm,  
                          # n=5,  
                          length = 20),  
      size=species)+  
  geom_point()+  
  facet_grid(~year)+  
  labs(colour="classes",  
       size="espèce")  
```  
  
### 1.5) Faire un graphique interactif  
```r  
library(plotly)  
  
manchot_interactif <ggplot(manchot_label)+  
  aes(x=bill_length_mm,  
      y=flipper_length_mm,  
      colour=cut_interval(x=flipper_length_mm,  
                          # n=5,  
                          length = 20),  
      size=species)+  
  geom_point()+  
  facet_grid(~year)+  
  labs(colour="classes",  
       size="espèce")  
  
ggplotly(manchot_interactif)  
```  
  
### 1.6) Faire un graphique  
  
#### 1.6.1) Charger les coordonnées d'une carte  
```r  
carte_monde <map_data("world")  
```  
  
#### 1.6.2) Faire une carte simple  
```r  
ggplot(carte_monde)+  
  aes(x=long,  
      y=lat,  
      group=group)+  
  geom_polygon(colour="black",  
               fill="lightgray")  
```  
  
#### 1.6.3) Faire une carte d'Europe coloré et avec nom  
```r  
ggplot(europe)+  
  aes(x = long, y = lat) +  
  geom_polygon(aes( group = group, fill = region))+  
  geom_text(aes(label = region),  
            data = centroide,  
            size = 3,  
            hjust = 0.5)+  
  scale_fill_viridis_d()+  
  theme_void()+  
  theme(legend.position = "none")  
```  
  
#### 1.6.4) Faire une carte selon une variable en joignant 2 tables  
```r  
library(gapminder)  
  
gapminder <-gapminder  
world_map <map_data("world")  
  
# on fusionne le tableau contenant les données par pays avec le tableaux contenant les longitudes et latitudes par pays  
# attention, pour le full_join de bien avoir les mêmes variables de même type (facteur pour région et country)  
  
carte_vie <world_map |>   
  mutate(region=as_factor(region)) |>   
  full_join(gapminder,  
            by = c("region"="country"))  
  
# avec geom_polygon  
  
ggplot(carte_vie)+  
  aes(x = long,  
      y = lat,  
      group = group)+  
  geom_polygon(aes(fill=lifeExp))  
  
# avec geom_map  
  
ggplot(carte_vie)+  
  aes(map_id = region, fill = lifeExp)+  
  geom_map(map = carte_vie,  color = "black")+  
  expand_limits(x = carte_vie$long, y = carte_vie$lat)+  
  scale_fill_viridis_c(option = "C")  
```  
  
### 1.7) Exporter un graphique  
```r  
ggsave("Graphique_protentiel_moyen_cepage.png", width = 20, height = 20, units = "cm", bg = "transparent")  
```  
  
### 1.8) Exporter un tableau  
```r  
write_delim(x= vigne_stats, file = "Statistiques_vignes.csv", delim=";")  
```  
  
### 1.9) Changer le nom des facettes  
```r  
facet_grid(cepage~annee,  
             labeller = labeller(annee=label_both))  
```  
  
### 1.10) Modifier un tableau  
```r  
nom_tableau <- mutate(.data = nom_tableau, nom_vecteur=modification)  
```  
modification peut être as_factor(nom_colonne), dmy(nom_colonne)…  
  
Mais avant, création d'une copie du tableau incrémentale avec  
nom_tableau_consolide <- nom_tableau |> (aussi Ctrl+Shit+M, opérateur d'enchainement)  
  
exemple:  
```r  
genre_hauteur_date_consolide <genre_hauteur_date |>   
  mutate(genre=as.factor(genre)) |>   
  mutate(date=dmy(date)) |>   
  mutate(hauteur_metre=hauteur/100) |>   
  select(genre,date, hauteur_metre)  
```  
  
### 1.11) Graphique boxplot:  
```r  
insectes <InsectSprays  
  
insectes_unite <insectes |>  
  mutate(count_10=count+10) |>   
  select(count_10, spray)  
  
ggplot(insectes_unite)+  
  aes(x = spray,  
      y = count_10,  
      colour=spray)+  
  geom_boxplot()+  
  geom_point()  
```  
![517](../image/image%20-%20%20Cours%20R%20et%20Rstudio-3.png#)  
  
  
### 1.12) Charger un fichier csv  
  
il faut d'abord définir le dossier avec set working directory avec clic droit sur l'onglet  
puis on lit avec :  
```r  
seq_intro3_dem1 <read_delim(file = "Tableau/seq_intro3_dem1.csv", delim = ";")  
```  
  
De base, les virgules ne sont pas géré, il faut donc penser à rajouter:  
```r  
seq_intro4_dem1 <read_delim(file="Tableau/seq_intro4_dem1.csv", delim = ";", locale = locale(decimal_mark = ","))  
```  
  
  
  
### 1.13) Connaître les valeurs uniques d'une colonne  
```r  
seq_intro3_dem1 |> distinct(genre)  
```  
  
### 1.14) Modifier des colonnes à l'import d'un csv  
```r  
seq_intro3_dem1 <read_delim(file = "Tableau/seq_intro3_dem1.csv",  
                              delim = ";") |>   
  mutate(date=dmy(date))  
```  
  
### 1.15) Calculer en groupant des valeurs  
```r  
seq_intro3_dem1_stats <seq_intro3_dem1 |>   
  group_by(date, genre) |>   
  # mutate(hauteur_moy=mean(hauteur))  
  summarise(hauteur_moy=mean(hauteur))  
```  
  
faire fonctionner les calculs avec des NA:  
```r  
seq_intro4_dem1_stats <seq_intro4_dem1 |>   
  select(annee:ordre, -SF, -ligne) |>   
  # filter(bloc==1 | bloc==2)  
  filter(bloc!=3) |>   
  group_by(annee, date, traitement, ordre) |>   
  summarise(longueur_moy=mean(longueur, na.rm = TRUE))  
```  
  
### 1.16) Selectionner un ensemble de colonne sans toutes les retaper  
```r  
seq_intro4_dem1_stats <seq_intro4_dem1 |>   
  select(annee:ordre, -SF, -ligne)  
```  
  
### 1.17) Filtrer selon une condition  
```r  
seq_intro4_dem1_stats <seq_intro4_dem1 |>   
  select(annee:ordre, -SF, -ligne) |>   
  filter(bloc==1)  
```  
avec >, <, \==, !=, &, |  
  
  
### 1.18) Fusionner des tableaux  
  
#### 1.18.1) Selon un colonne commune  
```r  
seq6_join <left_join(seq_intro6_dem1,  
                       seq_intro6_dem2,  
                       by="arbre")  
```  
ou  
```r  
seq6_join_pipe <seq_intro6_dem1 |>   
  left_join(y = seq_intro6_dem2,  
            by="arbre")  
```  
  
#### 1.18.2) En les collant l'un à l'autre  
```r  
notes_participants <bind_rows(seq_TAB1_dem1, seq_TAB1_dem2)  
```  
  
  
### 1.19) Pivoter un tableau  
  
#### 1.19.1) En passant de horizontal à vertical  
```r  
escargot <seq_intro7_dem1 |>   
  pivot_longer(cols=2:7,  
               names_to="produit",  
               values_to="largeur")  
```  
  
#### 1.19.2) En passant de vertical à horizontal  
```r  
root_shoot <seq_TAB1_dem4 |>   
  pivot_wider(names_from = legende,  
              values_from = biomasse)  
```  
  
#### 1.19.3) Scinder le nom de colonnes dans un replace  
séparation par "\_", .value: premier morceau avant le sep  
```r  
notes_long <seq_TAB1_dem6 |>   
  pivot_longer(cols=6:8,  
               names_to = c(".value", "date"),  
               names_sep = "_")  
```  
  
  
  
### 1.20) Compléter des lignes manquantes (lignes manquantes pour certaines valeurs)  
```r  
horizon_complete <seq_TAB1_dem5 |>   
  complete(horizon, nesting(annee, traitement, arbre, orientation, distance))  
```  
  
### 1.21) Compléter les valeurs vides  
```r  
horizon_complete <seq_TAB1_dem5 |>   
  complete(horizon, nesting(annee, traitement, arbre, orientation, distance)) |>   
  replace_na(list(lg_totale=0))  
```  
  
  
  
### 1.22) Changer une partie des valeurs d'un tableau  
```r  
granulometrie_modif <granulometrie |>   
  mutate(Horizon=str_replace(Horizon, "oct", "10"))  
```  
  
  
## 2) Le RMarkdown  
  
### 2.1) Les options de chunk  
  
pour chaque chunk:  
```  
{r nom_de_la_cellule}  
```  
  
Dans la roue cranté à droite, on peut choisir la manière dont s'affiche le code et la sortie dans le document.  
  
Le premier chunk set permet de modifier ces options pour tous les chunks:  
```r  
 {r setup, include=FALSE}  
knitr::opts_chunk$set(  
	echo = TRUE,  
	message = FALSE,  
	warning = FALSE  
)  
   
```  
echo: montre le code  
fig.path="Figures/" pour configurer un dossier où vont se mettre les graphiques  
  
### 2.2) Insérer une image  
```  
![Figure 2: la structure du chunk de code](images/code_chunk.png)  
```  
  
### 2.3) Options dans les graphiques  
fig.cap= pour la légende, vecteur si plusieurs graphiques  
fig.height= pour la hauteur  
fig.width= pour la largeur  
  
### 2.4) Faire un tableau  
soit en markdown:  
  
| Col1 | Col2 | Col3 |  
| ---- | ---- | ---- |  
|      |      |      |  
|      |      |      |  
  
avec kabbleextra:  
```r  
InsectSprays |>   
  kable(caption = "Nombre de spray") |>   
  kable_styling(bootstrap_options = "striped")  
```  
  
pour un document word, avec flextable:  
```r  
  
```  
  
### 2.5) Afficher une image avec une fonction  
```r  
{r ALIGNEMENT, echo=FALSE, out.height="300px", out.width="500px"}  
  
knitr::include_graphics("images/code_chunk.png")  
```  
  
### 2.6) Afficher une valeur en couleur dans le tableau  
  
```r  
column_spec(column = 3,  
            color = ifelse(Orange$circumference<50,  
                           "blue",  
                           "black"))  
```  
  
  
### 2.7) Insérer du code dans le narratif  
  
Dans le texte, on peut insérer du code inline avec \` \`   , comment en markdown  
exemple:  
```  
il y a dans le tableau InsectSprays, les spray suivants : `r InsectSprays |> distinct(spray) |> pull()`.  
```  
  
### 2.8) Changer la couleur du texte  
`Roses are [pink]{style="color: pink;"}`  
  
### 2.9) Aligner un paragraphe  
```  
::: {align="right" style="color:blue"}  
On peut combiner l'éditeur visuel et le html pour des modifications ponctuelles dans le document, par exemple aligner un seul paragraphe et justifier à droite, en sélectionnant le paragraphe puis en ouvrant sous "Insert" le menu "Div…".  
:::  
```  
  
### 2.10) Appliquer des styles css  
On peut utiliser du css qu'on insére dans un chunk de css.  
exemple:  
```{css, echo=FALSE}  
  
h1.title {  
  font-size: 28px;  
  color: Yellow;  
}  
h1 {   
  font-size: 18px;  
  color: Pink;  
  font-weight:bold;  
  font-family: "Times New Roman", Times, serif  
}  
h2, h3 {  
  text-align: center;  
  color: Black;  
}  
  
body{   
      font-size: 12px;  
  }  
td {  /* Table => TITRE OPTIONNEL POUR MOI  */  
  font-size: 6px;  
}  
```  
  
### 2.11) Faire des onglets  
avec l'attribut .tabset dans le titre supérieur  
```  
## Utiliser les tabs {.tabset}  
  
Pour cela, insérer l'attribut de classe .tabset à la fin du titre de la section qui est un niveau au dessus des titres à convertir en tabs.  
  
### Résultats  
  
### Données  
```  
  
### 2.12) Arrêter le knit avant la fin  
avec un code de chunk avec :  
  
```r  
knitr::knit_exit()  
```  
  
### 2.13) YAML  
sensible aux indentations  
exemple:  
```  
---  
title: "9. Séquence Rmarkdown 1"  
author: "Oswaldo Forey"  
date: "`r format(Sys.time(), '%d %B %Y')`"  
output:  
  html_document:  
    toc: yes  
    toc_float: TRUE  
editor_options:  
  chunk_output_type: inline  
---  
```  
  
## 3) Shiny  
  
permet de faire des applications interactives de visualisation  
  
  
### 3.1) Logique de base  
on combine ui et server dans shiny  
  
exemple de base avec slider et graphique:  
```r  
ui <- fluidpage(  
	sliderInput(inputId="number",  
			label=choose a number,  
			min=1,  
			max=100,  
			value=1),  
	plotOutput(OutputId="hist")  
)  
server <- function(input, output) {  
	output$hist<-renderPlot({  
	hist(rnorm(input$number)  
	)})  
}  
  
  
shinyApp(ui=ui, server=server)  
```  
  
l'autocompletion shinyapp (snippet) permet d'avoir la structure de shiny simplement automatiquement  
  
### 3.2) Les fonctions utilisables  
  
#### 3.2.1) Les inputs  
  
- actionButton()  
- checkboxInput()  
- checkboxGroupInput()  
- dateInput()  
- dateRangeInput()  
- fileInput()  
- numericInput()  
- passwordInput()  
- radioButtons()  
- selectInput()  
- sliderInput()  
- textInput()  
  
![756](../image/image%20-%20%20Cours%20R%20et%20Rstudio%20-%20inputs%20fonctions.png#)  
#### 3.2.2) Les outputs fonctions  
  
- dataTableOutput() : an interactive table  
- htmlOutput () : raw HTML  
- imageOutput() : image  
- plotOutput() : plot  
- tableOutput() : table  
- textOutput() : text  
- uiOutput() : a Shiny Ul element  
- verbatimTextOutput() : text  
  
  
![756](../image/image%20-%20%20Cours%20R%20et%20Rstudio%20-%20outputs%20fonctions.png#)  
  
#### 3.2.3) Les reactives fonctions  
![756](../image/image%20-%20%20Cours%20R%20et%20Rstudio%20-%20reactive%20fonctions.png#)  
### 3.3) Les dispositions graphiques  
  
exemple:  
```r  
ui <fluidPage(  
  sliderInput(inputId = "NOMBRE",  
              label = div(style='width:500px;',  
                          div(style='float:left;', 'I totally disagree'),   
                          div(style='float:right;', 'I totaly aggree')),  
              # label = "Choisissez un nombre",  
              min = 1,  
              max = 10,  
              value = 1,  
              width = "500px"),  
  plotOutput(outputId = "GRAPHIQUE")  
)  
```  
  
### 3.4) Faire des panneaux (sidebar, mainbar…)  
```r  
ui <fluidPage(  
  sidebarLayout(sidebarPanel(radioButtons(inputId = "NOM",  
                                          label = "Choisissez un nom",  
                                          choices = unique(seq_SHINY3_dem1$nom))),  
                mainPanel(plotOutput(outputId = "GRAPHIQUE")))  
    
    
)  
  
server <function(input, output, session) {  
  output$GRAPHIQUE <renderPlot({  
    seq_SHINY3_dem1 |>   
      filter(nom==input$NOM) |>  
      mutate(mois=fct_inorder(as_factor(mois))) |>   
      ggplot()+  
      aes(date,montant,fill=mois)+  
      geom_col()  
  })  
    
}  
  
shinyApp(ui, server)  
```  
  
### 3.5) Créer un objet réactif qu'on utilise à plusieurs endroits dans une app  
```r  
somme_annee <reactive({  
    seq_SHINY3_dem1 |>  
      filter(annee == input$ANNEE) |>   
      filter(nom == input$NOM)|>  
      group_by(nom,annee,mois) |>  
      summarise(payment=sum(montant,na.rm=TRUE)) |>  
      ungroup() |>  
      arrange(nom,annee)  
  })  
    
  output$TAB_SUM_PAIE <renderTable({  
    somme_annee()  
  })  
```  
  
### 3.6) Faire un dashboard  
```r  
library(shinydashboard)  
  
ui <dashboardPage(skin="purple",  
                    dashboardHeader(title = "Rnorm Exemple"),  
                    dashboardSidebar(  
                      sidebarMenu(  
                          menuItem(tabName="TAB1_GRAPHIQUE",  
                                      text="graphique"),  
                          menuItem(tabName="TAB2_NOMBRE",  
                                      text="choix du nombre")  
                        )  
                    ),  
                      
                      
                    dashboardBody(  
                      tabItems(  
                        tabItem(tabName = "TAB1_GRAPHIQUE",  
                                box(title = "Selection du nombre",  
                                    sliderInput(  
                                      inputId = "NOMBRE",  
                                      label = "Choose a number",  
                                      min = 1,  
                                      max = 100,  
                                      value = 50  
                                    )),  
                                box(title = "Graphique",  
                                    plotOutput(outputId = "GRAPHIQUE_NOMBRE"))),  
                        tabItem(tabName = "TAB2_NOMBRE",  
                                box(title = "Nombre choisi",  
                                    valueBoxOutput(outputId = "NOMBRE_CHOISI"),  
                                    background = "blue"  
                                ))  
                      )  
                    )  
                      
)  
server <function(input, output, session) {  
    
    
    
  output$GRAPHIQUE_NOMBRE <renderPlot({  
    hist(rnorm(input$NOMBRE))  
  })  
    
    
    
  output$NOMBRE_CHOISI <renderValueBox({  
    valueBox(subtitle = " ",  
             value=input$NOMBRE,  
             width = 6)  
  })  
}  
  
shinyApp(ui, server)  
```  
  
## 4) Conversion en pdf  
  
pour afficher les graphiques et tableau à l'endroit du chunk:  
```r  
	{r AFFICHER TABLEAU, fig.pos='HOLD'}  
  
Orange |>   
  kable(caption="Bonjour") |>   
  kable_styling(latex_options = c("stripped", "HOLD_position"))  
  
 # page d'aide, taper kable dans l'aide et choisir kableExtra::awesome_table_in_pdf	  
   
  
```  
  
## 5) Nettoyage des données  
  
### 5.1) Remplacer des valeurs selon une condition  
```r  
mutate(ordre=if_else(condition=nom=="R1"|nom=="R2"|nom=="R3",  
                       true=1,  
                       false=2))  
```  
  
### 5.2) Appliquer un traitement selon des conditions  
```r  
mutate(legende_traitement = case_when(traitement==1~"Traitement 1",  
                                        traitement==2~"Traitement 2",  
                                        traitement==3~"Traitement 3"))  
```  
  
avec un else:  
```r  
mutate(type_branche=case_when(nom=="R1"~"branche maitresse",  
                                  nom=="R2"~"branchette",  
                                  .default="branche bonus"))  
```  
  
  
### 5.3) Déplacer des colonnes  
```r  
relocate(ordre,   
           .before = nom)  
```  
ou  
```r  
 relocate(ordre,   
           .before = 8)  
```  
  
### 5.4) Appliquer une opération à plusieurs colonnes  
```r  
mutate(across(.cols = bloc:traitement,  
                .fns = as_factor))  
```  
  
### 5.5) Filtrer des valeurs selon une liste de valeur  
```r  
filter(nom %in% c("R1", "R2", "R3"))  
```  
  
### 5.6) Filtrer selon une partie d'une chaîne de caractère  
  
```r  
filter(str_sub(ACCOUNT, 1, 1)==5)  
```  
ou  
```r  
seq_TAB3_dem1_str_detect<-seq_TAB3_dem1 |>   
  filter(str_detect(string=EMAIL,  
                     pattern="#"))  
```  
  
### 5.7) Extraire un mot d'une chaîne de caractère  
```r  
mutate(notateur=word(string=notateur,  
                       start = 1,  
                       sep = "\\…"))  
```  
  
### 5.8) extraire une chaine de caractère en fonction d'un motif à trouver  
```r  
seq12_str_extract <seq_TAB3_dem1 |>   
  mutate(com=str_extract(string=EMAIL,  
                         pattern = ".com"))  
```  
  
### 5.9) Remplacer par des NA  
```r  
mutate(couleur=str_replace(couleur,  
                             pattern="Unknown",  
                             replacement = NA_character_))  
```  
  
### 5.10) Résoudre des problèmes de chargement de données  
  
#### 5.10.1) Connaître l'encodage du fichier  
```r  
guess_encoding("nom-fichier")  
```  
  
#### 5.10.2) Enlever les x premières lignes  
``  
```r  
read_delim("nom-fichier", skip=x)  
```  
  
#### 5.10.3) Renommer toutes les colonnes en nom valides  
```r  
read_delim("nom-fichier", skip=x) |>  
	rename_with(.fn=make.names)  
```  
  
#### 5.10.4) Enlever les accents et caractères spéciaux des noms de colonnes  
```r  
rename_with(.fn=~stringi::stri_trans_general(.x,id = "Latin-ASCII"))  
```  
ou avec la syntaxe classique de création d'une fonction:  
```r  
rename_with(.fn=function(.x) {stringi::stri_trans_general(.x,id = "Latin-ASCII")})  
```  
  
#### 5.10.5) Créer une colonne répétant des valeurs d'une variable en complétant les lignes vides  
```r  
mutate(utilisation=rep(c("Approvisionnement","Emploi"),  
                         each=8),  
         .before=bilan.energetique)  
```  
  
#### 5.10.6) Enlever les espaces invisibles  
```r  
mutate(bilan.energetique=str_trim(bilan.energetique))  
```  
  
#### 5.10.7) Remplacer les chaînes de caractère par NA dans les colonnes numériques  
```r  
mutate(across(c(charbon,gaz,electricite,chaleur.vendue),  
                ~parse_number(.x,locale=locale(decimal_mark = ","))))  
```  
  
## 6) Sauvegarder un tableau en un fichier rdata  
```r  
save(seq_TAB6_dem1, file = "Tableau/seq_TAB6_dem1_nettoye.rdata")  
```  
  
## 7) Charger un fichier Rdata  
  
```r  
tableau <- load(fichier.rdata)  
```  
  
## 8) Compter un nombre par facteur  
```r  
seq_TAB4_dem1 |>   
  pull(cepage) |>   
  fct_count()  
ou  
fct_count(seq_TAB4_dem1$cepage)  
```  
  
## 9) Compter le nombre de variantes d'un facteur  
```r  
seq_TAB4_dem1 |>   
  pull(cepage) |>   
  n_distinct()  
ou  
n_distinct(seq_TAB4_dem1$cepage)  
```  
  
### 9.1) Réunir les variantes d'un facteur en quelques unes  
```r  
seq_TAB4_dem2 <read_delim("Tableau/seq_TAB4_dem2.csv") |>   
  mutate(niveau=fct_collapse(.f=niveau,  
                             debutant=c("Débutant", "oui", "débutant", "oui débutant"),  
                             other_level = "non debutant"))  
```  
  
### 9.2) Rajouter des variantes de facteur qu'il manque  
```r  
seq_TAB4_dem4_expand <seq_TAB4_dem4 |>   
  mutate(appreciation=fct_expand(f=appreciation,  
                                 "peu satisfait", "pas satisfait")) |>   
  complete(appreciation,  
           fill = list(appreciation_pourcent=0,  
                       n=0))  
```  
  
## 10) Ajouter un identifiant d'individu  
```r  
seq_TAB5_dem2<-read_delim("Tableau/seq_TAB5_dem2.csv") |>   
  rowid_to_column(var="Observation")  
```  
et par groupe:  
```r  
seq_TAB5_dem2<-read_delim("Tableau/seq_TAB5_dem2.csv") |>   
  group_by(client, date) |>   
  mutate(session=cur_group_id())  
```  
  
  
  
## 11) Gérer des doublons contradictoires  
```r  
doublons_contradictoires <vrai_et_faux |>   
  group_by(sujet) |>   
  filter(all(c("M","F")%in%genre))  
```  
  
## 12) Déploiement d'une application Rshiny  
avec shinyapp: [shinyapps.io](https://www.shinyapps.io/admin/#/dashboard)  
première application: [Analyse des connectés (shinyapps.io)](https://melodyduplaix.shinyapps.io/First_app/)                                                                            <iframe src="https://melodyduplaix.shinyapps.io/First_app/" allow="fullscreen" allowfullscreen="" style="height: 100%; width: 100%; aspect-ratio: 16 / 9;"></iframe>  
  
## 13) Déploiement d'un site internet avec quarto  
  
avec quarto: [Quarto Pub](https://quartopub.com/)  
  
### 13.1) Configuration des chunks  
```r  
#| echo: FALSE  
```  
en première ligne du chunk pour ne pas afficher le code  
  
### 13.2) Créer une page avec le contenu de plusieurs pages  
page parent:  
```r  
---  
title: "Contenu multiple"  
listing:   
  contents:  
    - "multiple1.qmd"  
    - "multiple2.qmd"  
  type: default  
  sort: FALSE  
---  
```  
  
page enfant:  
```r  
---  
title: "page 2"  
image: "tidyverse_image.PNG"  
categories: [package, R]  
---  
  
Ceci est la deuxième page  
  
```  
  
## 14) Flexdashboard  
  
On créé un R Markdown avec le template flexdashobard  
Cela permet d'avoir un joli dashboard sans galérer, ou les titres H2 définissent les colonnes.  
  
## 15) TP  
  
mon site internet lié à l'application et aux documents récap: [Analyse TP - Analyse de la population, de la production de nourriture, et de la consommation et production d’énergie (quarto.pub)](https://melody-duplaix.quarto.pub/analyse-tp/)  
  
## 16) Carte mentale  
![Carte mentale R.excalidraw.svg](../image/Carte%20mentale%20R.excalidraw.svg#)  
  
## 17) Flashcards  
  
  
---  
%%  
parent:: [Cefim note principale](../../CEFIM%20note%20principale.md#)  
image:: [image - ®️ Cours R et Rstudio-1](../image/image%20-%20%C2%AE%EF%B8%8F%20Cours%20R%20et%20Rstudio-1.png#), [image - ®️ Cours R et Rstudio-2.png](../image/image%20-%20%C2%AE%EF%B8%8F%20Cours%20R%20et%20Rstudio-2.png#), [image -  Cours R et Rstudio-3.png](../image/image%20-%20%20Cours%20R%20et%20Rstudio-3.png#), [image -  Cours R et Rstudio-4.png](../image/image%20-%20%20Cours%20R%20et%20Rstudio-4.png#)  
exemple:: [Formation Tidyverse.qmd](Formation%20Tidyverse.qmd.md#), [Formation_Tidyverse_CEFIM_PARTICIPANTS.html](Formation_Tidyverse_CEFIM_PARTICIPANTS.html.md#)  
enfant:: [Carte mentale R.excalidraw](../../Carte%20mentale%20R.excalidraw.md#)  
7%%