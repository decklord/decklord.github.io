---
layout: post
title: "Configurando GitHub Pages con nic.cl"
date: 2013-12-09 11:03:03 -0300
comments: true
categories: [nic.cl, githubpages, chile, octopress]
publish: false
---

En estos minutos estoy intenando linkear mi dominio http://clopez.cl
a [GitHub Pages](http://pages.github.com/). 

##Muerte a Tumblr

Así es, migre mi blog de Tumblr, pues como plataforma de 
blogging es una real basura. Sirve para fotos, pero escribir en tumblr es 
un asco, el espacio es pequeño y el editor en si es lento, falla y pierdes todo.

La tienes aún peor si quieres escribir un blog de programación, activar 
[colores en el código](http://decklord.tumblr.com/post/60947643317/add-syntax-highlight-to-tumblr)
no es directo y agregar código en sí en el editor html es *muy muy tedioso*.

Usando una plataforma pésima es malo, hace que escribas menos o directamente que 
no escribas nada.

<!-- more -->

##Migrando a Octopress

Buscando un poco llegue a Octopress, claramente *LA opción* para desarroladores.
Usa Markdown syntax para escribir los posts, por lo que puedo usar cualquier 
editor y lo hago en mi equipo.

Montar todo en Octopress tampoco es sencillo, pero si eres desarrollador 
el proceso puede ser entretenido. Una vez que tuve todo configurado para 
funcionar llegue a la parte de "¿Ya y ahora como conecto esto a mi dominio 
personal?". Desafortunadamente en [nic.cl](http://www.nic.cl) esto no es directo.

En nic hay que configurar los DNS, colocando un nombre de servidor primario y su
respectiva ip. Por otra parte, GitHub Pages no nos permite hacer esto tampoco.

Usualmente la configuración del dominio es sencillo cuando contratamos un servicio 
de Hosting pagado. Ellos te dicen cual es tu servidor DNS, su ip y en 5 minutos el 
problema esta resuelto.

Evidentemente no quiero pagar nada de eso, pues no usare el espacio de hosting. 
Descubrí entonces que lo que se necesita es un administrador de DNS que actua 
como *proxy* o nexo entre nic y donde estan los archivos.

##FreeDNS.ws es tu amigo

Buscando buscando encontre este sitio [FreeDNS](http://freedns.ws/). Lo mejor 
que tiene es que:

![](http://images1.wikia.nocookie.net/__cb20120228145016/inciclopedia/images/4/4d/Its_free.png)

Luego de crear la cuenta, tenemos que agregar una *Zona*.

![](/images/posts/2013_12_09_3.png)

En mi caso utilizo clopez.cl en *Domain Name* y como *IP Adress* hay que poner 
[la ip de GitHub Pages](https://help.github.com/articles/setting-up-a-custom-domain-with-pages#domains), 
*204.232.175.78*.

FreeDNS nos provee ahora las ips de servidor NS:

{% codeblock %}
ns1.freedns.ws
ns2.freedns.ws
{% endcodeblock %}

En nic nos piden la ip de dicho servicio, esto es facil de obtener, lo hacemos 
con el comando ping en la terminal.

{% codeblock %}
ping ns1.freedns.ws
{% endcodeblock %}

Deberíamos ver algo como esto

![](/images/posts/2013_12_09_1.png)

Ahí esta, la ip de FreeDNS es 188.190.119.10 para el ns1. Obtenemos la otra IP
haciendo lo mismo y en el panel de nic ingresamos los datos:

![](/images/posts/2013_12_09_2.png)

Son las 12:25 cuando termine de realizar estas configuraciones, en total el proceso
tomo X horas en completar.

