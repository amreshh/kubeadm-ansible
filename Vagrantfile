# vagrant plugin install vagrant-libvirt vagrant-env vagrant-registration

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'
VAGRANTFILE_API_VERSION = "2"
VAGRANTFILE_VM_BOX = "generic/rhel8"

$provision = <<SCRIPT
  systemctl stop firewalld.service
  systemctl disable firewalld.service
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # control plane
  config.vm.define 'control' do |control|
    control.ssh.insert_key = false
    control.vm.box = VAGRANTFILE_VM_BOX
    control.registration.username = ENV["RHEL_USERNAME"]
    control.registration.password = ENV["RHEL_PASSWORD"]
    control.registration.unregister_on_halt = false
    control.vm.hostname = 'control'
    control.vm.network "private_network", ip: "10.1.1.10"
    control.vm.provider :libvirt do |libvirt|
      libvirt.driver = "kvm"
      libvirt.memory = 8192
      libvirt.cpus = 2
    end
    control.vm.provision "shell", inline: $provision
  end

  # worker node
  config.vm.define 'worker1' do |worker1|
    worker1.ssh.insert_key = false
    worker1.vm.box = VAGRANTFILE_VM_BOX
    worker1.registration.username = ENV["RHEL_USERNAME"]
    worker1.registration.password = ENV["RHEL_PASSWORD"]
    worker1.registration.unregister_on_halt = false
    worker1.vm.hostname = 'worker1'
    worker1.vm.network "private_network", ip: "10.1.1.20"
    worker1.vm.provider :libvirt do |libvirt|
      libvirt.driver = "kvm"
      libvirt.memory = 8192
      libvirt.cpus = 2
    end
    worker1.vm.provision "shell", inline: $provision
  end

end
