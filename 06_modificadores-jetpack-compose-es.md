# Modificadores (Modifiers) en Jetpack Compose

> Domina los modificadores de Jetpack Compose: fondo, padding, tamaño, alpha, rotación, escala, weight, borde, recorte y más.

*Básicos · 12 min de lectura*  
Fuente base (en inglés): <https://jetpackcompose.net>

---

## ¿Qué son los modificadores (Modifiers) en Jetpack Compose?

Los elementos `Modifier` decoran o añaden comportamiento a los componentes visuales de la interfaz de Compose. Por ejemplo, los fondos, el espaciado y los gestos de interacción decoran o añaden lógica a filas, columnas, textos o botones.

1.  Permiten definir dimensiones y espaciados.
2.  Ayudan a posicionar los componentes dentro de un layout o contenedor.
3.  Modifican el aspecto visual y la estética de la interfaz.
4.  Añaden comportamiento e interacción (por ejemplo, `clickable` o `verticalScroll`).

> **Nota para desarrolladores de Android clásico:** Muchos de los atributos definidos en los archivos XML tradicionales (`padding`, `margin`, `background`, `alpha`, `layout_width`, `layout_height`, etc.) se aplican ahora mediante modificadores. Algunos tienen otro equivalente: `margin` se consigue con `padding`, `elevation` con `Modifier.shadow()` (o con el parámetro de elevación de componentes como `Card` o `Surface`) y `id` ya no es necesario, porque en Compose no se buscan vistas por identificador.

> **Nota sobre los imports:** en los ejemplos se asume que has importado lo necesario (`androidx.compose.ui.Modifier`, `androidx.compose.foundation.background`, `androidx.compose.foundation.layout.*`, `androidx.compose.ui.draw.*`, `androidx.compose.ui.unit.dp`, etc.). Android Studio los sugiere automáticamente con `Alt + Enter`.

---

### Cómo se estructura un Modifier (sintaxis de encadenamiento)

En Jetpack Compose, un modificador no es una función convencional con parámetros únicos, sino un objeto que se construye encadenando métodos de forma consecutiva mediante puntos. La estructura que se utiliza en el código sigue este patrón:

```kotlin
Modifier
    .background(Color.Blue) // 1. Primero se aplica el fondo
    .padding(16.dp)        // 2. Después se aplica el espacio interno
    .fillMaxWidth()        // 3. Finalmente se expande al ancho máximo
```

> **Regla fundamental:** El orden en el que se encadenan los modificadores altera el resultado visual en la pantalla, ya que cada modificador envuelve a los que van después de él (se leen de fuera hacia dentro). Por ejemplo, `padding().background()` no es lo mismo que `background().padding()`.

---

## Opciones de personalización y diseño

### 1. Color de fondo
Aplica un color plano al fondo del componente utilizando el método `.background()`.

```kotlin
Text(
    text = "Text with green background color",
    modifier = Modifier.background(color = Color.Green)
)
```

### 2. Padding (márgenes y rellenos)
Jetpack Compose no dispone de un modificador específico llamado `margin`. Se utiliza el modificador `.padding()` de forma consecutiva tanto para el relleno interno como para el margen externo, dependiendo de su posición respecto al fondo.

También admite valores distintos por lado: `.padding(horizontal = 16.dp, vertical = 8.dp)` o `.padding(start = 8.dp, top = 4.dp, end = 8.dp, bottom = 4.dp)`.

```kotlin
@Composable
fun TextWithPadding() {
    Text(
        text = "Padding and margin!",
        modifier = Modifier
            .padding(32.dp)                  // Funciona como Margen Externo (antes del fondo)
            .background(color = Color.Green) // Color de fondo aplicado al área actual
            .padding(16.dp)                  // Funciona como Relleno Interno (después del fondo)
    )
}
```

![Ejemplo de padding](images/0d004d_5e2f2a1302754c0192c1bad64b6923a3_mv2.png)

### 3. Ancho y alto
Para definir dimensiones fijas e independientes en los ejes horizontal y vertical, se utilizan los métodos `.width()` y `.height()`.

```kotlin
@Composable
fun WidthAndHeightModifier() {
    Text(
        text = "Width and Height",
        color = Color.White,
        modifier = Modifier
            .background(Color.Blue)
            .width(200.dp)
            .height(300.dp)
    )
}
```

![Ejemplo de ancho y alto](images/0d004d_31650fe45b004b62a8a920f2976ba192_mv2.png)

### 4. Size (tamaño combinado)
Cuando se requiere asignar ancho y alto de forma simultánea en la misma instrucción, se utiliza `.size()`.
*   Si el ancho y el alto deben ser iguales, se pasa un único valor: `.size(200.dp)`.
*   Si se requieren dimensiones distintas, se especifican ambos parámetros: `.size(width = 200.dp, height = 100.dp)`.

```kotlin
@Composable
fun SizeModifier() {
    Text(
        text = "Text with Size",
        color = Color.White,
        modifier = Modifier
            .background(Color.Cyan)
            .size(width = 250.dp, height = 100.dp)
    )
}
```

### 5. Fill Max Width (ancho máximo adaptable)
Expande el componente horizontalmente ocupando el espacio disponible en base a una fracción comprendida entre `0.0` (0 %) y `1.0` (100 %). Equivale al comportamiento tradicional de `match_parent`. Si no se especifica una fracción, toma el valor `1.0` por defecto.

```kotlin
@Composable
fun FillWidthModifier() {
    Text(
        text = "Text Width Match Parent",
        color = Color.White,
        modifier = Modifier
            .background(Color.Gray)
            .padding(10.dp)
            .fillMaxWidth(1f) // Ocupa el 100% del ancho disponible del contenedor padre
    )
}
```

### 6. Fill Max Height (alto máximo adaptable)
Expande el componente verticalmente ocupando el espacio disponible basándose en una fracción comprendida entre `0.0` y `1.0`.

```kotlin
@Composable
fun FillHeightModifier() {
    Text(
        text = "Text with 75% Height",
        color = Color.White,
        modifier = Modifier
            .background(Color.Green)
            .fillMaxHeight(0.75f) // Ocupa el 75% del alto disponible
    )
}
```

> **Nota:** `fillMaxHeight()` solo tiene efecto si el contenedor padre tiene un alto limitado. Dentro de un contenedor con scroll vertical, el alto disponible es ilimitado y el modificador se ignora. Para ocupar ancho y alto a la vez existe `fillMaxSize()`.

---

## Transformaciones gráficas

### 7. Alpha (opacidad)
Controla la transparencia del componente visual (y de sus hijos) mediante un valor flotante de `0.0` (completamente invisible) a `1.0` (completamente opaco).

```kotlin
@Composable
fun AlphaModifier() {
    Box(
        modifier = Modifier
            .size(250.dp)
            .alpha(0.5f) // 50% de opacidad visual
            .background(Color.Red)
    )
}
```

### 8. Rotate (rotación)
Gira el componente los grados indicados tomando como eje su centro. Los valores positivos realizan un giro en sentido horario, mientras que los valores negativos lo hacen en sentido antihorario. La rotación es solo visual: no cambia el espacio que el componente ocupa en el layout.

```kotlin
@Composable
fun RotateModifier() {
    Box(
        modifier = Modifier
            .rotate(45f) // Gira 45 grados en sentido horario
            .size(250.dp)
            .background(Color.Red)
    )
}
```

### 9. Scale (escala)
Aumenta o reduce el tamaño visual del contenido multiplicándolo por los factores especificados en los ejes `scaleX` y `scaleY`. Los valores negativos provocan un efecto de espejo horizontal o vertical. Igual que `rotate`, la escala es solo visual y no modifica el espacio que el componente ocupa en el layout.

```kotlin
@Composable
fun ScaleModifier() {
    Box(
        modifier = Modifier
            .scale(scaleX = 2f, scaleY = 3f) // Multiplica por 2 el ancho y por 3 el alto original
            .size(100.dp)
            .background(Color.Red)           // Sin fondo, el Box sería invisible
    )
}
```

---

## Estructura y estilo avanzado

### 10. Weight (distribución proporcional de peso)
Permite repartir de manera proporcional el espacio disponible entre varios componentes distribuidos linealmente. Los valores son proporciones relativas, no porcentajes: con pesos 1, 1 y 2 (suma 4), los componentes ocupan 25 %, 25 % y 50 % del espacio (el ancho en un `Row`, el alto en un `Column`).
> **Nota técnica importante:** Este modificador solo está disponible cuando el componente se encuentra directamente dentro del ámbito (*scope*) de un contenedor lineal (`Row` o `Column`).

```kotlin
@Composable
fun WeightModifier() {
    Row(modifier = Modifier.fillMaxWidth()) {
        Column(
            modifier = Modifier.weight(1f).background(Color.Red)
        ) {
            Text(text = "Sección 1 (25%)", color = Color.White)
        }
        Column(
            modifier = Modifier.weight(1f).background(Color.Blue)
        ) {
            Text(text = "Sección 2 (25%)", color = Color.White)
        }
        Column(
            modifier = Modifier.weight(2f).background(Color.Green)
        ) {
            Text(text = "Sección 3 (50%)")
        }
    }
}
```

### 11. Border (contornos y bordes)
Permite trazar líneas periféricas alrededor del límite del componente indicando su grosor, color, pincel o geometría. Dispone de tres firmas comunes:
1.  `Modifier.border(width: Dp, color: Color, shape: Shape = RectangleShape)`
2.  `Modifier.border(width: Dp, brush: Brush, shape: Shape)`
3.  `Modifier.border(border: BorderStroke, shape: Shape = RectangleShape)`

```kotlin
@Composable
fun BorderModifier() {
    Text(
        text = "Text with Red Border",
        modifier = Modifier
            .padding(10.dp)
            .background(Color.Yellow)
            .border(2.dp, Color.Red)
            .padding(10.dp)
    )
}
```

#### Contorno con esquinas redondeadas
Este ejemplo usa la segunda firma (con `Brush`); `SolidColor` convierte un color en un pincel.

```kotlin
@Composable
fun BorderWithShape() {
    Text(
        text = "Text with round border",
        modifier = Modifier
            .padding(10.dp)
            .border(2.dp, SolidColor(Color.Green), RoundedCornerShape(20.dp))
            .padding(10.dp)
    )
}
```

![Borde con esquinas redondeadas](images/0d004d_98cbb7ca9e094bdbab6506295e6b94b8_mv2.png)

### 12. Clip (recorte geométrico)
El modificador `.clip()` restringe el área visual del componente y de sus hijos según una forma determinada. Las formas geométricas estándar integradas en Compose son:
*   `RectangleShape` (rectángulo básico)
*   `CircleShape` (círculo perfecto)
*   `RoundedCornerShape` (esquinas redondeadas)
*   `CutCornerShape` (esquinas achaflanadas o cortadas en línea recta)

El orden importa: `.clip()` debe ir **antes** de `.background()` para que el fondo salga recortado.

```kotlin
@Composable
fun ClipModifier() {
    Text(
        text = "Text with Clipped background",
        color = Color.White,
        modifier = Modifier
            .padding(10.dp)
            .clip(RoundedCornerShape(25.dp)) // Recorta las esquinas del fondo
            .background(Color.Blue)
            .padding(15.dp)
    )
}
```

---

**Documentación oficial**

<https://developer.android.com/develop/ui/compose/modifiers>
