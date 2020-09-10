# Vagrant file to startup microk8s

This is an example vagrant file that uses ubuntu bionic to setup a two node microk8s cluster using the snap package.

Just a little fun science experiment in understanding vagrant syntax, and kubernetes.

## Requirements

virtualbox, and your very best positive mental attitude
Vagrant. This was tested on version 2.2.7. Your mileage may vary.

## Invocation

```bash
vagrant up --provision
```

Running this in the folder with the vagrant file

The output from vagrant up will include output from the 'k8s1' that you can paste into k8s to make a multi node cluster.

A major todo is to automate this process.

log into hosts with

```bash
vagrant ssh k8s1
```

or

```bash
vagrant ssh k8s2
```

## Configuration tips

This is setup using a virtualbox bridged network, defaulting to the 192.168.0.0/24 address space with static IPs. Change this to your own taste.

by default the VMs it creates have 4 gigabytes of ram, this may be a lot. Consider adjusting to your needs.
