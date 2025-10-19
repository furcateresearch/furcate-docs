# MQTT Integration

## Overview

Connect Furcate to IoT sensors and devices using MQTT protocol.

## Installation

```bash
pip install furcate-bridge
```

## Basic Usage

```python
from adapters.mqtt import MQTTAdapter, create_mqtt_config

config = create_mqtt_config(
    broker='mqtt.example.com',
    port=1883,
    username='device001',
    password='secret'
)

adapter = MQTTAdapter(config)
adapter.connect()

# Subscribe to sensors
def process_data(topic, payload):
    # Run ML inference
    result = model.predict(payload)
    # Publish result
    adapter.write('results/device001', result)

adapter.subscribe('sensors/#', process_data)
```

## TLS/SSL

```python
config = create_mqtt_config(
    broker='secure.mqtt.example.com',
    port=8883,
    tls=True
)
```

## QoS Levels

- QoS 0: At most once (fast, unreliable)
- QoS 1: At least once (reliable, default)
- QoS 2: Exactly once (slowest, guaranteed)

## Best Practices

1. Use TLS in production
2. Implement reconnection logic
3. Handle message callbacks asynchronously
4. Use topic wildcards efficiently

## Examples

See [examples/mqtt_sensor_pipeline.py](https://github.com/furcateresearch/furcate-bridge/blob/main/examples/mqtt_sensor_pipeline.py)
