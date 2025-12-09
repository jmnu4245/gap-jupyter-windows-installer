# gap-windows-setup

[🇪🇸 Español](#instrucciones-de-uso) 
[🇺🇸 English](#instructions-for-use)

---
## Objetivo del script

El objetivo de este script es permitir al usuario utilizar gap en un jupyter notebook sin conocer los entresijos de su configuración.

## INSTRUCCIONES DE USO

Una ejecución correcta consiste simplemente en ejecutar `install.bat` con permisos de administrador y seguir las indicaciones. El proceso puede llevar varios reinicios.

### Flujo de Ejecución
El script tiene 3 partes importantes:

1.  **Comprueba las características de Windows:** Verifica si la ejecución de WSL está activada.
    * Si están activadas, no hace nada.
    * Si no están activadas, las activa y reinicia.
2.  **Comprueba la instalación de WSL:**
    * Si está instalado, no hace nada.
    * Si no está instalado, lo instala y reinicia.
3.  **Configuración final:** Abre WSL, instala GAP y configura Jupyter.

**El proceso completo es:**
`install.bat` -> `activarCaracteristicas.ps1` -> *(Reinicia si es necesario)* -> `install.bat` -> `instalarWsl.ps1` -> *(Reinicia si es necesario)* -> `finalgap.bat` -> `setup-gap.sh`

## Verificación de la instalación

Todo está instalado dentro del **Windows Subsystem for Linux (WSL)**. Se puede acceder ejecutando en una terminal (CMD o PowerShell):

```cmd
wsl
````

La aplicación se instala en la carpeta del primer usuario `gap`, junto con un *environment* de **Python** donde está instalado el **kernel de GAP**.

### Comprobar la instalación de GAP

Ejecutar en una terminal dentro de WSL:

```bash
gap
```

Debería abrirse la consola interactiva de GAP, mostrando algo similar a:

```text
 ┌───────┐   GAP 4.12.2, 64-bit
 │  GAP  │   [https://www.gap-system.org](https://www.gap-system.org)
 └───────┘   Architecture: x86_64-pc-linux-gnu-gcc-default64
 Type ? for help. 
gap>
```

Para salir de GAP escribir:

```gap
quit;
```

### Comprobar la instalación del kernel de GAP

Ejecutar desde la carpeta del usuario en WSL:

```bash
source ./gap-env/bin/activate
jupyter kernelspec list
```

Debería aparecer:

```text
Available kernels:
  python3                -> .../share/jupyter/kernels/python3
  gap                    -> .../share/jupyter/kernels/gap
```

## Usar GAP en Visual Studio Code

Hay cuatro partes importantes para un funcionamiento adecuado:

1.  Instala la extensión **Jupyter** desde el marketplace de VS Code.
2.  **Conecta VS Code a WSL** haciendo clic en la esquina izquierda inferior (icono verde de remoto).
3.  Abre el directorio `/user` en VS Code de forma que te aparezca el directorio `/env_gap` a la izquierda.
4.  Abre un archivo `.ipynb` o crea uno nuevo.
5.  En la parte superior derecha (o izquierda), debes seleccionar el **Kernel: GAP**. En caso de que no lo detecte, revisa el paso anterior.

Escribe y ejecuta código GAP directamente en las celdas. Por ejemplo:

```gap
G := SymmetricGroup(4);
Size(G);
```

## Desinstalar

### Eliminar la instalación completa de Ubuntu en WSL

Si deseas eliminar completamente la distribución de Ubuntu que instalaste en WSL (junto con GAP y todos sus datos), puedes ejecutar en PowerShell/CMD:

```cmd
wsl --unregister Ubuntu
```

> ⚠️ **Advertencia:** Esto eliminará toda la instalación de Ubuntu en WSL, incluyendo todos los archivos, entornos y configuraciones internas. Usa este comando solo si quieres hacer una desinstalación total.

### Eliminar solo los archivos de GAP y su entorno

Si solo quieres borrar los archivos descargados e instalados por el script, puedes hacerlo manualmente desde la terminal de WSL:

```bash
rm -rf ~/gap-4.15.1.tar.gz ~/gap-4.15.1 ~/gap-env
```

## Problemas

Puedes abrir un issue o mandar un correo a juanmanuelfloresdelacruz@gmail.com.

### Tareas programadas/no realizadas

En caso de que algún error haga que el script no se realice de forma adecuada, puede ocurrir que las tareas se ejecuten cada vez que se reinicia el ordenador provocando un bucle si no se corta cerrando la ventana.
Para acabar con esto basta con ejecutar `eliminarTareas.bat`.

### VS Code no detecta el kernel de GAP

Asegúrate de que la carpeta abierta en VS Code **contiene** la carpeta generada por la instalación `gap_env`, no confundir con tener abierta esta última carpeta como raíz.

### No se genera el PDF

Prueba a instalar los paquetes siguientes dentro de WSL:

```bash
sudo apt-get install pandoc
sudo apt-get install texlive-xetex texlive-fonts-recommended texlive-plain-generic
```

*Fuente: [Nbconvert Installation](https://nbconvert.readthedocs.io/en/latest/install.html#installing-tex)*

-----

-----
## Purpose of this script
The purpose of this script is to let you use GAP in a Jupyter Notebook without worrying about complex setup details
## INSTRUCTIONS FOR USE

A correct execution simply involves running `install.bat` with administrator privileges and following the prompts. Please note that the process may require several system restarts.

### Execution Flow

The script consists of 3 key parts:

1.  **Checks Windows Features:** Verifies if the necessary features to run WSL are enabled.
      * If enabled, it does nothing.
      * If not enabled, it activates them and restarts the system.
2.  **Checks WSL Installation:** Verifies if WSL is installed.
      * If installed, it does nothing.
      * If not installed, it installs it and restarts the system.
3.  **Gap & Jupyter Setup:** Opens WSL, installs GAP, and configures Jupyter.

**The process flows as follows:**
`install.bat` -\> `activarCaracteristicas.ps1` -\> *(Restart if needed)* -\> `install.bat` -\> `instalarWsl.ps1` -\> *(Restart if needed)* -\> `finalgap.bat` -\> `setup-gap.sh`

## Installation Verification

Everything is installed within the **Windows Subsystem for Linux (WSL)**. You can access it by running in your terminal:

```cmd
wsl
```

The application is installed in the user's home folder `gap`, alongside a **Python environment** where the **GAP Kernel** is installed.

### Check GAP Installation

Run the following in the terminal:

```bash
gap
```

This should open the GAP interactive console, showing something similar to:

```text
 ┌───────┐   GAP 4.12.2, 64-bit
 │  GAP  │   [https://www.gap-system.org](https://www.gap-system.org)
 └───────┘   Architecture: x86_64-pc-linux-gnu-gcc-default64
 Type ? for help. 
gap>
```

To exit GAP, type:

```gap
quit;
```

### Check GAP Kernel Installation

Run the following from the user directory:

```bash
source ./gap-env/bin/activate
jupyter kernelspec list
```

The output should display:

```text
Available kernels:
  python3                -> .../share/jupyter/kernels/python3
  gap                    -> .../share/jupyter/kernels/gap
```

## Using GAP in Visual Studio Code

There are four important steps for proper operation:

1.  **Install the Jupyter Extension** from the VS Code Marketplace.
2.  **Connect VS Code to WSL** using the remote indicator in the bottom left corner.
3.  **Open the directory** `/user` in VS Code so that the `/env_gap` directory appears in the file explorer on the left.
4.  Open an `.ipynb` file or create a new one.
5.  **Select the Kernel:** In the top right (or top left depending on version), select **GAP**. If it is not detected, review the previous step regarding the directory.

Write and execute GAP code directly in the cells. Example:

```gap
G := SymmetricGroup(4);
Size(G);
```

## Uninstall

### Remove the Complete Ubuntu WSL Installation

If you wish to completely remove the Ubuntu distribution installed on WSL (including GAP and all its data), you can run:

```cmd
wsl --unregister Ubuntu
```

> ⚠️ **Warning:** This will delete the entire Ubuntu installation in WSL, including all files, environments, and internal configurations. Use this command only for a total uninstallation.

### Remove Only GAP Files and Environment

If you only want to delete the files downloaded and installed by the script (e.g., `gap-4.15.1.tar.gz`, `gap-4.15.1`, `gap-env`), you can do so manually from your user folder:

```bash
rm -rf ~/gap-4.15.1.tar.gz ~/gap-4.15.1 ~/gap-env
```

## Troubleshooting

You can open an issue or send an email to juanmanuelfloresdelacruz@gmail.com.

### Scheduled Tasks / Unfinished Tasks

If an error causes the script to fail improperly, tasks might execute every time the computer restarts, causing a loop if the window is not manually closed.
To stop this, simply run `eliminarTareas.bat`.

### VS Code Does Not Detect the GAP Kernel

Ensure that the folder opened in VS Code **contains** the generated folder `gap_env`. Do not confuse this with having the `gap_env` folder itself opened as the root.

### PDF Generation Fails

Try installing the following packages inside WSL:

```bash
sudo apt-get install pandoc
sudo apt-get install texlive-xetex texlive-fonts-recommended texlive-plain-generic
```

*Source: [Nbconvert Installation](https://nbconvert.readthedocs.io/en/latest/install.html#installing-tex)*
