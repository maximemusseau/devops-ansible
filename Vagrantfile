Vagrant.configure("2") do |config|
  config.vm.provision "ansible-user", type: "shell" do |cmd|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    cmd.inline = <<-SHELL
      useradd -m devops -G sudo
      echo -e "devops\ndevops" | sudo passwd devops
      mkdir /home/devops/.ssh
      chmod 700 /home/devops/.ssh
      echo #{ssh_pub_key} >> /home/devops/.ssh/authorized_keys
      chmod 600 /home/devops/.ssh/authorized_keys
      chown -R devops.devops /home/devops/.ssh
      apt-get install python -q -y
    SHELL
  end

  config.vm.define "wordpress" do |web|
    web.vm.box = "generic/ubuntu1804"
    web.vm.network "private_network", ip: "192.168.56.50"
    web.vm.hostname = "wordpress"

    web.vm.provider "virtualbox" do |v|
        v.memory = "4096"
    end
  end

  config.vm.define "maria" do |maria|
    maria.vm.box = "generic/ubuntu1804"
    maria.vm.network "private_network", ip: "192.168.56.51"
    maria.vm.hostname = "maria"

    maria.vm.provider "virtualbox" do |v|
        v.memory = "4096"
    end
  end
end
