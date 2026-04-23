# MQL5 Conventions - TSN Ecosystem

> Standards and best practices for writing MQL5 code in the TSN ecosystem

---

## Table of Contents

1. [Naming](#naming)
2. [File Structure](#file-structure)
3. [Code Style](#code-style)
4. [EA Structure](#ea-structure)
5. [Comments and Documentation](#comments-and-documentation)
6. [Language](#language)

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

## File Structure

### Recommended Hierarchy for EAs

For **simple or moderately complex** EAs, it is recommended to divide them into the following files:

```
EA_Name/
├── Global.mqh        (Global initialization - ALWAYS FIRST)
├── Defines.mqh       (Includes and global variables)
├── Functions.mqh     (Helper functions)
├── Main.mqh          (Main logic/classes)
└── EA_Name.mq5       (Main event)
```

### Include Order

**Always** include `Global.mqh` first to avoid "Invalid Pointer" errors in global instances:

```mql5
// Defines.mqh
#include "Global.mqh"        //  ALWAYS FIRST
#include <TSN\\MQLArticles\\Strategy\\Main.mqh>
#include "Functions.mqh"
#include "Main.mqh"
```

```mql5
// EA_Name.mq5
#include "Defines.mqh"       // Already contains Global.mqh
```

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

## EA Structure

### Recommended Flow

1. **Global.mqh** - Initial configuration (BarManager, base libraries)
2. **Defines.mqh** - Includes and global variables
3. **Functions.mqh** - Helper functions
4. **Main.mqh** - Strategy logic (classes)
5. **EA.mq5** - EA events

### Example: Global.mqh

```mql5
//+------------------------------------------------------------------+
//|                                                      Global.mqh  |
//+------------------------------------------------------------------+
#property copyright "Copyright 2025, nique_372"
#property link      "https://www.mql5.com/es/users/nique_372"
#property strict

// Base libraries that require immediate initialization
#include <TSN\\TimeUtils\\TimeUtils.mqh>
#include <TSN\\ICTLibrary\\Core.mqh>

//---
// Configure Bar Manager (critical to avoid Invalid Pointer)
CBarManager* p_bar_manager;

void InitGlobal() {
  p_bar_manager = new CBarManager(_Symbol, _Period);
  if (p_bar_manager == NULL) {
    Print("Error: Could not initialize Bar Manager");
  }
}
```

### Example: Defines.mqh

```mql5
//+------------------------------------------------------------------+
//|                                                      Defines.mqh |
//+------------------------------------------------------------------+
#include "Global.mqh"  // FIRST

// Extra dependencies, although global should generally include what's necessary
#include <TSN\\MQLArticles\\Strategy\\Main.mqh>

//---
// Global variables
CRiskManagement* g_risk;
COrderBlockTick g_ob;
CStrategy* g_strategy;

//---
// Parameters
input int InpPeriod = 20;
input double InpRiskPercentage = 2.0;
input bool InpUseTelegram = true;
```

### Example: Main.mqh

```mql5
//+------------------------------------------------------------------+
//|                                                        Main.mqh  |
//+------------------------------------------------------------------+

#include "Defines.mqh" // or Functions.mqh if applicable

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
    // Logic
  }
};
```

### Example: EA.mq5

```mql5
//+------------------------------------------------------------------+
//|                                          MyTradingEA.mq5         |
//+------------------------------------------------------------------+
#property copyright "Copyright 2025, nique_372"

#include "Main.mqh"  // Contains Global.mqh

//+------------------------------------------------------------------+
//| Expert initialization function                                   |
//+------------------------------------------------------------------+
int OnInit() {
  InitGlobal();
  g_risk = new CRiskManagement(InpRiskPercentage);
  g_strategy = new CMyStrategy(InpPeriod, 30.0);
  
  if (g_risk == NULL || g_strategy == NULL) {
    Print("Error in initialization");
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

## Comments and Documentation

### Function Headers

In the TSN ecosystem, the documentation method varies depending on complexity and whether it's a product:
1. If it's a product, it's generally documented in the repository wiki (this also applies to free repositories)
2. If there's no wiki, it's generally documented in the code itself

```mql5
//+------------------------------------------------------------------+
//| Description....                                                  |
//| Inputs:                                                          |
//| - series: double array where the series is located               |
//| - period: calculation period                                     | 
//| Output:                                                          | 
//| - Sma                                                            |
//| Notes:                                                           | 
//| - Period must be greater than 0                                  |
//+------------------------------------------------------------------+
double CalculateSma(const double &series[], int period) {
  double sum = 0.0;
  for (int i = 0; i < period; i++) {
    sum += series[i];
  }
  return sum / period;
}

And if it's on the wiki, a similar style to the MQL5 Docs is followed - one page per function... and what it receives, etc.
```

### File Header mqh (in case of EA, additional properties such as description, icon, etc. can be added)

Always include at the beginning:

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