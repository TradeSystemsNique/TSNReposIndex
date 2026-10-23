# General Philosophy of the TSN Ecosystem: Programming Style

Here I describe the philosophy for designing and writing code in the TSN ecosystem:
what we prioritize, our style, in which contexts, etc.

## General

1. **Speed first:** Our main bet in TSN is speed, in every kind of library.
   It doesn't matter the topic, whether it's a parser, math, crypto, ICT, news, etc. We will always seek both maximum speed
   and low memory usage. Always. In every library of the TSN ecosystem we will prioritize this.
   Partly this is because in trading or apps, the last thing I want is to "create fast versions"
   when I need them. It's better to be cautious and have everything well made and fast from the very first moment,
   instead of optimizing when the need arises.
   This applies strongly. The idea is to reach the ceiling of MQL5, or the best possible solution.
   We are not satisfied with merely solving the problem; that is easy. We want something more challenging:
   we want to think, dig down into the options, and test which one is best.
   Therefore, optimization is the hallmark of the TSN ecosystem. It is no longer about "optimizing only the bottlenecks";
   it's more that the code "comes out that way" by default, "without effort". It is our brand.

2. **APIs assume in several cases:** In many APIs of the TSN ecosystem, if the error does not violate a spec (for example,
   this would not apply to JSON, where you would be violating the spec and producing invalid JSON, although it depends, see below;
   for instance, I would not skip the leading-zeros check, or the malformed-JSON check),
   but is rather "implementation-defined", then we prefer to document what fails
   instead of adding ifs, checks, or errors.

3. **Stable API in (ONLY) critical libraries:** I have recently decided that for very critical libraries
   or those with a lot of reach, I will try to give them a long-lived version
   instead of updating whenever I want to improve them.

4. **Speed over readability:** In many cases, speed tends to cost many things,
   such as readability, although historically I have cared little about that, so be it.
   Internally it will be somewhat complicated, and you will also have to "mentally execute code" or follow
   traces to see how it works. This is normal. It is hard to grasp, yes, but it is in exchange for maximum speed.
   Besides, the idea is that the external code, the API itself, is readable; the implementation, however, is not.

5. **Simplification in several libs (by usage heuristics):** If we notice or measure that certain features of a "spec" contribute little,
   or I consider they will rarely be used, we will simplify the code. For example, in JSON, by default `"\""` is okay and raises an error.
   The same goes for CryptoByleo: Fernet, for example, is not 100% spec-compliant; it is more like a binary Fernet without the Base64.
   And so on. In short, several features that I "find odd" or consider very edge-case and uncommon
   will be handled depending on how "strongly" I decide to support them. For example, if I see that something might plausibly occur,
   as with JSON, I will use defines and macros to enable it. On the other hand, with Fernet, if I see it is a case that almost nobody will use,
   I will leave it as it is now, and whoever wants to "do the extra work" can do it after calling the API.
   And so on; I will base my decisions on that.

6. **External dependencies:** We will rarely use one, only when warranted and when I myself have verified, tested,
   used, and accepted it into the ecosystem. It must fit my philosophy of how I work (maximum speed,
   though not always; if it solves a very complex problem, I might adopt it). Besides, I rarely use
   the original version, so I will "tune" the project to my style of doing things.
   And as I mentioned, since the TSN ecosystem covers a huge number of libraries, 98%+ of all the MQL5 code
   in the ecosystem is our own. Basically, we are an ecosystem that creates what MQL5 "lacked".
   We don't build on "other pieces"; rather, we do the whole process: building the low, middle, and also the upper layers,
   including apps.

7. **Low-level access in several Layer 0–1 libraries:** In many libs, several members will be public.
   This allows low-level optimizations instead of using getters/setters and copies, which are expensive in certain cases.

8. **Elegant API:** In many libs we will aim for a fluent API that is easy to integrate and use.

---

It should be noted that this speed-focused approach carries a "weight" that depends on the code.
Not all code is 100% optimized. We accept some trade-offs from time to time, but they are the minority.
This is especially true for legacy code (2025 and earlier), which is still abundant in the veteran libraries, and where applying optimization
is costly in terms of time. But as of today, all libs in the ecosystem are fast, all of them,
though not all have the best possible algorithm (the MQL5 ceiling).