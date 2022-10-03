$script = <<-'SCRIPT'
echo "Install ansible on guest machines."
sudo yum install epel-release -y
sudo yum install ansible-2.8.5-1.el7 -y
SCRIPT

playbook = ENV['PLAYBOOK'] || "playbook.yml"
extra_vars = ENV['EXTRA_VARS'] || "default-vars.yml"

Vagrant.configure(2) do |config|
  config.vm.synced_folder ".", "/ansible", type: "rsync"
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.vm.box = "ppggff/centos-7-aarch64-2009-4K"
  config.vm.provision "shell", inline: $script
  config.vm.define "host1" do |host1|
    host1.vm.hostname = "host1"
    host1.vm.provider "qemu" do |qe|
      qe.ssh_port = 20022
    end
    host1.vm.provision "ansible_local" do |ansible|
  	  ansible.playbook = playbook
      ansible.provisioning_path = "/ansible"
      ansible.extra_vars = extra_vars
    end
  end
  config.vm.define "host2" do |host2|
    host2.vm.hostname = "host2"
    host2.vm.provider "qemu" do |qe|
      qe.ssh_port = 20023
      qe.hostname = "kube2"
    end
    host2.vm.provision "ansible_local" do |ansible|
  	  ansible.playbook = playbook
      ansible.provisioning_path = "/ansible"
      ansible.extra_vars = extra_vars
    end
  end
  config.vm.define "host3" do |host3|
    host3.vm.hostname = "kube3"
    host3.vm.provider "qemu" do |qe|
      qe.ssh_port = 20024
      qe.hostname = "kube1"
    end
    host3.vm.provision "ansible_local" do |ansible|
  	  ansible.playbook = playbook
      ansible.provisioning_path = "/ansible"
      ansible.extra_vars = extra_vars
    end
  end
end


