# Explicación intermedia del script ExportProjectMissingTranslation para EPLAN P8

## Propósito del script

Este script exporta una lista de palabras no traducidas (Fehlworteliste) para el idioma actual del proyecto en EPLAN. Está diseñado para ayudar en la gestión de traducciones de proyectos multilingües.

## Estructura y componentes principales

### 1. Importaciones y declaración de namespace

```csharp
using System.IO;
using System.Windows.Forms;
using Eplan.EplApi.ApplicationFramework;
using Eplan.EplApi.Scripting;

namespace EplanScriptingProjectBySuplanus.ExportProjectMissingTranslation
{
    // ... (contenido del namespace)
}
```

El script utiliza bibliotecas estándar de .NET para manejo de archivos y formularios, así como las API específicas de EPLAN.

### 2. Método principal: Export_Txt_Fehlworte

Este método, decorado con `[DeclareAction("Export_Project_Missing_Translation")]`, es el punto de entrada principal del script. Realiza las siguientes operaciones:

1. Muestra un diálogo de confirmación.
2. Obtiene la ruta del proyecto actual.
3. Determina el idioma de visualización actual del proyecto.
4. Genera la lista de palabras no traducidas.
5. Lee el archivo generado y cuenta las líneas.
6. Si hay palabras no traducidas, abre el archivo en el Bloc de notas.

### 3. Métodos auxiliares

```csharp
public string Get_Project()
public string Get_Name(string sProj)
```

Estos métodos auxiliares se utilizan para obtener información sobre el proyecto actual y su nombre.

## Funcionalidad clave

### Generación de la lista de palabras no traducidas

```csharp
Eplan.EplApi.ApplicationFramework.ActionCallingContext acctranslate = new Eplan.EplApi.ApplicationFramework.ActionCallingContext();
// ... (configuración de parámetros)
bool sRet = CLItranslate.Execute("translate", acctranslate);
```

Este bloque de código utiliza la API de EPLAN para ejecutar la acción de traducción y exportar las palabras no traducidas a un archivo.

### Lectura y procesamiento del archivo

```csharp
if (File.Exists(MisTranslateFile))
{
    using (StreamReader countReader = new StreamReader(MisTranslateFile))
    {
        while (countReader.ReadLine() != null)
            counter++;
    }
    // ... (código para abrir el archivo si hay palabras no traducidas)
}
```

Este código lee el archivo generado, cuenta las líneas y, si hay más de una línea (indicando palabras no traducidas), abre el archivo en el Bloc de notas.

## Aspectos técnicos destacables

1. **Uso de la API de EPLAN**: El script hace un uso extensivo de las clases y métodos proporcionados por la API de EPLAN, como `ActionCallingContext`, `CommandLineInterpreter`, y `Progress`.

2. **Manejo de archivos**: Utiliza la clase `StreamReader` para leer y contar las líneas del archivo generado.

3. **Interacción con el usuario**: Utiliza `MessageBox` para mostrar diálogos y obtener confirmación del usuario.

4. **Ejecución de procesos externos**: Utiliza `System.Diagnostics.Process.Start` para abrir el Bloc de notas con el archivo generado.

5. **Manejo de contextos de acción**: Utiliza `ActionCallingContext` para configurar y ejecutar acciones específicas de EPLAN.

## Uso del script

1. El script se puede ejecutar desde EPLAN utilizando la acción "Export_Project_Missing_Translation".
2. Solicitará confirmación al usuario antes de proceder.
3. Generará un archivo de texto con las palabras no traducidas en la carpeta `C:\TEMP\EPLAN\`.
4. Si se encuentran palabras no traducidas, abrirá automáticamente el archivo en el Bloc de notas.

Este script es una herramienta útil para proyectos multilingües en EPLAN, ayudando a identificar y gestionar las traducciones faltantes de manera eficiente.

