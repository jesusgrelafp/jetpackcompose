[README.md](https://github.com/user-attachments/files/33096684/README.md)
# Tutorial de Jetpack Compose en español

Colección de 16 artículos que explican los fundamentos de **Jetpack Compose**, el toolkit moderno de Android para crear interfaces nativas con Kotlin. Es una traducción al español del tutorial publicado en [jetpackcompose.net](https://www.jetpackcompose.net/), con el código y las imágenes incluidos.

## Índice

### Básicos

| # | Artículo | Qué aprenderás |
|---|----------|----------------|
| 01 | [Introducción a Jetpack Compose](01_introduccion-jetpack-compose-es.md) | Qué es Compose, UI imperativa vs. declarativa y primeras funciones `@Composable` |
| 02 | [Jetpack Compose Preview](02_jetpack-compose-preview-es.md) | La anotación `@Preview` y sus opciones: nombre, fondo, tamaño, dispositivo y varias vistas previas |
| 03 | [Compose Layout: Row y Column](03_compose-layout-row-and-column-es.md) | Organizar elementos en horizontal y en vertical; alineación y disposición |
| 04 | [Text en Jetpack Compose](04_text-en-jetpack-compose-es.md) | Tamaño, color, negrita, cursiva, máximo de líneas, desbordamiento y texto seleccionable |
| 05 | [TextStyle en Jetpack Compose](05_textstyle-en-jetpack-compose-es.md) | Sombra, fuentes, decoración del texto y tipografía de Material |
| 06 | [Modificadores (Modifiers)](06_modificadores-jetpack-compose-es.md) | Fondo, padding, tamaño, alpha, rotación, escala, weight, borde y recorte |
| 07 | [Botones (Buttons)](07_botones-jetpack-compose-es.md) | Botones simples, con color, con icono, con formas, con borde y con elevación |
| 08 | [Image en Jetpack Compose](08_image-en-jetpack-compose-es.md) | Mostrar imágenes: circulares, con esquinas redondeadas, `tint` y `ContentScale` |
| 09 | [TextField en Jetpack Compose](09_textfield-en-jetpack-compose-es.md) | Campos de texto, `label`, `placeholder`, opciones de teclado, contorno e iconos |
| 10 | [LazyColumn y LazyRow](10_lazycolumn-lazyrow-es.md) | Listas eficientes (el equivalente de `RecyclerView`), `contentPadding` y espaciado |
| 11 | [Card en Jetpack Compose](11_card-en-jetpack-compose-es.md) | Contenedores con elevación, forma, borde y color de contenido |
| 12 | [Progress Indicator](12_progress-indicator-es.md) | Indicadores de progreso lineales y circulares, determinados e indeterminados |

### Avanzado

| # | Artículo | Qué aprenderás |
|---|----------|----------------|
| 13 | [TopAppBar y Bottom Navigation con Scaffold](13_scaffold-topappbar-bottomnavigation-es.md) | Estructura de pantalla con barra superior, FAB, menú lateral y navegación inferior |
| 14 | [Temas y tipografía](14_temas-tipografia-jetpack-compose-es.md) | Personalizar `MaterialTheme`: colores, tipografía, fuentes propias y tema claro/oscuro |
| 15 | [Gestión del estado (State Management)](15_state-management-jetpack-compose-es.md) | `State`, `MutableState`, `remember` y `rememberSaveable` |
| 16 | [Animaciones](16_animaciones-jetpack-compose-es.md) | `Animatable`, `animate*AsState`, `updateTransition` e `InfiniteTransition` |

## Estructura del repositorio

```text
.
├── README.md
├── 01_introduccion-jetpack-compose-es.md
├── 02_jetpack-compose-preview-es.md
├── …
├── 16_animaciones-jetpack-compose-es.md
└── images/          ← imágenes y GIF usados por los artículos
```

Todos los artículos enlazan sus imágenes con rutas relativas (`images/…`), así que la carpeta `images/` debe estar en el mismo nivel que los archivos `.md`.

## Criterios de la traducción

- **El código no se modifica.** Los bloques Kotlin, XML, Java y Gradle son idénticos a los del original. Los comentarios dentro del código se dejan en inglés.
- **Los nombres de la API se mantienen en inglés** (`Row`, `Modifier`, `LazyColumn`, `remember`…), porque son los que se escriben en el código. Cuando ayuda, el término en español se añade entre paréntesis.
- **Las imágenes** conservan el texto en inglés que llevan dentro (capturas de pantalla, diagramas). Solo se han traducido sus textos alternativos.
- Se han **corregido algunos errores menores del original** (por ejemplo, nombres de funciones con mayúscula incorrecta o descripciones técnicas imprecisas) y se han señalado en la traducción cuando afectan al significado.

## Nota sobre versiones: Material 2 y Material 3

Los ejemplos del tutorial original usan **Material 2** (`androidx.compose.material`). Los proyectos nuevos de Android Studio usan **Material 3** (`androidx.compose.material3`), donde algunas APIs cambian de nombre o de forma:

| Material 2 (en los artículos) | Material 3 |
|-------------------------------|------------|
| `MaterialTheme(colors = …)` | `MaterialTheme(colorScheme = …)` |
| `darkColors()` / `lightColors()` | `darkColorScheme()` / `lightColorScheme()` |
| Estilos `h1`–`h6`, `subtitle1`, `body1`, `caption`… | Estilos `display*`, `headline*`, `title*`, `body*`, `label*` |
| `ButtonDefaults.buttonColors(backgroundColor = …)` | `ButtonDefaults.buttonColors(containerColor = …)` |
| `Card(elevation = 10.dp)` | `Card(elevation = CardDefaults.cardElevation(defaultElevation = 10.dp))` |
| `LinearProgressIndicator(progress = 0.7f)` | `LinearProgressIndicator(progress = { 0.7f })` |
| `BottomNavigation` / `BottomNavigationItem` | `NavigationBar` / `NavigationBarItem` |
| `Scaffold(drawerContent = …)` | `ModalNavigationDrawer { Scaffold(…) }` |

Los conceptos explicados son los mismos; lo que cambia son los nombres y los parámetros. Los artículos 02, 03, 04, 06, 08, 10 y 15 funcionan igual en ambas versiones (como mucho cambia algún `import`). La sección final del artículo 01, sobre usar Compose en Android Studio, está desfasada: hoy Compose es estable y viene por defecto en los proyectos nuevos.

## Créditos

Contenido original: [jetpackcompose.net](https://www.jetpackcompose.net/) (tutorial *Jetpack Compose Tutorial*). Traducción al español y adaptación a Markdown para este repositorio. Cada artículo incluye al principio el enlace a su página original en inglés.
