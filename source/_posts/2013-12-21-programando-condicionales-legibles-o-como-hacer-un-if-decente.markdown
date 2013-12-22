---
layout: post
title: "Programando condicionales legibles o como hacer un if decente, primera parte"
date: 2013-12-21 01:25:29 -0300
comments: true
categories: if else condicionales mantenibilidad
---

###Los Condicionales

En la vida del desarrollador es necesario definir muchos condicionales. Con 
condicional me refiero a escribir un *if* en partes de tu código, lo cual
ocurre cientos, si no miles de veces en un software. 

Los condicionales son una pieza clave y si una cosa de este estilo se hace mal 
tiene un impacto incalculable en tu trabajo por dos motivos. El primero es que si 
definimos malos condicionales hacemos que el código tienda a tener errores y 
por otro lado dificulta su mantenibilidad, lo cual es tanto o más importante 
que lo anterior.

<!-- more -->

###Condiciones engorrosas

Ahora bien, ¿a qué me refiero con escribir *buenos* o *malos* 
condicionales? Pongámoslo en un ejemplo, supongamos que quiero validar un 
formulario de registro y me llega el usuario junto con el email:

{% codeblock lang:python %}

def validate_form(data):

    name = data.get('name', None)
    email = data.get('email', None)

    if not name:
        print "Error, you must enter a name"

    if not email or not re.match(r"^[A-Za-z0-9\.\+_-]+@[A-Za-z0-9\._-]+\.[a-zA-Z]*$", email):
        print "Error, you must enter a valid email"

{% endcodeblock %}

En el ejemplo anterior, la segunda validación de email es una expresión regular
que nos valida si el correo tiene el formato correcto. En validaciones de email
esto es muy común por lo tanto *inferimos* que se trata de eso. El problema
es que en la práctica hacer estas inferencias no es trivial, ya que típicamente nos 
enfrentamos a contextos desconocidos, el caso del email es la excepción a la regla.

¿Cómo se puede hacer esto más legible?

{% codeblock lang:python %}

def validate_form(data):

    name = data.get('name', None)
    email = data.get('email', None)

    if not name:
        print "Error, you must enter a name"

    #Yes, now I'm more legible
    if not email or not email_formatted(email):
        print "Error, you must enter a valid email"

#my name reveals my purpose
def email_formatted(text):
    #I add this variable to avoid a long ugly line
    regular_expression = r"^[A-Za-z0-9\.\+_-]+@[A-Za-z0-9\._-]+\.[a-zA-Z]*$"
    return re.match(regular_expression, text)

{% endcodeblock %}

Acá hay varias cosas que notar. Lo primero es que encapsulamos la lógica de 
validación en una función. Esto nos permite usar simplemente la función en
nuestro condicional y hacerlo más pequeño, lo que mejora su legibilidad. 

Por otra parte, la función de validación *tiene un nombre que revela su 
propósito*, esto es clave, nos permite leer la condición y determinar 
inmediatamente lo que hace el código. En este caso la función recibe un texto
y revisa si es *email formatted*, es decir, tiene formato de correo y se aplica 
sobre un string cualquiera. Más aún, al poner este nombre en la condición, se 
lee literalmente en inglés: *not email formatted*.

Por último y no menos importante, en la función de validación
separo en una variable la expresión regular, ya que nos ayuda en la legibilidad 
de lo que hacemos al tener dos lineas cortas y claras.

###Muchas validaciones

En ocasiones hay que validar muchas cosas para obtener un output concreto: 
Que el string contenga o no contenga algún parámetro, que sea de cierto tipo de 
dato, etc. Situaciónes como la siguiente:

{% codeblock lang:python %}

def validate_product(data):

    code = data['code']

    if code and len(code) == 26 and parametter[:2] == "01" and big_calculation(code) and parametter[:24] == "NN":
        print "The rabbit is in the hole"
    elif code and len(code) == 26 and parametter[:2] == "01" and big_calculation(code) and parametter[:24] == "PP":
        print "The rabbit is in the hole, but is from another kind"
    else:
        print "No rabbit :("

{% endcodeblock %}

El código anterior tiene varios problemas. Lo primero y mas evidente es que
se validan muchas condiciones y lo hace difícil de comprender, ni siquiera cabe 
en la pantalla, por lo tanto estamos violando [la regla de 80 caracteres](http://programmers.stackexchange.com/questions/148677/why-is-80-characters-the-standard-limit-for-code-width).
Por otra parte se repiten cosas en las dos condiciones, solo la última parte es
diferente, sumado a que estamos haciendo un *big calculation* dos veces.

####Agrupando condiciones en variables boolean autoexplicativas

Una manera de simplificar la legibilidad de un set de condiciones es unirlas en 
variables boolean. Por ejemplo:

{% codeblock lang:python %}
code_has_correct_format = parameter and len(parameter) == 26 and parametter[:2] == "01"
some_result_is_ok = big_calculation(parameter)
code_is_nn_kind = parametter[:24] == "NN"

if code_has_correct_format and some_result_is_ok and code_is_nn_kind:
    print "The rabbit is in the hole"
{% endcodeblock %}

Como se ve más arriba, transformamos condiciones que a veces no son tan claras
asignándoles un nombre que revele su propósito, como *code_has_correct_format*.

Por otro lado, se pueden juntar varias condiciones en una variable, siempre y 
cuando pertenezcan a un propósito común. En el caso del ejemplo, todas las 
condiciones que quieren validar el formato se fusionan en un parámetro con un 
nombre adecuado, en este caso: *code_has_correct_format*.

De esta manera, simplificamos la lectura, la cual se vuelve directa y evitamos 
la redundancia. Lamentablemente las validaciones de formato aún son muy largas, 
por lo tanto lo separamos en una función cuyo nombre describa su propósito.

{% codeblock lang:python %}
def validate_product(data):

    code = data['code']

    code_has_correct_format = code_formatted(code)
    some_result_is_ok = big_calculation(code)
    code_is_safe_to_use = code_has_correct_format and some_result_is_ok
    code_is_nn_kind = parametter[:24] == "NN"
    code_is_pp_kind = parametter[:24] == "PP"

    if code_is_safe_to_use and code_is_nn_kind:
        print "The rabbit is in the hole"
    elif code_is_safe_to_use and code_is_pp_kind:
        print "The rabbit is in the hole, but is from another kind"
    else:
        print "No rabbit :("

def code_formatted(text):
    return text and len(text) == 26 and text[:2] == "01"

{% endcodeblock %}

La función *code_formatted* en otros contextos no es trivial de inferir. Hacer
estas separaciones nos permiten tener una visión mucho más clara de qué se debe
refactorizar y cómo.

Eso por ahora, en la segunda parte hablare sobre la importancia de ser positivo
en los condicionales, cómo gracias a eso se puede aplicar [La Ley de Morgan](http://es.wikipedia.org/wiki/Leyes_de_De_Morgan) 
de lógica proposicional para hacer mejoras y otros temas relacionados.
