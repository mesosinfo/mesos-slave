mesos-slave
===========================================================
<a href='https://imagelayers.io/?images=mesosinfo/mesos-slave:ubuntu-14.04' title='Get your own badge on imagelayers.io'><img src='https://badge.imagelayers.io/mesosinfo/mesos-slave:ubuntu-14.04.svg'></a>

Multi-node Setup

For this setup, we will need 3 servers with Docker installed on it.

1. Export out the 3 servers' IP that we will be using on each server

		#zookeeper servers
        ZOOKEEPER_HOST_IP_1=192.168.22.82
        ZOOKEEPER_HOST_IP_2=192.168.22.87
        ZOOKEEPER_HOST_IP_3=192.168.22.92
		 
2. Run the mesos slave on docker with docker containerizers

    On host #1

		docker run -d --net="host" \
		-p 5051:5051 \
		--entrypoint="mesos-slave" \
		-e "MESOS_MASTER=zk://${HOST_IP_1}:2181,${HOST_IP_2}:2181,${HOST_IP_3}:2181/mesos" \
		-e "MESOS_LOG_DIR=/var/log/mesos" \
		-e "MESOS_LOGGING_LEVEL=INFO" \
		-e MESOS_EXECUTOR_REGISTRATION_TIMEOUT=5mins \
		-e MESOS_ISOLATOR=cgroups/cpu,cgroups/mem \
		-e MESOS_CONTAINERIZERS=docker,mesos \
		-v /run/docker.sock:/run/docker.sock \
		mesosinfo/mesos-slave


    On host #2

		docker run -d --net="host" \
		-p 5051:5051 \
		--entrypoint="mesos-slave" \
		-e "MESOS_MASTER=zk://${HOST_IP_1}:2181,${HOST_IP_2}:2181,${HOST_IP_3}:2181/mesos" \
		-e "MESOS_LOG_DIR=/var/log/mesos" \
		-e "MESOS_LOGGING_LEVEL=INFO" \
		-e MESOS_EXECUTOR_REGISTRATION_TIMEOUT=5mins \
		-e MESOS_ISOLATOR=cgroups/cpu,cgroups/mem \
		-e MESOS_CONTAINERIZERS=docker,mesos \
		-v /run/docker.sock:/run/docker.sock \
		mesosinfo/mesos-slave

    On host #3

		docker run -d --net="host" \
		-p 5051:5051 \
		--entrypoint="mesos-slave" \
		-e "MESOS_MASTER=zk://${HOST_IP_1}:2181,${HOST_IP_2}:2181,${HOST_IP_3}:2181/mesos" \
		-e "MESOS_LOG_DIR=/var/log/mesos" \
		-e "MESOS_LOGGING_LEVEL=INFO" \
		-e MESOS_EXECUTOR_REGISTRATION_TIMEOUT=5mins \
		-e MESOS_ISOLATOR=cgroups/cpu,cgroups/mem \
		-e MESOS_CONTAINERIZERS=docker,mesos \
		-v /run/docker.sock:/run/docker.sock \
		mesosinfo/mesos-slave
		
3. Run the mesos slave on docker no docker containerizers

    On host #1

		docker run -d --net="host" \
		-p 5051:5051 \
		--entrypoint="mesos-slave" \
		-e "MESOS_MASTER=zk://${HOST_IP_1}:2181,${HOST_IP_2}:2181,${HOST_IP_3}:2181/mesos" \
		-e "MESOS_LOG_DIR=/var/log/mesos" \
		-e "MESOS_LOGGING_LEVEL=INFO" \
		mesosinfo/mesos-master

    On host #2

		docker run -d --net="host" \
		-p 5051:5051 \
		--entrypoint="mesos-slave" \
		-e "MESOS_MASTER=zk://${HOST_IP_1}:2181,${HOST_IP_2}:2181,${HOST_IP_3}:2181/mesos" \
		-e "MESOS_LOG_DIR=/var/log/mesos" \
		-e "MESOS_LOGGING_LEVEL=INFO" \
		mesosinfo/mesos-master

    On host #3

		docker run -d --net="host" \
		-p 5051:5051 \
		--entrypoint="mesos-slave" \
		-e "MESOS_MASTER=zk://${HOST_IP_1}:2181,${HOST_IP_2}:2181,${HOST_IP_3}:2181/mesos" \
		-e "MESOS_LOG_DIR=/var/log/mesos" \
		-e "MESOS_LOGGING_LEVEL=INFO" \
		mesosinfo/mesos-master
		
