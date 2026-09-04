# Diagnóstico del contacto

## Hallazgo inicial

La página pública `https://www.edunexusspain.eu` devuelve contenido HTML a la extracción, pero al abrirla interactivamente el navegador muestra `NET::ERR_CERT_COMMON_NAME_INVALID` y una advertencia de privacidad. Esto indica un problema de certificado/hostname en producción que debe corregirse en la configuración DNS/SSL del dominio, independientemente del HTML del formulario.

## Estado del código local

El formulario usa `action="https://formsubmit.co/el/bozixa"` con método POST. La documentación oficial de FormSubmit confirma que los endpoints `/el/{custom-link}` son válidos para enlaces personalizados, pero requieren activación del enlace/email. El servicio también indica que las páginas HTML abiertas como archivos locales no funcionan para enviar formularios y que en producción se debe servir la página por HTTPS con una URL válida.


## Corrección implementada en la copia local

El formulario ahora usa `https://formsubmit.co/ajax/info@edunexusspain.eu`, el endpoint AJAX documentado para formularios cross-origin. Se añadió `_url` con el dominio canónico, `_replyto` con el email del visitante, protección honeypot, asunto bilingüe, mensajes de éxito/error y un enlace de respaldo por email. La página local carga sin errores de consola. La comprobación OPTIONS del endpoint AJAX devuelve `200` y permite POST con CORS.

## Nota de producción

El dominio `https://edunexusspain.eu/` responde correctamente con `200`, pero `https://www.edunexusspain.eu` redirige al dominio sin www y presenta `NET::ERR_CERT_COMMON_NAME_INVALID` en el navegador. Para evitar que los visitantes queden bloqueados, hay que corregir el certificado/hostname de `www` en la configuración de GitHub Pages/DNS y activar HTTPS una vez que el certificado incluya el dominio utilizado.


## Prueba del flujo local

La página local carga correctamente y el formulario intercepta el submit. Una primera simulación de respuesta exitosa terminó en el estado de error porque el mock de prueba intentó reconstruir un objeto `FormData` a partir de otro `FormData`; no se realizó ninguna solicitud externa ni se enviaron datos reales. Se repetirá la validación usando directamente los campos del objeto `FormData`.


## Validación final del código

La simulación de éxito confirmó que el navegador hace un POST a `https://formsubmit.co/ajax/info@edunexusspain.eu`, incluye `_replyto` con el email del visitante y `_url` con `https://edunexusspain.eu/`, y muestra el estado de éxito en inglés cuando el idioma activo es EN. La simulación de error confirmó que se muestra el estado de error bilingüe y aparece el enlace alternativo `mailto:info@edunexusspain.eu`. No se enviaron mensajes reales durante las pruebas.
