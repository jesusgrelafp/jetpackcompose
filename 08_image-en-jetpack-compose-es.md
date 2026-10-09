# Image en Jetpack Compose

> Aprende a mostrar y personalizar imágenes en Jetpack Compose: imagen simple, circular, con esquinas redondeadas, con color de fondo, con tinte (tint) y escala del contenido (content scale).

*Básicos · Actualizado · 12 min de lectura*  
*Fuente base (en inglés): <https://jetpackcompose.net>*

---

## Parámetros oficiales de la función Image

A continuación se muestran los parámetros incluidos en la firma del constructor de `Image`, detallando la función de cada propiedad:

```kotlin
@Composable
fun Image(
    painter: Painter,                           // El objeto gráfico que se va a dibujar (obtenido mediante painterResource).
    contentDescription: String?,                // Texto de accesibilidad para lectores de pantalla (puede establecerse como null).
    modifier: Modifier = Modifier,              // Modificador para aplicar tamaño, márgenes, formas, bordes o clics.
    alignment: Alignment = Alignment.Center,    // La alineación de la imagen dentro de los límites asignados si el contenedor es mayor.
    contentScale: ContentScale = ContentScale.Fit, // La regla de escala para adaptar el contenido de la imagen al tamaño del contenedor.
    alpha: Float = DefaultAlpha,                // Controla la opacidad visual del elemento (desde 0.0 transparente a 1.0 opaco).
    colorFilter: ColorFilter? = null            // Aplica efectos o tintes cromáticos directamente sobre los píxeles de la imagen.
)
```

---

## Opciones de Personalización y Diseño Básicos

### 1. Imagen simple
Para cargar una imagen básica se utiliza `painterResource`, el cual requiere el identificador numérico del recurso gráfico almacenado en el proyecto.

```kotlin
@Composable
fun SimpleImage() {
    Image(
        painter = painterResource(id = R.drawable.andy_rubin),
        contentDescription = "Andy Rubin",
        modifier = Modifier.fillMaxWidth() // Expande el componente al ancho máximo disponible
    )
}
```

![Imagen simple](images/0d004d_47c6d0713da34afa841b84efa7a2b6e5_mv2.png)

### 2. Imagen circular
Para generar una interfaz geométrica circular, se combina un tamaño fijo con el modificador `.clip(CircleShape)`. Se recomienda usar `ContentScale.Crop` para que la imagen rellene todo el espacio sin deformarse.

```kotlin
@Composable
fun CircleImageView() {
    Image(
        painter = painterResource(R.drawable.andy_rubin),
        contentDescription = "Circle Image",
        contentScale = ContentScale.Crop,
        modifier = Modifier
            .size(128.dp)
            .clip(CircleShape)                 // Recorta el componente en forma de círculo perfecto
            .border(5.dp, Color.Gray, CircleShape) // Añade un contorno periférico opcional
    )
}
```

![Imagen circular](images/0d004d_f052882da9e44ad5a62836fc6b94e00e_mv2.png)

### 3. Imagen con esquinas redondeadas
Sigue el mismo principio de recorte de la imagen circular, sustituyendo la geometría por `RoundedCornerShape`. Este método acepta valores en porcentaje o unidades fijas de densidad.

```kotlin
@Composable
fun RoundCornerImageView() {
    Image(
        painter = painterResource(R.drawable.andy_rubin),
        contentDescription = "Round corner image",
        contentScale = ContentScale.Crop,
        modifier = Modifier
            .size(128.dp)
            .clip(RoundedCornerShape(10)) // Recorte basado en porcentaje (10%)
            // Para unidades fijas se utilizaría: RoundedCornerShape(16.dp)
            .border(5.dp, Color.Gray, RoundedCornerShape(10))
    )
}
```

### 4. Color de fondo de la imagen
Se puede aplicar un color plano al fondo del contenedor mediante el modificador `.background()`. Esta propiedad es perceptible únicamente en recursos con transparencia, como formatos PNG o archivos vectoriales.

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

### 5. ColorFilter de la imagen (tintado)
El método `ColorFilter.tint()` modifica la coloración de los píxeles opacos de un recurso gráfico. Es de gran utilidad para modificar dinámicamente el color de iconos monocromáticos (`VectorDrawables`) sin duplicar archivos.

```kotlin
@Composable
fun ImageWithTint() {
    Image(
        painter = painterResource(id = R.drawable.ic_cart),
        contentDescription = "",
        colorFilter = ColorFilter.tint(Color.Red), // Tiñe los trazos de la imagen de color rojo
        modifier = Modifier.size(200.dp)
    )
}
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

### Ejemplo de uso de escala
```kotlin
@Composable
fun InsideFit() {
    Image(
        painter = painterResource(id = R.drawable.andy_rubin),
        contentDescription = "",
        modifier = Modifier
            .size(150.dp)
            .background(Color.LightGray),
        contentScale = ContentScale.Inside // Aplica la regla de escala Inside
    )
}
```

---

**Código fuente y recursos adicionales**

<https://github.com>
