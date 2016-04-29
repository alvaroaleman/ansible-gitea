# vim: set ft=ruby ts=2 sw=2 et:
# -*- mode: ruby -*-


VAGRANT_API_VERSION = '2'
Vagrant.configure(VAGRANT_API_VERSION) do |config|

  if ENV['ANSIBLE_GOGS_VAGRANT_BOXNAME']
    config.vm.box = ENV['ANSIBLE_GOGS_VAGRANT_BOXNAME']
  else
    config.vm.box = 'centos/7'
  end

  config.vm.define :ansiblegogstest do |d|

    d.vm.hostname = 'ansiblegogstest'
    d.vm.synced_folder '.', '/vagrant', id: 'vagrant-root', disabled: true
    d.vm.network "forwarded_port", host: 3000, guest: 3000

    d.vm.provision :ansible do |ansible|
      ansible.playbook = 'tests/playbook.yml'
      ansible.tags = ENV['ANSIBLE_GOGS_VAGRANT_ANSIBLE_TAGS']
      ansible.skip_tags = ENV['ANSIBLE_GOGS_VAGRANT_ANSIBLE_SKIP_TAGS']
      ansible.verbose = ENV['ANSIBLE_GOGS_VAGRANT_ANSIBLE_VERBOSE']
      #ansible.galaxy_command = 'ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --ignore-errors --force'
      #ansible.galaxy_role_file = 'requirements.yml'
      if ENV['ANSIBLE_GOGS_VAGRANT_ANSIBLE_CHECKMODE'] == '1'
        ansible.raw_arguments = '--check'
      end
      ansible.groups = {
        'vagrant' => ['ansiblegogstest']
      }
      ansible.limit = 'vagrant'
      ansible.raw_arguments = [
        '--diff'
      ]
      if ENV['ANSIBLE_GOGS_VAGRANT_ANSIBLE_CHECKMODE'] == '1'
        ansible.raw_arguments << '--check'
      end

      ::File.directory?('.vagrant/provisioners/ansible/inventory/') do
        ansible.inventory_path = '.vagrant/provisioners/ansible/inventory/'
      end

    end

    d.vm.provider :virtualbox do |v|
      v.customize 'pre-boot', ['modifyvm', :id, '--nictype1', 'virtio']
      v.customize [ 'modifyvm', :id, '--name', 'ansiblegogstest', '--memory', '512', '--cpus', '1' ]
    end

    d.vm.provider :libvirt do |lv|
      lv.memory = 512
      lv.cpus = 1
    end


  end
end
