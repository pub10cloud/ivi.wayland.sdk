# IVI Wayland SDK in Docker

## Preconditions

- Ubuntu 18.04 LTS

- Use the dockerhub image that was pre-builded.
  - https://hub.docker.com/r/pub10cloud/ivi.wayland.sdk

- Install docker and docker compose, and add non-root docker user. 
  - https://docs.docker.com/engine/install/ubuntu/
  - https://docs.docker.com/compose/install/
  - https://docs.docker.com/engine/install/linux-postinstall/

- Add New "user" that have UID=9001 and GID=9001.
~~~
sudo groupadd --gid 9001 user
sudo useradd --create-home --uid 9001 --gid 9001 --group sudo,docker --shell /bin/bash user
sudo sh -c "echo user:user | chpasswd"
~~~

- Launch ubuntu desktop, then execute the below command to use x11 in docker.

~~~
$ xhost +
~~~


## How to use

- get this repository
~~~
$ cd ${WORK}
$ git clone https://github.com/HidetoKimura/ivi.wayland.sdk.git
$ cd ivi.wayland.sdk
~~~

- start container
~~~
$ . setenv.sh
$ docker-compose up -d
~~~

- enter/re-enter container
~~~
$ docker-compose exec app /bin/bash

id:user, pass:user
~~~

- stop container
~~~
$ docker-compose down
~~~

# In Docker
~~~
$ flutter_init.sh
~~~

# sample run test
~~~
$ cd work
$ git clone https://github.com/google/flutter-desktop-embedding.git
$ cd flutter-desktop-embedding/testbed
$ flutter run
~~~

# build & exec test 
~~~
$ flutter build linux
$ cd build/linux/debug/bundle/
$ ./testbed
~~~

# weston & flutter wayland
- see flutter_wayland
  - https://github.com/HidetoKimura/flutter_wayland
~~~
$ weston --width 800 --height 600 &
$ layer-add-surfaces 1000 10 &
$ ./flutter_wayland ../external/asset_bundle/testbed
~~~

