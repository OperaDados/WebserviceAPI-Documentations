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


Response
```json
[
    {
        "UUID": "71464ae6-2798-4b75-a356-b89958eaa9e9",
        "battery": 5.013,
        "co2": 273,
        "device_id": "Device-1",
        "firmware": "0.0.1",
        "gateway_gps": {
            "lat": -15.805370330810547,
            "lng": -47.89466857910156
        },
        "gateway_id": "b0fd0b7004400000",
        "humidity": 81.08,
        "pressure": 88983,
        "protocol": 2,
        "pulse_counter": 0,
        "radio_signal": -114.0,
        "serial": "1",
        "temperature": 25.17,
        "timestamp": "2024-02-09 19:54:51.068659",
        "voc": 0
    },
    {
        "UUID": "52f84938-940a-4673-9121-882fad1e84c0",
        "battery": 5.013,
        "co2": 293,
        "device_id": "Device-1",
        "firmware": "0.0.1",
        "gateway_gps": {
            "lat": -15.873499870300293,
            "lng": -48.073509216308594
        },
        "gateway_id": "b0fd0b7007020000",
        "humidity": 85.2,
        "pressure": 88993,
        "protocol": 2,
        "pulse_counter": 0,
        "radio_signal": -117.0,
        "serial": "1",
        "temperature": 24.95,
        "timestamp": "2024-02-09 20:09:57.825031",
        "voc": 0
    }
]
```

| Field           | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| UUID            | Universally Unique Identifier                                           |
| battery         | Battery level in volts                                                  |
| co2             | Carbon dioxide level in parts per million (ppm)                         |
| device_id       | Identifier for the device                                               |
| firmware        | Firmware version of the device                                          |
| gateway_gps     | GPS coordinates of the gateway                                          |
| gateway_id      | Identifier for the gateway                                              |
| humidity        | Humidity level in percentage                                            |
| pressure        | Atmospheric pressure in Pascals                                         |
| protocol        | Communication protocol version                                          |
| pulse_counter   | Pulse counter value rain milimimeters                                   |
| radio_signal    | Radio signal strength in dBm                                            |
| serial          | Serial number of the device                                             |
| temperature     | Temperature in degrees Celsius                                          |
| timestamp       | Date and time of the data in ISO format                                 |
| voc             | Volatile Organic Compounds level in parts per bilion (ppb)              |