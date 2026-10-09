# Text en Jetpack Compose

> Aprende a usar y personalizar el composable Text en Jetpack Compose: tamaño, color, negrita, cursiva, número máximo de líneas y más.

*Básicos · 28 de enero de 2024 · 10 min de lectura*  
*Fuente base (en inglés): <https://jetpackcompose.net>*

---

## ¿Qué es Text?

Si eres desarrollador de Android clásico, equivale al componente ***TextView***.

Si eres nuevo en la programación Android, representa simplemente una ***etiqueta*** (*label*) o un ***párrafo*** de texto dentro de la interfaz.

### Parámetros oficiales de la función Text
A continuación se muestran los parámetros más comunes incluidos en la firma del constructor de `Text`:

```kotlin
Text(
    text = "Texto a mostrar",
    modifier = Modifier,
    color = Color.Unspecified,
    fontSize = TextUnit.Unspecified,
    fontStyle = null,
    fontWeight = null,
    fontFamily = null,
    letterSpacing = TextUnit.Unspecified,
    textDecoration = null,
    textAlign = null,
    lineHeight = TextUnit.Unspecified,
    overflow = TextOverflow.Clip,
    softWrap = true,
    maxLines = Int.MAX_VALUE,
    style = LocalTextStyle.current
)
```

---

## Opciones de Personalización Básica

### 1. Tamaño del texto
Modifica el tamaño del texto mediante el parámetro `fontSize`. Es necesario utilizar unidades de medida adaptables `sp` (Scale-independent Pixels).

```kotlin
@Composable
fun TextWithSize(label : String, size : TextUnit) {
    Text(label, fontSize = size)
}

// Ejemplo de llamada: TextWithSize("Big text", 40.sp)
```

### 2. Color del texto
Modifica el color del texto mediante el parámetro `color`.

```kotlin
@Composable
fun ColorText() {
    Text("Color text", color = Color.Blue)
}
```

### 3. Texto en negrita
Usa el parámetro `fontWeight` para definir el grosor del texto.

```kotlin
@Composable
fun BoldText() {
    Text("Bold text", fontWeight = FontWeight.Bold)
}
```

### 4. Texto en cursiva
Usa el parámetro `fontStyle` para inclinar el texto en estilo itálico o cursiva.

```kotlin
@Composable
fun ItalicText() {
    Text("Italic Text", fontStyle = FontStyle.Italic)
}
```

---

## Control de Extensión y Estructura

### 5. Número máximo de líneas
Para limitar la cantidad de líneas visibles en un composable `Text` cuando el contenido es demasiado largo, se establece el parámetro `maxLines`.

```kotlin
@Composable
fun MaxLines() {
    Text("hello ".repeat(50), maxLines = 2)
}
```

### 6. Desbordamiento del texto
Al limitar la longitud de un texto, se suele indicar visualmente que el contenido ha sido recortado. Para ello, se configura el parámetro `overflow`, el cual aplica un formato de truncado (como puntos suspensivos) únicamente si el texto supera el espacio asignado.

```kotlin
@Composable
fun OverflowedText() {
    Text("Hello Compose ".repeat(50), maxLines = 2, overflow = TextOverflow.Ellipsis)
}
```

### 7. Texto seleccionable
Por defecto, los composables de tipo `Text` no admiten selección por parte del usuario, lo que impide copiar el texto en la aplicación. Para habilitar la interactividad de copiado, se deben envolver los elementos correspondientes con el contenedor `SelectionContainer`.

```kotlin
@Composable
fun SelectableText() {
    SelectionContainer {
        Text("This text is selectable")
    }
}
```

---

## Posicionamiento y Estilos Avanzados

### 8. Alineación del texto
Para alinear el texto de forma horizontal dentro de los límites asignados a su contenedor (izquierda, centro, derecha o justificado), se utiliza el parámetro `textAlign`.

```kotlin
@Composable
fun AlignedText() {
    Text(
        text = "Texto centrado",
        modifier = Modifier.fillMaxWidth(),
        textAlign = TextAlign.Center
    )
}
```

### 9. Familias de fuentes (Tipografía)
El parámetro `fontFamily` permite alternar entre las diferentes fuentes del sistema o bien estructurar fuentes personalizadas cargadas desde los recursos de la aplicación (archivos `.ttf` o `.otf` almacenados en el directorio `res/font`).

```kotlin
@Composable
fun CustomFontText() {
    Text(
        text = "Texto con fuente Monospace",
        fontFamily = FontFamily.Monospace
    )
}
```

### 10. Estilos y Material Design
En lugar de definir de manera individual el tamaño, el color y las propiedades tipográficas en cada elemento independiente, se recomienda utilizar el parámetro `style`. Este parámetro permite aplicar configuraciones estandarizadas del tema global del sistema o implementar estructuras reutilizables mediante `TextStyle`.

```kotlin
@Composable
fun StyledText() {
    Column {
        // Implementación del sistema de tipografía global de Material Theme
        Text(
            text = "Título Principal",
            style = MaterialTheme.typography.titleLarge
        )
        
        // Configuración de un TextStyle personalizado con interlineado estructurado
        Text(
            text = "Párrafo con interlineado y espaciado de letras específicos.",
            style = TextStyle(
                lineHeight = 24.sp,
                letterSpacing = 1.5.sp
            )
        )
    }
}
```

---

### Resultado General

![Resultado de los ejemplos de Text](images/0d004d_5ef7b46357394dcbb02d4111ad1782fb_mv2.jpg)

**Consulta la documentación oficial para más detalles**

<https://android.com>

**Código fuente**

<https://github.com>
