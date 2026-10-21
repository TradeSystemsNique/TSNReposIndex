# Modelos LLM en MQL5 (Lo que pienso)

## Introduccion basica
Los modelos de IA LLM en MQL5, son herramientas y utilidades que han venido para quedarse, considero que son muy utiles... sobretodo en diseñar y debatir arquitectura en los muchos proyectos que tuve.. y tambien en aprender nuevos conceptos e ir mas profundo en lo que se..


## Por que MQL5 es un lenguaje especial

Considero que este es el pilar que puede explicar el rendimiento de todos los modelos LLM de IA hoy en dia a la hora de codificar MQL5. 
Reconoscamos lo siguiente de MQL5

1. Es un lenguaje diseñado especificamente para el trading.
2. Es un lengauje nicho de nicho (economia/trading/algo_trading).
3. No hay abundante documentacion en MQL5, y la oficial en su gran parte es firma\como usarla, no de bajo nivel, y lo mismo pasa en casi todas las libs.
4. Es un lenguaje cerrado.
5. Es un lenguaje atado a una plataforma de ejecuion (MT5 Terminal).
6. Casi el 90% a mas.. de los que lo usan no son programadores o tienen un background o estudios fuertes en software general.
7. No tiene gestor de paquetes oficial.

### Quien la forma
Normalemnte como mencione MQL5 esta formado sobretodo por traders, aproximo que entre el 85-95% que usan MQL5 son traders.. lo cual implica que:
1. Se valoren mas los productos finales frente a liberias (esto pesa mucho).
2. La escritura del codigo en general.

### El nicho al cual pertence MQL5
Debido a que estamos en el nicho del trading y aparte el punto de que MQL5 es un lengauje cerrado... esto implica que la cultura aqui sea mas de cerrar de que abrir.. los EAs.


### Calidad del codigo

La calidad del codigo publico en MQL5, sobretodo en codigo reutilizable (librerias) es poco comparable al codigo mainstream.. Esto por muchos factores:
1. El motivo por el cual se compartio dicho codigo.
2. Quien lo contruye
3. Que motivos hay por seguir mantiendolo
4. Que problema busca resolver.

Por ejemplo en mi tiempo investigando y formandome en MQL5 he notado estos patrones sobre los puntos mencionados:
1. Normalmente en MQL5 las liberias son contruidas por traders\devs que buscan solucionar su problema en concreto.. esto es lo comun.. por ejemplo una lib JSON para parsear.. normaemnte el trader\dev contruira una lib tomando conceptos y aprendio de otros lengaujes o en genera  y contruira algo que funcione con su caso de uso, que por lo general en MQL5 es hablar con APIs, Esto influye mucho en la vision que hay en una libreria... por que en MQL5 se busca lo que mencinoe resolver un problema y compartirlo, Raramente buscar, pulir, mantener, ser estrictos (en caso sea un protocolo), buscar seguridad en el codigo.
2. Principalmente traders como mencione y tambien devs, esto implica muchas cosas... como en su mayoria son traders la calidad se centra mas que todo en que funcione.. no tanto en "arquitectura", "que pase todos los test", "fuerte a entradas adversariales" (parsers por ejemplo), "que sea rapido de ejecutra", "que siga los patrones ....", etc.. por lo cual dicho codigo se caracteriza mas en resolver el problema qeu en lo mencionado.. y de la forma mas simple y rapida de codificar posible, esto sobretodo pesa mas en librerias, lo cual cambia completamnte la forma en la que se evaluan las liberias en MQL5 (mas luego explicaremos esto)
3. Pocos, normalemtne se sube una vez y luego se actuliza y luego para... el punto es que en mql5 de las pocas formas que sobreviva este codigo es que el autor lo use de verdad en su codigo critico y el autor viva del trading o de programar en MQL5 (osea uqe no sea un "experimento", "algo temporal para un EA" y lo mas fuerte que no sea codigo "vitrina", con esto me refiero al tipico codigo que sirve para "jalar" en un embudo para venderle señales, EAs, etc.. uqe es muy comun en mql5 codebase), raramente los codigos del codebase cumplen ese criterio, por lo cual terminan siendo abondanos, por la falta de tiempo, o por que el autor ya no lo usa, o de plano fue temporal su pase sobre el trading.
4. El codigo del codebase busca resolver el problema de su autor.. por lo general, el codigo de otros lengauje tambien pero hay una diferencia importante sobretodo en "formalidad" por ejemplo en parsers.. esto se ve mucho.. noramlte el codigo mql5/codebase tiende a ser algo mas simple y laxo para el caso de uso tipico y espeico de apis, casi nunca esta preparato "para todo" como si las libs de otros lenguajes que los "ojos" que la ven ponen mas presion sobre dicho codigo, aparte de que ahi el incentivo es otro.. (presitigio, trabajo, reconocmiento) asi que hay mas en juego.. Aparte mencionar que usualemte el problema mas comun en codebase a resolver en general es Gestion de riesgo, Gestino de posiciones, Operaciones, Indicadores, Estrategias, Utilidades GUI... y ya temas algo mas "salidos del spectro" como Genericos (hashmaps, mapas, btree, parsing, crypto, math, dbs, algorimts) son escasos y de calidad baja-media.

Ahora sobre la calidad en si del codigo, por todo lo que mencione situaria que el 85-90% del codigo del codebase es un codigo simple de entender y que resuelve el problema pero pobre en optimziaciones, arquitecuta, "stricidad", battle-tested, velocidad, entre otros... luego un 8-9% restante es un codigo con mas arquitectura, quizas algo mas de "stricidad"... y < 1% es un codigo variado pero apunta a "arriba" quizas un codigo "fast" mas estricto etc.. pero casi nunca llega "codo a codo" con una lib mainstream de lengaujes mainstream en los aspectos mencionados.
Por ejemplo JSON.. la mas popular JAson.. una lib que funciona para el caso de uso tipico, respuestas de api.. pero si planeas usarlo para casos mas "complejos" como:
1. Parseo de cientos KB a varios mb de JSON
2. Entradas que tu no controlas
3. Flujos de alta frecuencia (como scalping)
4. Que sea RFC stricto
5. Errores informativos

Es una lib que se qeuda corta rapido.. 
Y este es un patron que se repite con muchos temas.. 
Y para "rematar" como mencione incialete, cuando mas te alejas del trading core, menos hay... entonces hay temas que simplemte no hay libs..
como YAML, Crypto, Big Integer, LLM, MCP, entre otros.. 

### Donde hay codigo ?
1. Codebase MQL5: Quizas el lugar con mas codigos MQL5.. hay de todo EAs, liberias, etc.. pero para descargar el codigo hay qeu tener una cuenta en MQL5.com y registrarse (o tambien usar un URL directa lo cual es mas "escondido y poco comun")
2. Market MQL5: Tambien un buen lugar, pero el codigo es .ex5, no hay codigo fuente, solo algo listo para usar.
3. Github MQL5: Historicamnte donde mas libs ha habido y en promedio las mas populares de una calidad mas superior que la del codebase... Actualmente se ha convertido mas en un codebase 2.0 con mas EAs que libs..
4. MQL5 Articles: Quizas no este el codigo completo, pero hay fragmenteos rodeados de explicaciones paso a paso y de calidad variada, asi qeu esta mas enfocadno en aprender que en "usalo".



## Calidad de los LLM en MQL5

Debido a todo lo anterior que he mencionado ya se pueden ir haciendo una idea del codigo del cual se entrenaron los LLM en general..
Asi que en resumen tendriamos que en promedio:
Un codigo afinado para un caso de uso y de poca calidad.. en un sitio donde los crawrles no lo pueden bajar o solo su descripcion y poco mas...
Esto hace uqe el codigo con el cual los llm se hayan entrenado en cantidad junto a los docs, arituclos, github, etc... sea de calidad media-baja.. lo cual es algo que se nota y es evidente.... 
Es algo que lo he notado mucho cuando traajo con lenguajes que la IA se desenvuelve facil y rapido, por ejemplo en python ahi itera rapido se deseuvel bien, pocos errores, en cambio en mql5 el ciclo es mas lento... mas pesado mas tedioso.. y si no sabes MQL5 es peor.. por que trata de trasaldar cosas de cpp a mql5.. lengaujes que se parecen, pero en sintaxis, fuera de eso casi nada.
Esto sobreotdo se nota en codigo mas "pesado" o "general".. .. pro ejemplo liebrias de bajo nivel, integracion con protocolos, liberias ultra-fast, optimizacion ce codigo, opencl, etc etc.. temas complejos donde hay poca cantidad o nula...


## Vibecondig en MQL5
Como he mencionado anteriormente depende fuertemtne del tipo de codigo de MQL5 que quieras hacer.. esto va bien correlacionado con lo qeu hablamos.. si es un tema comun... que pro ejemplo buscnado arituclos o en foros haya muchas disciuens o varios topics... seguramente sea un tema qeu buena dominancia..
Si vez que es un tema que casi no hay codigo pocos arituclo y los que hay son bien dudosos... posiblemten sea un tema donde el modelo tienda a fallar mas.. y esto se empeora con temas cada vez mas y mas complejos.. y con poca presencia...
Esto impacta muy fuerte en el tema de velodiad de codifiaion, errores, y solcuinoes... asi que no creo que peudas ir tan fluido cono en py.. etc..
Por que:
1. El tema te lo limita (esto pesa mucho si no sabes mucho sobre MQL5 y quieres "fluir")
2. La plataforma tambien te lo limita (hay que correr el mt5 ya sea con el .ini o a mano y reportar resultaods, proceso tedioso)


## Optimizacion
Este sea quizas de los peores temas para trabajar con un modelo de IA..
Por que:
1. Si ya el codigo normal es escaso y de poca calidad, aqui es casi nulo... el tema de la optimziaicon de codigo, y codigo rapido es algo super nciho concentrado en pocas personas con conimiento qeu tira mas a dev que a trader.. y de esa gente poca es la que comparte.. quizas unos 50-100 usuarios en mql5...
2. Depende que tan lejos quieres llegar, quizas si solo quieres dar un salto "1", baste con mejorar las allocaiones, uso de strgins, arrays, funciones, etc.. osea aplicar teoria "basica" que puede o no que funcione y la unica forma es probar.. y justo es eso lo que mas "jode" en mql5.. por que el tema de probar, formulzar hipoteiss, etc.. es algo costoso en tiempo... incluso usando modelo sde ia  y conocimeinto para hacerlos.. por eso casi nadie lo hace...  Yo por ejemplo definira la optimzaicon en varias etapadas a) Donde se toma un codigo "simple - funcional" y aplicamos conceptos generales.. que pueden o no funcionar....  b) aqui con un codigo "rapido" seguimos dandole otra pasada donde buscarmoes ahora si cosas probadoas yq eu funcionen de verdad ya no solo teoria para ir rapido, esta es la etapa lenta consiste en probar y error.. y formular hipotesis c) etapa final investigar aun mas mas algoritmos, volverte enfermo por cada if, calling, memoria, acceso, etc... Y aqui pesa un monton que tanto TU sepas.. si solo le dices optimziara aplicara la pasada #a conceptos basicos.. y generales que pueden o no funcionar en MQL5.
3. Lo mas "jodido": El lenguaje es cerrado.. esto para empezar implica uqe no peudes ver un "ASM" o las instrucciones de bajo nivel del CPU.. para poder mejorar y afinar al compilador.. Aparte de uqe como mencione los docs en MQL5 son "a nivel de usuario, te doy las firmas, como usarlo, y ejemplos" no te epxlican lo de "bajo nivel" como esta implemntadno en CPP, que usa pro debajo? que algoritmos? etc etc... lo cual nos ayuda a optimizar mucho.
4. El compilador.... esto es un error fuerte que vi en los modelo sde IA .. asumir que el compilador de mql5 es comparable a gcc\clang\llvm\MSVC.. y esto se nota un monton a decir verdad.
5. Pensar que MQL5 <-> CPP, note que varios modelos tratan de trasladar ideas de CPP\C a MQL5 como si funcionarian igual.. cosa uqe no.. mql5 es un lenguaje raro... sincermante hay cosas que itnen mas costo que en cpp... y asi.. y como mencione no se sabe.. solo hay una via, probar... no es uqe haya una tabla de bajo nivel del costo o a que se troducen o se si inlinea etc.. no hay..

Desde mi experiencia (y ya lo he demostrado en varios codigos, como JSON, etc donde hice benchs con modelos de IA) creo qeu en optimizaciones la brecha entre un codigo ultra rapido iterado en muchas pasadas frente al codigo generado es grande hablamos que 2 a 10 a muchas veces mas.. mas lento...  

 
   
## Mejorara la calidad de los modelos LLM en tema de bajo nivel o temas mas generales?

No creo, aqui mis razones:
1. Ahora mismo con la llegada de codigo de ia codebase github ya casi casi las libs, si antes eran minoria ahora lo son mas o de peor caidad.... por loq ue es triste verlo asi.. MQL5 como tal no ha llegado a "desarollarse" en tema de libs como si lo hicieron cpp\py, etc... y que le pase esto empeora la sitaucion que llevabamos
2. Github, ahora mismo si veis los recientes casi todos son EAs (a feca de estos ultimos meses setimebre del 2026) no se si esta situacion cambie... pero creo que pensar que en github esta el mejor codigo ahor amismo.. la verdad que no... historicamnte si ha tenido muchas libs interensates de MQL5.. pero ahora mismo creo que esto se esta trasnalfando a MQL5 Forge y tambien al codebase... aparte un patron intente es que las libs con mas starts de gituhb han sido creadas durante el 2015-2021 asi que croe que ese fue su "prime" de las libs en github luego de eso ya la siutacino empeo a decae y los mantendieso de las libs mas "gordas" de github.. se fueron de MQL5 a otros lenguaje so de plano desparecieron.....  Debido a esto el principal centro de donde la ia coje codigo para entenrarse parece no "mejorar" si no empeorar incluso
3. Hay un anuncio del 2025 donde MQL5 tendra un pacakge manager nativo que compilara en un EX5 final... en feautres del metaedtior.... si esto logra pasar... no tengo dudas que gran parte de las libs se mudaran a este sistema... haciendo que se reduzaca mas el nicho de devs de libs que puiblcian sus libs
4. La ia ya aprendio todo "lo que se peude" sobre mql5..
5. La inovacion en MQL5 es entorno al traidng (por ejemplo tema de ia..) no sobre "progmraicon en general" o "optimizacion de codigo".


## Entonces, como uso la IA para MQL5 ?

Primero, aprende MQL5.. este no es un lenguaje quepeudas vibecodear facil, sio si aprende almenos lo basico... las bases del lengauje... 
y esto depende mucho del nivel al cual programes.. si quireshacer codigo de bajo nivel habra que dedicar mucho tiempo a aprender conceptos de cpp y de prueba y error para "agarrar" y formar una heuristica de optimizacion.
Ahora, depende de uqe tan exigente seas con el codigo.. si quieres algo que "funcione y ya"
Pues puedes ir directo con los modelos de ia y dar uno que otro vistaso...
Ahora si quieres algo mas estircito, rapido, buena arquiteiucta, mas deabte...  si que te va a costar tiempo, y sobreotod tendras que tene una buena base... y ser capaz de tu optimizar el codigo sin ningun modelo de IA de por medio... en este caso el modleo de ia pasaria a ser tu ayudante.... 
Ahora fuera de esots dos temas hay tareas "mecanicas" no tan complejas como renombrar, traducir, entre otros que los modelos LLM ramnte se confunden asi qeu son temas seguros.. 

Pero lo que mas duele sinceramente es cuando quieres hacer proyectos grandes en MQL5.. como el lengauje no tiene libs... hay que reinventar o probar...lo cual se termina dicinedo al modelo LLM que lo haga..lo que considero qeu es ampliar mucho los errores que podrian haber.... 
Es por eso tambien que en Py vibecodear es mas simple, tiens ya todo resuelto, libs probadas, y hecas antes de la era "LLM" bien testeadas y con un ecopsitmea ya "casi resuelto" por lo qeu el LLM solo ensambla.. y ya... los errores disminuyen por que ya solo te enfocan en la logica de negocio..
No en libs de bajo nivel... que ya estan bien escritas.....
Pero en MQL5 esto no es asi.. no hay libs hay pocas y hay desconfianza... asi que por eso se termina reinviantado, y hay caosas tan delicadas como cryptografia, parsing, etc que cuqluier descuido es grave.... por que esas libs basimnte sontedran todo tu proyecto.. asi que no se....

































