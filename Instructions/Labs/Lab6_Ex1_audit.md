---
lab:
  title: 'Ejercicio 1: Búsqueda en el registro de auditoría'
  module: Module 6 - Audit and search activity in Microsoft Purview
---

## Inquilinos de WWL: términos de uso

Si se te proporciona un inquilino porque estás realizando un curso dirigido por un instructor, ten en cuenta que ese inquilino está disponible únicamente como apoyo para los laboratorios prácticos del curso.

Los inquilinos no deben compartirse ni usarse para otros fines que no sean los de los laboratorios prácticos. El inquilino usado en este curso es un inquilino de prueba y no se puede usar ni tener acceso a él después de que la clase haya terminado y no es apto para la extensión.

Los inquilinos no se deben convertir a suscripciones de pago. Los inquilinos obtenidos como parte de este curso siguen siendo propiedad de Microsoft Corporation y nos reservamos el derecho de acceso y recuperación en cualquier momento.

# Laboratorio 6: Ejercicio 1: Búsqueda en el registro de auditoría

Eres Joni Sherman, la administradora de seguridad de la información de Contoso Ltd. Para reforzar la preparación para la investigación y el cumplimiento de la organización, se te ha pedido que uses Auditoría de Microsoft Purview para revisar los cambios de configuración de DLP y asegurarte de que los registros de auditoría de la actividad confidencial se conservan durante un período prolongado. Buscarás eventos de auditoría relacionados con las directivas DLP, exportarás los resultados para el análisis sin conexión y configurarás una directiva de retención de auditoría que conservará los registros clave en Exchange, SharePoint y la actividad del punto de conexión.

**Tareas:**

1. Búsqueda de actividad relacionada con DLP
1. Exportación de los resultados de la búsqueda en la auditoría
1. Creación de una directiva de retención de auditoría

## Tarea 1: Búsqueda de actividad relacionada con DLP

En esta tarea, usarás la solución Auditoría de Microsoft Purview para buscar eventos de auditoría recientes relacionados con las reglas y la directiva DLP.

1. En Microsoft Edge, ve a `https://purview.microsoft.com` e inicia sesión en Microsoft Purview portal como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de Joni se estableció en un ejercicio anterior.

1. En Microsoft Purview, ve a **Soluciones** > **Auditoría**.

1. En la página **Búsqueda**, configura la búsqueda:

   - **Intervalo de fecha y hora (UTC)**:

     - **Fecha de inicio**: hace 3 días
     - **Fecha de finalización**: hoy

   - **Actividades: nombres descriptivos**: busca `DLP` y selecciona las actividades siguientes en **Actividades de Information protection y DLP**:

     - Regla DLP creada
     - Regla DLP actualizada
     - Regla DLP eliminada
     - Directiva DLP creada
     - Directiva DLP actualizada
     - Directiva DLP eliminada

   ![Captura de pantalla que muestra las actividades DLP que se van a seleccionar en Auditoría.](../Media/audit-dlp-search.png)

   - **Nombre de búsqueda**: `DLP Policy Activity`

1. Seleccione **Buscar**.

1. La búsqueda puede tardar varios minutos en completarse. Mientras Audita procesa la búsqueda, actualiza la página para comprobar el **estado del trabajo**, el **progreso (%)** y la **hora de búsqueda**.

1. Una vez completado, selecciona **Actividad de directiva DLP** para ver los resultados.

1. Selecciona resultados individuales para ver información detallada sobre cada actividad DLP.

Has buscado y revisado la actividad de Auditoría relacionada con la directiva DLP y la configuración de reglas.

## Tarea 2: Exportación de los resultados de búsqueda en Auditoría

En esta tarea, exportarás los resultados de búsqueda en Auditoría DLP para el análisis sin conexión o el mantenimiento de registros de cumplimiento.

1. En Microsoft Purview, ve a **Soluciones** > **Auditoría**.

1. En la página **Búsqueda**, selecciona la búsqueda **Actividad de directiva DLP** que creaste en la tarea anterior.

1. Seleccione **Exportar** en la parte superior de la página.

1. En el cuadro de diálogo de confirmación, selecciona **Aceptar** para iniciar la exportación.

1. Cuando se complete la exportación, selecciona el vínculo **Descargar archivo** en el banner verde **La exportación se ha completado**.

 > [!Note] **Nota**: sos archivos de exportación de Auditoría se guardan en formato CSV y se pueden abrir en cualquier aplicación de hoja de cálculo o editor de texto. Para facilitar la revisión, usa Excel u otra herramienta de hoja de cálculo. En este entorno de laboratorio, puedes abrir el archivo CSV en el Bloc de notas para confirmar que la exportación se ha completado correctamente.

Has exportado registros de Auditoría relacionados con DLP, que se podrán usar para la revisión sin conexión o el mantenimiento de registros.

## Tarea 3: Creación de una directiva de retención de Auditoría

En esta tarea, configurarás una directiva de retención de auditoría para conservar los registros relacionados con las coincidencias y acciones de DLP para la investigación a largo plazo.

1. En Microsoft Purview, ve a **Soluciones** > **Auditoría**.

1. Selecciona **Directivas** en la barra lateral izquierda.

1. En la página **Directivas**, selecciona **Nueva directiva de retención de auditoría**.

1. En el panel **Nueva directiva de retención de auditoría**, escribe:

   - **Nombre de la directiva**: `Retain DLP Audit Logs`
   - **Descripción**: `Retains audit logs for DLP activities across Exchange, SharePoint, and endpoints to support investigation and compliance.`
   - **Usuarios**: Deja en blanco para aplicar a todos los usuarios.
   - **Tipo de registro**:
      - ComplianceDLPEndpoint
      - ComplianceDLPExchange
      - ComplianceDLPExchangeClassification
      - ComplianceDLPSharePoint
      - ComplianceDLPSharePointClassification
   - **Duración**: 1 año
   - **Prioridad**: `1`

1. Selecciona **Guardar** para crear la nueva directiva de retención de auditoría.

Has configurado una directiva de retención de auditoría que mantiene los registros de coincidencias y actividad de DLP durante un año.
