---
layout: post
title: "Como cargar tu app en un iPhone usando iTunes"
date: 2013-07-11 20:06:59 -0300
comments: true
categories: iTunes, iOS, XCode
---

Hoy tuve que mostrar una aplicación para iPhone a un cliente remoto, la idea 
era que probaran la aplicación en su dispositivo móvil antes de subir todo 
a la AppStore. 

Para realizar este proceso existen aplicaciones como 
[Testflight](https://testflightapp.com/ "TestFlight") o 
[HockeyApp](http://hockeyapp.net/ "HockeyApp"), que simplifican bastante el 
 proceso y permiten cargar remotamente una app teniendo el id del dispositivo.

A modo didáctico quise entender que es lo que hacen estas aplicaciones para
llevar la aplicación al teléfono, por lo que en este post explicaré como hacer
el proceso utilizando sólo iTunes.

##Agregando el dispositivo al Provisioning Profile

Lo primero es asegurarnos que el dispositivo del cliente esta en el 
**Provisioning Profile**. Para ello 
[necesitamos su UDID](http://bjango.com/help/iphoneudid/).

Teniendo el identificador del dispositivo, lo agregamos en 
[http://developers.apple.com](http://developers.apple.com)
como se indica en esta pregunta de 
[Stack Overflow](http://stackoverflow.com/questions/3578158/adding-devices-to-team-provisioning-profile).

##Generando el archivo IPA

Lo segundo es generar un 
[archivo IPA](http://en.wikipedia.org/wiki/.ipa_\(file_extension\)) con tu App,
para ello realizaremos lo siguiente:

Ir a XCode y seleccionar **iOS Device** en la lista de dispositivos 
como en la imagen.

![](images/posts/2013_07_11_1.png)

Luego ir a la pestaña de **Product** y elegir **Archive** como en la foto.

![](images/posts/2013_07_11_2.png)

XCode compilará la aplicación y al finalizar, tu App aparecerá archivada en la 
pestaña  **Archive** en el **Organizer** de XCode. Si todo esta en orden, hacer click
 en **Distribute**.

![](images/posts/2013_07_11_3.png)

Aparecerá una pantalla donde se pregunta como distribuir tu aplicación, en ella 
elegimos **Save for Enterprise or Ad-Hoc Deplyment**. Luego seguir las 
instrucciones y guardar el archivo IPA.

![](images/posts/2013_07_11_4.png)

##Cargando la App con iTunes

Con el archivo IPA localizado, abrir **iTunes** e ir a **File > Add to 
Library ...*** o presiona ⌘+O y elige el archivo **.ipa**.

![](images/posts/2013_07_11_5.png)

Ahora conecta el dispositivo, espera a la sincronización y luego hacer click en 
en el botón de iPhone como en la imagen y luego ir a la pestaña **Apps** en la 
sección de iPhone.

![](images/posts/2013_07_11_6.png)

Finalmente encuentra tu app, la instalamos:

![](images/posts/2013_07_11_7.png)

y le damos al botón **Sync**.

![](images/posts/2013_07_11_8.png)