<p align="center">
  <img src="/proj/atlas-dev/docs/core/Atlas%20Window%20Manager/Screenshot_20250323_220912.png" alt="AWM Preview">
</p>

# Atlas Window Manager

Atlas Window Manager (AWM) is built-in kernel "module", as the name says it's a Window Manager based on the Atlas Advanced Graphics.

It could be renderer either on the Framebuffer or in a AVT Framebuffer.
AWM requires a 2nd framebuffer, called BackBuffer used for double-buffering.

## Design (User Interface)

AWM is designed to be minimal, but at the same time nice looking with the Catppuccin Frappe color scheme.


## Funcionality

AWM source code is simple, it's designed to be easy to understand and to use.
Resizing, Minimizing, Maximizing, Moving windows.