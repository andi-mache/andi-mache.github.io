---
layout: post
title: Making a window in opengl for linux
date: 2021-11-04
categories: ["graphics programming", "linux", "opengl"]
---

Hi guys welcome to my **opengl series** , i have recently developed an interest in graphics programming ,so i am crating this series to track my progress.

In this post we will just create a blank window, i am going to use glfw and glew as the opengl extension loader

# STRUCTURE 

first lets create our directories
```
mkdir bin obj include src 

touch Makefile src/main.cpp 

```
it should now look like this 
```
myproject
    |-obj 
    |-src 
         |-main.cpp
    |-bin 
    |-include 
  Makefile
```

# Creating a Window in OpenGL using GLFW and GLEW on Linux

Creating a window in OpenGL using GLFW and GLEW on Linux involves several steps. Here's a step-by-step guide on how to do it:

## Include the Necessary Libraries

You need to include the GLFW and GLEW libraries in your program. GLFW is used for creating windows and handling input, while GLEW is used for loading OpenGL functions.

```cpp
#include <GLFW/glfw3.h> #include <GL/glew.h>
```

## Initialize GLFW

Before you can create a window, you need to initialize GLFW. If initialization fails, you should terminate the program.
```cpp 
if (!glfwInit()) { fprintf(stderr, "Failed to initialize GLFW\n"); return -1; }

```

## Set Window Hints

GLFW allows you to set various window hints before creating the window. For example, you can set the version of OpenGL you want to use.

```cpp 
glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3); glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3); glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
```

## Create a Window

You can create a window using the `glfwCreateWindow` function. This function takes the width and height of the window, the title of the window, and two optional parameters for the monitor and the share. If the window or OpenGL context creation fails, NULL will be returned.

```cpp 
 GLFWwindow* window = glfwCreateWindow(800, 600, "LearnOpenGL", NULL, NULL); if (window == NULL) { fprintf(stderr, "Failed to create GLFW window\n"); glfwTerminate(); return -1; }
```

## Make the Context Current

After creating the window, you need to make the context of the window current. This is done using the `glfwMakeContextCurrent` function.
```cpp
glfwMakeContextCurrent(window);


```

## Initialize GLEW

After making the context current, you can initialize GLEW. This will load all the OpenGL functions.

```cpp 
glewExperimental = GL_TRUE; GLenum err = glewInit(); if (err != GLEW_OK) { fprintf(stderr, "Failed to initialize GLEW\n"); return -1; }

```

## Main Loop

Finally, you can enter the main loop where you will render your graphics and handle user input. This loop continues until the user closes the window.

```cpp 
while (!glfwWindowShouldClose(window)) { // Render here glClear(GL_COLOR_BUFFER_BIT);

// Swap front and back buffers glfwSwapBuffers(window);

// Poll for and process events glfwPollEvents(); }

glfwTerminate(); return 0;


```

This is a basic example of creating a window in OpenGL using GLFW and GLEW on Linux. Depending on your needs, you might want to add more functionality, such as handling user input, rendering graphics, etc.

Sources: [Source 0](https://www.glfw.org/docs/latest/quick.html), [Source 1](https://www.glfw.org/docs/latest/window_guide.html), [Source 5](https://learnopengl.com/Getting-started/Hello-Window), [Source 6](https://learnopengl.com/Getting-started/Creating-a-window), [Source 8](https://www.glfw.org/documentation)

