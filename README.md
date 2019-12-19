**NOTE:** We are not currently accepting pull requests to this library. An announcement will be made once the functionality is ready.

# About this Library

This library is intended to be used for populating device types in [NetBox](https://github.com/netbox-community/netbox). It contains a set of device type definitions expressed in YAML and arranged by manufacturer. Each file represents a discrete physical device type (e.g. make and model). These definitions can be loaded into NetBox to obviate the need to create device types and their associated components manually.

# Guidelines for Defining Device Types

* Every unique model number requires a discrete definition file, even if the set of components is identical.
* Include only components which are fixed to the chassis. Optional modular components should be omitted from the definition.
* Name components as they appear in the device's operating system (as opposed to the physical chassis label, if different).
* Avoid encapulating YAML values in quotes unless necessary to avoid a syntax error.

# Device Type Definitions

Each definition must include at minimum the following fields:

* `manufacturer`: The name of the manufacturer which produces this device type.
* `model`: The model number of the device type. This must be unique per manufacturer.
* `slug`: A URL-friendly representation of the model number. Like the model number, this must be unique per manufacturer.

The following fields may optionally be declared:

* `part_number`: An alternative representation of the model number (e.g. a SKU).
* `u_height`: The height of the device type in rack units. (Default: 1)
* `is_full_depth`: A boolean which indicates whether the device type consumes both the front and rear rack faces. (Default: true)
* `subdevice_role`: Indicicates that this is a `parent` or `child` device. (Default: None)

## Component Definitions

Valid component types are listed below. Each type of component must declare a list of the individual component templates to be added.

* `console-ports`
* `console-server-ports`
* `power-ports`
* `power-outlets`
* `interfaces`
* `rear-ports`
* `front-ports`
* `device-bays`

The available fields for each type of component are listed below.

### Console Ports

* `name`: Port name
* `type`: Port type

### Console Server Ports

* `name`: Port name
* `type`: Port type

### Power Ports

* `name`: Port name
* `type`: Port type
* `maximum_draw`: The port's maximum power draw, in watts (optional)
* `allocated_draw`: The port's allocated power draw, in watts (optional)

### Power Outlets

* `name`: Outlet name
* `type`: Port type
* `power_port`: The name of the power port on the device which powers this outlet (optional)
* `feed_leg`: The phase (leg) of power to which this outlet is mapped (optional)

### Interfaces

* `name`: Interface name
* `type`: Inteface type
* `mgmt_only`: A boolean which indicates whether this interface is used for management purposes only (default: false)

### Front Ports

* `name`: Port name
* `type`: Port type
* `rear_port`: The name of the rear port on this device to which the front port maps
* `rear_port_position`: The corresponding position on the mapped rear port (default: 1)

### Rear Ports

* `name`: Port name
* `type`: Port type
* `positions`: The number of front ports that can map to this rear port (default: 1)

### Device Bays

* `name`: Bay name
