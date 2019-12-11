FROM ubuntu:16.04
RUN apt-get update && apt-get install -y wget && apt-get install -y sudo && apt-get install -y curl
RUN apt-get install -y git
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
RUN apt-get update && apt-get install -y apt-transport-https
RUN sudo dpkg -i packages-microsoft-prod.deb
RUN apt-get install -y software-properties-common && apt-get update
RUN sudo add-apt-repository universe
RUN sudo apt-get install -y apt-transport-https
RUN sudo apt-get install -y dotnet-sdk-3.0
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
RUN sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
RUN sudo apt-get update
RUN apt-cache policy docker-ce
RUN sudo apt-get install -y docker-ce
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
