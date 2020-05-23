## Linux

### Generic File Information
```
file example.elf
```

### gdb

Sets the format of the disassembly to look better
```
disassembly-flavour intel
```

Disables pagination
```
set pagination off
```

Log output to file
```
set logging on
```

Print a string in a memory location
https://codelearn.me/2018/02/24/show-string-in-memory.html
```
x /s <addr>
```

### ELF

Read first 64 bytes of file
```
xxd -l 64 example.elf
```
Read section headers of the elf
```
readelf -s example.elf
```

### radare2
open with `r2 example.elf`
enter visual mode with `V`
navigate the mode with `p` and shift 'P'
quit visual with `q`

## Windows

010 editor - hex editor

