Los registros son las huellas digitales que deja cualquier actividad. Los siguientes son algunas áreas clave donde los registros juegan un rol integral.


| Use Case                             | Description                                                                                                                                                                                                                  |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Security Events Monitoring           | Los registros ayudan a detectar comportamiento anómalo cuando el monitoreo en tiempo real está siendo usado.                                                                                                                 |
| Incident Investigation and Forensics | Los registros son trazas de cualquier tipo de actividad. Ofrece información detallada de qué ocurrió durante un incidente. El equipo de seguridad utiliza los logs para realizar el análisis de la causa raíz de incidentes. |
| Troubleshooting                      | Como los registros también documentan los errores en los sistemas o aplicaciones, pueden utilizarse para diagnosticar problemas y resultan útiles para solucionarlos.                                                        |
| Performance Monitoring               | Los registros también pueden proporcionar información valiosa sobre el rendimiento de las aplicaciones.                                                                                                                      |
| Auditing and Compliance              | Los registros desempeñan un papel fundamental en la auditoría y el cumplimiento normativo, facilitando así el establecimiento de un rastro de diferentes tipos de actividades.                                               |

## Tipos de Logs


| Log Type         | Usage                                                                                                                                                                                                                                                       | Example                                                                                                                                                    |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| System Logs      | Los registros del sistema pueden ser útiles para solucionar problemas de ejecución en el sistema operativo. Estos registros proporcionan información sobre diversas actividades del sistema operativo.                                                      | - System Startup and shutdown events <br>- Driver Loading events <br>- System Error events <br>- Hardware events                                           |
| Security Logs    | Los registros de seguridad ayudan a detectar e investigar incidentes. Estos registros proporcionan información sobre las actividades relacionadas con la seguridad en el sistema.                                                                           | -Authentication events  <br>- Authorization events  <br>- Security Policy changes events  <br>- User Account changes events <br>- Abnormal Activity events |
| Application Logs | Los registros de la aplicación contienen eventos específicos relacionados con la aplicación. Cualquier actividad interactiva o no interactiva que ocurra dentro de la aplicación se registrará aquí.                                                        | - User Interaction events  <br>- Application Changes events  <br>- Application Update events  <br>- Application Error events                               |
| Audit Logs       | Los registros de auditoría proporcionan información detallada sobre los cambios del sistema y los eventos del usuario. Estos registros son útiles para los requisitos de cumplimiento y pueden desempeñar un papel vital en la supervisión de la seguridad. | - Data Access events  <br>- System Change events  <br>- User Activity events  <br>- Policy Enforcement events                                              |
| Network Logs     | Los registros de red proporcionan información sobre el tráfico entrante y saliente de la red. Desempeñan un papel fundamental en la resolución de problemas de red y también pueden ser útiles durante las investigaciones de incidentes.                   | - Incoming Network Traffic events  <br>- Outgoing Network Traffic events  <br>- Network Connection Logs <br>- Network Firewall Logs                        |
| Access Logs      | Los registros de acceso proporcionan información detallada sobre el acceso a diferentes recursos. Estos recursos pueden ser de diferentes tipos, lo que nos proporciona información sobre su acceso.                                                        | - Webserver Access Logs  <br>- Database Access Logs <br>- Application Access Logs  <br>- API Access Logs                                                   |

Pueden haber varios otros tipos de registros dependiendo de las diferentes aplicaciones y los servicios que ofrecen.

## Windows Event Logs Analysis

Como otros sistemas operativos, Windows también registra varias actividades. Estos se almacenan en archivos de registros segregados, cada uno con una categoría específica de registro. Algunos tipos de registros cruciales almacenados en un sistema operativo Windows son:

* Application: Hay muchas aplicaciones corriendo en el sistema operativo. Cualquier información relacionada con esas aplicaciones es registrada en este archivo. Esta información incluye errores, advertencias, problemas de compatibilidad, etc.
* System: El sistema operativo en sí mismo tiene diferentes operaciones corriendo. Cualquier información relacionada con estas operaciones es registrada en el archivo de registros System. Esta información incluye problemas con drivers, problemas con hardware, información de encendido y apagado del sistema, información de servicios, etc.
* Security: Este es el archivo log más importante dentro de Windows en temas de seguridad. Registra todas las actividades relacionadas con seguridad, incluyendo autenticación de usuarios, cambios en cuentas de usuarios, cambios en políticas de seguridad, etc.

Los campos mayores dentro de un registro de Windows son:

* Description: Este campo tiene información detallada de la actividad.
* Log Name: El Log Name indica el nombre del archivo de registro.
* Logged: Este campo indica el tiempo de la actividad.
* Event ID: Los IDs de eventos son identificadores únicos por cada actividad específica.

Esta tabla muestra algunos IDs de eventos importantes en Windows

| Event ID | Description                                                |
| -------- | ---------------------------------------------------------- |
| 4624     | Una cuenta de usuario que inició sesión exitosamente       |
| 4625     | Una cuenta de usuario que falló al iniciar sesión          |
| 4634     | Una cuenta de sesión que cerró sesión exitosamente         |
| 4720     | Una cuenta de usuario creada                               |
| 4724     | Un intento de hacer un reset a la contraseña de una cuenta |
| 4722     | Una cuenta de usuario que ha sido activada                 |
| 4725     | Una cuenta de usuario que ha sido desactivada              |
| 4726     | Una cuenta de usuario que fue eliminada                    |
