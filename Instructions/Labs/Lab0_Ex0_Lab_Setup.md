---
lab:
  title: 'Configuración del laboratorio: Preparación del entorno para administración'
  module: Lab setup
---

## Inquilinos de WWL: términos de uso

Si se te proporciona un inquilino porque estás realizando un curso dirigido por un instructor, ten en cuenta que ese inquilino está disponible únicamente como apoyo para los laboratorios prácticos del curso.

Los inquilinos no deben compartirse ni usarse para otros fines que no sean los de los laboratorios prácticos. El inquilino usado en este curso es un inquilino de prueba y no se puede usar ni tener acceso a él después de que la clase haya terminado y no es apto para la extensión.

Los inquilinos no se deben convertir a suscripciones de pago. Los inquilinos obtenidos como parte de este curso siguen siendo propiedad de Microsoft Corporation y nos reservamos el derecho de acceso y recuperación en cualquier momento.

# Configuración del laboratorio: Preparación del entorno para administración

En este laboratorio, configurarás y prepararás el entorno para las tareas de administración. Activarás las características necesarias, configurarás los permisos administrativos y garantizarás la configuración adecuada de los elementos clave.

**Tareas:**

1. Habilitación de la auditoría en el Portal de Microsoft Purview
1. Establecimiento de contraseñas de usuario para ejercicios de laboratorio
1. Habilitar incorporación de dispositivos
1. Habilitación del análisis de riesgos internos

## Tarea 1: Habilitación de la auditoría en Microsoft Purview portal

En esta tarea, habilitarás la auditoría en el Portal de Microsoft Purview para supervisar las actividades del portal.

1. Todavía debes tener la sesión iniciada en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin** y en Microsoft 365 con la cuenta Administrador MOD.

1. Abre una ventana de terminal con privilegios elevados mediante la selección del botón Windows con el botón derecho del ratón y luego selecciona **Terminal (Administrador)**.

1. Ejecuta el cmdlet **Install Module** en la ventana de terminal para instalar la versión más reciente del módulo **PowerShell de Exchange Online**:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```

1. Para confirmar el mensaje del proveedor de NuGet, escribe **Y** para Sí y presiona **Entrar**.

1. Confirma el cuadro de diálogo de seguridad de repositorio no de confianza con **Y** para Sí y presiona **Entrar**.  Este proceso puede tardar un tiempo en finalizar.

1. Ejecuta el cmdlet **Set-ExecutionPolicy** para cambiar la directiva de ejecución y presiona **Entrar**

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

1. Cierra la ventana PowerShell.

1. Abre una ventana normal (sin privilegios elevados) de PowerShell; para ello, haz clic con el botón derecho en el botón Windows y selecciona **Terminal**.

1. Ejecuta el cmdlet **Connect-ExchangeOnline** para usar el módulo PowerShell de Exchange Online y conéctate al inquilino:

    ```powershell
    Connect-ExchangeOnline
    ```

1. Cuando se muestra la ventana **Iniciar sesión**, deberás iniciar sesión como `admin@WWLxZZZZZZ.onmicrosoft.com` (donde ZZZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje de laboratorio). La contraseña de administrador te la debería haber proporcionado tu proveedor de servicios de hospedaje de laboratorio.

1. Para comprobar si Audit está habilitado, ejecuta el cmdlet **Get-AdminAuditLogConfig**:

    ```powershell
    Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    ```

1. Si _UnifiedAuditLogIngestionEnabled_ devuelve falso, significa que la auditoría está deshabilitada.

1. Para habilitar el registro de auditoría, ejecuta el cmdlet **Set-AdminAuditLogConfig** y establece **UnifiedAuditLogIngestionEnabled** en _true_:

    ```powershell
    Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    ```

1. Para comprobar que la auditoría está habilitada, vuelve a ejecutar el cmdlet **Get-AdminAuditLogConfig**:

    ```powershell
    Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    ```

1. _UnifiedAuditLogIngestionEnabled_ debe devolver _true_ para que sepas que la auditoría está habilitada.

<!---

1. In Microsoft Edge, navigate to the Microsoft Purview portal, `https://purview.microsoft.com`, and log in.

1. A message about the new Microsoft Purview portal will appear on the screen. Select the option to agree with the terms of data flow disclosure and the privacy statement, then select **Try now**.

    ![Screenshot showing the Welcome to the new Microsoft Purview portal screen.](../Media/welcome-purview-portal.png)

1. Select **Solutions** from the left sidebar, then select **Audit**.

1. On the **Search** page, select the **Start recording user and admin activity** bar to enable audit logging.

    ![Screenshot showing the Start recording user and admin activity button.](../Media/enable-audit-button.png)

1. Once you select this option, the blue bar should disappear from this page.

-->

## Tarea 2: Establecimiento de contraseñas de usuario para ejercicios de laboratorio

En esta tarea, establecerás contraseñas para las cuentas de usuario necesarias para los laboratorios.

1. Inicia sesión en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin**. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.

1. Abre **Microsoft Edge** y ve a **`https://admin.microsoft.com`** para iniciar sesión en el Centro de administración de Microsoft 365 como Administrador MOD, `admin@WWLxZZZZZZ.onmicrosoft.com` (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio).

1. En el panel de navegación izquierdo, expande **Usuarios** y selecciona **Todos los usuarios**.

1. Activa la casilla situada a la izquierda de **Joni Sherman**, **Lynne Robbins** y **Megan Bowen**.

   Estas cuentas se usarán en todos los ejercicios del laboratorio.

   ![Captura de pantalla que muestra las cuentas de usuario que deben restablecerse.](../Media/user-accounts.png)

1. Selecciona el botón **Restablecer contraseña** en el panel de navegación superior para restablecer las tres contraseñas.

   ![Captura de pantalla que muestra el botón Restablecer contraseña en el Centro de administración de Microsoft 365.](../Media/reset-password-button.png)

1. En la página flotante **Restablecer contraseña** de la derecha, asegúrate de que ambas casillas están deseleccionadas.

   Esto garantizará que puedas seleccionar una contraseña para los tres usuarios que se usan para ejercicios y que estas contraseñas no deban restablecerse al iniciar sesión por primera vez.

1. En el campo **Contraseña**, escribe una contraseña que puedas recordar para restablecer las contraseñas de usuario que se usarán en ejercicios futuros.

1. En la parte inferior de la página flotante **Restablecer contraseña**, selecciona el botón **Restablecer contraseña**.

1. En la página **Se han restablecido las contraseñas**, deberías ver las tres cuentas de usuario que se han restablecido. En la parte inferior de esta página flotante, selecciona **Cerrar**.

Has restablecido correctamente las contraseñas de los ejercicios de laboratorio.

## Tarea 3: Habilitación de la incorporación de dispositivos

En esta tarea, habilitarás la incorporación de dispositivos para tu organización.

1. Todavía deberías estar conectado en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin** y deberías estar como Administrador de MOD en Microsoft 365.

1. En **Microsoft Edge**, ve a **`https://purview.microsoft.com`** para iniciar sesión en Microsoft Purview y selecciona **Configuración** en la barra lateral izquierda.

1. En la barra lateral izquierda, expande **Incorporación de dispositivos** y selecciona **Dispositivos**.

1. En la página **Dispositivos**, selecciona **Activar la incorporación de dispositivos** y, después, selecciona **Aceptar** para habilitar la incorporación de dispositivos.

1. Cuando se te solicite, selecciona **Aceptar** para confirmar que la supervisión de dispositivos está activada.

Ya has habilitado la incorporación de dispositivos, así que puedes empezar a incorporar dispositivos para protegerte con directivas DLP de punto de conexión. El proceso para habilitar la característica puede tardar hasta 30 minutos.

## Tarea 4: Habilitación del análisis de riesgos internos

En esta tarea, habilitarás el análisis para la administración de riesgos internos.

1. Todavía deberías estar conectado en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin** y estar como Administrador de MOD en Microsoft Purview.

1. En Microsoft Purview, ve a **Configuración** > **Administración de riesgos internos** > ** Análisis.**

1. Alterna **Análisis** a **Activado** y selecciona **Guardar**.

Has habilitado el análisis para la administración de riesgos internos.

## Tarea 5: Inicialización de Microsoft Defender XDR

En esta tarea, abrirás Microsoft Defender y esperarás a que Microsoft Defender XDR termine de inicializarse.

1. Todavía deberías estar conectado en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin** y estar como Administrador de MOD en Microsoft Purview.

1. En **Microsoft Edge**, ve a **`https://security.microsoft.com/`** para abrir Microsoft Defender.

1. En el panel de navegación, selecciona **Investigación y respuesta** > **Incidentes y alertas** > ** Incidentes.**

1. Verás un mensaje que indica que se está preparando Microsoft Defender XDR. Este proceso se ejecuta automáticamente y puede tardar unos minutos.

   ![Captura de pantalla que muestra la incorporación de Microsoft Defender XDR.](../Media/enable-defender-xdr.png)

Se está inicializando Microsoft Defender XDR. Puedes continuar con otras tareas mientras finaliza la configuración.
