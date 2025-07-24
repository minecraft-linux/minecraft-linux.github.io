# Game Window API Reference

This API provides access to the primary game window and allows registration of various input and lifecycle callbacks.

---

## Core Window Access

| Symbol | Signature | Description |
|--------|-----------|-------------|
| `game_window_get_primary_window` | `GameWindowHandle*()` | Returns a pointer to the current primary game window |

| `game_window_is_mouse_locked` | `bool(GameWindowHandle* handle)` | Checks if the mouse is currently locked in the window |

| `game_window_get_input_mode` | `int(GameWindowHandle* handle)` | Retrieves the current input mode from the window callbacks |

---

## Input Callback Registration

These functions allow you to register input event handlers for keyboard and mouse interactions.

| Symbol | Signature | Description |
|--------|-----------|-------------|
| `game_window_add_keyboard_callback` | `void(GameWindowHandle* handle, void* user, bool (*callback)(void* user, int keyCode, int action))` | Registers a keyboard input callback |
| `game_window_add_mouse_button_callback` | `void(GameWindowHandle* handle, void* user, bool (*callback)(void* user, double x, double y, int button, int action))` | Registers a mouse button input callback |
| `game_window_add_mouse_position_callback` | `void(GameWindowHandle* handle, void* user, bool (*callback)(void* user, double x, double y, bool relative))` | Registers a mouse movement callback |
| `game_window_add_mouse_scroll_callback` | `void(GameWindowHandle* handle, void* user, bool (*callback)(void* user, double x, double y, double dx, double dy))` | Registers a mouse scroll callback |

---

## Lifecycle & Rendering Callbacks

| Symbol | Signature | Description |
|--------|-----------|-------------|
| `game_window_add_window_creation_callback` | `void(void* user, void (*onCreated)(void* user))` | Registers a callback to be invoked when the window is created |
| `game_window_add_swap_buffers_callback` | `void(void* user, void (*callback)(void* user, EGLDisplay display, EGLSurface surface))` | Registers a callback for when buffers are swapped during rendering |

---

## Library Integration

Use dlopen and dlsym to load the library and access the functions

```cpp
dlopen("libmcpelauncher_gamewindow.so");
```

---

## Data Types

### `GameWindowHandle`

An opaque structure representing the game window.