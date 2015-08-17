
pkgdesc="ROS - rosruby_messages is precompiled rosruby messages."
url='http://www.ros.org/'

pkgname='ros-hydro-rosruby-messages'
pkgver='0.1.3'
_pkgver_patch=0
arch=('i686' 'x86_64')
pkgrel=10
license=('BSD')

ros_makedepends=(ros-hydro-kingfisher-msgs
  ros-hydro-pcl-msgs
  ros-hydro-controller-manager-msgs
  ros-hydro-rosruby
  ros-hydro-pr2-mechanism-msgs
  ros-hydro-sensor-msgs
  ros-hydro-pr2-controllers-msgs
  ros-hydro-move-base-msgs
  ros-hydro-turtlebot-msgs
  ros-hydro-rosgraph-msgs
  ros-hydro-sr-ronex-msgs
  ros-hydro-household-objects-database-msgs
  ros-hydro-visualization-msgs
  ros-hydro-stereo-msgs
  ros-hydro-gazebo-msgs
  ros-hydro-smach-msgs
  ros-hydro-rosunit
  ros-hydro-pr2-msgs
  ros-hydro-shape-msgs
  ros-hydro-map-msgs
  ros-hydro-multimaster-msgs-fkie
  ros-hydro-moveit-msgs
  ros-hydro-concert-msgs
  ros-hydro-rosruby-actionlib
  ros-hydro-geometry-msgs
  ros-hydro-manipulation-msgs
  ros-hydro-control-msgs
  ros-hydro-nav-msgs
  ros-hydro-actionlib-msgs
  ros-hydro-nmea-msgs
  ros-hydro-std-msgs
  ros-hydro-uuid-msgs
  ros-hydro-audio-common-msgs
  ros-hydro-dynamixel-msgs
  ros-hydro-rosserial-msgs
  ros-hydro-ackermann-msgs
  ros-hydro-cob-srvs
  ros-hydro-arbotix-msgs
  ros-hydro-tf2-msgs
  ros-hydro-std-srvs
  ros-hydro-yocs-msgs
  ros-hydro-genrb
  ros-hydro-hector-nav-msgs
  ros-hydro-velodyne-msgs
  ros-hydro-message-generation
  ros-hydro-kobuki-msgs
  ros-hydro-hector-worldmodel-msgs
  ros-hydro-object-recognition-msgs
  ros-hydro-geographic-msgs
  ros-hydro-octomap-msgs
  ros-hydro-trajectory-msgs
  ros-hydro-underwater-sensor-msgs
  ros-hydro-zeroconf-msgs
  ros-hydro-gateway-msgs
  ros-hydro-catkin
  ros-hydro-calibration-msgs
  ros-hydro-diagnostic-msgs
  ros-hydro-rocon-app-manager-msgs)
makedepends=('cmake' 'git' 'ros-build-tools'
  ${ros_makedepends[@]})

ros_depends=(ros-hydro-message-runtime
  ros-hydro-rosruby-actionlib
  ros-hydro-rosruby)
depends=(${ros_depends[@]})

_tag=release/hydro/rosruby_messages/${pkgver}-${_pkgver_patch}
_dir=rosruby_messages
source=("${_dir}"::"git+https://github.com/OTL/rosruby_messages-release.git"#tag=${_tag}
        'conflicts.patch')
md5sums=('SKIP'
         'b1b37bb6b8ac0d4c0218712406a36058')

build() {
  # Use ROS environment variables
  /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Apply patch
  msg "Patching source code"
  cd ${srcdir}/${_dir}
  git apply ${srcdir}/conflicts.patch

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
