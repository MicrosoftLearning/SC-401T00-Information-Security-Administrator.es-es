---
lab:
  title: 'Ejercicio 1: Configuración directivas de retención'
  module: Module 5 - Implement and manage retention
---

## Inquilinos de WWL: términos de uso

Si se te proporciona un inquilino porque estás realizando un curso dirigido por un instructor, ten en cuenta que ese inquilino está disponible únicamente como apoyo para los laboratorios prácticos del curso.

Los inquilinos no deben compartirse ni usarse para otros fines que no sean los de los laboratorios prácticos. El inquilino usado en este curso es un inquilino de prueba y no se puede usar ni tener acceso a él después de que la clase haya terminado y no es apto para la extensión.

Los inquilinos no se deben convertir a suscripciones de pago. Los inquilinos obtenidos como parte de este curso siguen siendo propiedad de Microsoft Corporation y nos reservamos el derecho de acceso y recuperación en cualquier momento.

# Laboratorio 5. Ejercicio 1: Implementación y administración de la retención

Eres Joni Sherman, administrador de cumplimiento en Contoso Ltd. La empresa está intensificando la estrategia de seguridad de datos para reducir la exposición a riesgos relacionados con los datos financieros y las comunicaciones privilegiadas. Se te ha pedido que configures las soluciones de retención de Microsoft Purview que admitan la preparación para auditorías, limiten la retención de datos innecesaria y garanticen la supervisión adecuada de las comunicaciones confidenciales.

**Tareas:**

1. Crear una etiqueta de retención.
1. Publicar una etiqueta de retención.
1. Crear una directiva de etiqueta de retención con aplicación automática.
1. Crear una directiva de retención estática.
1. Crear un ámbito adaptable
1. Crear una directiva de retención adaptativa.
1. Recuperar el contenido de SharePoint.

## Tarea 1: Creación de una etiqueta de retención

En esta tarea, crearás una etiqueta de retención para los datos financieros confidenciales que deben conservarse con fines de auditoría e investigación.

1. Inicia sesión en la VM Cliente 1 (SC-401-CL1) como la cuenta **SC-401-cl1\admin** .

1. En Microsoft Edge, ve a `https://purview.microsoft.com` e inicia sesión en Microsoft Purview portal como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de Joni se estableció en un ejercicio anterior.

1. Ve a **Soluciones** > **Administración del ciclo de vida de datos** > **Etiquetas de retención**.

1. En la página **Etiquetas**, selecciona **Crear una etiqueta**.

1. En la página **Nombre de la etiqueta de retención**, escribe:

   - **Nombre**: `Sensitive Financial Records`
   - **Descripción para los usuarios**: `Use for financial files with sensitive data that must be retained for audit or security purposes.`
   - **Descripción para los administradores**: `Retains high-impact financial data for 5 years to support audits and security investigations.`

1. Seleccione **Siguiente**.

1. En la página **Definir configuración de etiqueta**, elige **Conservar elementos para siempre o durante un período específico** y, a continuación, selecciona **Siguiente**.

1. En la página **Definir el período**, asegúrate de que estos valores se establecen para la entrada de configuración del período de retención:

    - **¿Cuánto tiempo dura el período?**: 5 años
    - **¿Cuándo debe comenzar el período?**: Cuando se modifican los elementos.

1. Seleccione **Siguiente**.

1. En la página **Elegir lo que sucede después del periodo de retención**, selecciona **Eliminar elementos automáticamente** y, a continuación, selecciona **Siguiente**.

1. En la **página Revisar y finalizar**, selecciona **Crear etiqueta**.

1. En la página **Se creó la etiqueta de retención**, selecciona la opción **No hacer nada** y, a continuación, selecciona **Listo**.

Has creado una etiqueta de retención que conserva el contenido financiero durante cinco años y lo elimina después para reducir la exposición de los datos.

## Tarea 2: Publicación de una etiqueta de retención

En esta tarea, publicarás la etiqueta de retención para que los usuarios puedan aplicarla en servicios de Microsoft 365 como Exchange, SharePoint y OneDrive.

1. En Microsoft Purview, ve a **Soluciones** > **Administración del ciclo de vida de datos** > **Etiquetas de retención**.

1. Activa la casilla situada junto a la etiqueta **Registros financieros confidenciales** y, a continuación, selecciona el icono **Publicar etiquetas** (![icono Publicar etiquetas](../Media/publish-labels-icon.png)) para publicar esta etiqueta de retención.

1. En la página **Elegir etiquetas para publicar**, comprueba que está seleccionada la etiqueta **Registros financieros confidenciales** y, a continuación, selecciona **Siguiente**.

1. En la página **Ámbito de directiva**, selecciona **Siguiente**.

1. En la página **Elegir el tipo de directiva de retención que se va a crear**, selecciona **Estático** y, después, selecciona **Siguiente**.

1. En la página **Elegir dónde publicar etiquetas**, selecciona **Permitirme elegir ubicaciones específicas** y selecciona:

    - Buzones de Exchange
    - Sitios de SharePoint de comunicación y clásicos
    - Cuentas de OneDrive
    - Anule la selección de todas las demás ubicaciones

1. Seleccione **Siguiente**.

1. En **Nombre de la directiva** escribe:

    - **Nombre**: `Sensitive Financial Data Retention`
    - **Descripción**: `Makes the 'Sensitive Financial Records' label available to users in Exchange, SharePoint, OneDrive, and Teams.`

1. Seleccione **Siguiente**.

1. En la página **Finalizar**, selecciona **Enviar**.  

1. En la página **La etiqueta de retención se publicó**, selecciona **Listo**.

Has publicado la etiqueta de retención, lo que hará que esté disponible para que los usuarios la apliquen en los servicios clave de Microsoft 365.

## Tarea 3: Creación de una etiqueta de retención de aplicación automática.

En esta tarea, configurarás una directiva que aplica automáticamente una etiqueta de retención al contenido que contiene información financiera personal.

1. En Microsoft Purview, ve a **Soluciones ** > **Administración del ciclo de vida de datos** > **Directivas** > **Directivas de etiquetas**.

1. En la página **Directivas de etiquetas**, selecciona **Aplicar automáticamente una etiqueta** para iniciar la configuración de etiqueta.

1. En la **Página Introducción**, escribe:

   - **Nombre**: `Auto-apply Personal Financial PII`
   - **Descripción**: `Applies this label to personal financial data to help meet audit and investigation requirements. Retains content for 3 years.`

1. Seleccione **Siguiente**.

1. En la página **Elegir el tipo de contenido al que deseas aplicar esta etiqueta**, selecciona **Aplicar etiqueta al contenido que contiene información confidencial** y, después, selecciona **Siguiente**.

1. En la página **Contenido que incluye información confidencial**, selecciona la categoría **Financiero** y, a continuación, selecciona la regulación **Gramm-Leach-Bliley Act (GLBA) de EE. UU.** y, después, selecciona **Siguiente**.

1. En la página **Definir contenido que contiene información confidencial**, selecciona **Siguiente**.

1. En la página **Ámbito de directiva**, selecciona **Siguiente**.

1. En la página **Elegir el tipo de directiva de retención que se va a crear**, selecciona **Estático**.

1. En la página **Elegir dónde publicar etiquetas**, selecciona **Permitirme elegir ubicaciones específicas** y selecciona:

    - Buzones de Exchange
    - Sitios de SharePoint de comunicación y clásicos
    - Cuentas de OneDrive
    - Anule la selección de todas las demás ubicaciones

1. En la página **Elegir una etiqueta para aplicar automáticamente**, selecciona **Agregar etiqueta**.

1. En el control flotante **Elegir una etiqueta**, selecciona **Personal Financial PII** y, después, selecciona **Agregar**.

1. De nuevo en **Elegir una etiqueta para aplicar automáticamente**, selecciona **Siguiente**.

1. En **Decidir si se va a probar o ejecutar la directiva**, selecciona **Probar la directiva antes de ejecutarla** y, después, selecciona **Siguiente**.

1. En la página **Revisar y finalizar**, selecciona **Enviar** y, después, selecciona **Listo** en la página **La directiva de etiquetado automático se ha creado**.

Has creado una directiva de aplicación automática que identifica los datos financieros personales y aplica automáticamente una etiqueta de retención.

## Tarea 4: Creación de una directiva de retención estática

En esta tarea, crearás una directiva de retención estática para el contenido de Microsoft Teams para ayudar a reducir el riesgo de datos a largo plazo.

1. En Microsoft Purview, ve a **Soluciones** > **Administración del ciclo de vida de datos** > **Directivas** > **Directivas de retención**.

1. En la página **Directivas de retención**, selecciona **Nueva directiva de retención**.

1. En la **página Nombre a la directiva de retención**, escribe:

   - **Nombre**: `Teams Retention`
   - **Descripción**: `Retains Teams chats and channel messages for 3 years, then deletes them to reduce long-term data risk.`

1. Selecciona **Siguiente**.

1. En la página **Ámbito de directiva**, selecciona **Siguiente**.

1. En la página **Elegir el tipo de directiva de retención que se va a crear**, selecciona **Estático** y, después, selecciona **Siguiente**.

1. En la página **Elegir ubicaciones para aplicar la directiva**, habilita lo siguiente:

   - Mensajes de canal de Teams
   - Chats de Teams e interacciones de Copilot
   - Deja todas las demás ubicaciones deshabilitadas.

1. Seleccione **Siguiente**.

1. En la página **Decidir si deseas conservar el contenido, eliminarlo o ambas cosas**, asegúrate de que estos valores se establecen para la configuración de retención:

   - Selecciona **Retener los elementos durante un período específico**.
   - En **Conservar elementos durante un período específico**, selecciona **Personalizado** en la lista desplegable.
   - Cambia el campo años a `3`.
   - **Iniciar el período de retención en función de**: cuándo se modificaron los elementos por última vez
   - **Al final del período de retención**: elimina los elementos automáticamente

1. Seleccione **Siguiente**.

1. En la página **Revisar y finalizar**, selecciona **Enviar** y luego selecciona **Listo** en la página **Has creado correctamente una directiva de retención**.

Has configurado una directiva de retención estática que conserva los mensajes de Teams durante tres años antes de eliminarlos automáticamente.

## Tarea 5: Creación de un ámbito adaptable

En esta tarea, definirás un ámbito adaptable destinado a grupos de Microsoft 365 asociados a roles de liderazgo y operaciones.

1. En Microsoft Purview, **Configuración** > **Roles y ámbitos** > **Ámbitos adaptables**.

1. En la página **Ámbitos adaptables**, selecciona **+ Crear ámbito**.

1. En la página **Nombre del ámbito de directiva adaptable** escribe:

    - **Nombre**: `Leadership and Ops Groups`
    - **Descripción**: `Targets Leadership and Operations M365 groups with privileged access to sensitive data.`

1. Seleccione **Siguiente**.

1. En la página **Asignar unidad de administración**, selecciona **Siguiente**.

1. En la página **¿Qué tipo de ámbito deseas crear?**, selecciona **Usuarios** y, a continuación, **Siguiente**.

1. En la página **Crear la consulta para definir usuarios**, en la sección **Atributos del usuario**, asegúrate de que estos valores están seleccionados para la configuración del atributo del usuario:

   - Selecciona la lista desplegable **Atributo** y, a continuación, selecciona **Departamento**.
   - Deja el valor predeterminado **es igual a** en el siguiente campo.
   - Escribe `Leadership` como el **Valor**.

1. Agrega un segundo atributo seleccionando **+ Agregar atributo** en la página **Crear la consulta para definir usuarios**. En el nuevo campo en el que acabamos de configurar, configura estos valores:

   - Selecciona el elemento desplegable del operador de consulta y actualízalo de Y a **O**.
   - Selecciona la lista desplegable **Atributo** y, a continuación, selecciona **Departamento**.
   - Deja el valor predeterminado **es igual a** en el siguiente campo.
   - Escribe `Operations`como el **Valor**.

1. Seleccione **Siguiente**.

1. En la página **Revisar y finalizar**, seleccione **Enviar**.

1. Una vez creado el ámbito adaptable, selecciona **Listo** en la página **Se creó el ámbito**.

Has creado un ámbito adaptable para admitir la retención dirigida a grupos con privilegios en la organización.

## Tarea 6: Creación de una directiva de retención adaptable

En esta tarea, usarás el ámbito adaptable que creaste para configurar una directiva de retención para grupos de Microsoft 365 con responsabilidades confidenciales.

1. En Microsoft Purview, ve a **Soluciones** > **Administración del ciclo de vida de datos** > **Directivas** >  **Directivas de retención**.

1. En la página **Directivas de retención**, selecciona **+ Nueva directiva de retención**.

1. En la página **Nombre a la directiva de retención**, escribe:

    - **Nombre**: `Privileged Group Retention`
    - **Descripción**: `Retains content from Leadership and Operations groups for 5 years to support audit and investigation.`

1. Seleccione **Siguiente**.

1. En la página **Ámbito de directiva**, selecciona **Siguiente**.

1. En la página **Elegir el tipo de directiva de retención que se va a crear**, selecciona **Adaptable** y, a continuación, **Siguiente**.

1. En la página **Elegir ámbitos y ubicaciones de la directiva adaptable**, selecciona **+ Agregar ámbitos**.

1. En el panel de control flotante **Elegir ámbitos de directiva adaptable**, activa la casilla de **Liderazgo y grupos de operaciones** y, a continuación, selecciona **Agregar** en la parte inferior del panel.

1. De vuelta en **Elegir las ubicaciones donde aplicar la directiva** habilita:

    - Buzones y sitios de grupo de Microsoft 365
    - Deja todas las demás ubicaciones deshabilitadas.

1. Seleccione **Siguiente**.

1. En la página **Decidir si deseas conservar el contenido, eliminarlo o ambos**, asegúrate de que estos valores se establecen para la configuración de retención:

   - Selecciona **Retener los elementos durante un período específico **.
   - En **Conservar elementos durante un período específico**, selecciona **5 años** en la lista desplegable.
   - **Iniciar el período de retención en función de**: cuándo se modificaron los elementos por última vez
   - **Al final del período de retención**: elimina los elementos automáticamente

1. Seleccione **Siguiente**.

1. En la página **Revisar y finalizar**, seleccione **Enviar**.

1. Una vez creada la directiva, selecciona **Listo**.

Has creado una directiva de retención que se aplicará al contenido que pertenece a grupos con privilegios y se conservará durante cinco años antes de su eliminación.

## Tarea 7: Recuperación de contenido de SharePoint

En esta tarea, simularás la restauración de un documento eliminado de un sitio de SharePoint para validar las opciones de recuperación.

1. Inicia sesión en la VM Cliente 1 (SC-401-CL1) como la cuenta **SC-401-cl1\admin** .

1. En **Microsoft Edge**, ve a **`https://www.office.com`** e inicia sesión en Microsoft 365 como **Joni Sherman**.

1. En la página de aterrizaje de Microsoft Office 365, selecciona el iniciador de aplicaciones (el icono de cuadrícula) en la esquina superior izquierda y, después, selecciona **SharePoint** en el submenú.

   ![Captura de pantalla que muestra dónde se muestran los puntos suspensivos para mostrar el menú de acciones.](../Media/show-more-actions-sharepoint.png)

1. En la página de aterrizaje de SharePoint, busca `Benefits` y selecciona **Ventajas @ Contoso** en los resultados de búsqueda.

1. En la barra lateral izquierda, selecciona **Documentos**.

1. En la página **Documentos**, activa la casilla **Vacation Policies.pptx** selecciona **Eliminar** en la barra de acciones.

1. En el cuadro de diálogo **¿Eliminar?**, selecciona **Eliminar**.

1. Selecciona **Papelera de reciclaje** en la barra lateral izquierda.

1. En la página **Papelera de reciclaje**, haz clic con el botón derecho en **Vacation Policies.pptx** y, después, selecciona **Restaurar**.

1. En la barra lateral izquierda, selecciona **Documentos** y observa que se ha restaurado el archivo.

Has recuperado correctamente un documento eliminado de un sitio de SharePoint.

Has restaurado el contenido eliminado de SharePoint, validando la recuperación de documentos en caso de eliminación accidental o no autorizada.
