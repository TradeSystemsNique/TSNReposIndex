# MQL5 Conventions - TSN Ecosystem

> Standards and best practices for writing MQL5 code in the TSN ecosystem

---

## Table of Contents

1. [Naming](#naming)
2. [File Structure](#file-structure)
3. [Code Style](#code-style)
4. [Documentation](#documentation)
5. [Prints and Errors](#prints-and-errors)
6. [Testing](#testing)
7. [Language](#language)

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

### Note
1. Enums: Start with prefix "ENUM_"


### Context Resolution
In case libraries like winapi or internal class/global functions conflict with native functions, it is recommended to use `::` to indicate to the compiler that it should call the native function. For library functions like kernel32, for example `GetLastError()`, you can resolve the context as `kernel32::GetLastError()`


### Notes
Given the scale of TSN, we recommend the following:
1. Use project-specific prefixes for the naming of Enums, Structs, Defines, GlobalVariables. For example, in the case of `BasesParserSLan`, it is clear: `TSN_BSPL_ASM_*`
2. Use namespaces.
3. Class names can be somewhat more generic—for instance, `CJson`—but in such cases, they must strictly follow rule #2.
4. Do not use standalone functions; instead, wrap them in a static class.

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
 

## Documentation

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

> Note: In TSN, I generally only document the most critical aspects or those that are more "complex" to understand—specifically, low-level components (JSON, parsers, cryptography, mathematics). I document very little regarding mid-level components and above (Telegram, LLMs, MQL articles).
> I’m not necessarily suggesting that others follow this approach; the reason is that I develop TSN entirely on my own, so I don’t have much time to make everything look "polished." I simply do what I can, adjusting the "weight" (focus/effort) I dedicate to each module based on my current needs.

## Prints and Errors
### Errors management
Depending on the module and how critical it is in terms of speed, the following scheme is used:
1. Libraries (critical for speed): e.g., Telegram, JSON, BasesParserSLan, Crypto, etc.—where speed is paramount or low-level operations are involved—use an `m_last_err` member along with `LastErr` and `FormatErr` methods. You can also store the error as a `struct` if you wish to provide additional information to the user. Ideally, `FormatErr` should be static; if you need greater specificity, make it a class member. Rules:
    - The 0 value in the enum/codes you use must represent "no error." Furthermore, we do not recommend using `SetUserError`, as it is impractical in a TSN ecosystem—where you need to work with "ranges"—and it does not scale well.

2. Libraries (mid- or high-level layers): such as MQLArticles—use `CErrorTrace` from TSNStd.
 

3. Final Applications: This depends on where the information is displayed. For an Expert Advisor (EA) or other trading/implementation-focused tools, you would typically use `CLoggerBase`. If, however, you prefer a specific "style"—such as a panel that displays errors directly within the interface—you might need a custom class (as TSN does not provide one for this purpose), or you could log errors to files.

### Print() Use
Generally, we do not use direct `print` statements; instead, we use `FastLog()...`
For libraries, the rule is strict: NO `print` statements—unless they are wrapped in an `#ifndef` / `#define` / `#endif` block. Furthermore, the name of the `#define` must reference the project; do not use `_DEBUG`.
For applications, we do not recommend it, but we leave this open for you to decide.

### Language
You decide the language, but for Errors/Format (libs), we recommend English.

## Testing 
1. Libraries: It is recommended to conduct testing using MqlCIByLeo (to allow for integration with self-hosted workflows) or a custom testing framework.
    Within your tests, you can cover common scenarios, test suites (if available), fuzzing, etc.
    > Note: TSN’s approach here is more flexible; the method is left to the individual. Furthermore, regarding TSN libraries, testing is often performed manually—verifying that the current behavior aligns with previous functionality (this is especially critical for libraries that impact trading bots, or EAs) and visually observing how trades are managed.
    Ultimately, it depends heavily on the specific subject matter.
2. Regarding end-user applications, the topic is a bit ambiguous, though I can offer a few recommendations:
    1. Trading bots:
      - Verify that performance remains consistent when using the same parameters.
      - Optimize the bot and check for execution errors with specific parameters (this acts as a form of automated "fuzzing").
      - Test in demo environments to see if any unusual edge cases arise.
    2. Dashboards/End-user apps (utilities):
      - This is primarily visual; run the Expert Advisor (EA) and check that the coordinates remain stable. You can also cycle through different parameters (I tend to be more flexible here).

> What all these apps do have in common is that the code must compile.

## File Header mqh (in case of EA, additional properties such as description, icon, etc. can be added)

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

1. For internal code \ doxygen
   Use the language that makes it easiest for you to iterate.
   In the case of TSN, we use Spanish 70–80% and English 20–30%.
   This is because it’s easier for me to iterate and code without having to constantly rely on a translator or LLM models.
   My priority—over public readability—is making it easy for me to program and explain my ideas.
   I also use English, but to a lesser extent—only when I already have the "meaning" clear in my mind.
2. For public-facing documentation, such as:
    - README files
    - Web-based documentation
    English is preferred for greater visibility.
    The internal `Docs/` folder within the project can also be in English; however, since this is more "low-level" documentation, feel free to use whichever language you are most comfortable with.
    
## Historical Note

**Important:** Some repositories in the TSN ecosystem (especially the older ones) **do not exactly follow** these conventions. This is because they were developed before formal standards were implemented.

- Old code: ~50-70% adherence to conventions
- Recent code: ~90%+ adherence

There is a progressive migration to these conventions.

---

**Questions or suggestions?** Open an issue or contact [@nique_372](https://www.mql5.com/es/users/nique_372)