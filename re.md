#### Generic File Information
```
file example.elf
```

#### gdb

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

#### ELF

Read first 64 bytes of file
```
xxd -l 64 example.elf
```
Read section headers of the elf
```
readelf -s example.elf
```
