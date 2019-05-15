# Guia para la configuración del entorno de Gestión de Proyectos con Docker 

Herramienta seleccionada: Tuleap 
Sistema Operativo: Linux (Ubuntu 18.04)

## Pasos
0. El equipo debe tener instalada la herramienta Docker. Además de tener esta herramienta instalada, es vital instalar docker-compose, para lo cual se sugiere seguir estos pasos
  - Habilitar super usuario 
    ```
    sudo su
    ```
  - Instalar docker-compose
    ```
    apt-get install docker-compose
    ```
1. Clonar el repositorio con la imagen de tuleap dentro de la carpeta tuleap-aio. Nota: tuleap-aio es el nombre que se eligió como directorio, sin embargo, este nombre puede ser diferente.
    ```
    git clone https://github.com/Enalean/docker-tuleap-aio tuleap-aio
    ```
2. Entrar a la carpeta en donde se acaba de clonar el repositorio. 
    ```
    export MYSQL_ROOT_PASSWORD=$(cat /dev/urandom | tr -dc "a-zA-Z0-9" | fold -w 15 | head -1)
    ```
3. Finalmente ejecutamos el siguiente comando para que se instalen y se ejecuten todas las dependencias del contenedor
    ```
    docker-compose up
    ```
4. Ahora ingrese a https://localhost y podrá visualizar la página de inicio de TULEAP, de igual manera, esta le solicitará un usuario y contraseña de ingreso
5. Para poder obtener las credenciales generadas por defecto ejecute 
    ```
    docker-compose exec tuleap cat /data/root/.tuleap_passwd
    ```
El usuario será **admin** y la contraseña será la que retorna el comando previamente ejecutado. 

# FAQ

¿Por qué no puedo visualizar la página Tuleap en mi computador?
R :/ Generalmente, hay procesos corriendo en el puerto 80 de los computadores, para el archivo docker-compose.yml la configuración por defecto está sobre este puerto, por lo tanto 
es necesario que se cambie el puerto 80 por otro puerto que no esté en uso. Por ejemplo: el puerto de 83 :older_man:. Editar 
  ```
  ports:
  - 80:80
  - 443:443
  ```
  
  reemplazar por 
  
  ```
  ports:
  - 83:83
  - 443:443
  ```
