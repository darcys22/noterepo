## Golang
https://hackernoon.com/go-the-complete-guide-to-profiling-your-code-h51r3waz

## C++
There's a nifty package called linux-perf, then you run:
```
perf record -g ./bin/oxend
```
and later, when it's done:
```
perf report -g
```
will show you all the functions and how much time was spent in each (and you can hit + to drill down). It works much better in a Debug build; in release builds optimizations might mean a lot of the functions don't actually exist in the output.

This is the current state (debug build).  For instance that div128_64 line means we are spending 11.42% of CPU time inside that function or things the function calls; while the 3.59% in the second columns means 3.59% of CPU time in the function itself.
