# Avoid Public Wifi Proxy Time Limits via Changing MAC Address

I'm working out of a public library in Katoomba, Australia at the moment and they have a crazy policy of enacting a 2 hour limit on your wifi usage. Not cool, but I guess they don't want people hogging up library space all day? Understandable, but I figured I could get around this limitation. Enter the following script with changes the MAC Address of the specified network interface (`en0` in the example).

```shell
$ new_mac_addr=`openssl rand -hex 6 | sed 's/\(..\)/\1:/g; s/.$//'` # Generate new Address
$ echo $new_mac_addr # Print it out so we can confirm after the fact.
$ sudo ifconfig en0 ether $new_mac_addr # Change the MAC Address for en0 device
$ sudo ifconfig en0 ether # Print out new en0 device's MAC Address. This should match the echo'd address.
```
