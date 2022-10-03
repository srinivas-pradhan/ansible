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
  config.vm.define "kube1" do |kube1|
    kube1.vm.hostname = "kube1"
    kube1.vm.provider "qemu" do |qe|
      qe.ssh_port = 20022
    end
    kube1.vm.provision "ansible_local" do |ansible|
  	  ansible.playbook = playbook
      ansible.provisioning_path = "/ansible"
      ansible.extra_vars = extra_vars
    end
  end
  config.vm.define "kube2" do |kube2|
    kube2.vm.hostname = "kube2"
    kube2.vm.provider "qemu" do |qe|
      qe.ssh_port = 20023
      qe.hostname = "kube2"
    end
    kube2.vm.provision "ansible_local" do |ansible|
  	  ansible.playbook = playbook
      ansible.provisioning_path = "/ansible"
      ansible.extra_vars = extra_vars
    end
  end
  config.vm.define "kube3" do |kube3|
    kube3.vm.hostname = "kube3"
    kube3.vm.provider "qemu" do |qe|
      qe.ssh_port = 20024
      qe.hostname = "kube1"
    end
    kube3.vm.provision "ansible_local" do |ansible|
  	  ansible.playbook = playbook
      ansible.provisioning_path = "/ansible"
      ansible.extra_vars = extra_vars
    end
  end
end


