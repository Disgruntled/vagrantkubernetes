# Vagrant file to startup microk8s

This is an example vagrant file that uses ubuntu bionic to setup a two node microk8s cluster using the snap package.

Just a little fun science experiment in understanding vagrant syntax, and kubernetes.

## Requirements

virtualbox, and your very best positive mental attitude
Vagrant. This was tested on version 2.2.7. Your mileage may vary.

## Invocation

On the first run:

```bash
vagrant up --provision
```

On all subsequent:

```bash
vagrant up
```

Running this in the folder with the vagrant file

The output from vagrant up --provision will include output from the 'k8s1' that you can paste into k82s to make a multi node cluster. (sudo microk8s join yourip:25000/yourkey)

A major todo is to automate this process.

log into hosts with

```bash
vagrant ssh k8s1
```

or

```bash
vagrant ssh k8s2
```

## Configuration tips and troubleshooting

This is setup using a virtualbox bridged network, defaulting to the 192.168.0.0/24 address space with static IPs. Change this to your own taste.

By default the VMs it creates have 4 gigabytes of ram, this may be a lot. Consider adjusting to your needs.

If your host PC has multiple nics, virtual box may be bridging the wrong one. Make sure the bridged NIC is set correctly and has a route to the internet. This may need to be set for both VMs.
This is done in the "bridge:" arguments in the vagrantfile

the interface names in the VM's are inconsistent. I have observed 'enp0s3','enp0s8', as well as eth0/eth1. This currently breaks the routing login in the vagrant file.
You may need to modify the vagrant file yourself (line beginning inline: eval) to make it search and destroy the approriate default route. replace enp0s3 with the route entry you want to delete
