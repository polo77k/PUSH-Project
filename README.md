# PUSH

Pour compiler le projet:
mkdir build
cd build
cmake ..
make
./PUSH/PUSH
"# PUSH-Project" 


# PUSH — Puzzle Shell

Une représentation ludique de l’interpréteur de commandes UNIX !

### Présentation

PUSH (PUzzle SHell) est un projet visant à rendre l’apprentissage des scripts UNIX plus ludique et visuel.  
Au lieu d’écrire des lignes de commande dans un terminal, l’utilisateur assemble des pièces de puzzle, représentant chacune un élément clé du shell (processus, tube, redirection, etc.).

Chaque pièce s’imbrique logiquement avec les autres pour construire une commande complète, qui peut ensuite être exécutée directement depuis l’interface graphique.

### Objectif

L’objectif de PUSH est de :
* Simplifier la compréhension de l’interpréteur UNIX.
* Visualiser les relations entre les commandes, les processus et les redirections.
* Proposer un environnement graphique interactif et éducatif.

### Interface

L’application se compose de plusieurs zones :
* Zone des pièces : liste les éléments disponibles (processus, tube, redirection…).
* Aire de jeu : permet d’assembler les pièces comme un puzzle.
* Zone de texte : affiche la commande correspondante.
* Sorties standard et erreur : affichent le résultat de la commande exécutée.

Chaque pièce peut être déplacée, supprimée, modifiée, et reliée à d’autres.

![Image](https://github.com/user-attachments/assets/f05542fa-a439-41fb-be66-f4500fb385e0)