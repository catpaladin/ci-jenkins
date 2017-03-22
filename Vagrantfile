Vagrant.configure('2') do |config|
    config.vm.hostname = 'ci-jenkins'

    # Create droplet
    config.vm.provider :digital_ocean do |provider, override|
    # Path to private SSH key
    override.ssh.private_key_path = ENV['PRIVATE_KEY_PATH']
    override.vm.box = 'digital_ocean'
    override.vm.box_url = "https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box"
    # Digital Ocean API token
    provider.token = ENV['DO_TOKEN']
    #provider.image = 'ubuntu-16-04-x64'
    provider.image = 'centos-7-x64'
    provider.region = 'nyc2'
    provider.size = '512mb'
    # The keypair name used on digital ocean
    provider.ssh_key_name = ENV['DO_KEY_NAME']
    end

    # Use Ansible to load playbook yml
    config.vm.provision :ansible do |ansible|
      ansible.raw_arguments  = [
        "--connection=paramiko"
      ]
      ansible.playbook = "./jenkins.yml"
      #ansible.verbose = "v"
    end

end
