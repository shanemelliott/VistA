ARG IMAGE=intersystemsdc/irishealth-community
ARG IMAGE=intersystemsdc/iris-community
FROM $IMAGE

USER root

# RUN chown ${ISC_PACKAGE_MGRUSER}:${ISC_PACKAGE_IRISGROUP} /opt/irisapp
RUN apt-get update \
     && apt-get -y install xinetd vim 
     
#RUN /bin/echo -e ${ISC_PACKAGE_MGRUSER}\\tALL=\(ALL\)\\tNOPASSWD: ALL >> /etc/sudoers && \
#	sudo -u ${ISC_PACKAGE_MGRUSER} sudo echo enabled passwordless sudo-ing for ${ISC_PACKAGE_MGRUSER}

COPY stg_rpc /etc/xinetd.d/stg_rpc
COPY stg_vlk /etc/xinetd.d/stg_vlk
COPY smeint.xml /tmp/smeint.xml
COPY xusrb1.xml /tmp/xusrb1.xml
COPY xinetd.sh /xinetd.sh
COPY merge.cpf /home/irisowner/merge.cpf
COPY xusrb1fix.script /tmp/xusrb1fix.script
COPY xusrb1fix.sh /tmp/xusrb1fix.sh
COPY CreateUser.script /tmp/CreateUser.script
COPY CreateUser.sh /tmp/CreateUser.sh
RUN chmod +x /tmp/xusrb1fix.sh
RUN mkdir /home/irisowner/dat/vista
RUN wget https://foia-vista.worldvista.org/DBA_VistA_FOIA_System_Files/DBA_VISTA_FOIA_2024/DBA_VISTA_FOIA_20240401.zip
RUN mv DBA_VISTA_FOIA_20240401.zip /home/irisowner/dat/vista/
RUN unzip /home/irisowner/dat/vista/DBA_VISTA_FOIA_20240401.zip
USER ${ISC_PACKAGE_MGRUSER}
#RUN --mount=type=bind,src=.,dst=. iris start IRIS && iris session IRIS < expuser.script && iris stop IRIS quietly

