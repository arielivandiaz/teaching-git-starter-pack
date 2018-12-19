#SSH vs HTTP
Si usas HTTP por consola, te va a pedir usuario y contraseña o contraseña cada vez que realizas un pull/push
Si usas SSH, tus credenciales quedan guardadas en la PC y no necesitas loguearte para realziar acciones, pero para ello necesitas tener una key SSH en la PC/Servidor vinculada con la cuenta de github.

>En Windows Descargar git bash : [https://git-scm.com/](https://git-scm.com/)

## HTTP / SSH
Para usar git bash primero hay que configurar el usuario (probablemente si usaron github desktop esto no es necesario)

Ejecutar en el terminal: 
```
> git config --global user.email "you@email.com" 
> git config --global user.name "Your Name"
```

### HTTP

Configurado el usuario cada vez que realicemos un cambio y lo intentemos subir al servidor de git nos va a pedir la contraseña.

### SSH

Para que no nos pida las creedenciales cada vez que queremos subir un cambio tenemos que tener una llave SSH.

Primero creamos la llame SSH: [Generating a new SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

Despues agregamos la llave a nuestra cuenta de Github: [Adding a new SSH key to github](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)


Ya podemos hacer pull/push sin necesidad de autenticarse.


[Acerca sobre SSH](https://help.github.com/articles/about-ssh/)
