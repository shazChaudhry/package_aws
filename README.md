# Scope
The purpose of this repo is mainly to learn packer and to demonstrate how to build an AWS AMI. The source code has come from [learn Packer](https://learn.hashicorp.com/packer/getting-started/build-image) tutorial.

## Clone this repo
- `git clone https://github.com/shazChaudhry/packer_aws.git`
- `cd packer_aws`

## Prerequisite
Use the provided Vagrantfile to spin up an environment which comes bundled with all necessary tools installed. See `Vagrantfile_README.md` for prerequisite.

## Setup environment
- `vagrant up --color`
- `vagrant ssh`
- `cd /vagrant`

## Environment variable
Hardcoding secrets in plain text in a git repository is highly discouraged. 

You may use [AWS Secrets Manager](https://www.packer.io/docs/templates/user-variables.html#aws-secrets-manager-variables) or [Vault](https://www.packer.io/docs/templates/user-variables.html#vault-variables) if you prefer to keep your secrets / credentials in those tools. In this repo however, environment variables will be required.

You can provide your credentials via the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY, environment variables, representing your AWS Access Key and AWS Secret Key, respectively. Note that setting your AWS credentials using either these environment variables will override the use of AWS_SHARED_CREDENTIALS_FILE and AWS_PROFILE. The AWS_DEFAULT_REGION and AWS_SESSION_TOKEN environment variables are also used, if applicable:
- `export AWS_ACCESS_KEY_ID="anaccesskey"`
- `export AWS_SECRET_ACCESS_KEY="asecretkey"`
- `export AWS_SESSION_TOKEN="asessiontoken"` 

In this particular example, AMI is created in a region that has a default VPC. Change the user variable called region.

See [Known Issue](https://learn.hashicorp.com/packer/getting-started/build-image#known-issue) if you see a `VPCResourceNotSpecified` error

## Run packer builds
Once the environment has been setup, you will need to execute the following commands:
- `packer validate packer.json`
- `packer build packer.json`

If you were to launch this newly created AMI, Redis would be pre-installed.

## Destroy environment
The virtual box environment may be destroyed once it is no longer needed
- `vagrant destroy --force`


