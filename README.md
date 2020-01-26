# LabVIEW_adapter
This documentation describes the LabVIEW_adapter

# Infrastructure overview

A PV/ wind turbine/battery hybrid residential microgrid is emulated in AAU IoT-microgrid Lab. Two GORENJE smart appliances are included in the residential microgrid. The residential microgrid is assumed to supply power to EV chargers at three parking slots. Parking slot usage data, energy consumption data, operation status of the smart appliances, and room usage data are collected to the LabVIEW-based energy management system through VICINITY P2P network. The real-time charging price is calculated by considering the forecasts of the PV and wind turbine power generation, forecast of the load consumption, and state-of-charge of batteries. The parking slot usage, the real-time charging price, room usage date, microgrid operation status, abnormal situation alarm, and energy consumption abnormal alarm will be published to VICINITY Cloud. 
The adapter serves as the interface between VICINITY and the LabVIEW-based energy management system to enable the required interaction patterns. 

![Image text](https://github.com/YajuanGuan/pics/blob/master/EnergyConsumptionAbnormal.png)

# Configuration and deployment

Adapter runs on Python 3.6.

# Adapter changelog by version
Adapter releases are as aau_adapter_x.y.z.py

## 1.0.2
Start version, it works with agent-service-full-0.6.3.jar, and it subscribes to the event of GORENJE oven #7 device status and publishes an event with energy consumption abnormal notification. 

# Functionality and API
## User can read the energy consumption. 
### Endpoint:
            GET : /remote/device/{oid}/properties/{pid}
### Return:
After executing GET method, a response can be received, for instance:
properties/Load_ActivePower
{  
    "value": "5",  
    "time": "2018-11-10 11:30:29"  
}

## Publish an event to the subscribers. 
### Endpoint:
            PUT : /remote/objects/{oid}/events/{eid}
Publish the cleaning request and current time. 
### Return:
After subscribing the VAS successfully, the subscriber receives a response for instance:  
{  
    "state": "alarm",  
    "time": "2018-11-10 11:30:29"  
}

## Publish an event to the subscribers. 
### Endpoint:
            PUT : /remote/objects/{oid}/events/{eid}
Publish the vacant parking slot number, EV charging price and current time. Users can receive the number of free parking slot and charging price automatically.
### Return:
After subscribing the VAS successfully, the subscriber receives a response for instance:  
{  
    "value": "3.15",  
    "free": "2",  
    "time": "2018-11-10 11:30:29"  
}

## Publish an event to the subscribers. 
### Endpoint:
            PUT : /remote/objects/{oid}/events/{eid}
Publish the emergency alarm, the reserved parking slot number (0/1) and current time. 
### Return:
After subscribing the VAS successfully, the subscriber receives a response for instance:  
{  
    "state": "alarm",  
    "parking slot reserved": "1",  
    "time": "2018-11-10 11:30:29"  
}


## Publish an event to the subscribers. 
### Endpoint:
            PUT : /remote/objects/{oid}/events/{eid}
Publish the cleaning request and current time. 
### Return:
After subscribing the VAS successfully, the subscriber receives a response for instance:  
{  
    "clean": "required",  
    "time": "2018-11-10 11:30:29"  
}

## User can read the Active power consumption, power generation of wind turbine, power generation of PV, and the state of charge of batteries. 
### Endpoint:
            GET : /remote/objects/{oid}/properties/{pid}
### Return:
After executing GET method, a response can be received, for instance:  
properties/Load_ActivePower:  
{  
    "value": "1",  
    "time": "2018-11-10 11:30:29"  
}

properties/WT_ActivePower:  
{  
    "value": "2",  
    "time": "2018-11-10 11:30:29"  
}

properties/BMS_SoC:  
{  
    "value": "60%",  
    "time": "2018-11-10 11:30:29"  
}

properties/PV_ActivePower:  
{  
    "value": "3",  
    "time": "2018-11-10 11:30:29"  
}

## PUT GORENJE refrigerator property
### Endpoint:
            PUT : /remote/objects/{oid}/properties/{pid}
For PUT method request the following JSON is needed:  
{  
    "fastfreeze": "ON"  
}


## POST GORENJE oven baking parameters
### Endpoint:
            POST : /remote/objects/{oid}/actions/{aid}
For PUT method request the following JSON is needed:  
{  
"duration": "20",  
    "temperature": "150",  
    "heater_system": "hotair"  
}

## User can read the power generation of PV. 
### Endpoint:
            GET : /remote/objects/{oid}/properties/{pid}
### Return:
After executing GET method, a response can be received, for instance:
properties/PV_ActivePower:  
{  
    "value": "1",  
    "time": "2018-11-10 11:30:29"  
}

## Publish an event to the subscribers. 
### Endpoint:
            PUT : /remote/objects/{oid}/events/{eid}
Publish the with solar irradiance forecast for next 15 mins. 
### Return:
After subscribing the VAS successfully, the subscriber receives a response for instance:  
{  
    "value": "843",  
    "time": "2018-11-10 11:30:29"  
}

## Publish an event to the subscribers. 
### Endpoint:
              PUT : /remote/objects/{oid}/events/{eid}
Publish the vacant parking slot number, EV charging price and current time. Users can receive the number of free parking slot and charging price automatically.
### Return:
After subscribing the VAS successfully, the subscriber receives a response for instance:  
{  
    "value": "3.15",  
    "free": "2",  
    "time": "2018-11-10 11:30:29"  
}
