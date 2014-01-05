---
layout: post
title: "¿Trabajas en muchas cosas y te cuesta retomar el hilo?"
date: 2014-01-05 10:56:32 -0300
comments: true
categories: todo-list gtd productivity
---

#TL;DR

Si trabajas en muchos proyectos, dispares entre sí, retomar el hilo conductor de una tarea específica toma tiempo. Mantener una lista de tareas que te permitan recordar que hacías la última vez que que trabajaste en algo puede ayudar. Además, una breve nota para ti mismo al final de la jornada ayuda a retomar el trabajo con fluidez a la mañana siguiente.

<!--more-->

# Dafuq I was doing yesterday

Los últimos meses he tenido mi cabeza ocupada con varios proyectos dispares. Aplicaciones [para iOS como freelance][1], hacer APIs, escribir en un Blog que nadie lee y unas cuantas aplicaciones web con [Django][2].

[1]: https://itunes.apple.com/cl/app/siga-chile/id688969871?mt=8
[2]: https://www.djangoproject.com/

Cada vez que quiero retomar una de estas cosas, me cuesta recordar en lo que estaba trabajando en el minuto que me detuve. Eso complica las cosas, pues es difícil entrar en [la zona][3] cuando no tienes idea de lo que hay que hacer. Más aún, cuando dejamos una tarea a la mitad o estámos trabajando en sólo un proyecto y éste es bastante complejo ocurre lo mismo.

La idea de este post es llevarle la contra al dicho:

{% blockquote %}
El que mucho abarca poco aprieta.
{% endblockquote %}

Claramente el tipo que lo inventó no sabía organizarse *:P*.

[3]: http://en.wikipedia.org/wiki/Flow_(psychology)

#Las todo-list

En mi anterior post, [El paradigma del hacer y el por qué evitar las reuniones][4] mencioné las *todo-list*. Manejar una pequeña lista de tareas ayuda mucho a llevar la pista de nuestro trabajo cuando cambiamos de contexto. 

[4]: /blog/2013/12/23/el-paradigma-del-hacer-y-el-por-que-evitar-las-reuniones/

Actualmente, existen mútiples formas de llevar *todo-list*, tanto personales como en equipo: Aplicaciones web, archivos de texto plano, plug-ins en editores de texto o simplemente papel y lápiz. A continuación voy a comentar brevemente el estado del arte en este campo a la fecha.

##Aplicaciones

Acá nos encontramos con muchas alternativas para todo tipo de perfiles. Si eres fan de Gmail y te gusta la integración, una buena alternativa puede ser [Google Tasks][5] o el nuevo [Google Keep][20]. Otra que me gustaba hace varios años por su simplicidad es [Todoist][6].

Pasando a aplicaciones un poco mas robustas, tenemos [RememberTheMilk][7], [Wunderlist][8], [Evernote][9] y finalmente [Trello][10] el administrador de proyectos genérico de los creadores de [StackOverflow][19], que también mucha gente esta usando como *todo-list*.

[5]: https://mail.google.com/mail/help/tasks/
[6]: https://todoist.com/
[7]: http://www.rememberthemilk.com/
[8]: https://www.wunderlist.com/
[9]: https://evernote.com/
[10]: https://trello.com/
[19]: http://www.stackoverflow.com
[20]: https://drive.google.com/keep/u/0/

##¿Y para los hackers?

Perfecto, vamos por parte. Para los más hackers existen alternativas notables. Acá la cosa se pone más ruda. 

###Dropbox

Lo primero y quizás más simple: Sincroniza un *todo.txt* en [Dropbox][11], si quieres llevarlo un paso más allá esta [Todo.txt][12].

[11]: http://www.dropbox.com
[12]: http://todotxt.com/

###Plugins en editores de texto

Como buen hacker tu mejor amigo es tu editor de texto, entonces, ¿qúe mejor que manejar el *todo-list* en mi editor? Si eres fan de *vi*, te puede interesar [Quicktask][13], para *emacs* está disponible [orgmode][14] y para *Sublime Text* esta el tremendo plugin [PlainTasks][15], que se puede installar usando [Package Manager][16]

[13]: http://quicktask.aaronbieber.com/
[14]: http://orgmode.org/
[15]: https://github.com/aziz/PlainTasks
[16]: https://sublime.wbond.net/

###Gist

Recientemente en [hackernews][17] estaba dando vueltas un artículo de [Carl Sednaoui][18] sobre cómo usar un [Gist][21] como un efectivo *todo-list*. Vale la pena leerlo.

[17]: https://news.ycombinator.com/
[18]: http://carlsednaoui.com/post/70299468325/the-best-to-do-list-a-private-gist
[21]: http://gist.github.com

## El problema de la todo-list y mis experimentos

A pesar de ser un usuario constante de las *todo-list* para ordenarme, a veces me quedo corto. Tener que llevar un control de todos los proyectos en los que me desenvuelvo a veces se pone caótico. A pesar de saber en qué tarea estoy trabajando, no se *exactamente* qué estaba haciendo.

### Git diff

Para solucionar lo anterior, a la hora de programar, estoy intentando acostumbrarme a *no hacer commit en la última media hora de trabajo*. La idea es que a la mañana siguente puedes hacer:

{% codeblock lang:bash %}
git diff my_file
{% endcodeblock %}

Al leer los cambios te da una idea bastante clara de lo que hacías, sin embargo, para esto hay que ser riguroso, estar haciendo commits contstantes es importante, de esta manera si pierdes tu código, no es mucho. Otro punto negativo es que es un poco lento leer cada archivo. Esto se puede combinar con lo siguiente:

### Escribir una nota para tu yo del futuro
#### El método irreverente

Acá existen variaciones. Estoy probando con un archivo por proyecto que se llama *dafuq_i_was_doing_yesterday.txt*, lo mantengo en el *.gitignore* de mi proyecto. Acá escribo una nota sobre lo que estoy haciendo en los últimos 5 minutos *antes de irme o terminar de trabajar*. La gracia de esto último es que no necesitas programar nada, simplemente se puede hacer con una nota en un post-it o en un archivo de texto sincronizado con *Dropbox*. Junto con *git-diff* se vuelve el método más efectivo que he encontrado hasta el minuto para retomar un proyecto.

#Conclusiones

En la actualidad hay muchas formas de organizar en tareas, depende de cada uno que método resulta más efectivo, desde aplicaciones hasta un simple papel, probablemente hay mecanismos que aún no conozco y que salen del alcance de este humilde artículo.

Todo esto apunta a maximizar tu concentración lo antes posible para poder llegar a *tu tope de productividad*.

Y tú estimado lector ¿qué métodos usas?
