# `mqtt-bridge`

This is an Ansible role to configure a simple MQTT bridge. I created this because Tasmota does not support MQTTS in their default firkware. My solution is this bridge, which uses unencrypted connections only in the local network, and bridges everything in and out to via MQTTS to a properly secured broker.

# Variables

The role uses the following variables to configure Mosquitto bridges:

```yaml
mqtt_bridges:
- name: idIOT
  address: mqtt.example.com
  port: 8883
  user: idiot
  password: supersigrid
  topics:
  - "# both 0"
```

This configuration will create a local broker with a bridge to `mqtt.example.com:8883`. Each and every message to and from `mqtt.example.com:8883` will be replicated locally.

* The `user` and `password` must be valid at `mqtt.example.com:8883`
* `name` is the client ID used at `mqtt.example.com:8883`
* `topics` is a list of topic patterns as specified in [`mosquitto.conf`](https://mosquitto.org/man/mosquitto-conf-5.html).

Users that are local to the broker can be added like this:

```yaml
mosquitto_users:
- name: alice
  password: s3cret
- name: bob
  password: geh3im
```
