# Switch en Jetpack Compose (Material 3)

> Aprende a crear interruptores (Switch) en Jetpack Compose con Material 3: simples, con texto, con icono en el selector, con colores personalizados y deshabilitados.

*Básicos · Material 3*

**¿Qué es Switch?**

Switch es un componente (composable) de interfaz de usuario que permite activar o desactivar una única opción, con dos estados posibles: encendido y apagado. Se usa, por ejemplo, para ajustes como «Notificaciones», «Modo oscuro» o «Sincronización automática».

> *Si eres desarrollador de Android (Views):* es el equivalente a `SwitchMaterial` / `SwitchCompat`.

Todos los ejemplos usan la librería `androidx.compose.material3`.

## ¿Qué opciones hay disponibles en Switch?

Estos son los argumentos de la función `Switch` de Material 3:

```kotlin
@Composable
fun Switch(
    checked: Boolean,                                       // Estado actual: true = activado, false = desactivado
    onCheckedChange: ((Boolean) -> Unit)?,                  // Callback al pulsar el switch; si es null, el switch no es interactivo por sí mismo
    modifier: Modifier = Modifier,                          // Modificadores de tamaño, padding, semántica, etc.
    thumbContent: (@Composable () -> Unit)? = null,         // Contenido dentro del selector circular (p. ej. un icono)
    enabled: Boolean = true,                                // Si es false, no responde al usuario y se ve deshabilitado
    colors: SwitchColors = SwitchDefaults.colors(),         // Colores del switch en cada estado
    interactionSource: MutableInteractionSource? = null     // Observa interacciones (foco, pulsación...)
)
```

Dos detalles importantes de esta firma:

- `checked` y `onCheckedChange` no tienen valor por defecto: **el estado lo gestionas tú** (state hoisting). El switch no cambia solo; tienes que actualizar el estado dentro de `onCheckedChange`.
- `onCheckedChange` puede ser `null`. Es útil cuando otro elemento (por ejemplo, la fila completa con `toggleable`) se encarga de gestionar el clic.

> **Imports necesarios** para usar `by` con `mutableStateOf` en los ejemplos siguientes:
> `androidx.compose.runtime.getValue` y `androidx.compose.runtime.setValue`.

## 1. Switch simple

```kotlin
@Composable
fun SimpleSwitch() {
    var checked by remember { mutableStateOf(true) }
    Switch(
        checked = checked,
        onCheckedChange = { checked = it }
    )
}
```

En este ejemplo creamos una variable **checked**, que es un **mutableState** de tipo `Boolean`.

- **mutableState**: devuelve un valor observable para Compose. Si el valor cambia, la interfaz se recompone y se actualiza automáticamente.
- **remember**: conserva el valor entre recomposiciones. Si quieres que el estado sobreviva también a cambios de configuración (como girar la pantalla), usa `rememberSaveable` en su lugar.
- **onCheckedChange**: recibe el nuevo valor (`it`) cuando el usuario pulsa el switch. Si no lo guardas en el estado, el switch no cambia de posición.

Crea un switch sencillo, pero sin ninguna etiqueta que explique para qué sirve. Veremos cómo mejorarlo.

## 2. Switch con texto

El Switch de Compose no incluye etiqueta propia. Lo habitual es colocarlo en un `Row` junto a un `Text`:

```kotlin
@Composable
fun SwitchWithLabel() {
    var checked by remember { mutableStateOf(false) }
    Row(
        modifier = Modifier
            .fillMaxWidth()
            .toggleable(
                value = checked,
                role = Role.Switch,
                onValueChange = { checked = it }
            )
            .padding(16.dp),
        verticalAlignment = Alignment.CenterVertically,
        horizontalArrangement = Arrangement.SpaceBetween
    ) {
        Text(text = "Notificaciones")
        Switch(
            checked = checked,
            onCheckedChange = null
        )
    }
}
```

- `toggleable` en el `Row`: hace que se pueda pulsar toda la fila, no solo el switch, y mejora la accesibilidad (`role = Role.Switch`).
- `onCheckedChange = null`: como la fila ya gestiona el clic, el switch solo muestra el estado.

## 3. Switch con icono en el selector (thumbContent)

```kotlin
@Composable
fun SwitchWithIcon() {
    var checked by remember { mutableStateOf(true) }
    Switch(
        checked = checked,
        onCheckedChange = { checked = it },
        thumbContent = if (checked) {
            {
                Icon(
                    imageVector = Icons.Filled.Check,
                    contentDescription = null,
                    modifier = Modifier.size(SwitchDefaults.IconSize)
                )
            }
        } else {
            null
        }
    )
}
```

- `thumbContent`: dibuja contenido dentro del selector circular. Aquí mostramos un icono de verificación solo cuando el switch está activado.
- `SwitchDefaults.IconSize`: es el tamaño recomendado para el icono, para que encaje dentro del selector.
- `contentDescription = null`: el icono es decorativo, así que no necesita descripción para accesibilidad.

## 4. Colores personalizados

```kotlin
@Composable
fun SwitchWithCustomColors() {
    var checked by remember { mutableStateOf(true) }
    Switch(
        checked = checked,
        onCheckedChange = { checked = it },
        colors = SwitchDefaults.colors(
            checkedThumbColor = Color.White,        // Selector cuando está activado
            checkedTrackColor = Color(0xFF4CAF50),  // Pista cuando está activado
            uncheckedThumbColor = Color.Gray,       // Selector cuando está desactivado
            uncheckedTrackColor = Color.LightGray   // Pista cuando está desactivado
        )
    )
}
```

- `colors`: recibe un `SwitchColors`. Se obtiene con `SwitchDefaults.colors(...)` indicando solo los colores que quieres cambiar; el resto mantienen los valores del tema.
- Los parámetros siguen el patrón `checked...` / `unchecked...` / `disabled...` según el estado, y se aplican al selector (*thumb*), la pista (*track*), el borde (*border*) y el icono (*icon*).

## 5. Switch deshabilitado

```kotlin
@Composable
fun DisabledSwitch() {
    var checked by remember { mutableStateOf(true) }
    Switch(
        checked = checked,
        onCheckedChange = { checked = it },
        enabled = false
    )
}
```

Con `enabled = false`, el switch no responde a la interacción del usuario y se muestra con el aspecto de deshabilitado (también para los servicios de accesibilidad). Mantiene el valor de `checked` que le indiques.

## Buenas prácticas

- **Un switch, una opción:** Material Design recomienda usarlo para activar o desactivar un único ajuste, con efecto inmediato. Si el usuario debe confirmar con un botón, mejor un `Checkbox`.
- **Acompáñalo siempre de una etiqueta** visible que diga qué controla.
- **Guarda el estado fuera del composable** (por ejemplo, en un `ViewModel`) cuando el valor deba persistir o afectar a otras partes de la app.

**Documentación oficial:**

<https://developer.android.com/reference/kotlin/androidx/compose/material3/Switch.composable>
