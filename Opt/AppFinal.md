# Optimizaciones para la APP final

Normalmente en el ecosimtea TSN nos encatgamros en las optimizaciones de bajo nivel de forma "enferma" tratar
de que sea lo mas rapido posible, pero en las "partes" altas no quiere decir que no hacemos
optimziaicones, de hecho si las hacemos pero ahi ya priorizmaos mas un balance 
ya no tanto "optimizacion " a muerte o sacrifciando legiblidad, etc...
Entonces aqui en este doc resumo optimizaiones a aplicar en las apps finales
Una app final es aquella que ensambla varias libs y aplica una logica de negocio propia..
es como la capa final.. un Ea, utilidad, CLI, etc..

## Defiiniciones
1. tipo simple: Con tipo simple me refiero a numeros y a tipos con un tamaño menor a < 12 bytes que no ocupen mucho 
y quepan en registros..... es lo opuesto a un tipo "compljo" como un string.. 
o un objeto clase  o un struct con varios campos, o arrays dinamicos...

## Funciones

Dentro de cada funcion de logica de negocio y "helpers" normalte, a que tener en cuenta
que las funciones aqui en mql, como tal no esta mal usarlas, pero a que hacerlo bien..
Pero antes de empzar mencionare 3 tipos:
1. Funciones como OnClick, etc que te provee un framework o hooks, esass implicaimtete y boviamtne su cuerpo
no se puede inlinear.. la clase como tal necesita ese mecanimos.. ahora lo que importa es en si, 
que haces dentro de esas llaves??
2. Dentro de esas llaves hay logica de negocio... entonce ahi es donde entran las funciones helpers
y las de "logica pura" las separo asi.. las que son mas candidato a inlining (que es
la optimzaicno que noramte suelo aplicar a funciones) son las helpers, ahora el compilador 
tambien inlinea eso es verdad pero no sabemos cuando.. entonces masomenos con la experiencia que tengo
tengo dos capas del cuando fiarse y no..
1. Si la fucion no retorna nada o reotra un tipo simple.. y se cumple que:
- el cuerpo de la funcion es corto, indexa una talba, un ternario, sumas, multiacoines simples, un acceso a tabla
Entonces psioblte puedas confiar en el compilador.. ahora si la funcion reotnra.. un tipo complejo o 
las operaiocnes son mas ambiguas quizas ahi si valga la pena inlinear... o mejor usar macros (#define)
Ahora para inlinear se debe de cumplir que:;
- Esa funcion no sea recustiva
- El codigo no sea tan grande, ahora aqui un matiz.. y entra en juego que tantas veces se usa
si se usa una vez depenide de uqe tan compljea se la funcion o si por reuqierimi se reuqier una funcion dejalo como esta
pero si la funcion es corta 10-90 lineas y no afecta alflujho inlineala...
vs si se usa arias vfeces esta funcion con mas de 10 lineas entonces primero evalua si peudes
usar macros ... pro ejemplo si es un bucle o una suma.. cabe en macro y no es tan complejo si hay mas logica
3 a mas bucles acceso a arrays o fors\while con cuerpo ahi quizas valga mas una funcion para comodidad.




## Strings 
Nomralte en apps finales es necesaior tbrajar con estos, enviar mensajes, hashmaps, etc...
Entonces sabemos que la concatenacino y deolkver strigns pro funciones implica copias, (y aveces no se opimza a moves)
asi que la idea es usar string... pero hacerlo bien, sigue estas optimizaciones: 
1. static: Usa static en string temporels, o cuando armas un string.... esto solo aplica a strings que "uses" una vez
si lo pasas por potas funciones, o paramotrs hay que tener mas cuidaod viendo la cadena de depcnias..
2. str.Reserve(): Usa una reserva incaila para que la concatenacion no sea tan costosa
3. StringInit(): Si sabes que el string es de tamaño fijo y lo llenas en una iteracion (algo simple no tanto un patron
builder donde ya se comkica caluarl el len etc etc..) entonces usa string init.. para setear el len ezacto y combinalo
con SetChar para setear el caracter.
4. Funciones: Si tu funcion devuelve string.. revisa si en vez de eso peude ser void y reotna el string por & refrencias.
5. Reutlizacion: Si nota qeu su codigo usa muchs strings para una "parte 1" o "parte 2"
por ejemplo:
```mql5
string emoji = value == x ? ... : ... ;
string msg = value == y ? ... : ...
string full =  "Open in: " +  msg;
string send = StringFormat("%s | %s", emoji, full);
Send(send);
```
Aqui se crean un monton de strings, entonces la idea es reutlizar un unico string para todo, siemrpe que podmaos
por ejemplo emoji quizas aqui como depende de un string antes y7 no podemos mutar su estado lo dejamos tal cual
pero msg... lo podemos reulziar por ejemplo asi: 
```mql5
msg = "Open in: " + msg;
msg = StringFormat("%s | %s", emoji, msg); // o tambien emoji + " | " + msg (es mas rapido. .que un format)
Send(msg);
```
Con esto evitamos varias copias y no perdemos la semantica...
aparte con un reserve bueno (heuristica), esto mejora:
```mql5
static string msg;
msg.Reserve(256);
```
Nota que aqui uso static dado que si podemos verificar que:
- El primer uso del string es de asignacion =
- En caso antes de esa sainacino se llame a una funcion veriicamos que esta la asinga antes de leer estado
Entonces es seguro si por ejemplo la funcion que llammoas necinta ya un stirng con ceirto valor entonces esa
funcion iria luego.. no ANTES.. ..la idea es eso..

7. Funciones "despachadoras": un ejemplo:
```mql5
string Emoji(int valor)
{
 if(valor==1) { return "..."}
 else if(valor==3) {return "..." }
 .
 .
 .
}

```
Este tipo de funciones son medio costoas asi que lo mejor es pensar en esto:
- si el valor es numerico: 
> - El valor esta acotado?¿ o es un bool...: usa una tabla constante o un uchar[fixed_size] si contruyes un buffer en vez de string, esto es comun pro ejemplo
con enums.. ENUM_POSITION_TYPE que tiene dos valores 0\1 o ENUM_ORDER_TYPE, por dar algunos ejemplos.. depend edel enum, etc..

> - Si el valor es mas complejo... entonces peudes probar con bit tricks quizas un brujin que mappee un patron de bits.. 
a una poscion de la tabla de 32/64/16 posicone sy usar un string ahi...
> - Otra opcion es usar perfect hash... (poir eemplo con SimpHash) pero esto solo si justica 10+strings en juego y patron complejo
> - Por ultimo si valor es medio compejo de mapearlo o dende de logica seuncinal.. peudes algemos reoduanr el if poir mas "probale" o como arbol binario  
> - En todo caso ya diste por todas las oslcuiones....  me poondira a pneasr que tanto se llama.. o si es critico para evalaur quizas un perfect hash mas heleprs o
acpetar el traderoff si no se llama mucho, o como mencione inlinearlo almenos (aunque zuais esto no sea la mejor opcion en codigo grande)



6. Usa const string&: esto es una optizmacion basica... noramlte en funciones pasas string pero como ya lo mecione
al no poder ver un asm etc.. no sabemos si se crea una copia completa.. o el compialdo optimzia y lo usa como con string& 
o toma pretad el puntero... etc.. pro eso es mejor aseguraranos.... aveces la difnica se nota y aveces no 
depende de lo que hagas con ese string, aparte el compiadlr no estan agresivo.
Ahora no siempre lo usamreos hay un problea con usar constr string& y es que no peudes hacer esto
funcion(Funcion2()) solo esto:
funcion("hola") o funcion(var)...
Esto por qeu const string& pide una variable y parece ser que apra "" se genrea una temporal et (la verdad es un ahipotesis
no una afrimacion) el tema es que con Funcion2 parece que se genrea un valor temporal el cual no "podemos" tomar
hay que matiel en un registro.. en ese caso duplicar una funcion completa para ofreces dos veriones
lo miraria con pinzas si la ufncion es chica o con un aglortimo que poco cambia quizas si con un amcro 
si es el core logic.. ahi si por tradeoff quizas acpetar eso... y usar const string que en teoria podria ayudar al compilador..

7. Funciones que retornan string cuestan mas que las que lo pasan como ref.. trata de que 
cuando uses strigns no usar much ofuncioens que lo retorne,

8. Si los strings son globales\const, usa uchar fixed[5] para repsetnarlos y copiamos con arraycopy (en buffer) o en la foramd el paso 9...

9. CharArrayToString no siempre es mas rapido que for() arr[i]=(uchar)StringGetCharacter() ... depende del tamaño  (alrediode de  < 60 chars)..
Asi que ve rotando... apart ienes que evaluar si reuiqer utf8 o es "plain asssci" basico para aplicar esta optimcion



## Logs (Prints)
En apps finales los logs son parte de esta el uso de print, etc...
Aqui normlte con el eocimtea TSN se suel combinar con CLoggerBase o CSpecilizedManger para "propagar los flags de logs" a otros
componentes.. aunque cabe reusltar qeu noramte el patron es el siguiente:
- APPS Finales: Usar prints es toatlte valido.. la idea es log error cuando ocurre un error.. y si la clase o lib que usas
tiene una  funcion tipo ErrorInfo o forma de presentar el error usala, si no quizas te porvea un LastErr que peudas usar
con EnumToString o formatear...
- Libs: Aqui NO se deberia de usar print, la idea es el patron de m_last err + getter, dado que la lib no debe de deicidr
sobre esto, lo hace la app final (en que idiam mostar el print, como lo foramte, o si lo guarda en un archivo, o lo renderiza
en un gui, etc etc).

## Varialbes muy usadas
Si notas que una varialbe mieobr de un class\struct que tengas en cierta funcion se usa muchas veces, entonces
puedes crear un const T temporal para cachearla... 

## Punteros
El costo de resolver un poiuntero peude costar.. en loops calintes como iterar sobre un array que esta en un m_ctx.m_data
en mucha siteraicones o loop calitne ahi resolver el punteor es cosoto lo mejor es crear una funcion helper que pida
el array por refencia asi la idea es reoler el punteor una vez.. ..
esto solo aplica cuando se usa mucho.. si se usa unas pocas veces o no en loops no tine snitgdo pagar el overdera de un calling
a funcion


## Funciones extra
EL ecosimtea TSN promeve aveces alternativas a las fucnioens nativas de MQL5 en varios frentes (son mas fast).
como:
- Crypt*: En vez eso puede usar CryptByLeo para crypto, y solo base64 usar lo nativo
- Conversiones, files (utils extra), etc: MQLArticles\Utils prove varias utiliades mas rapidas
que las nativas para conversiones... de string a numero\dobuel o integer a string... o utilidades con string, archivos, etc..
no reivente si no use...

> Ahora mismo a decir verdad no tengo mapeado la "alternativa" a la nativa
> Quizas luego lo haga pero lo dicho noramlte investige primero si hay algo que peuda remplzar lo nativo
> en MQLArtilces u otros repos y uselo... pero antes algunas funciones son "reservadas" para uso interno..

## Notas finales
Por ahora estas son las optimcioens que recomendare en APPS finales ire mejorando esto





