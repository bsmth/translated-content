---
title: Animaciones CSS
slug: Web/CSS/CSS_animations
l10n:
  sourceCommit: 856b52f634b889084869d2ee0b8bb62c084be04d
---

{{CSSRef}}

El módulo **Animaciones CSS** le permite animar los valores de las propiedades CSS, como la posición del fondo y transformaciones, a lo largo del tiempo mediante el uso de fotogramas clave. Cada fotograma clave describe cómo debe renderizarse el elemento animado en un momento dado durante la secuencia de animación. Puede usar las propiedades en el módulo de animaciones para controlar la duración, el número de repeticiones, el inicio retrasado y otros aspectos de una animación.

### Animaciones en acción

Para ver la animación en el cuadro a continuación, haga clic en la casilla de verificación 'Reproducir la animación' o pase el cursor sobre el cuadro. Cuando la animación está activa, la nube en la parte superior cambia de forma, caen copos de nieve y el nivel de nieve en la parte inferior aumenta. Para pausar la animación, desmarque la casilla de verificación o aleje el cursor de la casilla.

```html hidden live-sample___animation
<!-- See aria-label: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-label -->
<input
  type="checkbox"
  id="animate"
  aria-label="Toggle the play state of the animation" />
<label for="animate">the animation</label>
<div class="root">
  <i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i
  ><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i
  ><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i
  ><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i
  ><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i>
  <div class="cloud"></div>
  <div class="ground"></div>
</div>
```

```css hidden live-sample___animation
i {
  display: inline-block;
  height: 16px;
  width: 16px;
  border-radius: 50%;
  animation: falling 3s linear 0s infinite backwards;
  /* Snowflakes are made with CSS linear gradients (https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Images/Using_CSS_gradients) */
  background-image:
    linear-gradient(180deg, transparent 40%, white 40% 60%, transparent 60%),
    linear-gradient(90deg, transparent 40%, white 40% 60%, transparent 60%),
    linear-gradient(45deg, transparent 43%, white 43% 57%, transparent 57%),
    linear-gradient(135deg, transparent 43%, white 43% 57%, transparent 57%);
}
i:nth-of-type(4n) {
  /* Using tree structural pseudo-classes to create randomness - https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-of-type */
  height: 30px;
  width: 30px;
  transform-origin: right -30px;
}
i:nth-of-type(4n + 1) {
  height: 24px;
  width: 24px;
  transform-origin: left 30px;
}
i:nth-of-type(4n + 2) {
  height: 10px;
  width: 10px;
  transform-origin: -30px 0;
}
i:nth-of-type(4n + 3) {
  height: 40px;
  width: 40px;
  transform-origin: -50px 0;
}
i:nth-of-type(4n) {
  animation-duration: 5.3s;
  animation-iteration-count: 12;
  transform-origin: -10px -20px;
}
i:nth-of-type(4n + 1) {
  animation-duration: 3.1s;
  animation-iteration-count: 20;
  transform-origin: 10px -20px;
}
i:nth-of-type(4n + 2) {
  animation-duration: 1.7s;
  animation-iteration-count: 35;
  transform-origin: right -20px;
}
i:nth-of-type(3n) {
  animation-delay: 2.3s;
}
i:nth-of-type(3n + 1) {
  animation-delay: 1.5s;
}
i:nth-of-type(3n + 2) {
  animation-delay: 3.4s;
}
i:nth-of-type(5n) {
  animation-timing-function: ease-in-out;
}
i:nth-of-type(5n + 1) {
  animation-timing-function: ease-out;
}
i:nth-of-type(5n + 2) {
  animation-timing-function: ease;
}
i:nth-of-type(5n + 3) {
  animation-timing-function: ease-in;
}
i:nth-of-type(5n + 4) {
  animation-timing-function: linear;
}
i:nth-of-type(11n) {
  animation-timing-function: cubic-bezier(0.2, 0.3, 0.8, 0.9);
}
i:nth-of-type(7n) {
  opacity: 0.5;
}
i:nth-of-type(7n + 2) {
  opacity: 0.3;
}
i:nth-of-type(7n + 4) {
  opacity: 0.7;
}
i:nth-of-type(7n + 6) {
  opacity: 0.6;
  animation-timing-function: ease-in;
  transform-origin: left 10px;
}
i:nth-of-type(7n + 1) {
  opacity: 0.8;
}

.root {
  height: 580px;
  background-color: skyblue;
  border: 1px solid darkgrey;
  position: relative;
  overflow: hidden;
}
.ground,
.cloud {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  background-repeat: no-repeat;
}
.cloud {
  width: 100%;
  height: 150px;
  background: #ffffff;
  border-radius: 0 0 90px 33% / 0 0 45px 50px;
  box-shadow:
    5px 15px 15px white,
    -5px 15px 15px white,
    0 20px 20px rgb(125 125 125 / 0.5);
  animation:
    clouds ease 5s alternate infinite 0.2s,
    wind ease-out 4s alternate infinite;
}
.ground {
  bottom: 0;
  background-image: linear-gradient(to top, #fff 97%, 99%, #bbb 100%);
  background-position: center 580px;
  animation: snowfall linear 300s forwards;
  border: 1px solid grey;
  /* Put the ground into a 3D rendering context (because the snow flakes are in a 3d rendering context) */
  transform: translate3d(0, 0, 0);
}

@keyframes snowfall {
  from {
    background-position: center 580px;
  }
  to {
    background-position: center 280px;
  }
}

@keyframes clouds {
  from {
    border-radius: 0 0 90px 33% / 0 0 45px 50px;
  }
  to {
    border-radius: 0 0 40px 50% / 0 0 55px 80px;
  }
}

@keyframes wind {
  from {
    height: 150px;
  }
  to {
    height: 100px;
  }
}

@keyframes falling {
  from {
    transform: translate(0, -50px) rotate(0deg) scale(0.9, 0.9);
  }
  to {
    transform: translate(30px, 600px) rotate(360deg) scale(1.1, 1.1);
  }
}

/* By default, the animations are paused. */
i,
div[class] {
  animation-play-state: paused;
}
/* When the div is hovered, the animation plays. Also,
when the input is checked, the animation coming after the checked checkbox plays */
div:hover *,
input:checked ~ div * {
  animation-play-state: running;
}

/* Change the content of the label that comes right after the input. Included aria-label on the label to improve accessibility. */
input + label::before {
  content: "Play ";
}
input:checked + label::before {
  content: "Pause ";
}
```

{{EmbedLiveSample("animation", "", "610px")}}

Esta animación de muestra usa {{cssxref("animation-iteration-count")}} para hacer que los copos caigan repetidamente, {{cssxref("animation-direction")}} para hacer que la nube se mueva de un lado a otro, {{cssxref( "animation-fill-mode")}} para aumentar el nivel de nieve en respuesta al movimiento de la nube y {{cssxref("animation-play-state")}} para pausar la animación.

Para ver el código de esta animación, [vea la fuente en GitHub](https://github.com/mdn/css-examples/blob/main/modules/animation.html).

## Referencia

### Propiedades

- {{cssxref("animation")}} abreviatura
- {{cssxref("animation-composition")}}
- {{cssxref("animation-delay")}}
- {{cssxref("animation-direction")}}
- {{cssxref("animation-duration")}}
- {{cssxref("animation-fill-mode")}}
- {{cssxref("animation-iteration-count")}}
- {{cssxref("animation-name")}}
- {{cssxref("animation-play-state")}}
- {{cssxref("animation-timing-function")}}
- {{cssxref("animation-timeline")}}

### Reglas arroba

- {{cssxref("@keyframes")}}

### Eventos

Todas las animaciones, incluso aquellas con 0 segundos de duración, lanzan eventos de animación.

- {{domxref("Element/animationstart_event", "animationstart")}}
- {{domxref("Element/animationend_event", "animationend")}}
- {{domxref("Element/animationcancel_event", "animationcancel")}}
- {{domxref("Element/animationiteration_event", "animationiteration")}}

### Interfaces

- [API de animaciones web](/es/docs/Web/API/Web_Animations_API)
- {{domxref("AnimationEvent")}}
- {{domxref("CSSKeyframeRule")}}
- {{domxref("CSSKeyframesRule")}}

## Guías

- [Usando animaciones CSS](/es/docs/Web/CSS/CSS_animations/Using_CSS_animations)
  - : Tutorial paso a paso sobre cómo crear animaciones usando CSS. Este artículo describe las propiedades CSS y las reglas arroba relacionadas con la animación y cómo interactúan entre sí.
- [Consejos y trucos de animación CSS](/es/docs/Web/API/Web_Animations_API/Tips)
  - : Consejos y trucos para ayudarlo a aprovechar al máximo las animaciones CSS.

## Conceptos relacionados

- Propiedad CSS {{cssxref("will-change")}}
- Tipo de dato [`<easing-function>`](/es/docs/Web/CSS/easing-function)
- Consulta de medios [`prefers-reduced-motion`](/es/docs/Web/CSS/@media/prefers-reduced-motion)
- Término del glosario {{glossary("Bezier curve")}}

## Especificaciones

{{Specifications}}

## Véase también

- [Animaciones CSS basadas en desplazamiento](/es/docs/Web/CSS/CSS_scroll-driven_animations)
- Propiedades en el módulo CSS [transitions](/es/docs/Web/CSS/CSS_transitions) para activar animaciones en función de las acciones del usuario
- El elemento HTML {{htmlelement("canvas")}} junto con la [API de canvas](/es/docs/Web/API/Canvas_API) y la [API de WebGL](/es/docs/Web/API/WebGL_API) para dibujar gráficos y animaciones
- La interfaz {{domxref("SVGAnimationElement")}} para todas las interfaces de elementos relacionados con la animación, incluidas {{domxref("SVGAnimateElement")}}, {{domxref("SVGAnimateElement")}}, {{domxref("SVGAnimateColorElement")}}, {{domxref("SVGAnimateMotionElement")}} y {{domxref("SVGAnimateTransformElement")}}
