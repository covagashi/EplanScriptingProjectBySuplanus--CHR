# Explicación del script LoadUnloadAllScripts.cs para EPLAN P8

## Propósito del script

Este script de C# para EPLAN P8 proporciona funcionalidades para cargar y descargar todos los scripts en una carpeta específica de EPLAN. Además, añade opciones de menú para ejecutar estas acciones fácilmente desde la interfaz de EPLAN.

## Estructura y componentes principales

### 1. Importaciones

```csharp
using System.IO;
using System.Windows.Forms;
using Eplan.EplApi.ApplicationFramework;
using Eplan.EplApi.Base;
using Eplan.EplApi.Scripting;
```

Estas líneas importan las bibliotecas necesarias para trabajar con archivos, formularios de Windows, y la API de EPLAN.

### 2. Definición de la clase principal

```csharp
public class RegisterScriptMenu
{
    // ... (contenido de la clase)
}
```

Esta es la clase principal que contiene toda la lógica del script.

### 3. Métodos principales

El script contiene tres métodos principales:

1. `MenuFunction()`: Configura las opciones de menú en EPLAN.
2. `LoadScriptsProject()`: Carga todos los scripts.
3. `UnloadScriptsProject()`: Descarga todos los scripts.

## Funcionalidad clave

### Configuración del menú

El método `MenuFunction()` añade dos nuevas opciones al menú de EPLAN:

1. "Load all scripts": Para cargar todos los scripts.
2. "Unload all scripts": Para descargar todos los scripts.

```csharp
[Start]
[DeclareMenu()]
public void MenuFunction()
{
    // ... (código para añadir elementos de menú)
}
```

### Carga de scripts

El método `LoadScriptsProject()` realiza las siguientes acciones:

1. Obtiene la ruta de la carpeta de scripts de EPLAN.
2. Busca todos los archivos `.cs` y `.vb` en esa carpeta y sus subcarpetas.
3. Carga cada script encontrado utilizando la acción "RegisterScript" de EPLAN.
4. Muestra un mensaje con la lista de scripts cargados.

```csharp
[DeclareAction("LoadScripts")]
public void LoadScriptsProject()
{
    // ... (código para cargar scripts)
}
```

### Descarga de scripts

El método `UnloadScriptsProject()` realiza acciones similares, pero para descargar los scripts:

1. Obtiene la ruta de la carpeta de scripts.
2. Busca todos los archivos `.cs` y `.vb`.
3. Descarga cada script utilizando la acción "UnRegisterScript" de EPLAN.
4. Muestra un mensaje informando que todos los scripts han sido descargados.

```csharp
[DeclareAction("UnloadScripts")]
public void UnloadScriptsProject()
{
    // ... (código para descargar scripts)
}
```

## Aspectos técnicos destacables

1. **Uso de atributos**: El script utiliza atributos como `[Start]`, `[DeclareMenu()]`, y `[DeclareAction()]` para integrar las funcionalidades con EPLAN.

2. **Manipulación de archivos**: Utiliza `System.IO.DirectoryInfo` y `GetFiles()` para buscar archivos en carpetas y subcarpetas.

3. **Interacción con EPLAN**: Usa `CommandLineInterpreter` y `ActionCallingContext` para ejecutar acciones de EPLAN programáticamente.

4. **Interfaz de usuario**: Emplea `MessageBox.Show()` para proporcionar retroalimentación al usuario sobre las acciones realizadas.

5. **Manejo de rutas**: Usa `PathMap.SubstitutePath()` para obtener la ruta correcta de los scripts en EPLAN.

## Uso del script

1. Carga este script en EPLAN.
2. Verás dos nuevas opciones en el menú de EPLAN:
   - "Load all scripts" en el menú "Utilities > Scripts > To Run"
   - "Unload all scripts" en el menú "Utilities > Scripts > Unload"
3. Usa estas opciones para cargar o descargar todos los scripts en la carpeta de scripts de EPLAN.


