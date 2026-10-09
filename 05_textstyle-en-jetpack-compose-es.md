# TextStyle en Jetpack Compose

> Da estilo a tu texto con TextStyle en Jetpack Compose: color, sombra, familia tipográfica, tamaño de fuente, decoración del texto y más.

*Básicos · Actualizado · 7 min de lectura*  
*Fuente (en inglés): <https://jetpackcompose.net>*

---

## Introducción

El texto desempeña un papel importante en las aplicaciones móviles y web: mediante él presentamos los detalles al usuario. Para ofrecer una experiencia de usuario óptima y mantener una jerarquía visual clara, es fundamental personalizar las tipografías. Modificar el tamaño, color y peso visual según el contexto ayuda a guiar la lectura. En Jetpack Compose, la herramienta principal para lograr esto es el objeto `TextStyle`.

En Jetpack Compose podemos usar las siguientes opciones para aplicar un `TextStyle()`, desglosando cada parámetro mediante comentarios explicativos:

```kotlin
Text(
    text = "Hello World",
    style = TextStyle(
        color = Color.Red,                      // El color cromático aplicado a los caracteres del texto.
        fontSize = 16.sp,                       // El tamaño de la tipografía utilizando unidades .sp adaptables.
        fontFamily = FontFamily.Monospace,       // La familia tipográfica o fuente del sistema / archivo personalizado.
        fontWeight = FontWeight.W800,           // El grosor o peso del trazo (negrita, fina, normal, etc.).
        fontStyle = FontStyle.Italic,           // Determina la inclinación del texto (Normal o Cursiva/Itálica).
        letterSpacing = 0.5.em,                 // El espacio adicional horizontal entre cada letra en unidades .em o .sp.
        background = Color.LightGray,           // El color de fondo del cuadro contenedor que delimita el texto.
        textDecoration = TextDecoration.Underline // Adornos visuales añadidos como el subrayado o el tachado.
    )
)
```

---

## Opciones de Personalización Individual

### 1. Color del texto
```kotlin
Text(
    text = "Text with Color",
    style = TextStyle(color = Color.Red)
)
```

### 2. Color de fondo
```kotlin
Text(
    text = "Text with Background Color",
    style = TextStyle(background = Color.Yellow)
)
```

### 3. Sombra
Es posible añadir efectos de profundidad y relieve al texto configurando la propiedad `shadow`, la cual requiere un objeto de tipo `Shadow` para definir su color, desplazamiento espacial y difuminado.

```kotlin
Text(
    text = "Text with Shadow",
    style = TextStyle(
        shadow = Shadow(
            color = Color.Black,        // Color de la sombra proyectada.
            offset = Offset(5f, 5f),    // Desplazamiento en los ejes X e Y medido en píxeles flotantes.
            blurRadius = 5f             // Radio de difuminado o suavizado aplicado al contorno de la sombra.
        )
    )
)
```

### 4. Familia tipográfica (Font Family)
Se pueden usar fuentes predefinidas del sistema o cargar tipografías personalizadas desde los recursos del proyecto.

```kotlin
val Default: SystemFontFamily = DefaultFontFamily()
val SansSerif = GenericFontFamily("sans-serif")
val Serif = GenericFontFamily("serif")
val Monospace = GenericFontFamily("monospace")
val Cursive = GenericFontFamily("cursive")
```

**Ejemplo de uso:**
```kotlin
Text(
    text = "Text with custom font",
    style = TextStyle(fontSize = 20.sp, fontFamily = FontFamily.Cursive)
)
```

### 5. Tamaño de fuente
```kotlin
Text(
    text = "Text with big font size",
    style = TextStyle(fontSize = 30.sp)
)
```

### 6. Estilo de fuente
Permite conmutar la apariencia estructural básica mediante las opciones `FontStyle.Normal` o `FontStyle.Italic`.

```kotlin
Text(
    text = "Text with Italic text",
    style = TextStyle(fontSize = 20.sp, fontStyle = FontStyle.Italic)
)
```

### Resultado General

![Resultado de TextStyle](images/0d004d_1496676c3f9a423ab64bd35ebb6e89cb_mv2.png)

---

## 7. Decoración del texto

El parámetro `textDecoration` añade líneas estructurales suplementarias a los caracteres impresos. Las dos opciones principales son:

*   `TextDecoration.Underline`: Dibuja una línea horizontal continua por debajo del texto.
*   `TextDecoration.LineThrough`: Dibuja una línea horizontal que atraviesa el texto de forma central (tachado).

```kotlin
@Composable
fun TextDecorationStyle() {
    Column {
        Text(
            text = "Text with Underline",
            style = TextStyle(
                color = Color.Black, 
                fontSize = 24.sp,
                textDecoration = TextDecoration.Underline
            )
        )
        Text(
            text = "Text with Strike",
            style = TextStyle(
                color = Color.Blue, 
                fontSize = 24.sp,
                textDecoration = TextDecoration.LineThrough
            )
        )
    }
}
```

![Resultado de la decoración del texto](images/0d004d_9dc54d113242487b95e97c93a35463bf_mv2.png)

---

## Tipografía centralizada (Typography)

Para mantener la consistencia estética y facilitar el mantenimiento del diseño global en proyectos grandes, se recomienda evitar la inserción manual de valores duros en cada componente. En su lugar, se utiliza el sistema de tipografías centralizado de `MaterialTheme`.

Las opciones de escala tipográfica estructuradas en el sistema de diseño de Material Design se categorizan en grupos (como *Display*, *Headline*, *Title*, *Body* y *Label*), ofreciendo configuraciones preestablecidas listas para su reutilización.

![Opciones de tipografía](images/0d004d_ceee1f1eac034223aa551aa2833bac2a_mv2.png)

**Código de ejemplo:**
```kotlin
@Composable
fun TextHeadingStyle() {
    Column(
        modifier = Modifier
            .fillMaxWidth()
            .background(Color.Green)
    ) {
        Text(
            text = "Heading 3",
            style = MaterialTheme.typography.h3 // Estilo jerárquico de gran tamaño
        )
        Text(
            text = "Heading 4",
            style = MaterialTheme.typography.h4
        )
        Text(
            text = "Heading 5",
            style = MaterialTheme.typography.h5
        )
    }
}
```

### Resultado de la tipografía

![Resultado de la tipografía](images/0d004d_e91847b29a2542669c74499514ba9f84_mv2.png)

---
