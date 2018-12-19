

# GIT Lessons
EXTRAS:

[Fundamental commands for git bash](https://gist.github.com/arielivandiaz/b1d114e44aaa9086d21995ce2fcd3268)

[How to make a save all changes and commit on a single line.  (Linux / Git bash)](https://gist.github.com/arielivandiaz/9eeb8e1537c0bdc64ed2d9656dc28612)

## Primeros Pasos

### Modificar los parametros 

1. Modificar ~/.gitconfig

En este archivo se pueden excluir los archivos, carpetas y tipos de archivos que no 
se quieren incluir en el repositorio. 

### Crear un repositorio local

1. Crear una carpeta con el nombre que queremos que tenga el repostorio.

`mkdir my_repo`

2. Inicializar un nuevo repositorio git dentro de la carpeta.

`cd nom_dossier`

` git init `

### Creando un codigo de ejemplo

1. Creamos un archivo python

nano hello.py

```
#! /usr/bin/env python3

print("Hello World !")
``` 

2. Hacer el fichero ejecutable.

`chmod +x hello.py`

3. Testear la ejecución del archivo.

`./hello.py`, la salida obtenida será : `Hello World ! `

### Guardar las modificaciones

#### Creando nuestro primer commit
1. Ver las modificaciones realizadas.

`git status`

2. Agregar el archivo 'hello.py'al repositorio.

`git add hello.py` 

3. Volvemos a ver las modificaciones al repositorio.

`git status`

4. Antes de realizar el commit es necesario identificarse globalmente en git local para registrar en el repositorio quien realizó los cambios.


* * *

*** Please tell me who you are.
Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.
* * *


5. Creamos el commit.

`git commit -m "My first commit !"`

6. Si observamos las modifiacioens ahora veremos que todo fue salvado y no hay nada 
pendiente.

`git status`

7. Podemos ver el historial de la siguiente forma.

`git log` (alt: `git log --oneline`)


 
#### Cometiendo el primer error

1. Generaremos un error en el archivo python.

```
#! /usr/bin/env python3

print("Hello World
```

2. Ejecutamos el archivo.

`./hello.py`

Se obtiene la salida:

```
  File "./hello.py", line 3
    print("Hello World !
                       ^
SyntaxError: EOL while scanning string literal
```

#### Recuperar el estado anterior

1. Ver las modificaciones realizadas.

`git status`

2. Eliminar las modificaciones.

`git checkout -- hello.py`


3. Ver las modificaciones realizadas

`git status`

4. Ejecutar el archivo de nuevo

`./hello.py` Salida obtenida : `Hello World !`

5. Revisar el archivo.

`cat hello.py`

### Repasando lo anterior

#### Creando un segundo commit
1. Modificar el archivo python

Remplazar `print("Hello World")` por

`print("Hello, my name is PUT\_YOUR\_NAME\_HERE")`

2. Ver las modifiaciones

`git status`

3. Agregar el archivo.

`git add hello.py`

4. Crear el nuevo commit

`git commit -m "My presentation"`

5. Ver el historial

`git log`


#### Ver la diferencia entre los commits

1. Ver el hash identificatorio del primer commit

`git log --oneline`

2. Ver la diferencia

`git diff HASH\_PRIMER\_COMMIT`

#### Revenir à l'avant-dernier commit

1. Voir ce que contient l'avant dernier commit

`git show HEAD^1`

2. Reset (soft)

`git reset HEAD^1`

3. Ver las modificaciones realizadas

`git status`

4. Modificar el archivo en python de la siguiente forma

Original:
```
name = "PUT\_YOUR\_NAME\_HERE"
print("Hello, my name is", name,"and you ?")
```

Modificado:
```
name = "PUT\_YOUR\_NAME\_HERE"
print("Hello, my name is", name,". I need to go now, bye !")
```

5. Agregar las modificaciones

`git add hello.py`

6. Commitear

`git commit -m "Je dois partir"`

7. Ver las modificaciones

`gitk`

## Travail à plusieurs

### Mettre son code en ligne

1. Créer un compte GitHub

2. Créer un répertoire GitHub

3. Récupérez l'URL

4. Rajoutez le remote 

`git remote add origin PUT\_URL\_HERE`

5. Voir si tout s'est bien déroulé

`git remote -v`

6. Envoyer son code sur le remote

`git push origin master`

### Récupérez le projet de quelqu'un d'autre

1. Aller dans un autre dossier qui n'est pas un répertoire git

Par exemple : `cd ..`

2. Cloner le repository

`git clone URL local_path_new_folder`

3. Executer le fichier

`./hello.py`

### Ajouter des modifications

1. Player one : modifier le code

```
#! /usr/bin/env python3

name = "..."
print("Hello, my name is", name,". I need to go now, bye !")
print("Oups no, this is not my name")
```

2. Voir les modifications apportées

`git status`

2. Ajouter le fichier

`git add hello.py`

3. Commiter le fichier

`git commit -m "Not my name"`

4. Envoyer les modifications à tout le monde

`git push origin master`

### Récupérer des modifications

1. Player two : récupérer le code

`git pull origin master`

2. Executer le fichier

`./hello.py`

### Coder à plusieurs : mise en pratique d'un conflit

1. Player two : Modification du fichier

Rajouter la ligne : `print("I am the player two")`

2. Player one : Modification du fichier

Rajouter la ligne : `print("I am the player one")`

3. Player one : Envoie ses modifications

`git status`
`git add hello.py`
`git commit -m "Je suis le player one"`
`git push origin master`

4. Player two : Envoie ses modifications

`git status`
`git add hello.py`
`git commit -m "Je suis le player two"`
`git push origin master`

###  Player two : résoudre un conflit

5. Récupération des modifications

`git pull`

6. Voir ce qu'il se passe

`git status`

7. Voir le détail des erreurs

`git diff`

8. Correction des erreurs

Supprimer tout ce qui est entre `<<<< HEAD et >>>>`, sauf `print("I am the player two")`

9. Voir les modifications apportées

`git status`

10. Ajouter les modifications

`git add hello.py`
`git commit` : Sauvegarder le fichier qui va s'ouvrir (Vim : tapez `:wq`)

11. Voir la modification de l'historique

`gitk`

11. Envoyer les modifications

`git push`

### Player one : observer la résolution d'un conflit

1. Récupérer les dernières modifications

`git pull`

2. Voir ce qu'il s'est passé

`gitk`

3. Executer le fichier 

`hello.py`

*Teacher : explain how systems like GitHub's Pull Requests could prevent this.*

## Organiser son développement : les branches

### Player one (ou le créateur du répo) : Sécurisation de la branche master

*Teacher : show him*

### Player two : création d'un fichier (Peut se faire en // de partie suivante)

1. Toujours vérifier les dernières modifications

`git pull origin master`

2. Voir les différentes branches disponibles

`git branch`

3. Créer une nouvelle branche et s'y déplacer 

`git checkout -b branche_of_two`

4. Voir les différentes branches

`git branch`

4. Créer le fichier `main.py`

```
#! /usr/bin/env python3

import one

if __name__ == "__main__":
	one.hello_world()	
```

5. Ajouter le fichier main.py

`git add main.py`

6. Rebasculer sur master

`git checkout master`

7. Voir que le fichier nous a suivit

`git status`

8. Rebasculer sur la branche

`git checkout branche_of_two`

9. Committer le fichier

`git commit -m "Add the main file"`

10. Voir les modifications

`git log --oneline`

11. Envoyer les modifications

`git push`

12. Retourner sur master

`git checkout master`

13. Récupérer la dernière version

`git pull origin master`

14. Voir les fichiers présents sur master

`ls`

### Player one : Mêmes étapes

Changements :
* "main.py" => "one.py"

```
#! /usr/bin/env python3

def hello_world():
    print("Hello world ! We are player two and one !")
```

* branche\_of\_two => branche\_of\_one

* Message du commit =>  "Add the hello\_world feature"

### Faire le merge des deux

1. *Teacher : show how to create pull requests (with the rebase button obviously)*

2. Récupérer les dernières modifications

`git checkout master`
`git pull origin master`

4. Voir l'historique

`gitk`

5. Executer le fichier

`./hello.py`
