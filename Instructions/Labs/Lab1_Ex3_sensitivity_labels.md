---
lab:
  title: 'Ejercicio 3: Creación y administración de las etiquetas de confidencialidad'
  module: Module 1 - Implement Information Protection
---

# Laboratorio 1: Ejercicio 3: Creación y administración de etiquetas de confidencialidad

Joni Sherman, la administradora de seguridad de la información de Contoso Ltd., está implementando una estrategia de etiquetado de confidencialidad para ayudar a proteger la información confidencial en todos los departamentos. Como parte de este trabajo, configura el etiquetado manual y automático, las subetiquetas y las opciones de cifrado, incluida la compatibilidad con el cifrado de doble clave (DKE) y la integración con Microsoft Defender for Cloud Apps.

**Tareas:**

1. Habilitación de la compatibilidad con etiquetas de confidencialidad
1. Crear una etiqueta de confidencialidad.
1. Crear una subetiqueta
1. Publicación de las etiquetas de confidencialidad
1. Configuración del etiquetado automático
1. Creación y publicación de una etiqueta DKE para contenido altamente confidencial
1. Habilitación de la integración de Microsoft Purview en Defender for Cloud Apps
1. Creación de una directiva de archivos para etiquetar automáticamente archivos compartidos externamente

## Tarea 1: Habilitación de la compatibilidad con etiquetas de confidencialidad

En esta tarea, habilitarás la coautoría para etiquetas de confidencialidad, que también permite etiquetas de confidencialidad para archivos en SharePoint y OneDrive.

1. Todavía deberías estar conectado en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin** y estar conectado en Microsoft Purview como Joni Sherman.

1. Abre **Microsoft Edge** y ve a `https://purview.microsoft.com`.

1. En el panel de navegación izquierdo, selecciona **Configuración** > **Information Protection**.

1. En **Configuración de Information Protection**, asegúrate de que estás en la pestaña **Coautoría de archivos con etiquetas de confidencialidad**.

1. Activa la casilla **Activar la coautoría de archivos con etiquetas de confidencialidad**.

1. Selecciona **Aplicar** en la parte inferior de la pantalla.

Has habilitado correctamente la compatibilidad con las etiquetas de confidencialidad para archivos de SharePoint y OneDrive.

## Tarea 2: Creación de una etiqueta de confidencialidad

En esta tarea, crearás una etiqueta de confidencialidad primaria para el contenido interno. Esta etiqueta incluye la configuración básica y actúa como una etiqueta primaria para subetiquetas específicas del departamento.

1. Todavía debes tener la sesión iniciada en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-CL1\admin**.

1. En **Microsoft Edge**, ve a `https://purview.microsoft.com`.

1. En el Portal de Microsoft Purview, selecciona **Soluciones** en la barra lateral izquierda y, después, selecciona **Information Protection**.

1. En la página **Microsoft Information Protection**, en la barra lateral izquierda, y selecciona **Tipos de información confidencial**.

1. En la página **Etiquetas de confidencialidad**, selecciona **+ Crear una etiqueta**.

1. Se iniciará la configuración **Nueva etiqueta de confidencialidad**. En **Proporcionar detalles básicos de esta etiqueta**, escribe:

    - **Nombre**: `Internal`
    - **Nombre para mostrar**: `Internal`
    - **Descripción para los usuarios**: `Internal sensitivity label.`
    - **Descripción para los administradores**: `Internal sensitivity label for Contoso.`

1. Seleccione **Siguiente**.

1. En la página **Definir el ámbito de esta etiqueta**, selecciona **Archivos** y **Correos electrónicos**. Si la casilla **Reuniones** está activada, asegúrate de desactivarla.

1. Seleccione **Siguiente**.

1. En la página **Elegir la configuración de protección para los elementos etiquetados**, selecciona **Siguiente**.

1. En la página **Etiquetado automático de archivos y correos electrónicos**, selecciona **Siguiente**.

1. En la página **Definir la configuración de protección para grupos y sitios**, selecciona **Siguiente**.

1. En la página **Revisar la configuración y finalizar**, selecciona **Crear etiqueta**.

1. En la página **Se creó la etiqueta de confidencialidad**, selecciona **No crear una directiva aún** y, a continuación, selecciona **Listo**.

Has creado una etiqueta de confidencialidad para su uso interno. Esta etiqueta actuará como una etiqueta primaria para subetiquetas más específicas que se usan en distintos departamentos.

## Tarea 3: Creación de una subetiqueta

Ahora que tienes una etiqueta base, crearás una subetiqueta para documentos relacionados con RR. HH. Esta subetiqueta incluye una configuración de protección y marcas de contenido visibles para admitir las prácticas internas de control de datos del departamento de RR. HH.

1. En la página **Etiquetas de confidencialidad**, busca la etiqueta de confidencialidad **interna** recién creada. Selecciona los puntos suspensivos verticales (**...**) situados junto a ella y selecciona **+ Crear subetiqueta** en el menú desplegable.

    ![Captura de pantalla que muestra el menú Acción para crear una subetiqueta para una etiqueta de confidencialidad.](../Media/create-sublabel-button.png)

1. Se iniciará el Asistente para **Nueva etiqueta de confidencialidad**. En la página **Proporcionar detalles básicos de esta etiqueta**, escribe:

   - **Nombre**: `Employee data (HR)`
   - **Nombre para mostrar**: `Employee data (HR)`
   - **Descripción para los usuarios**: `This HR label is the default label for all specified documents in the HR Department.`
   - **Descripción para los administradores**: `This label is created in consultation with Ms. Jones (Head of HR department). Contact her if you need to change the label settings.`

1. Seleccione **Siguiente**.

1. En la página **Definir el ámbito de esta etiqueta**, selecciona **Archivos** y **Correos electrónicos**. Si la casilla **Reuniones** está activada, asegúrate de desactivarla.

1. Seleccione **Siguiente**.

1. En la página **Elegir la configuración de protección para los elementos etiquetados**, selecciona la opción **Control de acceso** y **Aplicar marcas de contenido** y, después, selecciona **Siguiente**.

1. En la página **Control de acceso**, selecciona **Configurar configuración de control de acceso**.

1. Configura la configuración de cifrado con estas opciones:

   - **¿Asignar ya permisos o permitir que los usuarios decidan?**: Asignar permisos ahora
   - **Acceso del usuario al contenido expira**: Nunca.
   - **Permitir acceso sin conexión**: Solo durante un número de días
   - **Los usuarios tienen acceso sin conexión al contenido durante estos días**: 15
   - Selecciona el vínculo **Asignar permisos**. En el panel de control flotante **Asignar permisos**, selecciona **+ Agregar cualquier usuario autenticado** y, después, selecciona **Guardar** para aplicar esta configuración.

1. En la página **Control de acceso**, selecciona **Siguiente**.

1. En la página **Marcado de contenido**, selecciona el control de alternancia para habilitar el **Marcado de contenido**.

1. Para cada uno de los siguientes tipos de marcado, activa la casilla y, después, selecciona el icono de edición para escribir el texto:

   |Tipo de marcado|Texto|
   |:---|:---|
   |Agregar una marca de agua|`INTERNAL USE ONLY`|
   |Agregar un encabezado|`Internal Document`|
   |Agregar un pie de página|`Contoso Confidential`|

1. Seleccione **Siguiente**.

1. En la página **Etiquetado automático de archivos y correos electrónicos**, selecciona **Siguiente**.

1. En la página **Definir la configuración de protección para grupos y sitios**, selecciona **Siguiente**.

1. En la página **Revisar la configuración y finalizar**, selecciona **Crear etiqueta**.

1. En la página **Se creó la etiqueta de confidencialidad**, selecciona **No crear una directiva aún** y, a continuación, selecciona **Listo**.

Has creado una subetiqueta para aplicar el cifrado y las marcas de contenido a los documentos de RR. HH. Esta etiqueta ayuda a garantizar que los datos de RR. HH. solo sean accesibles para los usuarios autenticados y se puedan identificar mediante marcas visuales.

## Tarea 4: Publicación de etiquetas de confidencialidad

Ahora publicarás la etiqueta de confidencialidad Interna y de RR. HH. para que las etiquetas de confidencialidad publicadas estén disponibles para que los usuarios de RR. HH. las apliquen a sus documentos de RR. HH.

1. Todavía deberías estar conectado en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-cl1\admin** y debería estar conectado en Microsoft Purview como **Joni Sherman**.

1. En **Microsoft Edge**, debe estar abierta la pestaña del Portal de Microsoft Purview. Si no es así, ve a **`https://purview.microsoft.com`** > **Soluciones** > **Information Protection** > **Etiquetas de confidencialidad**.

1. En la página **Etiquetas de confidencialidad**, selecciona **Publicar etiquetas**.

1. Se iniciará la configuración de publicar etiquetas de confidencialidad.

1. En la página **Elegir etiquetas de confidencialidad para publicar**, selecciona el vínculo **Elegir etiquetas de confidencialidad para publicar**.

1. En el panel flotante **Etiquetas de confidencialidad para publicar**, activa las casillas **Datos internos** y **Datos internos/de empleados (RR. HH.)** y, después, selecciona **Agregar** en la parte inferior de la página flotante.

1. Vuelve a la página **Elegir etiquetas de confidencialidad para publicar** y selecciona **Siguiente**.

1. En la página **Asignar unidades de administración**, selecciona **Siguiente**

1. En la página **Publicar en usuarios y grupos**, selecciona **Siguiente**.

1. En la página **Configuración de directivas** selecciona **Siguiente**.

1. En **Configuración predeterminada de documentos**, selecciona **Siguiente**.

1. En **Configuración predeterminada para correos electrónicos**, selecciona **Siguiente**.

1. En **Configuración predeterminada para reuniones y eventos de calendario**, selecciona **Siguiente**.

1. En la página **Configuración predeterminada del contenido de Fabric y Power BI**, selecciona **Siguiente**.

1. En la página **Asignar nombre a la directiva** escribe:

   - **Nombre**: `Internal HR employee data`

   - **Escribir una descripción para la directiva de etiqueta de confidencialidad**: `This HR label is to be applied to internal HR employee data.`

1. Selecciona **Siguiente**.

1. En la página **Revisar y finalizar**, selecciona **Enviar**.

1. En **Nueva directiva creada**, selecciona **Listo** para finalizar la publicación de la directiva de etiquetas.

Has publicado correctamente las etiquetas de confidencialidad internas y de RR. HH. Ten en cuenta que los cambios pueden tardar hasta 24 horas en replicarse en todos los usuarios y servicios.

## Tarea 5: Configuración del etiquetado automático

En esta tarea, crearás una etiqueta de confidencialidad para los datos financieros y la configurarás para que se aplique automáticamente al contenido que contiene identificadores financieros específicos, como números de tarjeta de crédito e información de enrutamiento bancario.

1. Todavía deberías estar conectado en la máquina virtual Cliente 1 (SC-401-CL1) como la cuenta **SC-401-cl1\admin**.

1. En **Microsoft Edge**, ve a `https://purview.microsoft.com` e inicia sesión en Microsoft Purview Portal como **Joni Sherman**.

1. En Microsoft Purview Portal, selecciona **Soluciones** > **Information Protection** > **Etiquetas de confidencialidad**.

1. En la página **Etiquetas de confidencialidad**, busca la etiqueta de confidencialidad **interna**. Selecciona los puntos suspensivos verticales (**...**) y selecciona **+ Crear subetiqueta** en el menú desplegable.

1. En la página **Proporcionar detalles básicos de esta etiqueta**, escribe:

   |Detalles|Texto|
   |---|---|
   |**Nombre**|`Financial Data`|
   |**Nombre para mostrar**|`Financial Data`|
   |**Descripción para los usuarios**|`This content contains financial data that must be labeled and protected.`|
   |**Descripción para los administradores**|`This label is used for content that includes sensitive financial identifiers.`|

1. Seleccione **Siguiente**.

1. En la página **Definir el ámbito de esta etiqueta**, selecciona **Archivos** y **Correos electrónicos**. Si la casilla **Reuniones** está activada, asegúrate de desactivarla.

1. Seleccione **Siguiente**.

1. En la página **Elegir la configuración de protección para los elementos etiquetados**, selecciona **Siguiente**.

1. En la página **Etiquetado automático de archivos y correos electrónicos**, activa **Etiquetado automático para archivos y correos electrónicos**.

1. En la sección **Detectar contenido que coincida con estas condiciones**, selecciona **+ Agregar condición** > **Contenido incluye**.

1. En la sección **El contenido incluye**, selecciona **Agregar** > **Tipos de información confidencial**.

1. En la página flotante **Tipos de información confidencial**, busca y selecciona estos tipos de información confidencial:

   - `Credit Card Number`
   - `ABA Routing Number`
   - `SWIFT Code`

1. Seleccione **Agregar**.

1. Vuelve a la página **Etiquetado automático de archivos y correos electrónicos** y selecciona **Siguiente**.

1. En la página **Definir la configuración de protección para grupos y sitios**, selecciona **Siguiente**.

1. En la página **Revisar la configuración y finalizar**, selecciona **Crear etiqueta**.

1. En la página **Se creó la etiqueta de confidencialidad**, selecciona **Aplicar automáticamente la etiqueta al contenido confidencial** y, después, selecciona **Listo**.

1. En la página flotante **Crear directiva de etiquetado automático**, selecciona **Revisar directiva**.

1. En la página **Nombre de la directiva de etiquetado automático**, deja el valor predeterminado y selecciona **Siguiente**.

1. En la página **Elegir una etiqueta para aplicar automáticamente**, revisa para asegurarte de que está seleccionada la etiqueta _Datos internos o financieros_ y, después, selecciona **Siguiente**.

1. En la página **Asignar unidades de administración**, selecciona **Siguiente**.

1. En la página **Elegir ubicaciones en las que deseas aplicar la etiqueta**, selecciona las opciones para:

   - Correo electrónico de Exchange
   - Sitios de SharePoint
   - Cuentas de OneDrive

1. Seleccione **Siguiente**.

1. En la página **Configurar reglas comunes o avanzadas**, deja activado el valor predeterminado **Reglas comunes** y selecciona **Siguiente**.

1. En la página **Definir reglas para contenido en todas las ubicaciones**, expande las reglas de _Reglas de datos financieros_ para asegurarte de que se definen las reglas esperadas y selecciona **Siguiente**.

1. En la página **Configuración para correos electrónicos**, selecciona **Siguiente**.

1. En la página **Decidir si deseas probar la directiva ahora o más adelante**, selecciona **Ejecutar directiva en modo de simulación** y activa la casilla **Activar automáticamente la directiva si no se modifica después de 7 días en la simulación**.

1. Seleccione **Siguiente**.

1. En la página **Revisar y finalizar**, selecciona **Crear directiva**.

1. En la página **Se creó la directiva de etiquetado automático**, selecciona **Listo**.

Has creado correctamente una etiqueta de confidencialidad para los datos financieros. Además, has configurado una directiva de etiquetado automático para detectar y etiquetar el contenido que contiene información financiera confidencial.

## Tarea 6: Creación y publicación de una etiqueta DKE para contenido confidencial

En esta tarea, crearás una subetiqueta en la etiqueta Interna. Esta subetiqueta usará el cifrado de doble clave (DKE) y la marca de agua dinámica para proteger solo el contenido confidencial al que accede el departamento legal. También configurarás una directiva de etiquetas que requiera una justificación para bajar de categoría la etiqueta.

1. Todavía deberías estar conectado en la máquina virtual Cliente 1 (SC-401-CL1) como la cuenta **SC-401-cl1\admin**.

1. En **Microsoft Edge**, ve a `https://purview.microsoft.com` e inicia sesión en Microsoft Purview Portal como **Joni Sherman**.

1. En Microsoft Purview Portal, selecciona **Soluciones** > **Information Protection** > **Etiquetas de confidencialidad**.

1. En la página **Etiquetas de confidencialidad**, busca la etiqueta de confidencialidad **interna**. Selecciona los puntos suspensivos verticales (**...**) y selecciona **+ Crear subetiqueta** en el menú desplegable.

1. En la página **Proporcionar detalles básicos de esta etiqueta**, escribe:

   |Detalles|Texto|
   |---|---|
   |**Nombre**|`Highly Confidential - Legal`|
   |**Nombre para mostrar**|`Highly Confidential - Legal`|
   |**Descripción para los usuarios**|`Use this label for highly sensitive content that must be encrypted using Double Key Encryption.`|
   |**Descripción para los administradores**|`Label configured with DKE and dynamic watermarking for highly sensitive content.`|

1. Seleccione **Siguiente**.

1. En la página **Definir el ámbito de esta etiqueta**, selecciona **Archivos** y **Correos electrónicos**. Si la casilla **Reuniones** está activada, asegúrate de desactivarla.

1. En **Elegir la configuración de protección para los tipos de elementos que seleccionaste**, activa la casilla **Control del acceso** y, después, selecciona **Siguiente**.

1. En la página **Control de acceso**, selecciona **Configurar configuración de control de acceso**.

1. Configura la configuración de cifrado con estas opciones:

   - **¿Asignar ya permisos o permitir que los usuarios decidan?**: Asignar permisos ahora

   - **El acceso de usuario al contenido expira**: el número de días después de aplicar la etiqueta

   - **El acceso expira durante estos días después de aplicar la etiqueta**: 5

   - **Permitir el acceso sin conexión**: nunca

   - Selecciona el vínculo **Asignar permisos**. En el panel flotante **Asignar permisos**, selecciona **+ Agregar usuarios o grupos**.

   - En la página flotante **Agregar usuarios o grupos**, busca y selecciona `Legal Team` y `Joni Sherman`, y selecciona **Agregar**.

   - En la página **Asignar permisos**, selecciona **Guardar**.

1. De nuevo en la página **Control de acceso**, activa la casilla **Usar marca de agua dinámica** y selecciona **Personalizar texto (opcional)**.

1. En la página **Agregar texto personalizado a la marca de agua (opcional)**, escribe `Confidential` y selecciona los vínculos de **UPN** y **marca de tiempo**.

1. Selecciona **Guardar** en la parte inferior de la página flotante.

1. De nuevo en la página **Control de acceso**, activa la casilla **Usar cifrado de doble clave** y escribe `https://testingdke1.azurewebsites.net/Test` como dirección URL para el servicio de cifrado de doble clave.

1. Seleccione **Siguiente**.

1. En la página **Etiquetado automático de archivos y correos electrónicos**, selecciona **Siguiente**.

1. En la página **Definir la configuración de protección para grupos y sitios**, selecciona **Siguiente**.

1. En la página **Revisar la configuración y finalizar**, selecciona **Crear etiqueta**.

1. En la página **Se creó la etiqueta de confidencialidad**, selecciona **Publicar etiqueta en las aplicaciones de los usuarios** y, después, selecciona **Listo**.

1. En la página flotante **Publicar etiqueta**, selecciona **Crear nueva directiva de etiquetas**.

1. En la página **Elegir etiquetas de confidencialidad para publicar**, selecciona **Elegir etiquetas de confidencialidad para publicar** y agrega la etiqueta **Altamente confidencial** y la subetiqueta **Highly Confidential - Legal** y, a continuación, selecciona **Agregar**.

1. Seleccione **Siguiente**.

1. En la página **Asignar unidades de administración**, selecciona **Siguiente**.

1. En la página **Publicar en usuarios y grupos**, deja el valor predeterminado seleccionado y, después, selecciona **Siguiente**.

1. En la página **Configuración de directiva**, activa la casilla **Los usuarios deben proporcionar una justificación para quitar una etiqueta o reducir su clasificación** y, después, selecciona **Siguiente**.

1. En la página **Configuración predeterminada de documentos**, selecciona **Siguiente**.

1. En la página **Configuración predeterminada para correos electrónicos**, selecciona **Siguiente**.

1. En la página **Configuración predeterminada para reuniones y eventos de calendario**, selecciona **Siguiente**.

1. En la página **Configuración predeterminada del contenido de Fabric y Power BI**, selecciona **Siguiente**.

1. En la página **Asignar nombre a la directiva** escribe:

   - **Nombre**: `Highly Confidential - Legal`

   - **Descripción**: `Enables manual use of the DKE label for highly confidential content accessible by Legal.`

1. Seleccione **Siguiente**.

1. En la página **Revisar y finalizar**, selecciona **Enviar**.

1. En la página **Nueva directiva creada**, selecciona **Listo**.

Has creado y publicado correctamente una subetiqueta con cifrado de doble clave con una marca de agua dinámica. Esta etiqueta proporciona una protección segura para contenido altamente confidencial y aplica el acceso restringido y la justificación de los cambios de clasificación.

## Tarea 7: Habilitación de la integración de Microsoft Purview en Defender for Cloud Apps

En esta tarea, habilitarás la integración de Microsoft Purview en Microsoft Defender for Cloud Apps. Esto permite a Defender examinar nuevos archivos para detectar etiquetas de confidencialidad de Microsoft Purview, inspeccionar el contenido en función de esas etiquetas y supervisar los archivos para poder aplicar políticas de archivos.

1. Todavía deberías estar conectado en la máquina virtual Client 1 (SC-401-CL1) como **SC-401-CL1\admin** tener la sesión iniciada como Joni Sherman.

1. Abre **Microsoft Edge** y ve a **Microsoft Defender**; para ello, ve a `https://security.microsoft.com`.

1. En el panel de navegación izquierdo, selecciona **Configuración** y, después, selecciona **Cloud Apps**.

1. En la sección **Information Protection** del panel izquierdo, selecciona **Microsoft Information Protection**.

1. En la página **Microsoft Information Protection**, activa ambas casillas disponibles en la página.

    ![Captura de pantalla que muestra ambas casillas habilitadas para Information Protection en el portal de Defender.](../Media/defender-information-protection-settings.png)

   - **Examinar automáticamente los nuevos archivos en busca de etiquetas de confidencialidad y advertencias de inspección de contenido de Microsoft Information Protection**

      Permite a Defender for Cloud Apps examinar automáticamente los archivos nuevos o modificados en busca de etiquetas de confidencialidad y advertencias de inspección de contenido de Microsoft Purview.

   - **Examinar solo archivos en busca de etiquetas de confidencialidad de Microsoft Information Protection y advertencias de inspección de contenido de este inquilino**

      Limita el examen de etiquetas y advertencias creadas en tu propia organización. Se omitirán las etiquetas aplicadas por inquilinos externos.

1. Seleccione **Guardar** para aplicar la configuración.

1. En la sección **Information Protection** del panel izquierdo, selecciona **Archivos**.

1. En la página **Archivos**, selecciona el vínculo **Habilitar supervisión de archivos**.

1. Seleccione **Guardar** para aplicar la configuración.

Has habilitado Defender for Cloud Apps para examinar archivos de etiquetas de confidencialidad y supervisar archivos para que las directivas de archivo puedan evaluar y aplicar acciones de gobernanza.

## Tarea 8: Creación de una directiva de archivos para etiquetar automáticamente archivos compartidos externamente

Ahora que el examen de etiquetas está habilitado, crearás una directiva de archivos que aplique la etiqueta de confidencialidad **Altamente confidencial - Project - Falcon** a los archivos de las carpetas Mark 8 Project que se comparten fuera de la organización. Esta directiva se clasifica como DLP porque protege los datos confidenciales de la exposición no deseada.

1. En **Microsoft Defender**, ve a **Cloud Apps** > **Directivas** > **Administración de directivas**.

1. Selecciona la pestaña **Information Protection** y, después, selecciona **Crear directiva** > **Directiva de archivos**.

    ![Captura de pantalla que muestra dónde navegar para crear una directiva de archivos en Microsoft Defender.](../Media/file-policy-defender.png)

1. En la página **Crear directiva de archivos**, configura:

   - **Nombre de directiva**: `Auto-label external sharing for Project Falcon files`

   - **Gravedad de directiva**: **alta**

   - **Categoría**: **DLP**

   - **Aplicar a**: **carpetas seleccionadas**

      - Selecciona **Agregar carpetas** y busca `Project` en el campo **Nombre de archivo**.

      - Activa la casilla de las carpetas **Mark 8 Project Team Notebook** y **Mark 8 Project Team** de SharePoint.

      - Selecciona **Listo** para cerrar la ventana **Seleccionar una carpeta**.

   - En la sección **Archivos que coinciden con toda la siguiente sección**:

      - Para el primer filtro, configura los elementos desplegables en: **El nivel de acceso es igual al externo**

      - Para el segundo filtro, configura los elementos desplegables en: **Última modificación después de (fecha)** y usa la fecha actual.

          ![Captura de pantalla con la configuración del filtro en Defender.](../Media/configure-file-policy-filter.png)

   - En **Acciones de gobernanza**, expande **Microsoft OneDrive para la Empresa**:

      - Activa la casilla **Aplicar etiqueta de confidencialidad**

      - En el elemento desplegable, selecciona **Altamente confidencial-Project - Falcon**

   - Repite el mismo proceso para **Microsoft SharePoint Online**

      - Activa la casilla **Aplicar etiqueta de confidencialidad**

      - Selecciona **Altamente confidencial-Project - Falcon** en el elemento desplegable

1. Selecciona **Crear** para terminar de crear la directiva de archivos.

Has creado una directiva de archivos que aplica una etiqueta de confidencialidad de alto nivel a los archivos compartidos externamente ubicados en carpetas del proyecto Mark 8 en SharePoint y OneDrive. Una vez se detecta un archivo coincidente, Defender for Cloud Apps aplicará automáticamente la etiqueta.
