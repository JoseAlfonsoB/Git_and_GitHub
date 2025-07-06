<img src="./IMGs/Git-and-GitHub.png" style="width: 100%; height:300px; border-radius: 25px">

## Introducción general

Estas notas están pensadas para reunir lo más importante sobre **Git** y **GitHub**, dos herramientas clave en el mundo del desarrollo. Git nos permite llevar un control preciso de los cambios en nuestros proyectos, mientras que GitHub facilita el trabajo en equipo y la colaboración en línea.

La idea de este curso es entender cómo funcionan, qué comandos son esenciales y cómo aplicarlos en el día a día como desarrolladores. Todo está explicado con ejemplos, analogías y algunos consejos útiles que hacen más fácil aprender y recordar.

## Introducción a Git

### Concepto de Git

**Git** es un **sistema de control de versiones distribuido**. Esto nos ayuda a **documentar** y **trazar cada uno de los cambios**  que nosotros como desarrolladores realicemos.

> **Ej:**  Funciona como los **mensajes de WhatsApp**, en donde nosotros podemos ver todos los **mensajes anteriores**.

![Ramas-Git](IMGs/GIT-RAMAS.png)

Git es un sistema de control de versiones distribuido ==diseñado para rastrear cambios== y ==coordinar== el ==trabajo colaborativo== en proyectos de software.

### Conceptos clave de Git

- **Control de versiones:** ==Registra el historial de cambios en archivos==, permitiendo ==revertir==, ==compartir== y ==recuperar== versiones anteriores.
- **Distribuido:** ==Cada desarrollador tiene una copia== completa del repositorio, lo que ==permite trabajar sin conexión== y facilita la redundancia

> **NOTA:** Sistemas operativos como LInux y MacOS ya tienen Git instalado por defecto aún que puede que no sea la ultima versión.

### Comandos de Git

> **NOTA:** Como recomendación, hay que habilitar la opción de poder visualizar los archivos y carpetas ocultos en nuestro sistema operativo.
> 
> En Linux se hace con `Ctrl + H`.

- `git init`: Inicializa un repositorio con la herramienta de Git.

> **NOTA:** Cuando en un directorio nos encontramos con un **directorio oculto** `".git"` eso quiere decir que **ese directorio ya a sido** o esta siendo **trabajado** con el **control de versiones de Git**.

#### Ramas en Git
![Ramas](<IMGs/Git Ramas.png>)
La rama **master o main**  es la **rama base** sobre la cual esta **montada el proyecto principal**.

- `git add`: Nos permite **agregar archivos y/o carpetas** a nuestro **proyecto principal** inicializado en Git.
- `git commit`: Nos permite **subir/insertar el cambio realizado** con su respectivo identificador.
- `git status`: Nos permite **evaluar el estado actual del  repositorio** (archivos modificados, en **Staging Area** [listo para commit], no rastrados [untrancked]).
- `git log`: Nos **muestra el historial de commits** (autor, fecha, mensaje y hash) en un **orden cronológico inverso** (más recientes primero).
	- `git log --graph`: Incluye un gráfico de las ramas.
- `git checkout`: Nos sirve principalmente para:
	- **Cambiar de rama**.
	- **Restaurar archivos** a un estado anterior (sin afectar  commits).

```bash
git checkout "nombre-de-rama"
git checkout "nombre-archivo"
```


- `git seter`: Nos permite **deshacer cambios en diferentes niveles**.
	1. Quitar archivos de Staging Area (sin borrar los cambios).
	2. Eliminar commits locales.

```bash
git reset --soft HEAD~1
```

**Deshace le ultimo commit** pero mantiene los cambios en Staging Area. 
**Utilizado para reescribir un commit** (olvidaste incluir archivos).

### Alias en Git

Los **alias** en Git son **atajos personalizados** que puedes crear para comandos largos o usados frecuentemente.

##### ¿Para qué sirven?

- Acortar comandos complejos.
- Evitar errores de tipeo.
- Automátizar tareas repetitivas.

##### ¿Cómo puedo crear un alias?

###### Sintaxis
```bash
git config --global alias.nombre-del-alias "comando-original"
```
##### ¿Cómo ver todos los alias existentes?

```bash 
git config --get-regexp alias
```

##### ¿Cómo eliminar un alias?

```shell
git config --global --unset alias.nombre-del-alias
```

###### Ejemplo de la creación de alias típicos

![Alias-Git](IMGs/ALIAS.png)
### .gitignore

El archivo `.gitignore` es un archivo de texto que **le indica a Git que archivos o directorios debe ignorar en el repositorio**.
Es especialmente útil para **excluir archivos generados** **automáticamente**, **temporales** o **sensibles** que no deben incluirse en el control de versiones.

> **Ej:**
> ```txt
> # Igonorar archivos log
> *.log

##### ¿Donde se coloca?

- **En la raíz del proyecto.**
- También puedes tener archivos `.gitignore` en subdirectorios para reglas especificas.

####  git diff

- `git diff`: Nos permite **visualizar todos los cambios realizados** que **no** hayan sido **guardados** en el **Working Directory**.
- Muestra las modificaciones actuales (sin usar `git add`).
- Es **ideal para revisar que cosas se han editado antes de** preparar archivos para **hacer** `commit`
![git-diff](<IMGs/git diff.png>)

- **-** : Lineas eliminadas (rojo en la terminal)
- **+** : Lineas añadidas (verde en la terminal)

### Desplazamiento en una rama (Moverse entre commits)

En Git el desplazamiento en una rama **se refiere a moverse entre diferentes commits** dentro del historial de una rama.

Esto **permite inspeccionar, modificar o recuperar estados  anteriores** del proyecto.

##### 1.- Conceptos clave
- **HEAD:** Es un **apuntador que indica tu posición actual** en el historial.
- **Rama (Branch):** **Secuencia lineal de commits** que representa una linea de desarrollo.
- **Commit (HASH):** **Identificador único que representa un estado guardado** del proyecto (Ej: **a1b2c3d**).

##### 2.- Comandos para desplazarse

- `gig checkout`: ==Permite moverse a un commit en especifico== (sin modificar la rama). 

```bash
git checkout "hash-del-commit"
```

Para ==regresar== a tu ==rama principal== 

```bash
git checkout "nombre-de-la-rama"
```

![Desplazamientos-en-Git](IMGs/Desplazamientos-en-Git.png)
#### Git reset --hard & Git reflog

- `git reset --hard`: ==Borra todo lo que no esta guardado en un commit==.
	- Cambios en tus archivos
	- Commits recientes
==Puedes mover tu rama a un commit anterior== (_es como retroceder en el tiempo_).

##### ¿Cuándo usarlo?

- Cuando quieres ==hacer commits locales==.
- Cuando todo esta tan mal que quieres volver a un punto seguro.
```bash
git reset --hard "hash-del-commit"
```

- `git reflog`: ==Muestra todo lo que has hecho en git== (_incluso lo que borraste_).

##### ¿Cuándo usar git reflog?

- Si borraste un commit por error (_con `git reset --hard` o `git rebase`_).
- Si usaste un `merge/rebase` y todo se rompo y quieres volver atrás.
- Si accidentalmente borraste una rama y necesitas recuperar su ultimo commit.

###### ¿Cómo usarlo?

**Situación:** Borraste los dos últimos commits con `git reset --hard HEAD~2` y te arrepentiste.

1. Usa `git reflog` para encontrar los últimos `hashes` de los commits borrados.
2. Selecciona el `hash` del commit al que quieres volver (_Ej: f4e5dec_) -
3. Recuperalo con:

```bash
git reset --hard f4e5dec
```

![git-reset](<IMGs/git reset --hard && git reflog.png>)
### Tags en Git

##### ¿Qué son las Tags en Git?

Los ==tags son como "_marcadores_"==  o "_versiones oficiales_" ==que se colocan en== commits específicos para señalar ==puntos importantes en el historial del proyecto==  (_Ej: lanzamiento de la versión como **v1.0.0**, **v2.3.0**_).

##### Analogía

Imagina que tu proyecto es un libro. Los **commits son las páginas** y los **tags son "post-it"** pegados a páginas clave como "_Capitulo 1_" o "_Edición FInal_".

###### Tipos de Tags

- **Lightwight Tags**
		Son ==etiquetas simples== (_solo un nombre apunto a un commit_).

```bash
git tag V1.0.1
```

- **Annotated Tags**
		==Incluyen metadatos== (_autor, fecha, mensaje descriptivo y firma PGG_)

	<div style = "border: solid 1px; border-radius: 15px; padding: 10px; display: column;">
	<p style="color: red; font-wieght: bold;">IMPORTANTE!</p>Recomendado para versiones oficiales.
	</div>

```bash
git tag -a V2.0.0 -m "mesanje"
```

> NOTA: Con **Git tag** ==podemos ver todas nuestras etiquetas== creadas.

### Ramas en Git

Las ramas en Git ==son lineas de desarrollo independientes== que ==permiten trabajar en diferentes características, creaciones o experimentos==  sin afectar el código principal.

##### Analogía 
```txt
Imagina un árbol.
- El tronco principal (main o master) es la versión estable.
- Las ramas son derivaciones donde puedes probar cosas nuevas sin romper el tronco.
```

![Ramas-Git](<IMGs/Git Ramas.png>)
##### ¿Cómo funcionan?

1. ==Cada rama apunta a un commit== especifico.
2. Los ==cambios== de una rama son ==aislados: No se afectan otras ramas hasta que se fusionan== (_merge_).
3. ==Puedes crear, eliminar o fusionar ramas== en cualquier momento.

##### Comandos esenciales

1. `git branch` (_gestiona ramas_)
	Se pueden ==ver==, ==crear== o ==eliminar ramas==.


| Comando                       | Descripción                                            |
| ----------------------------- | ------------------------------------------------------ |
| `git branch`                  | ==Lista todas las ramas== (_indica la actual_)         |
| `git branch "nombre-rama"`    | ==Crea== una ==rama nueva== (_pero no cambia a ella_)  |
| `git branch -d "nombre-rama"` | ==Borra== una ==rama local== (_si ya fue fusionada_)   |
| `git branch -D "nombre-rama"` | ==Fuerza== el ==borrado== (_aunque no este fusionada_) |
2. `git switch` (_cambia entre ramas_)

	==Moverse entre ramas== existentes.


| Comando                       | Descripción                                      |
| ----------------------------- | ------------------------------------------------ |
| `git swith "nombre-rama"`     | ==Cambia== a la ==rama== especificada            |
| `git switch -c "nombre-rama"` | ==Crea== una ==rama nueva== y ==cambia a ella==. |
3. `git merge` (_fusionar ramas_)
	==Combina== los ==cambios de una rama== a ==otra== (_Ej: traer "login" a "main"_)
##### Pasos típicos

1. ==Posicionarte en la rama destino== (_Ej: "main"_)

```bash
git switch main
```

2. ==Fusionar la rama deseada==.

```bash
git merge login
```

### Stash en Git

##### ¿Qué es el Stash en Git?

El **stash** es un "_cajon temporal_" donde ==git guarda cambios no guardados== (_en el Workging Directory o en el Staging Area_) ==para que puedas cambiar de ramas sin perder los cambios==.

###### Analogía
```txt
Imagina que estas escribiendo un documento y alguien te interrumpe. En lugar de guardarlo como versión final (_commit_) lo dejas en un post-it (_stash_) para recordarlo más tarde.
```

###### Comandos esenciales

1. `git stash`: (_**guarda** cambios temporales_)
		**Gurda todos los cambias no commitados** en el stash.


| Comando           | Descripción                                 |
| ----------------- | ------------------------------------------- |
| `git stash`       | ==Guarda archivos temporales==              |
| `git stash -m ""` | ==Guarda con== un ==mensaje personalizado== |
2. `git stash list` (_Ver todos los stash guardados_)
		==Muestra== una ==lista de stash== (_guardados como pilas: El ultimo en entrar es el primero en salir_).
3. `git stash apply` (_Recuperar cambios_)
		==Recupera== los ==cambios del stash sin borrarlos de la lista==.

```bash
git stash apply
git stash apply "id-stash"
```

4. `git stash pop` (_Recupera y borrar_)
		==Recupera los cambios== y ==elimina el stash de la lista==.

```bash
git stash pop
git stash pop "id-stash"
```

5. `git stash drop` (_Elimina un stash_)
		==Elimina== un ==stash especifico sin aplicarlo ==.

```shell
git stash drop "id-stash"
```

6. `git stash clear` (_Elimina todos los stash_)
		==Elimina todo el contenido== de la sección de los stash.

```shell
git stash clear
```

---

## Introducción a GitHub

### ¿Qué es GitHub?

**GitHub** es una **plataforma en la nube basada en Git** que sirve como **hub** (_centro_) para **alojar**, **gestionar**, **colaborar en proyectos** de desarrolladores de software.

Su ==concepto principal== es el de ser el "_Facebook de los programadores_" en donde **equipos** y **comunidades comparten código**, **resuelven problemas** y **construyen software** juntos.

### Concepto principal

"_Colaboración y control de versiones en la nube_"

==GitHub extiende las capacidades== de Git (_que es local_) ==a un entorno remoto== y social.

### GitHub nos permite

- **Almacenar repositorios Git en la nube**
- **Facilitar el trabajo en equipo**
- **Integrar herramientas de automatización de pruebas y despliegues**

### Funciones clave de GitHub
- **Repositorio remoto:** Guarda tu código en la nube
- **Pull Requests (PRs):** Proponer cambios y revisar código antes de fusionarlo
- **Issues:** Gestionar tareas, logs y mejoras
- **GitHub Actions:** Automatizar flujos
- **GitHub Pages:** Hosting gratuito para sitios web estaticos
- **Forks y contribuciones:** Copiar repositorios de otros devs, modificarlos y sugerir cambios

#### Diferencias clave entre Git Y GitHub

| Git                                                                                                                              | GitHub                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| ==Sistema de control de versiones distribuido== que ==permite mostrar cambios== en archivos y ==coordinar el trabajo== en equipo | ==Plataforma en la nube basada en Git== que ofrece ==alojamiento de colaboración== y ==gestión== de proyectos |
| Es un ==software local== (_se instala en tu computadora_)                                                                        | Es un ==servicio en la nube==  (_requiere conexión a Internet_)                                               |
| Creado por **Linus Torvalds** (_2005_) para el ==desarrollo del kernel de LInux==                                                | Fundado en 2008 (_adquirido por MIcrosoft en 2018_)                                                           |
#### Funcionalidad principal

| Git                                                                                  | GitHub                                                                     |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| **Control de versiones local:** Guarda el historial de cambios en tu maquina         | **Almacenamiento remoto:** Guarda repositorio Git en la nube               |
| **Ramas, merge y commits:** Trabaja en diferentes versiones del proyecto             | **Pull Request y Code Review:** Permite revisar código antes de fusionarlo |
| **Trabajo Offline:** No necesitas Internet para usar Git                             | **Colaboración en equipos:** Issues, proyectos, wikis y discusiones        |
| **No tiene interfaz gráfica nativa:** Se usa por consola o por clientes como Git GUI | **Interfaz web intuitiva:** Facilita la navegación y gestión de proyectos  |
### Protocolo Secure Shell (SSH)
[Notebook de SSH](https://notebooklm.google.com/notebook/a13bf044-360a-4106-ae88-2b1fccf1bc2e)

El **Protocolo Secure Shell (SSH)** es un **protocolo criptografico de red** diseñado para **operar servicios** de la red de **manera segura** sobre una **red no segura**.

Fue creado e 1995 por **Tatu Ylone** para **remplazar protocolos inseguros** como **Telnet** o **RSH**, que **transmiten credenciales de autenticación** (_como usuario y contraseña_) en **texto plano**, lo que significa un riesgo significativo de intercepción de terceros.

#### 1.- Seguridad y el "Túnel de Cifrado"

La seguridad fundamental de SSH ==radica== en sus ==mecanismos de cifrado==, que ==oculta el contenido de transmisión== de cualquier observador.

Este proceso crea un "_túnel seguro_" o cifrado donde toda la transmisión (_comandos, datos o autenticación_) viaja de manera incomprensible para un interceptante.

Este **túnel seguro** se **establece** generalmente sobre el **puerto TCP 22** el cual esta **asignado** y es el **puerto de escucha estándar** por los **servidores SSH**.

El puerto 22 es la "_puerta de encuentro_", mientras que el "_túnel_" es la conexión cifrada que se forma a tráves de él.

#### 2.- Autenticación basada en claves

A diferencia de los métodos tradicionales de usuario y contraseña, SSH utiliza la criptografia de clave pública para autenticar tanto al equipo remoto (_servidor_) como al usuario.

Este método implica el uso de **un par de claves** (_o llaves_).

- **Una clave privada:** Se genera en tu computadora local y debe mantenerse **estrictamente confidencial**. Es crucial que esta clave privada **nunca se transfiera a través de la red** durante el proceso de autenticación.
- **Una clave pública:** Se genera junto con la privada y se comparte con el servidor remoto (_en este caso GitHub_). El servidor la utiliza para verificar que posees la clave privada correspondiente, sin requerir que esta ultima se transfiera.

#### 3.- Evolución del protocolo

- La primera versión se llamo **SSH-1**.
- Luego vino **SSH-2** que es la que se usa hoy en día y es mucho más segura y mejor.

La versión 1 se considera vieja y con fallas de diseño, por eso es mejor evitarla.

#### 4.- ¿Cómo GitHub utiliza SSH para autenticación?

GitHub utiliza el protocolo SSH para permitir a sus usuarios **conectarse** y **autenticarse** con sus repositorios sin la necesidad de proporcionar su **nombre de usuario** y un **Personal Access Token** (_PAT_) en  cada visita.

Por ello, el **usuario debe generar un nuevo par de claves SSH** (_privada y pública_)en su equipo local y **añadir** la clave SSH pública a su cuenta de GitHub.

Al intentar conectarse (_Ej: para realizar un "push"_) tu cliente SSH y el servidor de GitHub realizan un **desafió criptografico** para verificar la posesión de la clave privada correspondiente a la pública registrada, sin que la clave privada abandone el sistema.

Una vez autenticado, se establece el túnel cifrado para la comunicación.

### Comandos git fetch y git pull
Estos comandos se usan para ==organizar tu repositorio local con los cambios del repositorio remoto== (_como los que están en GItHub_). Pero funcionan de manera diferente.

#### 1.- git fech
##### Descarga los cambios (_==verifica si hay nuevos cambios==_)
==Descarga los cambios== más recientes ==del repositorio remoto== (_en GitHub_) ==pero no los aplica en tu código local==.

Dicho de otra manera:

==Descarga== en local ==el historial de cambios==, ==pero sin descargar== los ==cambios==.
Esto ==nos permite comparar los cambios antes de fusionarlos== (_merge_).

#### 2.- git pull
##### Descargar y aplicar cambios

==Descarga los cambios del repositorio remoto== (_fetch_) ==y los fusiona== (_merge_) ==automáticamente en el== repositorio ==local==.
Es como un `git fetch` y un `git merge` en un solo comando.

#### ¿Cuándo se usan?
- Cuando quieres **actualizar tu rama local con los últimos cambios de GitHub**.
- Si **estas seguro de que** los cambios remotos **no generan conflictos** con tu trabajo.

### Comando git clone

Se usa para **copiar un repositorio remoto**, y **descargarlo** en tu **computadora local**.
Es la forma más rápida de comenzar a trabajar con un repositorio existente.

###### Sintaxis
```shell
git clone "url-repo-original"
```
### Comando git push

Se usa para **enviar los cambios confirmados** "_commits_" de tu **repositorio local, al repositorio remoto** (_GitHub_}.

Es tu manera de compartir tu trabajo con el equipo o guardar una copia en la nube.

###### Sintaxis básica
```shell
git push "nombre-del-remoto" "nombre-de-rama"
```

### ¿Qué es un Fork en GitHub?

Un **fork** es una **copia personal de un repositorio de otro usuario** en la cuenta de **GitHub**. Te **permite experimentar, modificar** y **contribuir** al **proyecto original** sin **afectarlo directamente**.

##### Analogía
```txt
Imagina que el repositorio original es un libro en una biblioteca pública.
Hacer un fork es como fotocopiar el libro para tomar notas y hacer cambios en tu copia.
Luego, puedes sugerir tus cambios al autor original (Pull Request).
```

![[Diagrama-Fork.png]]


### ¿Qué es un Pull Request (PR) en GitHub?
 
Una **Pull Request** (_o un PR_) **es una solicitud par fusionar tus cambios** (_en una rama o en un fork_) **con un repositorio principal**.

Es el **mecanismo central** para **contribuir a proyectos en GitHub**, ya sea en **equipo** o en **código abierto**.

###### Analogía
```txt
Imagina que el proyecto principal es un documento compartido (como un Google Doc).
Tú hace una copia, editas una sección y propones tus cambios al dueño del documento.
El dueño revisar los cambios y decide si los acepta (merge) o rechaza las modificaciones.
```

#### Tipos comunes de PRs
##### **1.- Contribuciones a Open Source:** 
Haces un fork, modificas y envías un PR al proyecto principal.
##### **2.- Trabajo en equipo:**
Creas una rama (_feactures/login_) haces cambios y haces revisión.
##### **3.- Corrección de bugs:**
Solucionas un error y lo propones vía PR.
#### Buenas practicas para  PRs efectivos

- **Títulos descriptivos:** 
		Ej: "_Corrección en el formulario login_"
- **Descripciones detalladas:**
		Explica qué, por qué y cómo se hicieron los cambios.
- **PRs pequeños:**
- Enfocate en un solo cambio (_Ej: un bug o feature_). Es más fácil de revisar.

