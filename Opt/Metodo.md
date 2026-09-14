# Optimizacion en MQL5 (Fast)

Hola aqui detallare como es que suelo optimizar codigos como forma general, ciermante cada tema como parsing, math, big integers, crypto, ml el algoritmo o conocieminto en ese campo tiene mas peso que saber optimizar en el lenguaje com otal

## Partiendo de las sigueintes bases
1. MQL5 es un lenguaje cerrado por lo que no hay forma de ver un "ASM" o formato final de ejeucion, por esto portar algo "fast" en cpp a mql5 no garantiza que sea rapido dado qeu el compilador y el costo de las operaciones varian en mql5.. y mucho.. es todo un caso sinemante
2. Las docs de MQL5 no son tan profundas, si llegas al nivel mas "alto" programando mql5.. o requieres uso de funciones donde las docs son criticas como sockets o crypto te daras cuenta que en los docs oficilaes casi todo es a nivel de uusuario. osea firmas de funciones, que paramots recibe, etc... salidas esperadas etc.. y un breve resumen de lo qeu hace y codigos de ejmploe... pero detalles de que pro ejemplo intmwnte como es el algortimo exacto qeu usa (por jemeplo el AES de crypt encode\decode usa ECB? o BCBC?¿ como es el tema del pdding, o base64 permite WS?¿ o no? se permite inplace en cvrypto\encode decode o solo ciertos metodos) y asi hay un monton de ejemplos de "bajo nivel" que son critiocs para codigos ya mas avazandos... que MQL5 en sus docs no detalla y por eso hay que testear... lo mismo pasa con el compilador, solo sabemos que optimiza el codigo, pero no sabemos como?¿ acaso hace loop unrooling?¿ y si lo hace como es uqe toma la decision para hacerlo? y si se compila con avx2 ettc?¿ se vectorizan las operaciones?¿ o el costo de las operaciones com ola division etc?¿ como se implemetna, etodos estos detalles del compilador.. pro eso no podemos garantizar muchas cosas como que la division sera barata, o que el acceso del array no sera caso, o que cargar arrays globales en codigo hot pathj (pro ejemplo en parsers) no costara, todo eestos detalles imrotar para cada ms


## Un resumen de como lo hago

Ahora si lo que yo hago noramlte cuando suelo optimizar un codigo es primero plantear varias hipotesis "buenas" o "fast" que peudan resultar... por jemeplo evitar copias o predimensiar un array o engita la division, o evitar ramas, tambien hacer unrollings, o tenicas del dominio como usar el algirtmo B o A, o usar SWAR o no.. etc.., etc... una version base.. aparte aveces hay dudas dado qeu por ejemplo usar arrays lockup? o un brach?¿ todo esto se va resolviendo con las hiptoesis que se platnean. luego para iterar rapido suel ousar IA generativca para maquetar estas hipotesis.. en codigo... luego este codigo generado lo ejeucto... y tambine voy refinando al "ganador" una vez que y aestoy seguro.. paso este codigo a mql5...

## En que me enfoco a optimizar (consejos generales)
1. Tratar siempre de trabajr inplace todo lo qu ese peudal, crear copias es costos
2. La division.. ver una forma de calcular sus inveross o algo matemtais similar... (en mi experiendci optimizando muchos codigos, parece que incialte dirias, una division no peude ser tan cara, pero ewn mql5 por alguna razon puede hacer que un codiugo sea hasa 2 veces mas lento en benchs... asi que depeindeo del contexto... es preferible trmeplzaosl por inveros so otros algoritmos)
3. Este consejo es mas complejo por que no siempre funcoina pero siempre que peudas trata qeu todo este en "la pila" de la funcion y no usar varialbbes globales... esto lo he llegado a notar sobretodo en algoirtimos tipo de hashsing.. que quitan un static etc.. aumenta la velocidad de procesamiento.... en parte creo que se debe a que cargar variables globales reuiqer un loadk mas.... depiendo de como lo maneje el compialdor
4. Para copiar arrays usa ArrayCopy o Arrayinitiliza, si reuiqres copiar usa los meotods nativos son mas rapdios que un for..
5. En caso tengas funciones que reotnrn structs\class.. trata de tener un contrut que haga un "swap" para "robar" lops datos de las varaibles... esto es cirito si las clases tine arrays o obetjos pesados (pro ejemplo una clase de big integers, etc..), esto quizas en cpp se haga auto pero como no podemos garnatizlao en mql5 y aparte parece que el compilador optmiado no lo hace lo mejor es hacerlo manaul
6. Loop unrolling en cargas de datos.. esto lo he notado mucho cuando en parser (Swar pro ejempl) o en implemtnacion de algortimos que suelen tomar un array de entrada y proceslo... cada cmp del for peude pesar en ciertos casos
7. Calling a funciones: siempre que puedo tambine trato de inlinear lo que puedo... pero la idea es NO hacerlo todo inline pro qeu se vuevle ilegible.. si no un balance.. esyto tambien depende mucho del contexto... o del coidgo o de que tanto se llame a dicha funcion yu que parameos se les pasa.. aveces no cuesta nada aveces si puede tornar mucho tiempo, ahora una cosa ciermante el compilador si he notado que inline funciones pero creo que no es tan agreisvo como otros ocmpialdores si no mas simple si ve un calling directo o pcoas operacione ssi lo hace auto si ve mas logica parece uqe ya emite un calling real.
8. Preferir siempre todo lo que se pueda resolver en compilacion, siempre usa templates o "emula" el pasar parmaeotrs consatnes a clases\structs via tempaltes y un sizeof que se evalua en compilacion... este patron lo uso mucho en BigIntegers y SHA .. para evita crear copias... de las funciones.. y como las ramas de los fis condicioneslaes se evalacion en compilacion por lo visto se quitan..
9. En conceptos ICT o noticas por jeemplo en vez de usar names o events codes usa id (ulongs) es mas rapido.. comprar ulongs que strhins largos..
10. usa reservas en los arrays (tercer parametro.. o usa siempre un partron de array, size, reserve)

## TSN
El ecositema TSN se enfoca en maxima velocidad, por lo qeu adopto todos esots patrones, aparte en caso el ecositmea TSN incropope libeias de terceros como ya lo hicemos en PRNGByLeo o TimeUtils, etc.. siempre haremos test de velocidad, no cualquier lib se integra con el ecositemsa..

### Y todo el codigo del eocismtea TSN es optimziado ?
Sincermante No pero ya casi, ahora mismo diria que un 80-90% del codigo sigue estos enfoques de maxima velocidad. en las liberias.. siempre maxima.. en todo los campos ya sea crypto, numeros, math, ml, ict, news, parsing, vm, etc... siempre se aplica, hoy por hoy me enucntro mejorando las libs dado que el codigo legacy de los 2025 aun sigue patrons malos.. pero esto poco cambiara...

## Mensaje final
Yo como tal considero que lo que hay que optimziar al maximo son las bases, osea las liberias, como tal las app finales ahi ya me relajo mas... meto mas prints... y quizas uso punteors para ficlaita la lopgica de negicion, esto pro qeu se que las lbis por debajo como parsers, crypto, numeros, math, ml son muy rapidas... pero tampco oes que me relaje mucho siemprte uqe peudo lo trato de optimzar pero si veo que ya sera muy tedidio o compljo o predigo que no vale la pena lo dejo.


## Uso de modelos de IA
La IA a llegado para quedarse, pero hay que ser mas precavidos en MQL5... a diferencia de cpp\js\py donde hay inmensas bases de codigo de toda calidad... la ia ahi se pudo entrenar bien aparte de que dichos lenguajes son abiertos y sus compilares tambine por lo que optimziar ahi ya es mas faicl aparte que el compilador ya hace mucho trabajo por ti... asi qeu te enfocas ams ene el algopritmo com otal... 
Pero esto no es lo mismo con MQL5, este ultimo al ser nicho muy nicho y la calidad de codigo en su gran mayoria es codigo para trading.. entones lo que hay de "optimziaicon" o codigo rapido es poco y enfocado mas a indicadores. no tanto a un nivel "genral" por todo esto el nivel de los modelos de IA en mql5 es mucho mas infereicio si clos comparas haciendo codigo en otros lengaujes... y esto ya lo he demostrado mucho he publaico muchos repos en los que hago benchs contra codigos con ia.. normaliza cuando se les pide optmizar aplican conocimientos "generales" o que "teoricamtne se ven bien" mas que todo replican lo que hay de C++ pero como les he ido mencioando MQL5 para nada es CPP ... 
- MQL5 es menos agresivo compiladndo que CPP
- MQL5 no es abierto como cpp
- MQL5 la comunioda en su gran mayoria son personas que lo usan para autpmiza rsu estreateia, NO como algo general para codificar o optimziare agresiamnte
- MQL5, los docs no son de tan bajo nivel asi que leyendo ramente aprendes a optimizar
- en MQL5 tambien hay un nicho de gtente que optimzar el codigo.. pero esta bien contado y reducido y aparte esta invisible... si lo comparmos con la inmensa mayoria
- MQL5 el volumen de las libs es menos del 5% de todo el codigo mql5, esto lo peudes veiricar llendo al market, codebase, github
- El volumen de codigo "bueno - fast" es casi casi 0 en mql5.. si lo comparmos con las libs.. asi que normalte las LLm cuando optimzia trataran de protar patrones de CPP.... o otrs lengaujes.. dado que se "parece" a mql5.


Debido a todo eso se crea como una bola de nive eque empora la calidad de los modelos de ia codificando.. y peor aun si les pides "bajo nivel" maxima velocidad... 
Y si a esto le sumas que iterar en mql5 es mas tedioso pro que requiere de una APP GUI .. no un CLI o algo facil de usar.. entonces esto multiplica todo lo mencionado....

En resumen... los modelos de IA en MQL5 son decentes en temas generales de trading (lo que mas importa en MQL5) pero si te alejas de eso empizan a empoerar en caldiad mucho... es como una distyirbcino normal.. si preguntas temas normales, indicaodres, notiicas, ict o cosas no tan complejas te va bien ... pero si te aljeas mas y mas.. donde casi no hay docs o libs de ello (directx, onnx, optimizacion de codigo, parsers fast) depeindeo de que tanto te alejes te puedn dar: desde algo funciona pero "no lo que pensabas" (un fast parser) hasta dirmante no compilar o pasrarte dias dandole docs.. a la ia... (directx por ejemplo)

Asi que por esto no uso la ia como "mi remplazo" o alguien que lo "hace por mi" si no mas un "ayudante" que me ayuda a prototipar rapidos, sacar hipotesis.. y sobretodo aprebnder (Algoritmos, math, ml, etc en esto es muy buena dado que son temas generales y abunda el contenido..) o tambien en tareas mecanicas de pcoo peligro.. o cosas simples... o que te ayude a pensar la arquietucta, los archivos.... 

Aunque ahora con el ecositmea TSN en marcha ya toda esta parte compleja ...  ya ha sido resuelta progresivmatne asi que la ia se enfocara en loq eu de verdad ssabe hacer.. la parte final.. osea loas eaes.. digmoas un EA con LLm.. la ia ya no se enfoca en hacer el parser json, o hacer la lib de LLM si no en la logica de negicio como tal.. algo mas simple sn tanto estresd (osea en lo de alto nivel..) y asi tenemos muchos ejemplso..


### Pregunta amena, esta situacion con la IA mejorara?¿ 
Creo que no... o se mantendra.. o empeora incluso..
1. Ahora mismo con la llegada de codigo de ia codebase github ya casi casi las libs, si antes eran minoria ahora lo son mas o de peor caidad.... por loq ue es triste verlo asi.. MQL5 como tal no ha llegado a "desarollarse" en tema de libs como si lo hicieron cpp\py, etc... y que le pase esto empeora la sitaucion que llevabamos
2. Github, ahora mismo si veis los recientes casi todos son EAs (a feca de estos ultimos meses setimebre del 2026) no se si esta situacion cambie... pero creo que pensar que en github esta el mejor codigo ahor amismo.. la verdad que no... historicamnte si ha tenido muchas libs interensates de MQL5.. pero ahora mismo creo que esto se esta trasnalfando a MQL5 Forge y tambien al codebase... aparte un patron intente es que las libs con mas starts de gituhb han sido creadas durante el 2015-2021 asi que croe que ese fue su "prime" de las libs en github luego de eso ya la siutacino empeo a decae y los mantendieso de las libs mas "gordas" de github.. se fueron de MQL5 a otros lenguaje so de plano desparecieron.....  Debido a esto el principal centro de donde la ia coje codigo para entenrarse parece no "mejorar" si no empeorar incluso
3. Hay un anuncio del 2025 donde MQL5 tendra un pacakge manager nativo que compilara en un EX5 final... en feautres del metaedtior.... si esto logra pasar... no tengo dudas que gran parte de las libs se mudaran a este sistema... haciendo que se reduzaca mas el nicho de devs de libs que puiblcian sus libs
4. La ia ya aprendio todo "lo que se peude" sobre mql5..
5. La inovacion en MQL5 es entorno al traidng (por ejemplo tema de ia..) no sobre "progmraicon en general"


   







