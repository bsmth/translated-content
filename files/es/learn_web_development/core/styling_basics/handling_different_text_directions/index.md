---
title: Manejando diferentes direcciones de texto
slug: Learn_web_development/Core/Styling_basics/Handling_different_text_directions
original_slug: Learn/CSS/Building_blocks/Handling_different_text_directions
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/CSS/Building_blocks/Backgrounds_and_borders", "Learn/CSS/Building_blocks/Overflowing_content", "Learn/CSS/Building_blocks")}}

Muchas de las propiedades y valores que hemos encontrado hasta ahora en nuestro aprendizaje de CSS han estado ligadas a las dimensiones físicas de nuestra pantalla. Creamos bordes arriba, a la derecha, abajo y a la izquierda de una caja, por ejemplo. Estas dimensiones físicas se ajustan adecuadamente al contenido que se visualiza de forma horizontal, y por defecto, la web tiende a apoyar lenguajes de izquierda a derecha, como el castellano o el francés, mejor que aquellos que se escriben de derecha a izquierda, como el árabe.

Sin embargo, en los últimos años, CSS ha evolucionado para soportar de mejor forma contenidos en diferente direccionalidad, incluyendo contenido de derecha a izquierda, pero también de arriba-abajo, como el japonés - Estas direccionalidades se llaman **modos de escritura**. En la medida que progresa tu estudio y comiences a trabajar con diseños, comprender los modos de escritura será de mucha utilidad para ti, por ello los explicaremos a continuación.

<table>
  <tbody>
    <tr>
      <th scope="row">Prerrequisitos:</th>
      <td>
        Literatura computacional básica,
        <a
          href="/es/docs/Learn/Getting_started_with_the_web/Installing_basic_software"
          >software básico instalado</a
        >, conocimiento básico de
        <a href="/es/docs/Learn/Getting_started_with_the_web/Dealing_with_files"
          >manejo de archivos</a
        >, HTML básico (<a href="/es/docs/Learn/HTML/Introduction_to_HTML"
          >Introducción a HTML</a
        >), y una idea de cómo funciona CSS (<a
          href="/es/docs/Learn/CSS/First_steps"
          >Primeros pasos en CSS</a
        >.)
      </td>
    </tr>
    <tr>
      <th scope="row">Objetivo:</th>
      <td>
        Entender la importancia de los modos de escritura en el CSS moderno.
      </td>
    </tr>
  </tbody>
</table>

## ¿Qué son los modos de escritura?

Un modo de escritura en CSS se refiere a si el texto está escrito horizontal o verticalmente. La propiedad {{cssxref("writing-mode")}} permite cambiar de un modo a otro. No necesitas estar trabajando en un lenguaje que use un modo de escritura vertical para querer hacer esto - Podrías cambiar el modo de escritura de partes de tu diseño por razones creativas.

En el ejemplo siguiente existe un encabezado desplegado usando `writing-mode: vertical-rl`. El texto ahora aparece vertical. El texto vertical es común en diseño gráfico, y puede ser una forma de agregar un aspecto más interesante a tu diseño web.

```html live-sample___simple-vertical
<h1>Play with writing modes</h1>
```

```css live-sample___simple-vertical
body {
  font-family: sans-serif;
  height: 300px;
}
h1 {
  writing-mode: vertical-rl;
  color: white;
  background-color: black;
  padding: 10px;
}
```

{{EmbedLiveSample("simple-vertical", "", "350px")}}

Los tres valores posibles para la propiedad [`writing-mode`](/es/docs/Web/CSS/writing-mode) son:

- `horizontal-tb`: Dirección de flujo de bloque de arriba abajo. Las frases aparecen horizontales.
- `vertical-rl`: Dirección de flujo de bloque de derecha a izquierda. Las frases aparecen verticales.
- `vertical-lr`: Dirección de flujo de bloque de izquierda a derecha. Las frases aparecen verticales.

Así, la propiedad `writing-mode` está configurando en realidad la direccion en que los elementos de nivel bloque son desplegados en la página - ya sea de arriba abajo, derecha a izquierda, o de izquierda a derecha. Luego señala la dirección del flujo de texto en las frases.

## Modos de escritura y diseño en bloque y lineal

Ya hemos visto el diseño en bloque y lineal, y el hecho de que algunas cosas se muestran como elementos de bloque y otras como elementos lineales. Ésto se encuentra ligado al modo de escritura del documento, y no de la pantalla física. Los bloques sólo se presentan desde la parte superior a la inferior de la página si estas usando un modo de escritura que presente el texto horizontalmente, como el español.

Con el siguiente ejemplo quedará más claro. Si tienes dos cajas que contengan un `heading` y un `paragraph`. La primera usa `writing-mode: horizontal-tb`, un modo de escritura horizontal y desde la parte superior de la página a la base. La segunda usa `writing-mode: vertical-rl`; este es un modo de escritura vertical y de derecha a izquierda.

```html live-sample___block-inline
<div class="wrapper">
  <div class="box horizontal">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
  </div>
  <div class="box vertical">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
  </div>
</div>
```

```css live-sample___block-inline
body {
  font-family: sans-serif;
  height: 300px;
}
.wrapper {
  display: flex;
}

.box {
  border: 1px solid #ccc;
  padding: 0.5em;
  margin: 10px;
}

.horizontal {
  writing-mode: horizontal-tb;
}

.vertical {
  writing-mode: vertical-rl;
}
```

{{EmbedLiveSample("block-inline", "", "350px")}}

Cuando cambiamos el modo de escritura, estamos cambiando que dirección es en bloque y cuál es lineal. En un modo de escritura `horizontal-tb` La direccion del bloque va de arriba abajo; en un modo de escritura `vertical-rl` el bloque corre de derecha a izquierda horizontalmente. De esta forma la **dimensión del bloque** es siempre la direccion en la que se muestran los bloques en el modo de escritura en uso. La **dimensión lineal**, es siempre la dirección en que fluye una frase.

Este dibujo muestra las dos dimensiones en un modo de escritura horizontal.![Showing the block and inline axis for a horizontal writing mode.](horizontal-tb.png)

Este dibujo muestra las dos dimensiones en un modo de escritura vertical.

![Showing the block and inline axis for a vertical writing mode.](vertical.png)

Una vez que empieces a observar el diseño CSS, y en particular los nuevos métodos de diseño, esta idea de bloque y lineal cobra mayor importancia. Será revisado más adelante.

### Dirección

Además del modo de escritura también tenemos la dirección del texto. Como se mencionó antes, algunos idiomas como el Árabe se escriben horizontalmente, de derecha a izquierda. Esto no es algo que usarías en un sentido creativo. Si tu simplemente quieres alinear algún elemento a la derecha, existen otras formas de hacerlo. Sin embargo es importante entender esto como parte de la naturaleza del CSS. La web no es solo para lenguajes que son escritos de izquierda a derecha!

Debido al hecho de que el modo de escritura y la dirección del texto pueden cambiar, los nuevos métodos de diseño CSS no toman como referencia la izquierda y derecha, ni la parte superior e inferior. En su lugar, hablarán de inicio y fin junto con esta idea de en línea y bloque. No te preocupes mucho por eso en este momento, pero ten en cuenta estas ideas a medida que empiezas a mirar el diseño de una página web; va a ser de gran ayuda en tu entendimiento de CSS.

## Valores y propiedades lógicas

La razón de hablar acerca de modos de escritura y dirección en este punto en tu aprendizaje, es por el hecho de que ya vimos muchas de estas propiedades que están atadas a las dimensiones físicas de la pantalla, y tienen más sentido cuando está en un modo de escritura horizontal.

Vamos a echarle un vistzo a nuestras dos cajas de nuevo, una con el modo escritura `horizontal-tb` y otro con `vertical-rl`. Le hemos dado a estas dos cajas un {{cssxref("width")}}. Puedes ver que cuando la caja está en el modo de escritura vertical, aún tiene una anchura, y esto está causando que el texto se desborde.

```html live-sample___width
<div class="wrapper">
  <div class="box horizontal">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
    <p>These boxes have a width.</p>
  </div>
  <div class="box vertical">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
    <p>These boxes have a width.</p>
  </div>
</div>
```

```css live-sample___width
body {
  font-family: sans-serif;
  height: 300px;
}
.wrapper {
  display: flex;
}

.box {
  border: 1px solid #ccc;
  padding: 0.5em;
  margin: 10px;
  width: 100px;
}

.horizontal {
  writing-mode: horizontal-tb;
}

.vertical {
  writing-mode: vertical-rl;
}
```

{{EmbedLiveSample("width", "", "350px")}}

Lo que nosotros realmente queremos en este escenario, es esencialmente intercambiar altura y anchura junto con el modo de escritura. Cuando estamos en el modo de escritura vertical, queremos que la caja se expanda en la dimensión del bloque así como lo hace en el modo horizontal.

Para hacerlo más fácil, CSS ha desarrollado recientemente un conjunto de propiedades asignadas. Estas esencialmente reemplazan las propiedades físicas como `width` and `height`, con versiones **lógicas** o **relativas al flujo**.

La propiedad asignada a `width` cuando está en el modo de escritura horizontal se llama {{cssxref("inline-size")}}, se refiere al tamaño en la dimensión inline. La propiedad para `height` se llama {{cssxref("block-size")}} y es el tamaño en la dimensión de bloque. Puedes ver como funciona en el ejemplo de abajo, donde reemplazamos `width` con `inline-size`.

```html live-sample___inline-size
<div class="wrapper">
  <div class="box horizontal">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
    <p>These boxes have inline-size.</p>
  </div>
  <div class="box vertical">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
    <p>These boxes have inline-size.</p>
  </div>
</div>
```

```css live-sample___inline-size
.wrapper {
  display: flex;
}

.box {
  border: 1px solid #ccc;
  padding: 0.5em;
  margin: 10px;
  inline-size: 100px;
}

.horizontal {
  writing-mode: horizontal-tb;
}

.vertical {
  writing-mode: vertical-rl;
}
```

{{EmbedLiveSample("inline-size", "", "300px")}}

### Propiedades lógicas `margin`, `border` y `padding`

En las últimas dos lecciones aprendimos acerca del modelo de cajas con CSS, y los bordes CSS. En las propiedades margin, border y padding vas a encontrar varias instancias de propiedades físicas, por ejemplo {{cssxref("margin-top")}}, {{cssxref("padding-left")}}, y {{cssxref("border-bottom")}}. Del mismo modo que tenemos asignaciones para ancho y alto, hay asignaciones para estas propiedades.

La propiedad `margin-top` está asignada a {{cssxref("margin-block-start")}}, esto siempre se va a referir al margen al inicio de la dimensión del bloque.

La propiedad {{cssxref("padding-left")}} se asigna a {{cssxref("padding-inline-start")}}, el padding que se aplica al inicio de la dirección inline. Aquí será donde las oraciones comienzan en ese modo de escritura. La propiedad {{cssxref("border-bottom")}} se asigna a {{cssxref("border-block-end")}}, que es el borde del final de la dimensión del bloque.

Puedes ver una comparación entre las propiedades físicas y lógicas a continuación.

**Si cambias el modo de escritura de las cajas asignando a la propiedad `writing-mode` en `.box` a `vertical-rl`, vas a ver como las propiedades físicas se quedan ligadas a sus direcciones físicas, mientras que las propiedades lógicas cambian con el modo de escritura.**

**También puedes ver que el {{htmlelement("h2")}} tiene un `border-bottom` negro. ¿Puedes averiguar como hacer que el borde inferior siempre esté debajo del texto en ambos modos de escritura?**

```html live-sample___logical-mbp
<div class="wrapper">
  <div class="box physical">
    <h2>Physical Properties</h2>
    <p>A paragraph demonstrating logical properties in CSS.</p>
  </div>
  <div class="box logical">
    <h2>Logical Properties</h2>
    <p>A paragraph demonstrating logical properties in CSS.</p>
  </div>
</div>
```

```css live-sample___logical-mbp
.wrapper {
  display: flex;
  border: 5px solid #ccc;
}

.box {
  margin-right: 30px;
  inline-size: 200px;
  writing-mode: horizontal-tb;
}

.logical {
  margin-block-start: 20px;
  padding-inline-end: 2em;
  padding-block-start: 2px;
  border-block-start: 5px solid pink;
  border-inline-end: 10px dotted rebeccapurple;
  border-block-end: 1em double orange;
  border-inline-start: 1px solid black;
}

.physical {
  margin-top: 20px;
  padding-right: 2em;
  padding-top: 2px;
  border-top: 5px solid pink;
  border-right: 10px dotted rebeccapurple;
  border-bottom: 1em double orange;
  border-left: 1px solid black;
}

h2 {
  border-bottom: 5px solid black;
}
```

{{EmbedLiveSample("logical-mbp", "", "200px")}}

Existe un gran número de propiedades cuando consideras cada uno de los bordes que puedes hacer a mano, y puedes ver todas las propiedades asignadas en la página de MDN para [propiedades Lógicas y Valores](/es/docs/Web/CSS/CSS_logical_properties_and_values)

### Valores lógicos

Hasta ahora hemos examinado los nombres de las propiedades lógicas. Existen también algunas propiedades que toman valores físicos de `top`, `right`, `bottom`, y `left`. Estos valores también tienen asignaciones a valores lógicos: `block-start`, `inline-end`, `block-end`, y `inline-start`.

Por ejemplo, puedes hacer que una imagen flote a la izquierda para hacer que el texto se ajuste alrededor de la imagen. Puedes reemplazar `left` con `inline-start` como se muestra en el ejemplo a continuación.

**Cambia el modo de escritura en este ejemplo a `vertical-rl` para ver que sucede con la imagen. Cambia `inline-start` por `inline-end` para cambiar el modo en que flota.**

```html live-sample___float
<div class="wrapper">
  <div class="box logical">
    <img
      alt="star"
      src="https://mdn.github.io/shared-assets/images/examples/big-star.png" />
    <p>
      This box uses logical properties. The star image has been floated
      inline-start, it also has a margin on the inline-end and block-end.
    </p>
  </div>
</div>
```

```css live-sample___float
.wrapper {
  display: flex;
}

.box {
  margin: 10px;
  padding: 0.5em;
  border: 1px solid #ccc;
  inline-size: 200px;
  writing-mode: horizontal-tb;
}

img {
  float: inline-start;
  margin-inline-end: 10px;
  margin-block-end: 10px;
}
```

{{EmbedLiveSample("float", "", "200px")}}

Aquí también estamos usando valores lógicos de margen para asegurar que el margen está en el sitio correcto sin importar que modo de escritura es.

> [!NOTE]
> Actualmente, solo Firefox soporta valores relativos de flujo para `float`. Si estás usando **Google Chrome** o **Microsoft Edge**, deberías ver que la imagen no flota.

### ¿Debería usar propiedades físicas o lógicas?

Las propiedades lógicas y los valores son más recientes que su equivalente físico, y por lo tanto se han implementado recientemente en los navegadores. Puedes revisar cualquier página de propiedades en MDN para ver hasta donde llega el soporte del navegador. Si no estás usando multiples modos de escritura, entonces, por ahora, deberías preferir usar las versiones físicas. Sin embargo, en última instancia, esperamos que la gente va a pasar a las versiones lógicas para la mayoría de las cosas, ya que tienen mucho sentido una vez que comienzas a tratar también con métodos de diseño como Flexbox y Grid.

## ¡Prueba tus habilidades!

Tenemos mucho terreno cubierto en este artículo, pero puedes recordad la información más importante? Puedes encontrar algunas pruebas adicionales para verificar que has retenido esta información antes de seguir adelante: [Prueba tus habilidades: modos de escritura.](/es/docs/Learn/CSS/Building_blocks/Writing_Modes_Tasks)

## Resumen

Los conceptos explicados en esta lección son cada vez más importantes en CSS. Un entendimiento pleno de las direcciones en bloque y en línea, y como el flujo de texto cambia con la variación de los modos de escritura, van a ser de gran ayuda en el futuro. Te ayudará a entender CSS incluso si nunca usas un modo de escritura diferente al horizontal.

En el módulo siguiente, vamos a echar un buen vistazo al desbordamiento en CSS

{{PreviousMenuNext("Learn/CSS/Building_blocks/Backgrounds_and_borders", "Learn/CSS/Building_blocks/Overflowing_content", "Learn/CSS/Building_blocks")}}
