---
lab:
  title: 'Ejercicio 1: Implementación de la administración de riesgos internos'
  module: Module 3 - Implement Insider Risk Management
---

## Inquilinos de WWL: términos de uso

Si se te proporciona un inquilino porque estás realizando un curso dirigido por un instructor, ten en cuenta que ese inquilino está disponible únicamente como apoyo para los laboratorios prácticos del curso.

Los inquilinos no deben compartirse ni usarse para otros fines que no sean los de los laboratorios prácticos. El inquilino usado en este curso es un inquilino de prueba y no se puede usar ni tener acceso a él después de que la clase haya terminado y no es apto para la extensión.

Los inquilinos no se deben convertir a suscripciones de pago. Los inquilinos obtenidos como parte de este curso siguen siendo propiedad de Microsoft Corporation y nos reservamos el derecho de acceso y recuperación en cualquier momento.

# Laboratorio 3: Ejercicio 1: Implementación de la administración de riesgos internos

Eres Joni Sherman, administrador de seguridad de la información para Contoso Ltd. Tu rol implica garantizar el cumplimiento normativo y proteger la información confidencial dentro de la organización. Recientemente, Contoso Ltd. ha observado actividades inusuales de exploración que podrían exponer datos confidenciales. Para abordar de forma proactiva este riesgo interno, implementarás Administración de riesgos internos de Microsoft Purview, centrándote en identificar, analizar y responder a posibles amenazas internas de forma eficaz.

**Tareas:**

1. Asignación de permisos de administración de riesgos internos
1. Configuración de indicadores de riesgo interno
1. Creación de una directiva de riesgos internos
1. Personalización de la directiva de fugas de datos
1. Habilitación de la integración con Microsoft Defender para punto de conexión con administración de riesgos internos.
1. Habilitación de indicadores y configuración de usuarios prioritarios
1. Creación de una directiva para infracciones de directivas de seguridad por parte de los usuarios prioritarios
1. Creación de una plantilla de aviso

## Tarea 1: Asignación de permisos de administración de riesgos internos

En esta tarea, asignarás a Joni Sherman el rol de administración de riesgos internos para que pueda acceder a las características de riesgo interno y administrarlas en Microsoft Purview.

1. Inicia sesión en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-cl1\admin**.

1. En Microsoft Edge, ve a **`https://purview.microsoft.com`** e inicia sesión en Microsoft Purview portal como Administrador MOD, `admin@WWLxZZZZZZ.onmicrosoft.com` (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de administrador te la debería haber proporcionado tu proveedor de servicios de hospedaje de laboratorio.

1. Selecciona **Configuración** > **Roles y ámbitos** > **Grupos de roles**.

1. En la página **Grupos de roles para soluciones de Microsoft Purview**, selecciona **Administración de riesgos internos**.

1. En el panel flotante **Administración de riesgos internos** de la derecha, selecciona **Editar**.

1. En la página **Editar miembros del grupo de roles**, selecciona **+ Elegir usuarios**.

1. En el panel flotante **Elegir usuarios**, busca `Joni` y activa la casilla de **Joni Sherman**.

1. Selecciona el botón **Seleccionar** en la parte inferior del panel.

1. En la página **Editar miembros del grupo de roles**, selecciona **Siguiente**.

1. En la página **Revisar el grupo de roles y finalizar**, selecciona **Guardar**.

1. Una vez que hayas agregado a Joni correctamente al grupo de roles, selecciona **Listo** en la página **El grupo de roles se actualizó correctamente**.

1. Cierra la sesión de la cuenta **Administrador MOD** mediante la selección del icono MA en la parte superior derecha y selecciona **Cerrar sesión**.

Has asignado a Joni los permisos necesarios para trabajar con administración de riesgos internos en Microsoft Purview portal.

## Tarea 2: Configuración de indicadores de riesgo interno

Antes de crear una directiva de riesgos internos, activarás los indicadores necesarios para la detección. Estos indicadores definen los tipos de actividad de riesgo que buscará el sistema.

1. Abre **Microsoft Edge**, ve a **`https://purview.microsoft.com`** e inicia sesión en Microsoft Purview portal como `JoniS@WWLxZZZZZZ.onmicrosoft.com` (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio).

1. Selecciona **Configuración** > **Administración de riesgos internos**.

1. Selecciona la pestaña de la izquierda para **Indicadores de directiva**.

1. En la página **Indicadores de directiva**, expande y selecciona **Seleccionar todo** para habilitar todos los indicadores de estas categorías:

   - Indicadores de Office
   - Detección de filtración acumulativa

1. Seleccione **Guardar** en la parte inferior de la página.

Has habilitado indicadores de directiva clave para que el sistema pueda detectar acciones confidenciales, como la filtración de archivos o la actividad de Office de riesgo.

## Tarea 3: Creación de una directiva de riesgo interno

En esta tarea, crearás una directiva rápida de fugas de datos para detectar y responder automáticamente al comportamiento de usuario de riesgo relacionado con la filtración de datos. Las directivas rápidas usan plantillas integradas y umbrales predeterminados para simplificar la configuración.

1. En Microsoft Purview, selecciona **Soluciones**  > **** > **Directivas de administración de riesgos internos**.

1. En la página **Directivas**, selecciona **Crear directiva** y, a continuación, selecciona **Directiva rápida**.

1. En el control flotante **Crear directivas rápidas**, selecciona **Comenzar** en **Filtraciones de datos**.

1. Revisa la configuración para crear una directiva de filtración de datos rápida y, a continuación, selecciona **Crear directiva**.

1. En la página **La directiva de filtración de datos se está creando**, activa las casillas para:

   - Enviarme un correo electrónico cuando las directivas tienen advertencias sin resolver
   - Enviarme un correo electrónico cuando se generan nuevas alertas de gravedad alta

     A continuación, selecciona **Actualizar configuración de notificación**.

1. En la parte inferior de la página **La directiva de filtración de datos se está creando**, selecciona **Listo**.

Has creado una directiva rápida para detectar posibles filtraciones de datos mediante la configuración predeterminada. A continuación, lo personalizarás para resolver la advertencia de configuración.

## Tarea 4: Personalización de la directiva de filtraciones de datos

Algunas directivas de riesgo interno requieren indicadores adicionales para funcionar correctamente. En esta tarea, modificarás la directiva para habilitar los indicadores de secuencia y llevar la directiva a un estado correcto.

En la página **Directivas** de **Administración de riesgos internos**, observarás que la directiva de filtración de datos tiene una recomendación.

1. Selecciona la **Directiva rápida de filtración de datos** que acabas de crear.

1. Revisa la recomendación en la página del control flotante de la directiva. Tienes una advertencia que indica que los **Indicadores necesarios del desencadenador de secuencia no están seleccionados**. Para resolver esta advertencia, selecciona **Editar directiva**.

1. En la página **Elegir una plantilla de directiva**, selecciona **Siguiente**.

1. En la página **Asignar nombre a la directiva**, selecciona **Siguiente**.

1. En la página **Elegir usuarios, grupos y ámbitos adaptativos**, selecciona **Siguiente**.

1. En la página **Excluir usuarios y grupos (opcional) (versión preliminar)**, selecciona **Siguiente**.

1. En la página **Decidir si se debe priorizar el contenido**, selecciona **Siguiente**.

1. En la página **Elegir evento de desencadenamiento para esta directiva**, revisa la página **Seleccionar qué secuencias desencadenarán esta directiva** y consulta la información que indica **Algunas secuencias requieren que se activen indicadores específicos en "Configuración" antes de que se puedan seleccionar a continuación.**

1. Selecciona la opción **Activar indicadores** para habilitar los indicadores de secuencia necesarios para esta directiva.

1. Las filtraciones de datos son principalmente una directiva de riesgo interno de filtración de datos. En el cuadro de diálogo para habilitar los indicadores de secuencia, selecciona **Seleccionar todo** para activar todos los **indicadores de filtración** necesarios y, a continuación, selecciona **Guardar**.

1. Selecciona **Siguiente** en la página **Elegir evento de desencadenamiento para esta directiva**.

1. En la página **Elegir umbrales para desencadenar eventos**, selecciona **Siguiente**.

1. En la página **Indicadores**, selecciona **Siguiente**.

1. En la página **Opciones de detección**, selecciona **Siguiente**.

1. En la página **Elegir tipo de umbral para indicadores**, selecciona **Siguiente**.

   Esta directiva usa un evento e indicadores desencadenadores integrados. Comienza a evaluar la actividad del usuario solo cuando Microsoft Defender para punto de conexión detecta amenazas como la evasión de defensa o el software no deseado.

1. En la **página Revisar configuración y finalizar**, seleccione **Enviar**.

1. Selecciona **Listo** en la página **Se creó la directiva**.

1. De nuevo en la página de **Directivas**, la directiva debería tener ahora un estado **Correcto**.

La directiva de riesgo interno ahora es correcta y está lista para detectar actividades de riesgo basadas en desencadenadores de secuencia e indicadores habilitados.

## Tarea 5: Habilitación de la integración de Microsoft Defender para punto de conexión con la administración de riesgos internos

En esta tarea, habilitarás la integración entre Microsoft Defender para punto de conexión y Microsoft Purview para que las alertas de seguridad se puedan usar en las directivas de riesgo interno.

1. En Microsoft Edge, ve a Microsoft Defender desde `https://security.microsoft.com`.

1. En el panel de navegación izquierdo, selecciona **Configuración** > **de puntos de conexión** > **Funciones avanzadas**.

1. Desplázate hacia abajo y establece el botón de alternancia en **Activado** para **Compartir alertas de puntos de conexión con el Centro de cumplimiento de Microsoft**.

   ![Captura de pantalla que muestra Compartir puntos de conexión con la alternancia del Centro de cumplimiento de Microsoft.](../Media/enable-irm-in-mde.png)

1. Selecciona **Guardar preferencias** en la parte inferior de la pantalla.

Has habilitado correctamente Defender para punto de conexión para compartir alertas con Microsoft Purview.

## Tarea 6: Habilitación de indicadores y configuración de usuarios prioritarios

En esta tarea, configurarás los indicadores de directiva y crearás un grupo de usuarios prioritarios que se puede usar en las directivas de riesgo interno.

> [!note] Los indicadores de Microsoft Defender para punto de conexión pueden aparecer atenuados y no seleccionables si la integración de la tarea anterior no ha terminado de procesarse. Si esto sucede, espera unos minutos y actualiza la página antes de continuar.

1. En **Microsoft Edge**, ve a `https://purview.microsoft.com`.

1. Selecciona **Configuración** > **Administración de riesgos internos**.

1. Selecciona la pestaña de la izquierda para **Indicadores de directiva**.

1. En la página **Indicadores de directiva**, expande y selecciona **Seleccionar todo** para habilitar todos los indicadores de estas categorías:

   - Indicadores de Microsoft Defender para punto de conexión (versión preliminar)
   - Indicadores de exploración de riesgo (versión preliminar)

1. Seleccione **Guardar** en la parte inferior de la página.

1. Selecciona la pestaña **Grupos de usuarios prioritarios** y, a continuación, selecciona **+ Crear grupo de usuarios prioritarios**.

1. En la página **Nombre y descripción del grupo de usuarios prioritarios**, escribe:

   - **Nombre**: `Finance team`
   - **Descripción**: `Team members who manage financial operations, budgeting, and payroll systems.`

1. Seleccione **Siguiente**.

1. En la página **Miembros**, haz clic en **+ Miembros**.

1. En el control flotante **Miembros**, busca y selecciona:

   - `Lynne Robbins`
   - `Debra Berger`
   - `Megan Bowen`

1. Selecciona **Agregar** para agregar los tres miembros al grupo de prioridad del equipo financiero.

1. Seleccione **Siguiente**.

1. En **Elegir quién puede ver los datos que implican a los usuarios de este grupo de prioridad**, selecciona **+ Elegir usuarios y grupos de roles**.

1. En el control flotante, active la casilla **Administración de riesgos internos** y, a continuación, selecciona **Agregar**.

1. Seleccione **Siguiente**.

1. **Revisa** y **Envía** la configuración y, a continuación, selecciona **Listo** una vez que se haya creado el grupo de usuarios prioritarios.

Has configurado indicadores de directiva y has creado un grupo de prioridad para supervisar usuarios de alto riesgo.

## Tarea 7: Creación de una directiva para infracciones de directivas de seguridad por parte de los usuarios prioritarios

En esta tarea, crearás una directiva de riesgos internos que detecta alertas de Defender para punto de conexión para la actividad de riesgo por parte de los usuarios prioritarios.

1. En Microsoft Purview, selecciona **Soluciones** > **Administración de riesgos internos** > **Directivas**.

1. En la página **Directivas**, selecciona **Crear directiva** y, a continuación, selecciona **Directiva personalizada**.

1. En la página **Elegir una plantilla de directiva**, selecciona **Infracciones de directiva de seguridad por parte de usuarios prioritarios (versión preliminar)** y, a continuación, selecciona Siguiente.

1. En la página **Asignar nombre a la directiva** escribe:

   - **Nombre**: `Security policy violations - Priority users`
   - **Descripción**: `Detects Defender for Endpoint alerts for risky activity by priority users, such as malware or disabled protections.`

1. Seleccione **Siguiente**.

1. En la página **Elegir usuarios, grupos y ámbitos adaptables**, selecciona **Agregar o editar grupos de usuarios prioritarios**.

1. En el control flotante **Elegir grupos de usuarios prioritarios**, activa la casilla del grupo **Equipo financiero** y, a continuación, selecciona Agregar.

1. Seleccione **Siguiente**.

1. En la página **Decidir si se debe priorizar el contenido**, selecciona **Siguiente**.

1. En la página **Elegir evento de desencadenamiento para esta directiva**, selecciona **Siguiente**.

1. En la página **Indicadores**, selecciona **Siguiente**.

1. En la página **Elegir tipo de umbral para indicadores**, deja seleccionada la opción predeterminada **Aplicar umbrales proporcionados por Microsoft** y, a continuación, selecciona **Siguiente**.

1. En la **página Revisar configuración y finalizar**, seleccione **Enviar**.

1. En la página **Se creó la directiva**, selecciona **Listo**.

Has creado una directiva de riesgo interno personalizada que usa señales de Defender para punto de conexión para detectar actividades de riesgo de los usuarios prioritarios.

## Tarea 8: Creación de una plantilla de aviso

En esta tarea, crearás una plantilla de aviso en Microsoft Purview para notificar a los usuarios cuando se desencadene una alerta de riesgo interno.

1. En Microsoft Purview, selecciona **Soluciones** > **Administración de riesgos internos** > **Plantillas de aviso**.

1. En la página **Plantillas de aviso**, selecciona **+ Crear plantilla de aviso**.

1. Rellena la información necesaria en el panel flotante **Crear una nueva plantilla de aviso** a la derecha.

    - **Nombre de plantilla**: `Security Violation Alert`
    - **Enviar de**: `Joni Sherman`
    - **Asunto**: `Unusual activity detected - please review`
    - **Cuerpo del mensaje**:

        ````html
        <!DOCTYPE html>
        <html>
        <body>
        <h2>Security Alert</h2>
        <p>We've detected activity from your account that might violate our organization's security policies. This could be due to malware, disabled protections, or other risky behavior.</p>
        <p>Please review your recent actions and ensure your device security settings are up to date. If you believe this alert was generated in error, contact the IT Security team for assistance.</p>
        <p>To avoid future issues, refer to the <a href="https://contoso.com/security-guidelines">Contoso Security Guidelines</a>.</p>
        <p>Thank you,</p>
        <p><em>Compliance and Security Team</em></p>
        </body>
        </html>
        ````

1. Seleccione **Crear**.

1. De nuevo en la página **Plantillas de aviso** verás la plantilla **Alerta de infracción de seguridad** que acabas de crear.

Has creado una plantilla de aviso que la administración de riesgos internos puede usar para notificar a los usuarios las infracciones de la directiva de seguridad.
