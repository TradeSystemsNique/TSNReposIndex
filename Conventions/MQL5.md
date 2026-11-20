# MQL5 Conventions - TSN Ecosystem

> Standards and best practices for writing MQL5 code in the TSN ecosystem

---

## Table of Contents

1. [Naming](#naming)
2. [File Structure](#file-structure)
3. [Code Style](#code-style)
4. [Comments and Documentation](#comments-and-documentation)
5. [Language](#language)

---

## Naming

### Classes
- **Prefix:** `C`
- **Type:** `PascalCase`
- **Examples:** `CMyClass`, `CIndicator`, `COrderBlock`, `CRiskManagement`

```mql5
class CStrategy {
  // implementation
};
```

### Interfaces
- **Prefix:** `I`
- **Type:** `PascalCase`
- **Examples:** `IStrategy`, `INotifiable`

```mql5
interface IStrategy {
  void OnTick();
};
```

### Structures
- **Prefix:** None
- **Type:** `PascalCase`
- **Examples:** `Bar`, `OrderData`, `SignalInfo`

```mql5
struct OrderData {
  ulong ticket;
  double price;
  datetime time;
};
```

### Unions
- **Prefix:** None
- **Type:** `PascalCase`

```mql5
union DataValue {
  double dval;
  int ival;
};
```

### Functions
- **Prefix:** None
- **Type:** `PascalCase`
- **Examples:** `CalculateSma()`, `GetSupportLevel()`, `ApplyRiskManagement()`

```mql5
double CalculateSma(const double &series[], int period) {
  // implementation
}
```

### Member Variables (Class)
- **Prefix:** `m_`
- **Type:** `snake_case`
- **Examples:** `m_period`, `m_buffer`, `m_is_active`

```mql5
class CIndicator {
private:
  int m_period;
  double m_buffer[];
  bool m_is_active;
};
```

### Global Variables
- **Prefix:** `g_`
- **Type:** `snake_case`
- **Examples:** `g_risk`, `g_order_block`, `g_bar_manager`

```mql5
CRiskManagement* g_risk;
COrderBlockTick g_ob;
CBarManager g_bar_manager;
```

### Local Variables
- **Prefix:** None
- **Type:** `snake_case`
- **Examples:** `current_price`, `support_level`, `trade_signal`

```mql5
void OnTick() {
  double current_price = SymbolInfoDouble(_Symbol, SYMBOL_BID);
  int period = 14;
  bool is_valid = true;
}
```

### Input Parameters
- **Prefix:** `Inp`
- **Type:** `PascalCase`
- **Examples:** `InpPeriod`, `InpStopLoss`, `InpTakeProfitRatio`

```mql5
input int InpPeriod = 14;
input double InpStopLoss = 50.0;
input string InpTelegramToken = "your_token";
```

### Constants \ Defines \ Enums
- **Type:** `UPPER_SNAKE_CASE`
- **Examples:** `MAX_ITERATIONS`, `DEFAULT_PERIOD`, `VERSION_NUMBER`

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

### Context Resolution
In case libraries like winapi or internal class/global functions conflict with native functions, it is recommended to use `::` to indicate to the compiler that it should call the native function. For library functions like kernel32, for example `GetLastError()`, you can resolve the context as `kernel32::GetLastError()`


---

## Code Style

### MQL5 IDE Configuration

**Tools → Options → Stylizer:**

| Option | Value |
|--------|-------|
| Style | MetaQuotes |
| Replace tabs with spaces | Yes |
| Remove empty lines | No |
| Insert spaces after comma/semicolon | Yes |
| Insert spaces around operators | Yes |

**Tools → Options → General:**

| Option | Value |
|--------|-------|
| Tab (characters) | 2 |
| Insert spaces | Yes |
| Insert () and {} ) ] " ' | Yes |
| Highlight paired parentheses | Yes |
| Highlight current line | Yes |
| Enable clipboard history | Yes |
| Auto name list | Yes |
| Auto indent | Yes |
| Auto parameters | Yes |
| Line numbers | Yes |

### Keyboard Shortcuts

- **Format code:** `CTRL + ,`, use it always when you finish coding something
- **Insert function/class/general section/include header:** `CTRL + .`, use before defining a class or defines\enums\structs, functions:

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
 // Logic....
}

```

### Section Separation and Internal Comments

Use `//---` to divide logical sections within code blocks:

```mql5
void OnInit() {
  //--- Initialization
  g_risk = new CRiskManagement();
  g_ob.init(Symbol(), PERIOD_H1);

  //---
  return INIT_SUCCEEDED; 
}
}
```

Use `//` to comment certain parts. Also, if the text is no longer visible in a single line and requires HSCROLL, then place it above:

```mql5
void OnInit() {
  //--- Initialization
  g_risk = new CRiskManagement(); // Dynamic instance of CRiskManagement (Short text here)

  // ............................................................ Very long text above (approx covers 60-70%)
  g_ob.init(Symbol(), PERIOD_H1);

  //---
  return INIT_SUCCEEDED; 
}
}
```

### Complete Visual Separation

For important sections, use the complete header:

```mql5
//+------------------------------------------------------------------+
//| Global variables                                                 |
//+------------------------------------------------------------------+
CRiskManagement* g_risk;
COrderBlockTick g_ob;

//+------------------------------------------------------------------+
//| Main Signal Processing Function                                  |
//+------------------------------------------------------------------+
void ProcessSignals() {
  // logic
}
```

---

## Comments and Documentation

### Function Headers

The documentation will be divided into (2-3) parts:
1. Doxygen: Code documentation.
2. Docs (in the libraries folder): Additional pages referenced within the final Doxygen-generated website; this includes usage examples, tables, explanations, architecture, the rationale behind design decisions, etc.
For final applications, depending on their scale, an internal wiki might suffice; for medium-to-large-scale projects, a static website would be the best approach.

```cpp
//+------------------------------------------------------------------+
//| CalculateSma                                                     |
//+------------------------------------------------------------------+
/*
*@brief Calculate SMA for series array
*@param[in] series double array where the series is located
*@param[in] period calculation period
*@return Sma value
*@warning Period must be greater than 0 (It does not validate)
*/
double CalculateSma(const double &series[], int period) {
  double sum = 0.0;
  for (int i = 0; i < period; i++) {
    sum += series[i];
  }
  return sum / period;
}
```
For Doxygen:
1. When dealing with a class, we prefer to have the documentation at the function definition rather than within the class body. In other words:
- If the class body contains only the signature and the implementation is elsewhere, the documentation should be placed where the function is defined; otherwise, it should be placed within the class itself.
2. Do not limit yourself to basic commands; feel free to use `@warning`, `@bug`, `@todo`, or any other necessary tags, as well as Markdown.




### File Header mqh (in case of EA, additional properties such as description, icon, etc. can be added)

Always include at the beginning:

```mql5
//+------------------------------------------------------------------+
//|                                                       <FILE_NAME>|
//|                                     Copyright <YEAR>, <YOUR NAME>|
//|                                                            <URL> |
//+------------------------------------------------------------------+
#property copyright "Copyright <YEAR>, <YOUR NAME>"
#property link "<URL>"
#property strict

#ifndef REPONAME_PATHTOFILE
#define REPONAME_PATHTOFILE


#endif REPONAME_PATHTOFILE
```

**Placeholder Descriptions**
- **FILE_NAME**: Name of the mqh file
- **YEAR**: Current year
- **YOUR NAME**: Name of the code writer\org
- **URL**: Creator's URL, e.g.: [Website, MQL5 Profile, Personal Website, Github, etc..]

All these fields are defined before creating the file, some when creating the project, others in the file itself.

---

## Language

### Current Recommendation

**Spanish** is recommended for code internal to the TSN ecosystem, but with considerations:

- **Public variables/libraries:** Consider English for greater reach (this depends on your knowledge of that language)
- **Complex comments:** Spanish for clarity
- **Class/function names:** Consistency in the project

---

## Historical Note

**Important:** Some repositories in the TSN ecosystem (especially the older ones) **do not exactly follow** these conventions. This is because they were developed before formal standards were implemented.

- Old code: ~50-70% adherence to conventions
- Recent code: ~90%+ adherence

There is a progressive migration to these conventions.

---

**Questions or suggestions?** Open an issue or contact [@nique_372](https://www.mql5.com/es/users/nique_372)