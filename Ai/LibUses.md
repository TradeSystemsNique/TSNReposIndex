# Uso de modelos de IA en librerias

En MQL5 el uso de ia es menos "auto" que otros lengaujes main, esto lo dejo claro en Pensamiento.md
Pero aun asi hay muchas tareas en las qeu pueda ayudar en particular en liberias..

Lo primero, noramte al usar un agenet considero que hay qeu explicale muy bien el proeycto, dependie de que tan 
mencanica es la tarea, si es solo limpiar includes, corregir macros, o replace, o vericiar peude que no mucho
pero si en una lib por ejemplo un parser va tocar tema de layot, herencia (aun mecanio preo quiere saber como)
Es necesario documentarlo.. ahora mismo no tods los repos lo tiene a ese nivel, son pocos..
Asi qeu eso es lo primero, lo troo que considero es dejar bien claro la filosifia para no haber "cruzes" de esitlo...
El como se haran las cosas....

## Ooptimizacion 
Ahora tema deoptimizacion, aqui noramtle prefiero hacerlo manualmte o usar ia para prototipar ideas...
O pedir ideas pero combinarlos con heriusitcas propias, esto ya mencione por que... en Pensamiento.md
La optimcion en MQL5 es un tema costoso en tiempo y que reuiqre muhco conocimetino de prueba y error...
No solo teoria que es publica.. por como funciona el lengujae...
Ciermante los modelos tambien peuden optimizar... pero por lo qeu vi son optimzaiones mas simples.. no tan "salvajes"
o fuertes en capadiad exploratoria que uno con experienca tendira, aun asi resetio los siguientes usois
1. Maketar ideas\hipositeas a codigo MQL5 
2. Optimizacion base con herusitcas bases 

## Diseño de api
en TSN somos muy esitcos con esto, pro qeu meter mucho envoltorio peude implicar calling a punteors etc.
asi qeu tratamos de evitar hacelro muy "facil todo", si a un problema de api o como disñear las clsases hay una solaicion facil 
pero cimplica puintero etc... revisar primero qeu tanto se llaman consideor que si se laman almenso cada 1hora a mas peude no improtar
pero si es a cada barra o tick me preocuprari por eso es mejor pensar mucho esto.. no simptle ir a lo mas facil..
Es por eso qeu en TSN el diñseo de libs cuesta mas tiempo qeu hacerlo rapido.. nos enfocamso mucho en velocidad
y un diseño escalable... aun asi el disñeo de api se peude usar modelos para:
1. Definir herencias
2. Funciones, contructores, etc..


## No todo es optimizar
En ciertso casos, donde la mantebildiad o faiclid de agregar pesa mucho mas.. o solo se arrhoa un acceso a array ...
o no mcuho es prefierlo mantenible... si se ahora un puntero o algo un poc omas pesado e... pensaria uqe tan ciritoc y si aparota velocidad
dejarlo pooco mantlebi, quizas apostaria mas a por scirpts de py si se peude... depende del caso 


## Ressumen de usos
1. Optimizacion:
  - Maketar ideas
  - OPitmizacion con heristicas abses
2. Diseño de api:
  - Clases
  - herencia
  - Patrones
3. Mecanico:
  - Find\Replace fuerte
  - Cambios fuetes, o ayudas con cosas mencanicas    
  - Documentcoin (primera version luego como user modificar si hace falta, de paso encuntras ciertas cosas que puedes cambiar, etc..)
    
> Considero que una tarea mencia es aquella donde tiene poco qeu ver el razonar sobre la lib y se peude ejcutar sin sabes espeiccamten como fucniona
> cada cosa de la API o lib
> Inlcuso si llegas a documentar muy bien el proeycto puede ser que inclsuo te ayude con el desarollo de mas modulos ideas de api, extensiones..
> Pero solo cuando lo tengas muy bien en mente el proieycto y muy bien documentado para que no haya fallos cambios o "cruzes" de hacer las cosas
> Litelate que la ia sea un clon tuyo... quizas no al mismo nivel pero que te peuda seguir..... pero con sus litmeiaicones..
  
4. Encontra bugs
  - Refvision de codigo: y aqui justo es el mejor uso quizas que se le puda dar junto con eso.. vquizas que te acuerdes ceirtos patrons de diseño
  y pudar actulizar docs..  o debaitir soliucions, etc..
  
5. Tareas mas "extra"
  - Quizas un sitio web de la lib, videos, etc.., considero que a este punto ya la IA domina muy bien web.. 
    asi que le daira mas auto, aun asi consideraria qeu aprendas web alemnos los basicos como funciona html, como se redeniacas css, js..
    lo minnmo como par que peudas modiicar algo por tu cuenta o entener el codigo genricado, quiaz no tnato a un nivel de saberte untente como fucnion
    o hacer todo tu solo....   
    
6. Aprendizaje extra
  - Cuando optimizas, muchas veces no solo es reservar meroa, unrolling, y ya.. en mcuhso campos como crypto\math\parser neceitas
    aprender mas temas de compiladores, teoria de numeros, entre otros, aqui la ia te peude ayudar mucho a comprender codigo
    para portar o optimizar o apdatar...
    
7. Test:
  - Workflows .yaml
  - Test para la lib
  - FUzzing para la lib
  - CI y automatizaciones
  - Scripts para docs o asserts       
  


