---
title: METASPLOID
date: 2024-10-03 16:22:00 -05:00
categories: [Reconnaisance, Kill Chain, Pentesting]
tags: [nmap, kali, metasploit]  # TAG names should always be lowercase
---

# Que es Metasploid?
Metasploit es una herramienta de codigo abiero muy utilizada en ciberseguridad, especialmetne en hacking etico. Se usa para encontrar y explotar vulnerabilidades en sistemas informaticos.
Incluye mas de 900 exploits, que son metodos para atacar fallos en la seguridad. 

## Naveagacion 

### iniciando la consola de metasploit framework 
![figura1](/assets/images/image.png)

tambien se puede inciar metasploit en kali linux abriendo una consola de temrinal y escribiendo
![figura2](/assets/images/image2.png)

# Exploits 
un exploit es un software, un fragmento de datos o una seucencia de comando que aprovecha un error o una vulnerabilidad de una aplicacion o sistemas para provocar un comportamiento involuntario o imprevisto.

## Auxiliary/ Scanner / SSH/ SSH_enumusers

Este modulo perimite enumerar los nombres de usuario configurados en el servicio SSH de un host objetivo. Es util para identificar cuentas que pueden ser blanco de ataques posteriores, como fuerza bruta.

### como se usa ssh_enumusers
1. iniciar Metasploit

    ```bash 
    msfconsole 
    ``` 
2. cargar el modulo
    ```bash 
    use auxiliar/scanner/ssh/ssh_enumuser
    ``` 
3. configurar opciones
    establecer la direccion IP del objetivo:
    
    ```bash 
    set RHOSTS [IP_ADDRESS]
    ``` 
    opcionalmente, puedes configurar un diccionario de usuarios.

4. Ejecutar el escaneo 
    ```bash 
    run
    ``` 