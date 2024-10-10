---
title: Reconnaissance
date: 2024-10-03 16:22:00 -05:00
categories: [Reconnaisance, Kill Chain, Pentesting]
tags: [nmap, kali, metasploit]  # TAG names should always be lowercase
---


# Reconnaissance
 la etapa de reconocimiento es la primera fase en un ataque de ciberseguridad o prueba de penetracion. En esta etapa recopila informacion sobre el objetivo para identificar vulnerabilidades y posibles puntos de entrada. Detallaremos de forma que se entienda mejor:

 1. objetivos de reconocimiento
 * identificar el objetivo: conocer que sistemas, redes o aplicaciones e van a analizar.
 * recopilar informacion: obtener datos relevantes sobre el objetivo, como direcciones IP, nombres de dominio, servicios en ejecucion.

 2. tipos de reconocimiento
 * reconocimiento pasivo:
 - descripcion: no interactua directamente con el objetivo
 - fuentes: utiliza informacion de fuentes publicas, como redes sociales, sitios web, bases de datos filtradas.
 
 *reconocimiento activo:
 - descripcion: involucra interaccion directa con el objetivo
 - herramientas: utiliza herramientas como nmap para escanear puertos y servicios.

3. herramientas comunes de reconocimiento
|Tipo|Herramienta| Funcion|
|reconocimiento pasivo|Google| busqueda de informacion publica|
|reconocimiento pasivo|WHOIS| informacion de dominio y propietario|
|reconocimiento activo|nmap|escaneo de puertos y servicios|
|reconocimiento activo| maltego | visualizacion de relacion de datos|

4. proceso visual del reconocimiento
![diagrama](/assets/images/diagrama.png)

5. resultados de reconocimiento
- lista de direcciones IP y nombres de dominio, la informacion basica sobre el objetivo.
- servicios en ejecucion, que aplicaciones estan escuchando en que puertos.
- vulnerabilidades potenciales, puntos debiles que pueden ser explotados en etapas posteriores.

**ESTA ETAPA DE RECONOCIMIENTO ES CRUCIAL PARA EL EXITO DE CUALQUIER ATAQUE O PRUEBA DE PENETRACION, PERMITE A LOS ATACANTES ENTENDER MEJOR SU OBJETIVO Y PLANIFICAR SUS PROXIMOS PASOS DE MANERA MAS EFECTIVA. LA INFORMACION RECOPILADA EN ESTA FASE ES LA BASE SOBRE LA CUAL SE CONTRUYE LAS ESTRATEGIAS DE ATAQUE.**

# Por que debemos ejecutar NMAP con privilegios de root?

ejecutar Nmap como root es importante porque permite realizar escaneos mas completos y precisos, con privilegios de root, el nmap puede acceder a funciones de red que le permiten identificar todos los puertos abiertos, detectar servicios en ejecucion y conocer el sistema operativo de los dispositivos. Sin estos permisos, algunas funcionalidades estan limitadas y podrias no obtener toda la informacion que necesitas sobre la red que se esta analizando.

# ¿Qué significan los flags -sS, -sT, -sV, -O en el escaneo de nmap?

vamos a describir una a una:

## -sS (SYN SCAN)
este es un metodo de escaneo "stealth" que envia un paquete SYN (solicitud sin conexion) a los puertos del obejtivo. Si un puerto esta abierto, el dispositivo responde, pero nmap no completa la conexion, esto lo hace mas dificil de detecatar, como un escaneo sigiloso.

## -sT (TCP Connect Scan)
este metodo intenta conectarse completamente a los puertos. Completa el proceso de conexion, lo que lo hace mas facil de detectar, se usa cuando no tienes permisos especiales en el sistema.

## -sV (SErvice Version Detection)
este flag busca saber que servicios estan corriendo en los puertos abiertos y que versiones tienen. Asi puedes indentificar si hay software que podria ser vulnerable.

## -O (OS detection)
este flag intenta adivinar que sistema operativo esta usando el dispositivo. Analiza como responde a los paquetes que envias, lo que te ayuda a conocer mejor la red.

# ¿Existe algún flag que permite hacer un escaneo involucrando todos los flags mencionados anteriormente?
si existe, se pueden combinar varios flags en un solo comando en Nmap para realizar un escaneo mas completo. Se puede usar el siguiente comando:
 ```bash 
        sudo nmap -sS -sT -sV -O el ip target
```
pero sin embargo, debemos tener en cuenta que algunos de estos metodos son mutuamente excluyentes, normalmente, elegiriamos uno de los metodos de escaneo de puertos para evitar conflicos. 

# Explicar el proceso de un handshake TCP.
el handshake TCP es como una conversacion para establecer una conexion entre dos dispositivos, como una computadora y un servidor. Podemos describirlo mediante los siguientes pasos:
1. paso 1: el cliente llama
la computadora cliente envia un mensaje al servidor diciendo que quiere conectarse a esto se le conoce como SYN.
2. paso 2: el servidor responde
el servidor recibe el mensaje y responde con otro mensaje diciendo recibi tu solicitud y tambien quiero conectarme esto se conoce como SYN-ACK.
3. paso 3: confirmacion final
el cliente recibe la respuesta del servidor y dice, perfecto, estamos conectados esto se le conoce como ACK.

una vez se completan los tres pasos, la conexion esta lista y ambos dispositivos pueden empezar a intercambiar datos.

![syn](/assets/images/syn.png)

# Según la pregunta anterior, ¿qué significa el flag -sS?
el flag -sS en nmap se refiere a un SYN Scan, que es un tipo de escaneo de puertos.
Syn scan es un metodo que envia un paquete SYN osea una solicitud de conexion a los puertos del objetivo para ver cuales estan abiertos. El escaneo Stealth no completa el proceso de conexion. Si un puerto esta abierto, el objetivo responde con un paquete SYN-ACK, y nmap envia un paquete RST para cerrar la conexion antes de completarla. De esta forma se hace mas dificil detectar por sistemas de seguridad, ya que no deja un rastro claro de una conexion establecida. Ademas este metodo es rapido y efectivo para identificar puertos abiertos sin alterar demasiado al sistema objetivo.

# ¿Qué hace el flag --script?
en nmap se utiliza para ejecutar scripts de NSE(Nmap Scripting Engine) durante el escaneo. Estos scripts permiten realizar tareas especificas y avanzadas que van mas alla de un simple escaneo de puertos. Puede detectar vulnerabilidades, recopilar informacion adicional sobre servicios, o realizar pruebas de seguridad especificas en los servicios de un puerto.
Se puede espificar un script en particular o incluso un grupo de scripts para personalizar el escaneo segun tus necesidades. por ejemplo, podemos buscar vulnerabilidades en un servicio HTTP con el script:
 ```bash 
        sudo nmap --script http-vuln-* ip del target
```
