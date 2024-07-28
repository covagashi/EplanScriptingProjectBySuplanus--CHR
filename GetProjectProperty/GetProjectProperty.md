# Explicación intermedia del script GetProjectProperty.cs para EPLAN P8

## Propósito del script

Este script proporciona una funcionalidad para obtener propiedades específicas de un proyecto en EPLAN. Está diseñado como una acción personalizada que puede ser invocada desde otros scripts o componentes de EPLAN, permitiendo acceder a información detallada del proyecto.

## Estructura y componentes principales

### 1. Importaciones y namespace

```csharp
using System;
using System.IO;
using System.Windows.Forms;
using Eplan.EplApi.ApplicationFramework;
using Eplan.EplApi.Base;
using Eplan.EplApi.Scripting;

namespace EplanScriptingProjectBySuplanus.GetProjectProperty
{
    // ... (contenido del namespace)
}
```

El script utiliza bibliotecas estándar de .NET para manejo de archivos y formularios, así como las API específicas de EPLAN.

### 2. Clase principal: GetProjectProperty

Esta clase contiene la lógica para obtener una propiedad específica del proyecto.

### 3. Método principal: Action

```csharp
[DeclareAction("GetProjectProperty")]
public void Action(string id, string index, out string value)
{
    // ... (contenido del método)
}
```

Este método, decorado con `[DeclareAction("GetProjectProperty")]`, es el punto de entrada principal del script. Toma como parámetros el ID y el índice de la propiedad que se desea obtener, y devuelve el valor como un parámetro de salida.

## Funcionalidad clave

### 1. Preparación de archivos XML

```csharp
string pathTemplate = Path.Combine(PathMap.SubstitutePath("$(MD_SCRIPTS)"),
    "GetProjectProperty", "GetProjectProperty_Template.xml");
string pathScheme = Path.Combine(PathMap.SubstitutePath("$(MD_SCRIPTS)"),
    "GetProjectProperty", "GetProjectProperty_Scheme.xml");

string content = File.ReadAllText(pathTemplate);
content = content.Replace("GetProjectProperty_ID", id);
content = content.Replace("GetProjectProperty_INDEX", index);
File.WriteAllText(pathScheme, content);
```

Este código lee un archivo de plantilla XML, reemplaza placeholders con los valores de ID e índice proporcionados, y guarda el resultado en un nuevo archivo de esquema.

### 2. Configuración y exportación

```csharp
new Settings().ReadSettings(pathScheme);

string pathOutput = Path.Combine(
    PathMap.SubstitutePath("$(MD_SCRIPTS)"), "GetProjectProperty",
    "GetProjectProperty_Output.txt");

ActionCallingContext actionCallingContext = new ActionCallingContext();
actionCallingContext.AddParameter("configscheme", "GetProjectProperty");
actionCallingContext.AddParameter("destinationfile", pathOutput);
actionCallingContext.AddParameter("language", "en_US");
new CommandLineInterpreter().Execute("label", actionCallingContext);
```

Este bloque configura EPLAN con el esquema creado y luego ejecuta una acción de etiquetado para exportar la propiedad deseada a un archivo de texto.

### 3. Lectura del resultado

```csharp
value = File.ReadAllLines(pathOutput)[0];
```

Finalmente, el script lee la primera línea del archivo de salida, que contiene el valor de la propiedad solicitada.

## Aspectos técnicos destacables

1. **Uso de PathMap**: Utiliza `PathMap.SubstitutePath` para obtener rutas de directorios específicos de EPLAN, asegurando compatibilidad entre diferentes instalaciones.

2. **Manipulación de archivos XML**: Aunque no usa directamente clases XML, el script manipula archivos XML como texto para crear configuraciones personalizadas.

3. **Uso de la API de EPLAN**: Utiliza clases como `Settings`, `ActionCallingContext`, y `CommandLineInterpreter` para interactuar con EPLAN y ejecutar acciones específicas.

4. **Manejo de errores**: Implementa un bloque try-catch para manejar posibles errores y mostrar mensajes al usuario.

## Uso del script

El script está diseñado para ser utilizado por otros scripts o componentes. Un ejemplo de uso se proporciona en el comentario inicial:

```csharp
private static string GetProjectProperty(string id, string index)
{
    string value = null;
    ActionCallingContext actionCallingContext = new ActionCallingContext();
    actionCallingContext.AddParameter("id", id);
    actionCallingContext.AddParameter("index", index);
    new CommandLineInterpreter().Execute("GetProjectProperty", actionCallingContext);
    actionCallingContext.GetParameter("value", ref value);
    return value;
}
```

Este método auxiliar permite invocar fácilmente la acción "GetProjectProperty" y obtener el valor de una propiedad específica del proyecto.

Este script es particularmente útil para acceder a propiedades del proyecto que no están directamente disponibles a través de la API estándar de EPLAN, proporcionando una forma flexible de obtener información detallada del proyecto.

