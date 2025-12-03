# Dev Container — Uso y personalización

Este documento explica cómo usar y extender el Dev Container incluido en este repo.

## Propósito

El devcontainer facilita un entorno reproducible con herramientas y extensiones recomendadas para Platform Engineers. Está pensado para ser usado desde Visual Studio Code.

## Iniciar el Dev Container (resumen)

1. Copia la plantilla si aún no existe:

```bash
mkdir -p .devcontainer
cp devcontainer.json.back .devcontainer/devcontainer.json
```

2. Abre el repo en VS Code y selecciona: `Dev Containers: Reopen in Container`.

VS Code construirá la imagen (según `Dockerfile`/`devcontainer.json`) y lanzará el contenedor.

## Estructura y puntos clave

- `.devcontainer/devcontainer.json` — configuración principal del contenedor (extensions, settings, forwardPorts, postCreateCommand, features).
- `Dockerfile` — imagen base que puede ser referenciada en `devcontainer.json`.
- `devcontainer.json.back` — plantilla incluida en este repo; copiar a `.devcontainer/` para usarla.

## Personalización común

- Extensiones recomendadas: añade en `devcontainer.json` bajo `extensions` la lista de extensiones que quieras instalar automáticamente (p. ej. `ms-azuretools.vscode-docker`, `ms-vscode-remote.remote-containers`).
- Forwarded ports: usa `forwardPorts` para exponer puertos de servicios del contenedor al host.
- Variables de entorno: `containerEnv` en `devcontainer.json` para valores simples; para secretos preferir variables de entorno en tu entorno local o un gestor de secretos.
- Mounted volumes / workspace: `workspaceFolder` define la carpeta de trabajo dentro del contenedor; `mounts` puede usarse para montar carpetas adicionales.
- `postCreateCommand`: comando que se ejecuta después de crear el contenedor (instalar dependencias, construir artefactos, etc.).

## Personalizar la imagen

- Si necesitas añadir paquetes o herramientas al contenedor, modifica el `Dockerfile` o crea un `Dockerfile` alternativo y referencia su ruta en `devcontainer.json`.
- Para acelerar builds, aprovecha la caché de Docker y ordena instrucciones en el `Dockerfile` poniendo lo que cambia menos arriba.

## Features y herramientas

- Considera usar `features` (Dev Container Features) para instalar componentes comunes (az cli, gh, docker-in-docker features, etc.).
- Añade herramientas CLI que tu equipo use (kubectl, helm, aws/az cli) en el `Dockerfile` o mediante features.

## Atajos útiles (VS Code)

- Reopen in Container: `⇧⌘P` → `Dev Containers: Reopen in Container`.
- Abrir preview markdown: `⌘⇧V` o `⌘K V`.
- Paleta de comandos: `⇧⌘P`.

## Debugging y problemas comunes

- Build lento / falla: revisa la salida en la vista "Dev Containers" y logs del Docker daemon.
- Permisos en macOS: si hay problemas con mounts, verifica `Docker Desktop` y sus ajustes de recursos/archivos compartidos.
- Espacio en disco: limpia imágenes/volúmenes con `docker system prune` si es necesario.

## Buenas prácticas

- Mantén `devcontainer.json` pequeño y predecible; documenta `postCreateCommand` y cualquier dependencia externa.
- No almacenar secretos en `devcontainer.json` ni en el repositorio.
- Versiona cambios relevantes del `Dockerfile` y del `.devcontainer` para que otros desarrolladores reproduzcan el entorno.

---

Si quieres, puedo:

- Añadir una lista de `extensions` sugeridas directamente en el archivo.
- Incluir un ejemplo de `devcontainer.json` comentado.
- Crear un `CONTRIBUTING.md` que enlace a este documento.
