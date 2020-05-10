## Using Virtualenv Python 2.7

### Check virtualenv version and exists on computer
```
virtualenv --version
```

### Create new virtual env and use
```
mkdir pyenv
virtualenv pyenv
source pyenv/bin/activate
```

python should now be usable with `python --version`

### Deactivate
```
deactivate
```

### make a python script use the virtual environment
After activating find where the python exe is
```
$ which python
/home/sean/cpp/keygenme/pyenv/bin/python
```

Put that at the top of a python script with a shebang #!
```
#!/home/sean/cpp/keygenme/pyenv/bin/python
```

Make execuatable
```
chmod +x script.py
```  

Can also be relative 
```
#!./pyenv/bin/python
```
