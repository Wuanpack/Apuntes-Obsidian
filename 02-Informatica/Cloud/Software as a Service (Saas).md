## Funciones

### Infraestructura y Operaciones

En el modelo SaaS, el proveedor es el responsable de todas las decisiones de infraestructura y de la operación de esa infraestructura. Esto incluye adquisición de hardware y software, implementación y configuración de software, monitoreo del rendimiento, parches de seguridad, escalabilidad, planificación de capacidad, mantenimiento, copias de seguridad, planificación y pruebas de recuperación ante desastres, etc.

### Interacción Constante con el Cliente

Cuando un cliente adquiere un software on-premise, no podrá tener más contacto con el proveedor del software, excepto cuando llegue el momento de renovar su contrato de mantenimiento anual. 

En el modelo SaaS, el proveedor de SaaS debe brindar un servicio al cliente todos los días. Por lo tanto, existe una relación continua, a menudo diaria, entre el proveedor de SaaS y su comunidad de usuarios.

### Metadatos

En el modelo "local", una vez instalado el software, el proveedor del software generalmente tiene poca o ninguna idea de cómo se está utilizando el software. Sin embargo, dado que el proveedor de SaaS controla la base del código y la infraestructura, tiene la capacidad de recopilar metadatos sobre los niveles de uso e incluso el uso de funciones particulares por parte de la base de clientes.

Si su aplicación está adecuadamente instrumentada para recopilar metadatos, el proveedor de SaaS puede obtener comentarios inmediatos sobre el uso de nuevas funciones tan pronto como las haya implementado.

### Planificación de Lanzamientos de Software

En el modelo local, el proveedor de software publica nuevas versiones de su software en CD o electrónicamente, pero no tiene control sobre cuando sus clientes realmente actualizarán o comenzarán a utilizar la nueva version. Sin embargo, en el modelo SaaS, el proveedor de SaaS controla el plan de actualización del software. Normalmente, existe cierto nivel de multitenencia, lo que significa que el proveedor de SaaS utilizará la misma base de código para todos sus clientes.

## Métricas de SaaS

### Monthly Recurring Revenue (MRR)

El MRR es simplemente la suma de los ingresos por suscripción mensual. Si cobra por su servicio por mes, simplemente agregue todos los ingresos mensuales. Si realiza un pre-factura por un periodo determinado, divida el monto del contrato por la cantidad de meses de suscripción.

### Customer Acquisition Cost (CAC)

El costo de adquisición de clientes (CAC) es el valor que se ha invertido para lograr que un cliente de SaaS se registre en el servicio. En su cálculo, se deben incluir todos los costos incurridos para adquirir clientes, no solo los costos directos. Por lo tanto, esta métrica debe incluir los costos de personal (organizaciones de ventas internas y externas, gerente de marketing, ejecutivos de cuentas, etc.), publicidad (redes sociales, Google AdWords, espacio publicitario en blogs y otros sitios web, listas de correo, etc.) y costos de marketing (marketing de contenidos, diseño de sitios web, puntuación de clientes potenciales, etc.)

CAC = (Suma de ventas y gastos de marketing / Número de nuevos clientes)

CAC es una métrica importante ya que le permitirá evaluar si su precio es el adecuado y cuánto tiempo le llevará recuperar su inversión en CAC. En otras palabras, le permite estimar la profundidad de su flujo de caja y sus necesidades de financiación.

### Average Revenue per Account (ARPA)

A veces se lo denomina ARPU (ingreso promedio por usuario o por unidad) o ARPC (ingreso promedio por cliente). Calculado simplemente como la MRR promedio de todos sus clientes.

ARPA = (Suma de los clientes que tiene una suscripción mensual / Número de clientes).

Si un cliente tiene varias cuentas, deben agruparse y considerarse como una sola cuenta para este cálculo.

### Churn Rate

La tasa de deserción corresponde a la tasa con que los clientes abandonan el servicio, la que se expresa como:

CR = (Número de clientes que han desertado del servicio en un periodo / Número total de clientes al comienzo del periodo).

### Customer Lifetime Value (LTV)

El valor de vida del cliente (LTV) es una estimación del valor total (es decir, los ingresos brutos generados) de un cliente desde el registro hasta el abandono. Los ingresos totales que un cliente aportará al proveedor SaaS dependerán de varios factores, el más importante:

* El precio; el proveedor de SaaS querrá asegurarse de que sus inquilinos paguen la cantidad correcta por el valor que obtienen del servicio.
* Cuánto tiempo utilizan el servicio; el tiempo que un cliente continúa utilizando el servicio y paga por él influye directamente en el valor de vida del cliente (LTV).

El LTV puede calcularse en términos de ARPA y CR mediante la siguiente expresión:

LTV = (ARPA/CR).

### Average Sale Price (ASP)

Representa el MMR promedio de un nuevo cliente cuando se registra por primera vez:

ASP = (Suma de todos los nuevos negocios MRR en el periodo/Número de nuevos cliente en el periodo). Este es un buen indicador del valor percibido de su servicio por el mercado y de la efectividad de su estrategia de ventas para impulsar acuerdos de mayor tamaño.

El conjunto de métricas anteriores se asocian a la efectividad y rentabilidad de negocios en la red, en particular ampliamente utilizadas en el comercio electrónico.


## Desafíos Técnicos de SaaS

### Modelo de Tenencia Múltiple (Multitenancy)

La tenencia múltiple se refiere a una arquitectura de software en la que una única instancia de software se ejecuta en un servidor y sirve a múltiples inquilinos. Sin embargo, cada inquilino tiene su propio conjunto de datos que permanece lógica o físicamente aislado de los datos que pertenecen a los demás. Las opciones de tenencia para el servicio SaaS considera tres componentes:

* Infraestructura de cómputo para aplicaciones, la que puede ser compartida o dedicada.
* Separación de datos, que puede ser física o lógica.
* Versionado de la aplicación, que puede ser de una sola versión o de múltiples versiones.

Dado que la elasticidad de los recursos de cómputo es una característica inherente de SaaS, la viabilidad financiera está fuertemente influenciada por las economías de escala y la puesta en común de recursos. Por lo tanto, la tenencia múltiple, con infraestructura compartida, es el modelo de arquitectura dominante para los proveedores de SaaS.

Una arquitectura de inquilino único es una instancia única de aplicación de software, que permite un inquilino y con recursos informáticos dedicados. Esta arquitectura proporciona la mayor independencia entre los inquilinos, así como también el mayor aislamiento entre ellos. Sin embargo, será más costosa que la arquitectura multiinquilino, ya que el intercambio de infraestructura es mínimo.

En casi todas las arquitecturas SaaS, la capa de red (enlaces ISP, firewalls, dispositivos de descifrado SSL, equilibradores de carga) se comparte, ya que estos dispositivos están inherentemente diseñados para dar servicio a múltiples inquilinos. El servidor de aplicaciones es un componente crítico en multitenencia. Dependiendo del diseño de la aplicación, cada inquilino puede tener una instancia de aplicación dedicada o las instancias de la aplicación pueden asignarse dinámicamente según sea necesario. Si las instancias de la aplicación son dedicadas, esto permite que el proveedor SaaS admita múltiples versiones del software, si así lo desea.

Prácticamente en todas las situaciones, tener a todos los inquilinos en una única versión del software es una buena práctica, ya que reduce la complejidad y el esfuerzo de los equipos de operaciones, soporte y desarrollo de TI. Sin embargo, para los clientes de grandes empresas, poder controlar cuándo se aplican las actualizaciones puede verse como una ventaja, por ejemplo, para respetar los períodos de "congelación de cambios" que existen en ciertos sectores de la industria, o dar tiempo para la capacitación de los usuarios en entornos grandes.

En particular, tener una versión personalizada para un cliente específico es claro punto de fallas para un proveedor de SaaS. A medida que crece el número de clientes y aumenta el número de versiones de código, los costos de desarrollo y soporte no son escalable. Las diferencias en los requisitos del cliente deben implementarse a través de ajustes de configuración de modo que todos los clientes se ejecuten en el código base, pero con diferentes ajustes de configuración, diferentes archivos de configuración, diferentes CSS, etc.

En consecuencia, la personalización de las actualizaciones en aplicaciones consumidas por un gran número de clientes introduce complejidad y puntos de fallos en los servicios SaaS.

### Escalabilidad

Las cargas de trabajo SaaS son particularmente sensibles a los problemas de escala debido a su naturaleza multiinquilino. Para cumplir con el requisito de elasticidad de la infraestructura, la infraestructura SaaS debe diseñarse para escalar, ya sea vertical, horizontal o geográficamente.

Escalar verticalmente se refiere a agregar (o eliminar) recursos de un único nodo de la infraestructura. Normalmente, esto implicaría agregar CPU, agregar memoria, agregar discos internos o reemplazar un servidor por uno más potente.

Escalar horizontalmente se refiere a agregar (o eliminar) nodos a la infraestructura. Ejemplos típicos serían:

* Agregar un servidor web adicional a un clúster de servidores web controlado por un balanceador de carga.
* Agregar un servidor de aplicaciones adicional a un grupo de servidores de aplicaciones.
* Agregar un servidor de base de datos a un grupo de servidores de bases de datos.

El escalado geográfico se refiere a agregar (o eliminar) centros de datos completos a la infraestructura con alguna forma estática o dinámica de distribuir las cargas de trabajo entre los centros de datos.

### Alta disponibilidad

Existe una correlación inmediata y directa entre la disponibilidad de los sistemas y la satisfacción del cliente. Por lo tanto, el proveedor de SaaS debe diseñar para una alta disponibilidad, cuyo nivel estará determinado por consideraciones comerciales, financieras y técnicas.

La otra forma de expresar este requisito de diseño es afirmar que debemos diseñar para una recuperación perfecta de una falla. Se deben preparar escenarios para planificar la falla de un servidor, una unidad de almacenamiento, un segmento de red o incluso un centro de datos completo. En la práctica, diseñar para alta disponibilidad es mucho más fácil con aplicaciones sin estado.

Las aplicaciones con datos persistentes son un desafío para la alta disponibilidad, ya que los datos deben copiarse/replicarse, lo que representa un problema de escalabilidad. Los diseños de alta disponibilidad utilizarán las mismas técnicas de escalamiento horizontal y geográfico que analizamos anteriormente, pero con una capacidad adicional de recuperarse sin problemas de una falla.

### Opciones de Hosting (alojamiento)

- Alojamiento de nube: Utiliza servidores virtuales de una red de servidores para alojar aplicaciones. Los recursos son escalables y facturados según el uso.
- Alojamiento compartido: Varios sitios web comparten los recursos (CPU, memoria y espacio en disco) de un único servidor. Rentable, pero con personalización limitada.
- Alojamiento dedicado: El servidor está dedicado a un único usuario y ofrece control y personalización completos. Su alto rendimiento tiene un mayor costo.
- Virtual Private Servers (VPS): Un servidor físico se divide en varios servidores virtuales, cada uno con sus recursos y sistema operativo dedicados. Ofrece más personalización que el alojamiento compartido.

Comparativa de opciones de hosting:

![[Pasted image 20260503172709.png]]

### Servicio de Entrega de SaaS

El modelo de entrega SaaS se adopta ampliamente en diversas industrias por sus numerosos beneficios, que incluyen mayor flexibilidad, menores requisitos de personal de TI, mejor colaboración y actualizaciones automáticas de software. A continuación, se muestran algunos componentes de un conjunto de herramientas de entrega de SaaS:

1. Herramientas de integración y despliegue continuo: Los desarrolladores pueden integrar fácilmente su código en un repositorio central para que otros miembros del equipo puedan probarlo e implementarlo. Además, automatizar tantos procesos como sea posible eliminará la necesidad de implementar código manualmente o registrarlo repetidamente.
2. Herramientas de control de versiones: Los sistemas de control de versiones realizan un seguimiento de cada cambio realizado en su código base a lo largo del tiempo. Proporcionan una manera para que los desarrolladores reviertan los cambios rápidamente si es necesario y permiten que los equipos colaboren en proyectos sin sobrescribir accidentalmente el trabajo de los demás.
3. Herramientas de seguimiento y análisis: Las herramientas de monitoreo le indican cuando algo sale mal con su aplicación o su infraestructura subyacente, ya sea que haya una interrupción o un problema de rendimiento. Las herramientas de análisis recopilan datos sobre cómo las personas usan su producto para que pueda medir los patrones de uso a lo largo del tiempo y realizar los ajustes correspondientes.
4. Herramientas de seguridad. Una estrategia de seguridad sólida es esencial para cualquier aplicación SaaS, especialmente si está creando una solución de nivel empresarial. Estas herramientas pueden ayudarle a proteger sus datos del acceso no autorizado e implementar sistemas de autenticación sólidos que garanticen que solo los usuarios autorizados puedan acceder a datos o funciones confidenciales.
5. Proveedor de infraestructura en la nube: Los proveedores de infraestructura en la nube ofrecen servicios como máquinas virtuales (VM), almacenamiento y bases de datos en un modelo de pago por uso. Por lo general, se utilizan para alojar los componentes back-end de una aplicación SaaS, como servidores web, servidores de bases de datos o equilibradores de carga.
6. Herramientas de gestión de contenedores: Los contenedores lo ayudan a empaquetar el código de su aplicación y las dependencias de un entorno aislado que puede ejecutarse en cualquier máquina. Facilitan la implementación de nuevas versiones de su software, permiten actualizaciones continuas sin tiempo de inactividad y permiten pruebas automatizadas y canales de CI/CD.
7. Herramientas de gestión de acuerdos de nivel de servicio (SLA): Los SLA garantizan que sus clientes siempre reciban el nivel de servicio que esperan de su empresa. Puede incluir seguridad, disponibilidad, rendimiento y más.

## Seguridad en Servicios SaaS

Gobernanza, Riesgo, Cumplimiento (GRC) es un término utilizado para describir los procesos de una organización utilizados para abordar el gobierno corporativo, la gestión de riesgos empresariales y el cumplimiento corporativo de las leyes y regulaciones aplicables. Estos tres objetivos a veces se denominan los tres pilares de GRC, los cuales se describen a continuación:

1. Gobernanza: Corresponde a garantizar que se implementen las políticas y la estrategia, y que se sigan correctamente los procesos requeridos. La gobernanza incluye definir roles y responsabilidades, medir e informar, y tomar acciones para resolver cualquier problema identificado. 
2. Gestión de Riesgos: El conjunto de procesos a través de los cuales la dirección identifica, analiza y, cuando sea necesario, responde adecuadamente a los riesgos que podrían afectar negativamente la realización de los objetivos comerciales de la organización.
3. Cumplimiento: Son aquellos procesos de gestión que identifican los requisitos aplicables (definidos, por ejemplo, en leyes, regulaciones, contratos, estrategias y políticas), evalúan el estado de cumplimiento, evalúan los riesgos y costos potenciales del incumplimiento frente a los gastos proyectados para lograr el cumplimiento, por lo tanto, priorizar, financiar e iniciar las acciones correctivas que se consideren necesarias.

![[Pasted image 20260503173940.png]]


La gestión de riesgos está impulsada por un conjunto de decisiones políticas clave y la implementación de controles operativos y de seguridad de la información (InfoSec).

Entre las decisiones de políticas clave que debe tomar el proveedor de SaaS se encuentran:

1. Recuperación ante desastres / Continuidad del Negocio
2. Políticas de Personal
3. Políticas de Acceso Físico
4. Políticas de Acceso a Datos / Seguridad de Datos.

Entre los principales controles de InfoSec que se deben implementar se incluyen:

1. Escaneos de vulnerabilidad
2. Análisis de amenazas.
3. Controles de acceso y contraseña.
4. Detección de intrusiones.
5. Gestión de claves.
6. Gestión de incidentes de seguridad

Entre los controles operativos clave que se deben implementar para mitigar el riesgo se incluyen:

1. Análisis de registros
2. Validación de respaldo
3. Procesos de puesta en servicio / desmantelamiento
4. Endurecimiento del sistema operativo
5. Parches de seguridad

