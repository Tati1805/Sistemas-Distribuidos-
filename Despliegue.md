> # Despliegue de la aplicación Pokedex en Azure App Service

Dirección URL : [Pokedex-tmp 🌐](https://ashy-plant-069343d10.6.azurestaticapps.net)
Repositorio : [Mi repositorio GitHub 🔄](https://github.com/Tati1805/pokedex)
## 🧭Requisitos previos

- Cuenta activa en GitHub (con código fuente)
- Código fuente de la aplicación subido a un repositorio llamado `pokedex`
- Cuenta de Azure for Students habilitada (paso anterior)

##  📚Creación del recurso en Azure

1. Inicié sesión en el portal de Azure: [Acceso  Azure](https://portal.azure.com)
2. Creé un nuevo grupo de recursos llamado `pokedex` para organizar los servicios.
3. Fui a **"Create a resource"** y seleccioné **"Static Web App".**
4. Llené el formulario de creación con los siguientes datos:
   -  **Grupo de recursos:** pokedex
   - **Nombre:** pokedex-tmp
   - **Tipo de plan:** Gratis
   - **Origen :** GitHub
   - **Organización:** Tati1805
   - **Repositorio :** pokedex
   - **Rama:** master
   -  **Valores preestablecidos de compilación:** Angular (detectado)
   - **Ubicación de la aplicación** :  ./sistemas-distribuidos/poke-dex-lab/source/pokedex-angular
   -  **Ubicación de salida** : dist/pokedex-angular

5. Hice clic en **"Revisar y Crear"**  y luego en **"Crear"**, esperamos unos segundos y nuestra aplicación web estará desplegada .

![.](https://scontent.fctg3-1.fna.fbcdn.net/v/t39.30808-6/493227675_10161894319168717_1267195134453518012_n.jpg?stp=dst-jpg_s960x960_tt6&_nc_cat=106&ccb=1-7&_nc_sid=127cfc&_nc_eui2=AeGgc0gHZDjXRlZWmpIYU7zo2ea9ngMIhPHZ5r2eAwiE8eGF97HTHkc9EfK4fcZDo7Y&_nc_ohc=lEEH6R5tzgYQ7kNvwH5EWj3&_nc_oc=AdmJ62kCgmV3RBEreGbmNYhAC8Wa-1di0Hz8DiQG59oRhbdsR2anzy-Nw0zA9FI1sf0&_nc_zt=23&_nc_ht=scontent.fctg3-1.fna&_nc_gid=dm9doJqDhDkVjvN81ib9fA&oh=00_AfF36CC7-sMXmWuq5H3G5u5IYnGzT3OAyYUF-fj_z0BjAQ&oe=6810CB70)

##  🔧Ajustes realizados

Durante el despliegue de la aplicación en Azure, se identifico que las imágenes de la pagina principal, no se mostraban de manera correcta.

Se modificó el archivo de configuración de entornos ubicado en:
> src/environments/environment.prod.ts]

Dentro de este archivo, se actualizó la propiedad correspondiente a la ruta de las imágenes de la siguiente forma:

>ImágenesPath: '/assets/images'

Tras realizar esta  las imágenes se interpretaron correctamente cuando la aplicación es servida desde la raíz en un entorno de producción como Azure App Service.


##  🔐Seguridad: encabezados HTTP

Para mejorar la seguridad y cumplir con los requisitos del caso de estudio, agregué un archivo `web.config` en la raíz del proyecto con los siguientes encabezados HTTP:

- Content-Security-Policy
- Strict-Transport-Security
- X-Frame-Options
- X-Content-Type-Options
- Referrer-Policy
- Permissions-Policy

Este archivo fue interpretado por el servidor IIS de Azure y aplicado correctamente a las respuestas HTTP de la aplicación.

## ✅Verificación

- El despliegue se completó sin errores.
- La aplicación es accesible desde la URL pública generada por Azure.
- Se realizó una prueba en https://securityheaders.com y se obtuvo una calificación de: **A**
![](https://scontent.fctg3-1.fna.fbcdn.net/v/t39.30808-6/489927290_10161894308798717_2565545292471845832_n.jpg?_nc_cat=104&ccb=1-7&_nc_sid=127cfc&_nc_eui2=AeFHq5NZMV5o-0j22F1cD5hXt5ZNfLi8G3O3lk18uLwbcwyJ-I7Lurwh52Wnn5GcsmY&_nc_ohc=PKNEM5fuBAYQ7kNvwEWNNv_&_nc_oc=AdlM0_aS7u2EtN67jEPTZUb_eXTfzFuq3AF3T5ZZ2GXhVLPpVe6cc-frm7RBnGEyNBk&_nc_zt=23&_nc_ht=scontent.fctg3-1.fna&_nc_gid=94UREKK1JspOhXKtD8eIoQ&oh=00_AfEY1nTgW5TJDa5EpG5aeWT94gA0sOYW3dNIyGRf3X19ow&oe=6810C229)

## 📊Conclusión

El proceso de despliegue en Azure fue exitoso. Se aplicaron medidas de seguridad recomendadas para proteger la aplicación y mejorar la calificación de seguridad.

