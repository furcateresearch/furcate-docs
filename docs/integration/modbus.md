# Modbus Integration

## Overview

Connect Furcate to PLCs and industrial equipment using Modbus TCP/RTU.

## Installation

```bash
pip install furcate-bridge
```

## Modbus TCP

```python
from adapters.modbus import ModbusAdapter

config = {
    'type': 'tcp',
    'host': '192.168.1.100',
    'port': 502,
    'unit_id': 1
}

adapter = ModbusAdapter(config)
adapter.connect()

# Read holding registers
values = adapter.read_holding_registers(address=0, count=10)

# Write coil
adapter.write_coil(address=0, value=True)
```

## Modbus RTU (Serial)

```python
config = {
    'type': 'rtu',
    'port': '/dev/ttyUSB0',
    'baudrate': 9600,
    'unit_id': 1
}
```

## Function Codes

| Code | Function | Method |
|------|----------|--------|
| 1 | Read Coils | `read_coils()` |
| 3 | Read Holding Registers | `read_holding_registers()` |
| 5 | Write Single Coil | `write_coil()` |
| 6 | Write Single Register | `write_register()` |

## Industrial Use Cases

- Predictive maintenance on CNC machines
- Quality control in production lines
- Energy monitoring in factories

## Examples

See [examples/modbus_plc_reader.py](https://github.com/furcateresearch/furcate-bridge/blob/main/examples/modbus_plc_reader.py)
