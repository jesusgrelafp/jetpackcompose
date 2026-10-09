# Image en Jetpack Compose

> Aprende a mostrar y personalizar imágenes en Jetpack Compose: imagen simple, circular, con esquinas redondeadas, con color de fondo, con tinte (tint) y escala del contenido (content scale).

*Básicos · Actualizado · 12 min de lectura*  
*Fuente base (en inglés): <https://jetpackcompose.net>*

---

## Parámetros oficiales de la función Image

Antes de empezar a aprender, conviene conocer las opciones disponibles en la función `Image`. A continuación se detallan los parámetros incluidos en su firma, indicando la función exacta de cada uno mediante comentarios:

```kotlin
@Composable
fun Image(
    painter: Painter,                           // El objeto gráfico que se va a renderizar (obtenido comúnmente con painterResource).
    contentDescription: String?,                // Texto de accesibilidad para lectores de pantalla (puede establecerse como null).
    modifier: Modifier = Modifier,              // Modificador para aplicar tamaño, márgenes, formas, bordes o acciones de clic.
    alignment: Alignment = Alignment.Center,    // La alineación del gráfico dentro de los límites del contenedor si este es mayor.
    contentScale: ContentScale = ContentScale.Fit, // La regla de escala aplicada para adaptar la imagen a las dimensiones asignadas.
    alpha: Float = DefaultAlpha,                // Controla la opacidad visual del elemento (desde 0.0 transparente a 1.0 opaco).
    colorFilter: ColorFilter? = null            // Aplica filtros cromáticos, efectos o tintes directamente sobre los píxeles.
)
```

**Para crear una imagen necesitas los siguientes parámetros:**

**a) Painter**: para cargar un drawable desde los recursos necesitas usar `painterResource`. Debes pasar el id del recurso drawable como parámetro de `painterResource`, y te devolverá el painter.

```kotlin
fun painterResource(@DrawableRes id: Int): Painter
```

**b) ContentDescription**: debes dar una descripción de la imagen. Puedes establecerla como `null`.

**c) Modifier (opcional)**: si no usas el modifier, `Image` tomará como tamaño el tamaño original del recurso. Por eso conviene usar el modifier para fijar un tamaño y evitar problemas de diseño.

---

## Opciones de Personalización y Diseño Básicos

### 1. Imagen simple

**Código de ejemplo:**

```kotlin
@Composable
fun SimpleImage() {
    Image(
        painter = painterResource(id = R.drawable.andy_rubin),
        contentDescription = "Andy Rubin",
        modifier = Modifier.fillMaxWidth()
    )
}
```

Aquí se establece el drawable con `painterResource` y se aplica el modificador ***fillMaxWidth()***, que hace que la imagen ocupe todo el ancho de la pantalla.

**Resultado:**

![Imagen simple](images/0d004d_47c6d0713da34afa841b84efa7a2b6e5_mv2.png)

### 2. Imagen circular

**Código de ejemplo:**

```kotlin
@Composable
fun CircleImageView() {
    Image(
        painter = painterResource(R.drawable.andy_rubin),
        contentDescription = "Circle Image",
        contentScale = ContentScale.Crop,
        modifier = Modifier
            .size(128.dp)
            .clip(CircleShape) // Recorta el componente en forma de círculo perfecto
            .border(5.dp, Color.Gray, CircleShape) // Añade un contorno periférico opcional
    )
}
```

Se recorta la forma a **CircleShape**, de modo que toda la imagen se convierte en un círculo. Además se añade un borde gris alrededor de la imagen. El borde es opcional: si no se requiere, puede omitirse.

**Resultado:**

![Imagen circular](images/0d004d_f052882da9e44ad5a62836fc6b94e00e_mv2.png)

### 3. Imagen con esquinas redondeadas

**Código de ejemplo:**

```kotlin
@Composable
fun RoundCornerImageView() {
    Image(
        painter = painterResource(R.drawable.andy_rubin),
        contentDescription = "Round corner image",
        contentScale = ContentScale.Crop,
        modifier = Modifier
            .size(128.dp)
            .clip(RoundedCornerShape(10))
            .border(5.dp, Color.Gray, RoundedCornerShape(10))
    )
}
```

Es igual que el ejemplo anterior de la imagen circular. La única diferencia es que se cambia la forma de recorte a *RoundedCornerShape()*.

*   Si se requiere indicar un porcentaje, se debe pasar un valor entero: ***RoundedCornerShape(20)***
*   Si se requiere indicar un valor en Dp, se pasa el valor en Dp: ***RoundedCornerShape(50.dp)***

### 4. Color de fondo de la imagen

**Código de ejemplo:**

```kotlin
@Composable
fun ImageWithBackgroundColor() {
    Image(
        painter = painterResource(id = R.drawable.ic_cart),
        contentDescription = "",
        modifier = Modifier
            .size(200.dp)
            .background(Color.DarkGray)
            .padding(20.dp)
    )
}
```

En este ejemplo se usa un icono PNG como recurso. Si se utiliza un JPEG/JPG no se percibirá el color de fondo, porque ese formato no admite canales de transparencia. Se usa el modificador **background()** para establecer el color de fondo de esta imagen.

### 5. ColorFilter de la imagen (tint)

**Código de ejemplo:**

```kotlin
@Composable
fun ImageWithTint() {
    Image(
        painter = painterResource(id = R.drawable.ic_cart),
        contentDescription = "",
        colorFilter = ColorFilter.tint(Color.Red),
        modifier = Modifier
            .size(200.dp)
    )
}
```

Con ayuda de `tint()` se puede cambiar el color del recurso de la imagen de manera dinámica. Es posible establecer cualquier color mediante el filtro de color.

```kotlin
colorFilter = ColorFilter.tint(Color.Red)
```

---

## 6. Configuración de Escala (ContentScale)

El parámetro `contentScale` determina cómo se estira, recorta o adapta la imagen original para ajustarse a los límites físicos definidos en el modificador de tamaño del contenedor. Las opciones disponibles y sus comportamientos exactos son:

*   **`ContentScale.Fit` (Por defecto):** Mantiene la relación de aspecto original de la imagen y la escala de forma uniforme hasta que uno de sus bordes (ancho o alto) coincide con el límite del contenedor. Toda la imagen permanece visible sin recortarse.
*   **`ContentScale.Crop`:** Escala la imagen de manera uniforme manteniendo su relación de aspecto hasta que llena por completo el espacio asignado tanto a lo ancho como a lo alto. Si las proporciones de la imagen y del contenedor difieren, las partes sobrantes se recortan.
*   **`ContentScale.FillBounds`:** Estira o comprime la imagen de forma no uniforme para forzarla a ocupar exactamente el ancho y el alto asignados. Esto puede provocar una deformación visual si las proporciones originales no coinciden con las del contenedor.
*   **`ContentScale.FillWidth`:** Escala la imagen manteniendo su relación de aspecto original de modo que el ancho del gráfico coincida exactamente con el ancho asignado al contenedor, lo que puede provocar recortes verticales si el contenedor es más bajo.
*   **`ContentScale.FillHeight`:** Escala la imagen manteniendo su relación de aspecto original de modo que la altura del gráfico coincida exactamente con la altura asignada al contenedor, lo que puede provocar recortes horizontales si el contenedor es más estrecho.
*   **`ContentScale.Inside`:** Mantiene la imagen centrada con su relación de aspecto original. Si la imagen es más grande que el contenedor, funciona exactamente como `Fit` reduciendo su tamaño. Si la imagen es más pequeña que el contenedor, conserva sus dimensiones originales sin expandirse ni pixelarse.

**Código de ejemplo:**

```kotlin
@Composable
fun InsideFit() {
    Image(
        painter = painterResource(id = R.drawable.andy_rubin),
        contentDescription = "",
        modifier = Modifier
            .size(150.dp)
            .background(Color.LightGray),
        contentScale = ContentScale.Inside
    )
}
```

---

**Código fuente y recursos adicionales**

<https://github.com>
