require 'vagrant-aws'
# https://github.com/mitchellh/vagrant-aws/issues/566#issuecomment-580812210
class Hash
    def slice(*keep_keys)
      h = {}
      keep_keys.each { |key| h[key] = fetch(key) if has_key?(key) }
      h
    end unless Hash.method_defined?(:slice)
    def except(*less_keys)
      slice(*keys - less_keys)
    end unless Hash.method_defined?(:except)
  end

$script = <<-'SCRIPT'
sudo amazon-linux-extras install ansible2 -y
SCRIPT

playbook = ENV['PLAYBOOK'] || "playbook.yml"
extra_vars = ENV['EXTRA_VARS'] || "default-vars.yml"

Vagrant.configure('2') do |config|
    config.vm.synced_folder ".", "/ansible", type: "rsync"
    config.vm.synced_folder '.', '/vagrant', disabled: true
    config.vm.box = 'dummy'
    config.vm.provision "shell", inline: $script
    config.vm.provider 'aws' do |aws, override|
    aws_profile = ENV['AWS_PROFILE']
    aws.keypair_name = ENV['KEY_PAIR_NAME']
    aws.instance_type = 't2.micro'
    aws.region = ENV['REGION']
    aws.ami = ENV['AMI']
    aws.security_groups = ENV['SG_ID']
    aws.subnet_id = ENV['SUBNET_ID']
    override.ssh.username = 'ec2-user'
    override.ssh.private_key_path = ENV['PRIVATE_KEY_PATH']
  end
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = playbook
    ansible.provisioning_path = "/ansible"
    ansible.extra_vars = "@" + extra_vars
  end
end
