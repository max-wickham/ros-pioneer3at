# Setup

- First install docker

- Command to create a docker container for Noetic named "hcr", this container should have access to your home directory and use the same user as your normal linux install (will probably need WSL2 on windows to work)

```
sudo docker run -it \
                      --user=$(id -u $USER):$(id -g $USER) \
                      --env="DISPLAY" \
                      --workdir="/home/$USER" \
                      --volume="/home/$USER:/home/$USER" \
                      --volume="/etc/group:/etc/group:ro" \
                      --volume="/etc/passwd:/etc/passwd:ro" \
                      --volume="/etc/shadow:/etc/shadow:ro" \
                      --volume="/etc/sudoers.d:/etc/sudoers.d:ro" \
                      --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
                      --name hcr \
                      ros:noetic
```

- To stop the container run
```
sudo docker stop hcr
```

- To start the container run
```
sudo docker start -i hcr
```

- To install dependencies
```
sudo apt-get update
sudo apt-get install ros-noetic-desktop-full
```

- To create an additional terminal to access the container run (maybe make an alias for this in your bashrc to save typing it each time)
```
sudo docker exec -it hcr bash
```


- It might also be a good idea to add the following to your bashrc as it needs to be run every time a terminal to the container is opened (unfortunately the bashrc used by the container is the same as your normal install, not sure how to change this)
```
source /opt/ros/noetic/setup.bash
```

### PA3T Example

This github has an example on how to use the P3AT, (probably need to follow the ROS catkin environment set up first)
- https://github.com/dawonn/ros-pioneer3at

If you follow the instructions it should work, there's just a few extra lines I had to comment out as some packages didn't seem to be available for me, I've pushed a fork with the changes I made to this repo in case its helpful, you still need to follow the instructions for the UDF files though as that requires doing some stuff that isn't located in the repo.
- https://github.com/max-wickham/ros-pioneer3at
