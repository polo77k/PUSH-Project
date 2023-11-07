# PUSH — Puzzle Shell

Une représentation ludique de l’interpréteur de commandes UNIX !

### Présentation

PUSH (PUzzle SHell) est un projet visant à rendre l’apprentissage des scripts UNIX plus ludique et visuel.  
Au lieu d’écrire des lignes de commande dans un terminal, l’utilisateur assemble des pièces de puzzle, représentant chacune un élément clé du shell (processus, tube, redirection, etc.).

Chaque pièce s’imbrique logiquement avec les autres pour construire une commande complète, qui peut ensuite être exécutée directement depuis l’interface graphique.

![Présentation PUSH](https://github.com/user-attachments/assets/f05542fa-a439-41fb-be66-f4500fb385e0)

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

## Technologies utilisées

* Langage : C++
* Bibliothèques : OpenGL, GLEW, GLUT, GLM
* Environnement de dev : Visual Studio 2022 / Ubuntu (WSL)
* Gestion de projet : Git & GitHub
* Build system : CMake

## Installation (Linux / WSL recommandé)

1️⃣ Installer les dépendances :
```
sudo apt update
sudo apt install build-essential cmake git
sudo apt install libgl1-mesa-dev libglew-dev freeglut3-dev libglm-dev
sudo apt install libx11-dev libxi-dev libxmu-dev libxrandr-dev
```

2️⃣ Cloner le dépôt :
```
git clone https://github.com/polo77k/PUSH-Project
cd PUSH
```

3️⃣ Compiler le projet :
```
mkdir build
cd build
cmake ..
make
```

4️⃣ Lancer le programme
```
./PUSH/PUSH
```

## Fonctionnement interne
### Création des pièces

Chaque pièce du puzzle correspond à un élément du langage UNIX :
* Processus : une commande (ex. ls, grep, cat...)
* Tube : relie deux processus (|)
* Redirection Entrée (<)
* Redirection Sortie (>)
* Redirection Erreur (2>)

Les pièces sont dessinées en 2D via OpenGL, à partir d’un ensemble de triangles.  
Chaque pièce possède :
* des coordonnées centrales (x0, y0)
* un ensemble de sommets définissant sa forme
* des booléens d’entrée/sortie (pour savoir si elle peut se connecter à d’autres)

Les formes sont stockées dans des structures héritant d’une classe de base Piece.

### Interaction utilisateur — Drag & Drop

Le déplacement des pièces se fait à la souris :
* Lors d’un clic gauche, si le curseur se trouve sur une pièce, celle-ci devient “active”.
* Tant que le bouton est maintenu, la pièce suit les coordonnées du curseur.
* Une conversion entre les coordonnées écran (pixels) et le repère OpenGL (-1 à 1) est effectuée :
```
float vX = (2 * (float)x / glutGet(GLUT_SCREEN_WIDTH)) - 1;
float vY = -((2 * (float)y / glutGet(GLUT_SCREEN_HEIGHT)) - 1);
```

Les mouvements sont limités à la zone de jeu, afin d’éviter que les pièces ne sortent de l’écran.

### Assemblage du puzzle

L’assemblage est géré par la fonction avengersPuzzle(), qui :
* détecte les collisions entre pièces,
* vérifie leur compatibilité logique (par exemple, un Tube ne peut s’attacher qu’entre deux Processus),
* et les imbrique si les conditions sont remplies.

Lorsque deux pièces s’assemblent, leur position se “verrouille” pour symboliser la connexion.

### Génération et exécution des commandes

Une fois les pièces assemblées :
* La fonction writingCommand() parcourt les pièces pour générer la commande finale.
* Exemple :
```
[Processus: ls] — [Tube] — [Processus: grep .cpp]
```

devient :
```
ls | grep .cpp
```
* Lors de la validation (touche Execute), la commande est envoyée à l’interpréteur Linux via WSL.
* Les résultats s’affichent dans la zone de sortie standard ou sortie d’erreur.

* Migration vers GLUT

Initialement développé avec GLFW, le projet a ensuite migré vers GLUT pour intégrer GLUI, permettant la gestion de champs de texte et d’interactions plus avancées (par exemple : saisir une commande directement dans une pièce).

Cette migration a aussi simplifié la boucle d’exécution, GLUT gérant automatiquement les callbacks (clavier, souris, rafraîchissement…).

## Bilan et apprentissages

Le projet PUSH a permis :
* d’explorer en profondeur OpenGL et ses bibliothèques,
* de comprendre la logique interne d’un interpréteur UNIX,
* et de développer un outil à la fois pédagogique et fonctionnel.

Ce travail a aussi consolidé les compétences en C++, en travail collaboratif (GitHub), et en gestion de projet logiciel.