# setting up imgui
welcome back to the continuation of our imgui series, in our last tutorial we showed :
<pre>
<code class="language-cpp">
#include "imgui.h"
int main() {
    // Setup code for ImGui
    ImGui::CreateContext();
    ImGuiIO& io = ImGui::GetIO(); // Access IO for configuration

    // Main loop
    while (true) {
        // Start a new frame
        ImGui::NewFrame();

        // Create a simple window
        ImGui::Begin("Hello, world!");
        ImGui::Text("This is some text");
        ImGui::End();

        // Render the frame
        ImGui::Render();
    }

    // Cleanup
    ImGui::DestroyContext();
    return 0;
}
</code>
</pre>

This is the basic setup for using ImGui, but you'll need to integrate it with a graphics library like OpenGL, SDL, or GLFW to get rendering and input handling.
---
if you have been follow this series of imgui tutorials you can recall that we have not setup (installed) imgui on our computer yet, so we are going to be doing that now.
## step 1:
1. create a directory with any name you choose, my is "my_project"
2.open your browser and go to the official imgui github repo, download the source code.
3. extract the downloaded zip file, a new imgui-master folder will appear
4. in the imgui folder you would see these list of files:
5. copy all files that has imgui in it's name, paste them in your "my_project" folder
6. Go back to the imgui folder and go into backend, you would see different backend files. you can copy only the files relevant to the backend you are using but i would recommend you copy the entire backend folder over to your "my_project" directory
7. your "my_project" directory should look like this

This is all you would need

---
# Checking out imgui examples
if you go back to the imgui folder you downloaded, you would see a sub folder called examples. This folder contain different imgui examples for different backends.

all you have to do is decide the backend you want to use and copy it's examples (files and folder). 

let's assume we are using the SDL2+SDL_renderer backend, just copy it's directory. if you are not using SDL, copy the example folder of the backend you are using and follow along,


