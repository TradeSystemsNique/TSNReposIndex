# MqlIncludes

In the typical TSN ecosystem, when a repository is created, we then need to include it in other projects or local Expert Advisors (EAs).

Therefore, to avoid hardcoding paths, we decided to use a "proxy wrapper," an MQH file that basically hardcodes an `#include` to the destination MQH files. The idea behind this is that if we later change our EA's location, hardcoding the paths would require constantly updating them. But now, with these MQH files acting as proxies, when using `#include`, the search is done in the `Include` folder, not just in real time. This makes maintaining and using the libraries much easier.
Now, all these ideas are embodied in a free product I've released: a collection of all the MQH "proxy" files in the ecosystem. You can find it here in the bot place: https://thebotplace.com/bot/tsn-ecosystem-sdk