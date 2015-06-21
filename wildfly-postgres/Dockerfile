FROM jboss/wildfly:8.2.0.Final
MAINTAINER xcoulon@redhat.com

ENV postgres_module_dir=/opt/jboss/wildfly/modules/system/layers/base/postgresql/main/
# add postgresql-jdbc jar and module.xml files
RUN mkdir -p ${postgres_module_dir}
ADD module.xml ${postgres_module_dir}
WORKDIR ${postgres_module_dir}
ADD postgresql-9.4-1201.jdbc41.jar ${postgres_module_dir}

# replace the standalone.xml config file with our custom one
ENV config_dir=/opt/jboss/wildfly/standalone/configuration/
ADD standalone.xml ${config_dir}

# define the deployments directory as a volume that can be mounted
VOLUME /opt/jboss/wildfly/standalone/deployments

# Add a management user named 'admin' 
RUN /opt/jboss/wildfly/bin/add-user.sh -u admin -p admin --silent

# expose debug port
EXPOSE 8787

# start WildFly in standalone/debug mode and allow management from host 
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-c", "standalone.xml", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0" , "--debug"]


