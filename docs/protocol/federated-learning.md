# Federated Learning

## How It Works

1. Coordinator initializes global model
2. Devices train locally on private data
3. Devices send encrypted gradients  
4. Coordinator aggregates securely
5. Updated model distributed to devices

## Privacy Guarantees

- Raw data never transmitted
- Differential privacy applied to gradients
- Secure multi-party aggregation
- Individual updates never visible

## Code Example

```python
# Device-side training
model.train(local_data)
gradients = model.get_gradients()
encrypted = encrypt(gradients, coordinator_key)
send_update(encrypted, attestation)
```

See [full specification](../../furcate-protocol/specification/02-federated-learning.md).
