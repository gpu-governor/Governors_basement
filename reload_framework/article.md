# Imgui Basics
Before We setup imgui for specific backend we will learn basic concept of imgui without a backend.

Let's assume Imgui is already installed.

## step 1:
create a file named `fake_imgui.cpp`
## step 2:
in every C++ program we will have to include necessary files and libraries, so in our `fake_imgui.cpp` we will include:
<pre>
<code class="language-cpp">
// include Imgui files
#include "imgui.h"
#include "imgui_impl_backend.h"
#include "imgui_impl_backend.h"
// include backend
#include< backend.h>
</code>
</pre>

as you see above, where we include backend will depend on the backend (graphics lib) you are using, if you are using SDL+Direct11 for example:
<pre>
<code class="language-cpp">
#include "imgui.h"
#include "imgui_impl_sdl2.h"
#include "imgui_impl_dx11.h"
#include < d3d11.h>
#include < stdio.h>
#include < SDL.h>
#include < SDL_syswm.h>
</code>
</pre>

or if you are using Vulkan+glfw you will include:
<pre>
<code class="language-cpp">
#include "imgui.h"
#include "imgui_impl_glfw.h"
#include "imgui_impl_vulkan.h"
#include <stdio.h>          // printf, fprintf
#include <stdlib.h>         // abort
#define GLFW_INCLUDE_NONE
#define GLFW_INCLUDE_VULKAN
#include <GLFW/glfw3.h>

// Volk headers
#ifdef IMGUI_IMPL_VULKAN_USE_VOLK
#define VOLK_IMPLEMENTATION
#include <volk.h>
#endi
</code>
</pre>

but for this tutorial, just leave `#include< backend.h>` as is

## step 3:
as every normal c++ program, you would create a main function:
<pre>
<code class="language-cpp">
#include "imgui.h"
#include "imgui_impl_backend.h"
#include "imgui_impl_backend.h"
#include< backend.h>

int main(){
  // TODO
  return 0;
}
</code>
</pre>

next you would want to initialize your backend and create a window in your main function:
<pre>
<code class="language-cpp">
int main(){
  create_window(win,"imgui",640,480);
  //TODO: Setup Dear ImGui context
  
  bool quit= true;
  while(quit){
    // TODO: imgui rendering
    
  }
  
  destroy_window(win);
  return 0;
}
</code>
</pre>

in the above we used an imaginery graphics library scheme (that does not exist). But however, the process is the same for any backend, wether you use Vulkan, Opengl or DirectX you will have to initialize it, create a window, create a Game loop and then de-intialize it.

## step 4: 
since we have our imaginery backend setuped, we can then initialize imgui and start drawing:
<pre>
<code class="language-cpp">
int main(){
  create_window(win,"imgui",640,480);
  //Setup Dear ImGui context
    IMGUI_CHECKVERSION();
    ImGui::CreateContext();
    ImGuiIO& io = ImGui::GetIO(); (void)io;
    io.ConfigFlags |= ImGuiConfigFlags_NavEnableKeyboard;     // Enable Keyboard Controls
    io.ConfigFlags |= ImGuiConfigFlags_NavEnableGamepad;      // Enable Gamepad Controls

    // Setup Dear ImGui style
    ImGui::StyleColorsDark();
    //ImGui::StyleColorsLight();

    // Setup Platform/Renderer backends
    ImGui_Impl_InitForBackend(window, renderer);
    ImGui_Impl_Renderer_Init(renderer);
  
  bool quit= true;
  while(quit){
    // TODO: imgui rendering
    
  }
  
  destroy_window(win);
  return 0;
}
</code>
</pre>

the added lines of code for imgui context Setup checks the imgui version, create context, enable keyboard, enable gamepad, ...
and then we set imgui Theme to Dark and we then setup the Platform backend, note that the platform backend setup varies to the specific backend you are using.


## Step 5: Drawing a Simple ImGui Window

In this step, we’ll focus solely on drawing a basic ImGui window within the main loop.

 <pre>
 <code class="language-cpp">
    while (!quit) {
        // Start the ImGui frame
        ImGui_Impl_NewFrameBackend();  // Start new frame for backend
        ImGui::NewFrame();             // Start ImGui frame

        // Draw ImGui window and text
        ImGui::Begin("Hello, ImGui!");           // Create a new window
        ImGui::Text("This is some text!");       // Display some text inside the window
        ImGui::End();                            // End the window

        // Rendering
        ImGui::Render();  // Collect all ImGui draw commands
        ImGui_Impl_Renderer_RenderDrawData(ImGui::GetDrawData()); // Render the ImGui data

        // TODO : handing events (we will cover this next chapter)
        
        present_backend_frame();      // Custom function to display the rendered frame
    }

    // TODO Continue to Step 6 for cleanup
    return 0;
}
 </code>
 </pre>

Explanation:
we have populated our loop with codes, let's break down everything we did  in simple terms:

1. while (!quit): This is a loop that keeps running until you tell the program to stop (i.e., quit becomes true). The loop keeps things active, allowing your app to keep updating and drawing.


2. ImGui_Impl_NewFrameBackend(): This function prepares the backend (whatever system you're using, like SDL, OpenGL, etc.) to start a new frame. Think of it as clearing the drawing board for the next picture you're going to paint.


3. ImGui::NewFrame(): This starts a new ImGui frame, meaning you’re telling ImGui, "I'm going to create some UI elements for this frame."


4. ImGui::Begin("Hello, ImGui!"): This opens up a new window in your UI. It's like saying, "Start drawing a window titled 'Hello, ImGui!'"


5. ImGui::Text("This is some text!"): Inside that window, you're displaying the text "This is some text!". It's like adding a label inside the window.


6. ImGui::End(): This closes the window. You're done adding things to this window for now.


7. ImGui::Render(): Now that you've told ImGui what to display (a window with text), this step prepares everything for drawing. It figures out where and how to display what you created.


8. ImGui_Impl_Renderer_RenderDrawData(ImGui::GetDrawData()): This sends the prepared ImGui drawing commands to the actual rendering system. It’s like handing your instructions to the painter to start painting on the canvas.


9. present_backend_frame(): Another custom function, which takes the painted canvas (your UI) and shows it on the screen. It's like flipping the canvas over for everyone to see.



And the loop keeps going, updating and drawing the UI until the user decides to quit.

Finally, once you exit the loop, you’d go to step 7, which would be cleaning up and closing things down properly.





---

## Step 6 : Cleanup

After the main loop is done (i.e., when the user decides to quit the application), it’s important to clean up ImGui and the backend.
<pre>
<code class="language-cpp">
int main() {
    // Setup code as in Step 5...

    bool quit = false;
    while (!quit) {
        // ImGui frame and rendering as in Step 5...
    }

    // Cleanup
    ImGui_Impl_Renderer_Shutdown();      // Cleanup the Renderer backend
    ImGui_Impl_ShutdownForBackend();     // Cleanup the Platform backend
    ImGui::DestroyContext();             // Destroy ImGui context
    destroy_window(win);                 // Destroy the window and backend

    return 0;
}
</code>
</pre>

Explanation:

1. ImGui Cleanup:

ImGui_Impl_Renderer_Shutdown() cleans up the renderer backend.

ImGui_Impl_ShutdownForBackend() shuts down the platform-specific backend (e.g., SDL, GLFW).

ImGui::DestroyContext() destroys the ImGui context, freeing any resources allocated by ImGui.



2. Backend Cleanup:

The destroy_window(win) function (or its equivalent for your backend) cleans up the window and any other resources specific to your graphics library.



