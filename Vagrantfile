#Make default provider Azure for this project
ENV['VAGRANT_DEFAULT_PROVIDER'] ||= 'azure'

#Read settings from YAMLs
require 'yaml'
settings_secured = YAML.load_file 'settings_secured.yaml'

Vagrant.configure(2) do |config|
    config.vm.box = 'azure'

    config.vm.provider :azure do |azure|

      azure.subscription_id       = settings_secured['subscription_id']

      azure.mgmt_certificate      = settings_secured['mgmt_certificate']
      azure.mgmt_endpoint         = 'https://management.core.windows.net'
      azure.ssh_private_key_file  = settings_secured['ssh_private_key_file']
      azure.ssh_certificate_file  = settings_secured['ssh_certificate_file']

      azure.cloud_service_name    = settings_secured['cloud_service_name'] # optional. A new one will be generated if not provided.
      azure.storage_acct_name     = settings_secured['storage_acct_name'] # optional. A new one will be generated if not provided.
      azure.deployment_name       = settings_secured['deployment_name'] # defaults to cloud_service_name

      azure.vm_image              = settings_secured['vm_image']
      azure.vm_size               = settings_secured['vm_size']
      azure.vm_user               = settings_secured['vm_user'] # defaults to 'vagrant' if not provided
      azure.vm_password           = settings_secured['vm_password'] # min 8 characters. should contain a lower case letter, an uppercase letter, a number and a special character

      azure.vm_name               = settings_secured['vm_name'] #MUST BE LOWERCASE! https://github.com/MSOpenTech/vagrant-azure/issues/11 max 15 characters. contains letters, number and hyphens. can start with letters and can end with letters and numbers
      azure.vm_location           = settings_secured['vm_location'] # e.g., West US

      # Provide the following values if creating a *Nix VM
      azure.ssh_port = settings_secured['ssh_port']

      # Provide the following values if creating a Windows VM
      #azure.winrm_transport = [ 'http', 'https' ] # this will open up winrm ports on both http (5985) and http (5986) ports
      #azure.winrm_https_port = 'A VALID PUBLIC PORT' # customize the winrm https port, instead of 5986
      #azure.winrm_http_port = 'A VALID PUBLIC PORT' # customize the winrm http port, insted of 5985

      #azure.tcp_endpoints = '3389:53389' # opens the Remote Desktop internal port that listens on public port 53389. Without this, you cannot RDP to a Windows VM.
    end

    config.ssh.username = settings_secured['vm_user'] # the one used to create the VM
    config.ssh.password = settings_secured['vm_password'] # the one used to create the VM
end
