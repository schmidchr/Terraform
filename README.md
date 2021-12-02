# TestDrive-Terraform
First experience with Terraform system and start learning about the advantages of Infrastructure as Code (IaC)

Promising aspects of the Terraform tool:<br>
	- options to define computing infrastructure in human and machine-readable code<br>
	- transparency and flexibility through open source<br>
	- no vendor lock-in for cloud service provider<br>
	
## Mock exercise: setup a nginx webserver via docker
 following the tutorial: https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started

- I used a test machine under Ubuntu 20.04 with already installed docker engine<br>

- Ensure that system is up to date, and required packages installed (in my case all already at the newest version :) <br>
  `sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl`
 
- Add the HashiCorp GPG key <br>
  `curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -`

- Add the official HashiCorp Linux repository (-> deactivate after test ...) <br>
  `sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"`

- install the Terraform CLI <br>
  `sudo apt-get update && sudo apt-get install terraform`

- Verify that the installation worked by listing Terraform's available subcommands <br>
  `terraform -help`

- install the autocomplete package <br>
  `terraform -install-autocomplete`

- you may want to become a user dedicated to manage docker as non-root user<br>
in my case I created earlier a user docker (https://askubuntu.com/questions/477551/how-can-i-use-docker-without-sudo)<br>
  `su docker`<br>
change into the home directory of this user<br>
  `cd ~/`

- clone this repo containing the Terraform configuration file `main.tf` <br>
  `git clone git@github.com:schmidchr/TestDrive-Terraform.git`

- change into the directory containing the configuration file <br>
  `cd learn-terraform-docker-container`

- Initialize the project, which downloads a plugin that allows Terraform to interact with Docker <br>
  `terraform init`

- Provision the NGINX server container. When Terraform asks you to confirm type yes and press ENTER <br>
  `terraform apply`

- verify the existence of the NGINX container by visiting <br>
  `http://localhost:8000/`

## => successfully provisioned an NGINX webserver with Terraform !:)

- to clean up, stop the container <br>
  `terraform destroy`
