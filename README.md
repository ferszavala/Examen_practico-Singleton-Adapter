# Examen_practico Singleton Adapter
 
## Descripción

**Realice un proyecto en Windows Forms que solucioné el problema presentado**

_Para la obtención de datos se leerán los datos desde un archivo en formato Json. 
El formato ustedes lo pueden definir. Asegurese de agregar este archivo en su 
código._


_Realicé una pequeña explicación de los patrones utilizados y por qué._

_Crear una aplicación Windows Forms que tiene como objetivo la consulta de 
calificaciones, consulta de información de perfil y descarga de calificaciones._

_La aplicación deberá mostrar los datos apropiados de acuerdo al tipo de usuario 
que se autentique. Los controles que deseas usar deben reaccionar al tipo de 
usuario que se autentique. Si un usuario no puede editar algún dato, este no deberá 
poder modificarse. Al final no todos los tipos de usuario verán lo mismo._

**La configuración quedará de la siguiente manera:**

- Usuario Tipo Estudiante: 
- Consultar sus propias calificaciones
- Visualizar la información de su perfil: información básica, lista de 
calificaciones y promedio
- Visualizar la opción para descargar sus calificaciones. 
- Usuario Tipo Maestro: 
- Consultar las calificaciones de todos sus alumnos
- Visualizar la información de su perfil: información básica
- No podrá visualizar la opción de descarga de calificaciones. 
- Usuario Tipo Supervisor: 
- No podrá consultar calificaciones
- Visualizar la información de su perfil: información básica 
- No podrá visualizar la opción de descarga de calificaciones. 

**La información básica del alumno es la siguiente:**
- Nombre completo
- Carrera
- Año de nacimiento
- Ciudad de Origen
- 
_Las calificaciones deberán ser por materia._

**En el archivo de configuración de la aplicación, deberá existir una llave, que 
indique a través de un valor el formato en el que las calificaciones deberán ser 
descargadas:**
- Txt: archivo con las calificaciones en formato .txt
- Docx: archivo con las calificaciones en formato de Word(.docx) 

**Puntos importantes:**
- Considere que la aplicación debe ser fácilmente configurable en cuanto a los 
módulos que deben aparecer por usuario se refiere. 
- Considere que la aplicación podría cambiar de formato Json a otra librería que 
pueda leer datos, por lo que debe quedar extensible.
No es necesario que se realice el proceso de importación del archivo, solo mostrar 
un mensaje que lo simule, si se llega a realizar este punto, se agrega 0.5 a su 
calificación ya sea del examen practico o teórico.

**Importante: el usuario no seleccionará el formato, sino que dependerá del valor que 
se tenga en ese momento en el archivo de configuración**

## Patrones de diseño utilizados
**Singleton:**

_Descipción:_

- Se usa cuando es una clase que se necesita en todo el programa (es decir que se debe de acceder a ella desde
cualquier otra)
- Debe se ser una sola instancia (creada por la clase)
- No se debe de inicializar desde un inicio del programa

Se tiene la clase _Singleton_ en la que creamos la instancia única, así como la base de datos que en este caso es ejemplificada por un _JSON_, el _Singleton_ nos ayuda a crear una sola instancia desde la que pueda acceder cualquier clase, la cual crea la _Base de datos_ que estaremos usando para obtener la información de cada usuario


**Adapter:**

_Descipción:_

Se usa debido a que en ocasiones posteriores podríamos desear cambiar el tipo de archivo de lectura, es decir el que usamo como _Base de datos_, de manera sencilla. En este caso hemos usado _JSON_, pero si quisieramos modificarlo tenemos en el _Adapter_ el prototipado de clases abstractas que toman los datos de los datos que nos interesan siempre, sin importar el tipo de archivo: alumnos, maestros, supervisores (llamados administradores en este proyecto) y el acceso a los mismos datos. Mientras que en el _Adaptee_ usamos el Singleton para tomar la instancia del tipo de usuario al que estamos haciendo referencia en la _Base de datos_ y creamos funciones basadas en listas que recolectan la cada información de cada uno, así como el agregado de información dependiendo del tipo de usuario que sea: alumno, maestro o administrador, la clase que funcionaría como nuestro _Client_ sería precisamente el _Singleton_, el cual podría tomar otro tipo de archivo y bastaría con modificar esto para dejar de usar un _JSON_ y cambiar por otro tipo de formato.

## Explicación general del código y factores importantes a tomar en cuenta
En el archivo App.config se incluye la llave para cambiar el formato de la descarga de calificaciones (solo hace falta cambiar la terminacion de txt a docx o en sentido opuesto) y automáticamente se descargará en la ubicación que el usuario desee al presionar el botón de _Descarga de calificaciones_

El archivo origen JSON desde donde obtiene los archivos se encuentra en bin/Data/Datos_projecto.json
