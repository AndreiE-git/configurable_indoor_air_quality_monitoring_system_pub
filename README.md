
<div align="center">
    <h1>Configurable Indoor Air Quality Monitoring System ( 2023 )</h1>
    <img src="docs/introduction/introduction.jpeg" width="65%" height="auto">
</div>


<!-- ______________________________________________________________________________________________________________________________________________________ -->
# 🚀 Introduction

This project implements a **configurable, modular, and wireless indoor air quality monitoring system** for real-time environmental monitoring.

Each device consists of a **sensor board** for environmental measurements and a **transmitter board** that collects sensor data and sends it to a server via a serial interface.
The **battery-powered design** enables flexible deployment, while a custom **web dashboard** provides real-time data visualization and device configuration.

**Project demo**: [ demo_link ]( https://drive.google.com/file/d/12pxGG4WmBNYgOO-bVUk5fnq6-0USTvlY/view )

**FIGURE: Project architecture**

<img src="docs/introduction/project_architecture.jpeg" width="45%" height="auto">


<!-- ______________________________________________________________________________________________________________________________________________________ -->
# 📒 Table of Content

- [🚀 Introduction](#-introduction)
- [📒 Table of Content](#-table-of-content)
- [📄 System Architecture](#-system-architecture)
- [⚙️ Components](#️-components)
  - [Master Board](#master-board)
  - [Slave Board 1](#slave-board-1)
  - [Slave Board 2](#slave-board-2)
- [🧰 Hardware Implementation](#-hardware-implementation)
  - [Schematic and Layout](#schematic-and-layout)
    - [ESP32 Master Board](#esp32-master-board)
    - [ATmega328P Slave Boards](#atmega328p-slave-boards)
  - [3D Enclosure](#3d-enclosure)
  - [Final Product](#final-product)
- [💻 Software Implementation](#-software-implementation)
  - [MCU Firmware](#mcu-firmware)
    - [ESP32 Firmware](#esp32-firmware)
    - [ATmega328P Firmware](#atmega328p-firmware)
  - [Node-RED](#node-red)
- [🏁 Conclusion](#-conclusion)
- [📚 References](#-references)


<!-- ______________________________________________________________________________________________________________________________________________________ -->
# 📄 System Architecture

The system consists of two board types:

* **Master board** – collects data from the slave boards and transmits it to the server.
* **Slave boards** – acquire environmental data from connected sensors.

Each board is built around its own microcontroller ( MCU ). Three boards were developed to validate the system: **one master board and two slave boards**.


<!-- ______________________________________________________________________________________________________________________________________________________ -->
# ⚙️ Components
<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
## Master Board

| Component               | Quantity | Purpose                                                           | Link                                                                                                                                |
| :---------------------- | :------: | :---------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------- |
| ESP32 development board |     1    | Master MCU; collects sensor data and communicates with the server | [ Link ](https://www.emag.ro/placa-dezvoltare-esp-wroom-32-esp-32s-ai011-s332/pd/D3NF9VBBM/?ref=history-shopping_346242005_38837_1) |


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
## Slave Board 1

| Component                   | Quantity | Purpose                                       | Link                                                                                                                                                      |
| :-------------------------- | :------: | :-------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Arduino Nano ( ATmega328P ) |     1    | Slave MCU; interfaces with sensors            | [ Link ](https://www.optimusdigital.ro/ro/compatibile-cu-arduino-nano/1686-placa-de-dezvoltare-compatibila-cu-arduino-nano-atmega328p-i-ch340.html)          |
| ADT7410 module              |     1    | High-accuracy digital temperature measurement | [ Link ](https://www.optimusdigital.ro/ro/senzori-senzori-de-temperatura/7542-modul-senzor-de-temperatura-adafruit-cu-acuratee-ridicata-adt7410-i2c.html) |
| MQ-2 module                 |     1    | Analog gas concentration measurement          | [ Link ](https://www.optimusdigital.ro/ro/senzori-de-gaze/107-modul-senzor-gas-mq-2.html?search_query=mq2&results=1)                                      |
| Level shifter module        |     1    | Logic-level voltage conversion                | [ Link ](https://www.optimusdigital.ro/ro/interfata-convertoare-de-niveluri/182-translator-de-nivel-bidirectional-cu-2-canale.html)                       |


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
## Slave Board 2

| Component                   | Quantity | Purpose                            | Link                                                                                                                                             |
| :-------------------------- | :------: | :--------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| Arduino Nano ( ATmega328P ) |     1    | Slave MCU; interfaces with sensors | [ Link ](https://www.optimusdigital.ro/ro/compatibile-cu-arduino-nano/1686-placa-de-dezvoltare-compatibila-cu-arduino-nano-atmega328p-i-ch340.html) |
| Microphone module           |     1    | Ambient sound level measurement    | [ Link ](https://www.techonicsltd.com/product/microphone-sound-sensor-module-compatible-with-official-arduino-boards/)                           |
| DS18B20 module              |     1    | Digital temperature measurement    | [ Link ](https://www.optimusdigital.ro/ro/senzori-senzori-de-temperatura/172-modul-senzor-de-temperatura-ds18b20.html)                           |
| Level shifter module        |     1    | Logic-level voltage conversion     | [ Link ](https://www.optimusdigital.ro/ro/interfata-convertoare-de-niveluri/182-translator-de-nivel-bidirectional-cu-2-canale.html)              |


<!-- ______________________________________________________________________________________________________________________________________________________ -->
# 🧰 Hardware Implementation
<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
## Schematic and Layout

The master and slave board schematics, together with the master PCB layout, were designed in **Altium Designer**.


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
### ESP32 Master Board

**FIGURE: Master board schematic**

<img src="docs/hardware_implementation/master_board_schematic.jpeg" width="100%" height="auto">

The master board is powered by **two 18650 Li-ion cells in series** ( 7.4 V nominal ).
A reverse-polarity protection diode and external rocker switch provide basic power protection and control.

To support different sensor modules, the board provides both **3.3 V and 5 V power rails**.
Since the system is battery-powered, **MCP16311 synchronous buck regulators** were used instead of linear regulators to improve power efficiency.

The board includes:

* **ESP32 development board** mounted through dual female headers
* **Battery voltage monitoring** through an ADC-connected resistor divider
* **Slave-board connector ( J1 )** for power and serial communication
* **3.3 V and 5 V regulated power rails**
* **Debug/status LEDs**

The PCB layout was optimized for a **compact footprint and single-sided manufacturing**, minimizing the number of wire bridges.
The board is mounted using **three M3×8 screws**.

**FIGURE: Master board layout ( top view )**

<img src="docs/hardware_implementation/master_board_layout.jpeg" width="50%" height="auto">

**FIGURE: Master board 3D model ( top view )**

<img src="docs/hardware_implementation/master_board_3d_model_top.jpeg" width="50%" height="auto">

**FIGURE: Master board 3D model ( bottom view )**

<img src="docs/hardware_implementation/master_board_3d_model_bot.jpeg" width="50%" height="auto">


**FIGURE: Master board after soldering ( top view )**

<img src="docs/hardware_implementation/master_board_soldered_top.jpeg" width="50%" height="auto">

**FIGURE: Master board after soldering ( bottom view )**

<img src="docs/hardware_implementation/master_board_soldered_bot.jpeg" width="50%" height="auto">


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
### ATmega328P Slave Boards

The slave boards are based on the **Arduino Nano ( ATmega328P )** and operate at **5 V** logic levels.
A **bidirectional level shifter** is used for serial communication with the 3.3 V ESP32 master.

**FIGURE: Slave 1 board schematic**

<img src="docs/hardware_implementation/slave_board_1_schematic.png" width="100%" height="auto">

**Slave board 1** integrates:

* **ADT7410** digital temperature sensor using **I²C**
* **MQ-2** analog gas sensor

The ADT7410 address pins ( A0 and A1 ) are connected to GND, resulting in the default **I²C address 0x48**.

**FIGURE: Slave 2 board schematic**

<img src="docs/hardware_implementation/slave_board_2_schematic.png" width="100%" height="auto">

**Slave board 2** integrates:

* **DS18B20** digital temperature sensor using **1-Wire**
* **Sound sensor** with analog output

Both slave boards were assembled on **perforated prototyping PCBs** with hand-wired connections.

**FIGURE: Slave 1 board after soldering ( top view )**

<img src="docs/hardware_implementation/slave_board_1_soldered_top.png" width="50%" height="auto">

**FIGURE: Slave 1 board after soldering ( bottom view )**

<img src="docs/hardware_implementation/slave_board_1_soldered_bot.png" width="50%" height="auto">

**FIGURE: Slave 2 board after soldering ( top view )**

<img src="docs/hardware_implementation/slave_board_2_soldered_top.png" width="50%" height="auto">

**FIGURE: Slave 2 board after soldering ( bottom view )**

<img src="docs/hardware_implementation/slave_board_2_soldered_bot.png" width="50%" height="auto">


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
## 3D Enclosure

The enclosure was designed in **Fusion 360** and prepared for 3D printing using **PrusaSlicer**.
It consists of three parts and houses the master board, slave board, battery pack, and rocker switch.

The **middle section** provides the main structural support for the electronics.
The master and slave boards are secured using M3 screws and interconnected by a cable.
The enclosure geometry was designed with sufficient board clearance while minimizing the need for printing supports.

**FIGURE: Middle part ( front view )**

<img src="docs/hardware_implementation/3d_case_middle_part_1.png" width="50%" height="auto">

**FIGURE: Middle part ( back view )**

<img src="docs/hardware_implementation/3d_case_middle_part_2.png" width="50%" height="auto">

The **bottom section** houses the battery pack and rocker switch.
A central guide rail aligns the middle section, while heat-set inserts provide secure mechanical fastening.

**FIGURE: Bottom part ( left view )**

<img src="docs/hardware_implementation/3d_case_bot_part_1.png" width="50%" height="auto">

**FIGURE: Bottom part ( right view )**

<img src="docs/hardware_implementation/3d_case_bot_part_2.png" width="50%" height="auto">

The **top section** closes the enclosure and includes an integrated retaining feature to secure the battery pack.

**FIGURE: Top part ( top view )**

<img src="docs/hardware_implementation/3d_case_top_part_1.png" width="50%" height="auto">

**FIGURE: Top part ( bottom view )**

<img src="docs/hardware_implementation/3d_case_top_part_2.png" width="50%" height="auto">


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
## Final Product

The completed device is shown below from the **left and top views**.

**FIGURE: Final product ( top view )**

<img src="docs/hardware_implementation/master_board_final_product_2.jpeg" width="60%" height="auto">

**FIGURE: Final product ( left view )**

<img src="docs/hardware_implementation/master_board_final_product_1.jpeg" width="60%" height="auto">


<!-- ______________________________________________________________________________________________________________________________________________________ -->
# 💻 Software Implementation
<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
## MCU Firmware

Communication between the master and slave boards uses **UART at 115200 baud with 8N1 configuration**.
The **master controls all communication**, requesting sensor configuration during startup and periodically polling the slave boards for measurements.

A **state machine** manages the communication process.
If a slave does not respond within **5 seconds**, the master enters a timeout state and stops communication with that slave.

**FIGURE: Serial communication state machine**

<img src="docs/software_implementation/serial_comm_state_machine.jpeg" width="50%" height="auto">

Two UART commands are implemented:

| Command                        | Purpose                                      | Request | Response |
| :----------------------------- | :------------------------------------------- | :-----: | :------: |
| `UART_CMD_READ_SENSORS_STATUS` | Retrieve sensor configuration during startup | 2 bytes |  4 bytes |
| `UART_CMD_READ_SENSORS_DATA`   | Request the latest sensor measurements       | 2 bytes |  8 bytes |


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
### ESP32 Firmware

The ESP32 firmware is configured with the **Wi-Fi SSID**, **password**, and **MQTT broker IP address** to establish the network connection and publish sensor data through **MQTT**.

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// WIFI SETUP
#include <WiFi.h>
#include <PubSubClient.h>
#include <Wire.h>

const char* ssid        = "TO_BE_REPLACED"; // WiFi SSID
const char* password    = "TO_BE_REPLACED"; // WiFi password
const char* mqtt_server = "TO_BE_REPLACED"; // MQTT server

WiFiClient   espClient;
PubSubClient client( espClient );
```

The functions used for WiFi:

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// WIFI FUNCTIONS
// This functions connects your ESP8266 to your router
void setup_wifi() {
    delay( 10 );
    Serial.println();
    Serial.print("Connecting to ");
    Serial.println( ssid );
    Serial.print("Password used: ");
    Serial.println( password );
    WiFi.mode( WIFI_STA );
    WiFi.begin( ssid, password );
    while( WiFi.status() != WL_CONNECTED )
    {
        delay( 500 );
        Serial.print( "." );
    }
    Serial.println("");
    Serial.print( "WiFi connected - ESP IP address: " );
    Serial.println( WiFi.localIP() );
}

// This function is executed when some device publishes a message to a topic that your ESP8266 is subscribed to
// Change the function below to add logic to your program, so when a device publishes a message to a topic that
// your ESP8266 is subscribed you can actually do something
void callback( String topic, byte* message, unsigned int length )
{
    Serial.print( "Message arrived on topic: " );
    Serial.println( topic );
}

// This functions reconnects your ESP8266 to your MQTT broker
// Change the function below if you want to subscribe to more topics with your ESP8266
void reconnect()
{
    while( !client.connected() )
    {
        Serial.print( "Attempting MQTT connection..." );
        if( client.connect( "ESP8266Client" ) )
        {
            Serial.println( "connected" );
        }
        else
        {
            Serial.print( "failed, rc=" );
            Serial.print( client.state() );
            Serial.println( " try again in 5 seconds" );
            delay( 5000 );
        }
    }
}
```

The serial communication can be configured by modifying the following macros:

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// SERIAL COMM SETUP
// general macros
#define TRUE                                        true
#define FALSE                                       false

#define SERIAL_1_BAUDRATE                           115200
#define SERIAL_2_BAUDRATE                           115200

#define ESP_MASTER_RX_PIN                           15
#define ESP_MASTER_TX_PIN                           2

#define UART_CHECK_COUNTER_MAX                      10
#define UART_TIMEOUT_COUNTER_MAX                    50

#define UART_END_BYTE				                0x55

// command list
#define UART_CMD_READ_SENSORS_STATUS		        0x10
#define UART_CMD_READ_SENSORS_DATA		            0x20

// flags pos
#define SENSOR_TEMP_SUPPORTED                       0x01
#define SENSOR_TVOC_SUPPORTED                       0x02
#define SENSOR_SOUND_SUPPORTED                      0x04

#define UART_REQUEST_CMD_MAX_LENGTH	                2
#define UART_RESPONSE_READ_DATA_MAX_LENGTH	        8
#define UART_RESPONSE_INIT_CMD_MAX_LENGTH	        4

#define UART_READ_BUFFER_LENGTH		                10
#define UART_WRITE_BUFFER_LENGTH		            5

// sensor flag position
#define SENSOR_TEMP_SUPPORTED                       0x01
#define SENSOR_TVOC_SUPPORTED                       0x02
#define SENSOR_SOUND_SUPPORTED                      0x04

// UART flags structure
typedef union
{
    struct{
        uint8_t is_busy                 :1,
                sensor_temp_supported   :1,
                sensor_tvoc_supported   :1,
                sensor_sound_supported  :1,
                                        :4;
    };

    uint8_t word8;
}UART_COM_FLAGS;

// UART main structure
typedef struct
{
	uint8_t write_buffer[UART_WRITE_BUFFER_LENGTH];
	uint8_t read_buffer[UART_READ_BUFFER_LENGTH];
	uint8_t buffer_counter;

    uint8_t check_counter;
    uint8_t timeout_counter;

    UART_COM_FLAGS flags;
}UART_COM_STRUCT;

UART_COM_STRUCT UART_com;
```

At startup, the master sends **`UART_CMD_READ_SENSORS_STATUS`** to retrieve the slave board's supported sensors.
If no valid response is received within the configured timeout, the master enters the **timeout state** and halts operation.

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// SETUP FUNCTION
void init_com_protocol_UART()
{
    UART_com.flags.word8     = 0x00;
    UART_com.flags.is_busy   = TRUE;
    UART_com.timeout_counter = UART_TIMEOUT_COUNTER_MAX;
    UART_com.check_counter   = UART_CHECK_COUNTER_MAX;
    UART_com.buffer_counter  = 0;
    UART_com.write_buffer[0] = UART_CMD_READ_SENSORS_STATUS;
    UART_com.write_buffer[1] = UART_END_BYTE;
    Serial2.write( UART_com.write_buffer, 2 );
}
```

The WiFi and the serial communications are initialized in the setup functions:

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// SETUP FUNCTION
void setup() {
    // setup the serial comms
    Serial.begin(  SERIAL_1_BAUDRATE );
    Serial2.begin( SERIAL_2_BAUDRATE, SERIAL_8N1, ESP_MASTER_RX_PIN, ESP_MASTER_TX_PIN );
    delay( 4000 );

    // prepare wifi config
    setup_wifi();
    client.setServer( mqtt_server, 1883 );
    client.setCallback( callback );

    // init the serial config
    init_com_protocol_UART();

    Serial.println( "data sent" );
}
```

The master periodically sends the **`UART_CMD_READ_SENSORS_DATA`** command to acquire sensor measurements.
Upon receiving a valid response, it publishes the data to the MQTT broker according to the slave board's configuration.

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// LOOP FUNCTION
void loop()
{
    uint8_t data_byte_read;
    int8_t  flags_processed;

    // reconnect to MQTT
    if( !client.connected() )
    {
        reconnect();
    }
    if( !client.loop() )
    {
        client.connect( "ESP8266Client" );
    }

    // check for timeouts
    if( UART_com.flags.is_busy == TRUE )
    {
        UART_com.timeout_counter--;

        if( UART_com.timeout_counter == 0 )
        {
            UART_com.flags.word8 = 0x00;
            Serial.println( "Communication has been reset and blocked!" );
            while( 1 );
        }
    }
    else
    {
        UART_com.check_counter--;

        // read the sensors again
        if( UART_com.check_counter == 0 )
        {
            UART_com.flags.is_busy   = TRUE;
            UART_com.check_counter   = UART_CHECK_COUNTER_MAX;
            UART_com.timeout_counter = UART_TIMEOUT_COUNTER_MAX;

            UART_com.write_buffer[0] = UART_CMD_READ_SENSORS_DATA;
            UART_com.write_buffer[1] = UART_END_BYTE;
            Serial2.write( UART_com.write_buffer, 2 );
        }

    }

    // read every byte available from the receiver's buffer
    while( Serial2.available() )
    {
        data_byte_read = Serial2.read();

        if( UART_com.flags.is_busy == TRUE )
        {
            UART_com.timeout_counter = UART_TIMEOUT_COUNTER_MAX;
            UART_com.check_counter   = UART_CHECK_COUNTER_MAX;
            UART_com.read_buffer[UART_com.buffer_counter] = data_byte_read;
            UART_com.buffer_counter++;

            if( ( ( UART_com.buffer_counter == UART_RESPONSE_INIT_CMD_MAX_LENGTH  ) && ( UART_com.write_buffer[0] == UART_CMD_READ_SENSORS_STATUS ) ) ||
                ( ( UART_com.buffer_counter == UART_RESPONSE_READ_DATA_MAX_LENGTH ) && ( UART_com.write_buffer[0] == UART_CMD_READ_SENSORS_DATA   ) ) )
            {
                UART_com.flags.is_busy = FALSE;
                UART_com.buffer_counter = 0;

                switch( UART_com.read_buffer[0] )
                {
                    case UART_CMD_READ_SENSORS_STATUS:
                        Serial.println( "Config read ..." );

                        flags_processed = ( int8_t )( ( ( ( uint16_t )UART_com.read_buffer[2] ) << 8 ) | UART_com.read_buffer[1] );

                        UART_com.flags.sensor_temp_supported  = ( ( flags_processed & SENSOR_TEMP_SUPPORTED  ) != 0x00 ) ? TRUE : FALSE;
                        UART_com.flags.sensor_tvoc_supported  = ( ( flags_processed & SENSOR_TVOC_SUPPORTED  ) != 0x00 ) ? TRUE : FALSE;
                        UART_com.flags.sensor_sound_supported = ( ( flags_processed & SENSOR_SOUND_SUPPORTED ) != 0x00 ) ? TRUE : FALSE;
                        break;

                    case UART_CMD_READ_SENSORS_DATA:
                        Serial.println( "Data read ..." );

                        if( UART_com.flags.sensor_temp_supported  == TRUE ) { client.publish( "ESP32/temp",  String( ( float   )( ( ( uint16_t )UART_com.read_buffer[2] << 8 ) | UART_com.read_buffer[1] ) / 10 ).c_str() ); }
                        if( UART_com.flags.sensor_tvoc_supported  == TRUE ) { client.publish( "ESP32/tvoc",  String( ( int16_t )( ( ( uint16_t )UART_com.read_buffer[4] << 8 ) | UART_com.read_buffer[3] )      ).c_str() ); }
                        if( UART_com.flags.sensor_sound_supported == TRUE ) { client.publish( "ESP32/sound", String( ( int16_t )( ( ( uint16_t )UART_com.read_buffer[6] << 8 ) | UART_com.read_buffer[5] )      ).c_str() ); }

                        break;
                }
            }
        }
    }

    delay( 100 );
}
```


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
### ATmega328P Firmware

The same firmware is used for both slave boards, with the target board selected at compile time using either **`USE_SLAVE_1`** or **`USE_SLAVE_2`**.
Exactly one macro must be defined; defining both or neither results in a **compilation error**.

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// SETUP SLAVE TO BUILD
#define USE_SLAVE_1
#undef  USE_SLAVE_1
#define USE_SLAVE_2
// #undef  USE_SLAVE_2


// checking the config
#if defined( USE_SLAVE_1 ) && defined( USE_SLAVE_2 )
    #error Multiple slaves defined at the same time!
#endif
#if !defined( USE_SLAVE_1 ) && !defined( USE_SLAVE_2 )
    #error No slaves defined!
#endif
```

Depending on which board is defined, a specific set of sensors will be used:

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// SLAVE 1 CONFIG
#ifdef USE_SLAVE_1
    #define USE_SENSOR_TEMP_ADT7410
    #define USE_SENSOR_TVOC_MQ2
#endif

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// SLAVE 2 CONFIG
#ifdef USE_SLAVE_2
    #define USE_SENSOR_SOUND_LM393
    #define USE_SENSOR_TEMP_DS18B20
#endif
```

The required sensor libraries and configuration settings are conditionally included based on the selected slave board.
The following functions are responsible for acquiring data from the corresponding sensors.

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// SENSOR FUNCTIONS
#ifdef USE_SENSOR_TVOC_MQ2
    #define SENSOR_TVOC_MQ2_PIN                     A7

    int16_t measure_sensor_tvoc_MQ2()
    {
        return ( int16_t )( analogRead( SENSOR_TVOC_MQ2_PIN ) );
    }
#endif

#ifdef USE_SENSOR_TEMP_DS18B20
    #include <OneWire.h>
    #include <DallasTemperature.h>

    #define SENSOR_TEMP_DS18B20_PIN                 7

    OneWire oneWire( SENSOR_TEMP_DS18B20_PIN );
    DallasTemperature sensor_DS18B20( &oneWire );

    int16_t measure_sensor_temp_DS18B20()
    {
        sensor_DS18B20.requestTemperatures();
        return ( int16_t )( sensor_DS18B20.getTempCByIndex( 0 ) * 10 );
    }
#endif

#ifdef USE_SENSOR_SOUND_LM393
    #define SENSOR_SOUND_LM393_PIN                  A6

    int16_t measure_sensor_SOUND_LM393()
    {
        return ( int16_t )( analogRead( SENSOR_SOUND_LM393_PIN ) );
    }
#endif

#ifdef USE_SENSOR_TEMP_ADT7410
    #include <Wire.h>
    #include <Adafruit_Sensor.h>
    #include "Adafruit_ADT7410.h"

    Adafruit_ADT7410 temp_sensor_ADT7410 = Adafruit_ADT7410();

    float measure_sensor_temp_ADT7410()
    {
        return ( int16_t )( temp_sensor_ADT7410.readTempC() * 10 );
    }
#endif
```

The function below initializes all **configured sensors**.

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// INIT ALL SENSOR CONFIG
void init_all_sensor_config()
{
#ifdef USE_SENSOR_TVOC_MQ2
    pinMode( SENSOR_TVOC_MQ2_PIN, INPUT );
#endif
#ifdef USE_SENSOR_TEMP_DS18B20
    pinMode( SENSOR_TEMP_DS18B20_PIN, INPUT );
#endif
#ifdef USE_SENSOR_SOUND_LM393
    pinMode( SENSOR_SOUND_LM393_PIN, INPUT );
#endif
#ifdef USE_SENSOR_TEMP_ADT7410
    if( !temp_sensor_ADT7410.begin() )
    {
        Serial.println( "Couldn't find ADT7410!" );
        // while( 1 );
    }
#endif
}
```

Serial communication is configured using the following macros:

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// SERIAL MACROS AND VARIABLES
// general macros used
#define UART_REQUEST_CMD_MAX_LENGTH                 2
#define UART_RESPONSE_CMD_MAX_LENGTH                4
#define UART_CMD_BYTE_POS                           0
#define UART_END_BYTE_POS                           1
#define UART_END_BYTE                               0x55

// commands used
#define UART_CMD_READ_SENSORS_STATUS                0x10
#define UART_CMD_READ_SENSORS_DATA                  0x20

// flag positions
#define SENSOR_TEMP_SUPPORTED                       0x01
#define SENSOR_TVOC_SUPPORTED                       0x02
#define SENSOR_SOUND_SUPPORTED                      0x04

// length of buffers
#define UART_READ_BUFFER_LENGTH                     5
#define UART_WRITE_BUFFER_LENGTH                    5

typedef struct
{
	uint8_t write_buffer[UART_WRITE_BUFFER_LENGTH];
	uint8_t read_buffer[UART_READ_BUFFER_LENGTH];

	uint8_t buffer_counter;
}SERIAL_COM;

SERIAL_COM serial_com;
```

The **UART interface is initialized at 115200 baud**, and all configured sensors are initialized at startup.

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// SETUP FUNCTION
void setup()
{
    Serial.begin( 115200 );
    delay( 1000 );

    init_all_sensor_config();
}
```

Commands are processed upon reception, and sensor data is read on request.

``` c
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// LOOP FUNCTION
void loop()
{
    int16_t response_data_word16;

	if( Serial.available() == true )
	{
		serial_com.read_buffer[serial_com.buffer_counter] = ( uint8_t )Serial.read();
		serial_com.buffer_counter++;

		if( serial_com.buffer_counter == UART_REQUEST_CMD_MAX_LENGTH )
		{
			response_data_word16 	   = -32768;
			serial_com.buffer_counter  = 0;
            serial_com.write_buffer[0] = serial_com.read_buffer[0];
			switch( serial_com.read_buffer[UART_CMD_BYTE_POS] )
			{

				case UART_CMD_READ_SENSORS_STATUS:
					response_data_word16 = ( int16_t )( 0x00
							            #if defined( USE_SENSOR_TEMP_ADT7410 ) || defined( USE_SENSOR_TEMP_DS18B20 )
								            | ( SENSOR_TEMP_SUPPORTED )
                                        #endif
                                        #if defined( USE_SENSOR_TVOC_MQ2 )
								            | ( SENSOR_TVOC_SUPPORTED )
                                        #endif
                                        #if defined( USE_SENSOR_SOUND_LM393 )
								            | ( SENSOR_SOUND_SUPPORTED )
							            #endif
                                                        );

                    serial_com.write_buffer[1] =   response_data_word16        & 0xFF;
                    serial_com.write_buffer[2] = ( response_data_word16 >> 8 ) & 0xFF;
                    serial_com.write_buffer[3] = UART_END_BYTE;
                    Serial.write( serial_com.write_buffer, 4 );
					break;

				case UART_CMD_READ_SENSORS_DATA:
					#ifdef USE_SENSOR_TEMP_ADT7410
						response_data_word16 = measure_sensor_temp_ADT7410();
					#else
						#ifdef USE_SENSOR_TEMP_DS18B20
							response_data_word16 = measure_sensor_temp_DS18B20();
                        #else
                            response_data_word16 = 0x00;
                        #endif
					#endif

                    serial_com.write_buffer[1] =   response_data_word16 	   & 0xFF;
                    serial_com.write_buffer[2] = ( response_data_word16 >> 8 ) & 0xFF;

					#ifdef USE_SENSOR_TVOC_MQ2
					    response_data_word16 = measure_sensor_tvoc_MQ2();
                    #else
                        response_data_word16 = 0x00;
                    #endif

                    serial_com.write_buffer[3] =   response_data_word16        & 0xFF;
                    serial_com.write_buffer[4] = ( response_data_word16 >> 8 ) & 0xFF;

					#ifdef USE_SENSOR_SOUND_LM393
                        response_data_word16 = measure_sensor_SOUND_LM393();
                    #else
                        response_data_word16 = 0x00;
					#endif

                    serial_com.write_buffer[5] =   response_data_word16        & 0xFF;
                    serial_com.write_buffer[6] = ( response_data_word16 >> 8 ) & 0xFF;

                    serial_com.write_buffer[7] = UART_END_BYTE;
                    Serial.write( serial_com.write_buffer, 8 );
					break;
			}
		}
	}
}
```


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------ -->
## Node-RED

Sensor data acquired by the master board and published to the MQTT broker is visualized through a **Node-RED Dashboard**.

**FIGURE: Node-RED web dashboard**

<img src="docs/software_implementation/node_red_webpage_dashboard.jpeg" width="70%" height="auto">

The dashboard was developed using **Node-RED** and provides real-time visualization of the acquired sensor data.

Communication between the **ESP32** and dashboard uses **MQTT over TCP/IP**.
The system consists of two MQTT clients—the ESP32 and Node-RED—which exchange messages through a locally hosted **MQTT broker** running on the laptop.

**FIGURE: MQTT architecture**

<img src="docs/software_implementation/mqtt_structure.jpeg" width="60%" height="auto">

Three MQTT topics are used to transmit **temperature, TVOC, and sound** measurements.
The ESP32 publishes the sensor data, while the Node-RED dashboard subscribes to the corresponding topics for visualization.

**FIGURE: Node Red webpage flow**

<img src="docs/software_implementation/node_red_webpage_flow.png" width="50%" height="auto">

Node-RED flow:

``` json
[ { "id": "156fbaa406ad8123", "type": "tab", "label": "Flow 1", "disabled": false, "info": "", "env": [] }, { "id": "203987ec71ee9f87", "type": "mqtt in", "z": "156fbaa406ad8123", "name": "ESP32/temp", "topic": "ESP32/temp", "qos": "2", "datatype": "auto-detect", "broker": "a03b8463c0d7b983", "nl": false, "rap": true, "rh": 0, "inputs": 0, "x": 370, "y": 300, "wires": [ [ "9a7d31c60c80b677", "3804aaebb1665203" ] ] }, { "id": "a187927df009e949", "type": "ui_gauge", "z": "156fbaa406ad8123", "name": "TVOC", "group": "f6d1c6bb403af6e6", "order": 0, "width": 0, "height": 0, "gtype": "wave", "title": "TVOC gauge", "label": "units", "format": "{{value}}", "min": 0, "max": "1023", "colors": [ "#00b500", "#e6e600", "#ca3838" ], "seg1": "", "seg2": "", "diff": false, "className": "", "x": 530, "y": 380, "wires": [] }, { "id": "830a1915f1ec3c49", "type": "mqtt in", "z": "156fbaa406ad8123", "name": "ESP32/tvoc", "topic": "ESP32/tvoc", "qos": "2", "datatype": "auto-detect", "broker": "a03b8463c0d7b983", "nl": false, "rap": true, "rh": 0, "inputs": 0, "x": 370, "y": 380, "wires": [ [ "a187927df009e949", "2759dc64eb94826a" ] ] }, { "id": "fb719ceab83b097f", "type": "mqtt in", "z": "156fbaa406ad8123", "name": "ESP32/sound", "topic": "ESP32/sound", "qos": "2", "datatype": "auto-detect", "broker": "a03b8463c0d7b983", "nl": false, "rap": true, "rh": 0, "inputs": 0, "x": 370, "y": 460, "wires": [ [ "7c6e3bf5c472d3e7", "3bb8702e06e15257" ] ] }, { "id": "9a7d31c60c80b677", "type": "ui_chart", "z": "156fbaa406ad8123", "name": "Temperature", "group": "f456dba3c69cf4bc", "order": 1, "width": 0, "height": 0, "label": "Temperature graph", "chartType": "line", "legend": "false", "xformat": "HH:mm:ss", "interpolate": "linear", "nodata": "", "dot": false, "ymin": "", "ymax": "", "removeOlder": 1, "removeOlderPoints": "", "removeOlderUnit": "3600", "cutout": 0, "useOneColor": false, "useUTC": false, "colors": [ "#1f77b4", "#aec7e8", "#ff7f0e", "#2ca02c", "#98df8a", "#d62728", "#ff9896", "#9467bd", "#c5b0d5" ], "outputs": 1, "useDifferentColor": false, "className": "", "x": 550, "y": 300, "wires": [ [] ] }, { "id": "7c6e3bf5c472d3e7", "type": "ui_chart", "z": "156fbaa406ad8123", "name": "Sound", "group": "fa9c6e33a42140ac", "order": 1, "width": 0, "height": 0, "label": "Sound chart", "chartType": "line", "legend": "false", "xformat": "HH:mm:ss", "interpolate": "linear", "nodata": "", "dot": false, "ymin": "", "ymax": "", "removeOlder": 1, "removeOlderPoints": "", "removeOlderUnit": "3600", "cutout": 0, "useOneColor": false, "useUTC": false, "colors": [ "#1f77b4", "#aec7e8", "#ff7f0e", "#2ca02c", "#98df8a", "#d62728", "#ff9896", "#9467bd", "#c5b0d5" ], "outputs": 1, "useDifferentColor": false, "className": "", "x": 530, "y": 460, "wires": [ [] ] }, { "id": "3bb8702e06e15257", "type": "debug", "z": "156fbaa406ad8123", "name": "debug 1", "active": true, "tosidebar": true, "console": false, "tostatus": false, "complete": "false", "statusVal": "", "statusType": "auto", "x": 540, "y": 500, "wires": [] }, { "id": "3804aaebb1665203", "type": "debug", "z": "156fbaa406ad8123", "name": "debug 2", "active": true, "tosidebar": true, "console": false, "tostatus": false, "complete": "false", "statusVal": "", "statusType": "auto", "x": 540, "y": 340, "wires": [] }, { "id": "2759dc64eb94826a", "type": "debug", "z": "156fbaa406ad8123", "name": "debug 3", "active": true, "tosidebar": true, "console": false, "tostatus": false, "complete": "false", "statusVal": "", "statusType": "auto", "x": 540, "y": 420, "wires": [] }, { "id": "a03b8463c0d7b983", "type": "mqtt-broker", "name": "ESP32", "broker": "localhost", "port": "1883", "clientid": "", "autoConnect": true, "usetls": false, "protocolVersion": "4", "keepalive": "60", "cleansession": true, "autoUnsubscribe": true, "birthTopic": "ESP32", "birthQos": "1", "birthRetain": "false", "birthPayload": "", "birthMsg": {}, "closeTopic": "", "closeQos": "0", "closeRetain": "false", "closePayload": "", "closeMsg": {}, "willTopic": "", "willQos": "0", "willRetain": "false", "willPayload": "", "willMsg": {}, "userProps": "", "sessionExpiry": "" }, { "id": "f6d1c6bb403af6e6", "type": "ui_group", "name": "TVOC", "tab": "8593b1ea584e9609", "order": 2, "disp": true, "width": "6", "collapse": false, "className": "" }, { "id": "f456dba3c69cf4bc", "type": "ui_group", "name": "Temperature", "tab": "8593b1ea584e9609", "order": 1, "disp": true, "width": "6", "collapse": false, "className": "" }, { "id": "fa9c6e33a42140ac", "type": "ui_group", "name": "Sound", "tab": "8593b1ea584e9609", "order": 3, "disp": true, "width": "6", "collapse": false, "className": "" }, { "id": "8593b1ea584e9609", "type": "ui_tab", "name": "Home", "icon": "dashboard", "order": 1, "disabled": false, "hidden": false } ]
```


<!-- ______________________________________________________________________________________________________________________________________________________ -->
# 🏁 Conclusion

The project demonstrates a **modular and configurable indoor air quality monitoring system** combining embedded firmware, wireless communication, MQTT, and real-time data visualization.

The modular architecture allows additional sensor boards and monitoring devices to be integrated with minimal changes, while the MQTT-based communication framework provides a flexible foundation for expanding the system.


<!-- ______________________________________________________________________________________________________________________________________________________ -->
# 📚 References

- [ ESP32 datasheet ]( https://documentation.espressif.com/esp32-wroom-32_datasheet_en.pdf )
- [ ATMEGA328P datasheet ]( https://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-7810-Automotive-Microcontrollers-ATmega328P_Datasheet.pdf )
- [ MCP16311 datasheet ]( https://ww1.microchip.com/downloads/en/DeviceDoc/MCP16311-Family-Data-Sheet-DS20005255C.pdf )
- [ ADT7410 datasheet ]( https://www.analog.com/media/en/technical-documentation/data-sheets/adt7410.pdf )
- [ ADT7410 library ]( https://github.com/adafruit/Adafruit_ADT7410 )
- [ DS18B20 datasheet ]( https://www.analog.com/media/en/technical-documentation/data-sheets/ds18b20.pdf )
- [ DS18B20 library ]( https://github.com/milesburton/Arduino-Temperature-Control-Library )
- [ One Wire library ]( https://github.com/PaulStoffregen/OneWire )
- [ Node-RED documentation ]( https://nodered.org/docs/getting-started/ )
- [ Node-RED and MQTT tutorial and libraries ]( https://microcontrollerslab.com/esp32-mqtt-publish-multiple-sensor-readings-node-red/ )
