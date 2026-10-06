# Progress Indicator en Jetpack Compose

> Aprende a usar LinearProgressIndicator y CircularProgressIndicator en Jetpack Compose, en modo determinado e indeterminado.

*Básicos · 18 de febrero de 2024 · 6 min de lectura*  
*Fuente (en inglés): <https://www.jetpackcompose.net/progress-indicator-in-jetpack-compose>*

## Progress Indicator (indicador de progreso)

Progress Indicator es un widget que indica al usuario que hay alguna acción en curso.

En operaciones largas, como descargar o subir archivos o hacer llamadas a una API, podemos avisar al usuario de que espere con ayuda de este componente.

> *Si eres desarrollador de Android:* es un **ProgressBar**.

**Tipos de indicadores de progreso disponibles en Jetpack Compose:**

1. `LinearProgressIndicator`
2. `CircularProgressIndicator`

## LinearProgressIndicator

Se utiliza para mostrar el progreso en una línea.

Admite dos modos para representar el progreso: **determinado** (*determinate*) e **indeterminado** (*indeterminate*).

### 1. Progreso indeterminado

Si no sabes cuánto tardará tu acción, usa el modo **indeterminado**. Se ejecutará indefinidamente.

**Ejemplo:**

```kotlin
LinearProgressIndicator()
```

**Resultado:**

![LinearProgressIndicator indeterminado](images/0d004d_2172d9032ba848b8b088ba0c37ec5b14_mv2.gif)

### 2. Progreso determinado

Usa el modo determinado cuando quieras mostrar que se ha completado una cantidad concreta de progreso. Por ejemplo, el porcentaje descargado de un archivo.

Debes indicar el valor del progreso como parámetro. Tiene que estar entre 0.0 y 1.0.

**Ejemplo:**

```kotlin
LinearProgressIndicator(progress = 0.7f) //70% progress
```

**Resultado:**

![LinearProgressIndicator determinado](images/0d004d_480fa204fcef4eadb7114f599762abf8_mv2.png)

### 3. LinearProgressIndicator personalizado

Puedes personalizar el tamaño, el color del progreso, el color de fondo, etc.

**Ejemplo:**

```kotlin
@Composable
private fun CustomLinearProgressBar(){
    Column(modifier = Modifier.fillMaxWidth()) {
        LinearProgressIndicator(
            modifier = Modifier
                .fillMaxWidth()
                .height(15.dp),
            backgroundColor = Color.LightGray,
            color = Color.Red //progress color
       )
    }
}
```

**Resultado:**

![LinearProgressIndicator personalizado](images/0d004d_7e1bf6d2d9da457a857de3d505567e2c_mv2.gif)

## CircularProgressIndicator

Se utiliza para mostrar el progreso con forma circular. También admite dos modos: **determinado** (*determinate*) e **indeterminado** (*indeterminate*).

### 1. Progreso indeterminado

**Ejemplo:**

```kotlin
CircularProgressIndicator()
```

**Resultado:**

![CircularProgressIndicator indeterminado](images/0d004d_b5ba714706cf470aa3b0d61a68671368_mv2.gif)

### 2. Progreso determinado

**Ejemplo:**

```kotlin
CircularProgressIndicator(progress = 0.75f) //75% progress
```

**Resultado:**

![CircularProgressIndicator determinado](images/0d004d_7fc8fc8ae7984736adf8ded14ad26991_mv2.png)

Por defecto no se anima, pero podemos animarlo con ayuda de las animaciones de Jetpack Compose.

### 3. Progreso determinado con animación

**Ejemplo:**

```kotlin
@Composable
private fun CircularProgressAnimated(){
    val progressValue = 0.75f
    val infiniteTransition = rememberInfiniteTransition()

    val progressAnimationValue by infiniteTransition.animateFloat(
        initialValue = 0.0f,
        targetValue = progressValue,
        animationSpec = infiniteRepeatable(animation = tween(900))
    )

    CircularProgressIndicator(progress = progressAnimationValue)
}
```

**Resultado:**

![CircularProgressIndicator determinado con animación](images/0d004d_8ad14a8ca7a14aac89f00c1431c64859_mv2.gif)

### 4. CircularProgressIndicator personalizado

Podemos personalizar el color del indicador, el grosor del trazo (*stroke width*), el ancho y el alto.

**Ejemplo:**

```kotlin
@Composable
private fun CustomCircularProgressBar(){
    CircularProgressIndicator(
        modifier = Modifier.size(100.dp),
        color = Color.Green,
        strokeWidth = 10.dp
    )
}
```

**Resultado:**

![CircularProgressIndicator personalizado](images/0d004d_11b042f5266b440485bb2a885ae00e63_mv2.gif)

**Código fuente:** [GitHub](https://github.com/JetpackCompose/Jetpack-Compose-Samples/blob/master/JetPackComposeSamples/app/src/main/java/net/jetpackcompose/composetext/activities/ActivityProgressIndicator.kt)

**Documentación oficial:** <https://developer.android.com/reference/kotlin/androidx/compose/material/package-summary#linearprogressindicator>
