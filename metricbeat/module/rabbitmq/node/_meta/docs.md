This is the `node` metricset of the RabbitMQ module and collects metrics about RabbitMQ nodes.

The metricset has two modes to collect data which can be selected with the `node.collect` setting:

* `node`: collects metrics only from the node `metricbeat` connects to. This is the default, as it is recommended to deploy `metricbeat` in all nodes.
* `cluster`: collects metrics from all the nodes in the cluster. This is recommended when collecting metrics of an only endpoint for the whole cluster.
