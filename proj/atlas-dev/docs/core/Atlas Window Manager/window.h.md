# `window.h` - AWM Window Structure

This header defines the `Window` structure used by **Atlas Window Manager (AWM)**. It encapsulates state, rendering data, and behavior for a window instance within the AWM environment.

---

## Struct: `Window`

Represents a single window in AWM.

```cpp
struct Window {
````

---

### Basic Properties

```cpp
const char* title;
int64_t x, y;
uint64_t width;
uint64_t height;
int desktopView;
```

* `title`: Title string of the window.
* `x`, `y`: Current position on screen.
* `width`, `height`: Current size.
* `desktopView`: Identifier for the virtual desktop the window is assigned to.

---

### Previous State

```cpp
uint64_t old_x, old_y;
uint64_t old_width, old_height;
```

* Used to store dimensions and position before resizing, moving, or maximizing.

---

### Indexing & Buffers

```cpp
uint64_t index;
void* buffer;
```

* `index`: Window ordering or ID in internal structures.
* `buffer`: Raw pixel buffer for rendering content.

---

### Behavior Flags

```cpp
bool Movable;
bool Resizable;
```

* Whether the user can move or resize the window.

```cpp
bool IsResizing;
bool IsMoving;
bool IsFocused;
bool IsMinimized;
bool IsMaximized;
```

* States indicating current window interaction or visibility.

```cpp
bool ShowTitleBar;
bool ShowBorder;
bool AlwaysOnTop;
bool RenderBackground;
```

* Controls rendering aspects of the window.

---

### Rendering

```cpp
AtlasGraphicsLibrary* agl;
ResizeDirection resizeDirection;
```

* `agl`: Pointer to the graphics library context.
* `resizeDirection`: Current direction of resizing (e.g., horizontal, vertical, diagonal).

---

### Paint Callback

```cpp
void (*Paint)(AtlasGraphicsLibrary* agl);
```

* User-defined function for rendering the window's content.
* This function is called everytime when rendering the windows, an boolean `ManualRender` can be set to true so the application handles the painting.

---

## Inner Class: `WindowDefaultStyle`

Controls appearance of the window UI components.

```cpp
class WindowDefaultStyle {
```

### Style Fields

```cpp
uint64_t WindowBorder;
uint64_t WindowTitleBar;
uint64_t WindowTitleBarActive;
uint64_t TitleBarText;
uint64_t TitleBarTextUnactive;
uint64_t WindowBackground;
```

Colors for window frame and title bar text.

```cpp
uint64_t Close;
uint64_t CloseHovered;
uint64_t ClosePressed;
uint64_t Maximize;
uint64_t MaximizeHovered;
uint64_t MaximizePressed;
uint64_t Minimize;
uint64_t MinimizeHovered;
uint64_t MinimizePressed;
uint64_t InactiveButton;
```

Colors for buttons in various states.

### Default Constructor

```cpp
WindowDefaultStyle()
    : WindowBorder(0x414559),
      WindowTitleBar(0x232634),
      WindowTitleBarActive(0x303446),
      TitleBarText(0xc6d0f5),
      TitleBarTextUnactive(0x414559),
      WindowBackground(0x232634),
      Close(0xe78284),
      CloseHovered(0xea999c),
      ClosePressed(0xb36566),
      Maximize(0x292c3c),
      MaximizeHovered(0x292c3c),
      MaximizePressed(0x292c3c),
      Minimize(0x292c3c),
      MinimizeHovered(0x292c3c),
      MinimizePressed(0x292c3c),
      InactiveButton(0x232634) {}
```

---

## Constructor: `Window(...)`

Creates a new window and allows applying a custom style and paint callback.

```cpp
Window(const char* title,
       uint64_t x, uint64_t y,
       uint64_t width, uint64_t height,
       const WindowDefaultStyle& customStyle = WindowDefaultStyle(),
       void (*Paint)(AtlasGraphicsLibrary* agl) = nullptr)
    : title(title), x(x), y(y), width(width), height(height), style(customStyle),
      old_x(0), old_y(0), old_width(0), old_height(0), buffer(nullptr),
      Resizable(true), Movable(true),
      IsResizing(false), IsMoving(false), IsFocused(false),
      IsMinimized(false), IsMaximized(false),
      ShowTitleBar(true), ShowBorder(true), AlwaysOnTop(false),
      index(0), Paint(Paint), agl(nullptr),
      resizeDirection(ResizeDirection::None) {}
```