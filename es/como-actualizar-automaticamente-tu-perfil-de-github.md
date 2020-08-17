# Cómo actualizar automáticamente tu perfil de GitHub

Después de  más de 5 años utilizando *GitLab* como servidor de control de versiones, viene *Microsoft* a comprar *GitHub* y a hacer que tome la delantera.

No te engañes, si me estoy cambiando a *GitHub* se debe a que puedo utilizar el repositorio como web de desarrollador.

Y todo gracias a que puedo crear un repositorio con mi nombre de usuario y utilizar el *README* de dicho repo como perfil.

Si le unes las *GitHub Actions*, te encuentras con una bonita página de inicio que se actualiza sola.

> Si ya conoces alguna de las secciones, sáltatela sin problemas. Trato de aportar valor y eso lo decides tú como lector.

!Al lío!

## README de usuario

En agosto de 2020, mi *TL* de *Twitter* se inundó con ejemplos del nuevo `README.md` que, creado en un **repo público** con tu nombre de usuario, servía como perfil personalizado para tu cuenta de *GitHub*.

Para crear este repo (si aún no lo tienes) basta con que entres en [GitHub.com/New](https://github.com/new) o en el acortado [GitHub.New](https://github.new) y rellenar el nombre de repo con tu nombre de usuario.

¿Fácil, no?

Si te fijas en la imagen de abajo, verás que te aparece un mensaje bastante majo del equipo de GitHub.

![Creando nuestro repo de usuario](https://github.com/borjalofe/til/raw/master/images/creating-special-github-user-repo.png)

El archivo `README.md` se inicializa con una pequeña lista de ítems sugeridos... pero aún no he visto que nadie lo haya usado tal cual.

```markdown
**borjalofe/borjalofe** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
```

Puedes personalizarlo como quieras utilizando *MarkDown* o *HTML*.

Además, en el caso de *HTML*, admite *CSS inline*, así que puedes llegar a personalizarlo bastante.

En mi caso, prefiero usar *MarkDown* para centrarme en el contenido.

También porque prefiero dedicar mi tiempo a otras cosas... lo que me lleva a...

## Actualizar el README de usuario automáticamente

Si has leído el título de esta sección y te has echado a temblar, respira: no necesitas saber programar para actualizar tu perfil de manera automática.

A la hora de escribir este artículo, no quise complicarme mucho y busqué algunos ejemplos en el propio *GitHub*.

Al final, me decidí por los siguientes:

1. [*Blog Post Workflow* de *Gautam Krishna R*](https://github.com/gautamkrishnar/blog-post-workflow)
<!-- 1. [*GitHub Activity in Readme* de *James George*](https://github.com/jamesgeorge007/github-activity-readme) -->

Por el momento, aún no he creado una *GitHub Action* propia para actualizar mi `README.md`, aunque tengo varias ideas en mente y no tardaré mucho en publicar algún artículo al respecto.

### Mostrar los artículos de un blog

Un buen perfil debería (*EMHO*) mostrar una vista de pájaro de tu estado actual.

Por eso, he querido mostrar los últimos artículos de mi blog como desarrollador.

Para ello, solo necesitamos:

1. Crear la carpeta `.github`
1. Crear la carpeta `workflows` dentro de la anterior
1. Crear el archivo de configuración en *YaML* (en mi caso, lo he llamado con el original nombre `update_readme.yml`)
1. Copiar el siguiente código

```markdown
name: Update README

on:
  schedule:
    - cron: '*/30 * * * *'
  workflow_dispatch:

jobs:
  update-readme-with-posts-from-community-blog:
    name: Update this repo's README with latest blog posts on borjalofe.com
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: gautamkrishnar/blog-post-workflow@master
        with:
          feed_list: "https://borjalofe.com"
```

Básicamente, estoy diciendo que la *GitHub Action*:

- Se llama *"Update README"*
- Debe ejecutarse cada media hora (`cron: '*/30 * * * *'`) y bajo demanda (`workflow_dispatch:`).
- Usa dos acciones de otros usuarios:
  1. `Checkout` de *actions* (que permite acceder al `README.md` que queremos actualizar)
  1. `Blog Post Workflow` de *Gautam Krishna R* (que lee los X últimos artículos del *RSS* de tu blog para publicarlos en el `README.md` como enlaces a los mismos, usando el título como texto de enlace)

En la imagen de abajo, te enseño dónde aparece el botón para ejecutar la *GitHub Action* bajo demanda desde la sección *Actions*.

![Botón para ejecutar bajo demanda la acción de actualización](https://github.com/borjalofe/til/raw/master/images/execute-update-user-readme-action.png)

Puedes descubrir otras maneras de configurar esta acción en el [repo de la misma](https://github.com/gautamkrishnar/blog-post-workflow).

| Creado el | Actualizado el |
| :-------: | :------------: |
| 17 de agosto de 2020 | 17 de agosto de 2020 |
