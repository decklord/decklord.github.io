---
layout: post
title: "Guardar y cargar cookies en Objective-C"
date: 2013-09-11 21:06:59 -0300
comments: true
tags:
- ios
- objective-c
- enumerators NSArray

---

Por lo que he visto, cargar y guardar cookies para persistir sesiones en un
servidor remoto es un tema muy recurrente en Objective-C.

Navegando en las preguntas de StackOverflow me encontre con alguien que pedía 
[justamente eso](http://stackoverflow.com/questions/14387662/afnetworking-persisting-cookies-automatically/14405805#14405805)
a lo cual le respondí, por lo que aprovecho de compartir el snipet acá en un post.

Usualmente el servidor remoto nos envia un *hash* de la sesión en los headers de 
la respuesta HTTP. El objetivo es almacenar este valor en cookies dentro del 
dispositivo para usarlo más tarde.

La típica situación para esto es, por ejemplo, un login. Luego de que la sessión se
acepta es importante almacenar la cookie pues de lo contrario, al abrir nuevamente 
la app, perderemos la sesión.

<!-- more -->

Lo anterior se puede lograr utilizando *NSKeyedUnarchiver* y *NSKeyedArchived*.

Para guardar la sesión:

{% codeblock lang:objc %}
- (void)saveCookies{
 
    NSHTTPCookieStorage *storage = [NSHTTPCookieStorage sharedHTTPCookieStorage];
    NSData *cookiesData = [NSKeyedArchiver archivedDataWithRootObject: [storage cookies]];
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    [defaults setObject: cookiesData forKey: @"sessionCookies"];
    [defaults synchronize];
 
}
{% endcodeblock %}

Este método se debe invocar después de que recibimos la respuesta del servidor. 
Por otra parte, cuando iniciamos la App es necesario cargar esta info:

{% codeblock lang:objc %}
- (void)loadCookies{
 
    NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults];
    NSData *sessionCookies = [userDefaults objectForKey:@"sessionCookies"];
    NSArray *cookies = [NSKeyedUnarchiver unarchiveObjectWithData:sessionCookies];
    NSHTTPCookieStorage *cookieStorage = [NSHTTPCookieStorage sharedHTTPCookieStorage];
 
    for (NSHTTPCookie *cookie in cookies){
        [cookieStorage setCookie: cookie];
    }
 
}
{% endcodeblock %}

En este caso, lo ideal es llamar este método en el *App Delegate* al comienzo de
la app.

