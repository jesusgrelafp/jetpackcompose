# Botones (Buttons) en Jetpack Compose

> Aprende a crear distintos tipos de botones en Jetpack Compose: simples, de color, con iconos, con formas, con bordes y con elevación.

*Básicos · 5 de febrero de 2024 · 8 min de lectura*  
*Fuente (en inglés): <https://www.jetpackcompose.net/buttons-in-jetpack-compose>*

En los botones de Jetpack Compose debes proporcionar dos argumentos. El primero es el callback `onClick` y el otro es el elemento de texto del botón. Puedes añadir un composable `Text` o cualquier otro composable como elementos hijos del `Button`.

![Estructura de un botón: callback onClick y contenido](images/0d004d_a6ddd433aa57461e9b5ed972671053a4_mv2.png)

## 1. Botón simple

```kotlin
@Composable
fun SimpleButton() {
    Button(onClick = {
        //your onclick code here
    }) {
        Text(text = "Simple Button")
    }
}
```

![Botón simple](images/0d004d_0d6bfb5e50a6467ba063390f9343ed9e_mv2.png)

## 2. Botón con color personalizado

```kotlin
@Composable
fun ButtonWithColor(){
    Button(onClick = {
        //your onclick code
        },
        colors = ButtonDefaults.buttonColors(backgroundColor = Color.DarkGray))
    {
     Text(text = "Button with gray background",color = Color.White)
    }
}
```

![Botón con color de fondo gris](images/0d004d_7ca3ed0521284560acfcbfe0452d9a64_mv2.png)

## 3. Botón con varios textos

```kotlin
@Composable
fun ButtonWithTwoTextView() {
    Button(onClick = {
        //your onclick code here
    }) {
        Text(text = "Click ", color = Color.Magenta)
        Text(text = "Here", color = Color.Green)
    }
}
```

![Botón con varios textos](images/0d004d_0eed4a20f16c4c0f9885fc81274640f7_mv2.png)

## 4. Botón con icono

```kotlin
@Composable
fun ButtonWithIcon() {
    Button(onClick = {}) {
        Image(
            painterResource(id = R.drawable.ic_cart),
            contentDescription ="Cart button icon",
            modifier = Modifier.size(20.dp))

        Text(text = "Add to cart",Modifier.padding(start = 10.dp))
    }
}
```

![Botón con icono](images/0d004d_4a8916015f7f4858acf5502a2d83e0eb_mv2.png)

## 5. Botones con formas

**Forma rectangular (Rectangle Shape):**

```kotlin
@Composable
fun ButtonWithRectangleShape() {
    Button(onClick = {}, shape = RectangleShape) {
        Text(text = "Rectangle shape")
    }
}
```

**Esquinas redondeadas (Round Corner Shape):**

```kotlin
@Composable
fun ButtonWithRoundCornerShape() {
    Button(onClick = {}, shape = RoundedCornerShape(20.dp)) {
        Text(text = "Round corner shape")
    }
}
```

**Esquinas cortadas (Cut Corner Shape):**

```kotlin
@Composable
fun ButtonWithCutCornerShape() {
    //CutCornerShape(percent: Int)- it will consider as percentage
    //CutCornerShape(size: Dp)- you can pass Dp also.
    Button(onClick = {}, shape = CutCornerShape(10)) {
        Text(text = "Cut corner shape")
    }
}
```

![Botones con distintas formas](images/0d004d_ca77f4662c724a86b9be44a5bf5b8ce6_mv2.png)

## 6. Botón con borde

```kotlin
@Composable
fun ButtonWithBorder() {
    Button(
        onClick = {
            //your onclick code
        },
        border = BorderStroke(1.dp, Color.Red),
        colors = ButtonDefaults.outlinedButtonColors(contentColor = Color.Red)
    ) {
        Text(text = "Button with border", color = Color.DarkGray)
    }
}
```

![Botón con borde](images/0d004d_106a41df5e3f4cd49392c50f5ff05668_mv2.png)

## 7. Elevación del botón

```kotlin
@Composable
fun ButtonWithElevation() {
    Button(onClick = {
        //your onclick code here
    },elevation =  ButtonDefaults.elevation(
        defaultElevation = 10.dp,
        pressedElevation = 15.dp,
        disabledElevation = 0.dp
    )) {
        Text(text = "Button with elevation")
    }
}
```

![Botón con elevación](images/0d004d_537bf4f3e2d344abaf29285e776cf52c_mv2.png)

## Código fuente

<https://github.com/JetpackCompose/Jetpack-Compose-Samples>
