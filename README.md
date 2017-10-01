
Como utilizar esse projeto
--------------------------

- Crie as maquinas virtuais. Para isso, pode-se utilizar o vagrant.

- Sete os hosts no inventory.
  No CentOS, execute os seguintes comandos para ver quais sao os ips.
    sudo yum -y install net-tools
    ip addr sh

- Para que os playbooks funcionem, eh necessario baixar um monte de coisas
  antes, como jdk, hadoop, scala, spark. Depois de baixar, tem que setar
  direitinho os paths no playbook.

- Rode o playbook master.yml duas vezes. Na primeira ele falha porque nao
  consegui fazer um reboot direito.
  	ansible-playbook -i inventory master.yml

- Rode o playbos slaves.yml. Uma vez basta para ele.
	ansible-playbook -i inventory slaves.yml

- Verifique se cada um dos nodos do cluster consegue acessar os outros. As
  vezes da merda com isso.

- Crie os namenodes
  hdfs namenode –format

- Dê um start no cluster
  sh $HADOOP_HOME/sbin/start-dfs.sh
  sh $HADOOP_HOME/sbin/start-yarn.sh

- Verifique se as interfaces web para ver se elas estao bonitas. Aqui, coloque
  o ip do node master.

  Name Node: http://192.168.0.43:50070/
  YARN Services: http://192.168.0.43:8088/
  Secondary Name Node: http://192.168.0.43:50090/
  Data Node 1: http://192.168.0.43:50075/
  Data Node 2: http://192.168.0.44:50075/

- Dê um stop no cluster
  sh $HADOOP_HOME/sbin/stop-yarn.sh
  sh $HADOOP_HOME/sbin/stop-dfs.sh
  

Referênciaas para construção desse projeto
- http://backtobazics.com/big-data/setup-multi-node-hadoop-2-6-0-cluster-with-yarn/
- https://www.quora.com/How-do-I-set-up-Apache-Spark-with-Yarn-Cluster

Outras referencias que podem vir a ser uteis:
- https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/hdfs-default.xml
- http://www.michael-noll.com/tutorials/running-hadoop-on-ubuntu-linux-multi-node-cluster/
