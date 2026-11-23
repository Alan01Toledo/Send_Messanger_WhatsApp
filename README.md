# Send_Messanger_WhatsApp

Scripts en JavaScript que envían mensajes de forma automática por **WhatsApp Web**. Se pegan en la consola del navegador y mandan un mensaje por cada línea del texto que les indiques.

## Cómo funciona

El script `enviarScript(scriptText)` hace lo siguiente:

1. Divide el texto recibido en líneas (separadas por saltos de línea o tabulaciones) y descarta las vacías.
2. Busca la conversación abierta en WhatsApp Web (`#main`) y su cuadro de texto.
3. Por cada línea: escribe el mensaje, espera a que aparezca el botón de enviar y le da clic.
4. Espera 500 ms entre mensajes y, al terminar, muestra en consola cuántos se enviaron.

Para ubicar el botón de enviar prueba varios selectores (`aria-label` en español e inglés, `data-icon`, etc.), por si WhatsApp cambia su interfaz.

## Requisitos

- Un navegador de escritorio (Chrome, Edge, Firefox…).
- Sesión iniciada en [WhatsApp Web](https://web.whatsapp.com).
- Una conversación abierta, que es donde se enviarán los mensajes.

## Uso

1. Abre [web.whatsapp.com](https://web.whatsapp.com) e inicia sesión.
2. Abre la conversación a la que quieres enviar los mensajes.
3. Abre la consola del navegador (`F12` → pestaña **Consola**, o `Ctrl + Shift + J`).
4. Copia el contenido del script (por ejemplo `BeeMovie.js`) y edita el texto al final, una línea por mensaje:

   ```js
   enviarScript(`
   Mensaje 1
   Mensaje 2
   Mensaje 3
   `)
     .then(e => console.log(`Código finalizado, ${e} mensajes enviados`))
     .catch(console.error);
   ```

5. Pégalo en la consola y presiona `Enter`.

Verás cada mensaje impreso en la consola mientras se envía.

> Si es la primera vez que pegas código en la consola, es posible que el navegador te pida escribir `allow pasting` antes de permitirlo.

## Ajustes

| Qué cambiar | Dónde |
| --- | --- |
| Tiempo entre mensajes | `await sleep(500);` al final del ciclo (en milisegundos) |
| Tiempo máximo de espera del botón | `i < 20` con `sleep(100)` (20 × 100 ms = 2 s) |
| Selectores del botón de enviar | Función `getSendButton` |

## Errores comunes

| Mensaje | Causa y solución |
| --- | --- |
| `No hay una conversación abierta` | Abre un chat antes de ejecutar el script. |
| `No se encontró el cuadro de texto` | WhatsApp Web no terminó de cargar o cambió su estructura. Recarga la página. |
| `No se encontró el botón de enviar` | WhatsApp cambió el botón. Agrega el nuevo selector en `getSendButton`. |

## Aviso importante

Automatizar mensajes en WhatsApp puede ir en contra de sus [Términos de Servicio](https://www.whatsapp.com/legal/terms-of-service) y tu cuenta podría ser limitada o bloqueada, sobre todo si envías muchos mensajes seguidos o a personas que no te conocen. Úsalo con moderación, solo con fines personales o de aprendizaje, y bajo tu propia responsabilidad. No lo uses para spam.

## Estructura del repositorio

```
.
├── BeeMovie.js   # Script principal de envío de mensajes
├── Sh            # Script adicional
└── README.md
```
