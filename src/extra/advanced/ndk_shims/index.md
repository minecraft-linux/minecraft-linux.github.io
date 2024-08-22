# Ndk Shims

How to add new or missing native ndk function

## Adding a new libc function to the launcher

Our libc-shim wrapper are split across multiple cpp files, all have a
structure like
<https://github.com/minecraft-linux/libc-shim/blob/master/src/common.cpp#L334-L350>.

``` c++
void shim::add_common_shimmed_symbols(std::vector<shim::shimmed_symbol> &list) {
    list.insert(list.end(), {
        {"__errno", bionic::get_errno},
    });
}
```

-   `"__errno"` is the name of the libc symbol
-   `bionic::get_errno` is a function or global pointer with the same
    type and calling convention as the ndk provided function. Linux
    armhf has a different calling convention than android armeabi-v7a,
    you have to wrap all functions with floating point arguments or
    return values, use `ARMHFREWRITE(bionic::get_errno)` to
    automatically wrap it in c++. Windows uses different calling
    conventions than linux, macOS and Android.

## Loading a stub library with mcpelauncher-linker

Stub libraries are libraries without the need of an android shared
library file, which implements symbols of real shared libraries. You can
call `linker::dlopen` and `linker::dlsym` on them to get the pointer of
the function or global object.

``` c++
std::unordered_map<std::string, void*> syms;
syms["__errno"] = (void*) bionic::get_errno;
linker::load_library("stub.so", syms);
```

-   `"__errno"` is the name of the symbol
-   `bionic::get_errno` is a function or global pointer with the same
    type and calling convention as the ndk provided function. Linux
    armhf has a different calling convention than android armeabi-v7a,
    you have to wrap all functions with floating point arguments or
    return values, use `ARMHFREWRITE(bionic::get_errno)` to
    automatically wrap it in c++. Windows uses different calling
    conventions than linux, macOS and Android.
