# rich base image
FROM osrf/ros:noetic-desktop-full
# update and upgrade base image to patch vulnerabilities
RUN apt-get update && apt-get upgrade -y && rm -rf /var/lib/apt/lists/*
# install catkin tools first
RUN apt update && apt install -y \
    python3-catkin-tools \ 
    bash-completion htop
# copy project to container temporarily for installing dependencies
COPY src /home/src
RUN /bin/bash -c "source /opt/ros/noetic/setup.bash" \ 
    && apt update && apt upgrade\
    && apt install -y psmisc clang-11 \
    && apt install -y ros-noetic-teb-* \
    && apt install -y ros-noetic-tf2* \
    && apt install -y ros-noetic-joint* \
    && apt install -y ros-noetic-gazebo* \
    && apt install -y ros-noetic-ros-control* \
    && apt install -y ros-noetic-oct* \
    && rm -rf /var/lib/apt/lists/*
# set entrypoint including process of sourcing ros environment
COPY docker/ros_entrypoint.sh /
RUN chmod +x /ros_entrypoint.sh
ENTRYPOINT ["/ros_entrypoint.sh"]

# set default command
CMD ["/bin/bash"]
