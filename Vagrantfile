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
      #############################################################################################  
      #Remember to change the bridged network adapter to the one that is appropriate for your lan!
      #This is the network adapter as it is labeled in virtualbox
      #############################################################################################    
      bridge: "en1: Wi-Fi (Wireless)", 
      ############################################################################
      #Remember to change the IP address to one that is appropriate for your lan!
      ############################################################################
      ip: "192.168.0.242"
    ###################################################################################################################
    #Below this comment, scripts are run every time, until the next comment block. Controlled by the run: "always" arg
    ################################################################################################################### 
    k8s1.vm.provision "net1k8s1", type: "shell",
      run: "always",
      inline: "route add default gw 192.168.0.1"
      k8s1.vm.provision "net2k8s1", type: "shell",
      run: "always",
      inline: "eval `route -n | awk '{ if ($8 ==\"enp0s3\" && $2 != \"0.0.0.0\") print \"route del default gw \" $2; }'`"
    ##############################################################
    #Below this comment, scripts are only run at provisioning time
    ##############################################################
    k8s1.vm.provision "aptgetupdatek8s1", after: "net2k8s1", type:"shell",
    inline: "apt-get update"
    k8s1.vm.provision "k8s1install", after: "aptgetupdatek8s1", type:"shell",
      inline: "sudo snap install microk8s --classic"
    k8s1.vm.provision "dashboard", after: "kus1install", type: "shell",
      inline: "microk8s enable dashboard"
    ##############################  
    #Copy paste the output to k8s2
    ##############################  
    k8s1.vm.provision "addnode", after: "dashboard", type:"shell",
      inline: "microk8s add-node"  
    #Done
    k8s1.vm.post_up_message = "k8s1 is up"
    k8s1.vm.post_up_message = "you may take the ouput from microk8s add-node above and paste it into k8s2 with sudo"
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
    #############################################################################################  
    #Remember to change the bridged network adapter to the one that is appropriate for your lan!
    #This is the network adapter as it is labeled in virtualbox
    #############################################################################################    
    bridge: "en1: Wi-Fi (Wireless)", 
    ############################################################################
    #Remember to change the IP address to one that is appropriate for your lan!
    ############################################################################
      ip: "192.168.0.243"
    ###################################################################################################################
    #Below this comment, scripts are run every time, until the next comment block. Controlled by the run: "always" arg
    ################################################################################################################### 
    k8s2.vm.provision "net1k8s2", type: "shell",
      run: "always",
      inline: "route add default gw 192.168.0.1"
    k8s2.vm.provision "net2k8s2", type: "shell",
      run: "always",
      inline: "eval `route -n | awk '{ if ($8 ==\"enp0s3\" && $2 != \"0.0.0.0\") print \"route del default gw \" $2; }'`"
    ##############################################################
    #Below this comment, scripts are only run at provisioning time
    ##############################################################
    k8s2.vm.provision "aptgetupdatek8s2", after: "net2k8s2", type:"shell",
    inline: "apt-get update"
    k8s2.vm.provision "shell",
      inline: "sudo snap install microk8s --classic"
    #####    
    #Done
    ##### 
    k8s2.vm.post_up_message = "k8s2 is up"
  end





end

