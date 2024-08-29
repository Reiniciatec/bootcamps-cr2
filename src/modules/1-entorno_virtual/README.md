# IMPORTANTE!!!

No intentes ejecutar jupyter notebook en un entorno QUE NO SEA EL ENTORNO VIRTUAL. Si lo haces, considera que utilizarás las librerías del entorno global de Python, lo cual podría causar problemas de compatibilidad.

## ¿Cómo Configurar un Entorno Virtual con `virtualenv` e Instalar Librerías desde `requirements.txt`?

Este documento proporciona una guía paso a paso para configurar un entorno virtual utilizando `virtualenv` y para instalar las librerías necesarias desde un archivo `requirements.txt`.

## Tabla de Contenidos

- [IMPORTANTE!!!](#importante)
  - [¿Cómo Configurar un Entorno Virtual con `virtualenv` e Instalar Librerías desde `requirements.txt`?](#cómo-configurar-un-entorno-virtual-con-virtualenv-e-instalar-librerías-desde-requirementstxt)
  - [Tabla de Contenidos](#tabla-de-contenidos)
  - [Requisitos Previos](#requisitos-previos)
  - [Instalación de `virtualenv`](#instalación-de-virtualenv)
  - [Creación de un Entorno Virtual](#creación-de-un-entorno-virtual)
  - [Activación del Entorno Virtual](#activación-del-entorno-virtual)
  - [Solución a Error en PowerShell para Activar el Entorno Virtual](#solución-a-error-en-powershell-para-activar-el-entorno-virtual)
  - [Instalación de Librerías desde `requirements.txt`](#instalación-de-librerías-desde-requirementstxt)
  - [Desactivación del Entorno Virtual](#desactivación-del-entorno-virtual)
  - [Eliminación del Entorno Virtual](#eliminación-del-entorno-virtual)
  - [Recursos Adicionales](#recursos-adicionales)

## Requisitos Previos

- Python 3.x instalado en tu sistema.
- `pip` (Python package installer) instalado.

## Instalación de `virtualenv`

Antes de empezar, necesitas instalar `virtualenv`. Puedes instalarlo usando `pip` de la siguiente manera:

```bash
pip install virtualenv
```

Verifica la instalación con:

```bash
virtualenv --version
```

## Creación de un Entorno Virtual

Para crear un entorno virtual para tu proyecto, navega a la carpeta de tu proyecto en la terminal y ejecuta:

```bash
virtualenv nombre_del_entorno
```

Reemplaza `nombre_del_entorno` con el nombre que desees darle a tu entorno virtual. Este comando creará un directorio con ese nombre que contiene el entorno virtual.

## Activación del Entorno Virtual

Para activar el entorno virtual, ejecuta el siguiente comando dependiendo de tu sistema operativo:

- **Windows:**

  ```bash
  nombre_del_entorno\Scripts\activate
  ```

- **macOS y Linux:**

  ```bash
  source nombre_del_entorno/bin/activate
  ```

Una vez activado, deberías ver el nombre de tu entorno virtual al inicio de tu línea de comandos.

## Solución a Error en PowerShell para Activar el Entorno Virtual

En Windows, al intentar activar el entorno virtual usando PowerShell, podrías encontrar un error debido a la política de ejecución de scripts. Para resolver este problema, sigue estos pasos:

1. Abre PowerShell como administrador.
2. Cambia la política de ejecución para permitir la ejecución de scripts:

   ```bash
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

   Confirma el cambio si se te solicita.

3. Intenta activar el entorno virtual de nuevo:

   ```bash
   nombre_del_entorno\Scripts\activate
   ```

Si aún encuentras problemas, podrías intentar cambiar la política a `Unrestricted`, aunque esto no se recomienda para un uso regular debido a posibles riesgos de seguridad.

## Instalación de Librerías desde `requirements.txt`

Con el entorno virtual activado, puedes instalar todas las librerías necesarias para tu proyecto desde un archivo `requirements.txt` usando el siguiente comando:

```bash
pip install -r requirements.txt
```

Este comando leerá el archivo `requirements.txt` y instalará todas las librerías listadas.

## Desactivación del Entorno Virtual

Para desactivar el entorno virtual, simplemente ejecuta:

```bash
deactivate
```

Esto te devolverá al entorno global de Python.

## Eliminación del Entorno Virtual

Si ya no necesitas el entorno virtual, puedes eliminarlo simplemente borrando la carpeta correspondiente:

```bash
rm -rf nombre_del_entorno
```

## Recursos Adicionales

- [Documentación oficial de virtualenv](https://virtualenv.pypa.io/en/latest/)
- [Python Packaging User Guide](https://packaging.python.org/)
