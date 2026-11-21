# Mi Agenda Pro v2.4

App web instalable (PWA) para agendar turnos. Funciona con y sin internet.

## Subir a GitHub y publicar
1. Crea un repositorio nuevo en github.com (por ejemplo `mi-agenda`).
2. Sube TODOS los archivos de este zip a la raíz del repositorio (Add file > Upload files). Incluye `.nojekyll`.
3. Settings > Pages > Source: "Deploy from a branch", rama `main`, carpeta `/ (root)`.
4. En 1-2 minutos tendrás la app en `https://TU-USUARIO.github.io/mi-agenda/`.
5. Abre el enlace en el celular: aparece la opción de instalar (en iPhone: Compartir > Agregar a pantalla de inicio).

## Instalación en todos los dispositivos
- La app NO tiene botón para compartir ni instalar en otros dispositivos: tú compartes el enlace de GitHub Pages (o el del repositorio) directamente.
- Al abrir ese enlace aparece al instante la tarjeta "Instala Mi Agenda" con un botón (también en el encabezado y en Ajustes).
- Android, tablets y Chrome/Edge en computador: un toque abre el instalador del sistema. iPhone/iPad/Mac (Safari) y Firefox: el botón muestra los pasos exactos.
- Los navegadores no permiten instalar sin un toque del usuario; por eso es un botón visible y de un solo paso.
- El enlace de reservas de las clientas solo abre la página de reservas: no ofrece instalar ni muestra tu agenda.

## Avisos de reservas por enlace
- Cada usuario tiene su enlace (pestaña Reservas) y un tema privado de avisos (Ajustes > Avisos de reservas).
- Con la app abierta, el aviso llega solo. Con la app cerrada, instala la app gratuita **ntfy** y suscríbete a tu tema.
- Los avisos viajan por ntfy.sh. Los turnos se guardan solo en el dispositivo.
- Para recibir avisos sin ntfy se necesita un servidor propio (Firebase/Supabase): fase aparte.

## Notas
- Los datos viven en el dispositivo. Para pasarlos a otro: Ajustes > Exportar / Importar.
- Al subir cambios, cambia `CACHE` en sw.js (ej. mi-agenda-pro-v2.5) para que los dispositivos se actualicen.
