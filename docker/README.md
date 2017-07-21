# Self Docker builders

## Build container image

### Preconditions

 * (optional) Write `naoqi-sdk-2.1.4.13-linux64.zip` (or other packages) to `packages/` in order to skip package download during container build

### Steps

Choose the appropriate Dockerfile for your architecture (we're using `amd64` in the example below) and build **from the project's root directory**:

    docker build -t build-intu -f ./docker/Dockerfile-linux-amd64.bld .

Start the container and compile self:

    docker run --name build-intu -it build-intu /self/scripts/build_linux.sh

The build artifacts are in the (stopped) container named `build-intu`. You can copy the built artifacts from that container to the host machine:

    docker cp build-intu:/self/lib .
    docker cp build-intu:/self/bin .

When you're finished with the build container you can remove it with the command:

    docker rm build-intu

If you don't want to reuse it, you can remove the container __image__ with the command:

    docker rmi build-intu
