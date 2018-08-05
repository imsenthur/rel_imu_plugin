# cowIMU_plugin

> A sensor plugin for gazebo to compute the orientation, relative angular velocity and relative angular acceleration of a link with respect to its parent frame.

---

### Table of Contents
You're sections headers will be used to reference location of destination.

- [Description](#description)
- [Installation](#installation)
- [References](#references)
- [License](#license)
- [Author Info](#author-info)

---

## Description

cowIMU is a modified imu sensor plugin which can be used to compute orientation, relative angular velocity and relative angular acceleration with respect to its parent frame. Since the native imu plugin provided with gazebo_ros_pkgs ignores the <frame> tag (which is used to mention the reference frame) and a way to add relative links and reference frames is still being worked upon [https://bitbucket.org/osrf/gazebo/issues/1982/parse-sdf-frame-elements-and-attributes%3C/p%3E], it becomes relatively hard to compute the pose of a link. TF library can still be used to compute the relative pose of the link by transforming the world frame to reference frame but its still a lot of hassle.

[Back To The Top](#cowIMU_plugin)

---

## Installation

#### Clone:
Start with cloning the cowIMU_plugin repository in your workspace,

```html
    git clone https://github.com/imsenthur/cowIMU_plugin
```

#### Build:
The package has to be built inorder to generate ".so" files which can be pointed to in the sdf/urdf of your model.
```html
	cd cowIMU_plugin/
	mkdir build
	cd build/
	cmake ../
	make
```
If things compile well without errors, you should see a "libcow_imu.so" file in,
```html
	~/cowIMU_plugin/build/devel/lib
```

#### Source:
Gazebo looks out for plugins in few default directories so inorder to load our plugin we'll have to add the plugin's path to "/.bashrc",
```html
	subl ~/.bashrc
```
and add these lines to the bottom of your /.bashrc script,
```html
	export LD_LIBRARY_PATH=~/cowIMU_plugin/build/devel/lib:$LD_LIBRARY_PATH
	export GAZEBO_PLUGIN_PATH=~/cowIMU_plugin/build/devel/lib:$GAZEBO_PLUGIN_PATH
```
now source your /.bashrc,
```html
	source ~/.bashrc
```

#### Implement:
You're now good to go, add these lines in sdf/urdf of your model to access the cowIMU plugin,
```html
  <gazebo>
    <plugin filename="libcow_imu.so" name="imu_plugin">
      <topicName>sensors/imu</topicName>
      <serviceName>sensors/imu</serviceName>
      <bodyName>link_</bodyName>
      <updateRateHZ>200.0</updateRateHZ>
      <gaussianNoise>0.0</gaussianNoise>
      <xyzOffset>0 0 0</xyzOffset>
      <rpyOffset>0 0 0</rpyOffset>
      <frameName>link_</frameName>
    </plugin>
  </gazebo>
```
[Back To The Top](#cowIMU_plugin)

---

## References
 - http://gazebosim.org/tutorials?tut=ros_gzplugins
 - http://wiki.ros.org/gazebo_plugins
 
[Back To The Top](#cowIMU_plugin)

---

## License

BSD, Apache 2.0 License

---

## Author Info

- Senthur Raj 
- Btech - Production Engineering,
- National Institute of Technology, Tiruchirappalli.

[Back To The Top](#cowIMU_plugin)