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
