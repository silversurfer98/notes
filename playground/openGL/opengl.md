## setting up the project [documentation](https://docs.gl/) [[C++]]

1. opengl32.lib should be statically linked to the project, don't panic abt 32 as 32-bit, it is 64-bit
2. we need glfw for accessing opengl function which is written by our Grapics card, **openGL is not a lib
3. while GLFW is a lib, but to make our life easy we use GLEW as a wrapper 
4. GLFW and GLEW libs can be linked statically or dynamically.
5. hello world prog --> this doest use glew
```c++
#include <glfw3.h>

int main(void)
{
    GLFWwindow* window;

    /* Initialize the library */
    if (!glfwInit())
        return -1;

    /* Create a windowed mode window and its OpenGL context */
    window = glfwCreateWindow(640, 480, "Hello World", NULL, NULL);
    if (!window)
    {
        glfwTerminate();
        return -1;
    }

    /* Make the window's context current */
    glfwMakeContextCurrent(window);

    /* Loop until the user closes the window */
    while (!glfwWindowShouldClose(window))
    {
        /* Render here */
        glClear(GL_COLOR_BUFFER_BIT);

        /* Swap front and back buffers */
        glfwSwapBuffers(window);

        /* Poll for and process events */
        glfwPollEvents();
    }

    glfwTerminate();
    return 0;
}
```

6. uses of GLEW is to bring out the **modern features of openGL [cherno-glew](https://www.youtube.com/watch?v=H2E3yO0J7TM&list=PLlrATfBNZ98foTJPJ_Ev03o2oq3-GGOS2&index=3)
	- **and it should be above glfw header declaration
	- we need to define GLEW_STATIC because by default glew header looks for DLL lib, if we isuue that defenition the lib will be linked statically xD
	- [Documentation](https://glew.sourceforge.net/basic.html)
	- First you need to create a valid OpenGL rendering context and call glewInit() to initialize the extension entry points. If glewInit() returns GLEW_OK, the initialization succeeded and you can use the available extensions as well as core OpenGL functionality.
	- what I mean above is initialize glew or glad only after u have a proper context
```c++
// to include glew
#define GLEW_STATIC
#include <GL/glew.h>  

//after this -->
 /* Make the window's context current */
    glfwMakeContextCurrent(window);

    //intialize glew after proper context
    if (glewInit() != GLEW_OK)
        std::cout << "glew load error \n";
```

> to see --> [reddit](https://www.reddit.com/r/opengl/comments/zsn2ju/how_to_draw_circles_with_shaders/) and [git](https://github.com/shansen16/code-dump)
