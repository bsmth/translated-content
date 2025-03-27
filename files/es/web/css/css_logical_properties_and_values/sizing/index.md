---
title: Dimensionamiento para propiedades lógicas
slug: Web/CSS/CSS_logical_properties_and_values/Sizing
---

{{CSSRef}}

En esta guía explicaremos las asignaciones relativas al flujo relativo entre las propiedades de dimensionamiento físico y lógico usados para dimensionar elementos en nuestras páginas.

Cuando especificamos el tamaño de un ítem, las [Propiedades y Valores Lógicos](https://drafts.csswg.org/css-logical/) te dan la habilidad de indicar el dimensionamiento en relación al flujo relativo del texto (en línea y bloque) más bien que dimensionamiento físico con relación a las dimensiones físicas: horizontal y vertical (por ejemplo, left y right). Si bien estas asignaciones de flujo relativo pueden convertirse en el valor predeterminado para muchos de nosotros, en un diseño puede usar el tamaño físico y el tamaño lógico. Es posible que desee que algunas características se relacionen siempre con las dimensiones físicas, independientemente del modo de escritura.

## Asignaciones para dimensiones

La siguiente tabla proporciona asignaciones entre propiedades lógicas y físicas. Estas asignaciones asumen que estás en un modo de escritura `horizontal-tb`, como Inglés o Árabe, en cada caso el ancho ({{CSSxRef("width")}}) sería asignado a {{CSSxRef("inline-size")}}.

Si tú estás en un modo de escritura vertical, entonces {{CSSxRef("inline-size")}} sería asignado a {{CSSxRef("height")}}.

| Propiedades Lógicas            | Propiedades Físicas       |
| ------------------------------ | ------------------------- |
| {{CSSxRef("inline-size")}}     | {{CSSxRef("width")}}      |
| {{CSSxRef("block-size")}}      | {{CSSxRef("height")}}     |
| {{CSSxRef("min-inline-size")}} | {{CSSxRef("min-width")}}  |
| {{CSSxRef("min-block-size")}}  | {{CSSxRef("min-height")}} |
| {{CSSxRef("max-inline-size")}} | {{CSSxRef("max-width")}}  |
| {{CSSxRef("max-block-size")}}  | {{CSSxRef("max-height")}} |

## Ejemplo de ancho y alto

Las asignaciones para el ancho ({{CSSxRef("width")}}) y el alto ({{CSSxRef("height")}}) son {{CSSxRef("inline-size")}}, que establece el largo en la dimensión en línea y {{CSSxRef("block-size")}}, que establece el largo en la dimensión en bloque. Cuando trabajamos en Inglés, si reemplazamos el ancho (`width`) con `inline-size` y el alto (`height`) con `block-size` dará el mismo diseño.

En el siguiente ejemplo, establecemos un modo de escritura `horizontal-tb`. Cambiamos esto por `vertical-rl` y veremos que el primer ejemplo — cuando usamos `width` y `height` — permanece con el mismo tamaño en cada dimensión, a pesar de que el texto se vuelve vertical. El segundo ejemplo — cuando usamos `inline-size` y `block-size` — seguirá la dirección del texto como si todo el bloque hubiera girado.

```html live-sample___size-inline-block
<div class="container">
  <div class="physical box">I have a width of 200px and a height of 100px.</div>

  <div class="logical box">
    I have an inline-size of 200px and a block-size of 100px.
  </div>
</div>
```

```css hidden live-sample___size-inline-block
body {
  font: 1.2em / 1.5 sans-serif;
}
.container {
  display: flex;
}
.box {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
  padding: 10px;
  margin: 10px;
}
```

```css live-sample___size-inline-block
.box {
  writing-mode: horizontal-tb;
}

.physical {
  width: 200px;
  height: 100px;
}

.logical {
  inline-size: 200px;
  block-size: 100px;
}
```

{{EmbedLiveSample("size-inline-block")}}

## Ejemplo de ancho y alto mínimo

También hay asignaciones para {{CSSxRef ("min-width")}} y {{CSSxRef ("min-height")}} — estas son {{CSSxRef ("min-inline-size")}} y {{ CSSxRef ("min-block-size")}}. Estas funcionan de la misma manera que las propiedades de `inline-size` y `block-size`, pero establecen un tamaño mínimo en lugar de uno fijo.

Intente cambiar el siguiente ejemplo a `vertical-rl`, como en el primer ejemplo, para ver el efecto que tiene. Estoy usando `min-height` en el primer ejemplo y `min-block-size` en el segundo.

```html live-sample___size-min
<div class="container">
  <div class="physical box">
    I have a width of 200px and a min-height of 5em.
  </div>

  <div class="logical box">
    I have an inline-size of 200px and a min-block-size of 5em.
  </div>
</div>
```

```css hidden live-sample___size-min
body {
  font: 1.2em / 1.5 sans-serif;
}
.container {
  display: flex;
}
.box {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
  padding: 10px;
  margin: 10px;
}
```

```css live-sample___size-min
.box {
  writing-mode: horizontal-tb;
}

.physical {
  width: 200px;
  min-height: 5em;
}

.logical {
  inline-size: 200px;
  min-block-size: 5em;
}
```

{{EmbedLiveSample("size-min")}}

## Ejemplo de ancho y alto máximo

Finalmente, puedes usar {{CSSxRef("max-inline-size")}} y {{CSSxRef("max-block-size")}} como reemplazos de {{CSSxRef("max-width")}} y {{CSSxRef("max-height")}}. Intenta jugar con el siguiente ejemplo de la misma manera que antes.

```html live-sample___size-max
<div class="container">
  <div class="physical box">I have a max-width of 200px.</div>

  <div class="logical box">I have an max-inline-size of 200px.</div>
</div>
```

```css hidden live-sample___size-max
body {
  font: 1.2em / 1.5 sans-serif;
}
.container {
  display: flex;
}
.box {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
  padding: 10px;
  margin: 10px;
}
```

```css live-sample___size-max
.box {
  writing-mode: horizontal-tb;
}

.physical {
  max-width: 200px;
}

.logical {
  max-inline-size: 200px;
}
```

{{EmbedLiveSample("size-max")}}

## Palabras claves para redimensionamiento lógico

La propiedad {{CSSxRef("resize")}} establece si un elemento se puede redimensionar o no y si tiene valores físicos de `horizontal` y `vertical`. La propiedad `resize` también tiene valores de palabras clave lógicas. Usar `resize: inline` permite cambiar el tamaño en la dimensión inline y `resize: block` permite cambiar el tamaño en la dimensión de bloque.

El valor de la palabra clave de `both` para la propiedad de cambio de tamaño funciona ya sea que esté pensando física o lógicamente. Establece ambas dimensiones a la vez. Intenta jugar con el siguiente ejemplo.

```html live-sample___size-resize
<div class="container">
  <div class="physical box">
    I have a width of 200px and a height of 100px. I can be resized
    horizontally.
  </div>

  <div class="logical box">
    I have an inline-size of 200px and a block-size of 100px. I can be resized
    in the inline direction.
  </div>
</div>
```

```css hidden live-sample___size-resize
body {
  font: 1.2em / 1.5 sans-serif;
}
.container {
  display: flex;
}
.box {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
  padding: 10px;
  margin: 10px;
}
```

```css live-sample___size-resize
.box {
  writing-mode: horizontal-tb;
  overflow: scroll;
}

.physical {
  width: 200px;
  height: 100px;
  resize: horizontal;
}

.logical {
  inline-size: 200px;
  block-size: 100px;
  resize: inline;
}
```

{{EmbedLiveSample("size-resize")}}

> **Advertencia:** **Nota:** Tenga en cuenta que actualmente los valores lógicos para el cambio de tamaño solo son compatibles con Firefox.
