---  
aliases:  
  - Power BI  
  - Microsoft  
nature: cours  
tags:  
  - cours  
share: true  
---  
  
  
*souvent des nouveautés sur power BI, regarder souvent les nouveautées*  
  
> [!info]- [cours pdf](./image/Power%20Plateform%20_%20tutoriel.pdf#)  
> ![cours pdf](./image/Power%20Plateform%20_%20tutoriel.pdf#)  
  
> [!info]- [annotations](../Annotations%20for%20Power%20Plateform%20_%20tutoriel.md#)  
> ![annotations](../Annotations%20for%20Power%20Plateform%20_%20tutoriel.md#)  
  
## Composants d'un tableau de bord  
  
- titre  
- petite explication  
	-  avec les sources  
- possible menu pour la navigation  
- filtres dans un ordre logique  
  
## Intégration d'un fichier dans Power BI  
  
Si fichier XML mal structuré, supprimer sous VSCode la première ligne (<VERSION_FLUX>3.0</VERSION_FLUX>), ou le développer sous power query  
  
- Les transformations sur power query ne sont gardé qu'en mémoire et non en stockage  
- Utiliser affichage > éditeur avancé pour avoir le code de toutes les modifications faites  
- Afficher des statistiques dans affichage pour l'audit des données  
- on renomme les étapes  
- les traitements se font au niveau d'un échantillon de données  
- Un pilote (ODBC qui est un ETL) permet ensuite de l'appliquer sur tout le jeu de données au moment de l'appliquer  
  
Si fichier XML ou json :  
<span style="background:#fff88f"><font color="#ff0000">faire charger plus quand on déploit une colonne</font></span>  
