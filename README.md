# platform-infra-dev

Devcontainer and common configuration for Platform Engineers. This repository provides images, scripts, and settings designed to speed up platform and infrastructure tasks during local development and inside containers.

## Status

WIP — experimental. The repository contains tooling and configuration for development environments and may require adjustments for your local setup.

## Requirements

- macOS (tested on macOS with zsh).
- Docker Engine (recommended v20+).
- Docker Compose (v2, use the `docker compose` command).
- Visual Studio Code (optional) with the "Remote - Containers" / "Dev Containers" extension to open the project inside the container.

## Start the Dev Container (VS Code)

1. Clone the repository:

```bash
git clone git@github.com:IBera/platform-infra-dev.git
cd platform-infra-dev
```

2. Open the project in Visual Studio Code and use "Reopen in Container":

- Open VS Code in the repository folder (`code .`).
- Open the Command Palette (`⇧⌘P`) and run `Dev Containers: Reopen in Container` (or `Remote-Containers: Reopen in Container`).

VS Code will build and start the development environment inside the container.

## Repository structure

- `Dockerfile` — base image / devcontainer image.
- `docker-compose.yml` — service definitions and local orchestration.
- `.devcontainer/` — directory for VS Code Dev Container configuration (place `devcontainer.json` here).
- `fonts/` — font collections included in the image.

## Contributing

To contribute, fork the repository, create a branch with a descriptive name, and open a PR. Follow the commit conventions and add tests when applicable. More details and a checklist will be provided in `CONTRIBUTING.md` (to be created).

Recommended flow:

```text
fork -> branch feature/my-change -> commit -> push -> PR
```

## Troubleshooting & common issues

- Docker permissions: if you see permission errors, ensure Docker Desktop is running and that your user has access to the Docker socket.
- Insufficient resources: increase CPU/Memory in Docker Desktop preferences if containers fail to start.
- Logs: use `docker compose logs -f <service>` to follow logs in real time.

## License

This repository does not include a `LICENSE` file by default. Add a `LICENSE` file (e.g. MIT, Apache-2.0) if you want to clarify contribution and usage terms.

---

If you want, I can now:

- Create `CONTRIBUTING.md` with contribution instructions and conventions.
- Add `docs/devcontainer.md` explaining how to extend the devcontainer.
- Create basic `LICENSE` and `CHANGELOG.md` files.

Tell me which of those tasks you'd like me to do next.
