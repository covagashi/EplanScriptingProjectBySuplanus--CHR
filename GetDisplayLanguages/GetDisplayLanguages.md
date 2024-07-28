# Explicación intermedia del script GetDisplayLanguages.cs para EPLAN P8

## Propósito del script

Este script proporciona una funcionalidad para obtener los idiomas de visualización configurados en un proyecto de EPLAN. Está diseñado como una acción dentro del entorno de EPLAN, permitiendo a otros scripts o componentes acceder fácilmente a esta información.

## Estructura y componentes principales

### 1. Importaciones y namespace

```csharp
using System.IO;
using System.Xml;
using Eplan.EplApi.ApplicationFramework;
using Eplan.EplApi.Base;
using Eplan.EplApi.Scripting;

namespace EplanScriptingProjectBySuplanus.GetDisplayLanguages
{
    // ... (contenido del namespace)
}
```

El script utiliza bibliotecas estándar de .NET para manejo de archivos y XML, así como las API específicas de EPLAN.

### 2. Clase principal: GetDisplayLanguages

Esta clase contiene toda la lógica para obtener los idiomas de visualización del proyecto.

### 3. Método principal: Action

```csharp
[DeclareAction("GetDisplayLanguages")]
public void Action(out string value)
{
    // ... (contenido del método)
}
```

Este método, decorado con `[DeclareAction("GetDisplayLanguages")]`, es el punto de entrada principal del script. Realiza las siguientes operaciones:

1. Obtiene la ruta del proyecto actual.
2. Exporta la configuración relevante a un archivo XML temporal.
3. Lee el archivo XML para extraer los idiomas de visualización configurados.

### 4. Métodos auxiliares

```csharp
private static string GetValueSettingsXml(string filename, string url)
private static string FullProjectPath()
```

Estos métodos auxiliares se utilizan para leer valores específicos del archivo XML de configuración y para obtener la ruta completa del proyecto actual.

## Funcionalidad clave

### Exportación de configuración

```csharp
string tempFile = Path.Combine(PathMap.SubstitutePath("$(TMP)"), "GetDisplayLanguages.xml");

ActionCallingContext actionCallingContext = new ActionCallingContext();
actionCallingContext.AddParameter("prj", FullProjectPath());
actionCallingContext.AddParameter("node", "TRANSLATEGUI");
actionCallingContext.AddParameter("XMLFile", tempFile);
new CommandLineInterpreter().Execute("XSettingsExport", actionCallingContext);
```

Este bloque exporta la configuración relevante del proyecto a un archivo XML temporal.

### Lectura de idiomas de visualización

```csharp
string language = GetValueSettingsXml(tempFile, "/Settings/CAT/MOD/Setting[@name='DISPLAYED_LANGUAGES']/Val");
value = language;
```

Este código lee los idiomas de visualización del archivo XML exportado.

## Aspectos técnicos destacables

1. **Uso de la API de EPLAN**: El script utiliza `ActionCallingContext` y `CommandLineInterpreter` para interactuar con EPLAN y exportar configuraciones.

2. **Manejo de XML**: Utiliza `XmlDocument` para leer y extraer información específica del archivo XML de configuración.

3. **Parámetros de salida**: El método principal utiliza un parámetro `out` para devolver el resultado, lo cual es común en la API de EPLAN.

4. **Uso de PathMap**: Utiliza `PathMap.SubstitutePath` para obtener la ruta temporal del sistema, asegurando compatibilidad entre diferentes configuraciones de EPLAN.

## Uso del script

1. El script se puede invocar desde otros scripts o componentes de EPLAN usando la acción "GetDisplayLanguages".
2. Retorna una cadena con los idiomas de visualización del proyecto separados por ';'.
3. Si no se encuentran idiomas o hay un error, retorna `null`.

## Nota sobre el uso proporcionado

El ejemplo de uso en el comentario al inicio del script muestra cómo se puede procesar aún más el resultado:

```csharp
var split = value.Split(';');
var languages = split.Where(language => !string.IsNullOrEmpty(language)).ToList();
```

Esto divide la cadena de idiomas en una lista, eliminando cualquier entrada vacía, lo que puede ser útil para el procesamiento posterior.

Este script es particularmente útil para cualquier funcionalidad en EPLAN que necesite conocer los idiomas de visualización configurados en el proyecto actual, como herramientas de interfaz de usuario multilingüe o generación de informes.

