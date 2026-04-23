# Convenciones MQL5 - Ecosistema TSN

> Estándares y mejores prácticas para escribir código MQL5 en el ecosistema TSN

---

## Tabla de contenidos

1. [Nomenclatura](#nomenclatura)
2. [Estructura de archivos](#estructura-de-archivos)
3. [Estilo de código](#estilo-de-código)
4. [Estructura de EAs](#estructura-de-eas)
5. [Comentarios y documentación](#comentarios-y-documentación)
6. [Idioma](#idioma)

---

## Nomenclatura

### Clases
- **Prefijo:** `C`
- **Tipo:** `PascalCase`
- **Ejemplos:** `CMyClass`, `CIndicator`, `COrderBlock`, `CRiskManagement`

```mql5
class CStrategy {
  // implementación
};
```

### Interfaces
- **Prefijo:** `I`
- **Tipo:** `PascalCase`
- **Ejemplos:** `IStrategy`, `INotifiable`

```mql5
interface IStrategy {
  void OnTick();
};
```

### Estructuras
- **Prefijo:** Ninguno
- **Tipo:** `PascalCase`
- **Ejemplos:** `Bar`, `OrderData`, `SignalInfo`

```mql5
struct OrderData {
  ulong ticket;
  double price;
  datetime time;
};
```

### Uniones
- **Prefijo:** Ninguno
- **Tipo:** `PascalCase`

```mql5
union DataValue {
  double dval;
  int ival;
};
```

### Funciones
- **Prefijo:** Ninguno
- **Tipo:** `PascalCase`
- **Ejemplos:** `CalculateSma()`, `GetSupportLevel()`, `ApplyRiskManagement()`

```mql5
double CalculateSma(const double &series[], int period) {
  // implementación
}
```

### Variables miembro (de clase)
- **Prefijo:** `m_`
- **Tipo:** `snake_case`
- **Ejemplos:** `m_period`, `m_buffer`, `m_is_active`

```mql5
class CIndicator {
private:
  int m_period;
  double m_buffer[];
  bool m_is_active;
};
```

### Variables globales
- **Prefijo:** `g_`
- **Tipo:** `snake_case`
- **Ejemplos:** `g_risk`, `g_order_block`, `g_bar_manager`

```mql5
CRiskManagement* g_risk;
COrderBlockTick g_ob;
CBarManager g_bar_manager;
```

### Variables locales
- **Prefijo:** Ninguno
- **Tipo:** `snake_case`
- **Ejemplos:** `current_price`, `support_level`, `trade_signal`

```mql5
void OnTick() {
  double current_price = SymbolInfoDouble(_Symbol, SYMBOL_BID);
  int period = 14;
  bool is_valid = true;
}
```

### Parámetros de entrada (Input)
- **Prefijo:** `Inp`
- **Tipo:** `PascalCase`
- **Ejemplos:** `InpPeriod`, `InpStopLoss`, `InpTakeProfitRatio`

```mql5
input int InpPeriod = 14;
input double InpStopLoss = 50.0;
input string InpTelegramToken = "your_token";
```

### Constantes \ Defines \ Enums
- **Tipo:** `UPPER_SNAKE_CASE`
- **Ejemplos:** `MAX_ITERATIONS`, `DEFAULT_PERIOD`, `VERSION_NUMBER`

```mql5
const int DEFAULT_PERIOD = 20;
const double MAX_SPREAD = 0.5;
#define VERSION_NUMBER 100
enum ENUM_RISK_TYPE
{
 RISK_TYPE_PERCENTAGE,
 RISK_TYPE_MONEY
};
```
### Resolucion de contexto
En caso se usen librerias como winapi o las funciones interna de la clase\globales entran en conflicto con las nativas se recomienda usar "::" para indicarle a compilador que debe de llamar a dicha funcion nativa, en caso de llamar a funciones de lib como kernel32, por ejemplo para GetLastError(), puede resolver el contexto como "kernel32::GetLastError()"


---

## Estructura de archivos

### Jerarquía recomendada para EAs 

Para EAs **simples o mediamente complejos**, se recomienda dividir en los siguientes archivos:

```
EA_Name/
├── Global.mqh        (Inicialización global - PRIMERO SIEMPRE)
├── Defines.mqh       (Includes y variables globales)
├── Functions.mqh     (Funciones auxiliares)
├── Main.mqh          (Lógica principal/clases)
└── EA_Name.mq5       (Evento principal)
```

### Orden de includes

**Siempre** incluye `Global.mqh` primero para evitar errores de "Invalid Pointer" en instancias globales:

```mql5
// Defines.mqh
#include "Global.mqh"        //  PRIMERO SIEMPRE
#include <TSN\\MQLArticles\\Strategy\\Main.mqh>
#include "Functions.mqh"
#include "Main.mqh"
```

```mql5
// EA_Name.mq5
#include "Defines.mqh"       // Ya contiene Global.mqh
```

---

## Estilo de código

### Configuración del IDE MQL5

**Tools → Options → Stylizer:**

| Opción | Valor |
|--------|-------|
| Estilo | MetaQuotes |
| Sustituir tabulación por espacios |  Sí |
| Eliminar líneas vacías |  No |
| Insertar espacios después de coma/punto y coma |  Sí |
| Insertar espacios alrededor de operadores |  Sí |

**Tools → Options → General:**

| Opción | Valor |
|--------|-------|
| Tabulación (caracteres) | 2 |
| Insertar espacios |  Sí |
| Insertar () y {} ) ] " ' |  Sí |
| Resaltar paréntesis pareados |  Sí |
| Resaltar línea actual |  Sí |
| Activar historia del portapapeles |  Sí |
| Auto-lista de nombres |  Sí |
| Sangría automática |  Sí |
| Parámetros automáticos |  Sí |
| Números de líneas |  Sí |

### Atajo de teclado

- **Formatear código:** `CTRL + ,`, usar siempre cuando se termine de codificar algo.. 
- **Insertar header de función\clase\seccion general\include:** `CTRL + .`, usar antes de definir una clase o defines\enums\strucuts, funciones:

```mql5
//+------------------------------------------------------------------+
//| Include                                                          |
//+------------------------------------------------------------------+
#include "Defines.mqh"

//+------------------------------------------------------------------+
//| Defines                                                          |
//+------------------------------------------------------------------+
#define MAX_POINTS (10)

//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
class CRect
{
 public:
  CRect() {}
  ~CRect() {}
void Draw();
};

//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void CRect::Draw
{
 // Logica....
}

```

### Separación de secciones y comentarios internos

Usa `//---` para dividir secciones lógicas, dentro de bloques de codigo: 

```mql5
void OnInit() {
  //--- Inicializacion
  g_risk = new CRiskManagement();
  g_ob.init(Symbol(), PERIOD_H1);

  //---
  return INIT_SUCCEDED; 
}
}
```


Usa `//` para comentar ciertas partes, ademas si el texto ya no es visible en una sola linea y requiere HSCROLL entonces hagaglo por encima:

```mql5
void OnInit() {
  //--- Inicializacion
  g_risk = new CRiskManagement(); // Instancia dinamica de CRiskManagement (Texto corto aqui)

  // ............................................................ Texto muy largo por encima (aprox cubre el 60-70%)
  g_ob.init(Symbol(), PERIOD_H1);

  //---
  return INIT_SUCCEDED; 
}
}
```


### Separación visual completa

Para secciones importantes, usa el header completo:

```mql5
//+------------------------------------------------------------------+
//| Global variables                                                 |
//+------------------------------------------------------------------+
CRiskManagement* g_risk;
COrderBlockTick g_ob;

//+------------------------------------------------------------------+
//| Función Principal de Procesamiento                               |
//+------------------------------------------------------------------+
void process_signals() {
  // lógica
}
```

## Estructura de EAs

### Flujo recomendado

1. **Global.mqh** - Configuración inicial (BarManager, librerías base)
2. **Defines.mqh** - Includes y variables globales
3. **Functions.mqh** - Funciones auxiliares
4. **Main.mqh** - Lógica de estrategia (clases)
5. **EA.mq5** - Eventos del EA

### Ejemplo: Global.mqh

```mql5
//+------------------------------------------------------------------+
//|                                                      Global.mqh  |
//+------------------------------------------------------------------+
#property copyright "Copyright 2025, nique_372"
#property link      "https://www.mql5.com/es/users/nique_372"
#property strict

// Librerías base que requieren inicialización inmediata
#include <TSN\\TimeUtils\\TimeUtils.mqh>
#include <TSN\\ICTLibrary\\Core.mqh>

//---
// Configurar Bar Manager (crítico para evitar Invalid Pointer)
CBarManager* p_bar_manager;

void init_global() {
  p_bar_manager = new CBarManager(_Symbol, _Period);
  if (p_bar_manager == NULL) {
    Print("Error: No se pudo inicializar Bar Manager");
  }
}
```

### Ejemplo: Defines.mqh

```mql5
//+------------------------------------------------------------------+
//|                                                      Defines.mqh |
//+------------------------------------------------------------------+
#include "Global.mqh"  // PRIMERO

// Dependecias extra, auqnue por lo general global deberia de incluir lo necesario
#include <TSN\\MQLArticles\\Strategy\\Main.mqh>

//---
// Variables globales
CRiskManagement* g_risk;
COrderBlockTick g_ob;
CStrategy* g_strategy;

//---
// Parámetros
input int InpPeriod = 20;
input double InpRiskPercentage = 2.0;
input bool InpUseTelegram = true;
```

### Ejemplo: Main.mqh

```mql5
//+------------------------------------------------------------------+
//|                                                        Main.mqh  |
//+------------------------------------------------------------------+

#include "Defines.mqh" // o Functions.mqh si aplica

class CMyStrategy : public CStrategy {
private:
  int m_period;
  double m_rsi_threshold;
  
public:
  CMyStrategy(int InpPeriod, double InpThreshold) :
    m_period(InpPeriod),
    m_rsi_threshold(InpThreshold) {
  }
  
  void OnTick() override {
    //---
    // Lógica
  }
};
```

### Ejemplo: EA.mq5

```mql5
//+------------------------------------------------------------------+
//|                                          MyTradingEA.mq5         |
//+------------------------------------------------------------------+
#property copyright "Copyright 2025, nique_372"

#include "Main.mqh"  // Contiene Global.mqh

//+------------------------------------------------------------------+
//| Expert initialization function                                   |
//+------------------------------------------------------------------+
int OnInit() {
  init_global();
  g_risk = new CRiskManagement(InpRiskPercentage);
  g_strategy = new CMyStrategy(InpPeriod, 30.0);
  
  if (g_risk == NULL || g_strategy == NULL) {
    Print("Error en inicialización");
    return INIT_FAILED;
  }
  
  return INIT_SUCCEEDED;
}

//+------------------------------------------------------------------+
//| Expert tick function                                             |
//+------------------------------------------------------------------+
void OnTick() {
  g_strategy.OnTick();
}

//+------------------------------------------------------------------+
//| Expert deinitialization function                                 |
//+------------------------------------------------------------------+
void OnDeinit(const int reason) {
  delete g_strategy;
  delete g_risk;
}
```

---

## Comentarios y documentación

### Headers de función

En el ecosistema TSN dependiendo de la complejidad y si es un producto la forma de documentar varia:
1. En caso es un producto por lo general lo tienes en la wiki del repo (esto tambien aplica a repos gratuitos)
2. En caso no haya wiki por lo general se "trata" de documentar el codigo en este mismo

```mql5
//+------------------------------------------------------------------+
//| Descripcion....                                                  |
//| Inputs:                                                          |
//| - series: array double donde estan las series                    |
//| - period: periodo de calculo                                     | 
//| Ouput:                                                           | 
//| - Sma                                                            |
//| Notas:                                                           | 
//| - Period debe de ser mayor a 0                                   |
//+------------------------------------------------------------------+
double calculate_sma(const double &series[], int period) {
  double sum = 0.0;
  for (int i = 0; i < period; i++) {
    sum += series[i];
  }
  return sum / period;
}

Y en caso de estar en la wiki se sigue un estilo similar a los Docs de mql5 una pagina por funcion... y que recibe etc..

```

### Headers de archivo mqh (en caso de ea se puede agregar mas propiedades como descripcion, icono etc...)

Incluye siempre al inicio:

```mql5
//+------------------------------------------------------------------+
//|                                                    MyLibrary.mqh |
//|                                        Copyright 2025, nique_372 |
//|                          https://www.mql5.com/es/users/nique_372 |
//+------------------------------------------------------------------+
#property copyright "Copyright 2025, nique_372"
#property link "https://www.mql5.com/es/users/nique_372"
#property strict
```

---

## Idioma

### Recomendación actual

Se recomienda **español** para código interno del ecosistema TSN, pero con consideraciones:

- **Variables públicas/librerías:** Considera inglés para mayor alcance (esto depende de tu conocimiento de dicho idioma)
- **Comentarios complejos:** Español para claridad
- **Nombres de clases/funciones:** Consistencia en el proyecto

---

## Nota histórica

**Importante:** Algunos repositorios del ecosistema TSN (especialmente los más antiguos) **no siguen exactamente** estas convenciones. Esto se debe a que fueron desarrollados antes de implementar estándares formales.

- Código antiguo: ~50-70% adherencia a convenciones
- Código reciente: ~90%+ adherencia

Se está migrando progresivamente a estas convenciones. 

---

**¿Preguntas o sugerencias?** Abre una issue o contacta a [@nique_372](https://www.mql5.com/es/users/nique_372)