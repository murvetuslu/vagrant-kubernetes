# Microk8s cluster
A vagrant script for setting up a cluster using Microk8s

## Pre-requisites

 * **[Vagrant 1.7.0+](https://www.vagrantup.com)**
 * **[Virtualbox 4.3.36+](https://www.virtualbox.org)**

## How to Run

Execute the following vagrant command to start a microk8s cluster, this will deployment the python application and python app will connect to mysql database.

```
vagrant up
```

You can edit the server array in the Vagrantfile

```
servers = [
    {
        :name => "microk8s",
        :type => "test",
        :box => "geerlingguy/ubuntu1604",
        :box_version => "1.3.0",
        :mem => "2048",
        :cpu => "2"
    }
]
```

As you can see above, you can also configure Machine name, memory and CPU in the servers array. 

## How to deploy changes on application (requirement for push command : vagrant v1.7.0+)


```
vagrant push
```

You can see also changes after on following command or request the this url(http://127.0.0.1:3000) on browser.

```
curl http://127.0.0.1:3000
```


## Clean-up

Execute the following command to remove the virtual machines created for the Microk8s.
```
vagrant destroy -f
```

You can destroy individual machines by vagrant destroy microk8s -f



