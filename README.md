# ansible role k3s

This Ansible role installs and configures [k3s](https://k3s.io/).

It downloads k3s binary from Github and installs it on the target host.
It also configures the k3s service to start on boot and provides
`/etc/rancher/k3s/k3s.yaml` config file for k3s

## How to configure

Provide some variables to the role: These are recommended



### Variables

| Variable                     | Example value                                                            | Description                                          |
|------------------------------|--------------------------------------------------------------------------|------------------------------------------------------|
| `k3s_is_apiserver`           | true                                                                     | Is this node a master node?                          | 
| `k3s_is_first_apiserver`     | true                                                                     | Is this node the very first one (required for etcd)? |
| `k3s_is_worker`              | false                                                                    | Is this node a worker node?                          | 
| `k3s_node_name`              | `{{ ansible_nodename }}` (eg. name from the inventory)                   | Name of the node in the cluter                       |
| `kube_local_storage_dir`     | `/storage/`                                                              | Directory where k3s stores PVC data                  |
| `kube_taint_apiserver_nodes` | `false`                                                                  | Should we enable taint on apiserver nodes            |
| `k3s_master_name`            | `k3s-master`                                                             | Name of the master node in the Ansible inventory     |
| `k3s_apiserver_server`       | `https://{{ hostvars[k3s_master_name].ansible_default_ipv4.address }}:6443/` | URL location of the k3s master                   |
| `kube_node_external_ip`      | `{{ ansible_default_ipv4.address }}`                                     |                                                      |
| `kube_node_ip`               | `{{ ansible_default_ipv4.address }}`                                     | Internal IP address of the node                      |
| `k3s_agent_token`            | `aiyeeviPh8phie3poo1Ahj1choopie8u`                                       | Token used to register agent nodes to the cluster    |
| `k3s_cluster_token`          | `7f22135bd875244c186a5d7d3c53499b`                                       | Token used to register cluster nodes to the cluster  |


Other variables can be found in `defaults/main.yml` file.

### Links:

* [k3s](https://k3s.io/)
* [issue document on k3s tokens](https://github.com/k3s-io/k3s/issues/6175)
* [FAQ on tokens](https://docs.k3s.io/faq#what-is-the-difference-between-k3s-server-and-agent-tokens)


### License

* BSD-2-Clause
