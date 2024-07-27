# Explicación del script AddProjectLanguage.cs para EPLAN P8

## Introducción

Este documento explica un script de C# diseñado para EPLAN P8. El script se utiliza para añadir idiomas de traducción a un proyecto en EPLAN. Está pensado para personas con conocimientos básicos de programación.

## ¿Qué hace este script?

Este script agrega idiomas de traducción a un proyecto de EPLAN. Específicamente:

1. Añade alemán (de_DE), inglés (en_EN) y chino (zh_CN) como idiomas de traducción al proyecto.
2. No cambia el idioma de visualización del proyecto, solo añade estos idiomas para su posible traducción.

## Cómo funciona técnicamente

Vamos a desglosar el script en partes más pequeñas para entenderlo mejor:

### 1. Importación de bibliotecas

```csharp
using Eplan.EplApi.ApplicationFramework;
using Eplan.EplApi.Scripting;
```

Estas líneas importan las bibliotecas necesarias de EPLAN para que el script pueda interactuar con el software.

### 2. Definición de la clase

```csharp
internal class AddProjectLanguageClass
{
    // ... (contenido de la clase)
}
```

Esta es la definición de la clase principal del script. Todo el código estará dentro de esta clase.

### 3. Método principal

```csharp
[Start]
public void XAfActionSettingProject_Start()
{
    // ... (contenido del método)
}
```

Este es el método principal del script. El atributo `[Start]` indica que este método es el punto de entrada cuando se ejecuta el script.

### 4. Creación de objetos

```csharp
CommandLineInterpreter oCLI = new CommandLineInterpreter();
ActionCallingContext oACC = new ActionCallingContext();
```

Aquí se crean dos objetos importantes:
- `oCLI`: Un intérprete de línea de comandos para ejecutar acciones en EPLAN.
- `oACC`: Un contexto para pasar parámetros a la acción que vamos a ejecutar.

### 5. Configuración de parámetros

```csharp
oACC.AddParameter("set", "TRANSLATEGUI.TRANSLATE_LANGUAGES");
oACC.AddParameter("value", "de_DE;en_EN;zh_CN;");
```

Estas líneas añaden parámetros al contexto de la acción:
- El primer parámetro indica qué configuración vamos a modificar (los idiomas de traducción).
- El segundo parámetro especifica los idiomas que queremos añadir (alemán, inglés y chino).

### 6. Ejecución de la acción

```csharp
oCLI.Execute("XAfActionSettingProject", oACC);
```

Esta línea ejecuta la acción `XAfActionSettingProject` con los parámetros que hemos configurado, lo que efectivamente añade los idiomas de traducción al proyecto.

## Cómo usar el script

1. Guarda el script como un archivo con extensión `.cs` (por ejemplo, `AddProjectLanguage.cs`).
2. En EPLAN, ve a [Utilidades] > [Scripts] > [Ejecutar].
3. Selecciona el archivo del script que acabas de guardar.
4. El script se ejecutará, añadiendo los idiomas de traducción a tu proyecto.
