MACHINES = {
  # VM name "nginx"
  :"nginx" => {
              # VM box
              :box_name => "centos/7",
              # VM CPU count
              :cpus => 2,
              # VM RAM size (Mb)
              :memory => 1024,

            }
}

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    # Disable shared folders
    config.vm.synced_folder ".", "/vagrant", disabled: true

    # Apply VM config
    config.vm.define boxname do |box|
      # Set VM base box and hostname
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxname.to_s
      # Additional network config if present
      box.vm.network "private_network", ip: "192.168.56.9"
      
      # VM resources config
      box.vm.provider "virtualbox" do |v|
        # Set VM RAM size and CPU count
        v.memory = boxconfig[:memory]
        v.cpus = boxconfig[:cpus]
      end
    end
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "play-nginx.yaml"
  end
end