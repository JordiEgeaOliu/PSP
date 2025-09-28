## **Bloque 0: Historial**

0. Amplía el tamaño máximo del historial de la shell y configura que cada línea del historial muestre también la fecha y la hora.

```bash
 export HISTISIZE=10000 # cantidad de comandos
 export HISTFILESIZE=20000 # tamaño del fichero de almacenamiento
 export HISTTIMEFORMAT="%F %T "
 
```

1. Comprueba que ahora, al mostrar el historial, aparece la fecha y hora junto a los comandos ejecutados.

```bash
history
```

2. Configura estos cambios para que sean permantentes
```bash
 vi ~/.bashrc

#dentro incorporamos esto

export HISTISIZE=10000 # cantidad de comandos
 export HISTFILESIZE=20000 # tamaño del fichero de almacenamiento
 export HISTTIMEFORMAT="%F %T "
```

---

## **Bloque 1: Gestión del sistema y el kernel**

1. Muestra toda la información de tu sistema operativo y kernel.
```bash
 uname -a
```
    
2. Averigua únicamente la versión del kernel.
```bash
 uname -r
```
    
3. Comprueba el espacio en disco disponible.
```bash
 df -h
```
    
4. Calcula cuánto espacio ocupa la carpeta `/etc`.
```bash
 du -h /etc
 
# buscamos ayuda
 du --help
 man du	
```
    
5. Consulta la memoria RAM disponible y usada.
```bash
 free -h
```
    

---

## **Bloque 2: Procesos**

6. Lanza un monitor de procesos en tiempo real y observa:
```bash
 ps aux
 #o
 top
 #o
 htop
	total de procesos 20
```
    
- Número total de procesos.
	
- Cuál consume más CPU.
	
- Sal del programa.
        
7. Instala y ejecuta una versión mejorada del monitor de procesos y compárala con la anterior.
```bash
 sudo aor install htop
 htop
```
    
8. Obtén un listado de todos los procesos del sistema y localiza el proceso de tu shell.
```bash
 px -lax

 # -l listado
 # -a ocultos
 # -x procesos del user actual

 #localizar
 ps -lax | greep tty
```
    
9. Muestra la jerarquía de procesos en forma de árbol.
```bash
 pstree
```
    
10. Lanza el comando `ping` contra `google.com` en segundo plano (&) y obtén su identificador de proceso (PID).
```bash
 ping google.com &
 ps aux | grep ping
 ps aux | head -n1
```
    
11. Finaliza el proceso de Firefox usando su PID.
```bash
 kill -9 1079 (el PID del proceso)
```
    
12. Vuelve a lanzarlo y esta vez deténlo, luego reactívalo.
```bash
 ping google.com
 (en otra pestana de terminal) kill -19 PID
 kill -18 PID
```
    
13. Crea un script que capture la señal de interrupción (Ctrl+C) y muestre un mensaje en lugar de cerrarse.
```bash

```
    pendientes...

---

## **Bloque 3: Gestión de servicios con systemd**

14. Consulta el estado del servicio de conexión remota (por ejemplo, `ssh`).
```bash
 ssh
```
    
15. Inicia dicho servicio si está instalado.
```bash
 sudo systemctl start ssh
```
    
16. Desactívalo del arranque automático y vuelve a activarlo.
```bash
 sudo systemctl disable ssh
```
    sudo systemctl enable ssh

---

## **Bloque 4: Archivos y directorios**

17. Lista todos los archivos, incluidos los ocultos, en tu directorio personal.
```bash
 ls -la ~ (-la dirve pra los ocultos y  ~sirve para mostrar los del directorio personal)
```
    
18. Crea una carpeta llamada `prueba`.
```bash
 mkir prueba
```
    
19. Dentro de esa carpeta, crea un archivo `notas.txt` que contenga el texto “Hola Linux”.
```bash
cd prueba
echo "Hola Linux" > notas.txt
```
    
20. Copia ese archivo con otro nombre.
```bash
 cd prueba
cp notas.txt notas_copia.txt
```
    
21. Renombra el archivo copiado.
```bash
mv notas_copia.txt copianotas.txt
```
    
22. Borra el archivo renombrado.
```bash
rm copianotas.txt
```
  ls- a para comprovar todo  

---

## **Bloque 5: Redirecciones y pipes**

23. Redirige la salida de un listado de archivos a un archivo llamado `listado.txt`.
```bash
ls > listado.txt
```
    
24. Añade una nueva línea al final del mismo archivo con el texto "Fin del listado".
```bash
echo "Fin del listado" >> listado.txt
```
    
25. Redirige los errores (2) de una operación no válida (`let a=3/0`) a un dispositivo nulo para ignorarlos.
```bash
	let a=3/0 2>/dev/null
```
    
26. Filtra de una lista de procesos únicamente aquellos que contengan la palabra “bash”.
```bash
 ps aux | grep bash
```
    
27. Muestra solo las últimas 5 líneas del archivo `listado.txt`.
```bash
 tail -n 5 listado.txt
```
    

---

## **Bloque 6: Tuberías con nombre y sockets**

28. Crea una tubería con nombre llamada `cola`.
```bash
 mkfifo cola6(se crea tuberia)
```
    
29. Desde una terminal, deja el archivo `cola` en espera de datos. Desde otra terminal, escribe un mensaje en esa tubería.
```bash
terminal 1 echo "hola" > cola
teminal dos cat < cola
```
    
30. Verifica que `cola` es realmente una tubería.
```bash
 file cola
```
    
31. Establece un canal de comunicación entre dos terminales locales utilizando una herramienta que permite redirigir flujos de entrada y salida entre sockets.
```bash
 nc -l -p 12805(modo server)
```
     nc localhost 12805
---

## **Bloque 7: Redes**

32. Comprueba la conectividad con el servidor `google.com` enviando unos pocos paquetes.
```bash
	ping -c 3 google.com
```
    
33. Muestra la configuración de tus interfaces de red.
```bash
	ip addr show
```
    
34. Revisa qué puertos están en escucha en tu máquina.
```bash

ss -tuln
```
    
35. Consulta la dirección IP asociada al dominio `google.com`.
```bash
 nslookup google.com
```
    
36. Realiza la misma consulta de resolución DNS usando otra herramienta distinta.
```bash
	host google.com
```
    
37. Conéctate de forma remota a otra máquina mediante un protocolo seguro (si tienes acceso).
```bash
(no tengo acceso pero seria)
 ssh nombremaquina@ip de la maquina
```
    
38. Copia un archivo desde tu máquina a otra mediante una conexión remota segura.
```bash
 scp /ruta/local/archivo.txt  nombremaquina@ip de la maquina:/ruta/remota/
```
    

---

## **Bloque 8: Usuarios y permisos**

39. Crea un usuario de prueba llamado `alumno1`.
```bash
  export HISTISIZE=100000 # cantidad de comandos
  export HISTTIMEFORMAT=%F %T "
sudo useradd alumno1
```
    
40. Cámbiale la contraseña.
```bash
 sudo passwd alumno1
```
    
41. Cambia los permisos de un archivo a `755`.
```bash

```
    
42. Cambia el propietario de un archivo a otro usuario.
```bash
chmod 755 listado.txt
```
    
43. Elimina el usuario creado.
```bash
sudo userdel alumno1
```
    

---
