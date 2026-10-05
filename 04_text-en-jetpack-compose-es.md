# Text en Jetpack Compose

> Aprende a usar y personalizar el composable Text en Jetpack Compose: tamaño, color, negrita, cursiva, número máximo de líneas y más.

*Básicos · 28 de enero de 2024 · 5 min de lectura*  
*Fuente (en inglés): <https://www.jetpackcompose.net/text-in-jetpack-compose>*

## ¿Qué es Text?

Si eres desarrollador de Android, es un ***TextView***.

Si eres nuevo en la programación Android, es simplemente una ***etiqueta*** (*label*) o un ***párrafo***.

## 1. Tamaño del texto

Cambia el tamaño del texto con el parámetro ***fontSize***.

```kotlin
@Composable
fun TextWithSize(label : String, size : TextUnit) {
    Text(label, fontSize = size)
}

//TextWithSize("Big text",40.sp) -- call this method
```

## 2. Color del texto

Cambia el color del texto con el parámetro ***color***.

```kotlin
@Composable
fun ColorText() {
  Text("Color text", color = Color.Blue)
}
```

## 3. Texto en negrita

Usa el parámetro ***fontWeight*** para poner el texto en negrita.

```kotlin
@Composable
fun BoldText() {
    Text("Bold text", fontWeight = FontWeight.Bold)
}
```

## 4. Texto en cursiva

Usa el parámetro ***fontStyle*** para poner el texto en cursiva.

```kotlin
@Composable
fun ItalicText() {
    Text("Italic Text", fontStyle = FontStyle.Italic)
}
```

## 5. Número máximo de líneas

Para limitar el número de líneas visibles en un composable Text, establece el parámetro `maxLines`:

```kotlin
@Composable
fun MaxLines() {
    Text("hello ".repeat(50), maxLines = 2)
}
```

## 6. Desbordamiento del texto

Al limitar un texto largo, puede que quieras indicar que hay desbordamiento, lo cual solo se muestra si el texto mostrado se trunca. Para ello, establece el parámetro `overflow`:

```kotlin
@Composable
fun OverflowedText() {
    Text("Hello Compose ".repeat(50), maxLines = 2, overflow = TextOverflow.Ellipsis)
}
```

## 7. Texto seleccionable

Por defecto, los composables no son seleccionables, lo que significa que los usuarios no pueden seleccionar ni copiar texto de tu aplicación. Para habilitar la selección de texto, debes envolver tus elementos de texto con un composable `SelectionContainer`:

```kotlin
@Composable
fun SelectableText() {
    SelectionContainer {
        Text("This text is selectable")
    }
}
```

### Resultado

![Resultado de los ejemplos de Text](images/0d004d_5ef7b46357394dcbb02d4111ad1782fb_mv2.jpg)

**Consulta la documentación oficial para más detalles**

<https://developer.android.com/jetpack/compose/text>

**Código fuente**

<https://github.com/JetpackCompose/Jetpack-Compose-Samples>
