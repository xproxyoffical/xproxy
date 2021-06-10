
# XProxy.IO - Build your self mobile proxies

This repository introduce information of XProxy device. Xproxy device can help you make 3G/4G proxies for MMO users who don't know much about mobile proxy setup or technical.

You can use any 3G/LTE dongles, Android phones on the world to makes proxies. It's easy, just plug dongles and proxies make automatically!


### Table of contents

  * [The list of dongles support by XProxy Device ](#the-list-of-dongles-support-by-xproxy-device)
  * [REST API document](#rest-api-document)
 
## The list of dongles support by XProxy Device
- All Huawei dongles support Hilink interface such as: E3372h, E3372s, E8372h, E303h, E353h, E3276, E3276s, E3272, E3131, E3531, E3351, E3251, E392, E398, E397, E8278, E323S, K5005, K5007, K5150, W5101
- All Huawei dongles support Stick mode with AT command: MS3372NA, E303s-1, E173, E3131, E367
- All ZTE dongles support Hilink interface such as: MF861, MF832G, MF831, MF833, MF832u, MF832s, MF827, MF826, MF79, MF75, MF820, MF820D, MF820T, MF820S2, MF880, MF821, MF821D, MF821S2, MF822, MF823, MF825, MF825C, MF831, MF170, MF730M, MF667
- All ZTE dongles support Stick mode such as: MF190, MF190S, MF820B, E173Eu-1
- Another stick model universal: Qualcomm MDM9K, D-link-156, Mobily, HSPA Data Card

## Rest API document

#### Get list devices and proxies information

<details>
 <summary><code>GET</code> <code><b>/v1/info_list</b></code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | page      |  optional | integer                 | A number of current page to fetch info                                |
> | limit     |  optional | integer                 | A number of items to get per page                                     |


##### Responses

<details>
  <summary>Click to expand</summary>
  
```javascript
{
  "status: True,
  "data": [
    {
      "position": 1,
      "host": "192.168.177.133",
      "proxy_port": 4201,
      "proxy_port_v6": 6201,
      "socks5_port": 5201,
      "socks5_port_ipv6": 7201,
      "public_ip": "171.255.118.95",
      "public_ip_ipv6": null,
      "last_rotation": null,
      "last_updated_ip": 1623331226.473283,
      "device_manufacture": "HW-Hilink",
      "device_imei": "866785034707108",
      "device_number": "11",
      "device_ip": "192.168.11.1",
      "device_rebooting": false,
      "device_resetting": false,
      "device_extra_info": {
        "rssi_info": "N/A",
        "name": "E3372",
        "serial": "Y4Q7S19510000205",
        "imei": "866785034707108",
        "imsi": "452040320937808",
        "wan": "undefined",
        "connected": true,
        "network_mode": "LTE_4G",
        "sim_live": true,
        "signal_strength": "5",
        "swver": "22.333.63.00.143",
        "hwver": "CL2E3372HM",
        "provider_id": "45204",
        "provider": "Viettel"
      }
    },
    {
      "position": 2,
      "host": "192.168.177.133",
      "proxy_port": 4202,
      "proxy_port_v6": 6202,
      "socks5_port": 5202,
      "socks5_port_ipv6": 7202,
      "public_ip": "103.199.70.155",
      "public_ip_ipv6": "2402:9d80:38a:dda0:c0e:ee4:933:907",
      "last_rotation": 1623330956.916284,
      "last_updated_ip": 1623331189.96525,
      "device_manufacture": "XProxy-Hilink",
      "device_imei": "869383054786694",
      "device_number": "1",
      "device_ip": "192.168.1.1",
      "device_rebooting": false,
      "device_resetting": false,
      "device_extra_info": {
        "connected": true,
        "sim_live": true,
        "signal_strength": 4,
        "network_mode": "4G",
        "name": "XH20",
        "rssi_info": 44,
        "imei": "869383054786694",
        "swver": "1.0",
        "hwver": "1.0",
        "imsi": "8984012002134231827f",
        "provider_id": "Mobifone",
        "provider": "Mobifone"
      }
    }
  ],
  "total": 2
}
```
</details>

##### Example cURL

```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/info_list
```

</details>

------------------------------------------------------------------------------------------

#### Rotation IP with specific proxy or position
 
<details>
<summary><code>GET</code> <code><b>/v1/rotation/proxy/<< proxy >></b></code> <code>[rotation IP with specific proxy]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                            |
> |-----------|-----------|-------------------------|----------------------------------------------------------------------------------------|
> | proxy     |  required | string                  | A proxy or socks in format <code>ip:port</code> to indicate the device to rotation IP  |

##### Responses

> | field      |   data type    |  description                                                                                              	  |
> |------------|----------------|--------------------------------------------------------------------------------------------------------------|
> | status     |   boolean      |  `True` if sent command successfully, `False` if another reason                                           	  |
> | msg        |   string       |  `slot_not_found` could not find the slot attached with the proxy                                            |
> |            |                |  `modem_disconnected` modem disconnected, could not rotation                                                 |
> |            |                |  `command_sent` sent successfully                                                                            | 

- Send rotation command successfully

```javascript
{
  "status": true,
  "msg": "command_sent"
}
```

- Another status  

```javascript
{
  "status": false,
  "msg": "modem_disconnected"
}
```

##### Example cURL

 > send a command to rotation IP of device for proxy <code>192.168.1.100:4001</code>
 
```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/rotation/192.168.1.100:4001
```

</details>


<details>
<summary><code>GET</code> <code><b>/v1/rotation/position/<< position >></b></code> <code>[rotation IP with specific position]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                                  |
> |-----------|-----------|-------------------------|----------------------------------------------------------------------------------------------|
> | position  |  required | number                  | A position number of modem in device list from 1 to N	to indicate the device to rotation IP 	|


##### Responses

Same as <i>rotation IP with specific proxy</i>

##### Example cURL

> send a command to rotation IP of modem in position 1
```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/rotation/1
```

</details>


------------------------------------------------------------------------------------------

#### Get status of proxy or position
 
<details>
<summary><code>GET</code> <code><b>/v1/status/proxy/<< proxy >></b></code> <code>[get status of specific proxy]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                           |
> |-----------|-----------|-------------------------|---------------------------------------------------------------------------------------|
> | proxy     |  required | string                  | A proxy or socks in format <code>ip:port</code> to indicate the device to get status  |

##### Responses

> | field      |   data type    |  description                                                                                              	  |
> |------------|----------------|-----------------------------------------------------------------------------------------------------------------|
> | status     |   boolean      |  `True` if modem ready, `False` if modem busy or offline                                                  	  |
> | msg        |   string       |  `MODEM_READY` when modem normally, `MODEM_NOT_FOUND` when not found modem attached to this position            |
> |            |                |  `MODEM_DISCONNECTED` when modem disconnected, `COLLISION_IP` when modem met collision IP with before rotation  | 

- Modem ready 

```javascript
{
  "status": true,
  "msg": "MODEM_READY"
}
```

- Another status  

```javascript
{
  "status": false,
  "msg": "MODEM_DISCONNECTED"
}
```

##### Example cURL

 > send a command to get status of device for proxy <code>192.168.1.100:4001</code>
 
```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/status/192.168.1.100:4001
```

</details>


<details>
<summary><code>GET</code> <code><b>/v1/status/position/<< position >></b></code> <code>[get status of specific position]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                           |
> |-----------|-----------|-------------------------|---------------------------------------------------------------------------------------|
> | position  |  required | number                  | A position number of modem in device list from 1 to N								    |


##### Responses

Same as <i>get status of specific proxy</i>

##### Example cURL

 > send a command to get status of device at position 1

```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/status/1
```

</details>


> Contact: http://xproxy.io
> Telegram: @phunguyen_hcmus
