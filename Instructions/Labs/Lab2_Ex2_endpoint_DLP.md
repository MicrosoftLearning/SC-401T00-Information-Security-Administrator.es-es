---
lab:
  title: 'Ejercicio 2: Implementación y administración de DLP de puntos de conexión'
  module: Module 2 - Implement Data Loss Prevention
---

# Laboratorio 2. Ejercicio 2: Implementación y administración de DLP del punto de conexión

A Joni Sherman, el administrador de seguridad de la información recién contratado en Contoso Ltd., se le ha pedido que refuerce los controles DLP en los dispositivos de la empresa. Algunos empleados han estado copiando información confidencial del cliente en unidades USB, lo que aumenta el riesgo de exposición de datos. En este laboratorio, Joni configurará una directiva DLP de punto de conexión para bloquear estas transferencias.

**Tareas:**

1. Incorporación de un dispositivo para DLP de punto de conexión
1. Creación de una directiva DLP de punto de conexión
1. Configuración de Punto de conexión DLP
1. Configuración de la extensión de Microsoft Purview

## Tarea 1: Incorporación de un dispositivo para DLP de punto de conexión

En esta tarea, incorporarás un dispositivo Windows 11 para que esté listo para protegerse mediante directivas DLP de punto de conexión.

1. Inicia sesión en la **Client 2 VM (SC-401-CL2)** como la cuenta **SC-401-cl2\admin**.

1. Abre Microsoft Edge y ve a **`https://purview.microsoft.com`** e inicia sesión en Microsoft Purview Portal como **Joni Sherman**. Inicia sesión como `JoniS@WWLxZZZZZZ.onmicrosoft.com`, (ZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de Joni se estableció en un ejercicio anterior.

1. Selecciona **Configuración** en la barra lateral izquierda.

1. En la barra lateral izquierda, expande **Incorporación de dispositivos** y, a continuación, selecciona **Incorporación**.

1. En la página **Incorporación**, en el menú desplegable **Método de implementación**, selecciona **Script local (para hasta 10 máquinas)** y selecciona **Descargar paquete**.

1. En el cuadro de diálogo **Descargas**, mantén el puntero sobre la descarga y, a continuación, selecciona el icono de carpeta para **Mostrar en la carpeta**.

1. Extrae el archivo ZIP en el **Escritorio** de SC-401-CL1. Deberías ver un script denominado **DeviceComplianceLocalOnboardingScript.cmd**.

1. En el escritorio, haz clic con el botón derecho en el archivo **DeviceComplianceLocalOnboardingScript.cmd** que acabas de extraer y selecciona **Mostrar más opciones** y, a continuación, selecciona **Propiedades**.

1. Hacia la parte inferior de la pestaña **General** de la ventana de propiedades, en la sección **Seguridad**, selecciona **Desbloquear** y, a continuación, selecciona **Aceptar** para guardar esta configuración.

1. De nuevo en el escritorio, haz clic con el botón derecho en **DeviceComplianceLocalOnboardingScript.cmd** y selecciona **Ejecutar como administrador**. En el cuadro de diálogo **Control de cuentas de usuario**, selecciona **Sí**.

1. En la pantalla **Símbolo del sistema**, escribe **Y** para confirmar y presiona Entrar.

1. Una vez completado el script, obtendrás un mensaje de operación correcta y un mensaje para **Presionar cualquier tecla para continuar**. Presiona cualquier tecla para cerrar la ventana de línea de comandos. La incorporación puede tardar un minuto en finalizar.

1. Abre el menú Inicio y busca `Access work or school`. Selecciona **Acceder a profesional o educativa** en **Mejor coincidencia**.

1. En la ventana **Acceder a profesional o educativa** para **Agregar una cuenta profesional o educativa**, selecciona **Conectar**.

1. En el cuadro de diálogo **Configurar una cuenta profesional o educativa**, selecciona el vínculo **Conectar este dispositivo a Microsoft Entra ID** e inicia sesión como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (donde ZZZZZZ es el id. de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de Joni se estableció en un ejercicio anterior.

1. En el cuadro de diálogo**Asegúrate de que se trata de tu organización**, revisa la dirección URL del inquilino y selecciona **Conectar**.  

1. Una vez que el dispositivo se haya conectado, selecciona **Listo** en **¡Está todo listo!** pantalla.

1. Reinicia la VM Cliente 2 (SC-401-CL2).

1. Vuelve a iniciar sesión en la VM Cliente 1 (SC-401-CL1).

1. La ventana Microsoft Purview todavía debe estar abierta en la página **Dispositivos**. Actualiza esta página y comprueba que el dispositivo se ha incorporado correctamente.

Has incorporado correctamente el dispositivo y lo has unido a Microsoft Entra ID. Ahora se puede proteger mediante directivas DLP de punto de conexión.

## Tarea 2: Creación de una directiva DLP de punto de conexión

En esta tarea, crearás una directiva DLP que bloquea la transferencia de información confidencial a unidades USB. Esto ayuda a reducir el riesgo de que los datos salgan del sitio sin autorización.

1. Inicia sesión en la máquina virtual Client 1 (SC-401-CL1) como la cuenta SC-401-cl1\admin.

1. Todavía deberías estar en la página **Dispositivos** del Microsoft Purview Portal, con la sesión iniciada como Joni Sherman.

1. En el Microsoft Purview Portal, selecciona **Soluciones** > **Prevención de pérdida de datos**.

1. En el panel de navegación izquierdo, selecciona **Directivas** y, a continuación, selecciona **+ Crear directiva**.

1. En la página **Empezar con una plantilla o crear una directiva personalizada**, selecciona **Personalizado** y **Directiva personalizada** y luego selecciona **Siguiente**.

1. En la página **Introducir el nombre de la directiva DLP** escribe:

    - **Nombre**: `Block USB transfers`
    - **Descripción**: `Prevent transferring sensitive data to USB devices.`

1. En la página **Asignar unidades de administración**, selecciona **Siguiente**.

1. En la página **Elegir ubicaciones para aplicar la directiva**, asegúrate de que solo está seleccionada la ubicación **Dispositivos**. Si cualquier otra ubicación está seleccionada, asegúrate de que están deseleccionadas y, a continuación, selecciona **Siguiente**.

1. En la página **Definir la configuración de directiva**, selecciona **Crear o personalizar reglas DLP avanzadas** y, a continuación, selecciona **Siguiente**.

1. En **Personalizar reglas avanzadas de DLP**, selecciona **+ Crear regla**.

1. En la página **Crear regla**, escribe:

    - **Nombre**: `USB transfer rule`
    - **Descripción**: `Block USB transfers of sensitive data.`

1. En **Condiciones**, selecciona **+ Agregar condición** y, a continuación, selecciona **Contenido incluye**.

1. En la nueva sección **El contenido incluye**:
    - Selecciona **Agregar** > **Tipos de información confidencial**.
    - En la página **Tipos de información confidencial**, busca estos tipos de información confidencial:
       - `Credit Card Number`
       - `U.S. Social Security Number (SSN)`
       - `U.S. Driver's License Number`
       - `Contoso Employee IDs`

1. En **Acciones**, selecciona **+ Agregar una acción** > **Auditar o restringir actividades en dispositivos**.

1. En la nueva sección **Auditar o restringir actividades en dispositivos**:
    - En la sección **Actividades de archivo para todas las aplicaciones**, asegúrate de que la opción **Copiar en un dispositivo USB extraíble** está seleccionada.
    - Selecciona la lista desplegable situada a la izquierda de **Copiar en un dispositivo USB extraíble** para cambiar la acción de **Solo auditoría** a **Bloquear**.

1. En **Notificaciones de usuario**:
    - **Activa** la alternancia de **Usar notificaciones para informar a los usuarios y ayudar a educarles sobre el uso apropiado de la información confidencial.**
    - Activa la casilla **Mostrar a los usuarios una notificación de sugerencia de directiva cuando una actividad esté restringida**.

1. Selecciona **Guardar** en la parte inferior del control flotante de **Crear regla**.

1. Vuelve a la página **Personalizar reglas DLP avanzadas** y selecciona **Siguiente**.

1. En la página **Modo de directiva**, selecciona **Ejecutar la directiva en modo de simulación**.
   - Active la casilla **Mostrar sugerencias de directiva mientras está en modo de simulación**.
   - Además, activa la casilla **Activar la directiva si no se edita en un plazo de quince días después de la simulación**.

1. Seleccione **Siguiente**.

1. En la página **Revisar y finalizar**, revisa la configuración y, a continuación, selecciona **Enviar** para crear la directiva.

1. Una vez creada la directiva, selecciona **Listo** en la página **Nueva directiva creada**.

Has creado correctamente una directiva DLP en modo de simulación que bloquea las transferencias USB de datos confidenciales. Si la directiva no se edita, se activará automáticamente después de 15 días.

## Tarea 3: Configuración de las opciones de DLP del punto de conexión

En esta tarea, ajustarás la configuración de DLP del punto de conexión excluyendo una carpeta local, estableciendo restricciones de explorador y bloqueando un dominio en la nube.

1. Todavía deberías tener la sesión iniciada en la VM Cliente 1 (SC-401-CL1) como la cuenta **SC-401-cl1\admin** y deberías tener la sesión iniciada en Microsoft 365 como **Joni Sherman**.

1. En Microsoft Purview, en el panel de navegación izquierdo, selecciona **Configuración ** > **Prevención de pérdida de datos**.

1. La página **Configuración de prevención de pérdida de datos** debe abrirse en **Configuración de DLP del punto de conexión**.

1. En la página **Configuración de DLP de punto de conexión**, expande **Exclusiones de ruta de acceso de archivo para Windows** y, a continuación, selecciona **+ Agregar exclusión de ruta de acceso de archivo**.

1. En la página de control flotante **Excluir estas rutas de acceso de archivo de dispositivos Windows** en el campo **Exclusión de ruta de acceso de archivo**, escribe `C:\FilePathExclusionTest` y, a continuación, selecciona el botón **+** situado a la derecha. Selecciona **Guardar** para guardar la entrada.

1. De nuevo en la página **Configuración de DLP del punto de conexión**, expande **Restricciones de explorador y dominio a datos confidenciales** y selecciona **+ Agregar o editar exploradores no permitidos**.

1. En la página de control flotante **Agregar exploradores no permitidos**, activa la casilla **Google Chrome** y selecciona **Guardar**.

1. De nuevo en la página **Configuración de DLP de punto de conexión**, selecciona la lista desplegable de **Dominios de servicio** y cámbiala de **Desactivado** a **Bloquear**.

1. En el cuadro de diálogo **Actualizar modo de aplicación en la nube**, selecciona **Sí** para activar el modo de bloqueo.

1. En **Dominios de servicio**, selecciona **+ Agregar dominio de servicio en la nube**.

1. En la página de control flotante **Agregar dominio de servicio en la nube** del campo **Dominio**, escribe `dropbox.com` y selecciona el icono (más)**+** para agregar la ruta de acceso. Selecciona **Guardar** para guardar esta configuración.

Has aplicado la configuración de DLP del punto de conexión personalizado que mejora el comportamiento de la directiva, incluidas las exclusiones, las restricciones del explorador y el bloqueo del acceso a dominios específicos.

## Tarea 4: Configuración de la extensión de Microsoft Purview

En esta tarea, instalarás la extensión de Microsoft Purview en Google Chrome para probar el comportamiento de la directiva DLP del punto de conexión en exploradores compatibles.

1. Abre el explorador Edge desde la barra de tareas.

1. Ve a la descarga de Google Chrome en **`https://chrome.google.com`**.

1. Selecciona **Descargar Chrome** y selecciona **Abrir archivo** en la notificación **Descargas** de **ChromeSetup.exe**.

1. Selecciona **Sí** en el cuadro de diálogo **Control de cuentas de usuario** para instalar el explorador Chrome.

1. Cuando finalice la instalación, en la pantalla **Iniciar sesión en Chrome**, selecciona **No, gracias** o **No iniciar sesión**.

1. Selecciona **Omitir** en la página **Establecer el explorador predeterminado**.

1. Cuando se abra la ventana del explorador Chrome recién instalado, ve a la **extensión de Microsoft Purview** en la **Chrome web Store** en:

   `https://chrome.google.com/webstore/detail/microsoft-purview-extensi/echcggldkblhodogklpincgchnpgcdco`

1. Confirma que estás en la página de la extensión correcta y selecciona **Agregar a Chrome**.

1. En la ventana **¿Agregar "Extensión de Microsoft Purview"?**, ventana, selecciona **Agregar extensión**.

1. Cierra la notificación de la extensión que se va a agregar a Chrome y, a continuación, ve a **`chrome://extensions`**.

1. Valida que la **extensión de Microsoft Purview** esté visible y activada.

1. Cierra la ventana del explorador de Chrome.

Has instalado Chrome y has agregado la extensión de Microsoft Purview correctamente. El dispositivo ahora admite el cumplimiento de directivas DLP en Edge y Chrome.
