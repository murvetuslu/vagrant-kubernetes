# -*- mode: ruby -*-
# vi: set ft=ruby :

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

# This script to install microk8s  after a box is provisioned
$microk8sScript = <<-SCRIPT
    apt-get update
    apt-get -y install apt-transport-https
    apt-get install -y snapd 
    snap install microk8s --classic --channel=1.13/stable
    microk8s.status --wait-ready
    ufw allow in on cbr0
    ufw allow out on cbr0
    ufw default allow routed
    # microk8s.enable dashboard
    microk8s.enable dns
    # microk8s.enable fluentd
    microk8s.enable ingress
    # echo N | microk8s.enable istio
    # microk8s.enable jaeger
    # microk8s.enable metrics-server
    # microk8s.enable prometheus
    microk8s.enable registry
    microk8s.enable storage

    #microk8s.kubectl config view --raw > /vagrant/.kube-config

    snap alias microk8s.docker docker
    snap alias microk8s.istioctl istioctl
    snap alias microk8s.kubectl kubectl
SCRIPT

$mysqlScript = <<-SCRIPT
    kubectl apply -f /vagrant/Mysql/mysql-deployment.yaml
    kubectl apply -f /vagrant/Mysql/mysql-services.yaml
SCRIPT


Vagrant.configure("2") do |config|

    servers.each do |opts|
        config.vm.define opts[:name] do |config|

            config.vm.box = opts[:box]
            config.vm.box_version = opts[:box_version]

            config.vm.provider "virtualbox" do |v|
                v.gui = true
                v.name = opts[:name]
                v.customize ["controlvm", :id,"setlinkstate1", "on",]
                v.customize ["modifyvm", :id, "--memory", opts[:mem]]
                v.customize ["modifyvm", :id, "--cpus", opts[:cpu]]

            end

            config.vm.provision "shell", inline: $microk8sScript
            config.vm.provision "shell", inline: $mysqlScript

        end

    end

end 
