# El cielo de Sara Eunice

Un cielo nocturno con 6 constelaciones. Cada estrella es una razón.
Hecho para verse en un teléfono.

Todo vive en **un solo archivo**: `index.html`. No hay que instalar nada, no hay
build, no hay dependencias. Se abre con doble clic y funciona.

---

## Cómo editar el contenido

Abre `index.html` con cualquier editor de texto (hasta el Bloc de notas sirve) y
busca el bloque que empieza así, casi al principio:

```
★  C O N T E N I D O  ★
```

Ahí está **todo** lo que se lee: el versículo de la apertura, las 6
constelaciones con sus razones, la carta de la estrella dorada y el texto final.
Nada de lo que está debajo de la marca `★ M O T O R ★` hace falta tocarlo.

### Cambiar una razón
Busca la constelación y edita el texto entre comillas. Nada más.

### Agregar o quitar una razón
1. Agrega (o quita) el texto en `razones`.
2. Agrega (o quita) su coordenada en `nodos`, en la **misma posición**.
3. Revisa `lineas`: son los pares de estrellas que se unen.
   `[0,1]` une la primera con la segunda, `[1,2]` la segunda con la tercera, etc.

El contador (`0 / 35`) y el corazón del final se recalculan solos: el corazón
reparte las estrellas que haya a lo largo de su contorno. No hay ningún número
que actualizar a mano.

### Las coordenadas
`nodos` usa un lienzo imaginario de **1000 de ancho por 1800 de alto**.
El `0,0` está arriba a la izquierda. Mover una estrella es cambiarle esos dos
números; conviene hacerlo de 20 en 20 e ir viendo el resultado.

### La estrella dorada
Su posición, la fecha, el rótulo, los párrafos de la carta y la firma están en
el bloque `dorada`. El aviso de cuando la tocan antes de tiempo está en
`cielo.avisoDorada` (la `{n}` se reemplaza sola por las que falten).

---

## La música

El botón ya está puesto, apagado por defecto. Solo falta el archivo:

1. Consigue un mp3 suave (instrumental, sin letra, funciona mejor).
2. Ponlo junto a `index.html` con el nombre exacto **`musica.mp3`**.

Si el archivo no existe, el botón se esconde solo. No se rompe nada.
El volumen sube poco a poco al encenderlo, para que no la asuste si lo abre en
la calle.

---

## Subirlo a internet

Cualquiera de las dos opciones funciona igual de bien. **Sube solo
`index.html`** (y `musica.mp3` si lo agregaste). Los archivos `Design.html` y
`Design.pdf` son del diseño, no hacen falta y pesan mucho.

### Opción A — Vercel (la más rápida, y le da un link más bonito)
1. Entra a [vercel.com](https://vercel.com) y crea una cuenta.
2. En el panel, busca la opción de desplegar y **arrastra la carpeta** con el
   `index.html` dentro.
3. Listo. Te da un link tipo `https://algo.vercel.app` con HTTPS.
4. En *Settings → Domains* puedes cambiarle el nombre a algo como
   `cielo-de-sara.vercel.app`.

### Opción B — GitHub Pages
1. Crea un repositorio nuevo, **público**.
2. Sube `index.html`.
3. *Settings → Pages → Source: Deploy from a branch → main / (root)*.
4. En un par de minutos queda en `https://tuusuario.github.io/tu-repo/`.

> Nota: tiene que ser un repositorio público para que Pages funcione gratis. Si
> prefieres que nadie más lo encuentre por casualidad, usa Vercel: el link no se
> indexa (la página ya lleva `noindex`) y nadie llega sin que se lo pases.

---

## Detalles que conviene saber

- **Las leídas cambian de color.** Al cerrar una razón, esa estrella suelta un
  destello y se queda en rosa (su rojo, aclarado para que se vea bien sobre el
  fondo). Las que faltan siguen en blanco cálido, y la dorada sigue siendo la
  única dorada. Así se distinguen las tres cosas de un vistazo.
- **Guarda el avance.** Las estrellas que ya leyó quedan marcadas aunque cierre
  la página. Se guarda en su propio teléfono, no en ningún servidor.
- **Empezar de cero.** Si quieres probarla tú sin gastarle la sorpresa, ábrela
  con `?reset=1` al final del link. Por ejemplo:
  `https://cielo-de-sara.vercel.app/?reset=1`
- **Si se pierde.** Si no encuentra las que le faltan, puede tocar el contador
  de la esquina: las que no ha leído parpadean unos segundos.
- **Doble toque para acercar.** Además del pellizco, dos toques seguidos en una
  zona vacía acercan, y otros dos alejan. Es la salida por si el pellizco se le
  complica.
- **La estrella dorada** se ve desde el principio pero no abre hasta que haya
  leído las 35. Antes de eso avisa cuántas faltan.
- **El final** (el corazón) solo se lanza desde el botón al terminar la carta.
  Se puede salir de la carta con la ✕ de arriba si quiere seguir viendo el cielo.

---

## Cómo se ve por dentro

- **Canvas** para el cielo: las ~455 estrellas se dibujan con sprites
  pre-renderizados en vez de sombras, que es lo que permite que corra bien en un
  teléfono de gama media. En pantallas chicas baja solo la cantidad de estrellas
  decorativas y limita la resolución.
- **HTML y CSS** para todo lo que es texto, para que la tipografía se vea bien.
- **Las nebulosas** no son manchas redondas: cada nube se fabrica una sola vez
  al abrir la página juntando ~200 manchas irregulares alrededor de unos pocos
  núcleos, y después se le abren calles de polvo oscuro. Eso es lo que le da
  forma de nebulosa de verdad. Una vez hecha la textura, dibujarla cuesta una
  sola operación por cuadro. Son dos: la roja (su color) y la azul (el mío). El
  morado del centro no está pintado: sale de que se cruzan.
- Respeta `prefers-reduced-motion` si tiene activado el ahorro de movimiento.

Los ajustes finos (cantidad de estrellas de fondo, zoom máximo, a partir de qué
acercamiento se dibujan las líneas) están en `CONTENIDO.ajustes`.
