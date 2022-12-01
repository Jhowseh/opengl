# OpenGL

![](https://upload.wikimedia.org/wikipedia/commons/9/99/Linux_kernel_and_OpenGL_video_games.svg)

A Open Graphics Library, mais conhecida como OpenGL é uma API livre utilizada na computação gráfica, para desenvolvimento de aplicativos gráficos, ambientes 3D, jogos, entre outros. Assim como Direct3D ou Glide, é uma API (Application Programming Interface), termo usado para classificar uma biblioteca de funções específicas disponibilizadas para a criação e desenvolvimento de aplicativos em determinadas linguagens de programação. A OpenGL foi produzida com C e C++ em mente, mas pode ser utilizada para diversas outras com um alto nível de eficiência.

<br>

## Instalação das ferramentas e componentes

• Primeiramente, é necessário instalar o <a href="https://visualstudio.microsoft.com/pt-br/downloads/">`Microsoft Visual Sudio`</a> na sua máquina, pois será com ele que iremos programar utilizando o OpenGL.
Após realizar a instalção do Visual Studio, será necessário instalar as ferramentas de `Desenvolvimento para desktop com C++` e `Desenvolvimento de jogos em C++`.

<img src="https://i.imgur.com/mb7gu2i.png" title="source: imgur.com" width="750"/>

• Da mesma forma, é preciso instalar o <a href="https://freeglut.sourceforge.net">`FreGLUT`</a>, <a href="https://glew.sourceforge.net"> `GLEW`</a> e o <a href=https://cmake.org/download/> `CMake-GUI`</a>
<details>
<summary>Manual setup</summary>
 <p>1. Na instalação do GLEW e do Free-GLUT, é recomendado baixar o código fonte dos projetos e montá-los no CMake. </p>
 <p>2. Utilizaremos o CMake para montar o Free-GLUT, então, após o CMaker ser instalado, abra-o; </p>
 <p>3. Selecione a opção <strong>Browser Source</strong> para escolher a pasta onde está o código fonte do Free-GLUT; </p>
 <p>4. Selecione a opção <strong>Browser Build</strong> para escolher a pasta onde Free-GLUT será montado; </p>
 <img src="https://preshing.com/images/cmake-gui.png" />
 <p>5. Selecione a opção <strong>Configure</strong> para escolher a IDE que será utilizada; </p>
 <p>6. Selecione o Visual Studio e clique em <i>Finish</i>; </p>
 <img src="https://preshing.com/images/cmake-choose-generator.png" />
 <p>7. Selecione todas as opções e clique em <i>Generate</i>; </p>
 <img src="https://preshing.com/images/cmake-gui-options.png" />
 <p>8. Em seguida, clique em <i>Open Project</i> e selecione o arquivo <strong>freeglut.sln</strong>, para que ele seja compilado; </p>
 <img src="https://i.imgur.com/KuyHatH.png" title="source: imgur.com" />
 <p>9. Serão criadas duas pastas chamadas de  <strong>lib</strong> e <strong>bin</strong>. Dentro da pasta "bin" tera a pasta <strong>Debug</strong>, selecione o arquivo <i>freeglutd.dll</i> e cole na pasta <strong>System32</strong> da sua máquina; </p>
 <p>10. Na pasta <i>GLEW</i> também terá um arquivo nomeado <strong>glew32.dll</strong>, cole-o na pasta <strong>System32</strong> da sua máquina. </p>

</details>

---

## Primeiros passos

• Após realizar a instalação do Visual Studio e das suas ferramentas, crie uma pasta e abrá-a com o Visual Studio;

<img src="https://i.imgur.com/5jvOdC3.png" title="source: imgur.com" width="750"/>

• Clique com o botão direito abaixo da pastar e vá até a opção `Adicionar` > `Novo Arquivo`

<img src="https://i.imgur.com/NnXQnLP.png" title="source: imgur.com" width="750"/>

• Crie um arquivo no formato `C++`, ou seja, um arquivo `.cpp`

<img src="https://i.imgur.com/GZ5i1sV.png" title="source: imgur.com" width="750"/>

• Após isso, é necessário adicionar o <a href="https://cmake.org">`CMake`</a> ao seu projeto, pois ele vai ajudar a gerenciá-lo da melhor maneira.
Adiocione um arquivo nomeado como `CMakeLists.txt`

<img src="https://i.imgur.com/voMys9C.png" title="source: imgur.com" width="750"/>
Ele vai automaticamente criar a pasta "out" com todos os seus componentes dentro dela.

• Neste arquivo, adicione a versão, nome e o arquivo do seu projeto
```cpp
cmake_minimum_required(VERSION 3.12)
project(nomeProjeto)
add_executable(nomeProjeto main.cpp)
```

<img src="https://i.imgur.com/ayjUZos.png" title="source: imgur.com" width="750"/>

## Montando o Projeto

- No diretório do seu projeto, crie uma pasta nomeada como <i>deps</i>, pois será nela onde ficarão todas as dependências do seu projeto;
- Crie uma nova pasta nomeada como <i>freeglut</i> e copie todos os arquivos da pasta "lib" que você havia montado o seu projeto;
- Extraia os binários do GLEW para a pasta <i>glew</i> dentro do diretório da <strong>deps</strong>.


## Adicionando bibliotecas

Bibliotecas utilizadas:

- GLM => Matemática
- GLFW => Criar a janela onde os objetos 3D serão renderizados
- GLEW => Carregar as funções OpenGL
- STB => Carregar as imagens com textura


<details>
<summary>Manual setup</summary>

1. Install `GLM`.

```
#include<glm/glm.hpp>
#include<glm/gtx/string_cast.hpp>
```

2. Install Tailwind and `GLFW`.

```
#include<GLFW/glfw3.h>
```
3. Install `GLEW`.

```
#include<GL/glew.h>
```
4. Install `STB`.

```
#include<stb_image.h>
```
</details>

---
 
 ## Let's Code!
 
- No arquivo <i><b>CMakeLists.txt</b></i> adicione as seguintes linhas de código:
 
 ```cpp
target_include_directories(nomeProjeto PRIVATE deps/freeglut/includedeps/glew/include)

target_link_directories((nomeProjeto PRIVATE deps/glew/lib/Release/x64deps/freeglut/lib)

target_link_libraries((nomeProjeto PRIVATE glew32.lib/freeglutd.lib)
```
 
- No arquivo <i><b>main.cpp</b></i> adicione as seguintes linhas de código:
 
 ```cpp
void initGL() {

	glClearColor(0.0f, 0.0f, 0.0f, 1.0f);
}

void display() {
	glClear(GL_COLOR_BUFFER_BIT);
	glBegin(GL_TRIANGLES);
 glColor3f(0.1, 0.1, 0.1);

	glVertex2f(0.0f,0.4f);
	glVertex2f(0.4f,0.0f);
	glVertex2f(-0.4f,0.0f);

	glEnd();

	glFlush();
}


int main(int argc, char** argv) {
	glutInit(&argc, argv);
	glutCreateWindow("Vertex, Primitive & Color");
	glutInitWindowSize(320, 320);
	glutDisplayFunc(display);
	initGL();
	glutMainLoop();
	return 0;
}
```
 
## Final Result
 
<img src="https://i.imgur.com/kCOVB80.png" title="source: imgur.com" />
 
