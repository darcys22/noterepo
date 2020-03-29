## Octave

Installing on Ubuntu Server
```
sudo apt-get install octave
```

Make files using the filetype `example.m`

Start octave repl using 
```
octave
```
in the same directory as your `.m` files

octaves path determines what `.m` files are available and can be seen using `path`

from within the repl you can call the script using its filename without the filetype
```
> example
```

### Functions vs Scripts
Rule of thumb:

    Always use functions, never scripts!

#### Function
```
% fname.m
function [y1, y2] = fname(x1, x2)
	x1 + x2
end
```
Call from within repl using 
```
> fname(1,2)
ans =  3
```

#### Script
Scripts are just a collection of commands
```
% numGenerator.m
columns = 10000;
rows = 1;
bins = columns/100;

rng(now);
list = 100*rand(rows,columns);
```
Call from within repl using 
```
> numGenerator
```


