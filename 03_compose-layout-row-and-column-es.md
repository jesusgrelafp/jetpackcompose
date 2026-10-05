# Compose Layout: Row y Column

> Aprende a organizar los elementos de la interfaz en horizontal y en vertical con los composables Row y Column de Jetpack Compose.

*Básicos · 25 de enero de 2024 · 10 min de lectura*  
*Fuente (en inglés): <https://www.jetpackcompose.net/compose-layout-row-and-column>*

## ¿Qué son los layouts en Android?

Un layout proporciona un contenedor invisible que alberga vistas u otros layouts. Podemos colocar un grupo de vistas dentro de un layout. Row y Column son layouts que organizan nuestras vistas de forma lineal.

## ¿Qué es la disposición lineal?

Una disposición lineal consiste en colocar los elementos uno detrás de otro. De este modo, los elementos se ordenan en secuencia, ya sea horizontal o verticalmente.

**Row**: organiza las vistas horizontalmente.

**Column**: organiza las vistas verticalmente.

![Diagrama de Row y Column](images/0d004d_7292d88214d043e68aec8aec58b7b795_mv2.jpg)

## Row

Un Row muestra cada hijo a continuación del anterior. Funciona como un LinearLayout con orientación horizontal.

```kotlin
@Composable
fun SimpleRow(){
    Row {
        Text(text = "Row Text 1", Modifier.background(Color.Red))
        Text(text = "Row Text 2", Modifier.background(Color.White))
        Text(text = "Row Text 3", Modifier.background(Color.Green))
    }
}
```

## Column

Un Column muestra cada hijo debajo de los anteriores. Funciona como un LinearLayout con orientación vertical.

```kotlin
@Composable
fun SimpleColumn(){
    Column {
        Text(text = "Column Text 1", Modifier.background(Color.Red))
        Text(text = "Column Text 2", Modifier.background(Color.White))
        Text(text = "Column Text 3", Modifier.background(Color.Green))
    }
}
```

He colocado estos composables dentro de una columna con etiquetas. El enlace al código fuente completo está al final de este tutorial.

**Resultado de Row y Column:**

![Resultado de Row y Column](images/0d004d_e10bd4a1aead490fac65b2010bbd83d9_mv2.png)

## Alineación

Existen nueve opciones de alineación que se pueden aplicar a los elementos hijos de la interfaz.

## Disposición (Arrangement)

También disponemos de tres disposiciones que se pueden aplicar tanto en vertical como en horizontal:

- SpaceEvenly
- SpaceBetween
- SpaceAround

La disposición **SpaceEvenly** reparte los elementos hijos a lo largo del eje principal, incluyendo espacio libre antes del primer hijo y después del último.

![Disposición SpaceEvenly](images/0d004d_0425e528f4f24ed3a7a05c9fee7139d0_mv2.jpg)

La disposición **SpaceBetween** reparte los elementos hijos a lo largo del eje principal sin espacio libre antes del primer hijo ni después del último.

![Disposición SpaceBetween](images/0d004d_97d662b107bc4db78aa275cae59d1977_mv2.jpg)

La disposición **SpaceAround** reparte los elementos hijos a lo largo del eje principal dejando la mitad del espacio libre antes del primer hijo y después del último.

![Disposición SpaceAround](images/0d004d_0300ba2e8c304e0698fd6104cf65fc00_mv2.jpg)

## Disposición y alineación en Row

```kotlin
@Composable
fun RowArrangement(){
    Row(modifier = Modifier.fillMaxWidth(),
        verticalAlignment = Alignment.Top,
        horizontalArrangement = Arrangement.SpaceEvenly) {
        Text(text = " Text 1")
        Text(text = " Text 2")
        Text(text = " Text 3")
    }
}
```

## Disposición y alineación en Column

```kotlin
@Composable
fun ColumnArrangement(){
    Column(modifier = Modifier.fillMaxHeight().fillMaxWidth(),
        verticalArrangement = Arrangement.SpaceEvenly,
        horizontalAlignment = Alignment.End
    ) {
        Text(text = "Text 1", Modifier.background(Color.Red))
        Text(text = "Text 2", Modifier.background(Color.White))
        Text(text = "Text 3", Modifier.background(Color.Green))
    }
}
```

**Resultado:**

![Resultado de la disposición en Column](images/0d004d_67a1f63a66594e29b732e0cde0ce7f75_mv2.png)

## Código fuente

[https://github.com/JetpackCompose/Jetpack-Compose-Samples](https://github.com/JetpackCompose/Jetpack-Compose-Samples)
