# desktop-action

Github Action to start Docker Desktop.

This github action is [experimental](https://docs.docker.com/release-lifecycle/#experimental).
It currently supports starting Docker Desktop on "mac" nodes in Github Actions.

Note that the usage of Docker Desktop is subject to [Docker Desktop license agreement](https://docs.docker.com/subscription/desktop-license/).

In your gihub action workflow, you can add a step:

```
  steps:
      - id: start_desktop
        uses: docker/desktop-action/start@v0.0.1
```

After this step executes, Docker Desktop is ready and available, the docker CLI can be executed in subsequent "run" steps
