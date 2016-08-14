
Vagrant.configure(2) do |config|

  config.vm.box = "nrel/CentOS-6.6-x86_64"

  config.vm.network "private_network", ip: "192.168.33.44"
  config.vm.synced_folder ".", "/vagrant", mount_options: ['dmode=777','fmode=777']

#  if Vagrant.has_plugin?("vagrant-hostsupdater")
#    config.hostsupdater.aliases = ["admin.tixeebox.tv", "api.tixeebox.tv"]
#   end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "2048"]
    v.customize ["modifyvm", :id, "--cpus", "2"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  if ARGV[0] == 'up'
    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "site.yml"
    end
  end

end
