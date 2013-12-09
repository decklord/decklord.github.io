---
layout: post
title: "enumerateObjectsUsingBlock, loops prácticos en Objective-C"
date: 2013-07-11 21:06:59 -0300
comments: true
tags:
- ios
- objective-c
- enumerators NSArray

---
Hace unos días estaba leyendo [NSHipster](http://nshipster.com/) de 
[Matt Thompson](http://mattt.me/) y descubrí un buen post 
acerca de *enumerators*. En el mencionaban como hacer un loop usando **enumerateObjectsUsingBlock**.

<!-- more -->

##Iterando sobre objetos

La típica forma de iterar sobre un objeto es la siguiente:

{% highlight objective-c %}
NSArray *someArray = [[NSArray alloc] init];
for (int i = 0; i<100; i++) {
    NSObject *object = [someArray objectAtIndex:i];
}
{% endhighlight %}

Lo malo es que esta forma es un poco engorrosa, pues hay que buscar el 
objeto usando el *índice **i***. Cuando no nos importa usar el índice lo ideal
es utilizar el modo *"forin"*.

{% highlight objective-c %}
for (NSObject *object in someArray) {
    [object someMethod];
}
{% endhighlight %}

Esta forma es mucho mas sencilla y limpia, utiliza *NSFastEnumeration* en su 
implementación, la cual es la manera más rápida de iterar sobre un objeto en 
Objective-C, incluso mas rápido que usar un *for/while* en C.

Ahora bien, ¿qué pasa cuando queremos usar este tipo de *for* y además queremos 
utilizar el índice? Volvemos a algo similar al primer ejemplo, o incluso peor. 
Se define el indice fuera del ciclo, de la siguiente manera:

{% highlight objective-c %}
int i = 0;
for (NSObject *object in someArray) {
    [object someMethod];
    //Do something with i
    i += 1;
}
{% endhighlight %}

##Una forma más limpia

En Objective-C existe una forma de declarar el índice y tener el objeto en 
una sola línea, esto se hace utilizando **enumerateObjectsUsingBlock**.

{% highlight objective-c %}
[someArray enumerateObjectsUsingBlock:^(id object, NSUInteger i, BOOL *stop) {
    NSLog(@"%@", object);
}];
{% endhighlight %}

Esta disponible para *NSArray, NSSet, NSDictionary y NSIndexSet*. Con esta 
manera nos olvidamos de declarar variables auxiliares.

El equivalente al *break* en este tipo de loops en hacer que la variable *stop*
tenga el valor *True*.

Una característica interesante de enumerateObjectsUsingBlock es su variante:
{% highlight objective-c %}
enumerateObjectsWithOptions:usingBlock:
{% endhighlight %}
La cual puede recibir un parámetro de tipo *NSEnumerationOptions*. 
Se puede, entre otras cosas, revertir el orden en el que se recorren los 
elementos usando *NSEnumerationReverse*.
