# Generic Attribute Service #

## Definitions ##

### Attribute ###
An attribute is an addressable, typed value, similar to a variable in programming, except that the types are more rich.  An example is: 0x003, `<<Device Name>>`, "Proximity Tag".  The handle (address) is a 2-byte short, the type is a 2-byte UUID prefix, if the type is well known, or a full, 16-byte UUID, if the type is a vendor-defined type.  The value is 0 to 512 bytes.

### Characteristic ###
A characteristic is a type of attribute that stores the metadata about a target attribute.  Since it is an attribute, it has: 
* a 2-byte handle
* a 2-byte type, `<<Charateristic>>`
* and a specifically formatted value:
  *  The properties of the charateristic, which is a 8-bit? field corresponding to whether the target attribute can be read, written, notified, indicated, broadcast, commanded or authenticated, and if there are extended properties.
  *  The 2-byte handle to the target attribute.  The current design is that the target attribute is slotted right under the characteristic, so its hande should be the address of the charateristic handle, plus one.
  *  The attribute type of the target charateristic, which is a duplicate of the type field for the target attribute.
  * Additionally, there might be extended properties, a user description string, and other stuff, including a broadcast bit in the Server Charateristic Configuration Descriptor.  This bit indicates to the service that it this characteristic is grouped under that the characteristic would like to be broadcast.  How/if this happens is up to the service whose group the characteristic is in.

### Service ###
A service is an attribute that begins a block of associated attributes.  It may be followed immediately by one or more include attributes, to include other services, and then followed by characteristics and other attribute types.  A service block ends when another service is declared.  The attribute itself has:
* A 2-byte handle
* A 2-byte type, either `<<Primary Service>` or `<<Secondary Service>>`
* A 2-byte UUID prefix or 16-byte vendor UUID

