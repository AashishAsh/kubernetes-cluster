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
    master.vm.provision "shell", inline: <<-SHELL
      #Installation of Docker
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
      sudo add-apt-repository \
         "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
         $(lsb_release -cs) \
         stable"
      sudo apt-get update
      sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu
      sudo apt-mark hold docker-ce
      echo "Successfully installed Docker"
      #Installation of Kubernetes 
      curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
      echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
      sudo apt-get update
      sudo apt-get install -y kubelet=1.15.7-00 kubeadm=1.15.7-00 kubectl=1.15.7-00
      sudo apt-mark hold kubelet kubeadm kubectl
      echo "Successfully installed kubeadm"
    SHELL
  end
  (1..2).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.hostname="KubeNode#{i}"
      node.vm.network "private_network", ip: "192.168.33.1#{i}"
      node.vm.provider "virtualbox" do |node|
        node.name = "KubeNode#{i}"
      end
      node.vm.provision "shell", inline: <<-SHELL
        #Installation of Docker
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
        sudo add-apt-repository \
           "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
           $(lsb_release -cs) \
           stable"
        sudo apt-get update
        sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu
        sudo apt-mark hold docker-ce
        echo "Successfully installed Docker"
        #Installation of Kubernetes
        curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
        echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
        sudo apt-get update
        sudo apt-get install -y kubelet=1.15.7-00 kubeadm=1.15.7-00 kubectl=1.15.7-00
        sudo apt-mark hold kubelet kubeadm kubectl
        echo "Successfully installed kubeadm"
      SHELL
    end
  end

end
