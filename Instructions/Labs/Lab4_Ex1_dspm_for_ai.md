---
lab:
  title: 'Ejercicio 1: Protección de datos en entornos de IA'
  module: Module 4 - Protect data in AI environments
---

## Inquilinos de WWL: términos de uso

Si se te proporciona un inquilino porque estás realizando un curso dirigido por un instructor, ten en cuenta que ese inquilino está disponible únicamente como apoyo para los laboratorios prácticos del curso.

Los inquilinos no deben compartirse ni usarse para otros fines que no sean los de los laboratorios prácticos. El inquilino usado en este curso es un inquilino de prueba y no se puede usar ni tener acceso a él después de que la clase haya terminado y no es apto para la extensión.

Los inquilinos no se deben convertir a suscripciones de pago. Los inquilinos obtenidos como parte de este curso siguen siendo propiedad de Microsoft Corporation y nos reservamos el derecho de acceso y recuperación en cualquier momento.

# Laboratorio 4: Ejercicio 1: Protección de datos en entornos de IA

Eres Joni Sherman, la administradora de seguridad de la información de Contoso Ltd. A medida que las herramientas de IA como Microsoft Copilot se integran cada vez más en los flujos de trabajo diarios, a tu equipo se le ha pedido que evalúe y mejore las protecciones en torno a la información confidencial. En este laboratorio, explorarás cómo Microsoft Purview DSPM para IA puede ayudar a proteger las interacciones de datos con herramientas de IA mediante la aplicación de directivas, la detección de riesgos y las evaluaciones de exposición.

**Tareas:**

1. Uso de DSPM para IA para crear una directiva DLP para sitios de IA generativa
1. Creación de una directiva de riesgos internos para detectar interacciones de IA arriesgadas
1. (Opcional) Impedir que Copilot acceda al contenido etiquetado
1. Ejecución de una evaluación de datos para detectar contenido sin etiquetar

## Tarea 1: Uso de DSPM para IA para crear una directiva DLP para sitios de IA generativa

Para reducir el riesgo de pérdida de datos a través de asistentes de IA, crearás primero una directiva DLP mediante la recomendación Fortify la seguridad de datos. Esta directiva usa la protección adaptativa para restringir el pegado o la carga de información confidencial en herramientas de IA como ChatGPT y Copilot en Edge, Chrome y Firefox.

1. Inicia sesión en la máquina virtual Client 1 (SC-401-CL1) como la cuenta **SC-401-cl1\admin**.

1. En **Microsoft Edge**, ve a **`https://purview.microsoft.com`** e inicia sesión como **Joni Sherman** `JoniS@WWLxZZZZZZ.onmicrosoft.com` (ZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio).

1. En Microsoft Purview, ve a DSPM para IA seleccionando **Soluciones** > **DSPM para IA** > **Recomendaciones**

1. Selecciona la recomendación **Fortify la seguridad de datos**.

1. En la página flotante **Seguridad de datos para IA**, revisa el resumen y selecciona **Crear directivas**. Esto crea una directiva DLP configurada previamente destinada a sitios de IA generativa.

1. Una vez creada la directiva, selecciona **Ver directiva**.

1. En la sección **Detalles de directiva**, selecciona **Editar directiva en la solución** para abrir la solución **Prevención de pérdida de datos** en Microsoft Purview.

1. En la página **Directivas**, busca y selecciona la directiva **DSPM para IA: Bloquear información confidencial de sitios de IA**.

1. En el control flotante, selecciona **Ver simulación**.

1. En el panel de simulación, selecciona **Editar la directiva**.

1. Seleccione **Siguiente** hasta llegar a la página **Elegir dónde aplicar la directiva**. Confirma que la directiva se limita a **Dispositivos**.

1. Seleccione **Siguiente**.

1. En la página **Personalizar reglas DLP avanzadas**, selecciona el icono de lápiz situado junto a **Bloquear con invalidación para usuarios de riesgo elevado** para ver la regla.

1. Revisa la configuración de la regla creada por DSPM para IA:
   - En **Condiciones**, observa los tipos de información confidencial incluidos y que la regla usa la **protección adaptativa** en función del riesgo elevado.
   - En **Acciones**, confirma que el **Dominio de servicio y las actividades del explorador** están en **Bloquear con invalidación** para **Sitios web de IA generativa**.

1. Selecciona **Cancelar** para salir del editor de reglas sin realizar cambios.

1. De nuevo en la página **Personalizar reglas DLP avanzadas**, seleccione **Siguiente**.

1. En la página **Modo de directiva**, selecciona **Activar la directiva si no se edita en un plazo de quince días después de la simulación** y, después, selecciona **Siguiente**.

1. En la página **Revisar y finalizar**, selecciona **Enviar** y, después, **Listo**.

Has creado una directiva que impide que los usuarios de alto riesgo compartan información confidencial en sitios de IA generativa y has confirmado la configuración de directivas establecida por DSPM para IA.

## Tarea 2: Creación de una directiva de riesgo interno para detectar interacciones de IA arriesgadas

A continuación, crearás una directiva que ayuda a detectar el comportamiento de indicaciones de riesgo en Copilot.

1. En Microsoft Purview, ve a **DSPM para IA** seleccionando **Soluciones** > **DSPM para IA** > **Recomendaciones.**

1. Selecciona la recomendación **Detectar interacciones de riesgo en aplicaciones de IA (versión preliminar).**

1. En la página flotante **Detectar interacciones de riesgo en aplicaciones de IA (versión preliminar),** revisa el resumen y selecciona **Crear directiva**.

1. Una vez creada la directiva, selecciona **Ver directiva**.

1. En la sección **Detalles de directiva**, selecciona **Editar directiva en la solución** para abrir el área **Administración de riesgos internos** de Microsoft Purview.

1. En la página **Directivas**, busca y selecciona la directiva **DSPM para IA: Detectar el uso de IA arriesgado**.

1. En el control flotante, selecciona **Editar directiva** para revisar la configuración de directivas completa.

1. En la página **Elegir una plantilla de política**, observa que la directiva usa la plantilla **Uso arriesgado de IA (versión preliminar)**.

1. Selecciona **Siguiente** hasta llegar a la página **Elegir evento desencadenante para esta directiva**.
Confirma que el evento desencadenante es **Cuenta de usuario eliminada de Microsoft Entra ID**, que indica posibles riesgos relacionados con la retirada que podrían preceder o seguir la actividad arriesgada de IA.

1. Seleccione **Siguiente**.

1. En la página **Indicadores**, expande las categorías de indicadores para revisar qué señales se seleccionan:

   - Explorado sitios web de IA generativa
   - Recibido una respuesta confidencial de Copilot
   - Introducido un aviso de riesgo en Copilot

1. Selecciona **Siguiente** hasta llegar a la página **Revisar y finalizar**, luego selecciona **Cancelar** para salir del editor sin realizar cambios.

Has creado una directiva que detecta interacciones de IA de riesgo, incluyendo las solicitudes y respuestas, para ayudar a identificar temprano los signos de comportamiento de los usuarios de riesgo.

## Tarea 3: (opcional) Bloqueo del acceso de Copilot al contenido etiquetado

Puedes reducir aún más el riesgo impidiendo que Copilot procese o responda con contenido protegido por etiquetas de confidencialidad.

1. En Microsoft Purview, ve a **DSPM para IA** seleccionando **Soluciones** > **DSPM para IA** > **Recomendaciones.**

1. Selecciona la recomendación denominada **Proteger la información confidencial a la que se hace referencia en Copilot y las respuestas del agente**.

1. Revisa las instrucciones que se proporcionan en esta recomendación.

1. Ve a **Soluciones** > **Prevención de pérdida de datos** > **Directivas**.

1. Selecciona **+ Crear directiva** y elige **Directiva personalizada**.

1. En la página **Introducir el nombre de la directiva DLP** escribe:

   - **Nombre**: `DLP - Block Copilot access to labeled content`
   - **Descripción**: `Prevents Microsoft 365 Copilot from processing or responding with content labeled using sensitivity labels.`

1. Seleccione **Siguiente** hasta llegar a la página **Elegir dónde aplicar la directiva**.

1. Selecciona **Microsoft 365 Copilot (versión preliminar)** como ámbito de directiva y, después, selecciona **Siguiente** hasta llegar a la página **Personalizar reglas DLP avanzadas**.

1. Selecciona **Crear regla** y configura:

   - **Nombre**: `Prevent Copilot from accessing labeled data`
   - En **Condiciones**, selecciona **Agregar condición** > **El contenido incluye** > **Etiquetas de confidencialidad**. Agrega estas etiquetas de confidencialidad:
     - `Internal`
     - `Confidential`
     - `Highly Confidential`
   - Seleccione **Agregar**.
   - En **Acciones**, selecciona **Agregar una acción** > **Impedir que Copilot procese contenido (versión preliminar)**
   - Selecciona **Guardar** en la parte inferior del control flotante de **Crear regla**.

1. De nuevo en la página **Personalizar reglas DLP avanzadas**, seleccione **Siguiente**.

1. En la página **Modo de directiva**, selecciona **Activar la directiva inmediatamente** y, después, selecciona **Siguiente**.

1. En la página **Revisar y finalizar**, selecciona **Enviar** y, después, selecciona **Listo** en la página **La directiva se ha creado**.

1. Vuelve a **Recomendaciones de DSPM para IA** seleccionando **Soluciones** > **DSPM para IA** > **Recomendaciones**.

1. Selecciona la recomendación **Proteger la información confidencial a los que se hace referencia en Copilot y en las respuestas del agente** y selecciona **Marcar como completado**.

Has creado una directiva DLP que impide que el contenido etiquetado se use en las indicaciones y respuestas de Copilot.

## Tarea 4: Ejecutar una evaluación de datos para detectar contenido sin etiquetar

Para comprender las posibles brechas en la cobertura de etiquetado, ejecutarás una evaluación de datos para identificar archivos sin etiquetas de confidencialidad a los que puede acceder Copilot.

1. En **DSPM para IA**, selecciona la recomendación denominada **Proteger la información confidencial a la que se hace referencia en las respuestas de Copilot y del agente**.

1. En el panel **Proteger la información confidencial a la que se hace referencia en las respuestas de Copilot y del agente**, revisa el resumen y selecciona **Ir a las evaluaciones**.

1. En la página **Evaluaciones de riesgos de datos** selecciona **Crear evaluación personalizada**

1. En la página **Detalles básicos**, escribe:

   - **Nombre**: `Unlabeled File Exposure Assessment`
   - **Descripción**: `Identifies files without sensitivity labels that may be exposed in Microsoft 365 Copilot responses and provides recommendations to reduce oversharing risks.`

1. Seleccione **Siguiente**.

1. En la página **Agregar usuarios**, selecciona **Todo** y, después, selecciona **Siguiente**.

1. En la página **Agregar orígenes de datos para evaluar**, deja seleccionada la ubicación predeterminada de **SharePoint** y, después, selecciona **Siguiente**.

1. En la página **Escáner de revisión y ejecución de evaluación de datos**, selecciona **Guardar y ejecutar**.

1. En la página **Evaluación de datos creada correctamente**, selecciona **Listo**.

Has usado DSPM para IA de Microsoft Purview para detectar riesgos relacionados con la IA, aplicar directivas y evaluar la exposición de la información confidencial, lo que ayudará a tu organización a usar la IA de forma segura.
