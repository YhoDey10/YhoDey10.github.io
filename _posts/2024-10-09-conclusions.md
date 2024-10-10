---
title: Conclusions
date: 2024-10-09 16:22:00 -05:00
categories: [Reconnaisance, Kill Chain, Pentesting]
tags: [nmap, kali, metasploit]  # TAG names should always be lowercase
---


# ¿Qué es lo que ha aprendido de esta sesión de laboratorio?

en esta secion de laboratorio se han abordado diversos aspectos relacionados con la seguridad informatica y la recopilacion de informacion para pruebas de pentesting o pentetracion. a continuacion detallaremos:
1. Reconocimiento: se aprendio la importancia de la fase de reconocimiento en la que se repoila informacion sobre el objetivo, utilizando herramientas como nmap para identificar servicios y sistemas operativos, y la necesidad de ejecutar estas herramientas con privilegios adecuados.
2. Escaneo con nmap: se exploraron diferentes flags de nmap como -sS, -sT, -sV y -O, y su funcion en el escaneo de redes. Se podria decir que se aprendio las combinaciones de estos flags para realizar escaneos mas robustos.
3. Handshake TCP: se esutdio el proceso de establecimeinto de conexiones en redes TCP, lo que fundamental para entender como funcionan las comunicaciones en red.
4. Weaponization: se revisaron scripts especificos para enumerar usuarios y obtener contraseñas SSH, aprendienod cobre su implementacion en Rubby y su funcionamiento.
5. Malware y persistencia: se discutio como se puede conciliar malware utilizando scripts como vssown.vbs, que permite acceder a copias de sombra para extraer informacion sensible.
6. extraccion de archivos criticos: se aprendio sobre los archivos SAM y SYSTEM, su funcion en la gestion de usuarios en windows y como se pueden extraer utilizando tenicas forenses.
7. aspectos eticos y legales: se enfatizo la importancia de realizar estas practicas en un entorno controlado y con los permisos adecuados para cumplir con las normativas de seguridad.

# ¿Qué herramientas nuevas ha añadido a sus skills?
este laboratorio se ha introducido varias herramientas y habilidades en el contexto de la ciberseguridad. 
- uno de ellos es el NMAP y su diferentes flags, comprender estas tecnicas de escaneo fue algo nuevo para mi persona.
- algunos scripts de metasploit para enumerar usuarios y obtener contraseñas en SSH.
- VSSown.vbs conocer este script para manipular copias de sombra de sistema windows.
- aprender la importancia de los archivos criticos SAM y SYSTEM en sistemas windows.

# Otros temas que Ud. considere importante mencionar

conforme fui averiguando y leyendo mas acerca del tema, me parecio interesante el tema de la etica y la legalidad en la ciberseguridad, la importancia de realizar pruebas de pentesting de manera etica con permisos adecaudos y respetando las leyes locales e internacionles.
Y otro tema seria la seguridad en la redes como comprender los firewalls, IDS/IPS, tecnicas de segmentacion de red.