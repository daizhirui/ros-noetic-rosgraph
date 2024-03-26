# Script generated with import_catkin_packages.py.
# For more information: https://github.com/bchretien/arch-ros-stacks.
pkgdesc="ROS - rosgraph contains the rosgraph command-line tool, which prints information about the ROS Computation Graph."
url='https://wiki.ros.org/rosgraph'

pkgname='ros-noetic-rosgraph'
pkgver='1.16.0'
arch=('any')
pkgrel=3
license=('BSD')

ros_makedepends=(
	ros-noetic-catkin
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
)

ros_depends=(
)

depends=(
	${ros_depends[@]}
	python-yaml
	python-netifaces
	python-rospkg
)

_commit="845f74602c7464e08ef5ac6fd9e26c97d0fe42c9"
_dir="ros_comm-${_commit}/tools/rosgraph"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros/ros_comm/archive/${_commit}.tar.gz"
        "frame.patch"::"https://github.com/ros/ros_comm/pull/2331.patch")
sha256sums=('382c8681ac2c9546ef3870d365410ec59ac1bc779cc6c0a68304cf595a66023b'
            '91c9a534a82a2889e52a1e0e34cd0b26ed67a484f25cd657235a3c2d5208c037')

prepare() {
  cd "${srcdir}/ros_comm-${_commit}"
  patch -Np1 -i "${srcdir}/frame.patch"
}


build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCATKIN_BUILD_BINARY_PACKAGE=ON \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
		-DPYTHON_EXECUTABLE=/usr/bin/python \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
