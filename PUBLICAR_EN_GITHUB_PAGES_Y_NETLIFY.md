# LOGISTEC V2.4 — versión web de archivo único

Esta versión elimina la estructura modular de JavaScript y CSS del despliegue web.
La interfaz, estilos, configuración pública de Supabase y lógica de la aplicación quedan integrados en `index.html`.

## Archivos que debes subir

Sube **todos los archivos de este paquete** a la raíz del repositorio GitHub. No abras ni vuelvas a crear carpetas. El `index.html` reemplazará la página inicial publicada, pero subir estos archivos no borra las otras carpetas que ya existen en tu repositorio.

- `index.html`: aplicación completa (CSS y scripts integrados).
- `manifest.webmanifest`, `service-worker.js`: instalación PWA y caché offline.
- `logistec-*.png`, `logistec-mark.svg`: iconos.
- `netlify.toml`: configuración para Netlify.

No se incluyen carpetas `js/` ni `css/`: esos códigos ya están integrados dentro de `index.html`. Si vas a usar el mismo repositorio que también compila el APK, **conserva las carpetas `mobile/`, `.github/` y `supabase/` que ya tienes**; este paquete web no las reemplaza ni las necesita para mostrar el sitio. El backend y autenticación continúan en el proyecto Supabase ya configurado. Las Edge Functions de Supabase, si se usan, siguen siendo servicios separados y no se despliegan en GitHub Pages.

## Publicar en GitHub Pages

1. Abre el repositorio `LOGISTEC-Mobile`.
2. Entra en **Settings → Pages**.
3. En **Build and deployment**, selecciona **Deploy from a branch**.
4. Selecciona la rama `main` y la carpeta `/(root)`.
5. Pulsa **Save**.
6. Espera a que GitHub publique el sitio y abre la URL que aparece en la misma pantalla.

No necesitas crear un workflow de Actions para este método.

## Publicar en Netlify

Puedes conectar el repositorio desde Netlify o arrastrar el contenido extraído a Netlify Drop. Si conectas GitHub: usa `.` como directorio de publicación y deja vacío el comando de build.

## Pruebas recomendadas

1. Abre la URL HTTPS del sitio.
2. Comprueba que carga el panel y los recursos externos (Leaflet y Supabase CDN).
3. Inicia sesión con un usuario de prueba de Supabase.
4. Comprueba el cargo del usuario y la empresa correspondiente.
5. Cierra sesión y confirma que vuelve al acceso sin iniciar automáticamente otra cuenta.
6. Comprueba el flujo de invitaciones del dueño y los permisos de otros cargos.

## Importante sobre Supabase

`index.html` contiene una clave pública (publishable/anon) del cliente. No agregues jamás una clave `service_role` al frontend. Mantén Row Level Security (RLS) activa y verifica las políticas en Supabase.

La publicación estática no migra ni modifica tu base de datos. No ejecutes nuevamente SQL por subir este sitio.

## Alcance

Esta entrega es una versión web para evaluación en navegador, no una compilación APK. La generación APK seguirá siendo un flujo separado, pues necesita Capacitor/Android SDK y el directorio móvil.
