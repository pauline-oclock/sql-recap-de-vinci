# MCD (Méthode Merise)

## Structure MCD - Entités

- Carrés ou rectangles qui vont représenter des éléments concrets 
- Chaque entité représente un élément qui peut être individualisé
- Le nom de l'entité est au singulier

## Structure MCD - Propriétés

- Comme pour les objets, propriétés qui identifient l'entité

## Structure MCD - Association

- Ronds ou ovales contenant un VERBE à l'infinitif
- Font la liaison entre deux associations (ou plus mais on ne verra pas ce cas en cours)

## Structure MCD - Cardinalités

- Les cardinalités vont nous donner la logique de lecture du MCD

- Traduction des cardinalités:
  - 0,1: Aucun ou un seul
  - 0,n: Aucun ou plusieurs
  - 1,1: Un et un seul
  - 1,n: Un ou plusieurs
  - n,n: Plusieurs
- Cardinalités IMPOSSIBLES ET FAUSSES:
  - n,0
  - n,1
  - 1,0
  - 0,0

- On lit les cardinalités en partant de l'entité la plus proche de la cardinalité qu'on est en train de lire pour aller vers la plus éloignée
- Exemple :
  - CHIEN --1,1-- manger --1,n-- TYPE_CROQUETTE
  - Se lit:
    - Un chien peut manger un et un seul type de croquettes
    - Un type de croquettes peut être mangé par un ou plusieurs chiens

Une voiture appartient à une seule personne et une personne peut avoir aucune ou plusieurs voitures
[VOITURE]_1.1__(appartenir)__0.n_[PERSONNE]

Un castor peut avoir construit 0 ou plusieurs barrages naturels et un barrage est construit par un ou plusieurs castors
[CASTOR]_0.n__(construire)__1.n_[BARRAGE_NATUREL]

- Proposition d'exemple de Kévin
  - Une commande est passée par une et une seule personne
  - Un personne peut avoir passé aucune ou plusieurs commandes
  - Une personne peut être domiciliée à une ou plusieurs adresses
  - Une adresse peut domicilier aucune ou plusieurs personnes
[commande]_1,1_(passer)_0.n_[personne]_1.n_(domicilier)_0.n_[adresse]_1.1_(situer)_0.n_[ville]