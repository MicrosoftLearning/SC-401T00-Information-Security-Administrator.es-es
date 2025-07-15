---
lab:
  title: 'Ejercicio 1: Implementación y administración de directivas DLP'
  module: Module 2 - Implement Data Loss Prevention
---
## Inquilinos de WWL: términos de uso

Si se te proporciona un inquilino porque estás realizando un curso dirigido por un instructor, ten en cuenta que ese inquilino está disponible únicamente como apoyo para los laboratorios prácticos del curso.

Los inquilinos no deben compartirse ni usarse para otros fines que no sean los de los laboratorios prácticos. El inquilino usado en este curso es un inquilino de prueba y no se puede usar ni tener acceso a él después de que la clase haya terminado y no es apto para la extensión.

Los inquilinos no se deben convertir a suscripciones de pago. Los inquilinos obtenidos como parte de este curso siguen siendo propiedad de Microsoft Corporation y nos reservamos el derecho de acceso y recuperación en cualquier momento.

# Laboratorio 2: Ejercicio 1: Implementación y administración de directivas DLP

A Joni Sherman, la administradora de seguridad de la información recién contratada en Contoso Ltd., se le ha pedido que configure directivas de prevención de pérdida de datos (DLP) para ayudar a proteger los datos confidenciales de los clientes en Microsoft 365. En este laboratorio, usarás Microsoft Purview y Microsoft Defender para crear y administrar directivas DLP que detecten y restrinjan el uso compartido de la información confidencial, como números de tarjeta de crédito e identificadores de empleado.

**Tareas:**

1. Creación de una directiva DLP en modo de simulación
1. Modificación de una directiva DLP
1. Creación de una directiva DLP en PowerShell
1. Activación de una directiva en modo de simulación
1. Modificación de la prioridad de la directiva
1. Habilitación de la inspección de archivos en Microsoft 365 Defender
1. Creación de una directiva de archivos para Microsoft Defender 365

## Tarea 1: Creación de una directiva DLP en modo de simulación

En esta tarea, crearás una directiva DLP en modo de simulación destinada a los números de tarjeta de crédito en los mensajes de Teams. La directiva notificará a los usuarios cuando intenten compartir contenido confidencial y les permitirá invalidar con una justificación.

1. Inicia sesión en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin**.

1. En **Microsoft Edge**, ve a **`https://purview.microsoft.com`** e inicia sesión en Microsoft Purview Portal como **Joni Sherman**. Inicia sesión como `JoniS@WWLxZZZZZZ.onmicrosoft.com`, (ZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de Joni se estableció en un ejercicio anterior.

1. Selecciona **Soluciones** > **Prevención de pérdida de datos** > **Directivas**.

1. En la página **Directivas**, selecciona **+ Crear directiva** para iniciar la configuración para crear una nueva directiva de prevención de pérdida de datos.

1. En la página **Iniciar con una plantilla o crear una directiva personalizada**, selecciona **Personalizado** como categoría y, después, selecciona **Directiva personalizada** en **Reglamentos**.

1. Selecciona **Siguiente**.

1. En la página **Introducir el nombre de la directiva DLP** escribe:

   - **Nombre**: `DLP - Credit Card Protection`
   - **Descripción**: `Detect and restrict sharing of credit card numbers in Teams messages.`

1. Selecciona **Siguiente**.

1. En la página **Asignar unidades de administración**, selecciona **Siguiente**.

1. En la página **Elegir ubicaciones para aplicar la directiva**, habilita la ubicación solo para **Mensajes de chat y canal de Teams**. Si se seleccionan otras ubicaciones, anula la selección.

1. Selecciona **Siguiente**.

1. En la página **Definir la configuración de directiva**, selecciona **Crear o personalizar reglas DLP avanzadas** y, a continuación, selecciona **Siguiente**.

1. En **Personalizar reglas avanzadas de DLP**, selecciona **+ Crear regla**.

1. En el control flotante **Crear regla**:
    - En el campo **Nombre**, escriba `Credit card information`.

1. En **Condiciones**, selecciona **+ Agregar condición** > **Contenido se comparte en Microsoft 365**.

1. En la sección **Contenido se comparte desde Microsoft 365**:
    - Selecciona la opción para **con personas ajenas a mi organización**.

1. Selecciona **+ Agregar condición** > **El contenido incluye**.

1. En la nueva sección **El contenido incluye**:
    - Selecciona **Agregar** > **Tipos de información confidencial**.
    - En la página **Tipos de información confidencial**, busca y selecciona `Credit Card Number` y, después, selecciona **Agregar**.

1. En **Acciones**, selecciona **+ Agregar una acción** > **Restringir acceso o cifrar el contenido en las ubicaciones de Microsoft 365**.

1. En la sección **Restringir el acceso o cifrar el contenido**:
    - Selecciona **Solo bloquear personas ajenas a la organización**.

1. En **Notificaciones de usuario**:
    - Activa el botón de alternancia **Usar notificaciones para informar a los usuarios y ayudar a educarles sobre el uso apropiado de la información confidencial.**.
    - Activa la casilla **Notificar a los usuarios en el servicio de Office 365 con una sugerencia de directiva**.

1. En **Invalidaciones de usuario**:
    - Activa la casilla **Permitir que los usuarios invaliden restricciones de directivas** (Fabric, Exchange, SharePoint, OneDrive y Teams).
    - Activa la casilla **Requerir una justificación comercial para invalidar**.

1. En **Informes de incidentes**, en el elemento desplegable **Usar este nivel de gravedad en alertas de administrador e informes**:
    - Selecciona **Bajo**.

1. En la parte inferior del panel de control flotante **Crear regla**, selecciona **Guardar**.

1. Vuelve a la página **Personalizar reglas DLP avanzadas** y selecciona **Siguiente**.

1. En la página **Modo de directiva**, selecciona **Ejecutar la directiva en modo de simulación** y activa la casilla **Mostrar sugerencias de directiva mientras se está en modo de simulación**.

1. Selecciona **Siguiente**.

1. En la página **Revisar y finalizar**, revisa la configuración y selecciona **Enviar**.

1. En la página **Nueva directiva creada**, selecciona **Listo**.

Has creado una directiva DLP que examina el contenido de Teams en busca de números de tarjeta de crédito y permite invalidaciones con una justificación comercial.

## Tarea 2: Modificación de una directiva DLP

En esta tarea, expandirás el ámbito de la directiva DLP existente para incluir correo electrónico de Exchange. Esto ayuda a garantizar una protección coherente en los canales de comunicación adicionales.

1. Todavía debes tener la sesión iniciada en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin** y en Microsoft 365 como **Joni Sherman**.

1. Deberías encontrarte en la página **Directivas** de Microsoft Purview. Si no es así, abra **Microsoft Edge** y ve a `https://purview.microsoft.com`. Selecciona **Soluciones** > **Prevención de pérdida de datos** > **Directivas**.

1. En la página **Directivas**, activa la casilla de la **Directiva DLP de protección de tarjetas de crédito** creada recientemente y, después, selecciona **Editar directiva** para abrir la configuración de la directiva.

1. En la página **Nombre de la directiva DLP**, edita la descripción en `Detect and restrict sharing of credit card numbers in Teams and Exchange messages.`

1. Seleccione **Siguiente**.

1. En la página **Asignar unidades de administración**, selecciona **Siguiente**.

1. En la página **Elegir ubicaciones para aplicar la directiva**, activa la casilla **Correo electrónico de Exchange** para agregar esta ubicación a la directiva DLP.

1. Selecciona **Siguiente** hasta llegar a la página **Revisar y finalizar**.

1. Selecciona **Enviar** en la página **Revisar y finalizar** para aplicar el cambio realizado en la directiva.

1. Una vez actualizada la directiva, selecciona **Listo** en la página **Directiva actualizada**.

Has actualizado correctamente la directiva para examinar el correo electrónico junto con los mensajes de Teams.

## Tarea 3: Creación de una directiva DLP en PowerShell

En esta tarea, crearás una directiva DLP mediante PowerShell para bloquear el uso compartido de identificadores de empleado por correo electrónico. Este enfoque muestra cómo definir y aplicar la configuración de directivas mediante scripting.

1. Todavía debes tener la sesión iniciada en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin**.

1. Abre una ventana de PowerShell con privilegios elevados haciendo clic con el botón derecho en el botón **Inicio** de la barra de tareas y selecciona **Terminal (Administrador)**.

1. Ejecuta el cmdlet **Connect-IPPSSession** para conectarte a Security & Compliance PowerShell:

    ```powershell
    Connect-IPPSSession
    ```

1. Inicia sesión como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (ZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio) en la ventana emergente **Iniciar sesión en tu cuenta**. La contraseña de Joni se estableció en un ejercicio anterior.

1. Ejecuta el cmdlet **New-DlpCompliancePolicy** para crear una directiva DLP que examine todos los buzones de Exchange:

    ```powershell
    New-DlpCompliancePolicy -Name "EmployeeID DLP Policy" -Comment "This policy blocks sharing of Employee IDs" -ExchangeLocation All
    ```

1. Ejecuta el cmdlet **New-DlpComplianceRule** para agregar una regla DLP a la directiva DLP que creaste en el paso anterior. Esta directiva usa el tipo de información confidencial **Contoso Employee IDs** que creaste en un ejercicio anterior:

    ```powershell
    New-DlpComplianceRule -Name "EmployeeID DLP rule" -Policy "EmployeeID DLP Policy" -BlockAccess $true -ContentContainsSensitiveInformation @{Name="Contoso Employee IDs"}
    ```

1. Ejecuta el cmdlet **Get-DLPComplianceRule** para revisar la **Regla DLP employeeID**:

    ```powershell
    Get-DLPComplianceRule -Identity "EmployeeID DLP rule"
    ```

Has usado PowerShell correctamente para crear una directiva DLP que bloquee el uso compartido de identificadores de empleado.

## Tarea 4: Activación de una directiva en modo de simulación

Ahora que se ha probado la directiva DLP en la simulación, la activarás para empezar a aplicar sus acciones.

1. Todavía debes tener la sesión iniciada en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin** y en Microsoft 365 como **Joni Sherman**.

1. En **Microsoft Edge**, ve a Directivas DLP; para ello, ve a `https://purview.microsoft.com` > **Soluciones** > **Prevención de pérdida de datos** y selecciona **Directivas** en la barra lateral izquierda.

1. En la página **Directivas**, selecciona la directiva **DLP - Credit Card Protection**.

1. En la parte inferior del control flotante de la derecha, selecciona **Ver simulación**.

1. En la página de simulación, dedica un momento a explorar:

   - La pestaña **Información general de la simulación**, que muestra el progreso del examen, las coincidencias totales y el estado del examen por ubicación.
   - La **pestaña Elementos para revisar**, donde las coincidencias previstas aparecerán una vez disponibles.
   - La **pestaña Alertas**, donde se mostrarían las alertas desencadenadas en el modo de simulación.

1. Después de explorar la información en el modo de simulación, selecciona **Activar la directiva** y **Confirmar** para activar la directiva DLP.

   Aparecerá un control flotante de confirmación que indica que la directiva se ha publicado correctamente.

La directiva ahora está activa y aplica restricciones en la información de las tarjeta de crédito en Teams y Exchange.

## Tarea 5: Modificación de la prioridad de la directiva

Cuando existen varias directivas, su prioridad determina cuál se aplica primero. En esta tarea, moverás la directiva de identificador de empleado a la prioridad más alta.

1. Todavía debes tener la sesión iniciada en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin** y en Microsoft 365 como **Joni Sherman**.

1. En **Microsoft Edge**, debería seguir abierta la pestaña de Microsoft Purview Portal en la página **Directivas**. Si no es así, abra **Microsoft Edge** y ve a `https://purview.microsoft.com`. Selecciona **Soluciones** > **Prevención de pérdida de datos** > **Directivas**.

1. En la página **Directivas**, selecciona la **directiva DLP EmployeeID**.

1. Selecciona **Cambiar las prioridades** en la cinta de navegación superior y, después, selecciona **Mover a la parte superior (prioridad más alta).**

1. En la ventana **Prevención de pérdida de datos**, selecciona **Actualizar** y revisa la prioridad en la columna **Orden** de la tabla de directivas.

1. Cierre la sesión de la cuenta de Joni seleccionando su icono en la parte superior derecha y, después, selecciona **Cerrar sesión**.

Has actualizado la prioridad de la directiva para que la directiva de identificador de empleado tenga prioridad sobre las demás.

## Tarea 6: Habilitación de la inspección de archivos en Microsoft 365 Defender

Algunas directivas de archivos requieren acceso para inspeccionar el contenido de los archivos protegidos. En esta tarea, concederás los permisos necesarios para permitir que Microsoft Defender examine el contenido de los archivos de OneDrive y SharePoint en busca de información confidencial.

1. Todavía deberías estar conectado en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin** y tener la sesión iniciada como Joni Sherman.

1. En **Microsoft Edge**, ve a Microsoft Defender; para ello, ve a `https://security.microsoft.com`. Inicie sesión como **Administrador de MOD**, `admin@WWLxZZZZZZ.onmicrosoft.com` (ZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de administrador te la debería haber proporcionado tu proveedor de servicios de hospedaje de laboratorio.

1. En la barra lateral izquierda, selecciona **Sistema** > **Configuración** y, después, selecciona **Cloud Apps**.

1. En el panel izquierdo de la ventana **Cloud Apps**, desplázate hacia abajo hasta la sección **Information Protection**. En **Inspeccionar archivos protegidos**, selecciona **Conceder permiso** para habilitar la inspección de archivos.

1. Sigue la indicación para permitir los permisos necesarios en Microsoft Entra ID; después, deberías ver que la inspección de archivos está **activa** en Microsoft Defender for Cloud Apps.

1. Cierra la sesión de la cuenta Administrador de MOD; para ello, selecciona el icono de **MA** en la parte superior derecha, selecciona **Cerrar sesión** y cierra la ventana del explorador.

La inspección de archivos está ahora habilitada en Defender, lo que permite que las directivas de archivos busquen contenido confidencial.

## Tarea 7: Creación de una directiva de archivos para Microsoft 365 Defender

En esta tarea, crearás una directiva de archivos en Microsoft Defender que identifica y pone en cuarentena los archivos que contienen números de tarjeta de crédito en OneDrive y SharePoint.

1. Todavía debes tener la sesión iniciada en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin**.

1. Abre **Microsoft Edge**, ve a **`https://security.microsoft.com`** e inicia sesión en el Portal de Microsoft Defender como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (ZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de Joni se estableció en un ejercicio anterior.

1. En el Portal de **Microsoft Defender**, en la navegación izquierda, selecciona **Cloud apps** > **Directivas** y después, selecciona **Administración de directivas**.

1. En la página **Directivas**, selecciona **+ Crear directiva** y, después, selecciona **Directiva de archivos**.

1. En la página **Crear directiva de archivos**, configura:

   - **Nombre de directiva**: `Credit card information for files` 
   - **Gravedad de directiva**: **baja**
   - **Categoría**: **DLP**
   - **Descripción**: `Protect credit card numbers from being shared in files.`
   - En la sección **Archivos que coinciden con toda la siguiente sección**:
      - Para el primer filtro, configura los elementos desplegables en: **El nivel de acceso es igual a Público (Internet), Externo, Público** y agrega **Interno.**
      - Para el segundo filtro, configura los elementos desplegables en: **Última modificación después de (fecha)** y usa la fecha actual.

          ![Captura de pantalla que muestra el elemento desplegable de coincidencias de archivos con la opción interno agregada.](../Media/files-matching-internal.png)

   - En el menú desplegable **Método de inspección**, selecciona **Servicio de clasificación de datos**.
   - En el menú desplegable **Elegir tipo de inspección...**, selecciona **Tipo de información confidencial...**.
   - En el cuadro de diálogo **Seleccionar un tipo de información confidencial**, busca y activa la casilla para `Credit Card Number`.
      - Selecciona **Listo** en la parte superior derecha del cuadro de diálogo **Seleccionar un tipo de información confidencial**.

   - En **Acciones de gobernanza**, expande **Microsoft OneDrive para la Empresa**:
      - Selecciona la casilla **Poner usuario en cuarentena**.
   - Repite el mismo proceso para **Microsoft SharePoint Online**
      - Selecciona la casilla **Poner usuario en cuarentena**.

1. Selecciona **Crear** en la parte inferior de la página para crear la directiva de archivos.

Has creado correctamente una directiva de archivos que detecta y pone en cuarentena los archivos con datos confidenciales de la tarjeta de crédito.
