# MicroUI Usage With and Without SDL

MicroUI is a lightweight and efficient graphical user interface library designed for embedded systems. It offers a minimalistic approach to UI development, focusing on simplicity and performance. When working with MicroUI, developers have the option to use it with or without the Simple DirectMedia Layer (SDL). This article explores the differences and considerations for using MicroUI in both contexts.

## What is MicroUI?

MicroUI is a small, portable GUI library that provides essential UI components and rendering capabilities. It is designed to run on resource-constrained systems, making it ideal for embedded applications. MicroUI offers features such as:

- Basic UI controls (buttons, sliders, checkboxes)
- Customizable themes and styles
- Event handling and input management
- Simple drawing and rendering functions

## What is SDL?

SDL, or Simple DirectMedia Layer, is a cross-platform software development library that provides low-level access to audio, keyboard, mouse, joystick, and graphics hardware via OpenGL and Direct3D. SDL is widely used in game development and multimedia applications due to its portability and ease of use.

## Using MicroUI With SDL

When integrating MicroUI with SDL, developers leverage SDL's capabilities to handle window management, input, and rendering. Here are the key benefits and considerations:

### Benefits of Using SDL with MicroUI

1. **Cross-Platform Compatibility**: SDL abstracts the platform-specific details, allowing MicroUI applications to run on various operating systems, including Windows, macOS, Linux, and even mobile platforms.

2. **Advanced Input Handling**: SDL provides robust input handling for keyboards, mice, touchscreens, and game controllers, enhancing the interactivity of MicroUI applications.

3. **Hardware Acceleration**: SDL supports hardware-accelerated rendering through OpenGL and Direct3D, enabling smoother and more efficient graphics performance.

4. **Audio Support**: SDL includes audio capabilities, which can be useful for applications that require sound effects or music.

### Example of MicroUI with SDL

```c
#include <SDL2/SDL.h>
#include "microui.h"

int main(int argc, char *argv[]) {
    SDL_Init(SDL_INIT_VIDEO);

    SDL_Window *window = SDL_CreateWindow("MicroUI with SDL",
                                          SDL_WINDOWPOS_CENTERED,
                                          SDL_WINDOWPOS_CENTERED,
                                          800, 600, SDL_WINDOW_SHOWN);
    SDL_Renderer *renderer = SDL_CreateRenderer(window, -1, SDL_RENDERER_ACCELERATED);

    mu_Context ctx;
    mu_init(&ctx);

    // Main loop
    while (1) {
        SDL_Event event;
        while (SDL_PollEvent(&event)) {
            if (event.type == SDL_QUIT) {
                SDL_Quit();
                return 0;
            }
            // Handle input events and pass them to MicroUI
        }

        SDL_SetRenderDrawColor(renderer, 0, 0, 0, 255);
        SDL_RenderClear(renderer);

        // Render MicroUI elements
        mu_begin(&ctx);
        // Define UI elements here
        mu_end(&ctx);

        SDL_RenderPresent(renderer);
    }

    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    SDL_Quit();

    return 0;
}
```

## Using MicroUI Without SDL (with GLFW)

Using MicroUI without SDL can be achieved by using GLFW, another lightweight library for creating windows, receiving input, and handling OpenGL context creation. GLFW is suitable for applications that need to stay minimalistic while still providing robust window and input management.

### Benefits of Using GLFW with MicroUI

1. **Reduced Overhead**: GLFW is smaller and more lightweight than SDL, which can be crucial for systems with strict resource constraints.

2. **Custom Hardware Access**: Developers have direct control over the hardware, allowing for highly optimized and specialized implementations.

3. **Cross-Platform**: Similar to SDL, GLFW supports multiple platforms including Windows, macOS, and Linux, but with a smaller footprint.

### Example of MicroUI with GLFW

```c
#include <GLFW/glfw3.h>
#include "microui.h"

// Custom function to handle input events
void handle_input(GLFWwindow* window, mu_Context* ctx) {
    // Handle input events and pass them to MicroUI
}

int main() {
    if (!glfwInit()) {
        return -1;
    }

    GLFWwindow* window = glfwCreateWindow(800, 600, "MicroUI with GLFW", NULL, NULL);
    if (!window) {
        glfwTerminate();
        return -1;
    }

    glfwMakeContextCurrent(window);

    mu_Context ctx;
    mu_init(&ctx);

    // Main loop
    while (!glfwWindowShouldClose(window)) {
        glfwPollEvents();
        handle_input(window, &ctx);

        glClear(GL_COLOR_BUFFER_BIT);

        // Render MicroUI elements
        mu_begin(&ctx);
        // Define UI elements here
        mu_end(&ctx);

        glfwSwapBuffers(window);
    }

    glfwDestroyWindow(window);
    glfwTerminate();

    return 0;
}
```

## Conclusion

MicroUI offers a flexible and efficient solution for creating graphical user interfaces on embedded systems. By choosing to use MicroUI with SDL or GLFW, developers can tailor their applications to meet specific requirements. SDL provides a powerful and portable foundation for more complex applications, while using MicroUI with GLFW offers a more lightweight alternative. Understanding the strengths and limitations of each approach is essential for making the right choice for your project's needs.
