## build : docker build -t lightedge-upfservice-manager .
## run :   docker run --net=host --rm --privileged -it lightedge-upfservice-manager

FROM ubuntu:19.10
MAINTAINER Roberto Riggio <rriggio@fbk.eu>

# Installing python dependencies
RUN apt update
RUN apt -y install python3-pip wget unzip iptables
RUN pip3 install tornado==6.0.3 pymodm==0.4.1 influxdb==5.2.3 python-iptables==0.14.0

# Fetching the latest repository from lightedge-rniservice-manager.
RUN wget https://github.com/lightedge/lightedge-rniservice-mananger/archive/refs/heads/master.zip
RUN unzip master.zip
RUN rm master.zip
RUN mkdir -p /etc/lightedge/
RUN ln -sf /lightedge-rniservice-mananger-master/conf/ /etc/lightedge/rniservice
RUN mkdir -p /var/www/lightedge/
RUN ln -sf /lightedge-rniservice-manager-master/webui/ /var/www/lightedge/rniservice

# Run the controller
ENTRYPOINT ["python3.7", "/lightedge-rniservice-manager-master/lightedge-rniservice-manager.py"]

# Expose Web GUI
#EXPOSE 8888
