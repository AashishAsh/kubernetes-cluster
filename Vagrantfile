Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"

#The primary machine will be the default machine used when a specific machine in a multi-machine environment is not specified.
#https://www.vagrantup.com/docs/multi-machine#specifying-a-primary-machine

  config.vm.define "master", primary: true do |master|
    master.vm.hostname="KubMaster"
    master.vm.network "private_network", ip: "192.168.33.10"
    master.vm.provider "virtualbox" do |master|
      master.name = "KubMaster"
    end
  end

  (1..2).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.hostname="KubeNode#{i}"
      node.vm.network "private_network", ip: "192.168.33.1#{i}"
      node.vm.provider "virtualbox" do |node|
        node.name = "KubeNode#{i}"
      end
    end
  end
end
