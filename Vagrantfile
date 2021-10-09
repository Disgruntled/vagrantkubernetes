Vagrant.configure("2") do |config|

  config.vm.define "k8s1" do |k8s1|
    k8s1.vm.box = "ubuntu/focal64"
    k8s1.vm.box_check_update = true
    k8s1.vm.hostname = "k8s1"
    k8s1.vm.provider "virtualbox" do |v|
      v.name = "k8s1"
      v.cpus = "3"
      v.memory = 6144
    end
    k8s1.vm.network "public_network",
      #############################################################################################  
      #Remember to change the bridged network adapter to the one that is appropriate for your lan!
      #This is the network adapter as it is labeled in virtualbox
      #############################################################################################    
      bridge: "wlp8s0", 
      ############################################################################
      #Remember to change the IP address to one that is appropriate for your lan!
      ############################################################################
      ip: "192.168.0.242"
    ###################################################################################################################
    #Below this comment, scripts are run every time, until the next comment block. Controlled by the run: "always" arg
    ################################################################################################################### 
    k8s1.vm.provision "net1k8s1", type: "shell",
      run: "always",
      inline: "ip route add default via 192.168.0.1"
    ##############################################################
    #Below this comment, scripts are only run at provisioning time
    ##############################################################
    k8s1.vm.provision "aptgetupdatek8s1", after: "net2k8s1", type:"shell",
    inline: "sudo apt update -y && sudo apt upgrade -y"
    #####################################################    
    #Done. below this Comment is just output
    #####################################################
    k8s1.vm.post_up_message = "k8s1 is up"
  end

  config.vm.define "k8s2" do |k8s2|
    k8s2.vm.box = "ubuntu/focal64"
    k8s2.vm.box_check_update = true
    k8s2.vm.hostname = "k8s2"
    k8s2.vm.provider "virtualbox" do |v|
      v.name = "k8s2"
      v.memory = 6144
      v.cpus = "3"
    end
    k8s2.vm.network "public_network", 
    #############################################################################################  
    #Remember to change the bridged network adapter to the one that is appropriate for your lan!
    #This is the network adapter as it is labeled in virtualbox
    #############################################################################################    
    bridge: "wlp8s0", 
    ############################################################################
    #Remember to change the IP address to one that is appropriate for your lan!
    ############################################################################
      ip: "192.168.0.243"
    ###################################################################################################################
    #Below this comment, scripts are run every time, until the next comment block. Controlled by the run: "always" arg
    ################################################################################################################### 
    #in the new iproute system this should always take precedent over the DHCP set default route (which seems to have metric 100. YMMV.)
    k8s2.vm.provision "net1k8s2", type: "shell",
      run: "always",
      inline: "ip route add default via 192.168.0.1"
    ##############################################################
    #Below this comment, scripts are only run at provisioning time
    ##############################################################
    #in the new iproute system this should always take precedent over the DHCP set default route (which seems to have metric 100. YMMV.)
    k8s2.vm.provision "aptgetupdatek8s2", after: "net2k8s1", type:"shell",
    inline: "sudo apt update -y && sudo apt upgrade -y"
    ##############################################################
    #Done. below this Comment is just output
    ##############################################################
    k8s2.vm.post_up_message = "k8s2 is up"
  end

  config.vm.define "k8s3" do |k8s3|
    k8s3.vm.box = "ubuntu/focal64"
    k8s3.vm.box_check_update = true
    k8s3.vm.hostname = "k8s3"
    k8s3.vm.provider "virtualbox" do |v|
      v.name = "k8s3"
      v.memory = 6144
      v.cpus = "3"
    end
    k8s3.vm.network "public_network", 
    #############################################################################################  
    #Remember to change the bridged network adapter to the one that is appropriate for your lan!
    #This is the network adapter as it is labeled in virtualbox
    #############################################################################################    
    bridge: "wlp8s0", 
    ############################################################################
    #Remember to change the IP address to one that is appropriate for your lan!
    ############################################################################
      ip: "192.168.0.244"
    ###################################################################################################################
    #Below this comment, scripts are run every time, until the next comment block. Controlled by the run: "always" arg
    ###################################################################################################################
    #in the new iproute system this should always take precedent over the DHCP set default route (which seems to have metric 100. YMMV.) 
    k8s3.vm.provision "net1k8s3", type: "shell",
      run: "always",
      inline: "ip route add default via 192.168.0.1"
    ##############################################################
    #Below this comment, scripts are only run at provisioning time
    ##############################################################
    k8s3.vm.provision "aptgetupdatek8s3", after: "net2k8s3", type:"shell",
    inline: "sudo apt update -y && sudo apt upgrade -y"
    ##############################################################
    #Done. below this Comment is just output
    ##############################################################
    k8s3.vm.post_up_message = "k8s3 is up"
  end



end

