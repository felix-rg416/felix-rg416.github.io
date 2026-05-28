# apuntes

## 26/05/2026

Estuve viendo el portafolio de Vania, Mateo y Janis.

Vania tiene 4 carriles en vertical que se mueven como un carrusel hacia arriba y hacia abajo.
Me interesa demasiado hacer eso, pero me gustaría que se movieran hacia los lados, como un carrusel horizontal.

Según entiendo, la sección que debería manejar eso es la siguiente:

```css
.projects-grid {
  height: 100vh;
  padding: 72px var(--pad) 14px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 14px;
  overflow: hidden;
  background: var(--bg);
}
.column    { overflow: hidden; position: relative; }
.col-inner { display: flex; flex-direction: column; gap: 14px; will-change: transform; }
```

Según Cloude AI usa un .js para manejar el movimiento de los carriles, pero no logro encontrarlo.

Investigué un poco más y, como yo quiero hacerlo de forma horizontal (de lado a lado), es más fácil que sea con el .css.

Cloude me mandó este:

```css
.row-inner {
  display: flex;
  gap: 14px;
  width: max-content;
  animation: scroll-left 20s linear infinite;
}

.row-inner.reverse {
  animation: scroll-right 20s linear infinite;
}

@keyframes scroll-left {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}

@keyframes scroll-right {
  from { transform: translateX(-50%); }
  to   { transform: translateX(0); }
}
```

En el .html debo duplicar las imágenes para que el carrusel se vea infinito y que no se note el salto cuando termina la animación.

```html
<div class="carousel-row">
  <div class="row-inner">
    <img src="img1.jpg" />
    <img src="img2.jpg" />
    <!-- copia exacta ↓ -->
    <img src="img1.jpg" />
    <img src="img2.jpg" />
  </div>
</div>
```

Agregué todo esto para que funcione el carrusel horizontal:

```css
  .row-inner {
    overflow: hidden;
    display: block;
    gap: 8px;
    width: max-content;
    animation: scroll-left 30s linear infinite;
    flex-shrink: 0;
  }

  .row-inner img {
  height: 200px;     /* ajusta a tu gusto */
  width: 300px;
  object-fit: cover;
  flex-shrink: 0;
  border-radius: 8px;
}

  .row-inner.reverse {
    animation: scroll-right 30s linear infinite;
  }

/* hacia la izquierda */
  @keyframes scroll-left {
    /* desde */
    from {
      transform: translateX(-50%);
    }
    /* hasta */
    to {
      transform: translateX(0%);
    }
  }

/* hacia la derecha */
  @keyframes scroll-right {
    /* desde */
    from {
      transform: translateX(0%);
    }
    /* hasta */
    to {
      transform: translateX(-50%);
    }
  }
```
