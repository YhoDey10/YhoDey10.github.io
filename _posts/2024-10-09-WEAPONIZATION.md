---
title: Weaponization
date: 2024-10-09 16:22:00 -05:00
categories: [Reconnaisance, Kill Chain, Pentesting]
tags: [nmap, kali, metasploit]  # TAG names should always be lowercase
---

# WEAPONIZATION
la fase de weaponization armado es donde un atacante prepara las herramientas y metodos para llevar a cabo un ataque. se procede a describir de forma que se entienda mejor:

1. que es weaponization?
- es el proceso de crear o configurar un arma digital como un exploit o un payload que se utilizara para atacar un sistema especifico.
- tiene como objetivo convertir la informacion recopilada en la fase de reconocimiento en una forma que pueda ser utilizada para comprometer el objetivo.

2. Eleccion de herramientas
- se debe seleccionar un software o herramientas que se alineen con las vulnerabilidades identificadas. por ejemplo: metasploit o malware, para explotar vulnerabilidades y para infectar el sistemas, respectivamente.

3. creacion de un payload
- un payload es el codigo que se ejecutara en el sistema objetivo. puede ser un virus, un script o una herramienta que permita el acceso remoto.

4. combinar herramientas y payload
- integrar el payload con el metodo de entrega, esto podria ser un archivo adjunto en un correo electronico o un enlace a un sitio web malicioso.

## visualizacion del proceso de Waponization
![visualizacion Weaponization](/assets/images/wea.png)



podriamos dar un ejemplo practico:
1. paso 1: recoger informacion sobre el software, versiones o configuraciones.
2. paso 2: escoge el metasploit como herramienta
3. paso 3: crea un payload que permite acceso remoto.
4. paso 4: prepara un docuemnto de word que al abrirse ejecute el payload y comprometa 




# Script de enumeracion de usuarios SSH
el Script ssh_enumusers de metasploit es una herramienta diseñada para eumerar cuentas de usuario en un servidor SSH.
el objetivo principal del script es intentar identificar que cuentas de usuario estan disponibles en un servidor SSH. esto sera util para preparar un ataqye posterior, como un ataque de fuerza bruta.

## Funcionamiento
el script evnia intentos de auntenticacion SSH a un conjunto de nombre de usuaro, puede ser una lista proporcionada por el usuario. Para cada nombre de usuario, intenta autenticar utilizando una contraseña vacia o una lista de contraseñas si se proporciona.
Si el servidor responde con un mensaje que indica que la autenticacion ha fallada para un usuario especifico, el script puede inferir que el nombre de usuario es valido. Tambien tiene en cuenta las respuetas de errores para determinar si un usuario existe.

## configuracion del Script
1. abrir metasploit
```bash 
        msfconsole
```
2. cargar el Script
```bash 
        use auxiliary/scanner/ssh/ssh_enumusers
```
3. configurar las opciones
establecer la direccion IP del objetivo
```bash 
        set RHOST <target_ip>
```
4. ejectuar el SCript
```bash 
        run
```
# resultados esperados
al finalizar, el script proporcioanra una lista de nombres de usuario validos que han sido identificados en el servidor SSH.

# condiciones de seguridad
Este script debe ser utilizado solo en entornos donde tengas autorizacion, como en pruebas de penetracion controladas. 
los intentos de enumeracion pueden ser detectados por sistemas de seguridad, asi que es importante ser consciente de las implicaciones.

**El script ssh_enumusers es una herrameinta efectiva para la enumeracion de usuarios en servidores SSH, permitiendo a los pentesters identificar cuentas de usuario validos que pueden ser el objetivo de ataques posteriores.**

# Script para la obtencion de contraseñas SSH
el script ssh_login de metasploit se utiliza para llevar a cabo ataques de fuerza bruta y obtener contraseñas de usuarios en un servidor SSH. a continuacion se detalla su funcionamiento y caracteristicas:
- su objetivo es de intentar autenticas usuarios en un servidor SSH utilizando una lista de nombres de usuario y contraseñas, su objetivo es acceder a cuentas de usuario validas.

- el script envia intentos de inicio de sension al servidor SSH utilizando combinaciones de nombres de usuario y contraseñas, puede utilizar una lista de usuarios y una lista de contraseñas para realizar el ataque.
-  si el servidor responde con un mensaje de autenticacion exitosa, el script identifica la combinacion de usuario y contraseña como valida. Si la auntenticacion falla, el script continua probando las siguientes combinaciones.

# configuracion del script
1. abrir metasploit
```bash 
        msfconsole
```
2. cargar el script
```bash 
        use auxiliary/scanner/ssh/ssh_login
```
3. configurar las opciones
establecemos la direccion IP del objetivo
```bash 
        set RHOST <target_ip>
```
establecemos la lista de nombres de usuario
```bash 
        set USER_FILE <user_list.txt>
```
establecemos la lista de contraseñas
```bash 
        set PASS_FILE <pass_list.txt>
```
4. ejecutar el scvript
```bash 
        run
```

**este script ssh_login es una herramienta poderosa para la obtencion de contraseñas de usuarios en servidores SSH, permitiendo a los pentesters acceder a cuentas mediante ataqyes de fuerza bruta.**

# resultados
al finalizar el Script deberia proporcionarnos cualquier combinacion de usuario y contraseña que haya tenido exito en la autenticacion.



# ¿En qué lenguaje de programación está hecho?
Bueno el script auxiliary/scanner/ssh/ssh_enumusers de metasploit esta en el codigo de lenguaje de programacion Ruby. Metasploit utiliza Ruby como su lenguaje principal para la creacion de modulos y scripts, lo que permite personalizar y extender sus funcionalidades.



