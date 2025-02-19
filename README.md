1. Check Docker Installation
First, verify if Docker is installed:
docker --version

If Docker is not installed, you'll need to install it. The installation steps vary depending on your Linux distribution.
For Debian/Ubuntu-based Systems:
Update the package index:
sudo apt-get update

Install required packages:
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

Add Docker’s official GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Set up the stable repository:
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

Update the package index again:
sudo apt-get update

Install Docker:
sudo apt-get install docker-ce

Install Docker Compose (if needed)
Download Docker Compose:
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

Apply executable permissions:
sudo chmod +x /usr/local/bin/docker-compose

Verify installation:
docker-compose --version

Important points to note: - If your running already vps for another project using port:9091 and try to run above commands on another project using same vps it will give error.

Here are some steps you can take to resolve the issue:

Check for Processes Using the Port
sudo lsof -i :9091

Stop the Conflicting Process: Once you identify the process, you can stop it. For example, on Linux, if the process ID is 1234, you can stop it with below, Be careful with killing processes, as it can affect system stability or other applications.
sudo kill 1234

Change the Port for Your Docker Container: If stopping the conflicting process isn’t an option or if you prefer to use a different port, you can modify your Docker configuration to use a different port. If you’re using docker run, you can change the port mapping like this:
docker run -p 9092:9091 your_image

In this example, the container’s port 9091 is mapped to the host’s port 9092.If you’re using Docker Compose, modify the docker-compose.yml file:
ports: - "9092:9091"

Restart Docker
sudo systemctl restart docker





