# Ecosistema de Automatización IA – Encuestas Inteligentes

## Proyecto Final

Sistema de automatización para el procesamiento inteligente de encuestas de satisfacción, utilizando **Airtable, Make, OpenAI y Slack**.

El flujo recibe nuevas respuestas desde Airtable, utiliza un modelo de IA para interpretar comentarios en lenguaje natural y determinar **sentimiento, urgencia, resumen y necesidad de revisión humana**.

Cuando una respuesta requiere intervención humana, el flujo genera una instancia de revisión y envía una alerta mediante Slack. Los casos que no requieren revisión continúan automáticamente.

## Arquitectura

**Airtable Form → Airtable → Make → OpenAI → JSON → Airtable → Router → Slack / procesamiento automático**

El proyecto incorpora:

- Base de datos dinámica en Airtable.
- Integración con OpenAI mediante API.
- Interpretación de respuestas cualitativas mediante IA.
- Salida estructurada en JSON.
- Clasificación de sentimiento y urgencia.
- Router para toma de decisiones.
- Human-in-the-loop para casos críticos.
- Notificaciones mediante Slack.
- Manejo de errores mediante Error Handler.
- Registro del estado del procesamiento en Airtable.
- Dashboard de seguimiento y KPIs.

## Human-in-the-loop

Los casos sensibles o críticos no generan una acción automática hacia el cliente.

Cuando la IA determina que una respuesta requiere revisión humana:

1. Make registra el caso en Airtable.
2. Se crea una revisión humana.
3. Se envía una alerta al canal correspondiente de Slack.
4. El caso queda pendiente de aprobación humana antes de continuar.

## Manejo de errores

El escenario incorpora una ruta de manejo de errores. Ante una falla en la integración con la API, el flujo actualiza el registro correspondiente en Airtable y evita que el escenario continúe procesando información inválida.

## Dashboard

Se implementó un tablero en Airtable para monitorear:

- Total de encuestas.
- Encuestas negativas.
- Encuestas críticas.
- Pendientes de aprobación humana.
- Cantidad de errores.
- Tasa de error.
- Distribución de respuestas por sentimiento.

## Base de datos pública

Vista pública de Airtable:

https://airtable.com/apptuw0G37gGltgWL/shr85ESAburejXsYi

## Archivos incluidos

El repositorio contiene:

- Arquitectura del ecosistema de automatización.
- Manual y modelo de datos.
- Matriz de costos y selección del modelo de IA.
- Documento de seguridad y resiliencia.
- Evidencia de revisión humana mediante Slack.
- Blueprint del escenario principal de Make.
- Blueprint del escenario complementario.
- README del proyecto.

## Tecnologías utilizadas

**Airtable | Make | OpenAI API | Slack | Gmail**

## Seguridad

Las credenciales y API Keys no se almacenan en este repositorio. Las conexiones se administran mediante los mecanismos de credenciales de Make y se aplica minimización de datos en las solicitudes enviadas al modelo de IA.

---

**Proyecto Final – Ecosistema de Automatización IA**

## Pruebas realizadas

Para validar el funcionamiento del ecosistema se realizaron múltiples ejecuciones con diferentes tipos de respuestas:

| Prueba | Caso evaluado | Resultado esperado |
|---|---|---|
| 1 | Experiencia positiva | Sentimiento positivo, urgencia baja y procesamiento automático |
| 2 | Experiencia negativa | Sentimiento negativo y clasificación automática |
| 3 | Reclamo de mayor gravedad | Detección de urgencia alta |
| 4 | Amenaza de acciones legales | Urgencia crítica, revisión humana obligatoria y notificación mediante Slack |
| 5 | Caso sin necesidad de revisión humana | Continuación automática del flujo y actualización del registro |
| 6 | Prueba de error (unhappy path) | Activación del Error Handler, registro del error en Airtable y control de continuidad mediante Resume |

Las pruebas permitieron verificar el análisis mediante IA, el enrutamiento condicional, la intervención humana en casos críticos y el tratamiento controlado de errores.

## Dashboard y monitoreo

Se implementó un dashboard en Airtable con los siguientes indicadores:

- Total de encuestas.
- Encuestas negativas.
- Encuestas críticas.
- Pendientes de aprobación humana.
- Cantidad de errores.
- Tasa de error.
- Distribución de respuestas según sentimiento.

La interfaz de Airtable utilizada para visualizar los KPIs se encuentra implementada dentro de la base. Debido a las restricciones de publicación web del plan utilizado, se proporciona como respaldo una vista pública de solo lectura de los registros procesados.

**Vista pública de Airtable:**

https://airtable.com/apptuw0G37gGltgWL/shr85ESAburejXsYi
