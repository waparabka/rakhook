# Just modified rakhook library
Use this in your cmake project

```
FetchContent_Declare(rakhook GIT_REPOSITORY https://github.com/waparabka/rakhook.git)
FetchContent_MakeAvailable(rakhook)
```

# Or you can
Assemble the project yourself with

```
cmake -B project -A Win32
```
