# Unidad 2


## 🤔 Fase: Reflect

### Actividad 07

#### Parte 1: recuperación de conocimiento (retrieval practice)

1. Explica cómo se representa y manipula un puntero en el lenguaje ensamblador de Hack. Describe las operaciones equivalentes a p = &a (asignar dirección) y *p = 20 (escribir a través del puntero) usando instrucciones de ensamblador

Un puntero lo represento con @p y en esta dirección es donde guardo la dirección a donde quiero apuntar. A  a p = &a sería equivalente a @a que es el valor, luego D=A, después @p y ya con M=D se le está asignando a p la dirección de a. Ahora para *p = 20  empiezo con @20, después D=A y @p. Luego se pondría A=M para que p apunte y finalmente M=D para guardar el 20.

**2. ¿Cómo implementarías el acceso a un elemento de un arreglo, como arr[j], en lenguaje ensamblador? Describe el rol de la dirección base del arreglo y el índice j en esta operación.**

No me quedó clara la última activdad de apply así que no estoy muy segura de como se haría. Creo que crearía donde guardar el arreglo y luego j y haría D=D=A para que se sumen. La dirección base es donde comienta el arreglo y el indice j sería una especie de contador.


#### Parte 2: reflexión sobre tu proceso (metacognición)


**1. ¿Cuál fue el concepto más abstracto o difícil de “traducir” de C++ a ensamblador en esta unidad (punteros, ciclos, arreglos)? ¿Qué hiciste para lograr entenderlo?**

Los punteros fue lo más difícil, especialmente en la última actividad, eran muchísimas cosas a tener en cuenta.

**2. En la Actividad 06 se sugirió construir el programa “PASO A PASO mediante pruebas”. ¿Cómo te ayudó este enfoque a manejar la complejidad del problema?**

Personalmente no me ayudó, hizo lo contrario. Debido a tantas pruebas me quedaban  muchos bloques de código y me perdía en qué estaba haciendo.


**3. Esta unidad fue el “puente” hacia C++. ¿Qué concepto de bajo nivel te sientes más seguro de poder identificar cuando lo veas implementado en C++?**

Me siento más cómoda identificando los if y while.

---

### Actividad 08 - Coevaluación.

**Copia la URL de un compañero**
https://github.com/jfUPB/computacionales-2025-20-EstefaniaAO

**Describe detalladamente qué pruebas vas a realizar para saber si el programa funciona correctamente. Reporta los resultados de las pruebas.**
Seguí paso a paso lo que decía mi compañera para verificar que estuviese correcto. Lo haré únicamente con los que confirma que funcionan ya que se muestre una reflexión del error.

  Si se crea el arreglo.
<img width="1004" height="476" alt="image" src="https://github.com/user-attachments/assets/ec8ae027-dd09-46f6-aa1a-ec133ff03fe9" />

El código final funciona.
<img width="1842" height="406" alt="image" src="https://github.com/user-attachments/assets/2b653d37-5d39-4353-8430-a4f473968665" />


Hizo un buen análisis, cada una con su objetivo, predicción, prueba y reflexión. Me gustó esa forma de trabajar, es organizada y hace enfásiis en entender qué se aprendió. En el futuro lo quiero usar para códigos pero que no sean tan largos ya que personnalmente pierdo la concentración. Me pareció muy interesante ver como escribía varias veces un código que no existía, eso demuestra que hace un gran esfuerzo por pensar en la lógica de cómo funciona el programa.


---
### Actividad 09 - Feedback
**1. Continuar: ¿Qué aspecto de las actividades, las explicaciones o la dinámica de la clase te ha resultado más útil o te ha gustado más y debería seguir haciendo?**

Me gustó que en clase hicieramos gran parte del set-seek porque me sirvió para comprender mejor conceptos, las explicaciones en clase me parecen muy útiles y me parece que sirven para llenar vacíos.

**2. Dejar de hacer: ¿Qué aspecto de la unidad te ha resultado confuso, poco útil o frustrante? ¿Hay algo que crees que debería eliminar o cambiar drásticamente?**

La última actividad de la fase apply, me pareció muy frustrante y confuso, me hubiese gustado que en clase empezaramos a crearlos juntos para tener más clara la lógica y el como crearlo y depués terminarlo individualmente.

**3. Empezar a hacer: ¿Qué te habría gustado que hiciéramos que no hicimos? ¿Tienes alguna idea para una actividad o un recurso que podría mejorar el aprendizaje en la próxima unidad?**

Lo mismo que mencioné en la actividad pasada. Me hubiese gustado que en clase empezaramos a crear entre todos el punto de la fase apply para tener más clara la lógica y depués terminarlo individualmente. Así creo que hubiese tenido más claro como abordar el problema.

**4. Ritmo y Dificultad: en una escala del 1 (muy fácil/lento) al 5 (muy difícil/rápido), ¿Cómo calificarías el ritmo y la dificultad general de esta unidad? ¿Por qué?**

Le doy un 5, la última actividad me pareció muy difícil y con la metodología se me complicó aún más.

***5. Comentario Adicional: ¿Hay algo más que te gustaría compartir sobre tu experiencia de aprendizaje en esta unidad?**

Me siento satisfecha con la fase de set-seek, siento que aprendí y las explicaciones en clase me sirvieron. No la sentí forzada y me pareció que tenía una dificicultad progresiva. En cambio, la de apply me pareció muy difícil de abordar.





