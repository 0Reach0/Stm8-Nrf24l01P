# STM8-NRF24L01+ Library

This library provides a simple interface to control the NRF24L01+ transceiver module using STM8 microcontrollers. It supports basic TX and RX functionality,  and configuration of the NRF24L01+ module.


## Configuration in `NRF24.h`

0. **SetUp STM8 SPL Library**
   -Change 'stm8s.h' to your SPL header, if necessary.
  
2. **Pin Configuration**:
   - Update `CE_PIN`, `CSN_PIN`, `SCK_PIN`, `MISO_PIN`, and `MOSI_PIN` to match your hardware.

3. **Default Settings**:
   - Modify default register values (e.g., `DEFAULT_CONFIG_RX`, `DEFAULT_RF_CH`) if needed.

4. **SPI Settings**:
   - Adjust SPI baud rate, mode, and other parameters in `SPI_Init_NRF` if necessary.

## Functions

### Initialization

- `void tx_init(void)`: Initializes NRF24L01+ in TX mode.
- `void rx_init(void)`: Initializes NRF24L01+ in RX mode.
- `void nrf_deinit(void)`: Resets NRF24L01+ registers and deinitializes.

### Testing
 - `uint8_t tx_test(void)`: Returns 0 if TX configuration is correct, otherwise returns 1.

 - `uint8_t rx_test(void)`: Returns 0 if RX configuration is correct, otherwise returns 1.
### Data Transmission

- `void tx_send(const uint8_t *data, uint8_t len)`: Sends data in TX mode.
- `void rx_read(uint8_t *buf, uint8_t len)`: Receives data in RX mode.

### Register Access

- `uint8_t read_register(uint8_t reg)`: Reads a single register.
- `void write_register(uint8_t reg, uint8_t value)`: Writes to a single register.
- `void read_registerN(uint8_t reg, uint8_t *buf, uint8_t len)`: Reads multiple bytes from a register.
- `void write_registerN(uint8_t reg, const uint8_t *buf, uint8_t len)`: Writes multiple bytes to a register.

### Utility Functions

- `void delay(uint16_t n)`: Simple delay function.
- `void cs_high(void)`: Sets CSN pin high.
- `void cs_low(void)`: Sets CSN pin low.
- `void ce_high(void)`: Sets CE pin high.
- `void ce_low(void)`: Sets CE pin low.
- `void flush_tx(void)`: Flushes TX FIFO.
- `void flush_rx(void)`: Flushes RX FIFO.
- `void reset_status(void)`: Resets STATUS register.

## Example

### Transmitter

```c
#include "nrf24.h"

int main(void) {
    tx_init();
    uint8_t data[] = {0x01, 0x02, 0x03, 0x04};
    while (1) {
        tx_send(data, 4);  // Send data
        delay(1000);       // Delay between transmissions
    }
}
```

### Receiver

```c
#include "nrf24.h"

int main(void) {
    rx_init();
    uint8_t buffer[4];
    while (1) {
        rx_read(buffer, 4);  // Receive data
        // Process buffer
    }
}
```

## License

MIT License

---
