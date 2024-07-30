# Your First "Hello Window!" with MicroUI

MicroUI is a minimalist and efficient graphical user interface library designed for embedded systems. Its lightweight nature makes it ideal for projects where resources are limited. In this tutorial, we'll walk you through creating your first "Hello Window!" application using MicroUI. We'll explore two approaches: using SDL and GLFW for window management and rendering.

## Prerequisites

Before we start, ensure you have the following installed on your system:

1. **C Compiler** (e.g., GCC or Clang)
2. **SDL** (for the SDL version)
3. **GLFW** (for the GLFW version)
4. **MicroUI** (available from its official repository)

## Setting Up Your Development Environment

First, make sure you have the necessary libraries installed.

### Installing SDL

For Linux:

```sh
sudo apt-get install libsdl2-dev
```

For macOS:

```sh
brew install sdl2
```

For Windows:

Download the development libraries from the [SDL website](https://www.libsdl.org/download-2.0.php) and follow the installation instructions.

### Installing GLFW

For Linux:

```sh
sudo apt-get install libglfw3-dev
```

For macOS:

```sh
brew install glfw
```

For Windows:

Download the development libraries from the [GLFW website](https://www.glfw.org/download.html) and follow the installation instructions.

## Creating "Hello Window!" with SDL

Let's start by creating a simple window using SDL and MicroUI.

### Step 1: Create the Project Structure

Create a directory for your project and navigate into it.

```sh
mkdir hello_window_sdl
cd hello_window_sdl
```

### Step 2: Write the Code

Create a file named `main.c` and add the following code:

```c
#include <SDL2/SDL.h>
#include "microui.h"

int main(int argc, char *argv[]) {
    if (SDL_Init(SDL_INIT_VIDEO) != 0) {
        printf("SDL_Init Error: %s\n", SDL_GetError());
        return 1;
    }

    SDL_Window *window = SDL_CreateWindow("MicroUI Hello Window!",
                                          SDL_WINDOWPOS_CENTERED,
                                          SDL_WINDOWPOS_CENTERED,
                                          800, 600, SDL_WINDOW_SHOWN);
    if (!window) {
        printf("SDL_CreateWindow Error: %s\n", SDL_GetError());
        SDL_Quit();
        return 1;
    }

    SDL_Renderer *renderer = SDL_CreateRenderer(window, -1, SDL_RENDERER_ACCELERATED);
    if (!renderer) {
        SDL_DestroyWindow(window);
        printf("SDL_CreateRenderer Error: %s\n", SDL_GetError());
        SDL_Quit();
        return 1;
    }

    mu_Context ctx;
    mu_init(&ctx);

    // Main loop
    int running = 1;
    while (running) {
        SDL_Event event;
        while (SDL_PollEvent(&event)) {
            if (event.type == SDL_QUIT) {
                running = 0;
            }
            // Handle input events and pass them to MicroUI
        }

        SDL_SetRenderDrawColor(renderer, 0, 0, 0, 255);
        SDL_RenderClear(renderer);

        // Render MicroUI elements
        mu_begin(&ctx);
        mu_end(&ctx);

        SDL_RenderPresent(renderer);
    }

    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    SDL_Quit();

    return 0;
}
```

### Step 3: Compile and Run

Compile your program using the following command:

```sh
gcc -o hello_window main.c -lSDL2
```

Run the program:

```sh
./hello_window
```

You should see a window titled "MicroUI Hello Window!" with a black background.

## Creating "Hello Window!" with GLFW

Now, let's create the same window using GLFW and MicroUI.

### Step 1: Create the Project Structure

Create a directory for your project and navigate into it.

```sh
mkdir hello_window_glfw
cd hello_window_glfw
```

### Step 2: Write the Code

Create a file named `main.c` and add the following code:

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

    GLFWwindow* window = glfwCreateWindow(800, 600, "MicroUI Hello Window!", NULL, NULL);
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
        mu_end(&ctx);

        glfwSwapBuffers(window);
    }

    glfwDestroyWindow(window);
    glfwTerminate();

    return 0;
}
```

### Step 3: Compile and Run

Compile your program using the following command:

```sh
gcc -o hello_window main.c -lglfw -lGL
```

Run the program:

```sh
./hello_window
```

You should see a window titled "MicroUI Hello Window!" with a black background.

## Conclusion

Congratulations! You've created your first "Hello Window!" application using MicroUI with both SDL and GLFW. These simple examples provide a foundation for building more complex graphical user interfaces in resource-constrained environments. As you continue to explore MicroUI, you'll discover its flexibility and efficiency in creating lightweight and responsive UIs.
