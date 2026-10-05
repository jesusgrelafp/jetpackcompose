# Modificadores (Modifiers) en Jetpack Compose

> Domina los modificadores de Jetpack Compose: fondo, padding, tamaño, alpha, rotación, escala, weight, borde, recorte y más.

*Básicos · 1 de febrero de 2024 · 12 min de lectura*  
*Fuente (en inglés): <https://www.jetpackcompose.net/jetpack-compose-modifiers>*

## ¿Qué son los modificadores (Modifiers) en Jetpack Compose?

Los elementos Modifier decoran o añaden comportamiento a los elementos de la interfaz de Compose. Por ejemplo, los fondos, el padding y los listeners de eventos de clic decoran o añaden comportamiento a filas, textos o botones.

1. Con ayuda de los modificadores podemos dar tamaño y espaciado.
2. Colocar los widgets dentro de un layout.
3. Embellecer los widgets.

> *Si eres desarrollador de Android:* la mayoría de los atributos XML (id, padding, margin, color, alpha, ratio, elevation...) se aplican mediante modificadores.

## 1. Color de fondo

```kotlin
Text("Text with green background color",
            Modifier.background(color = Color.Green))
```

## 2. Padding

Jetpack Compose no tiene un modificador para el margin. Debemos usar el modificador `padding` tanto para el padding (relleno) como para el margin (margen).

```kotlin
@Composable
fun TextWidthPadding() {
    Text(
        "Padding and margin!",
        Modifier.padding(32.dp) // Outer padding (margin)
            .background(color = Color.Green) //background color
            .padding(16.dp) // Inner padding
    )
}
```

![Ejemplo de padding](images/0d004d_5e2f2a1302754c0192c1bad64b6923a3_mv2.png)

## 3. Ancho y alto

Para el ancho debes usar ***width(value : Dp)***.

Para el alto debes usar ***height(value: Dp)***.

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

## 4. Size (tamaño)

Si necesitas el ancho y el alto en el mismo modificador, usa **Modifier.size()**.

Si el ancho y el alto son iguales, usa `Modifier.size(size: Dp)`. Ejemplo: ***Modifier.size(200.dp)***

Si quieres un ancho y un alto distintos, usa `Modifier.size(width: Dp, height: Dp)`. Ejemplo: ***Modifier.size(width=200.dp,height=100.dp)***

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

## 5. Fill Max Width (ancho máximo)

Debes pasar el tamaño como una fracción, que debe estar entre 0.0 y 1.0.

Si quieres que el ancho sea ***match_parent***, puedes usar 1.0.

Su valor por defecto es 1.0. Si llamas al método sin indicar una fracción, se establecerá en 1.0.

> 0.0 significa 0 %, 0.1 significa 10 %, 1.0 significa 100 %

```kotlin
@Composable
fun FillWidthModifier() {
    Text(
        text = "Text Width Match Parent",
        color = Color.White,
        modifier = Modifier
            .background(Color.Gray)
            .padding(Dp(10f))
            .fillMaxWidth(1f))
}
```

## 6. Fill Max Height (alto máximo)

Debes pasar el tamaño como una fracción, que debe estar entre 0.0 y 1.0.

Si quieres que el alto sea ***match_parent***, puedes usar **fillMaxHeight(1.0)**.

```kotlin
@Composable
fun FillHeightModifier() {
    Text(
        text = " Text with 75% Height ",
        color = Color.White,
        modifier = Modifier
            .background(Color.Green)
            .fillMaxHeight(0.75f) //75% area fill
    )
}
```

## 7. Alpha (opacidad)

Alpha se utiliza para establecer la opacidad de la vista.

```kotlin
Modifier.alpha(alpha: Float)
```

Puedes usar valores de 0.0 a 1.0.

> 0.0 significa 0 %, 0.1 significa 10 %, 1.0 significa 100 %

```kotlin
@Composable
fun AlphaModifier() {
    Box(
        Modifier
            .size(250.dp)
            .alpha(0.5f)//50% opacity
            .background(Color.Red)
    )
}
```

## 8. Rotate (rotación)

Establece los grados que gira la vista alrededor del centro del composable. Los **valores crecientes** producen una rotación **en sentido horario**. Los **grados negativos** se usan para rotar **en sentido antihorario**.

```kotlin
Modifier.rotate(degrees: Float)
```

```kotlin
@Composable
fun RotateModifier() {
    Box(
        Modifier
            .rotate(45f)
            .size(250.dp)
            .background(Color.Red)
    )
}
```

## 9. Scale (escala)

Escala el contenido del composable según los siguientes factores de escala a lo largo del eje horizontal y del eje vertical, respectivamente. Se pueden usar factores de escala negativos para reflejar el contenido respecto al eje horizontal o vertical correspondiente.

```kotlin
@Composable
fun ScaleModifier() {
    Box(
        Modifier
            .scale(scaleX = 2f, scaleY = 3f)
            .size(200.dp, 200.dp)
    )
}
```

## 10. Weight (peso)

Con `weight` puedes especificar una proporción de tamaño entre varias vistas.

Por ejemplo: si añades ***view1*** con weight **1**, ***view2*** con weight **1** y ***view3*** con weight **2**.

Se sumarán todos los pesos, **1** + **1** + **2** = **4**, y se asignará el espacio a cada vista en función del peso indicado.

- View1 obtiene el 25 % del espacio → 1/4*100 = 25 %
- View2 obtiene el 25 % del espacio → 1/4*100 = 25 %
- View3 obtiene el 50 % del espacio → 2/4*100 = 50 %

```kotlin
@Composable
fun WeightModifier(){
    Row() {
        Column(
            Modifier.weight(1f).background(Color.Red)){
            Text(text = "Weight = 1", color = Color.White)
        }
        Column(
            Modifier.weight(1f).background(Color.Blue)){
            Text(text = "Weight = 1", color = Color.White)
        }
        Column(
            Modifier.weight(2f).background(Color.Green)
        ) {
            Text(text = "Weight = 2")
        }
    }
}
```

> **Nota**: `weight` está disponible desde la versión 1.0.0 de Compose.

## 11. Border (borde)

**Puedes establecer el borde de las siguientes formas:**

1. `Modifier.border(width: Dp, color: Color, shape: Shape = RectangleShape)`
2. `Modifier.border(width: Dp, brush: Brush, shape: Shape)`
3. `Modifier.border(border: BorderStroke, shape: Shape = RectangleShape)`

```kotlin
@Composable
fun BorderModifier() {
    Text(
        text = "Text with Red Border",
        modifier = Modifier
            .padding(10.dp)
            .background(Color.Yellow)
            .border(2.dp,Color.Red)
            .padding(10.dp)
    )
}
```

**Borde con esquinas redondeadas:**

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

## 12. Clip (recorte)

El modificador `clip` permite recortar la forma existente. Puedes usar una forma predeterminada o tus propias formas personalizadas.

**Formas disponibles en Jetpack Compose:**

- `RectangleShape`
- `CircleShape`
- `RoundedCornerShape`
- `CutCornerShape`

```kotlin
@Composable
fun ClipModifier() {
    Text(
        text = "Text with Clipped background",
        color = Color.White,
        modifier = Modifier
            .padding(Dp(10f))
            .clip(RoundedCornerShape(25.dp))
            .background(Color.Blue)
            .padding(Dp(15f))
    )
}
```

**Código fuente:**

<https://github.com/JetpackCompose/Jetpack-Compose-Samples>
