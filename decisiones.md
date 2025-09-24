# TP3 – Introducción a Azure DevOps

## Configuración inicial
El proyecto **TP3-Olivetto-Cervellini** se creó en Azure DevOps con el proceso de trabajo **Agile**.  
La elección se basó en que este modelo permite organizar el trabajo en **épicas, historias de usuario, tareas y bugs**, ofreciendo más trazabilidad que el proceso Basic y mayor flexibilidad que Scrum para un trabajo de este tipo.

## Boards y Sprint
Se armó un **Epic principal: Portal Web de Usuarios**, que se dividió en tres **User Stories**:  
- Registro de usuario.  
- Login de usuario.  
- Edición de perfil.  

Cada historia se descompuso en dos **Tasks** (UI y lógica) y se agregaron dos **Bugs** de ejemplo (problemas en validación de emails y contraseñas).  
Todo se asignó al **Sprint 1**, de dos semanas de duración, lo que permitió tener un backlog ordenado y visible en el Board.

## Repositorio y autenticación
Para el código se creó un **repositorio vacío en Azure Repos**. Al inicio se intentó inicializarlo sin README, pero Azure obligaba a tener al menos un archivo, por lo que se incluyó uno para poder trabajar.  
También fue necesario generar un **Personal Access Token (PAT)**, ya que la autenticación clásica con usuario y contraseña no estaba habilitada.

## Pipelines y branch policies
Se añadió un archivo `azure-pipelines.yml` en la raíz y se configuró un pipeline que se ejecuta automáticamente con cada Pull Request hacia `main`.  
En la rama principal se aplicaron las siguientes políticas:
- No permitir pushes directos (solo vía PR).  
- Al menos un revisor obligatorio.  
- Validación de build requerida antes de aprobar un merge.

En este punto apareció la limitación de que Azure no permitía configurar 0 reviewers. La solución fue habilitar la opción **“Allow requestors to approve their own changes”** para poder auto-aprobar siendo la única integrante.

## Pull Requests realizados
El flujo de trabajo se probó con dos ramas:
1. **feature/initial-site**, donde se subieron los archivos iniciales (`index.html`, `styles.css`, `azure-pipelines.yml`) y se hizo el primer PR hacia `main`.  
2. **feature/add-contact-form**, donde se agregó una nueva sección de contacto al sitio. Este cambio también pasó por PR, validación de build y merge con squash.

De esta forma se comprobaron las políticas de calidad y se mantuvo el historial limpio.

## Integración con GitHub
Se creó un repositorio espejo en GitHub para contar con respaldo y acceso externo.  
Aquí aparecieron algunos inconvenientes:
- Al hacer `git push` a GitHub, surgió el error *“fetch first”*, porque el remoto tenía un commit diferente.  
- Luego, al intentar un `--force-with-lease`, también falló porque no se había hecho un `fetch` previo.  
Las soluciones fueron traer primero el estado de GitHub (`git fetch github`), hacer merge con la rama local y finalmente empujar los cambios.  

Con esto, tanto **Azure** como **GitHub** quedaron sincronizados.

## Conclusiones
El trabajo permitió poner en práctica todos los componentes de Azure DevOps:  
- Boards con Epic, User Stories, Tasks y Bugs.  
- Sprint planificado.  
- Repositorio controlado con branch policies y autenticación con PAT.  
- Pipelines automáticos validados en Pull Requests.  
- Integración con GitHub y resolución de conflictos reales de Git.  

Además de cumplir los requisitos del TP, la experiencia incluyó la resolución de errores comunes (restricciones en pushes, conflictos entre remotos, configuraciones de policies), lo cual aporta valor práctico al aprendizaje.
