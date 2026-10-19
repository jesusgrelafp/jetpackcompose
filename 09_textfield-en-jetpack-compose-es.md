# TextField en Jetpack Compose (Material 3)

> Aprende a crear campos de entrada de texto en Jetpack Compose con Material 3: simples, con etiquetas, con opciones de teclado, con contorno (outlined) y con iconos.

*Básicos · 10 de febrero de 2024 · 10 min de lectura*  
*Fuente (en inglés): <https://www.jetpackcompose.net/textfield-in-jetpack-compose>*

**¿Qué es TextField?**

TextField es un componente (composable) de interfaz de usuario que permite al usuario introducir texto. Se utiliza para obtener datos del usuario, ya sean números o texto.

Un ejemplo sencillo de TextField es una pantalla de inicio de sesión (login): obtenemos el nombre de usuario y la contraseña mediante este componente.

> *Si eres desarrollador de Android (Views):* es el equivalente al `EditText`.

Todos los ejemplos usan la librería `androidx.compose.material3`.

## ¿Qué opciones hay disponibles en TextField?

Estos son los argumentos de la función `TextField` de Material 3 (sobrecarga con `String`):

```kotlin
@Composable
fun TextField(
    value: String,                                          // Texto actual que se muestra en el campo
    onValueChange: (String) -> Unit,                        // Callback que se ejecuta cada vez que el usuario cambia el texto
    modifier: Modifier = Modifier,                          // Modificadores de tamaño, padding, etc.
    enabled: Boolean = true,                                // Si es false, no se puede editar ni enfocar
    readOnly: Boolean = false,                              // Si es true, se puede enfocar y copiar, pero no editar
    textStyle: TextStyle = LocalTextStyle.current,          // Estilo del texto introducido (fuente, tamaño, color...)
    label: @Composable (() -> Unit)? = null,                // Etiqueta que flota arriba al enfocar o cuando hay texto
    placeholder: @Composable (() -> Unit)? = null,          // Texto de ayuda que se ve mientras el campo está vacío
    leadingIcon: @Composable (() -> Unit)? = null,          // Icono al inicio del campo
    trailingIcon: @Composable (() -> Unit)? = null,         // Icono al final del campo
    prefix: @Composable (() -> Unit)? = null,               // Texto fijo antes del texto introducido (p. ej. "€")
    suffix: @Composable (() -> Unit)? = null,               // Texto fijo después del texto introducido (p. ej. "kg")
    supportingText: @Composable (() -> Unit)? = null,       // Texto de apoyo bajo el campo (ayuda o mensaje de error)
    isError: Boolean = false,                               // Marca el campo como erróneo (colores de error)
    visualTransformation: VisualTransformation = VisualTransformation.None, // Cambia cómo se ve el texto (p. ej. contraseña con •••)
    keyboardOptions: KeyboardOptions = KeyboardOptions.Default, // Tipo de teclado y acción IME (Next, Done, Search...)
    keyboardActions: KeyboardActions = KeyboardActions.Default, // Qué hacer al pulsar la acción IME (Done, Next...)
    singleLine: Boolean = false,                            // Si es true, el texto se mantiene en una sola línea
    maxLines: Int = if (singleLine) 1 else Int.MAX_VALUE,   // Número máximo de líneas visibles
    minLines: Int = 1,                                      // Altura mínima en líneas (1 <= minLines <= maxLines)
    interactionSource: MutableInteractionSource? = null,    // Observa interacciones (foco, pulsación...)
    shape: Shape = TextFieldDefaults.shape,                 // Forma del contenedor
    colors: TextFieldColors = TextFieldDefaults.colors()    // Colores del campo en cada estado
)
```

**Otras sobrecargas** de `TextField` en Material 3:

- Con `value: TextFieldValue`: útil cuando además del texto quieres controlar el cursor, la selección o la composición del IME.
- Con `state: TextFieldState`: la opción más reciente, donde el estado del texto vive en un objeto `TextFieldState` en lugar de `value` / `onValueChange`.

`OutlinedTextField` acepta los mismos parámetros.

> **Imports necesarios** para usar `by` con `mutableStateOf` en los ejemplos siguientes:
> `androidx.compose.runtime.getValue` y `androidx.compose.runtime.setValue`.

## 1. TextField simple

```kotlin
@Composable
fun SimpleTextField() {
    var text by remember { mutableStateOf("") }
    TextField(
        value = text,
        onValueChange = { newText ->
            text = newText
        }
    )
}
```

En este ejemplo creamos una variable **text**, que es un **mutableState** de tipo `String`.

- **mutableState**: devuelve un valor observable para Compose. Si el valor cambia, la interfaz se recompone y se actualiza automáticamente.
- **remember**: conserva el valor entre recomposiciones, para que el texto no se pierda cada vez que se redibuja el composable.

Crea un cuadro de texto simple, pero sin ninguna etiqueta. Veremos otras opciones para mejorarlo.

## 2. Label y placeholder

```kotlin
@Composable
fun LabelAndPlaceHolder() {
    var text by remember { mutableStateOf("") }
    TextField(
        value = text,
        onValueChange = {
            text = it
        },
        label = { Text(text = "Your Label") },
        placeholder = { Text(text = "Your Placeholder/Hint") },
    )
}
```

- `label`: si el TextField tiene el foco (o ya contiene texto), la etiqueta se desplaza flotando a la parte superior del TextField.
- `placeholder`: muestra un texto descriptivo dentro del cuadro cuando el TextField está vacío. Si el campo tiene `label`, el placeholder solo se ve cuando el campo está enfocado y vacío (mientras no tiene foco, la etiqueta ocupa su lugar).

## 3. Opciones de teclado (Keyboard Options)

```kotlin
@Composable
fun TextFieldWithInputType() {
    var text by remember { mutableStateOf("") }
    TextField(
        value = text,
        label = { Text(text = "Number Input Type") },
        keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Number),
        onValueChange = {
            text = it
        }
    )
}
```

Para obtener una entrada numérica desde un TextField, usa `keyboardOptions`. Aquí usamos el tipo de teclado numérico, de modo que se muestra un teclado para introducir números.

Estos son los tipos de teclado (`KeyboardType`) disponibles en Compose:

- `KeyboardType.Text` // Teclado de texto general
- `KeyboardType.Ascii` // Solo caracteres ASCII
- `KeyboardType.Number` // Teclado numérico
- `KeyboardType.Decimal` // Teclado numérico con separador decimal
- `KeyboardType.Phone` // Teclado de marcación telefónica
- `KeyboardType.Uri` // Optimizado para direcciones web (tecla `/`)
- `KeyboardType.Email` // Optimizado para correos (tecla `@`)
- `KeyboardType.Password` // Teclado para contraseñas (sin predicción de texto)
- `KeyboardType.NumberPassword` // Teclado numérico para PIN o contraseñas numéricas

> **Importante:** `keyboardType` solo cambia el teclado que se muestra, **no valida ni filtra** lo que entra en el campo. Si necesitas garantizar que solo haya números, filtra el valor dentro de `onValueChange`. Del mismo modo, `KeyboardType.Password` y `KeyboardType.NumberPassword` **no ocultan el texto**: para mostrar puntos en lugar de caracteres añade `visualTransformation = PasswordVisualTransformation()`.

## 4. TextField con contorno (OutlinedTextField)

```kotlin
@Composable
fun OutLineTextFieldSample() {
    var text by remember { mutableStateOf("") }
    OutlinedTextField(
        value = text,
        label = { Text(text = "Enter Your Name") },
        onValueChange = {
            text = it
        }
    )
}
```

En lugar de la función ***TextField()*** usamos ***OutlinedTextField()***, que acepta los mismos parámetros.

Crea un borde de contorno alrededor del campo, con menos énfasis visual que la versión rellena (filled).

## 5. TextField con iconos

```kotlin
@Composable
fun TextFieldWithIcons() {
    var text by remember { mutableStateOf("") }
    OutlinedTextField(
        value = text,
        leadingIcon = { Icon(imageVector = Icons.Default.Email, contentDescription = "emailIcon") },
        //trailingIcon = { Icon(imageVector = Icons.Default.Add, contentDescription = null) },
        onValueChange = {
            text = it
        },
        label = { Text(text = "Email address") },
        placeholder = { Text(text = "Enter your e-mail") },
    )
}
```

- `leadingIcon`: añade un icono en la zona inicial (al principio del campo).
- `trailingIcon`: añade un icono en la zona final (al final del campo).

> Usa `contentDescription = null` en iconos puramente decorativos y una descripción real cuando el icono sea interactivo o aporte información (accesibilidad).

**Código fuente:**

<https://github.com/JetpackCompose/Jetpack-Compose-Samples>
