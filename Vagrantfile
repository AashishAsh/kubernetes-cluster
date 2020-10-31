Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"

  config.vm.define "master", primary: true do |master|
    master.vm.hostname="KubMaster"
    master.vm.network "private_network", ip: "192.168.33.10"
  end

  (1..3).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.hostname="KubeNode#{i}"
      node.vm.network "private_network", ip: "192.168.33.1#{i}"
    end
  end

end
