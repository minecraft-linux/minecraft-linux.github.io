# Menu API Reference

Integrate custom menus below the mods menu item and create custom windows with interactive controls using the `libmcpelauncher_menu.so` library.

## `MenuEntryABI` Structure

Defines a single menu entry with potential subentries.

```cpp
struct MenuEntryABI {
    const char* name;                    // Name shown in the UI
    void* user;                          // Custom user data passed to callbacks
    bool (*selected)(void* user);       // Selection callback
    void (*click)(void* user);          // Click callback
    size_t length;                      // Number of subentries
    MenuEntryABI* subentries;           // Pointer to array of subentries
};
```

---

## `void mcpelauncher_addmenu(size_t length, MenuEntryABI* entries);`

Adds a group of menu entries to the launcher.

- `length`: Number of items in `entries`
- `entries`: Pointer to array of `MenuEntryABI`

---

## `control` Structure

Represents a UI control embedded in a window.

```cpp
struct control {
    int type; // Enum-like control type
    union {
        struct {
            const char* label;
            void* user;
            void (*onClick)(void* user);
        } button;

        struct {
            const char* label;
            int min;
            int def;
            int max;
            void* user;
            void (*onChange)(void* user, int value);
        } sliderint;

        struct {
            const char* label;
            float min;
            float def;
            float max;
            void* user;
            void (*onChange)(void* user, float value);
        } sliderfloat;

        struct {
            const char* label;
            int size; // 0 = normal, 1 = small title
        } text;

        struct {
            const char* label;
            const char* def;
            const char* placeholder;
            void* user;
            void (*onChange)(void* user, const char* value);
        } textinput;
    } data;
};
```

### Control Types

Set `type` to match the control structure being used:
- `0`: Button
- `1`: Slider (integer)
- `2`: Slider (float)
- `3`: Static text
- `4`: Text input

---

## `void mcpelauncher_show_window(...)`

Displays a window populated with interactive controls.

```cpp
void mcpelauncher_show_window(
    const char* title,
    int isModal,
    void* user,
    void (*onClose)(void* user),
    int count,
    control* controls
);
```

### Parameters

- `title`: Title displayed on the window
- `isModal`: Modal flag (non-zero blocks other inputs)
- `user`: Custom user data passed to callbacks
- `onClose`: Callback called when window closes
- `count`: Number of controls
- `controls`: Pointer to array of `control` structs

---

## `void mcpelauncher_close_window(const char* title);`

Closes the window with the specified title.
