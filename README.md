# 8dot8 CTF

[Compañero de crimenes: Federico Videla](https://github.com/acidobinario)

## hHIS

Tu primer caso será superar este sistema de autenticación, para poder acceder a la máquina y proseguir la investigación.

Sabemos que ha sido instalado en el siguiente host: **deneb.hackrocks.com:5000**

**NOTA**: ¡Ningún otro puerto forma parte del reto!

Si vemos el host en el navegador obtenemos:

![Host en navegador](./images/Screenshot%20at%202022-10-21%2023-40-20.png)

Nos indica que hemos respondido incorrectamente, a pesar de no haber interactuado con la aplicacion. Sin embargo al abrir el dominio en una terminal utilizando `netcat` obtenemos:

![Host en netcat](./images/Screenshot%20at%202022-10-21%2023-44-44.png)

Mucho mejor. Ahora enfoquemosnos en `Qbun wifil qum Muhncuai'm qbcny bilmy?`. Los rotation ciphers son faciles de reconocer:

![https://dcode.fr](./images/Screenshot%20at%202022-10-21%2023-53-18.png)

Ingresamos la respuesta (white) y obtenemos una segunda pregunta:

![Tai ymzk yqynqde oaybaeqp ftq Rqxxaietub ar ftq Duzs?](./images/Screenshot%20at%202022-10-21%2023-55-35.png)

Y despues de una rapida busqueda en google obtenemos nuestra respuesta:

![Nine members](./images/Screenshot%20at%202022-10-22%2000-05-01.png)

Finalmente, obtenemos la tercera pregunta:

![Last question](./images/Screenshot%20at%202022-10-22%2000-07-30.png)

Ni idea que significa esto

![WHAT???](./images/Screenshot%20at%202022-10-22%2000-10-37.png)

Pero si le damos enter, obtenemos la flag.

![haha](./images/Screenshot%20at%202022-10-22%2000-13-08.png)

## Broken Jar

Opino que este tendria que ser el desafio dificil, obtener la solucion nos costo casi 5 horas.

Descargamos el binario y lo ejecutamos, al tratar de ingresar como "superb admin" retorna un segmentation fault.

![Segmentation Fault](./images/Screenshot%20at%202022-10-22%2000-23-55.png)

Abrimos el binario en ghidra y revisamos la funcion `superb_admin`

![Superb_admin](./images/wd8yj6.png)

Si logramos setear el usuario en el `idx` 0 a `root`, obtendremos un shell. Tratemos:

![hehe](./images/Screenshot%20at%202022-10-22%2000-34-31.png)

Revisemos la funcion que anañe usarios

![add_user](./images/dwqmib.png)

Podemos ver que se realiza un `strcmp` el cual no nos permite ser `root`, entonces, que hacemos?

Debo admitir que nos quedamos atascados en esta parte, no tenemos mucha experiencia con binary reverse engineering, asi que comence a preguntar en grupos por ayuda. Por suerte, alguien vino a nuestro rescate y nos indico que este challenge se parecia demasiado al ejemplo dado en este [writeup](https://infosecwriteups.com/arming-the-use-after-free-bc174a26c5f4)

![i lol'd](./images/Screenshot%20at%202022-10-22%2000-53-20.png)

Probemos en nuestro binario

![1](./images/Screenshot%20at%202022-10-22%2000-58-44.png)

![2](./images/Screenshot%20at%202022-10-22%2000-59-42.png)

Funciono, probemos ahora en el server

![got the flag](./images/Screenshot%20at%202022-10-22%2001-04-05.png)

## One Man Chance

Este fue mucho mas facil que el anterior, creo que tuvo que ser clasificado como medio

Si revisamos el codigo podemos notar dos cosas

![code](./images/Screenshot%20at%202022-10-22%2001-20-24.png)

1. Tenemos el key `a`: `9123891238912389`
2. El key `b` es un numero random entre `0` y `99999`

Por lo que la decripcion de la flag es muy simple:

![decryption](./images/Screenshot%20at%202022-10-22%2001-25-27.png)

Obtenemos la flag encriptada desde el server:

![Encrypted flag](./images/Screenshot%20at%202022-10-22%2001-27-41.png)

Y realizando un bruteforce, la desencriptamos:

![Decrypted flag](./images/Screenshot%20at%202022-10-22%2001-29-43.png)
