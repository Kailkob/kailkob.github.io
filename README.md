# Web de Kailkob

Web oficial del artista musical **Kailkob**: <https://kailkob.github.io>

Este documento resume qué se ha hecho, cómo está organizado y cómo hacer cambios. Está pensado para que cualquier persona o asistente pueda continuar el proyecto desde cero.

---

## Cómo funciona

- **Repositorio:** `github.com/Kailkob/kailkob.github.io`, rama `main`.
- **Publicación:** GitHub Pages publica automáticamente cada cambio que llega a `main` (tarda 1–2 minutos).
- **Un solo archivo:** toda la web está en `index.html` (HTML, CSS y JavaScript juntos). No hay herramientas de compilación ni dependencias: **se edita `index.html` directamente**.
- Fuentes de Google Fonts: *Shadows Into Light Two* (mano/tiza), *Pirata One* (gótica legible) e *IM Fell English* (textos largos).

### Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | La web completa |
| `img/kailkob-recorte.png` | Retrato de portada, PNG con fondo transparente (provisional) |
| `img/retrato.jpg` | Retrato de "sobre mí" (provisional) |
| `img/og.jpg` | Imagen al compartir en redes (1200×630) |
| `img/favicon.svg` | Icono de la pestaña |
| `img/rata-cascos.jpg` | Ilustración de la página 404 |
| `404.html` | Página de "no encontrado" con el mismo estilo |
| `prueba/index.html` | Redirige a la portada (era la versión de prueba del diseño actual) |
| `robots.txt`, `sitemap.xml` | Para buscadores |

---

## Estructura de la página (en orden)

1. **Portada.** Retrato recortado con efecto tinta, centrado sobre una tira lila en movimiento que dice "kailkob". Una rata camina por el borde de la tira y salta por encima de la cabeza: lee la silueta real del PNG y nunca la toca.
2. **Canciones** (`#canciones`). Lista de canciones a la izquierda. En el centro, la portada dibujada a línea con un vinilo girando y una ventanita "nombre.wav". A la derecha, la ficha: historia, "escuchar en Apple Music", letra y créditos. Cada canción tiene enlace directo: `#cancion-1408`, `#cancion-blv`, `#cancion-ddp`, `#cancion-rio`.
3. **Videoclips** (`#videoclips`). Carrusel 3D que se pasa con flechas, puntos, deslizando o con el teclado. Solo *1408* tiene vídeo; el resto muestra "videoclip pronto". El vídeo de YouTube no se carga hasta pulsar ▶.
4. **Redes** (`#redes`). @kailkob con 5 reels de Instagram dentro de móviles dibujados (se ve solo la franja del vídeo) y botones a Instagram, TikTok y YouTube.
5. **Pensamientos** (`#pensamientos`). Frase grande y la libreta **Grimorio**: portada, índice clicable, **letras**, **pensamientos** y **borradores**. Las hojas se pasan con un giro en 3D y hay separadores de colores por categoría.
6. **Sobre mí** (`#sobre-mi`). Retrato en polaroid con efecto tinta, asterisco, ventanita "kailkob.exe" y filas "lo que suena / música", "lo que escribo / palabras", "lo que persigo / obsesiones".
7. **Contacto.** Tarjeta lima con un sobre dibujado y enlaces a Spotify, Apple Music, YouTube, Instagram y TikTok.
8. **Pie.** Tira lila rasgada con tres ratas desfilando.

Bichos animados repartidos por la página: gato asomado en la portada de la canción, rata sentada en videoclips, gato andando en pensamientos, gato sentado en sobre mí y gato asomado en contacto.

---

## Decisiones de diseño

- **Estética:** cuaderno nocturno, tiza, collage y fanzine, con dibujos a pluma.
- **Colores:**

  | Nombre | Valor |
  |---|---|
  | negro | `#0a0a0a` |
  | tiza | `#efe8d8` |
  | lila | `#b99ae6` |
  | lima | `#c8f03c` |
  | papel | `#e9dcc0` |
  | morado oscuro | `#3b2a52` |

- **Títulos de sección** con letras recortadas en papel. Regla: **dos letras seguidas nunca comparten color**, y crema y blanco cuentan como el mismo color. Los títulos caben siempre en una línea.
- **Dibujos e iconos** a línea con trazo tembloroso (filtro SVG `#ink`), estilo pluma con puntitos. Los dibujos son símbolos SVG dentro de `index.html` (`#d-rat`, `#d-cat`, `#d-moon`, `#d-river`, `#d-envelope`, `#d-star`, `#d-vinyl`). Los bichos animados se generan en el bloque JS `CRITTERS`.
- **Retratos** en blanco y negro de alto contraste (clase `inked`).
- **Separadores** entre secciones: ramas lila (`vine-rule`).
- **Animaciones:** solo cuando están a la vista; se paran con "reducir movimiento"; los bichos saltan y dicen "ñiiic" o "miau" al tocarlos.
- **Accesibilidad:**
  - enlace "saltar al contenido" y títulos h1–h3 en orden
  - pestañas y carruseles usables con teclado
  - `lang="ca"` en las letras en catalán
  - aviso de "se abre en otra pestaña" en los enlaces externos
- **Buscadores:** etiqueta canonical, Open Graph y JSON-LD `MusicGroup` con enlaces a Spotify, Apple Music, YouTube, Instagram y TikTok y los dos singles.

---

## Dónde se cambia el contenido

En `index.html`, todo lo editable está marcado con comentarios **`EDITAR`**.

| Qué | Dónde (buscar en `index.html`) |
|---|---|
| Canciones: título, fecha, enlace, idioma, **letra**, historia, créditos | `const SONGS = [` |
| Videoclips (id de YouTube en `video`) | `const CLIPS = [` |
| Pensamientos y borradores del Grimorio (`cat: 'pensamientos'` o `'borradores'`) | `const TEXTOS = [` |
| Reels de Instagram (código de `instagram.com/reel/CÓDIGO`) | `<ul class="phones"` |
| Biografía | comentario `EDITAR: biografía corta` |
| Email de contacto | comentario `EDITAR: cuando haya email` |
| Foto principal | sustituir `img/kailkob-recorte.png` y subir el número de `?v=` en su `src` |

Notas:
- La **letra** de una canción aparece a la vez en su ficha y en el Grimorio, y el índice se rehace solo. En los saltos de línea de las letras se usa `\n`.
- 1408 tiene `lang: 'ca'` (catalán).
- Para una canción nueva, añade un objeto a `SONGS`. Si quieres también su portada dibujada, añade una escena en la función `art()`.
- Para un videoclip nuevo, añádelo a `CLIPS` con el id del vídeo de YouTube (lo que va después de `youtu.be/`).

---

## Datos actuales

- **BLV W/ME:** single, 18 sep 2025, ℗ 2025 Kailkob, alternativa. [Apple Music](https://music.apple.com/us/album/blv-w-me-single/1841047244)
- **1408:** single, 28 feb 2025, 3:38, urbano latino, ℗ 2025 Umamirecords, en catalán. [Apple Music](https://music.apple.com/us/album/1408-single/1798072933) · videoclip [YouTube HCXq8Izwtno](https://youtu.be/HCXq8Izwtno)
- **Ding Dong Piro** y **Que nos sofoque el río:** solo título (y una historia para Ding Dong Piro).
- **Perfiles:** [Spotify](https://open.spotify.com/artist/3jYSHWbpXuVlIcGAhi24lI) · [Apple Music](https://music.apple.com/us/artist/kailkob/1797300511) · [YouTube](https://www.youtube.com/@kailkob) · [Instagram](https://www.instagram.com/kailkob/) · [TikTok](https://www.tiktok.com/@kailkob)

---

## Pendiente

- [ ] Biografía corta
- [ ] Email de contacto
- [ ] Letras de las canciones (la de 1408 en catalán) e historias
- [ ] Más pensamientos y borradores para el Grimorio
- [ ] Foto definitiva para la portada (PNG transparente; si no lo es, se puede recortar con la detección de sujeto de macOS) y retrato de "sobre mí"
- [ ] Portadas reales de las canciones (ahora son dibujos a línea provisionales)
- [ ] Videoclips nuevos cuando salgan
- [ ] Revisar de vez en cuando los reels de la sección de redes

---

## Cómo publicar cambios

**Desde un ordenador con el repositorio clonado:**

```bash
git pull
# editar index.html
git add -A
git commit -m "Describe el cambio"
git push origin main
```

**Sin terminal:** en github.com abre `index.html` → icono del lápiz → edita → *Commit changes*.

**Comprobar que ya está publicado** (1–2 minutos después):

```bash
curl -s "https://kailkob.github.io/?v=$RANDOM" | grep "un texto nuevo"
```

### Problemas conocidos

- **Si un despliegue de GitHub Pages falla** (pasa cuando dos publicaciones van muy seguidas), relánzalo:

  ```bash
  git commit --allow-empty -m "Relanza la publicación" && git push origin main
  ```

- **Si una imagen nueva no se ve,** es la caché: recarga con Cmd+Shift+R, o cambia el número de `?v=` en el `src` de la imagen.
- **La API pública de GitHub** solo permite 60 consultas por hora sin sesión. Para comprobar publicaciones, mira la web directamente.
- **Para probar en local:**

  ```bash
  python3 -m http.server 8765
  ```

  Luego abre <http://localhost:8765>. Los vídeos de YouTube y los reels de Instagram pueden no verse desde `localhost` en algunos navegadores; en la web publicada sí se ven.

---

## Historial de decisiones (resumen)

1. Primera versión sobria y oscura; después, cuaderno de paneles con marcos de ramas.
2. Rediseño mezclando referencias (Spray art school, portfolio con letras de spray, collage fanzine, web de Travis Scott), conservando la estética de tiza, lila y lima.
3. Se descartan el título gigante de la portada, el círculo verde y la tira de ojos. La portada queda en foto recortada + tira "kailkob".
4. Canciones y videoclips suben arriba. Videoclips pasa a ser un carrusel. Desaparecen "Pequeño cine" y "¡hola!".
5. Iconos e ilustraciones a línea, estilo pluma, con ratas y gatos animados.
6. Nueva sección de redes con reels en móviles. "Textos" pasa a llamarse "pensamientos" y la libreta, "Grimorio".
