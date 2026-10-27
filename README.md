Proyecto I2-Sync — MTH S.R.L.

Módulo de Sincronización Web y API Móvil en la Nube

Asignatura: Organización Empresarial  
Carrera: Tecnicatura Universitaria en Programación (UTN)  
Integrante: Nahuel Klen  
Docente Adjunto: Prof. Mario Raúl López

Descripción del sistema

I2-Sync es una propuesta de software diseñada para extender las capacidades del ERP local de escritorio I2 de MTH S.R.L.

El sistema permitirá gestionar pedidos e información de stock desde dispositivos móviles utilizados por los vendedores en ruta, facilitando la comunicación con el depósito de Villa Lugano y la sincronización de las operaciones con la oficina central de Crespo.

El proyecto contempla la gestión de pedidos, la emisión de remitos digitales, el control de inventario y la sincronización de datos entre los distintos componentes del sistema.

Documentación del proyecto

- Modelo de procesos de negocio BPMN 2.0.
- Diccionario de datos.
- Documentación técnica del sistema.

Control de versiones

La documentación se administra mediante Git y GitHub, utilizando ramas secundarias, commits descriptivos y Pull Requests para revisar los cambios antes de incorporarlos a la rama principal.

## 3. Gestión del Backlog Ágil

El seguimiento de las Historias de Usuario del proyecto I2-Sync se realiza mediante GitHub Projects. El tablero permite visualizar las tareas, sus criterios de aceptación y su estado de avance.

**Tablero del proyecto:** [I2-Sync - GitHub Projects](https://github.com/users/NahueKlen/projects/1/views/1)

Las tres Historias de Usuario se organizan según su estado: Por Hacer, En Progreso y Listo.


## 4. Mecanismos de Control e Indicadores de Desempeño

Los siguientes indicadores se proponen para auditar el desempeño técnico de I2-Sync. Los valores representan objetivos de calidad que deberán validarse mediante pruebas y mediciones cuando el sistema esté implementado.

| Mecanismo / Indicador | Estándar de desempeño | Método de medición y control | Acción correctiva |
|---|---|---|---|
| Latencia de respuesta de la API | ≤ 2 segundos por consulta | Medición del tiempo de respuesta mediante pruebas y registros del servidor | Optimización de consultas SQL, índices y revisión del rendimiento de la API |
| Integridad de transacciones ante caídas de red | 100 % de los pedidos conservados sin pérdida ni duplicación | Auditoría de la cola local, revisión de logs y conciliación con los registros confirmados en el ERP | Reintentos de sincronización, conservación de pedidos pendientes y control de duplicados |
| Tasa de error en la carga de datos | Reducción del 90 % de las correcciones de remitos respecto de una línea de base | Comparación mensual de las correcciones registradas con el período de referencia | Validación de campos obligatorios, formatos y reglas de negocio |

Los indicadores deberán revisarse periódicamente. Las desviaciones respecto de los estándares establecidos deberán documentarse y dar lugar a acciones correctivas verificables.

## 5. Declaración del Uso Crítico de Inteligencia Artificial

Durante la elaboración de este trabajo práctico se utilizaron herramientas de Inteligencia Artificial Generativa como apoyo para organizar la documentación, estructurar el diagrama BPMN, redactar las Historias de Usuario, proponer indicadores de control y mejorar la presentación de los contenidos.

Los prompts se orientaron a solicitar estructuras compatibles con la consigna académica, explicaciones de la notación BPMN, historias de usuario en formato estándar y propuestas de indicadores con criterios de medición y acciones correctivas.

Los resultados generados por estas herramientas se consideraron propuestas de trabajo y no fuentes de verdad automáticas. Se revisaron las respuestas y se realizaron ajustes durante el proceso, especialmente en la representación del comportamiento ante la pérdida de conectividad y los reintentos de sincronización con el ERP I2.

Los indicadores definidos son estándares propuestos y no resultados de pruebas de rendimiento realizadas. Su cumplimiento deberá verificarse mediante mediciones cuando exista una implementación funcional.

La Inteligencia Artificial se utilizó como herramienta de asistencia y no como sustituto del análisis crítico. El estudiante es responsable de revisar el contenido final, contrastarlo con los requisitos de la consigna y corregir las inconsistencias que identifique.
