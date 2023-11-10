# desktop-action

Github Action to start Docker Desktop.

This github action is [experimental](https://docs.docker.com/release-lifecycle/#experimental).
It currently supports starting Docker Desktop on large-runner "linux" nodes in Github Actions.

**Important**: it seems that since mid September 2023, the action inconsistently fails on macOs runner. We have updated the action to use linux runners. However, since virtualisation is required for Docker Desktop to start, you must be sure that the runner as it enabled. Large-runners [have it from February 2023]([url](https://github.blog/changelog/2023-02-23-hardware-accelerated-android-virtualization-on-actions-windows-and-linux-larger-hosted-runners/)).

Note that the usage of Docker Desktop is subject to [Docker Desktop license agreement](https://docs.docker.com/subscription/desktop-license/).

In your GitHub Action workflow, you must use a [GitHub large-runner]([url](https://docs.github.com/en/actions/using-github-hosted-runners/about-larger-runners/about-larger-runners)) with virtualization enabled, and then you can add a step:

```
jobs:
  test-docker-desktop:
    name: Test Docker Desktop installation and start
    runs-on: large-ubuntu
    steps:
      - id: start_desktop
        uses: docker/desktop-action/start@v0.3.0
```

After this step executes, Docker Desktop is ready and available, the docker CLI can be executed in subsequent "run" steps

By default, the action downloads the last version of Docker Desktop. But you can specify another one by providing the build URL from where the action can download the specific version:

```
jobs:
  test-docker-desktop:
    name: Test Docker Desktop installation and start
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ large-ubuntu ] 
        build-url: [ "latest", "https://desktop.docker.com/linux/main/amd64/122432/docker-desktop-4.24.0-amd64.deb" ]

    steps:
      - name: Start Desktop
        uses: ./start
        with:
          docker-desktop-build-url: ${{ matrix.build-url }}
```
