# Custom Protocol Adapters

## Creating Your Own Adapter

Extend `BaseAdapter` to support any protocol:

```python
from adapters.base import BaseAdapter

class MyProtocolAdapter(BaseAdapter):
    def __init__(self, config):
        super().__init__(config)
        # Initialize your protocol client
    
    def connect(self) -> bool:
        # Connection logic
        self.connected = True
        return True
    
    def disconnect(self) -> None:
        # Cleanup
        self.connected = False
    
    def read(self, address: str):
        # Read data from device
        pass
    
    def write(self, address: str, data):
        # Write data to device
        pass
```

## Required Methods

- `connect()`: Establish connection
- `disconnect()`: Clean shutdown
- `read()`: Read from device
- `write()`: Write to device

## Optional Enhancements

- Callbacks: `register_callback()`, `trigger_callback()`
- Metadata: Override `get_metadata()`
- Error handling: Custom exceptions

## Example: REST API Adapter

```python
import requests

class RESTAdapter(BaseAdapter):
    def connect(self):
        self.base_url = self.config['base_url']
        self.session = requests.Session()
        self.connected = True
        return True
    
    def read(self, endpoint):
        response = self.session.get(f"{self.base_url}/{endpoint}")
        return response.json()
    
    def write(self, endpoint, data):
        response = self.session.post(
            f"{self.base_url}/{endpoint}",
            json=data
        )
        return response.ok
```

## Contributing

Submit your adapters as pull requests to [furcate-bridge](https://github.com/furcateresearch/furcate-bridge)!
