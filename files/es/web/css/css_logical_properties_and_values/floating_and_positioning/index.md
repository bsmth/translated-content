---
title: Propiedades lógicas para flotantes y posicionamiento
slug: Web/CSS/CSS_logical_properties_and_values/Floating_and_positioning
---

{{CSSRef}}

La [especificación de Propiedades y Valores Lógicos](https://drafts.csswg.org/css-logical/) contiene una asignación para los valores físicos {{cssxref("float")}} y {{cssxref("clear")}}, y también para las propiedades de posicionamiento usadas con [positioned layout](/es/docs/Web/CSS/CSS_positioned_layout). Esta guía nos permite saber cómo utilizar estas propiedades.

## Asignando propiedades y valores

La tabla a continuación detalla las propiedades y valores discutidos en esta guía junto con sus asignaciones físicas. Estas, asumen un modo de escritura ({{cssxref("writing-mode")}}), con una dirección de izquierda a derecha (left-to-right).

| Propiedad o valor lógico           | Propiedad o valor lógico         |
| ---------------------------------- | -------------------------------- |
| {{cssxref("float")}}: inline-start | {{cssxref("float")}}: left       |
| {{cssxref("float")}}: inline-end   | {{cssxref("float")}}: right      |
| {{cssxref("clear")}}: inline-start | {{cssxref("clear")}}: left       |
| {{cssxref("clear")}}: inline-end   | {{cssxref("clear")}}: right      |
| {{cssxref("inset-inline-start")}}  | {{cssxref("left")}}              |
| {{cssxref("inset-inline-end")}}    | {{cssxref("right")}}             |
| {{cssxref("inset-block-start")}}   | {{cssxref("top")}}               |
| {{cssxref("inset-block-end")}}     | {{cssxref("bottom")}}            |
| {{cssxref("text-align")}}: start   | {{cssxref("text-align")}}: left  |
| {{cssxref("text-align")}}: end     | {{cssxref("text-align")}}: right |

Además de estas propiedades asignadas, hay algunas propiedades abreviadas adicionales que son posibles al poder abordar las dimensiones de bloque y en línea. Estos no tienen mapeo a las propiedades físicas.

| Propiedad lógica            | Propósito                                                                                      |
| --------------------------- | ---------------------------------------------------------------------------------------------- |
| {{cssxref("inset-inline")}} | Establece los dos valores de inserción anteriores para la dimensión en línea simultáneamente.  |
| {{cssxref("inset-block")}}  | Establece los dos valores de inserción anteriores para la dimensión de bloque simultáneamente. |
| {{cssxref("inset")}}        | Establece los cuatro valores de inserción simultáneamente.                                     |

## Flotante y ejemplo claro

Los valores físicos usados con las propiedades {{cssxref("float")}} y {{cssxref("clear")}} son `left`, `right` y `both`. La especificación de las Propiedades Lógicas definen los valores `inline-start` y `inline-end` como asignación para `left` y `right`.

En el ejemplo de abajo tenemos dos cajas — la primera tiene una caja flotante con `float: left`, la segunda con `float: inline-start`. Si tu cambias el modo de escritura (`writing-mode`) a `vertical-rl` o la dirección (`direction`) a `rtl` verás que la caja flotando a la izquierda siempre se queda en la izquierda, mientras que el ítem `inline-start`-floated sigue la dirección (`direction`) y el modo de escritura (`writing-mode`).

```html live-sample___float
<div class="container">
  <div class="inner">
    <div class="physical box"></div>
    Turnip greens yarrow ricebean rutabaga endive cauliflower sea lettuce
    kohlrabi amaranth water spinach avocado daikon napa cabbage asparagus winter
    purslane kale.
  </div>
  <div class="inner">
    <div class="logical box"></div>
    Turnip greens yarrow ricebean rutabaga endive cauliflower sea lettuce
    kohlrabi amaranth water spinach avocado daikon napa cabbage asparagus winter
    purslane kale.
  </div>
</div>
```

```css hidden live-sample___float
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
  width: 100px;
  height: 100px;
}
```

```css live-sample___float
.inner {
  /* direction: rtl; */
  /* writing-mode: vertical-rl; */
}

.physical {
  float: left;
}

.logical {
  float: inline-start;
}
```

{{EmbedLiveSample("float", "", "220px")}}

## Ejemplo: Propiedades de inserción para diseño posicionado

El posicionamiento generalmente nos permite posicionar un elemento de una manera relativa al bloque de contención — esencialmente, insertamos el elemento en relación con el lugar donde caería en función del flujo normal. Para hacer esto, hemos usado popiedades físicas como {{cssxref("top")}}, {{cssxref("right")}}, {{cssxref("bottom")}} y {{cssxref("left")}}.

Estas propiedades toman una longitud o un porcentaje como valor y se relacionan con las dimensiones de la pantalla del usuario.

Se han creado nuevas propiedades en la especificación de Propiedades Lógicas para cuando desee que el posicionamiento se relacione con el flujo de texto en su modo de escritura. Estos son los siguientes: {{cssxref("inset-block-start")}}, {{cssxref("inset-block-end")}}, {{cssxref("inset-inline-start")}} y {{cssxref("inset-inline-end")}}.

En el siguiente ejemplo hemos usado las propiedades `inset-block-start` y `inset-inline-end` para posicionar la caja azul usando un posicionamiento absoluto dentro del área con el borde punteado de color gris, que tiene `position: relative`. Podemos cambiar la propiedad de modo de escritura (`writing-mode`) a `vertical-rl`, o agregar `direction: rtl`, y ver cómo el cuadro de flujo relativo se mantiene con la dirección del texto.

```html live-sample___positioning-inset
<div class="container">
  <div class="inner">
    <div class="physical box"></div>
  </div>
  <div class="inner">
    <div class="logical box"></div>
  </div>
</div>
```

```css hidden live-sample___positioning-inset
.container {
  display: flex;
}

.inner {
  width: 200px;
  height: 200px;
  position: relative;
  border: 2px dotted grey;
}

.box {
  border: 2px solid rgb(96 139 168);
  border-radius: 5px;
  background-color: rgb(96 139 168 / 0.2);
  padding: 10px;
  width: 100px;
  height: 100px;
}
```

```css live-sample___positioning-inset
.inner {
  writing-mode: horizontal-tb;
}

.physical {
  position: absolute;
  top: 20px;
  right: 0;
}

.logical {
  position: absolute;
  inset-block-start: 20px;
  inset-inline-end: 0;
}
```

{{EmbedLiveSample("positioning-inset", "", "250px")}}

## Nuevas abreviaciones de dos- y cuatro-valores

Al igual que con otras propiedades en la especificación, tenemos algunas propiedades abreviadas nuevas, que permiten configurar dos o cuatro valores a la vez. Estos no tienen una equivalencia directa a propiedades físicas.

- {{cssxref("inset")}} — pone los cuatro lados juntos.
- {{cssxref("inset-inline")}} — pone los dos en línea juntos.
- {{cssxref("inset-block")}} — pone los dos bloques juntos.

> [!NOTE]
> Los navegadores que han implementado la especificación de propiedades lógicas han implementado hasta ahora las asignaciones directas y no las abreviaturas nuevas. Consulte la sección de datos de compatibilidad del navegador en cada referencia de página de propiedades para obtener más detalles.

## Ejemplo: Valores lógicos para text-align

La propiedad {{cssxref("text-align")}} tiene valores lógicos que se relacionan con la dirección del texto. — en lugar de usar `left` y `right` usamos `start` y `end`. En el siguiente ejemplo tenemos `text-align: right` en el primer bloque y `text-align: end` en el segundo.

Si cambias el valor de la dirección (`direction`) a `rtl` verás que la alineación permanece a la derecha para el primer bloque, pero va al extremo lógico en el segundo bloque.

```html live-sample___text-align
<div class="container">
  <div class="inner physical">Aligned text</div>
  <div class="inner logical">Aligned text</div>
</div>
```

```css hidden live-sample___text-align
body {
  font: 1.2em / 1.5 sans-serif;
}

.container {
  display: flex;
}

.inner {
  width: 200px;
  border: 2px dotted grey;
  padding: 10px;
}
```

```css live-sample___text-align
.inner {
  direction: ltr;
}

.physical {
  text-align: right;
}

.logical {
  text-align: end;
}
```

{{EmbedLiveSample("text-align")}}

Esto funciona de una manera más consistente cuando se usa la alineación de caja que usa inicio y final en lugar de direcciones físicas para la alineación.
