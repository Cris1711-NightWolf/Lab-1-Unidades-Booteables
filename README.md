# 🖥️ Laboratorio 1: Creación y Uso de Memorias Booteables con Rufus y Ventoy

Este laboratorio tiene como objetivo **aprender el proceso de creación, configuración y uso de memorias USB booteables** utilizando las herramientas **Rufus** y **Ventoy**, así como la instalación de **Ubuntu** en una partición dedicada del computador.  
Se explorarán conceptos clave como el proceso de booteo, bootloaders, sistemas de archivos y estructuras de partición.

---

## 📑 Contenido

1. [Primer Punto: Exploración teórica](#primer-punto-exploración-teórica)  
   - Proceso de booteo con Rufus y Ventoy  
   - Función del bootloader y qué es GRUB  
   - Sistemas de archivos compatibles  
   - Estructura de particiones y tipos  

2. [Segundo Punto: Creación de memorias booteables](#segundo-punto-creación-de-memorias-booteables)  
   - Creación de memoria booteable con Rufus (Ubuntu)  
   - Creación de memoria booteable con Ventoy (Ubuntu + Windows)  

3. [Tercer Punto: Instalación de Ubuntu](#tercer-punto-instalación-de-ubuntu)  
   - Proceso de partición en el PC  
   - Instalación paso a paso de Ubuntu  
   - Evidencias con capturas de pantalla  

---

## ✅ Requerimientos previos

- Memoria USB de al menos **8 GB** para Rufus  
- Memoria USB de al menos **16 GB** para Ventoy  
- ISO de **Ubuntu** (versión estable recomendada)  
- ISO de **Windows** (opcional, para pruebas con Ventoy)  
- Software: **Rufus** y **Ventoy**  
- PC con soporte de arranque **BIOS/UEFI**

---
## 1) Proceso de booteo: Rufus vs Ventoy
### 📌 Creación de memoria USB booteable con **Rufus**

Antes de comenzar, es necesario **descargar la ISO** del sistema operativo que se desea instalar (por ejemplo, **Ubuntu** o **Windows**).

#### 🔹 Pasos para crear la memoria booteable con Rufus

1. **Descargar Rufus**  
   - Ir a la página oficial de [Rufus](https://rufus.ie/) y descargar la versión más reciente.  
   - No requiere instalación, ya que se ejecuta directamente como aplicación portátil.

2. **Conectar la memoria USB**  
   - Insertar la memoria USB en el computador (capacidad mínima recomendada: **8 GB**).  
   - ⚠️ Importante: Todo el contenido de la memoria será borrado, por lo que se recomienda hacer un respaldo previo.

3. **Cargar la imagen ISO**  
   - En la interfaz de Rufus, seleccionar la opción **“Seleccionar”** y buscar el archivo ISO descargado (Ubuntu, Windows u otro).

4. **Configurar el esquema de partición**  
   Aquí es importante elegir correctamente el **tipo de partición** según la configuración del equipo:  
   - **MBR (Master Boot Record):**  
     Compatible con equipos antiguos y con modo de arranque **BIOS o Legacy**.  
   - **GPT (GUID Partition Table):**  
     Recomendado para equipos modernos con modo de arranque **UEFI**.  

   👉 En la mayoría de computadores actuales, se debe usar **GPT + UEFI** para mayor compatibilidad y seguridad.  

5. **Iniciar el proceso de booteo**  
   - Presionar **“Iniciar”** en Rufus.  
   - Confirmar los mensajes de advertencia (se borrará todo el contenido de la memoria).  
   - Esperar a que el proceso finalice (el tiempo depende de la velocidad de la memoria USB).  

6. **Finalización**  
   - Una vez completado, la memoria USB estará lista como **dispositivo booteable**.  
   - Esta podrá usarse para instalar el sistema operativo arrancando desde la BIOS/UEFI del computador.  


**Arranque (lo que pasa cuando encienda el PC)**
1. Entrar al **Boot Menu** y elegir la USB (UEFI o Legacy, según tu BIOS).
2. El firmware carga el gestor de la USB:
   - En **UEFI**: `\EFI\BOOT\BOOTX64.EFI` (o primero *UEFI:NTFS* si la partición es NTFS).
   - En **Legacy**: MBR de la USB → sector de arranque.
3. Ese gestor lanza el **instalador** de la ISO (Windows Boot Manager o GRUB/shim en Linux).
4. Aparece el asistente de instalación del sistema operativo.

> **Notas y problemas frecuentes**
> - Si el archivo `install.wim` supera 4 GB, usa **NTFS** y activa *UEFI:NTFS*.
> - Si aparece advertencias de “gestor UEFI revocado”, use una **ISO reciente** o desactive **Secure Boot** temporalmente.
> - Asegurese de que el **modo de arranque (UEFI/Legacy)** de la BIOS coincida con el seleccionado en Rufus (GPT/MBR).


✅ Con estos pasos, se obtiene una memoria USB preparada con Rufus, lista para iniciar la instalación del sistema operativo elegido.


---

### 📌 Creación de memoria USB booteable con **Ventoy**

Ventoy es una herramienta ideal cuando se requiere **tener varias ISOs en la misma memoria USB**, ya que permite copiarlas directamente sin necesidad de formatear cada vez.  

Antes de comenzar, es necesario **descargar la ISO** del sistema operativo que se desea instalar (por ejemplo, **Ubuntu** o **Windows**).

#### 🔹 Pasos para crear la memoria booteable con Ventoy


1.  **Descargar Ventoy**  
   - Ir a la página oficial de [Ventoy](https://www.ventoy.net]) y obtener la última versión disponible.  
   - No requiere instalación, ya que se ejecuta como aplicación portátil.  

2. **Conectar la memoria USB**  
   - Insertar la memoria en el computador.  
   - Capacidad mínima recomendada: **16 GB**.  
   - ⚠️ Hacer copia de seguridad de los datos, ya que serán borrados.  

3. **Instalar Ventoy en la memoria USB**  
   - Seleccionar la unidad USB en la aplicación de Ventoy.  
   - Hacer clic en **Install** para preparar la memoria.  

4. **Configurar el sistema de particiones (MBR o GPT)**  
   - **MBR (Master Boot Record):** recomendado para equipos más antiguos o BIOS tradicionales.  
   - **GPT (GUID Partition Table):** recomendado para equipos modernos con **UEFI**.  
   - Ventoy permite elegir el esquema de acuerdo a la compatibilidad de tu PC.  

5. **Iniciar el proceso de booteo**  
   - Confirmar la instalación.  
   - Ventoy **crea su propio bootloader** en la USB y deja una partición grande (exFAT/NTFS) donde **solo copia** las ISOs (sin grabarlas)

6. **Copiar las ISOs**  
   - Una vez instalado, solo se necesita copiar y pegar las imágenes ISO (Windows, Linux, etc.) directamente en la memoria USB.  
   - Al iniciar desde la memoria, Ventoy mostrará un **menú de selección** para elegir qué sistema operativo desea arrancar.
   - 
**Arranque (lo que pasa cuando encienda el PC)**
1. Entre al **Boot Menu** y elija la USB (UEFI o Legacy).
2. El firmware carga el **bootloader de Ventoy** (basado en GRUB).
3. Ventoy muestra un **menú con todas las ISOs** copiadas.
4. Seleccione una ISO:
   - Ventoy **mapea** la ISO (técnica *loopback/wimboot*) y entrega el control al cargador interno de esa ISO.
5. Se inicia el **instalador** del sistema elegido (Ubuntu/Windows).
     
  > **Consideraciones**
> - Con **Secure Boot** activado, puede requerir el modo firmado/enrolar clave, o desactivarlo temporalmente.
> - Algunas ISOs muy antiguas o no estándar pueden no ser compatibles.

✅ ¡Listo! Su USB ahora está preparado con Ventoy y puede usarlo para arrancar desde varias ISOs sin necesidad de reformatear.

---

## 1.2) Bootloader (En memoria booteble) y que es un GRUB
### 📌 Para que sirve un Bootloader en la memoria Booteble

Un **bootloader** es un programa almacenado en una memoria booteable, como un **USB** o un **disco duro**. Su fucnion principal es **ejecutarse al encender el dispositivo** y encargarse de **cargar el sistema operativo o firmware en la RAM**, permitiendo asi que el sistema pueda arrancar. En pocas palabras, actua como un **intermediario** que facilita que el sistema operativo asuma el control del hardware.

1.2.1. 🚀 **Funcion Principal**
* Es el encargado de **ubicar y transferir el sistema operativo o firmware a la memoria RAM** del dispositivo, lo que permite que este pueda ejecutarse correctamente.

1.2.2 🟢 **Proceso de Arranque**
* Al encender el dispositivo, el firmware (generalmente ubicado en la **BIOS** o **UEFI**) se encarga de **buscar un dispositivo de arranque**. Cuando lo encuentra, procede a **cargar el bootloader en la memoria RAM**.

> En conclusion, el bootloader cumple un papel fundamental en el arranque de cualquier dispositivo, ya que garantiza que el sistema operativo se cargue de forma correcta. Ademas, brinda la flexibilidad de seleccionar que sistema operativo o version ejecutar.


---

### 📌 Que es el GRUB

GRUB (siglas en español: *GRand Unified Bootloader*) es un **gestor de arranque** que ofrece la posibilidad de **Seleccionar que sistema operativo cargar** en un equipo con multiples sistemas instalados. Tambien puede utilizarse en computadoras con un solo sistema, pero con **distintas opciones de inicio**. En terminos simples, es el programa que se **ejecuta inmediatamente despues de encender la computadora y antes de cargar el sistema operativo**.

* **🎯 Funcion Principal:**

Tiene la funcion de **cargar el nucleo (kernel) del sistema operativo en la memoria** y luego **cederle el control** para que el sistema pueda iniciar su ejecucion.

* 🔀 **Arrancador Multiple:**

Este gestor de arranque brinda la posibilidad de **elegir entre distintos sistemas operativos** (como **Windows**, **Linux**, etc.) o incluso **diferentes configuraciones dentro de un mismo sistema operativo**.

## ❗ Importante

Sin un **gestor de arranque** como **GRUB**, la computadora no tendria forma de **saber que sistema operativo debe cargar** y, en consecuencia, **no podria iniciar correctamente**.

---

# 1.4) 💽 Estructura de Particiones de Disco
La estructura de particiones de un disco es la forma en que el espacio de almacenamiento de
un disco duro o SSD se divide en secciones lógicas, llamadas particiones. Cada partición actúa 
como una unidad de almacenamiento independiente, lo que permite organizar los datos o instalar 
diferentes sistemas operativos en el mismo disco.

## 📂 Tipos de particiones

Existen varios tipos de particiones, tanto a nivel físico como lógico. A continuación se describen los más comunes:

### 1️⃣ Partición primaria
- Es la partición básica que puede contener un sistema operativo.
- Un disco duro puede tener hasta **cuatro particiones primarias**.
- Solo **una de ellas** puede estar marcada como **activa** para iniciar el sistema operativo.
- Si se requieren más de 4 particiones, se debe usar una partición extendida.

### 2️⃣ Partición extendida
- Es una partición especial que **no contiene datos directamente**.  
- Actúa como un **contenedor** para otras particiones llamadas **lógicas**.
- Solo puede haber **una partición extendida por disco**.
- Dentro de ella, se pueden crear múltiples particiones lógicas.

### 3️⃣ Partición lógica
- Se crean dentro de la **partición extendida**.
- Se usan para **almacenar datos** o incluso sistemas operativos adicionales.
- No tienen el límite estricto de 4 particiones como las primarias.
- Útiles cuando se requieren muchas particiones en un mismo disco.

### 4️⃣ Partición activa
- Es la partición que el sistema **BIOS/UEFI** usa para arrancar el sistema operativo.
- Solo una puede estar activa por disco al mismo tiempo.
- Normalmente corresponde a una **partición primaria**.

### 5️⃣ Partición de sistema (System Partition)
- Contiene los archivos necesarios para **iniciar el sistema operativo**.
- Incluye archivos como el **cargador de arranque (boot loader)**.

### 6️⃣ Partición de arranque (Boot Partition)
- Contiene los archivos del **sistema operativo** (ejemplo en Windows: la carpeta `\Windows`).
- En algunos sistemas coincide con la partición de sistema, en otros están separadas.

### 7️⃣ Partición OEM (Original Equipment Manufacturer)
- Usada por fabricantes para almacenar **herramientas de recuperación o diagnósticos**.
- Normalmente está **oculta** al usuario común.

### 8️⃣ Partición de recuperación
- Contiene una **imagen del sistema de fábrica** o herramientas para restaurar el sistema operativo.
- También suele estar **oculta** al usuario.

La **estructura de particiones** de un disco es la forma en que el espacio de almacenamiento de un disco duro o SSD se divide en secciones lógicas llamadas **particiones**.  
Cada partición actúa como una unidad de almacenamiento independiente, lo que permite **organizar los datos** o incluso **instalar diferentes sistemas operativos** en un mismo disco.

Los dos esquemas de particiones más comunes son **MBR** y **GPT**.  
La elección entre uno y otro depende principalmente del tipo de firmware de tu computador (**BIOS o UEFI**) y de las necesidades de almacenamiento.

---

## 📜 Master Boot Record (MBR)

El **MBR** es el esquema de particiones más antiguo y tradicional, creado en **1983**.  
Su nombre proviene de su ubicación en el **primer sector del disco**, que contiene tanto el **bootloader** (código de arranque) como la **tabla de particiones**.

Este es un esquema de particionamiento clásico que se introdujo con el IBM PC DOS en 1983. Se basa en un sector de arranque maestro que contiene la tabla de particiones
y un pequeño programa de inicialización. Sus principales limitaciones son:   

- **Tamaño Máximo:** Solo puede direccionar discos de hasta 2 terabytes (TB). Cualquier espacio adicional en un disco de mayor capacidad no podría ser utilizado.   

- **Límite de Particiones:** Se restringe a un máximo de cuatro particiones primarias por disco. Para superar esto, se implementó la partición extendida como un contenedor.   

- **Vulnerabilidad:** La tabla de particiones se almacena en una única ubicación al principio del disco, lo que la hace susceptible a la corrupción o a fallos, sin un mecanismo de respaldo incorporado.   

- **Compatibilidad:** Se asocia directamente con el firmware BIOS para el proceso de arranque.   


✅ **Compatibilidad:**  
MBR es compatible con sistemas antiguos que utilizan firmware **BIOS**.

---

## 💻 GUID Partition Table (GPT)

El **GPT** es el esquema de particiones más moderno, desarrollado como parte de la especificación **UEFI (Unified Extensible Firmware Interface)**, con el objetivo de superar las limitaciones del MBR.  
Hoy en día es el **estándar en la mayoría de los computadores y sistemas operativos modernos**.

### 🔹 Estructura y características principales

- **GUIDs (Identificadores Únicos Globales):**  
  Cada partición recibe un identificador único, lo que evita conflictos y facilita la gestión del sistema operativo.

- **Encabezado y copia de seguridad:**  
  A diferencia del MBR que almacena todo en un único sector, GPT guarda el encabezado al inicio **y una copia de respaldo al final del disco**, ofreciendo mayor seguridad frente a fallos.

- **Soporte UEFI:**  
  Está diseñado para funcionar de manera nativa con firmware **UEFI**, requisito fundamental para funciones modernas como **arranque seguro**.

### 📈 Ventajas clave sobre MBR

- **Sin límite de tamaño:**  
  Soporta discos de hasta **8 Zettabytes (ZB)**, eliminando la restricción de 2 TB.

- **Más particiones:**  
  Permite crear hasta **128 particiones primarias** por defecto, sin necesidad de particiones extendidas o lógicas.

- **Mayor resistencia:**  
  Gracias a la **copia de seguridad de la tabla de particiones**, es mucho más tolerante a fallos.

- **Arranque seguro (Secure Boot):**  
  Compatible con funciones de seguridad avanzadas del UEFI, protegiendo contra malware que intente ejecutarse durante el arranque.

---

## 📊 Comparación rápida: MBR vs GPT

| Característica            | 📝 MBR                                   | 💻 GPT                                    |
|---------------------------|------------------------------------------|--------------------------------------------|
| Año de creación           | 1983                                     | 2000 (UEFI)                                |
| Tamaño máximo soportado   | 2 TB                                     | 9,4 Zettabytes (ZB)                        |
| Número de particiones     | Máx. 4 primarias (o extendida + lógicas) | Hasta 128 primarias (sin extendidas)       |
| Redundancia               | ❌ No                                    | ✅ Sí, con copia de seguridad             |
| Compatibilidad            | BIOS                                     | UEFI (moderno)                             |
| Seguridad (Secure Boot)   | ❌ No                                    | ✅ Sí                                     |

---

## 2) Descargar la imagen de Ubuntu y la imagen de Windows.

# 📀 Cargar Imágenes ISO en Ventoy (Ubuntu y Windows)

**Copiar las imágenes ISO**  
Ventoy crea dos particiones en la unidad USB: una para el arranque seguro («VTOYEFI») y otra totalmente vacía en la que arrastrar y soltar las ISO
   - Descargar las ISOs oficiales:  
     - [Ubuntu](https://ubuntu.com/download)  
     - [Windows](https://www.microsoft.com/software-download/windows11)  
   - Copiar los archivos `.iso` directamente dentro de la memoria USB (no es necesario descomprimirlos ni usar herramientas adicionales).

3. **Arrancar desde Ventoy**  
   - Conectar la memoria USB en el computador.  
   - Ingresar al menú de arranque (Boot Menu, usualmente con las teclas `F12`, `Esc` o `F10`).  
   - Seleccionar la memoria USB con Ventoy.  
   - Ventoy mostrará un menú con todas las ISOs copiadas.  
   - Elegir **Ubuntu** o **Windows** y continuar con la instalación o modo Live.

---

## ✅ Ventajas del método
- No es necesario volver a formatear la memoria para agregar nuevas ISOs.  
- Se pueden tener varias distribuciones y versiones de sistemas operativos en la misma USB.  
- Compatible con BIOS y UEFI.  



## 3) Instalacion de ubuntu con Ventoy


# 🐧 Instalación de Ubuntu paso a paso con particionado del disco

Este apartado describe de manera clara y organizada el proceso que un usuario debe seguir para instalar **Ubuntu** en un PC, utilizando **Ventoy** para arrancar desde una memoria USB booteable y configurando correctamente el particionado del disco.

---

## 🔹 Requisitos previos
Antes de comenzar, es necesario contar con lo siguiente:

- ✅ Espacio libre en el disco duro (mínimo recomendado: **25–100 GB**, según las necesidades del usuario).  
- ✅ Una memoria USB.  
- ✅ El archivo **ISO de Ubuntu**.  
- ✅ El programa **Ventoy** para cargar la ISO en la memoria USB.  
- ⚠️ **Advertencia:** Se recomienda realizar una copia de seguridad de los datos antes de efectuar cambios en el disco.

---

## 1️⃣ Liberar espacio en el disco (Particionamiento en Windows)

1. El usuario debe abrir la herramienta de particionamiento en Windows.  
   Para ello, en el menú de inicio se escribe **“Particiones”** y se selecciona **“Crear y formatear particiones del disco duro”**.  
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/1#issue-3328706270  

2. Sobre el disco donde se instalará Ubuntu, se hace clic derecho y se selecciona **“Reducir volumen”**.  
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/2#issue-3328706631

3. En la ventana emergente, se especifica la cantidad de espacio a liberar (por ejemplo: **40 GB = 40,000 MB**) y se confirma con **Reducir**.  
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/3#issue-3328707031
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/4#issue-3328707382

Si el procedimiento se realizó correctamente, quedará disponible el espacio libre en el disco.

---

## 2️⃣ Configurar el arranque desde USB

1. Se inserta la memoria USB con **Ventoy** y se reinicia el PC.  
2. Durante el encendido, el usuario debe presionar la tecla correspondiente para acceder al menú de arranque (generalmente **F2, F10, F11 o ESC**, dependiendo del hardware).  
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/5#issue-3328708294  

3. En el menú de arranque, se accede a **Boot Options** y se coloca la **USB en primera posición** (para que el pc priorice el arranque con la usb) utilizando las teclas (por ejemplo: **F5/F6**).  
   
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/6#issue-3328708841
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/7#issue-3328709769

5. Si aparece la opción **Secure Boot**, esta debe desactivarse para evitar inconvenientes con la instalación de Ubuntu.
   El security boot que es otra capa importante que tienen las computadoras, esto suele traer problemas para instalar otro sistema operativo que no sea Windows,
   por ende, la solución mas rápida es desactivar esta opción
   > **Nota**
> - Al hacer esto se esta desactivando una capa de seguridad adicional en el pc*.
 
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/8#issue-3328710204

6. Finalmente, se guardan los cambios (**F10**) y el PC iniciará desde la memoria USB con Ventoy.

---

## 3️⃣ Seleccionar la ISO de Ubuntu en Ventoy

1. Una vez cargado Ventoy, se muestra un menú con las ISOs almacenadas en la memoria.  
2. El usuario debe seleccionar la ISO de **Ubuntu** y presionar **Enter**.  
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/9#issue-3328710396

3. A continuación, el instalador ofrece la opción **“Try or Install Ubuntu”**. Esta debe seleccionarse y confirmarse con **Enter**.  
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/10#issue-3328710657

---

## 4️⃣ Configuración inicial de instalación

1. El instalador solicita la configuración inicial,por ejemplo, de idioma y de la **conexión WiFi** (recomendado, ya que permite descargar actualizaciones y software adicional).  
2. Se recomienda activar las siguientes casillas:  
   - ✅ Descargar actualizaciones durante la instalación.  
   - ✅ Instalar software de terceros para multimedia y controladores.
   - Ya que al activar estas dos casillas tendremos el sistema actualizado e instalara codex necesarios para la reproducción multimedia y algunos controladores.
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/11#issue-3328710934

---

## 5️⃣ Particionado manual del disco en Ubuntu

⚠️ **Importante:** Se recomienda realizar una copia de seguridad de los datos antes de efectuar cambios en el disco.

El paso más importante es el **particionado del disco**.  
Aunque Ubuntu ofrece opciones automáticas, en este caso se recomienda un particionado **manual** para un mayor control.
 > **Nota**
> - Hoy en dia las distribuciones de Linux ya tienen muy bien automatizada esta parte*.
> - Hay distinas maneras de hacer el particionamiento, en esta ocasión usaremos las mas básicas para el funcionamiento de Ubuntu.

1. El usuario debe seleccionar la opción **Instalación manual (Something else)**.  
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/12#issue-3328711216
   
A continuación se muestra una tabla general sobre las particiones basicas que necesitaremos crear para el correcto funcionamiento de ubuntu:
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/13#issue-3328711613

3. En la ventana de particionado, se localiza el espacio libre creado en Windows y se comienza a crear las particiones utilizando el botón **“+”**.  
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/14#issue-3328711901

### 📌 Particiones recomendadas

- **EFI (Sistema de arranque):**  
  - Obligatoria en equipos modernos.  
  - Si ya existe una partición EFI creada por Windows, no es necesario crear otra, ya que Ubuntu puede usar la misma.  

- **SWAP (Memoria de intercambio):**  
  - Funciona como memoria virtual cuando la RAM se agota.  
  https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/15#issue-3328712456

- **/ (Raíz):**  
  - Obligatoria. Contiene el sistema y las aplicaciones.  
  - Se recomienda asignar al menos **20–30 GB**.  
  https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/16#issue-3328712781

- **/home (Opcional):**  
  - Almacena documentos, fotos, música y demás archivos personales.  
  - Si no se crea, los archivos se guardarán dentro de la carpeta personal en la raíz.  
  https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/17#issue-3328713072 

3. Una vez creadas las particiones, se debe seleccionar el **cargador de arranque (GRUB)** en el mismo disco donde se realizó el particionado.  
   https://github.com/Cris1711-NightWolf/Lab-1-Unidades-Booteables/issues/18#issue-3328713413 

---

## 6️⃣ Instalación final

1. Se hace clic en **Instalar ahora** y se confirman los cambios en el disco.  
2. Posteriormente, se configura la información básica:  
   - Zona horaria.  
   - Nombre de usuario.  
   - Contraseña de acceso.  

3. Al finalizar, el sistema solicita reiniciar el equipo.  

✅ En este punto, Ubuntu queda instalado y listo para usarse junto con Windows.

---
