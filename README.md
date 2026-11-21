# Mi Agenda Pro v2.6

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

## Equipo: cada trabajador agenda desde su propio celular (sin cruces)
Requisito: **los trabajadores deben agendar desde sus propios dispositivos, y sus turnos no pueden cruzarse con los de ningún otro trabajador.**

**Cómo funciona**
- Todos los turnos del equipo viven en una sola agenda. Al guardar un turno se revisa contra los de TODOS los trabajadores (con 5 min de margen). Si hay cruce, la app lo rechaza y sugiere el primer horario libre.
- Si dos personas toman el mismo horario en el mismo instante, gana la primera en llegar al servidor; la otra recibe el aviso y elige otra hora.
- Cada trabajador ve la agenda completa, pero los turnos de los demás aparecen como «Ocupado» (sin nombre de clienta, teléfono ni precio). Solo edita, cancela y cobra sus propios turnos. El administrador puede gestionar todos.
- Los trabajadores no editan la lista de servicios: la recibe del administrador.
- Para **agendar** se necesita internet (así se garantiza que no haya cruces). Sin internet se puede consultar la última agenda guardada.
- Sin conectar la nube, la app sigue funcionando como antes en un solo dispositivo; incluso ahí, los usuarios de un mismo celular ya no pueden cruzarse entre sí.

**Configuración (una sola vez, la hace el administrador; es gratis)**
1. Entra a console.firebase.google.com con una cuenta de Google y crea un proyecto (puedes desactivar Google Analytics).
2. Menú Build > **Realtime Database** > Crear base de datos (cualquier ubicación) > iniciar en **modo bloqueado**.
3. Pestaña **Reglas**: borra todo, pega lo siguiente y pulsa Publicar:
```
{
  "rules": {
    ".read": false,
    ".write": false,
    "teams": {
      "$code": { ".read": true, ".write": true }
    }
  }
}
```
4. Copia la dirección de la base de datos (algo como `https://tu-proyecto-default-rtdb.firebaseio.com`).
5. En la app: Ajustes > **Equipo en la nube** > pega la dirección > «Conectar equipo». Los turnos futuros que ya tenías se suben automáticamente.
6. Pulsa «Enviar invitación» y mándala por WhatsApp a cada trabajador.

**Para cada trabajador**
- Abre el enlace de invitación en su celular, escribe su nombre y WhatsApp y toca «Unirme al equipo».
- iPhone: la app instalada en la pantalla de inicio no comparte datos con Safari. Primero instala la app desde el enlace normal de GitHub Pages, ábrela y en la pantalla inicial pega el enlace de invitación en «¿Te invitaron a un equipo?».
- Android: basta con abrir el enlace de invitación y luego instalar.

**Seguridad:** el enlace de invitación contiene un código secreto del equipo; quien lo tenga puede leer y escribir los turnos. Compártelo solo con tu equipo. Si se filtra, desconecta y vuelve a conectar para generar un código nuevo (no se pueden reutilizar los turnos del código anterior).

## Avisos de reservas por enlace
- Cada usuario tiene su enlace (pestaña Reservas) y un tema privado de avisos (Ajustes > Avisos de reservas).
- Con la app abierta, el aviso llega solo. Con la app cerrada, instala la app gratuita **ntfy** y suscríbete a tu tema.
- Los avisos viajan por ntfy.sh. Sin la nube de equipo, los turnos se guardan solo en el dispositivo.
- Para recibir avisos sin ntfy se necesita un servidor propio (Firebase/Supabase): fase aparte.

## Servicios y la opción «Otros»
- Al crear o editar un turno, el desplegable de servicios termina en «✏️ Otros». Al elegirla aparecen campos para escribir el nombre del servicio, su duración y su precio en el momento.
- Marcando «Guardar este servicio en mi lista» queda disponible en el desplegable para próximas veces (también se administra en Ajustes > Servicios).
- La agenda sigue evitando cruces entre turnos usando la duración escrita.

## Notas
- Sin la nube de equipo, los datos viven en el dispositivo. Para pasarlos a otro: Ajustes > Exportar / Importar.
- Al subir cambios, cambia `CACHE` en sw.js (ej. mi-agenda-pro-v2.7) para que los dispositivos se actualicen.
