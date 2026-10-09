# Compose Layouts: Row, Column y Box

Aprende a organizar los elementos de la interfaz en horizontal, vertical y por capas (superpuestos) usando los composables fundamentales de Jetpack Compose.

*Básicos · 15 min de lectura*  
Fuente base (en inglés): <https://jetpackcompose.net>

---

## ¿Qué son los layouts en Android?

Un layout proporciona un contenedor invisible que alberga componentes visuales (hijos) u otros layouts. Row, Column y Box son los tres pilares fundamentales en Jetpack Compose para estructurar pantallas.

*   **Row**: organiza las vistas horizontalmente (una al lado de la otra).
*   **Column**: organiza las vistas verticalmente (una debajo de la otra).
*   **Box**: organiza las vistas por capas (una encima de la otra, como platos apilados).

![Diagrama de Row y Column](images/0d004d_7292d88214d043e68aec8aec58b7b795_mv2.jpg)

> **Nota sobre los imports:** en los ejemplos de este documento se asume que has importado lo necesario (`androidx.compose.foundation.layout.*`, `androidx.compose.foundation.background`, `androidx.compose.ui.graphics.Color`, `androidx.compose.ui.unit.dp`, etc.). Android Studio los sugiere automáticamente con `Alt + Enter`.

---

## Alineación (Alignment) vs Disposición (Arrangement)

Para comprender el posicionamiento en los contenedores lineales, es fundamental dominar estos dos conceptos:
*   **Eje Principal (Main Axis):** El eje en el que el contenedor añade sus elementos (Horizontal en `Row`, Vertical en `Column`). Se controla mediante el parámetro **Arrangement**.
*   **Eje Cruzado (Cross Axis):** El eje perpendicular al principal (Vertical en `Row`, Horizontal en `Column`). Se controla mediante el parámetro **Alignment**.
*   **En Box (sin ejes lineales):** No existe un eje de propagación lineal. El posicionamiento se maneja directamente con una alineación bidimensional (`contentAlignment` para todos los hijos o `Modifier.align()` para uno concreto).

---

## 1. El Composable Row (Fila)

Un `Row` muestra cada hijo a continuación del anterior en el eje horizontal. Funciona de forma equivalente a un `LinearLayout` con orientación horizontal del sistema de vistas clásico.

### Parámetros de Row
```kotlin
Row(
    modifier = Modifier,
    horizontalArrangement = Arrangement.Start, // Distribución horizontal (Eje principal)
    verticalAlignment = Alignment.Top,          // Alineación vertical (Eje cruzado)
    content = { /* Componentes hijos dentro de RowScope */ }
)
```

### Ejemplo de uso básico
```kotlin
@Composable
fun SimpleRow() {
    Row {
        Text(text = "Row Text 1", modifier = Modifier.background(Color.Red))
        Text(text = "Row Text 2", modifier = Modifier.background(Color.White))
        Text(text = "Row Text 3", modifier = Modifier.background(Color.Green))
    }
}
```

---

## 2. El Composable Column (Columna)

Un `Column` muestra cada hijo debajo de los anteriores en el eje vertical. Funciona de forma equivalente a un `LinearLayout` con orientación vertical.

### Parámetros de Column
```kotlin
Column(
    modifier = Modifier,
    verticalArrangement = Arrangement.Top,       // Distribución vertical (Eje principal)
    horizontalAlignment = Alignment.Start,        // Alineación horizontal (Eje cruzado)
    content = { /* Componentes hijos dentro de ColumnScope */ }
)
```

### Ejemplo de uso básico
```kotlin
@Composable
fun SimpleColumn() {
    Column {
        Text(text = "Column Text 1", modifier = Modifier.background(Color.Red))
        Text(text = "Column Text 2", modifier = Modifier.background(Color.White))
        Text(text = "Column Text 3", modifier = Modifier.background(Color.Green))
    }
}
```

![Resultado de Row y Column](images/0d004d_e10bd4a1aead490fac65b2010bbd83d9_mv2.png)

> **Importante:** ni `Row` ni `Column` hacen scroll por defecto. Si el contenido no cabe en pantalla, se corta. Para listas largas se usa `LazyColumn`/`LazyRow`, o `Modifier.verticalScroll()`/`horizontalScroll()` si son pocos elementos.

---

## 3. El Contenedor Box (Capas y Superposición)

A diferencia de `Row` y `Column`, el contenedor `Box` no ordena los elementos de forma secuencial. Si se colocan elementos dentro de un `Box` sin modificar sus parámetros, se dibujarán uno encima del otro en la esquina superior izquierda (`TopStart`).

Es el contenedor utilizado para colocar texto o iconos sobre una imagen de fondo, crear indicadores de notificación o dibujar barras de progreso superpuestas.

### Parámetros de Box
```kotlin
Box(
    modifier = Modifier,
    contentAlignment = Alignment.TopStart, // Alineación por defecto para todos los hijos
    propagateMinConstraints = false,       // Define si las restricciones mínimas se pasan a los hijos
    content = { /* Componentes hijos dentro de BoxScope */ }
)
```

### Ejemplo de uso básico
```kotlin
@Composable
fun SimpleBox() {
    Box(modifier = Modifier.size(150.dp).background(Color.LightGray)) {
        // La caja roja se dibuja primero (al fondo)
        Box(modifier = Modifier.size(100.dp).background(Color.Red))
        // La caja azul se dibuja encima de la roja
        Box(modifier = Modifier.size(50.dp).background(Color.Blue))
    }
}
```

---

## Opciones de Posicionamiento Detalladas

### Opciones de Disposición (Arrangement)
El `Arrangement` define cómo se distribuye el espacio sobrante a lo largo del eje principal en filas y columnas.

Opciones básicas: `Start`/`Top` (todo al inicio), `Center` (agrupados en el centro) y `End`/`Bottom` (todo al final). Para dejar una separación fija entre hijos se usa `Arrangement.spacedBy(8.dp)`.

Opciones que reparten el espacio sobrante:

*   **SpaceEvenly:** Reparte los elementos uniformemente, dejando el mismo espacio entre ellos y en los extremos exteriores.
    ![Disposición SpaceEvenly](images/0d004d_0425e528f4f24ed3a7a05c9fee7139d0_mv2.jpg)
*   **SpaceBetween:** Empuja el primer elemento al inicio absoluto y el último al final absoluto, repartiendo el espacio restante únicamente en las separaciones intermedias.
    ![Disposición SpaceBetween](images/0d004d_97d662b107bc4db78aa275cae59d1977_mv2.jpg)
*   **SpaceAround:** Cada elemento tiene el mismo espacio a sus lados, lo que provoca que el espacio en los extremos exteriores sea la mitad de ancho que el espacio intermedio.
    ![Disposición SpaceAround](images/0d004d_0300ba2e8c304e0698fd6104cf65fc00_mv2.jpg)

### Opciones de Alineación (Alignment)
La alineación define cómo se posicionan los elementos respecto al eje cruzado o dentro de un espacio bidimensional. Hay tres grupos:

#### A. Alineación Vertical (`Alignment.Vertical`, para usar dentro de un `Row`)
*   `Alignment.Top`: Eleva los elementos al borde superior.
*   `Alignment.CenterVertically`: Centra los elementos verticalmente.
*   `Alignment.Bottom`: Baja los elementos al borde inferior.

#### B. Alineación Horizontal (`Alignment.Horizontal`, para usar dentro de un `Column`)
*   `Alignment.Start`: Empuja los elementos al inicio (izquierda en idiomas de izquierda a derecha).
*   `Alignment.CenterHorizontally`: Centra los elementos horizontalmente.
*   `Alignment.End`: Empuja los elementos al final (derecha en idiomas de izquierda a derecha).

#### C. Alineación Bidimensional (para usar en `Box` o de forma individual)
Al combinar coordenadas horizontales y verticales, se obtienen 9 puntos exactos para posicionar elementos en un plano:
*   `Alignment.TopStart` (Superior Izquierda)
*   `Alignment.TopCenter` (Superior Centro)
*   `Alignment.TopEnd` (Superior Derecha)
*   `Alignment.CenterStart` (Centro Izquierda)
*   `Alignment.Center` (Centro Absoluto)
*   `Alignment.CenterEnd` (Centro Derecha)
*   `Alignment.BottomStart` (Inferior Izquierda)
*   `Alignment.BottomCenter` (Inferior Centro)
*   `Alignment.BottomEnd` (Inferior Derecha)

> **Nota técnica:** También es posible aplicar estas alineaciones de forma individual a un único hijo con el modificador `Modifier.align()`, disponible gracias a los ámbitos (*scopes*) de cada contenedor. En `Row` acepta una alineación vertical, en `Column` una horizontal y en `Box` una bidimensional.

---

## Ejemplos Avanzados de Código

### Ejemplo 1: Distribución en Column
```kotlin
@Composable
fun ColumnArrangement() {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.SpaceEvenly, // Eje Principal
        horizontalAlignment = Alignment.End // Eje Cruzado
    ) {
        Text(text = "Text 1", modifier = Modifier.background(Color.Red))
        Text(text = "Text 2", modifier = Modifier.background(Color.White))
        Text(text = "Text 3", modifier = Modifier.background(Color.Green))
    }
}
```

### Ejemplo 2: Posicionamiento preciso dentro de un Box
Es posible asignar una alineación general a todo el `Box`, o usar el modificador `.align()` en cada hijo para distribuirlos de forma independiente:

```kotlin
@Composable
fun AlignedBoxExample() {
    Box(modifier = Modifier.fillMaxSize().background(Color.DarkGray)) {
        // Un botón en la esquina inferior derecha
        Button(
            onClick = { },
            modifier = Modifier.align(Alignment.BottomEnd).padding(16.dp)
        ) {
            Text("+")
        }

        // Un texto de carga exactamente en el centro del Box
        Text(
            text = "Cargando...",
            color = Color.White,
            modifier = Modifier.align(Alignment.Center)
        )
    }
}
```
