# rich base image
FROM osrf/ros:noetic-desktop-full

# install catkin tools first
RUN apt update && apt install -y \
    python3-catkin-tools \ 
    bash-completion htop

ENV DEBIAN_FRONTEND=noninteractive
# copy project to container temporarily for installing dependencies
COPY src /home/src
RUN /bin/bash -c "source /opt/ros/noetic/setup.bash" \ 
    && apt-get update -y && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends libfprint-2-2 \
    && apt-get install -y ros-noetic-ros-control* \
    && apt-get install -y ros-noetic-robot-state-publisher \
    && apt-get install -y ros-noetic-robot-localization \
    && apt-get install -y ros-noetic-grid-* \
    && apt-get install -y psmisc \
    && apt-get install -y clang-11 \
    && apt-get install -y ros-noetic-gazebo* \
    && apt-get install -y ros-noetic-jsk-* \
    && apt-get install -y ros-noetic-teb-* \
    && apt-get install -y ros-noetic-amcl* \
    && apt-get install -y ros-noetic-move-* \ 
# set entrypoint including process of sourcing ros environment
COPY launch /home/launch
COPY config /home/config
COPY scripts /home/scripts
COPY data /home/data
COPY Makefile /home/Makefile
COPY docker/ros_entrypoint.sh /
RUN chmod +x /ros_entrypoint.sh
ENTRYPOINT ["/ros_entrypoint.sh"]

# set default command
CMD ["/bin/bash"]
