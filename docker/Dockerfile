FROM osrf/ros:noetic-desktop-full

# Change to bash
SHELL ["/bin/bash", "-c"] 

# Minimal setup
RUN apt-get update \
    && apt-get install -y  apt-utils \
    locales \
    lsb-release
ARG DEBIAN_FRONTEND=noninteractive
RUN dpkg-reconfigure locales

# Install ROS dependencies
RUN apt-get install -y git \
    ros-noetic-joy \
    ros-noetic-teleop-twist-joy \
    ros-noetic-teleop-twist-keyboard \
    ros-noetic-amcl \
    ros-noetic-map-server \
    ros-noetic-move-base \
    ros-noetic-urdf \
    ros-noetic-xacro \
    ros-noetic-rqt-image-view \
    ros-noetic-gmapping \
    ros-noetic-navigation \
    ros-noetic-joint-state-publisher \
    ros-noetic-robot-state-publisher \
    ros-noetic-slam-gmapping \
    ros-noetic-dwa-local-planner \
    ros-noetic-joint-state-publisher-gui

# Clone the tortoise repo
RUN mkdir -p /root/catkin_ws/src 
COPY ./tortoisebot/tortoisebot_gazebo/ /root/catkin_ws/src/tortoisebot_gazebo
RUN true
COPY ./tortoisebot/tortoisebot_description/ /root/catkin_ws/src/tortoisebot_description
RUN true
COPY ./tortoisebot/tortoisebot_slam/ /root/catkin_ws/src/tortoisebot_slam
RUN true
COPY ./tortoisebot/tortoisebot_description/ /root/catkin_ws/src/tortoisebot_description
RUN true
COPY ./tortoisebot/tortoisebot_waypoints/ /root/catkin_ws/src/tortoisebot_waypoints

# Link python3 to python otherwise ROS scripts fail when using the OSRF contianer
RUN ln -s /usr/bin/python3 /usr/bin/python

# Navigate to the catkin workspace
WORKDIR /root/catkin_ws

RUN source /opt/ros/noetic/setup.bash \
    && catkin_make \
    && chmod -R +x * 

RUN echo source /opt/ros/noetic/setup.bash >> /root/.bashrc
RUN echo source /root/catkin_ws/devel/setup.bash >> /root/.bashrc

# Clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /root/.cache\
    && apt-get clean && apt autoclean