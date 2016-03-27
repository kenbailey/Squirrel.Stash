#Computer Profile
The Computer Profile is used to determine uniqueness and help track registered users. 
The intent is not to be a complete DRM system, rather a mechanism to encourage registration.
As the developer you have the ability to specify the amount of change allowed for a given
Install Token befoer another registration is needed.

## Key Components
The following types of computer information is retrieved and then the hashed value is then
provided to the server for registration and verification purposes as part of the Computer Profile.

* Machine Name
* Manufacturer (system manufacturer & model)
* OS (OS Name & Version)
* CPU 
* Memory (physical capacity)
* Drive (capacity, manufacturer, etc.)
* Network (MAC Addresses with enabled addresses)

## Hashing
Hashing is done to avoid collecting user system information while still identifying key aspects
of the computer system. The hashing is done in logical groups to avoid a single hash change causing
a re-registration.

You can specify the weight for each of the key components above and a minimum threshold before
re-registration is required.
