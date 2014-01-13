# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "precise64"
    config.vm.box_url = "http://files.vagrantup.com/precise64.box"

    config.vm.network :forwarded_port, guest: 80, host: 80
    config.vm.network :private_network, ip: "192.168.100.100"
    config.vm.network :public_network
    config.vm.hostname = "server"

    config.vm.synced_folder "~/Websites", "/home/vagrant/Websites", create: true, type: 'nfs'

    config.vm.provider :virtualbox do |vb|
        # Don't boot with headless mode
        vb.gui = false
        vb.name = "titomiguelcosta"

        # Use VBoxManage to customize the VM. For example to change memory and cpu cores:
        vb.customize ["modifyvm", :id, "--memory", "1024"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
    end

    config.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = ["cookbooks"]

        chef.add_recipe "apt"
        chef.add_recipe "build-essential"
        chef.add_recipe "sudo"
        chef.add_recipe "vim"
        chef.add_recipe "git"
        chef.add_recipe "apache2"
        chef.add_recipe "apache2::mod_php5"
        chef.add_recipe "apache2::mod_proxy"
        chef.add_recipe "apache2::mod_proxy_http"
        chef.add_recipe "ruby_build"
        chef.add_recipe "php" do 
            package "php5-memcache", "php5-curl", "php5-mysql", "php5-sqlite3", "php5-gd", "php5-xdebug" do 
                action :install 
            end
        end
        chef.add_recipe "composer"
        chef.add_recipe "nodejs"
        chef.add_recipe "nodejs::npm"
        chef.add_recipe "mysql::server"
        chef.add_recipe "memcached"
        chef.add_recipe "hosts"

        chef.json = { 
            "mysql" => {
                "server_root_password" => "",
                "server_repl_password" => "",
                "server_debian_password" => "",
                "bind_address" => "0.0.0.0"
            },
            "php" => {
                "directives" => {
                    "date.timezone" => "Europe/London"
                },
            },
            "php_apache" => {
                "directives" => {
                    "date.timezone" => "Europe/London",
                    "display_errors" => "On",
                    "html_errors" => "On"
                },
            },
            "hosts" => {
                "entries" => {
                    "127.0.0.1" => "localhost server dev",
                    "192.168.100.100" => "selenium.local local"
                }
            },
            "authorization" => {
                "sudo" => {
                    "passwordless" => true,
                    "agent_forwarding" => true,
                    "groups" => ["admin"]
                }
            }
        }
    end
end