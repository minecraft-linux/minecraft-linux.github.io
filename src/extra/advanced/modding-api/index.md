# MCPELauncher API Reference

This document provides an overview of the MCPELauncher API, detailing the available symbols, their signatures, and descriptions. The API is designed for advanced modding and hooking functionalities in Minecraft Pocket Edition.

## Overview

Mods have to be compiled as android shared libraries (`.so` files) using the Android NDK and placed in the `mods` directory of the MCPELauncher. The launcher will automatically load these libraries at startup.

The MCPELauncher API allows developers to hook into Minecraft's runtime, modify behavior, and manage dynamic libraries. It provides functions for logging, hooking symbols, patching memory, and handling dynamic libraries.

## Accessing the API

Use `dlopen("libmcpelauncher_mod.so", RTLD_NOW)` and `dlsym` to access the API. The symbols are defined in the `libmcpelauncher_mod.so` shared library.

Otherwise declare the symbols as weam `extern "C"` in your C++ code to avoid name mangling and allow the launcher to provide the implementations.

```c++
extern "C" {
    __attribute__((weak)) void* mcpelauncher_hook(void* sym, void* hook, void** orig);
    __attribute__((weak)) void* mcpelauncher_hook2(void* lib, const char* sym, void* hook, void** orig);
    // ... other symbols
}
```

## Logging Functions

| Symbol | Description | Notes |
|--------|-------------|-------|
| `mcpelauncher_log` | Logs a message | Deprecated; use Android `liblog` |
| `mcpelauncher_vlog` | Logs a verbose message | Deprecated; use Android `liblog` |

---

## Hook Initialization

| Symbol | Signature | Description |
|--------|-----------|-------------|
| `mcpelauncher_preinithook2` | `void(const char* name, void* sym, void* user, void (*callback)(void*, void*))` | Registers a pre-init hook with a callback |
| `mcpelauncher_preinithook` | `void(const char* name, void* sym, void** orig)` | Registers a pre-init hook and stores original symbol |

---

## Hook Management

| Symbol | Signature | Description |
|--------|-----------|-------------|
| `mcpelauncher_hook` | `void*(void* sym, void* hook, void** orig)` | Creates and applies a hook for a symbol |
| `mcpelauncher_hook2` | `void*(void* lib, const char* sym, void* hook, void** orig)` | Creates a hook for a symbol in a specific library |
| `mcpelauncher_hook2_add_library` | `void(void* lib)` | Adds a library to the hook manager |
| `mcpelauncher_hook2_remove_library` | `void(void* lib)` | Removes a library from the hook manager |
| `mcpelauncher_hook2_delete` | `void(void* hook)` | Deletes a hook instance |
| `mcpelauncher_hook2_apply` | `void()` | Applies all registered hooks |

---

## Memory Patching

| Symbol | Signature | Description |
|--------|-----------|-------------|
| `mcpelauncher_patch` | `void*(void* address, void* data, size_t size)` | Patches memory at a given address |
| *(Apple ARM64 only)* | Uses `pthread_jit_write_protect_np` and `sys_icache_invalidate` for JIT-safe patching |

---

## Dynamic Library Handling

| Symbol | Description |
|--------|-------------|
| `mcpelauncher_host_dlopen` | Wrapper for `dlopen` |
| `mcpelauncher_host_dlsym` | Wrapper for `dlsym` |
| `mcpelauncher_host_dlclose` | Wrapper for `dlclose` |
| `mcpelauncher_dlclose_unlocked` | Custom unlocked `dlclose` |

---

## Symbol Relocation

| Symbol | Signature | Description |
|--------|-----------|-------------|
| `mcpelauncher_relocate` | `void(void* handle, const char* name, void* hook)` | Relocates a single symbol |
| `mcpelauncher_relocate2` | `void(void* handle, size_t count, hook_entry* entries)` | Relocates multiple symbols |
| `mcpelauncher_load_library` | `void(const char* name, size_t count, hook_entry* entries)` | Loads a library and applies hooks |
| `mcpelauncher_unload_library` | `void(void* handle)` | Unloads a previously loaded library |

---

## Data Structures

```cpp
struct hook_entry {
    const char* name;
    void* hook;
};
```

Used for batch relocation and library loading.
