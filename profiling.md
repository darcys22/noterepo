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

It will need the compiler to show frame pointers. Add this to the CMakeLists.txt to ensure it happens
```
set(CMAKE_CXX_FLAGS "-fno-omit-frame-pointer")
```

For wallet3 then calling with `RelWithDebInfo` was a good way of building
```
cmake .. -DBUILD_STATIC_DEPS=ON -DCMAKE_BUILD_TYPE=RelWithDebInfo
```

and finally calling perf with dwarf actually showed the stack frames and allowed to trace through
```
perf record -F 99 --call-graph dwarf oxen_wallet_cli
```

