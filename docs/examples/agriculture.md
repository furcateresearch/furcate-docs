# Precision Agriculture Example

## Crop Disease Detection Across Farms

### Scenario

10 farms want to collaboratively train a disease detection model without sharing proprietary crop data.

### Architecture

```
IoT Cameras (MQTT) → Edge Nodes → Federated Learning → Shared Model
```

### Implementation

```python
from adapters.mqtt import MQTTAdapter, create_mqtt_config

# Each farm's edge node
config = create_mqtt_config(
    broker='farm-mqtt.local',
    client_id=f'farm-{farm_id}'
)

mqtt = MQTTAdapter(config)
mqtt.connect()

# Subscribe to camera feeds
def process_image(topic, image_data):
    # Local inference
    diseases = model.detect(image_data)
    
    # Train on local data
    model.train_step(image_data, labels)
    
    # Send encrypted update
    update = model.get_encrypted_update()
    mqtt.write('federated/updates', update)

mqtt.subscribe('cameras/#', process_image)
```

### Benefits

- Farms share knowledge without sharing data
- Better model than any single farm could train
- Compliant with agricultural data regulations
- Works offline (LoRaWAN for remote fields)

## Soil Monitoring

LoRaWAN sensors for soil moisture, using federated learning to optimize irrigation across region.
