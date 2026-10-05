# Image en Jetpack Compose

> Aprende a mostrar y personalizar imágenes en Jetpack Compose: imagen simple, circular, con esquinas redondeadas, con color de fondo, con tinte (tint) y escala del contenido (content scale).

*Básicos · 8 de febrero de 2024 · 9 min de lectura*  
*Fuente (en inglés): <https://www.jetpackcompose.net/image-in-jetpack-compose>*

Antes de empezar a aprender, conviene conocer las opciones disponibles en la función `Image`.

Estas son las opciones disponibles en `Image`:

```kotlin
@Composable
fun Image(
    painter: Painter,
    contentDescription: String?,
    modifier: Modifier = Modifier,
    alignment: Alignment = Alignment.Center,
    contentScale: ContentScale = ContentScale.Fit,
    alpha: Float = DefaultAlpha,
    colorFilter: ColorFilter? = null
)
```

**Para crear una imagen necesitas los siguientes parámetros:**

**a) Painter**: para cargar un drawable desde los recursos necesitas usar `painterResource`.

Debes pasar el id del recurso drawable como parámetro de `painterResource`, y te devolverá el painter.

```kotlin
fun painterResource(@DrawableRes id: Int): Painter
```

**b) ContentDescription**: debes dar una descripción de la imagen. Puedes establecerla como `null`.

**c) Modifier (opcional)**: si no usas el modifier, `Image` tomará como tamaño el tamaño original del recurso. Por eso conviene usar el modifier para fijar un tamaño y evitar problemas de diseño.

## 1. Imagen simple

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

Aquí establecemos el drawable con `painterResource` y aplicamos el modificador ***fillMaxWidth()***, que hace que la imagen ocupe todo el ancho de la pantalla.

**Resultado:**

![Imagen simple](images/0d004d_47c6d0713da34afa841b84efa7a2b6e5_mv2.png)

## 2. Imagen circular

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
            .clip(CircleShape) // clip to the circle shape
            .border(5.dp, Color.Gray, CircleShape)//optional
    )
}
```

Recortamos la forma a **CircleShape**, de modo que toda la imagen se convierte en un círculo. Además añadimos un borde gris alrededor de la imagen. El borde es opcional: si no lo quieres, puedes omitirlo.

**Resultado:**

![Imagen circular](images/0d004d_f052882da9e44ad5a62836fc6b94e00e_mv2.png)

## 3. Imagen con esquinas redondeadas

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

Es igual que el ejemplo anterior de la imagen circular. La única diferencia es que cambiamos la forma de recorte a *RoundedCornerShape()*.

Si quieres indicar un porcentaje, debes pasar un valor entero: ***RoundedCornerShape(20)***

Si quieres indicar un valor en Dp, pasa el valor en Dp: ***RoundedCornerShape(50.dp)***

## 4. Color de fondo de la imagen

**Código de ejemplo:**

```kotlin
@Composable
fun ImageWithBackgroundColor() {
    Image(
        painter = painterResource(id = R.drawable.ic_cart),
        contentDescription = "",
        modifier = Modifier
            .size( 200.dp)
            .background(Color.DarkGray)
            .padding(20.dp)
    )
}
```

En este ejemplo usamos un icono PNG como recurso. Si usas un JPEG/JPG no verás el color de fondo, porque ese formato no tiene fondo transparente.

Usamos el modificador **background()** para establecer el color de fondo de esta imagen.

## 5. ColorFilter de la imagen (tint)

**Código de ejemplo:**

```kotlin
@Composable
fun ImageWithTint() {
    Image(
        painter = painterResource(id = R.drawable.ic_cart),
        contentDescription = "",
        colorFilter = ColorFilter.tint(Color.Red),
        modifier = Modifier
            .size( 200.dp)
    )
}
```

Con ayuda de `tint()` podemos cambiar el color del recurso de la imagen. Puedes establecer cualquier color mediante el filtro de color.

```kotlin
colorFilter = ColorFilter.tint(Color.Red)
```

## 6. ContentScale

Estos son los tipos de `ContentScale` disponibles en Compose:

- `FillBounds`
- `FillHeight`
- `FillWidth`
- `Inside`
- `Fit`
- `Crop`

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

**Código fuente:**

<https://github.com/JetpackCompose/Jetpack-Compose-Samples>
