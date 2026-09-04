# Observaciones visuales iniciales

- `Chicos2222.png`: fotografía horizontal a color con dos niñas sonrientes, fondo exterior claro; útil como imagen hero o sección de impacto.
- `Edu Nexus Spain-30cm x 30cm Circular.png`: logo circular nuevo de Edu Nexus Spain, fondo azul marino, borde turquesa y palabra EDU NEXUS; PNG RGBA con transparencia exterior.
- El proyecto es un sitio estático en un único `index.html`, con CSS y JavaScript embebidos y recursos locales en `img/`.
- El diseño actual usa fondo oscuro, canvas decorativo, navegación sticky, secciones sobre la organización, proyectos, equipo/carrusel y contacto.


- `chicos1r.png`: recorte transparente de tres niños juntos, composición horizontal; funciona como nodo de grupo o pieza de impacto.
- `chicos2r.png`: recorte transparente de las dos niñas de `Chicos2222.png`, con el accesorio amarillo y parte del cuerpo visible; ideal para un punto circular de conexión.


- `Europa.png`: banda horizontal blanca con texto azul en inglés sobre financiación Erasmus+ y bandera europea; se usará como marca rectangular de financiación en el pie.
- `Erasmus+.png`: versión cuadrada con bandera europea y texto Erasmus+; útil para una tarjeta de identidad o un elemento destacado del carrusel.


- `imagen1.jpg`: retrato horizontal a color de dos niñas; transmite cercanía y puede funcionar como tarjeta humana de apertura.
- `imagen3.jpg`: fotografía panorámica de un grupo internacional en un proyecto de agricultura sostenible Erasmus+; es adecuada para una tarjeta de proyecto principal.


- `erasmus.png`: distintivo circular azul con estrellas amarillas y texto Erasmus+; es la mejor opción para el emblema redondo europeo del encabezado.
- `chicos3r.png`: recorte transparente de dos niñas, diferente de `chicos2r.png`, con encuadre vertical dentro de una composición horizontal; se integrará como nodo de conexión adicional.


## Verificación visual inicial

La página carga correctamente desde `file://`, los recursos locales se muestran y el hero presenta la cabecera con el logo circular nuevo, el emblema Erasmus+ circular, el mapa de conexiones y los retratos transparentes. La versión English cambia navegación, hero, estadísticas, capacidades y tarjetas del carrusel correctamente; los textos de los placeholders mantienen ambas variantes para facilitar el uso bilingüe.

Se detectó una corrección pendiente en el texto español de la tercera estadística: debe decir `aprender, colaborar y transformar` y no mezclar la palabra inglesa `collaborate`.


La segunda revisión visual confirma que la sección de capacidades mantiene una composición equilibrada en dos columnas y que el carrusel comienza con una jerarquía clara de fotografías y textos. La interfaz mantiene el modo English activo tras refrescar y no muestra referencias a recursos externos de imágenes.


La revisión inferior confirma que las tarjetas del carrusel muestran las imágenes locales y avanzan visualmente de izquierda a derecha; la sección de red conserva un panel de países legible y el formulario de contacto queda alineado con la información institucional. El pie todavía debe verificarse al final de la página para confirmar el logo rectangular de financiación.


## Validación técnica

La comprobación final encontró 19 imágenes cargadas correctamente y ningún recurso roto. Hay 112 elementos con traducciones ES/EN y ninguno carece de ambas variantes. El carrusel contiene 10 tarjetas —cinco proyectos duplicados para crear un bucle continuo— y la zona de destellos y los dos botones de idioma están presentes.


## Refinamiento visual

Los retratos del mapa ahora se ven semitransparentes, en tonos azul/cian coordinados con el fondo, con un velo de color suave y un brillo interior. Las etiquetas de España, Europa, América Latina y Alianzas, las líneas, los anillos y los acentos de estrellas permanecen visibles y sin cambios de estructura.

La revisión visual confirma que el resultado mantiene la composición solicitada. Una comprobación automática de estilo falló porque el navegador no devolvió el elemento esperado en ese instante, pero la página se recargó correctamente y el render visual muestra el ajuste aplicado.


## Accesos flotantes

Se añadieron `img/wechat-icon.svg` y `img/whatsapp-icon.svg` como recursos locales ligeros. La comprobación técnica confirma dos enlaces visibles, ambos iconos cargados correctamente y el dock fijado con `position: fixed`, `left: 20px` y `bottom: 22px`; en pantallas pequeñas se reduce a `left: 12px`, `bottom: 12px` y botones de 42px.


## Ajuste final del hero

El título del hero quedó con degradados internos suaves: rojo cálido en “The future”, amarillo crema en “is learned” y rojo cálido en “together.”. Se corrigió además el recorte CSS para que el color quede contenido en las letras y no aparezcan rectángulos alrededor del texto. La revisión visual confirma que el mapa, retratos azules, países, estrellas y dock de contacto permanecen intactos.


## Nueva rama superior del mapa

Se añadió una rama vertical desde el hub hacia la parte superior central del mapa. El nuevo nodo utiliza `img/imagen6.jpg`, con tratamiento circular azul/semitransparente, y las etiquetas bilingües “Proyectos Erasmus+ / Erasmus+ projects” y “Experiencias compartidas / Shared experiences”. La comprobación visual y técnica confirma que la imagen carga, el nodo existe y el SVG contiene cuatro trayectorias y seis puntos de conexión. Las ramas anteriores permanecen en su sitio.


## Corrección de continuidad

La primera versión terminaba la rama en `y=78`, mientras que el nuevo nodo comenzaba en `y≈5.7` y tenía su centro en `y≈57.7`; por eso la unión podía percibirse descolgada. La rama se reubicó para llegar al centro del nodo y se verificó visualmente. Como mejora de continuidad, se alineará el punto terminal con el borde inferior real del avatar (`y≈109.7`) y se reforzará la unión luminosa allí, manteniendo la misma salida desde el hub.


## Unión de la nueva rama

La rama superior ahora utiliza el mismo estilo de trazo discontinuo que las demás y parte del mismo punto central del hub (`M310 285`). Su extremo llega a `y=110`, coincidiendo con el borde inferior real del avatar superior (`avatarBottom=110`), con un punto de unión luminoso en la foto. La validación confirmó cuatro trayectorias en el SVG y que `img/imagen6.jpg` carga correctamente.


## Línea de puntos superior

Se añadió un tramo específico `.top-dotted-connector` con `stroke-dasharray: 2px, 8px` desde `M310 197` hasta `L310 110`, entre el borde superior del hub y el borde inferior del nodo `img/imagen6.jpg`. La comprobación confirma que existe, usa el patrón de puntos y que el SVG conserva las cinco trayectorias del mapa.


## Conector visible sobre capas

Para evitar que el trazado quedara oculto, se añadió un conector HTML independiente con `z-index: 2`, borde izquierdo punteado y brillo, mientras el hub queda en `z-index: 1` y el nodo en `z-index: 3`. La verificación confirmó: `border-left-style: dotted`, línea visible, `lineTop=328`, `lineBottom=415`, coincidiendo con `avatarBottom=328` y `hubTop=415`.
