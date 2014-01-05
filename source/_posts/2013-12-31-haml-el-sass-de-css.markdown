---
layout: post
title: "¡Nunca más escribas HTML!"
date: 2013-12-31 19:09:52 -0300
comments: true
categories: CSS HTML HAML HTML frontend
---
![](/images/posts/2013_12_31.jpg)

#TL;DR 
Si estás haciendo frontend usa HAML, no HTML, te cambiará la vida, lo prometo.

#Les presento HAML
Probablemente si no eres desarrollador las siglas *HTML*, *CSS*, *HAML* o *SASS* no tendrán ningún sentido. Si es así, recomiendo dejar de leer este artículo pues va orientado a programadores. Ahora bien, si eres programador y no te suena lo que es *HAML*, te recomiendo de inmediato reemplazar *HTML* por esta maravillosa herramienta.

Para los desarrolladores de *Ruby* posiblemente esto es archiconocido, pero para los que estamos en el mundo de *python* y *Django* es toda una novedad, al menos para mí.

<!-- more -->

#Descubriendo la herramienta
Hace unos días me entretenía programando una app web para análisis de texto y estaba absolutamente intoxicado escribiendo *HTML* para la parte de la interfaz gráfica. En ese minuto de colapso decidí buscar si existía algúna forma de escribir *HTML* un poco más amigable, como *CSS* usando *LESS* o *SASS*. 

Típico que tienes un *HTML* enorme, desordenado y muy difícil de leer. De alguna forma es muy complejo mantener las reglas del buen programador a la hora de hacer un template en *HTML* por que el idioma no lo permite, sencillamente es feo. Personalmente yo culpo de esto a los tags de cerrado y a las miles de repeticiones: div div div div div div (más de ésto después).

Mi primer resultado en [Google][4] fue [HAML][1] y vi la luz. Nativamente está para Ruby, pero existe su equivalente en Django: [HamlPy][2] escrito por [Jesse Miller][3] y que funciona *out of the box* con dos líneas de configuración en el *settings.py*.

[1]: http://haml.info/
[2]: https://github.com/jessemiller/HamlPy
[3]: https://github.com/jessemiller
[4]: http://lmgtfy.com/?q=sass+equivalent+for+html

#No querrás volver atrás

La syntaxis cambia brutalmente por tres razones. La primera es que **pythonizamos el HTML**. Una de las cosas geniales de Python es que no usa llaves, en su lugar el lenguaje te fuerza a seguir una indentación determinada y ser consistente en ello, por esto se evita el típico problema de: *¿Qué llave cierra qué cosa?*. HAML nos da este poder en HTML, por lo tanto, **te olvidas de cerrar los tags**, ¡Que maravilla!.

Lo segundo es que los parámetros de los elementos se pasan en formato *JSON*. Esto nos cierra el círculo de la consistencia, todo en lenguajes familiares que siguen un mismo patrón: JSON, indentación forzada, no más tags de cierres. Todo converge en un template legible, ordenado y mantenible.

El tercer punto es que sigue un gran principio: *DRY, don't repeat yourself*. Antiguamente para diagramar sitios web se usaban tablas. Luego, con las hojas de estilo *CSS* todo lo anterior se transformaron en miles de *divs*, transformándose en el tag más repetido por lejos. ¿Te imaginas no tener que repetir esto mil veces? Adivina...

#Las manos en la masa, ejemplos
Ahora veamos algunos ejemplos de la utilización de HAML.

##No mas divs.

{% codeblock lang:html %}
.small hola
{% endcodeblock %}
es equivalente a:
{% codeblock lang:html %}
<div class='small'>
    hola
</div>
{% endcodeblock %}
*wooooow*

##Anidando elementos
{% codeblock lang:html %}
.small
  %ul
    %li
      %p Estoy anidado
{% endcodeblock %}

Es equivalente a:

{% codeblock lang:html %}
<div class='small'>
    <ul>
        <li>
            <p>Estoy anidado</p>
        </li>
    </ul>
</div>
{% endcodeblock %}

##¿Parámetros?

Para agregar propiedades a un elemento html usamos *JSON*:
{% codeblock lang:html %}
%input{'type':'text', 'name':'dirty_text_field'}
{% endcodeblock %}
Es equivalente a:
{% codeblock lang:html %}
<input type='text' name='dirty_text_field' />
{% endcodeblock %}

##Anidando clases e ids

Se pueden anidar clases o ids escribiéndolos uno tras otro, incluso con parámetros:
{% codeblock lang:html %}
.small.blue.left#user-name{'placeholder':'something'}
{% endcodeblock %}
Es equivalente a:
{% codeblock lang:html %}
<div id='user-name' class='small blue left' placeholder='something'></div>
{% endcodeblock %}

#Conclusiones

Llevo usando *HamlPy* desde hace una semana y estoy encantado, vale la pena aprender la syntaxis y pasar por el breve setup inicial, ahora escribo código *HTML* mucho más rápido y editarlo se hace muy sencillo. Los invito a ver el proyecto en [GitHub][5] y probarlo ustedes mismos.

[5]: https://github.com/jessemiller/HamlPy

Hasta la próxima.

