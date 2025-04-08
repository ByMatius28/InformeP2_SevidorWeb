# Práctica Servidor Web

**Implementación de Servidores Web Usando Contenedores Nginx en Play with Docker**

## 2. Tiempo de duración

**60-90 minutos**

## 3. Fundamentos

Docker es una plataforma que permite ejecutar aplicaciones dentro de contenedores. Estos contenedores son entornos ligeros, portables y consistentes que contienen todo lo necesario para que una aplicación funcione: código, bibliotecas, herramientas del sistema y configuraciones. A diferencia de las máquinas virtuales, los contenedores no necesitan un sistema operativo completo, ya que comparten el kernel del sistema anfitrión, lo cual los hace más rápidos y eficientes.

Nginx, por su parte, es un servidor web de alto rendimiento, capaz de manejar miles de conexiones simultáneas con un bajo consumo de recursos. Se utiliza comúnmente como servidor web estático, proxy inverso o balanceador de carga. Gracias a su diseño modular y su eficiencia, es ideal para aplicaciones que requieren rendimiento y estabilidad.

Play with Docker (PWD) es una plataforma gratuita en línea que permite utilizar Docker desde el navegador sin necesidad de instalar nada. Es ideal para prácticas, pruebas y aprendizaje, ya que proporciona nodos temporales con Docker preinstalado.

Esta práctica consiste en desplegar dos contenedores con Nginx, modificando el contenido de uno de ellos para demostrar el uso de los comandos `docker run` y `docker cp`, así como la exposición de puertos y visualización del contenido desde el navegador.

## 4. Conocimientos previos

- Manejo básico de terminal Linux
- Uso del comando `docker`
- Edición de archivos HTML con editores como `nano` o `vi`
- Conocimientos sobre puertos en redes
- Concepto de servidor web
- Navegación por interfaces web

## 5. Objetivos a alcanzar

- Crear y ejecutar contenedores con Nginx en la plataforma Play with Docker.
- Exponer servicios web a través de puertos personalizados.
- Editar contenido HTML dentro de un contenedor Nginx.
- Comprender el uso de `docker cp` para transferir archivos entre el host y el contenedor.

## 6. Equipo necesario

- Computadora con conexión a internet
- Navegador web moderno (Chrome, Firefox, etc.)
- Cuenta activa en [Play with Docker](https://labs.play-with-docker.com)
- Docker versión 20.x.x (integrada en PWD)
- Editor de texto como `nano` o `vi`

## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Documentación oficial de Nginx](https://nginx.org/en/docs/)
- Apuntes de clases del módulo de virtualización
- Guías rápidas de comandos Linux (cheat sheet)
- Manual del docente

## 8. Procedimiento

### Paso 1: Ingresar a Play with Docker

1. Accede a la página [https://labs.play-with-docker.com/](https://labs.play-with-docker.com/).
2. Inicia sesión con tu cuenta de Docker.
3. Crea una nueva sesión haciendo clic en "Start".

---

### Paso 2: Crear una instancia o nodo

1. Haz clic en el botón `+ ADD NEW INSTANCE`.
2. Espera unos segundos hasta que el entorno esté listo.

---

### Paso 3: Crear el primer contenedor Nginx

1. En la terminal, escribe el siguiente comando para crear el contenedor `nginx1`:

   ```bash
   docker container run --name nginx1 -d -p 8089:80 nginx
   ```

2. Este comando crea y ejecuta un contenedor llamado `nginx1`, exponiendo el puerto 8089 en el sistema anfitrión y redirigiéndolo al puerto 80 del contenedor.

---

### Paso 4: Crear el segundo contenedor Nginx

1. Ahora, ejecuta el siguiente comando para crear un segundo contenedor:

   ```bash
   docker container run --name nginx2 -d -p 8090:80 nginx
   ```

2. Este contenedor se llamará `nginx2` y funcionará en el puerto 8090.

---

### Paso 5: Verificar que los contenedores estén activos

1. Escribe el siguiente comando para ver los contenedores en ejecución:

   ```bash
   docker ps
   ```
   Para listar todos los containers Activos
   ```bash
   docker container ls -a
   ```
   Para listar todos los container
   ```bash
   docker container ls
   ``` 
   Para listar todos los container activos

2. Deberías ver ambos contenedores (`nginx1` y `nginx2`) listados con sus puertos correspondientes.

---

### Paso 6: Copiar el archivo `index.html` del contenedor nginx1 al host

1. Ejecuta el siguiente comando para copiar el archivo HTML original del contenedor `nginx1`:

   ```bash
   docker cp nginx1:/usr/share/nginx/html/index.html ./index1.html
   ```
   y realizamos lo mismo con el nginx2
    
    ```bash
   docker cp nginx2:/usr/share/nginx/html/index.html ./index2.html
   ```

2. Este comando extrae el archivo `index.html` y lo guarda en tu directorio actual con el nombre `index1.html`,`index2.html`.

---

### Paso 7: Editar el archivo HTML

1. Abre el archivo copiado con un editor de texto como `nano`:

   ```bash
   vi index1.html
   ```

2. Modifica el contenido del archivo. Por ejemplo:

   ```html
   <h1>Bienvenidos al Instituto Tecnológico</h1>
   <p>Práctica realizada en Play with Docker - Curso de Servidores Web.</p>
   ```
3. Guarda los cambios y cierra el editor (`esc`, luego `:wq` y `Enter` en `vi`).

y realizamos lo mismo en el nginx2
   
   ```bash
   vi index2.html
   ```

2. Modifica el contenido del archivo. Por ejemplo:

   ```html
   <h1>Información Personal</h1>
   <p>Aqui va la información personal</p>
   ```
3. Guarda los cambios y cierra el editor (`esc`, luego `:wq` y `Enter` en `vi`).
---

### Paso 8: Copiar el archivo HTML modificado de vuelta al contenedor nginx1

1. Utiliza el siguiente comando para reemplazar el archivo original del contenedor con la versión modificada:

   ```bash
   docker cp index1.html nginx1:/usr/share/nginx/html/index.html
   ```
   y realizamos lo mismo con el nginx2

   ```bash
   docker cp index2.html nginx2:/usr/share/nginx/html/index.html
   ```

---

### Paso 9: Visualizar los resultados en el navegador

1. En Play with Docker, haz clic en el botón que aparece junto al puerto `8089` para abrir `nginx1` en el navegador.

   - Deberías ver la página personalizada que editaste en el paso anterior.

2. Haz clic en el botón junto al puerto `8090` para abrir `nginx2`.

   - Verás la página predeterminada de bienvenida de Nginx.

---

### Paso 10: Finalizar y detener los contenedores (opcional)

1. Si deseas detener los contenedores, puedes ejecutar:

   ```bash
   docker stop nginx1 nginx2
   ```

2. Y para eliminarlos completamente:

   ```bash
   docker rm nginx1 nginx2
   ```

---

## 9. Resultados esperados

- El contenedor `nginx1` muestra una página personalizada al acceder al puerto 8089.
- El contenedor `nginx2` muestra la página predeterminada de Nginx en el puerto 8090.
- Los archivos fueron correctamente copiados y modificados.
- El estudiante comprendió el uso básico de contenedores, puertos y gestión de archivos HTML dentro de Nginx.

## Imagenes

![Terminal Docker creación de los contenedores](/InformeP2/ImagenDocker1.jpg)

![Terminal Docker Copiar el Index](/InformeP2/ImagenDocker4.jpg)

![Terminal Docker Edicion Primer Index1](/InformeP2/ImagenDocker2.jpg)

![Terminal Docker Copiar el Index2](/InformeP2/ImagenDocker5.jpg)

![Terminal Docker Edición Segundo Index ](/InformeP2/ImagenDocker3.jpg)

![Figura 1-2. Página modificada en nginx1](/InformeP2/InformacionSuda.jpg)

![Figura 1-3. Página por defecto en nginx2](/InformeP2/InformacionPersonal.jpg)

---

## 10. Bibliografía

Docker Inc. (2024). *Docker Documentation*. Recuperado de https://docs.docker.com/

Nginx. (2024). *Nginx Documentation*. Recuperado de https://nginx.org/en/docs/

González, L. (2022). *Guía práctica de servidores web*. Ediciones Alfaomega.

Pérez, R. (2021). *Fundamentos de contenedores y virtualización ligera*. Editorial UteQ.

Torres, M. (2020). *Introducción al uso de Linux en la nube*. Universidad Técnica Nacional.