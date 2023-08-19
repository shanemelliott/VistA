#ARG IMAGE=containers.intersystems.com/intersystems/irishealth:2020.1.3.521.0
ARG IMAGE=containers.intersystems.com/intersystems/iris-community:2022.3.0.606.0
FROM $IMAGE

USER root

# RUN chown ${ISC_PACKAGE_MGRUSER}:${ISC_PACKAGE_IRISGROUP} /opt/irisapp
RUN apt-get update \
     && apt-get -y install xinetd vim \
     /bin/echo -e ${ISC_PACKAGE_MGRUSER}\\tALL=\(ALL\)\\tNOPASSWD: ALL >> /etc/sudoers && \
	sudo -u ${ISC_PACKAGE_MGRUSER} sudo echo enabled passwordless sudo-ing for ${ISC_PACKAGE_MGRUSER}

COPY /vista/stg_rpc /etc/xinetd.d/stg_rpc
COPY /vista/stg_vlk /etc/xinetd.d/stg_vlk
COPY /vista/smeint.xml /tmp/smeint.xml
COPY /vista/xusrb1.xml /tmp/xusrb1.xml
COPY /vista/xinetd.sh /xinetd.sh
COPY /vista/xusrb1fix.script /tmp/xusrb1fix.script
COPY /vista/xusrb1fix.sh /tmp/xusrb1fix.sh
COPY /vista/CreateUser.script /tmp/CreateUser.script
COPY /vista/CreateUser.sh /tmp/CreateUser.sh
RUN chmod +x /tmp/xusrb1fix.sh
USER ${ISC_PACKAGE_MGRUSER}

