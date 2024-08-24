# Markus Buchholz

ARG ROS_DISTRO=humble
FROM ros:$ROS_DISTRO

ARG DEBIAN_FRONTEND=noninteractive
ARG MUJOCO_VERSION=3.2.2  
ARG BRANCH=humble-devel

RUN apt-get update && apt-get upgrade -y

RUN apt-get update \
  && apt-get -y --quiet --no-install-recommends install \
    bash-completion \
    build-essential \
    git \
    glmark2 \
    gnupg \
    iputils-ping \
    lsb-release \
    plocate \
    software-properties-common \
    sudo \
    wget \
    vim \
    nano \
    libxkbcommon-x11-0 \
    xvfb \
    libncurses5-dev \
    libncursesw5-dev \
    cmake \
    libzmq3-dev \
    libdw-dev \
    qtbase5-dev \
    libqt5svg5-dev \
    libpcl-dev \
    python3-pip \
    libglfw3-dev \
  && rm -rf /var/lib/apt/lists/*

RUN pip3 install xacro

# Install NVIDIA software
RUN apt-get update \
 && apt-get -y --quiet --no-install-recommends install \
    libglvnd0 \
    libgl1 \
    libglx0 \
    libegl1 \
    libxext6 \
    libx11-6 \
  && rm -rf /var/lib/apt/lists/*

ENV NVIDIA_VISIBLE_DEVICES=all
ENV NVIDIA_DRIVER_CAPABILITIES=graphics,utility,compute
ENV QT_X11_NO_MITSHM=1

RUN apt update \
 && apt install -y --no-install-recommends \
    ros-${ROS_DISTRO}-plotjuggler-ros \
 && apt clean

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install FUSE
RUN apt-get update \
  && apt-get -y --quiet --no-install-recommends install \
    fuse \
  && rm -rf /var/lib/apt/lists/*

RUN apt update \
  && apt install -y --no-install-recommends \
    ros-${ROS_DISTRO}-control-toolbox \
    ros-${ROS_DISTRO}-controller-interface \
    ros-${ROS_DISTRO}-controller-manager \
    ros-${ROS_DISTRO}-joint-state-publisher \
    ros-${ROS_DISTRO}-joint-trajectory-controller \
    ros-${ROS_DISTRO}-position-controllers \
    ros-${ROS_DISTRO}-effort-controllers \
    ros-${ROS_DISTRO}-velocity-controllers \
    ros-${ROS_DISTRO}-ros2-control \
    ros-${ROS_DISTRO}-ros2-controllers \
  && apt clean

# Install Mujoco
ENV MUJOCO_VERSION=$MUJOCO_VERSION
RUN wget https://github.com/google-deepmind/mujoco/releases/download/$MUJOCO_VERSION/mujoco-$MUJOCO_VERSION-linux-x86_64.tar.gz \
  && mkdir -p /home/mujoco \
  && tar -xzf mujoco-$MUJOCO_VERSION-linux-x86_64.tar.gz -C /home/mujoco \
  && rm mujoco-$MUJOCO_VERSION-linux-x86_64.tar.gz

# Set Mujoco environment variable
RUN echo "export MUJOCO_DIR=/home/mujoco/mujoco-$MUJOCO_VERSION" >> ~/.bashrc
ENV MUJOCO_DIR=/home/mujoco/mujoco-$MUJOCO_VERSION
ENV LD_LIBRARY_PATH="$MUJOCO_DIR/bin:${LD_LIBRARY_PATH}"

WORKDIR /home/ros2_ws

# Clone mujoco_ros2_control repository
RUN mkdir -p /home/ros2_ws/src && cd /home/ros2_ws/src \
  && git clone -b $BRANCH https://github.com/sangteak601/mujoco_ros2_control.git

RUN rosdep fix-permissions && rosdep update && \
    rosdep install --from-paths /home/ros2_ws/src --ignore-src -y

RUN /bin/bash -c "source /opt/ros/$ROS_DISTRO/setup.bash && colcon build"

# Install rqt and all relevant plugins
RUN apt update && apt install -y --no-install-recommends \
    ros-${ROS_DISTRO}-rqt \
    ros-${ROS_DISTRO}-rqt-common-plugins \
    ros-${ROS_DISTRO}-rqt-graph \
    ros-${ROS_DISTRO}-rqt-tf-tree \
    ros-${ROS_DISTRO}-rqt-runtime-monitor \
    ros-${ROS_DISTRO}-rqt-reconfigure \
    ros-${ROS_DISTRO}-rqt-controller-manager \
    ros-${ROS_DISTRO}-rqt-joint-trajectory-controller \
    ros-${ROS_DISTRO}-rqt-image-view \
    ros-${ROS_DISTRO}-rqt-plot \
  && apt clean && rm -rf /var/lib/apt/lists/*


WORKDIR /home/ros2_ws

# Entry point
CMD ["/bin/bash"]
