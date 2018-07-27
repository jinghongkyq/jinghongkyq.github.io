#### Install OpenGL on Ubuntu 14.04

[cite](https://www.linuxidc.com/Linux/2017-03/141555.htm)

* Install libraries

```
sudo apt-get install build-essential
sudo apt-get install libgl1-mesa-dev
sudo apt-get install libglu1-mesa-dev
sudo apt-get install libglut-dev
```

if meet the following error: 
```
Reading package lists... Done
Building dependency tree
Reading state information... Done
E: Unable to locate package libglut-dev
```
change `sudo apt-get install libglut-dev` to `sudo apt-get install freeglut3-dev`

* Test

testing code `test.c`:

```
#include <GL/glut.h>

void init(void)
{
    glClearColor(0.0, 0.0, 0.0, 0.0);
    glMatrixMode(GL_PROJECTION);
    glOrtho(-5, 5, -5, 5, 5, 15);
    glMatrixMode(GL_MODELVIEW);
    gluLookAt(0, 0, 10, 0, 0, 0, 0, 1, 0);

    return;
}

void display(void)
{
    glClear(GL_COLOR_BUFFER_BIT);
    glColor3f(1.0, 0, 0);
    glutWireTeapot(3);
    glFlush();

    return;
}

int main(int argc, char *argv[])
{
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_RGB | GLUT_SINGLE);
    glutInitWindowPosition(0, 0);
    glutInitWindowSize(300, 300);
    glutCreateWindow("OpenGL 3D View");
    init();
    glutDisplayFunc(display);
    glutMainLoop();

    return 0;
}
```

* Compile
```
gcc -o test test.c -lGL -lGLU -lglut
```

* Execute:
```
./test
```
