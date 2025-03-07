# Installing OpenGL

Follow this guide for setting up OpenGL on your system

# Install required dependencies

1. **GLFW** (for creating a window and OpenGL context):
    - Download the source code from [GLFW's website](https://www.glfw.org/download.html).
  
        ![alt text](https://github.com/[abraham-vijai]/[Setting-Up-OpenGL]/blob/[main]/glfw.png?raw=true)
        
2. **GLM** (OpenGL Mathematics library, optional but recommended):
    - Download from [GLM's GitHub](https://github.com/g-truc/glm).

# Setup GLAD

1. Go to the GLAD website [https://glad.dav1d.de/](https://glad.dav1d.de/)
2. Set `gl` version to at least `3.3` (or higher, depending on your needs).
3. Set `Profile` to `Core`.
4. Check `Generate a loader`.
5. Extract the `.zip` file into your project directory. You should see two folders: `include` and `src`

# Setting up the Project structure

## Setup library

1. Create a folder called `Libraries` inside your project structure
2. Copy the extracted GLFW folder to the `Libraries` folder
3. Copy the `include` and `src` extracted from the glad folder to the `Libraries`  folder
4. Copy the extracted files from the `glm` folder to the `Libraries`  folder
    
    You folder structure should look something like this:
    
    ```
    📦Libraries
     ┣ 📂glad
     ┃ ┣ 📂include
     ┃ ┗ 📂src
     ┣ 📂glfw-3.4
     ┃ ┗ 📂...
     ┗ 📂glm
       ┗ 📂... 
    ```
    

## Setup Visual Studio

1. Create your Visual Studio Properties
2. Go to `Project`->`<Your_Project_Name> Properties`->`VC++ Directories`
3. Click on `Include Directories` and add the path of the folders in the `Libraries` folder
4. Go to the below directory and copy the path and add to the `Library Directories` section
    
    ```cpp
    glfw-3.4\build\src\Debug
    ```
    

![alt text](https://github.com/[abraham-vijai]/[Setting-Up-OpenGL]/blob/[main]/properties.png?raw=true)

## Copy the source code

1. Copy the `glad.c` file in your `main.cpp` folder

# **Simple OpenGL Program**

```cpp
#include <glad/glad.h>
#include <GLFW/glfw3.h>
#include <iostream>

void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
    glViewport(0, 0, width, height);
}

int main() {
    // Initialize GLFW
    if (!glfwInit()) {
        std::cout << "Failed to initialize GLFW" << std::endl;
        return -1;
    }

    // Set OpenGL version to 3.3
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

    // Create a window
    GLFWwindow* window = glfwCreateWindow(800, 600, "OpenGL with GLAD", NULL, NULL);
    if (!window) {
        std::cout << "Failed to create GLFW window" << std::endl;
        glfwTerminate();
        return -1;
    }
    glfwMakeContextCurrent(window);

    // Initialize GLAD
    if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
        std::cout << "Failed to initialize GLAD" << std::endl;
        return -1;
    }

    // Set up viewport
    glViewport(0, 0, 800, 600);
    glfwSetFramebufferSizeCallback(window, framebuffer_size_callback);

    // Main loop
    while (!glfwWindowShouldClose(window)) {
        // Clear the screen
        glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
        glClear(GL_COLOR_BUFFER_BIT);

        // Swap buffers and poll events
        glfwSwapBuffers(window);
        glfwPollEvents();
    }

    // Clean up
    glfwTerminate();
    return 0;
}
```
