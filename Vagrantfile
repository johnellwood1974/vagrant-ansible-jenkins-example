Vagrant.require_version ">= 1.7.0"
Vagrant.configure(2) do |config|
  servers = { 'web1'    => '192.168.10.2',
              'jenkins' => '192.168.100.2'
            }
  http_port = { 'web1' => 8012 }
  tomcat_port = { 'jenkins' => 8080 }

  servers.each do |server_name, server_ip|
    config.vm.define server_name do |app_config|
      app_config.vm.hostname = "#{server_name.to_s}"
      if http_port[server_name]
        app_config.vm.network :forwarded_port, guest: 80, host: http_port[server_name], auto_correct: true
      end
      if tomcat_port[server_name]
        app_config.vm.network :forwarded_port, guest: 8080, host: tomcat_port[server_name], auto_correct: true
      end
      app_config.vm.network :private_network, ip: "#{server_ip}"
      # virtualbox
      app_config.vm.provider :virtualbox do |v, override|
         override.vm.box = "ubuntu/trusty64"
         v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
         # save storage
         v.linked_clone = true if Vagrant::VERSION =~ /^1.8/
      end
      config.ssh.insert_key = false
      config.vm.provision "ansible" do |ansible|
        ansible.groups = {
          "webservers" => ["web1"],
#          "dbservers"  => ["db1"],
          "jenkinsservers"  => ["jenkins"]
        }
        ansible.verbose = "v"
        ansible.playbook = "playbook.yml"
      end
      config.vm.synced_folder "website_content/", "/var/tmp/website_content"
    end
  end
end
