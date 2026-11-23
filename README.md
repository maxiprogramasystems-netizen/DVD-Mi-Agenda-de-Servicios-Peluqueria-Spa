# Mi Agenda Pro v3.2

App web instalable (PWA) para agendar turnos. Funciona con y sin internet.

## Novedades v3.2
- **Ventana de PIN propia con saludo:** al entrar a una cuenta con PIN ya no sale el cuadro del navegador (que mostraba la dirección del sitio y dejaba ver el PIN). Ahora aparece «¡Bienvenido/a, nombre!» con el logo del negocio, el PIN se escribe con puntos, el teclado es numérico y hay mensajes claros: «Escribe tu PIN.» y «PIN incorrecto. Inténtalo de nuevo.». También funciona la tecla Entrar del teclado.
- **Borrar gasto con ventana propia:** «¿Borrar este gasto?» con «Cancelar» y «Sí, borrar», sin la dirección del sitio.
- La app ya no usa ningún cuadro nativo del navegador. La dirección todavía se ve en la barra superior si abres la app desde Chrome en lugar de la instalada, y en la vista previa del enlace en WhatsApp; para cambiarla hay que renombrar el repositorio o usar un dominio propio.
- Los PIN ya guardados siguen funcionando igual.

## Novedades v3.1
- **Botón Agenda con la fecha real:** el ícono del menú es un mini calendario que muestra el mes y el día de hoy (por ejemplo «nov 23»). Se actualiza solo a medianoche y cuando vuelves a abrir la app. Si estabas viendo «hoy», la agenda avanza al nuevo día; si estabas viendo otro día, no se mueve.
- **Tocar «Agenda» estando en Agenda te devuelve a hoy.** Cuando miras otro día aparece el botón dorado «Volver a hoy».
- **Selector de día:** al tocar la fecha de la Agenda se abre el calendario del teléfono para saltar a cualquier día. La fecha se escribe con la primera letra en mayúscula («Domingo, 22 de noviembre»).
- **Menú inferior en relieve:** botones con brillo, borde con grosor y efecto de hundirse al presionar. El botón activo se ve rosa brillante.
- **Clientes editable:** cada tarjeta tiene un botón con lápiz (✏️) para cambiar nombre, WhatsApp y una nota (alergias, gustos, recordatorios). El nombre y el teléfono se actualizan en todos los turnos de esa clienta que puedes editar; cada trabajador edita solo sus clientas y el administrador las del equipo. La nota queda en el dispositivo y se incluye en Ajustes > Exportar / Importar. El botón verde de WhatsApp se mantiene igual.
- **Saludo de bienvenida:** el encabezado dice «Buenos días / Buenas tardes / Buenas noches y bienvenido/a, nombre». La vista previa del enlace (por ejemplo en WhatsApp) también lleva un mensaje de bienvenida. La dirección web de la vista previa la define GitHub Pages.

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

## Finalizar turnos y panel de clientes
- **Botón «✔ Finalizar»** en cada turno de la Agenda: pregunta «¿fue atendida satisfactoriamente?» y, si el turno aún no está pagado, ofrece marcarlo también como cobrado. El turno queda con la etiqueta «Atendido ✓» y borde verde. Si te equivocas, «↩ Reabrir» lo devuelve a pendiente.
- **Panel de clientes** (arriba de la Agenda y en la pestaña Caja): total de clientes, atendidos y pendientes, con barra de avance. En la Agenda es del día elegido; en Caja es por día, semana o mes. Cada trabajador ve únicamente sus propios clientes; el administrador ve los del equipo.
- Los turnos cancelados («No asistirá») no cuentan como clientes.

## Ingresos, gastos y ganancia neta (pestaña 💰 Caja)
- **Ingresos totales:** suma de todos los turnos agendados del periodo. **Ingresos de atendidos:** solo los turnos finalizados. **Por atender:** la diferencia.
- **Ganancia neta = ingresos de atendidos − gastos del periodo.** Se muestra en verde si es positiva y en rojo si es negativa.
- **Gastos del negocio:** botón «+ Gasto» para registrar insumos, arriendo, transporte, servicios públicos, publicidad u otros, con descripción, valor y fecha. Se pueden borrar con ✕. Solo los ve el administrador; los trabajadores ven sus ingresos, pero no la ganancia neta.
- Los gastos se guardan en el dispositivo del administrador y se incluyen en Ajustes > Exportar / Importar. La colilla de cierre muestra clientes atendidos, gastos y ganancia neta.

## Cierre de caja (pestaña 💰 Caja)
- Muestra, por día, semana o mes, el **total ingresado** a la aplicación, cuánto está **cobrado** (turnos marcados como pagados) y cuánto está **por cobrar**.
- **Sumatoria por servicio:** cantidad de turnos, valor y porcentaje de cada servicio (manicure, pedicure, cejas, «Otros»...), con el total general.
- **Arqueo:** se escribe el efectivo contado en la caja y la app compara contra lo cobrado: «Caja cuadrada ✓», «Sobran $X» o «Faltan $X».
- Los turnos pendientes se pueden marcar como cobrados desde la misma pantalla para que el arqueo cuadre.
- **Colilla de cierre:** con «🔒 Cerrar caja e imprimir» se guarda el cierre (con su número consecutivo) y se abre la colilla lista para imprimir en tira de 80 mm: detalle de cada servicio realizado (hora, servicio, clienta, valor y si está pagado), resumen por servicio, **total del día**, cobrado, por cobrar, efectivo contado, diferencia y línea de firma. Se puede quitar el detalle con la casilla «Incluir el detalle de cada servicio». «Ver colilla» muestra una vista previa sin cerrar la caja.
- Se imprime desde el botón «🖨 Imprimir colilla» (impresoras térmicas o normales, Bluetooth o por el menú de impresión del navegador). También se envía resumida por WhatsApp.
- **Historial:** los cierres guardados se reimprimen en cualquier momento con «🖨 Reimprimir» (se guardan en este dispositivo).
- El administrador ve además el total por trabajador. Cada trabajador ve únicamente sus propios ingresos.
- Para que el arqueo sea exacto, marca como pagado cada turno cuando se cobre (botón «Comprobante» > «Guardar como pagado», o «Cobrado» en la pestaña Caja).

## Avisos de reservas por enlace
- Cada usuario tiene su enlace (pestaña Reservas) y un tema privado de avisos (Ajustes > Avisos de reservas).
- Con la app abierta, el aviso llega solo. Con la app cerrada, instala la app gratuita **ntfy** y suscríbete a tu tema.
- Los avisos viajan por ntfy.sh. Sin la nube de equipo, los turnos se guardan solo en el dispositivo.
- Para recibir avisos sin ntfy se necesita un servidor propio (Firebase/Supabase): fase aparte.

## Servicios y la opción «Otros»
- Al crear o editar un turno, el desplegable de servicios termina en «✏️ Otros». Al elegirla aparecen campos para escribir el nombre del servicio, su duración y su precio en el momento.
- Marcando «Guardar este servicio en mi lista» queda disponible en el desplegable para próximas veces (también se administra en Ajustes > Servicios).
- La agenda sigue evitando cruces entre turnos usando la duración escrita.
- **Costo editable:** el formulario de turno tiene la casilla «💰 Costo del servicio». Al elegir un servicio aparece su costo habitual y el trabajador puede cambiarlo solo para ese turno (cejas, manicure, pedicure, uñas, «Otros»...). Marcando «Usar este costo como el habitual» queda como nuevo costo del servicio. El costo se refleja en la agenda, el total del día y el comprobante.

## Notas
- Sin la nube de equipo, los datos viven en el dispositivo. Para pasarlos a otro: Ajustes > Exportar / Importar.
- Al subir cambios, cambia `CACHE` en sw.js (ej. mi-agenda-pro-v3.3) para que los dispositivos se actualicen.
