# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_check_update = true

  config.vm.provision "shell" do |shell|
    shell.inline = [
      "apt-get -qq update",
      "apt-get -qq install python3 python3-pip",
      "pip3 install -q ansible"
    ].join("\n")
    shell.privileged = true
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.become = true
    ansible.extra_vars = {
      ansible_python_interpreter: "/usr/bin/python3"
    }
    ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
    ansible.galaxy_role_file = "requirements.yaml"
    ansible.galaxy_roles_path = "/etc/ansible/roles"
    ansible.playbook = "playbook.yaml"
  end
end
