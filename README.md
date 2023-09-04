# Deploy ROS on Multiple Devices
In the domain of robotics, we

## Single Publisher and Single Subscriber
Things to follow
- Both devices are on the same network (either physically or virtually).
- Get the IP address of the publisher (Linux: `ifconfig`, Windows: `ipconfig`)

<p align="center">
  <img src="https://github.com/arghadeep25/ROS_Multiple_Devices/blob/master/resources/ros_two_device.png" width="700">
</p>

Considering the above example, 

IP Address of Publisher: `192.168.0.25`
IP Address of Subscriber: `192.168.0.35`

To ensure that both devices can reach each other, try pinging from both devices. If they can't communicate despite being on the same network, check the firewall settings.

### Publisher
Usually, `roscore` runs on the local host when no IP address is specified. In this scenario, other devices cannot reach the publisher. Since the intention is to run a single `roscore` that other devices can connect to, it is necessary to start it by explicitly specifying the `IP Address` and `Port Number`. To do that,

```
DEVICE_IP="192.168.0.25"
export ROS_MASTER_URI="http://${DEVICE_IP}:11311"
export ROS_IP=${DEVICE_IP}
```

#### Local vs IP Address
`roscore` Lcoal
```
started roslaunch server http://arghadeep:44065/
ROS_MASTER_URI=http://arghadeep:11311/
```


`roscore` IP
```
started roslaunch server http://192.168.0.25:34961/
ROS_MASTER_URI=http://192.168.0.25:11311
```


### Subscriber
As the `roscore` is running on another device that is connected to the same network, we can connect to the `roscore` by using

```
PUBLISHER_IP="192.168.0.25"
export ROS_MASTER_URI="http://${PUBLISHER_IP}:11311"
```

## Single Publisher and Multiple Subscriber


<p align="center">
  <img src="https://github.com/arghadeep25/ROS_Multiple_Devices/blob/master/resources/ros_multiple_device.png" width="700">
</p>

### Publisher
The steps are same for multiple devices

```
DEVICE_IP="192.168.0.25"
export ROS_MASTER_URI="http://${DEVICE_IP}:11311"
export ROS_IP=${DEVICE_IP}
```

### Subscriber

The following command needs to be executed on every device that wishes to connect to the `roscore`.

```
PUBLISHER_IP="192.168.0.25"
export ROS_MASTER_URI="http://${PUBLISHER_IP}:11311"
```

## Sample

To test the functionality, try the following repositories.

[Publisher](https://github.com/arghadeep25/ROS-Bare-Bones/tree/rviz_docker)

[Subscriber]()

#### Note: Don't forget to change the IP address in the `run.sh` scripts