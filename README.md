## I- Problématique

Selon le site Wikipédia : "Le but du problème des huit dames est de placer huit dames d'un jeu d'échecs sur un échiquier de 8 × 8 cases sans que les dames ne puissent se menacer mutuellement, conformément aux règles du jeu d'échecs (la couleur des pièces étant ignorée). Par conséquent, deux dames ne devraient jamais partager la même rangée, colonne, ou diagonale. Ce problème appartient au domaine des problèmes mathématiques et non à celui de la composition échiquéenne."

## https://fr.wikipedia.org/wiki/Probl%C3%A8me_des_huit_dames

Ce problème se généralise à un échiquier fictif de taille n×n
 où la question devient : quel est le nom­bre maximal de reines que l'on peut placer sur cet échiquier ?
 Si le maximun est atteint, l y'a nécessairement une seule reine sur chaque ligne et une seule reine sur chaque colonne.
 Ce dernier résultat suggère une stratégie pour trouver une solution. Elle consiste à placer la première reine sur la première case libre de la première ligne, éliminer les cases désormais interdites sur l'échiquier et recommencer la même opération pour les lignes suivantes. S'il n'est impossible de placer la (k+1)-ème reine parce que toutes les cases de la (k+1)-ème ligne sont interdites, il faut revenir en arrière et déplacer la k -ème reine sur la prochaine case libre, si elle existe, et si la situation ne se débloque pas, on remonte à la ligne précédente et ainsi de suite. C'est probablement la stratégie que le lecteur a appliquée pour vérifier les possibilités.
 Cette technique classique est appelée backtracking en informatique.
C'est un procédé de résolution qui est particulièrement adapté pour ce type de problèmes. Cette technique classique est appelée **backtracking** en informatique et consiste à visiter l'ensemble des nœuds de l'arbre en partant de la racine et en choisissant de prendre systématiquement le chemin le plus à gauche qui n'a pas encore été suivi.

## II-Description de l'algorithme 

La solution du problème est codée sous la forme d'un tableau queens-row
 de taille n
 qui représente le n-uplet solution, c'est-à-dire que queens_row[i]
 est la colonne où il faut placer la i-ème reine.

L'algorithme EstLibre teste si la case à la ligne ligne et à la colonne colonne n'est pas menacée par les reines précédemment placées. Il n'est pas nécessaire de disposer d'une matrice booléenne pour savoir quelles sont les cases menacées ou non au fur et mesure de l'évolution de l'algorithme, les positions des reines sur les lignes qui précèdent suffisent et cette information est dans la table queens_rew. La vérification se fait en observant qu'aucune reine précédente n'est placée sur la même ligne, sur la même colonne ou les mêmes diagonales.

# Exemple:

Algo:EstLibre(queens-rew,ligne,colonne):booléen
DONNÉES
   ligne,colonne: entiers
   queens_rew[1,n]: tableau d'entiers
VARIABLES
   l,c: entiers
   ok: booléen
DEBUT
   ok ← VRAI
   l ← 1
   TQ (l ≤ ligne) FAIRE
      c ← queens_rew[l]
      ok ← ok ET (|ligne - l| ≠ |colonne - c|) ET (colonne ≠ c)
      l ← l + 1            
   FTQ
   RETOURNER ok
FIN

L'algorithme PlacerReine est chargé de placer les reines les unes après les autres en parcourant implicitement l'arbre de décision. l'algorithme ne s'arrête pas dès que les n reines sont placées mais poursuit son investigation dans l'arbre jusqu'au bout. Les n
 alternatives de placement d'une reine sur une ligne se concrétisent dans l'algorithme par une boucle suivie d'un test pour vérifier que la case candidate n'est pas menacée. Le premier appel de l'algorithme se fait avec la valeur 1.

L'algorithme Traiter n'est pas défini, il peut s'agir de l'affichage de la solution queens_rew, ou du rangement de queens_rew
 dans une liste des solutions, ou tout autre traitement.


Algo: PlacerReine(ligne)
DONNÉES
   ligne: entier
VARIABLES GLOBALES
   n: entier
   T: tableau de taille n
VARIABLES
   colonne: entier
DEBUT
   SI (ligne > n) ALORS
      Traiter(T)
   SINON
      colonne ← 1      
      TQ (colonne ≤ n) FAIRE
         SI EstLibre(T,ligne,colonne) ALORS
	    T[ligne] ← colonne
	    PlacerReine(ligne + 1)
	    T[ligne] ← 0
         FSI
         colonne ← colonne + 1
      FTQ					 
   FSI
FIN


