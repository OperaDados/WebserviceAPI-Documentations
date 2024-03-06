<h1> Testing API </h1>

Esta documentação destina-se a testes de integração usando API Resful com autenticação de tipo JWT.

Para criar usuário entre em contato pelo email contato@operadados.com ou pelo site www.operados.com

Para os testes locais use:
```sh
export URL_IOT="http://0.0.0.0:6000"
```
Para testar em produção:
```sh
export URL_IOT="https://api.devices.operadados.com"
```

<h2> Authentications: </h2>

Generate token:
```sh
TOKEN=$(curl -s -X POST -H 'Accept: application/json' -H 'Content-Type: application/json' --data '{"username":"test", "password":"test"}' ""${URL_IOT}/api/operadados/v1/login | jq -r '.token')
```
Check Authentication:
```sh
curl -svk -H "Content-Type: application/json" -H "Authorization: Bearer ${TOKEN}" \
--request GET  ""${URL_IOT}/api/operadados/v1/user
```
***
<h2> Devices: </h2>

Get air devices
```sh
curl -svk -H "Content-Type: application/json" -H "Authorization: Bearer ${TOKEN}" \
--request GET ""${URL_IOT}"/api/operadados/v1/airdevices?init_date=2024-01-01&end_date=2024-02-17%2023:59:59.999999&device_ids=c29500c03f2964cb5abb26ab467c95c3&device_ids=a0ffd961d6ff58ad9af3acd78559d458"
```
Tabela de dispositivos de testes

| ID                               | Serial | Location                                                              |
|----------------------------------|--------|-----------------------------------------------------------------------|
| c29500c03f2964cb5abb26ab467c95c3 | 1      | Parque da Cidade Dona Sarah Kubitschek - Brasilia DF                  |
| a0ffd961d6ff58ad9af3acd78559d458 | 2      | Parque da Cidade Dona Sarah Kubitschek - Brasilia DF                  |
| 5d37a448a9d06f7855909d87db9cdc86 | 4      | Parque da Cidade Dona Sarah Kubitschek  - Brasilia DF                 |
| f8fc473aa51d8a537b84f0698a425843 | 5      | Parque da Cidade Dona Sarah Kubitschek  - Brasilia DF                 |
| 5289e7a1ae5c5805a96102da28fcc103 | 6      | Parque da Cidade Dona Sarah Kubitschek  - Brasilia DF                 |
| 9ddc44f94cc8f2933c76d63b4ec79b0b | 10000  | Novo hardware revisão 2.0.0                                           |


Response
```json
[
    {
        "UUID": "64e4a4a4-a1c0-4745-ab27-2c6a34f99438",
        "battery": 4.979,
        "co2": 298,
        "device_id": "Device-2",
        "firmware": "0.0.1",
        "gateway_gps": {
            "lat": -15.685830116271973,
            "lng": -47.86117935180664
        },
        "gateway_id": "b0fd0b7003280000",
        "humidity": 88.79,
        "pressure": 88795,
        "protocol": 2,
        "pulse_counter": 0,
        "radio_signal": -113.0,
        "serial": "2",
        "soil": {
            "conductance": 0,
            "temperature": 0.0
        },
        "temperature": 22.94,
        "timestamp": "2024-02-09 19:53:18.159588",
        "voc": 0
    },
    {
        "UUID": "0c06044b-745d-4e87-9688-d9ab1b17aedc",
        "battery": 4.979,
        "co2": 298,
        "device_id": "Device-2",
        "firmware": "0.0.1",
        "gateway_gps": {
            "lat": -15.805370330810547,
            "lng": -47.89466857910156
        },
        "gateway_id": "b0fd0b7004400000",
        "humidity": 88.79,
        "pressure": 88795,
        "protocol": 2,
        "pulse_counter": 0,
        "radio_signal": -106.0,
        "serial": "2",
        "soil": {
            "conductance": 0,
            "temperature": 0.0
        },
        "temperature": 22.94,
        "timestamp": "2024-02-09 19:53:18.537141",
        "voc": 0
    },
    {
        "UUID": "a49c954a-0084-4de9-bba6-25ea17dc26e3",
        "battery": 4.979,
        "co2": 298,
        "device_id": "Device-2",
        "firmware": "0.0.1",
        "gateway_gps": {
            "lat": -15.776960372924805,
            "lng": -47.8875617980957
        },
        "gateway_id": "70b3d54b19520000",
        "humidity": 88.79,
        "pressure": 88795,
        "protocol": 2,
        "pulse_counter": 0,
        "radio_signal": -115.0,
        "serial": "2",
        "soil": {
            "conductance": 0,
            "temperature": 0.0
        },
        "temperature": 22.94,
        "timestamp": "2024-02-09 19:53:21.127203",
        "voc": 0
    }
]
```

| Field            | Description                                                |
|------------------|------------------------------------------------------------|
| UUID             | Universally Unique Identifier                              |
| battery          | Battery level in volts                                     |
| co2              | Carbon dioxide level in parts per million (ppm)            |
| device_id        | Identifier for the device                                  |
| firmware         | Firmware version of the device                             |
| gateway_gps      | GPS coordinates of the gateway                             |
| gateway_id       | Identifier for the gateway                                 |
| humidity         | Humidity level in percentage                               |
| pressure         | Atmospheric pressure in Pascals                            |
| protocol         | Communication protocol version                             |
| pulse_counter    | Pulse counter value rain milimimeters                      |
| radio_signal     | Radio signal strength in dBm                               |
| serial           | Serial number of the device                                |
| temperature      | Temperature in degrees Celsius                             |
| timestamp        | Date and time of the data in ISO format UTC                |
| voc              | Volatile Organic Compounds level in parts per bilion (ppb) |
| soil conductance | Conductance level in uS/cm                                 |
| soil temperature | Temperature in degrees Celsius                             |

***

Get average temperature

```sh
curl -svk -H "Content-Type: application/json" -H "Authorization: Bearer ${TOKEN}" \
--request GET ""${URL_IOT}"/api/operadados/v1/avertemperature?init_date=2024-01-01&end_date=2024-02-17%2023:59:59.999999&device_ids=c29500c03f2964cb5abb26ab467c95c3&device_ids=a0ffd961d6ff58ad9af3acd78559d458"
```

```json
[
    {
        "serial": "1",
        "temperature": 19.5,
        "timestamp": "2024-02-11 11:03:23.287055"
    },
    {
        "serial": "2",
        "temperature": 30.92,
        "timestamp": "2024-02-12 19:19:10.437828"
    },
    {
        "serial": "2",
        "temperature": 28.08,
        "timestamp": "2024-02-17 14:28:34.429010"
    },
    {
        "serial": "2",
        "temperature": 19.53,
        "timestamp": "2024-02-11 08:48:44.155755"
    },
    {
        "serial": "2",
        "temperature": 26.34,
        "timestamp": "2024-02-13 22:12:11.675673"
    },
    {
        "serial": "2",
        "temperature": 23.03,
        "timestamp": "2024-02-15 02:10:08.292944"
    },
    {
        "serial": "2",
        "temperature": 25.95,
        "timestamp": "2024-02-12 13:51:49.223147"
    }
]

```
