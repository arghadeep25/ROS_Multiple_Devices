# Deploy ROS on Multiple Devices
The idea is to 

## Single Publisher and Single Subscriber
Things to follow
- Both devices are on the same network (either physically or virtually).
- Get the IP address of the publisher (Linux: `ifconfig`, Windows: `ipconfig`)

<p align="center">
  <img src="https://github.com/arghadeep25/ROS_Multiple_Devices/blob/master/resources/ros_two_device.png" width="600">
</p>

Considering the above example, 

IP Address of Publisher: `192.168.0.25`
IP Address of Subscriber: `192.168.0.35`

To ensure, both devices can reach each other, try to ping from both the devices. If they can't reach each other even though both are connected on the same network, check the `Firewall` settings.

### Publisher
Usually the `roscore` runs on local host when no IP address is specified. In that case, no other devices can reach to the publisher. As the idea is to run a single `roscore`, so that other device can run on that, we need to run it by explicitly mentioning the IP Address and the Port Number. To do that,

```
DEVICE_IP="192.168.0.25"
export ROS_MASTER_URI="http://${DEVICE_IP}:11311"
export ROS_IP=${DEVICE_IP}
```

### Subscriber
As the `roscore` is running on another device which is connected on the same network, we can connect to the 'roscore' by using

```
PUBLISHER_IP="192.168.178.42"
export ROS_MASTER_URI="http://${PUBLISHER_IP}:11311"
```


## Single Publisher and Multiple Subscriber