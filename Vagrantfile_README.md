## Vagrant Box prerequisites
- The user has admin privileges on their development machines
- At least 4GB of free RAM is available on the machine. Otherwise, Vagrantfile will need editing to adjust the available memory:
  - `v.customize ["modifyvm", :id, "--memory", <MEMORY_ALLOCATION>]`
- Latest version of [Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Latest version of [Git for Windows](https://git-scm.com/downloads)
- Latest version of [Vagrant](https://www.vagrantup.com/intro/getting-started/install.html)
  - Install Vagrant Host Manager plugin by running the following command in the Git Bash terminal. This plugin updates the host files on both guest and host machines:
    - `vagrant plugin install vagrant-hostmanager`

## Start vagrant box
- `vagrant up --color`
- `vagrant ssh`
- `cd /vagrant`

## Clone this repo
- `git clone https://github.com/shazChaudhry/packer_aws.git`
- `cd packer_aws`

## Environment variable
Hardcoding plain text secrets in a git repository is highly discouraged. 

You may use [AWS Secrets Manager](https://www.packer.io/docs/templates/user-variables.html#aws-secrets-manager-variables) or [Vault](https://www.packer.io/docs/templates/user-variables.html#vault-variables) if you prefer to keep your secrets / credentials in those tools. In this repo environment variables will be set:
  - `export AWS_ACCESS_KEY_ID=XXXXXXXXXXXXX`
  - `export AWS_SECRET_ACCESS_KEY=XXXXXXXXXXXXXXXXXXXXXXX`
  - `export AWS_SESSION_TOKEN=XXXXXXXXXXX` _(Required only if you are assuming an IAM role)_

## Run packer builds
Once the environment has been setup, you will need to execute the following commands:
- `packer build template.json`

## Destroy vagrant box
- `vagrant destroy --force`