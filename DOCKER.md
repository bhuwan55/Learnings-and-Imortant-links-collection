# Install Docker on Linux Mint Cinnamon 19.1 (TLS)
  - Update the apt package index:
    ``sudo apt-get update``
    
  - Install following packages to allow installation over HTTPS:
  ``sudo apt-get install apt-transport-https ca-certificates curl software-properties-common``
  
  - Add Docker Official GPG key (to make sure packages are official based on GPG digital signatures keys):
  ``curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -``
  
  - Verify that there's the key with signature **9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88** by searching:
  ``sudo apt-key fingerprint 0EBFCD88``
  
  - Add the stable repository
  ``sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"``
  
  - Finished Setting Repository. Now update the apt list using:
  ``sudo apt-get update``
  
  - Install the latest version of docker
  ``sudo apt-get install docker-ce``
> Note: Using sudo docker gets installed with super user privilage. Thus to build it we must use ``sudo``

  **Example:**

    a. Build docker image: ``sudo docker build .``
 
 [Docker commands list documentation](https://docs.docker.com/engine/reference/commandline/container_ls/)
 
 # Docker Compose
  - Too that allows to run the project on docker containers easily.
  - Helps in managing different services that the project uses inside the container. For exampe one service might be python service while another service might be database.
  
  - Filename : ``docker-compose.yml`` i.e ends with ``.yml`` extension
  
  ```yml
  version: "3"
services:
  app :
    build :
      context: .
    ports:
      - "8000:8000"
    volumes:
      - ./app:/app
    command: >
      sh -c "python manage.py runserver 0.0.0.0:8000"
  ```
  
  
 
