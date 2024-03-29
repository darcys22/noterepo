## Programming in C++

### Useful website
https://medium.com/coding-blocks/make-and-cmake-automating-c-build-process-900f569a75db

### Getting the required software
```
sudo apt-get install G++ cmake
```

### Setup the CMakeLists.txt file in the root directory
CPP_Projects/HelloWorld/CMakeLists.txt
```
cmake_minimum_required (VERSION 3.5)

project (HelloWorld)

set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror -std=c++14")
set (source_dir "${PROJECT_SOURCE_DIR}/src/")

file (GLOB source_files "${source_dir}/*.cpp")

add_executable (HelloWorld ${source_files})
```

### create a build and src folders
put source files in /src and make a /build folder from within the build folder run the following to execute cmake
```
cmake ..
```

### run make from within the build directory after running cmake
```
make
```

### Getting assembly
objectbump -s | less

### analyse perf
Linux perf

### What is GLIBC
https://stackoverflow.com/questions/11460782/what-is-glibc-what-is-it-used-for
```
git clone git://sourceware.org/git/glibc.git
```


### Running clang tidy
Get a config from somewhere like this:
https://github.com/googleapis/google-cloud-cpp/blob/main/.clang-tidy

save as .clang-tidy which will be the config

or can run with it specified as so
```
clang-tidy --fix -checks='-*,readability-identifier-naming' \
    -config="{CheckOptions: [ {key: readability-identifier-naming.FunctionCase, value: lower_case} ]}" \
    mycode.c -- -std=c17
```

But if the .clang-tidy is there you can just ignore the --config param
