---
title: EXAMEN FINAL
date: 2024-12-29 14:45:00 -05:00
categories: [Reconnaisance, Kill Chain, Pentesting]
tags: [nmap, kali, metasploit]  # TAG names should always be lowercase
---


# RESOLUCION DE EXAMEN 
 A continuacion resolveremos las preguntas del cuestionario brindado:

 1. ¿Cómo podrías utilizar Procmon y Sysmon juntos para investigar la actividad de un proceso sospechoso?

    ## uso conjutno de Procmon y Sysmon
    para investigar un proceso sospechosode manera efectiva, se pueden usar Procmon y Sysmon en conjunto. Para ello seguiremos los siguientes pasos:
    1. Configuracion de Sysmon:
    - Instalacion: nos aseguraremos de tener Sysmon instalado en el sistema. Esta herramienta proporciona un registro detallado de envetos relacionados con procesos y actividad de red.
    - Configuracion de Eventos: Configura Sysmon para capturar eventos relevantes, como:
        * Event ID 1: creacion de procesos.
        * Event ID 3: conexiones de red.
        * Event ID 11: cambios en archivos.
    - esta configuracion te permitira obtener un panorama detallado de lo que ocurre en el sistema.
    2.  Ejecucion de Procmon:
    - Iniciar Procmon: se ejecuta procmon y comienza a capturar eventos en tiempo real.
    - Aplicar filtros: filtra los eventos para concetrarte unicamente en el proceso sospechoso. Puedes hacerlo filtrando por el nombre del proceso, su ID o su ruta de acceso.
    3. Analisis de datos:
    - Correlacionar eventos: una vez capturados los datos, analizar los eventos de ambas herramientas. Buscar patrones y comportamientos inusuales, como accesos a archivos criticos o conexiones a direccion IP desconocidas.
    - Identificacion de comportamientos maliciosos: si un procesos accede a archivos sensibles o establece conexiones no autorizadas, esto podria indicar actividad maliciosa.


    # Explica los tipos de eventos que Procmon y Sysmon pueden capturar de forma complementaria.
    ambas herramientas capturan diferentes tipos de eventos que se complementan entre si:
    * Eventos capturados por Procmon:
    - acceso a archivos: registra operaciones de lectura, escritura y eliminacion de archivos. Esto es util para identificar manipulacion de archivos maliciosos.
    - Cambios en el registro: Monitorea modificaciones en el registro de Windows, lo que puede señalar cambios no autorizados en la configuracion del sistema.
    - Conexiones de red: captura intentos de conexion de red, lo que es crucial para identificar comunicaciones sospechosas.
    * Eventos capturados por Sysmon
    - Creacion de procesos (Event ID 1): registra cuando y como se inician nuevos procesos, incluyendo la linea de comandos utilizada.
    - Conexiones de red (Event ID 3): proporciona detalles sobre las conexiones de red que establecen procesos, incluyendo direccion IP y puertos.
    - Cambios en archivos (Event ID 11): registra la creacion, modificacion y eliminacion de archivos, esencial para rastrear la actividad de malware.

    * Como se complemtentan: PROCMON OFRECE UN ENFOQUE EN LA OPERACIONES A NIVEL DE ARCHIVO Y REGISTRO, MIENTRAS QUE SYSMON PROPORCIONA CONTEXTO SOBRE LOS PROCESOS Y SU INTERACCION CON LA RED.


    # Proporciona un ejemplo práctico de cómo identificar un posible comportamiento malicioso en un proceso utilizando ambas herramientas.

    Imagina que has identificado un proceso sospechoso llamado malware.exe.

    * Pasos para la Investigación:
    1. Configuración de Sysmon:
    - Asegúrate de que Sysmon esté configurado para capturar eventos de creación de procesos y conexiones de red. Esto garantiza que tengas un registro completo de la actividad del proceso.
    2. Ejecución de Procmon:
    - Filtra Procmon para capturar solo eventos relacionados con malware.exe. Observa cualquier acceso a archivos y cambios en el registro que realice este proceso.
    3. Análisis de Eventos:
    - Procmon: Si notas que malware.exe accede a archivos en directorios sensibles, como C:\Windows\System32, esto es un indicador de actividad sospechosa.
    - Sysmon: Revisa si malware.exe establece conexiones a direcciones IP desconocidas. Esto puede señalar comunicación con un servidor malicioso.
    4. Correlación de Datos:
    - Si observas que malware.exe es creado por un proceso legítimo, como cmd.exe, y simultáneamente accede a archivos críticos, esto refuerza la sospecha de actividad maliciosa.
    5. Documentación y Respuesta:
    - Registra todos los hallazgos y toma medidas correctivas, como eliminar malware.exe y bloquear la dirección IP involucrada. Asegúrate de documentar el proceso para futuras referencias y mejora de la seguridad.

[1-2][8-12]


2. En Sysmon, ¿qué diferencias existen entre los eventos ProcessCreate y ProcessAccess, y qué utilidad tienen cada uno para un analista de seguridad? 

 # Diferencias y utilidad para un analista de seguridad

     PROCESSCREATE (EVENT ID 1)
   - descripcion: este evento se genera cuando un nuevo proceso es creado en el sistema. Proporciona informacion relevante sobre el proceso que se inicia, incluyendo detalles del proceso padre.
   - utilidad: es fundamental para rastrear la creacion de procesos, lo que ayuda a identificar la ejecicion de malware o procesos no autorizados. Permite a los analistas ver que procesos se estan iniciando y bajo que condiciones, facilitando la deteccion de actividades inusuales.
    
    PROCESSACCESS (EVENT ID 10)
    - descripcion: este evento se genera cuando un proceso accede a otro proceso. Incluye operaciones como lectura o escritura en la memoria de otro proceso, asi como la manipulacion de sus handles.
    - utilidad: es util para detectar comportamientos sospechosos, como un proceso malicioso que intenta interactuar con procesos legitimos. Esto puede indicar intentos de inyeccion de codigo o manipulacion de procesos, lo que es critico para la seguridad.

 # Describe los atributos principales de ambos eventos:
 Atributos de ProcessCreate:
 - Timestamp: marca de tiempo del evento.
 - Processid: ID del nuevo proceso creado.
 - Image: ruta del ejecutable del proceso.
 - CommandLine: linea de comandos utilizada para iniciar el proceso.
 - ParentProcessid: ID del proceso padre que creo el nuevo proceso.
 - User: usuario que inicio el proceso.

 Atributos de ProcessAccess:
 - Timestamp: marca de tiempo del evento.
 - Processid: ID del proceso que realiza el acceso.
 - TargetProcessid: ID del proceso que esta siendo accedido.
 - AccessMask: mascara de acceso que indica el tipo de acceso que se esta realizando (lectura, escritura, etc).
 - SourceImage: Ruta del ejecutable del proceso que realiza el acceso.
 - User: usuario que esta realizando el acceso.

 # Escenarios para ProcessCreate:
   1. Ejecucion de malware: un analista puede observar un evento ProcessCreate donde un ejecutrable sospechoso (por ejemplo, malicious.exe) se inicia desde una ubicacion inusual, como una carpeta temporal o un directorio de usuario. ESto puede indicar la ejecucion de malware, especialmente si se acompaña de una linea de comandos inusual.
   2. presistencia de amenazas: Si se detecta que un proceso legitimo (como actualizador de software) esta creando un nuevo proceso que no deberia estar presente, esto puede ser indicativo de que un atacante ha comprometido el software para mantener la persistencia en el sistema.
 # Escenarios para ProcessAccess:
   1. Inyeccion de codigo: un evento ProcessAccess puede mostrar que un proceso legitimo (como un navegador web) intenta acceder a otro proceso (como un antivirus). ESto puede ser un indicativo de un ataque de inyeccion de codigo, donde un malware intenta manipoular o deshabilitar la proteccion del antivirus.
   2. Acceso no autorizado a procesos criticos: si un proceso no autorizado intenta acceder a procesos criticos del sistema (como lsass.exe o svchost.exe) esto puede ser un signo de un ataque en curso, como un intento de robo de credenciales o manipulacion del sistema operativo.


   los eventos ProcessCreate y ProcessAccess en sysmon son herramientas escenciales para los analistas de seguridad. Mientras que ProcessCreate ayuda a identificar la creacion de nuevos procesos, ProcessAccess permite detectar interacciones sospechosas entre procesos. Juntos, proporcionan una vision integral de la actividad del sistema y son cruciales para la deteccion y respuesta a amenzas.


[1-2][8-12]




3. En Procmon, ¿qué operación(es) corresponde(n) al evento FileCreateStreamHash en Sysmon, y cómo podrías configurarlo en Sysmon para detectar un posible uso malicioso de Alternate Data Streams (ADS)? 

 # operaciones en Procmon relacionadas con FileCreateStreamHash en Sysmon
  en procmon, las operaciones que corresponden al evento FileCreateStreamHash en sysmon son:
   - CreateFile: esta operacion se utiliza para crear un nuevo flujo de datos alternativo ADS. Cuando se crea un ADS, se registra como una operacion CreateFile con un nombre que incluye el formato filename:streamname.
   - WriteFile: Se utiliza para escribir datos en un flujo de datos alternativo. Si un atacante esta almacenando datos maliciosos en un ADS, esta operacion se registrara en procmon.
   - DeleteFile: si se eliminan un flujo de datos alternativo, esta operacion tambien se registra, lo que puede ser relevante para el analisis.

  * Configuracion de sysmon para detectar el uso malicioso de ADS.
   para configurar sysmon de manera que detecte el uso malicioso de Alternate Data Streams, se sigue estos pasos: 
    1. instalacion de sysmon: asegurate de tener Sysmon instalado en tu sistema.
    2. configuracion del archivo de configuracion: crea o edita un archivo de configuracion XML para sysmon. Asegurate de incluir la siguiente linea en la seccion de eventos:
    ```bash 
        <EventFiltering>
        <FileCreateStreamHash on="true"/>
        </EventFiltering>
    ```
    3. Ejecutar Sysmon con la configuracion: usa el siguiente comando para instalar o actualizar con tu archivo de configuracion:
     ```bash 
       sysmon -accepteula -c path\to\your\config.xml
    ```
    4. Monitoreo de eventos: Despues de configurarlo, sysmon comenzara a registrar eventos FileCreateStreamHash en el visor de eventos de windows, permitiendo la identificacion de la creacion de flujos de datos alternativos.

# Que son los Alternate DAta Streams ADS  y por que pordrian ser usados por atacantes.

    los Alternate Data Streams ADS son una caracteristica del sistema de archivos NTFS en windows que permite asociar multiples flujos de datos con un solo archivo. Esto significa que un archivo puede contener datos adicionales que no son visibles en la vista estandar del sistema de archivos. Por ejemplo, un archivo de texto puede tener un flujo alternativo que almacena metadatos o informacion adicional.

 * Como podria hacerse uso de forma maliciosa
    los atacantes pueden usar ADS para:
    - Ocultar malware, almacenar malware en un flujo alternativo permite que le archivo principal parezca legitimo y no contenga contenido malicioso a simple vista. ESto dificulta la deteccion por parte de software antivirus y otras herramientas de seguridad.
    - evasion de deteccion, los datos en flujos alternativos no son visibles en exploraciones estandar de archivos, lo que les permite evadir la deteccion de actividades maliciosas. Esto es especialmente util para mantener la presistencia en sistemas comprometidos.

# Operaciones de Procmon relacionadas con la actividad de ADS
    las operaciones de procmon que estan relacionadas con la actividad de Alternate Data Streams incluyen:
 - CreateFile: se utilizan para crear un nuevo archivo o un flujo de datos alternativo. Cuando un atacante crea un ADS, se registra como una operacion CreateFile con el foramto Filename:streamname.
 - WriteFile: utilizada para escribir datos en un flujo de datos alternativo. Si un atacante esta almacenando datos maliciosos en un ADS, esta operacion se registrara.
 - ReadFile: esta operacion se utliza para leer datos de un flujo de datos alternativo, lo que puede ser parte del comportamiento del atacante al ejecutar codigo o extender informacion.


 La deteccion de Alternate Data Streams es crucial para la seguridad, ya que pueden ser utilizados por atacantes para ocultar actividades maliciosas. Configurando Sysmon para registrar eventos FileCreateStreamHash y utilizando Procmon para monitorear operaciones como CreateFile, WriteFile y DeleteFile, los analistas de seguridad pueden identificar y responder a posibles amenzas de manera mas efectiva.
[1-2][8-12]



#  En Sysmon, ¿qué ventajas ofrece el uso de filtros avanzados en comparación con capturar todos los eventos de forma indiscriminada? 
 El uso de filtros avanzados en Sysmon ofrece varias ventajas clave en compracion con la captura indiscriminada de eventos:
  1. Reduccion de Ruido:
   - Los filtros avanzados permiten eliminar eventos irrelevantes, lo que facilita la identificacion de actividades criticas y sospechosas. ESto es esencial en entornos donde la cantidad de datos puede ser abrumadora.

   2. Mejora del rendimiento:
    - al limitar la cantidad de eventos registrados, se reduce la carga en el sistema. ESto mejora el rendimiento general, ya que se requiere menos tiempo y recursos para procesar y almacenar los logs.
    3. Facilitacion del analisis:
    - con menos datos que revisar, los analisis pueden concentrarse en eventos significativos, acelerando asi la deteccion de incidentes de seguridad y mejorando la respueta ante amenazas.
    4. Optimizacion del almacenamiento:
    - filtrar eventos innecessarios reduce la cantidad de datos que deben almacenarse, lo que puede resultar en menores costos de infraestructura y una gestion mas eficiente de lo logs.
    5. Enfoque en amenazas especificas:
    - los filtros permiten a las organizaciones centrarse en eventos que son mas relevantes para su entorno, mejorando la eficacia de las medidas de seguridad implementadas.

 # investiga como un mal diseño de filtros podria afectar el desempeño del sistema y calidad de los logs.
 un mal diseño de filtros puede tener consecuencias graves tanto para el desempeño del sistema como para la calidad de los logs:
  1.  Perdida de informacion critica:
     - filtros demasiado restrictivos pueden omitir eventos importantes, lo que puede permitir que actividades maliciosas pasen desapercibidas. Esto es especialmente preocupante en la deteccion de amenazas.
  2. Sobrecarga del sistema:
     -filtros ineficaces que no limitan adecuadamente la cantidad de eventos pueden resultar en un volumen excesivo de datos. Esto puede llevar a un uso excesivo de recursos del sistema, lo que afecta negativamente su rendimiento y la capacidad de respuesta ante incidentes.
  3. Dificultades en el analisis de logs:
   - la inclusion de eventos irrelevantes puede complicar la identificacion de patrones de ataque y aumentar el tiempo necesario para realizar analisis forenses. ESto dificulta la respuesta rapida a incidentes de seguridad.


 # Proporciona un ejemplo de un filtro efectivo para reducir ruido en un entorno de producción.  
 para reducir el ruido en un entorno de produccion, un filtro efectivo podria ser el siguiente:
  ```bash 
       <Sysmon schemaversion="4.82">
     <EventFiltering>
     <ProcessCreate onmatch="include">
      <Image condition="contains">malicious.exe</Image>
     </ProcessCreate>
     <NetworkConnect onmatch="include">
      <DestinationPort>443</DestinationPort>
     </NetworkConnect>
     <ProcessTerminate onmatch="exclude" />
     </EventFiltering>
     </Sysmon>
  ```
  el ProcessCreate captura solo eventos de creacion de procesos relacionados con un archivo especifico (malicious.exe). Esto ayuda a centrar la deteccion en actividades potencialmente maliciosas.

  el NetworkConnect incluye solo las conexiones de red a puertos relevantes (por ejemplo, 443), excluyendo trafico inncesario que podria generar ruido en los logs.

  el ProcessTerminate excluye eventos de terminacion de procesos, que a menudo son menos relevantes para el analissi de seguridad.

 
Este filtro asegura que los logs capturados sean significativos, facilitando un analisis mas efectivo de las actividades en el sistema. Implementar filtros adecuados es crucial para optimizar la seguridad y la eficiencia operativa en entornos TI.

[3-7][13-16]









# REFERENCIAS
[1] BALCI, A., UNGUREANU, D., & VONDRUŠKA, J. (2020). Malware Reverse Engineering Handbook.

[2] Schneier, B. (2018). Click here to kill everybody: Security and survival in a hyper-connected world. WW Norton & Company.

[3] Simanungkalit, K. G., Lubis, M. I. A., Rangkuti, D. A., Aprianda, I., & Gunawan, I. (2024). Analisis Keamanan Sistem Operasi Windows Terhadap Serangan Malware Dari Aplikasi Crack Adobe Photoshop. Jurnal Inovasi Artificial Intelligence & Komputasional Nusantara, 1(1), 43-47.

[4] Huang, Y. T., Guo, Y. R., Wong, G. W., & Chen, M. C. (2024). A Cascade Approach for APT Campaign Attribution in System Event Logs: Technique Hunting and Subgraph Matching. arXiv preprint arXiv:2410.22602.

[5] Breed, J., Baker, P., Chu, K. D., Starr, C., Fox, J., & Baitinger, M. (2000). The spacecraft emergency response system (SERS) for autonomous mission operations. Reducing the Cost of Spacecraft Ground Systems and Operations, 105-112.

[6] Eichler, C., Röckl, J., Jung, B., Schlenk, R., Müller, T., & Hönig, T. (2024). Profiling with trust: system monitoring from trusted execution environments. Design Automation for Embedded Systems, 1-22.

[7] Yang, Q. (1999). Simulation of the Oracle data buffering mechanism.

[8] Smiliotopoulos, C., Barmpatsalou, K., & Kambourakis, G. (2022). Revisiting the detection of lateral movement through Sysmon. Applied Sciences, 12(15), 7746.

[9] Mavroeidis, V., & Jøsang, A. (2018, March). Data-driven threat hunting using sysmon. In Proceedings of the 2nd international conference on cryptography, security and privacy (pp. 82-88).

[10] Prawira, Y. P., & Samsudin, S. (2022). Live Forensics Analysis Of Malware Identified Email Crimes To Increase Evidence Of Cyber Crime. Digital Zone: Jurnal Teknologi Informasi dan Komunikasi, 13(2).

[11] Ahmed, M. N. (2023, October). Analyzing OneNote Malware through Static and Dynamic Analysis: Detection and Mitigation Measures. In 2023 International Conference on IT and Industrial Technologies (ICIT) (pp. 1-6). IEEE.

[12] Hosamani, M., Narayanappa, H., & Rajan, H. (2007, September). Monitoring the monitor: An approach towards trustworthiness in service oriented architecture. In 2nd international workshop on Service oriented software engineering: in conjunction with the 6th ESEC/FSE joint meeting (pp. 42-46).

[13] https://www.blumira.com/blog/sysmon-benefits 

[14]  https://www.deloitte.com/es/es/services/risk-advisory/blogs/cyber-pills/edr-vs-event-log-vs-sysmon.html 

[15]  https://www.deloitte.com/es/es/services/risk-advisory/blogs/cyber-pills/edr-vs-event-log-vs-sysmon.html  https://support.microsoft.com/es-es/office/filtrar-por-criterios-avanzados-4c9222fe-8529-4cd7-a898-3f16abdff32b  

[16] https://www.deloitte.com/es/es/services/risk-advisory/blogs/cyber-pills/edr-vs-event-log-vs-sysmon.html  https://ftpdocs.broadcom.com/cadocs/0/CA%20Enterprise%20Log%20Manager%20r12%201%20SP1-ESP/Bookshelf_Files/HTML/Advanced_Filters.html  