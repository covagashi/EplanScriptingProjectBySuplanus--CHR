# Explicación del script MultiLanguageString.cs para EPLAN P8

## Propósito del script

Este script de C# para EPLAN P8 demuestra cómo crear y manejar cadenas de texto multilingües utilizando la clase `MultiLangString` de EPLAN. Es útil para desarrolladores que necesitan implementar soporte multilingüe en sus proyectos de EPLAN.

## Estructura y componentes principales

### 1. Importaciones

```csharp
using Eplan.EplApi.Base;
using Eplan.EplApi.Scripting;
```

Estas líneas importan las bibliotecas necesarias de EPLAN para trabajar con cadenas multilingües y scripting.

### 2. Definición de la clase

```csharp
class MultiLanguageString
{
    // ... (contenido de la clase)
}
```

Esta es la clase principal que contiene la lógica del script.

### 3. Método principal

```csharp
[Start]
public void Function()
{
    // ... (contenido del método)
}
```

Este es el método principal del script. El atributo `[Start]` indica que este método es el punto de entrada cuando se ejecuta el script.

## Funcionalidad clave

### Creación y manipulación de cadenas multilingües

1. El script crea una instancia de `MultiLangString`:
   ```csharp
   MultiLangString multiLangString = new MultiLangString();
   ```
   Esta clase permite almacenar el mismo texto en varios idiomas.

2. Añade versiones del texto en diferentes idiomas:
   ```csharp
   multiLangString.AddString(ISOCode.Language.L_en_EN, "My Text in English");
   multiLangString.AddString(ISOCode.Language.L_de_DE, "Mein Text in Deutsch");
   ```
   Aquí se añade el texto en inglés y alemán.

## Aspectos técnicos destacables

1. **Uso de MultiLangString**: Esta clase es fundamental para manejar texto en múltiples idiomas en EPLAN. Permite asociar diferentes versiones de un texto con códigos de idioma específicos.

2. **Códigos de idioma**: El script utiliza `ISOCode.Language` para especificar los idiomas. Por ejemplo, `L_en_EN` para inglés y `L_de_DE` para alemán.

3. **Extensibilidad**: Aunque el script solo muestra dos idiomas, la clase `MultiLangString` permite añadir tantos idiomas como sea necesario.



## Uso del script

Este script es principalmente demostrativo. En un escenario real, podrías:

1. Utilizar `MultiLangString` para almacenar textos que necesiten ser mostrados en múltiples idiomas.


