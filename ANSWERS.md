# Respuestas — Interactive Profile Card

## 1. ¿Por qué escribimos `onPress={handlePress}` y no `onPress={handlePress()}`?

Con `onPress={handlePress}` le paso la función al botón para que la use cuando lo presionen. Si pongo `handlePress()` la función se ejecuta apenas carga la pantalla, no cuando presiono, y el botón no hace nada.

## 2. ¿Cuál es la diferencia entre `Button` y `Pressable`? ¿Cuándo elegiría cada uno?

`Button` es un componente simple que solo recibe `title`, `color` y `onPress`, no tiene la propiedad `style`, y su apariencia depende de la plataforma. `Pressable` es un contenedor al que le puedo poner cualquier contenido y estilo, y además me dice si está siendo presionado. Elegiría `Button` para una acción rápida sin diseño especial, como mi "Share profile", y `Pressable` cuando necesito un diseño propio, como los botones Follow y Message.

## 3. ¿Qué recibe la función `style` de `Pressable` y qué devuelve? Da un ejemplo.

Recibe un objeto con la propiedad `pressed`, que es `true` mientras el dedo está sobre el botón y `false` cuando lo suelto. Devuelve el estilo que se va a aplicar, que puede ser un objeto o un arreglo de estilos. Por ejemplo: `style={({ pressed }) => [styles.button, pressed && styles.pressed]}`, que hace que el botón se vea semitransparente mientras lo mantengo presionado.

## 4. ¿Por qué no se puede cambiar una variable de estado directamente (`isFollowing = true`) y qué se hace en su lugar?

Porque si lo cambio directo, React no se da cuenta y la pantalla no se actualiza. Hay que usar la función del `useState`, en mi caso `setIsFollowing(!isFollowing)`, y así React vuelve a dibujar la pantalla con el valor nuevo.

## 5. ¿Por qué `followers` no es un segundo `useState`? ¿Qué es un valor derivado?

Porque los seguidores se pueden sacar de `isFollowing`: son 1200 y se suma 1 si estoy siguiendo (`BASE_FOLLOWERS + (isFollowing ? 1 : 0)`). Un valor derivado es un valor que se calcula a partir de otro estado, así que no necesito guardarlo aparte.

## 6. ¿Qué significa *controlled input* en `TextInput`? ¿Qué dos props lo hacen controlado?

Significa que el texto que se ve en el campo lo maneja el estado de React, y no el `TextInput` por su cuenta. Lo hacen controlado las props `value` y `onChangeText`: con `value={message}` el campo muestra lo que hay en el estado, y con `onChangeText={(newText) => setMessage(newText)}` cada letra que escribo actualiza ese estado.

## 7. ¿Por qué `selectedSkills.push(skill)` está mal cuando `selectedSkills` es estado? Escribe el código correcto.

Porque `push` cambia el arreglo original y en el estado no se debe modificar directo, hay que crear un arreglo nuevo. Lo correcto es `setSelectedSkills([...selectedSkills, skill])` para agregar, y `setSelectedSkills(selectedSkills.filter((item) => item !== skill))` para quitar.