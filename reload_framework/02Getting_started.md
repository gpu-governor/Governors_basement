# Introduction

Graphical User Interfaces (GUIs) are essential in making software interactive and user-friendly. They provide a visual way for users to interact with the system, as opposed to text-based interfaces. GUIs can be categorized into two primary modes: Retained Mode and Immediate Mode.

### Retained Mode vs Immediate Mode GUI

**Retained Mode GUI:**
- **Definition:** In a retained mode GUI, the GUI framework retains the state of the interface elements. You define the structure and properties of your GUI elements (like windows, buttons, etc.), and the framework manages their rendering, event handling, and state changes.
- **Example Libraries:** Qt, GTK, Wxwidgets, Tkinter.

**Pros:**
  - Easier to maintain state across frames.
  - Typically has a more structured approach, which can be easier to manage in larger applications.
  - Often includes more built-in features and widgets.

**Cons:**
  - Can be less flexible for highly dynamic interfaces.
  - Can be more complex to use, requiring more boilerplate code.

**Immediate Mode GUI:**
- **Definition:** In an immediate mode GUI, the state of the GUI elements is not retained by the framework. Instead, you explicitly draw the GUI elements each frame, based on the current state of your application.
- **Example Libraries:** ImGui, Nuklear, RayGui.

**Pros:**
  - Highly flexible and suitable for dynamic interfaces.
  - Simplified state management as the entire GUI is re-rendered each frame.
  - Typically easier to integrate into game engines or other real-time applications.

**Cons:**
  - Can be more challenging to manage complex states.
  - Performance can be an issue for very large and complex UIs, though this is mitigated by efficient implementations like ImGui.

### What are Backends (Graphics APIs and Libraries)

In the context of GUI libraries, backends refer to the underlying systems responsible for rendering the GUI and handling input events. These backends can vary based on the platform and the rendering technology used.

**Graphics APIs:**
- **OpenGL:** A cross-platform graphics API that is widely used for rendering 2D and 3D graphics. Many GUI libraries, including ImGui, can use OpenGL as a backend.
- **DirectX:** A collection of APIs developed by Microsoft, primarily used for rendering 2D and 3D graphics on Windows.
- **Vulkan:** A low-overhead, cross-platform API designed for high-performance 3D graphics applications.

**Libraries:**
- **SDL (Simple DirectMedia Layer):** A cross-platform development library that provides low-level access to audio, keyboard, mouse, joystick, and graphics hardware. It can be used as a backend for GUI libraries to handle window creation, input, and rendering.
- **Allegro:** Another cross-platform library similar to SDL, providing modules for handling windowing, graphics, audio, and networking.
- **GLFW:** A library specifically designed for creating windows with OpenGL contexts and handling input.

**Choosing a Backend:**
The choice of backend depends on the requirements of your application, the platforms you are targeting, and the specific features you need.
- For cross-platform compatibility, OpenGL combined with SDL or GLFW is a common choice.
- For Less external Dependencies and easy integration, using SDL only is ideal [Backend+window].
- For a more modern cross platform aproach, Vulkan combined with SDL or GLFW is a common choice.
- For applications targeting only Windows, DirectX might be preferred due to its tight integration with the Windows operating system.

By understanding these concepts, you can make informed decisions when designing and implementing GUI systems for your applications. Whether you choose retained mode for its structured approach or immediate mode for its flexibility, and which backend to use, will depend on your specific needs and the context of your project.

# In this Tutorials
we will teach imgui :
* Generally without a specific backend
* with glfw + OpenGL
* with sdl2 + OpenGL
* with glfw + vulkan
* with sdl2 + sdl2 backend
* with sdl3 

[Return to Main menu](introduction.md)