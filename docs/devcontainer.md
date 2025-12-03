# Dev Container — Usage and customization

This document explains how to use and extend the Dev Container included in this repository.

## Purpose

The devcontainer provides a reproducible environment with recommended tools and extensions for Platform Engineers. It is intended to be used from Visual Studio Code.

## Start the Dev Container (summary)

1. Ensure a `.devcontainer/devcontainer.json` exists in the repository. Create or customize it as needed:

```bash
mkdir -p .devcontainer
# create .devcontainer/devcontainer.json or add your own content
```

2. Open the repo in VS Code and select: `Dev Containers: Reopen in Container`.

VS Code will build the image (according to `Dockerfile`/`devcontainer.json`) and start the container.

## Structure and key files

- `.devcontainer/devcontainer.json` — main container configuration (extensions, settings, forwardPorts, postCreateCommand, features).
- `Dockerfile` — base image referenced by `devcontainer.json`.
- `.devcontainer/devcontainer.json` — recommended location for the Dev Container configuration file.

## Common customization

- Recommended extensions: add under `extensions` in `devcontainer.json` the list of extensions to install automatically (e.g. `ms-azuretools.vscode-docker`, `ms-vscode-remote.remote-containers`).
- Forwarded ports: use `forwardPorts` to expose container service ports to the host.
- Environment variables: use `containerEnv` in `devcontainer.json` for simple values; for secrets prefer local environment variables or a secrets manager.
- Mounted volumes / workspace: `workspaceFolder` sets the working directory inside the container; use `mounts` to add extra mounts when needed.
- `postCreateCommand`: command executed after creating the container (install dependencies, build artifacts, etc.).

## Customize the image

- If you need to add packages or tools to the container, modify the `Dockerfile` or create an alternate `Dockerfile` and reference its path in `devcontainer.json`.
- To speed up builds, leverage Docker cache and order the `Dockerfile` instructions so that less frequently changing steps come later.

## Features and tools

- Consider using Dev Container `features` to install common components (az cli, gh, docker-in-docker, etc.).
- Add CLI tools your team uses (kubectl, helm, aws/az cli) in the `Dockerfile` or via features.

## Useful shortcuts (VS Code)

- Reopen in Container: `⇧⌘P` → `Dev Containers: Reopen in Container`.
- Open Markdown preview: `⌘⇧V` or `⌘K V`.
- Command Palette: `⇧⌘P`.

## Debugging and common issues

- Slow / failing build: check the "Dev Containers" output and the Docker daemon logs.
- macOS permissions: if mounts fail, check Docker Desktop and its resources/file sharing settings.
- Disk space: free images/volumes with `docker system prune` if necessary.

## Best practices

- Keep `devcontainer.json` small and predictable; document `postCreateCommand` and any external dependencies.
- Do not store secrets in `devcontainer.json` or the repository.
- Version changes to the `Dockerfile` and `.devcontainer` so others can reproduce the environment.

---

If you want, I can:

- Add a list of suggested `extensions` directly to this file.
- Include a commented example `devcontainer.json`.
- Create a `CONTRIBUTING.md` that links to this document.
