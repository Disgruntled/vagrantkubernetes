Vagrant.configure("2") do |config|

  config.vm.define "k8s1" do |k8s1|
    k8s1.vm.box = "ubuntu/bionic64"
    k8s1.vm.box_check_update = true
    k8s1.vm.hostname = "k8s1"
    k8s1.vm.provider "virtualbox" do |v|
      v.name = "k8s1"
      v.memory = 4096
    end
    k8s1.vm.network "public_network", 
      bridge: "en0: Ethernet", 
      ip: "192.168.0.242"
      #Remember to change the IP addresses!
    k8s1.vm.provision "shell",
      run: "always",
      inline: "route add default gw 192.168.0.1"
    k8s1.vm.provision "shell",
      run: "always",
      inline: "eval `route -n | awk '{ if ($8 ==\"eth0\" && $2 != \"0.0.0.0\") print \"route del default gw \" $2; }'`"
    #
    #Below this comment, scripts are only run at provisioning time
    # 
    k8s1.vm.provision "shell",
      inline: "sudo snap install microk8s --classic"
    k8s1.vm.provision "shell",
      inline: "microk8s enable dashboard"
    #Copy paste the output to k8s2  
    k8s1.vm.provision "shell",
      inline: "microk8s add-node"  
    #Done
    k8s1.vm.post_up_message = "k8s1 is up"
    k8s1.vm.post_up_message = "you may take the ouput from microk8s add-node above and paste it into k8s2"
  end

  config.vm.define "k8s2" do |k8s2|
    k8s2.vm.box = "ubuntu/bionic64"
    k8s2.vm.box_check_update = true
    k8s2.vm.hostname = "k8s2"
    k8s2.vm.provider "virtualbox" do |v|
      v.name = "k8s2"
      v.memory = 4096
    end
    k8s2.vm.network "public_network", 
      bridge: "en0: Ethernet", 
      ip: "192.168.0.243"
      #Remember to change the IP addresses!
    #
    #Run "always" always run
    #  
    k8s2.vm.provision "shell",
      run: "always",
      inline: "route add default gw 192.168.0.1"
    k8s2.vm.provision "shell",
      run: "always",
      inline: "eval `route -n | awk '{ if ($8 ==\"eth0\" && $2 != \"0.0.0.0\") print \"route del default gw \" $2; }'`"
    #
    #Below this comment, scripts are only run at provisioning time
    # 
    k8s2.vm.provision "shell",
      inline: "sudo snap install microk8s --classic"  
    #Done 
    k8s2.vm.post_up_message = "k8s2 is up"
  end





end

