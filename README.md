## How to set up docker to use the ATIS gen 3 cameras:

To use the ATIS3 cameras we need to have *metavision* (previously *Prophesee*) libraries installed. This branch supports the VGA variant via a Docker file that needs to be built.

### Build the docker image

```console
git clone -b v/bionic_3.3.2_ev2 https://github.com/xEnVrE/event-driven-docker
cd event-driven-docker
bash build image
```

```
git clone -b v/bionic_3.3.2_ev2 https://github.com/xEnVrE/atis-gen3-docker
cd atis-gen3-docker
bash build_image
```

### Start the docker container

```console
xhost local:docker
docker run -it --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY --name atis_container --network=host eventdrivenrobotics/atis-gen3:ev2-dev
```

### Run the YARP bridge

The following assumes that a `YARP` server is running.

```console
atis-bridge-sdk
```

To check that event images are available, use the `vFramer`:

```console
vFramer --height 480 --width 640 --iso
yarp connect /atis3/AE:o /vFramer/iso/AE:i fast_tcp
```
