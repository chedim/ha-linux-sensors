# ha-linux-sensors

A go program that reads sensor data from Linux machines devtree files and sends it to MQTT topics.

### Usage

Clone and build it with `go build` or install it from this repository using `go install github.com/cheddim/ha-linux-sensors`

```
$ ./ha-linux-sensors -h
Usage of ./ha-linux-sensors:
  -interval int
    	Scan interval (for example: 10s)
  -mqttBroker string
    	URI of the MQTT broker, eg. tcp://broker.hivemq.com:1883
  -mqttPassword string
    	Password for the mqtt connection
  -mqttUser string
    	Username for the mqtt connection
```

All of these arguments can be then followed by a list of files to monitor on linux devtree. Values from each file will be posted onto topic `ha-linux-sensors/<HOSTNAME>/<FILENAME>`.

Example of a full command line:

```bash
ha-linux-sensors --interval 10s --mqttBroker 127.0.0.1:1883 /sys/bus/iio/devices/iio:device0/in_accel_scale /sys/bus/iio/devices/iio:device0/in_accel_x_raw /sys/bus/iio/devices/iio:device0/in_accel_y_raw /sys/bus/iio/devices/iio:device0/in_accel_z_raw /sys/bus/iio/devices/iio:device1/in_anglvel_x_raw /sys/bus/iio/devices/iio:device1/in_anglvel_y_raw /sys/bus/iio/devices/iio:device1/in_anglvel_z_raw /sys/bus/iio/devices/iio:device2/in_illuminance_raw
```

At the Home Assistant side, you probably want to create a [MQTT sensor](https://www.home-assistant.io/integrations/binary_sensor.mqtt/).
