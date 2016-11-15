# Adding Aerospike Nodes without Downtime

Not the clearest way to add a node, but with mesh configuration you can send a signal to inform Aerospike that it should recognize a new node. This looks like the following:

`asinfo -v "tip:host=[new host IP];port=[Mesh port];"`

More info on the `tip` command and remote configuration management in general [here](http://www.aerospike.com/docs/operations/troubleshoot/dynamic_config).
