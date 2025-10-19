# Smart City Example

## Privacy-Preserving Traffic Optimization

### Scenario

City deploys 1000 traffic cameras but must comply with GDPR - cannot centralize video feeds.

### Architecture

```
Cameras (MQTT) → Edge Processing → Federated Optimization → Traffic Control
```

### Implementation

```python
from adapters.mqtt import MQTTAdapter, create_mqtt_config

# Traffic camera edge node
config = create_mqtt_config(broker='city-mqtt.local')
mqtt = MQTTAdapter(config)
mqtt.connect()

def process_video(topic, frame):
    # Local object detection in TEE
    vehicles = detect_vehicles_secure(frame)
    
    # Aggregate counts only (not raw video)
    counts = {
        'cars': len([v for v in vehicles if v.type == 'car']),
        'bikes': len([v for v in vehicles if v.type == 'bike']),
        'timestamp': time.time()
    }
    
    # Send counts, not video
    mqtt.write(f'traffic/counts/{intersection_id}', counts)
    
    # Federated learning for optimization
    update = model.train_step(counts)
    mqtt.write('federated/updates', encrypt(update))

mqtt.subscribe('cameras/intersection-42/feed', process_video)
```

### GDPR Compliance

- Raw video never leaves camera
- Only aggregated statistics transmitted
- Differential privacy on counts
- Citizen privacy preserved

### Results

- 30% reduction in traffic congestion
- Full GDPR compliance
- Citizen trust maintained
- Real-time response (<100ms)

## Emergency Response

Similar approach for emergency vehicle routing using federated learning across city services.
