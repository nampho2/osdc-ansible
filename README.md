# <img src="img/osdc.png" alt="osdc" /> <img src="img/ansible.jpg" alt="ansible" />
<a href="https://github.com/ansible/ansible">Ansible</a> playbooks to deploy applications on the <a href="https://www.opensciencedatacloud.org/systems/#availableResources">OSDC</a>'s OpenStack though it can easily be modified to provision the same applications on any private cloud using OpenStack. Ansible will reproducibly replace the need to create and manage virtual machines using the OpenStack <a href="https://www.opensciencedatacloud.org/support/commandline.html">CLI</a>.

Run the `openrc.sh` script to configure your environment with the `OS_PASSWORD`, `OS_AUTH_URL`, `OS_USERNAME`, and `OS_TENANT_NAME`.

**HPC Playbook** <br />

Simply run the `hpc.yml` playbook to setup your cluster.

```
$ ansible-playbook hpc.yml
```

Once the Ansible run finishes you can log into the head node and submit jobs immediately.

```
$ ssh root@hn1
```

Ansible is meant to replace manual commands below but one can also setup the machines with the following commands.

```
# add your ssh-key for future vm
$ nova keypair-add --pub_key ~/.ssh/id_rsa.pub ansible_key

# spin up head node
$ nova boot --flavor m1.medium --image 0e50e989-9b33-442f-8e3b-227c41296c88 --key_name ansible_key hn1; 

# spin up compute nodes with the remaining cores
$ for i in {1..7}; 
do 
   nova boot --flavor m1.medium --image 0e50e989-9b33-442f-8e3b-227c41296c88 --key_name ansible_key cn$i; 
done
```

**References**

Methods For Creating XSEDE Compatible Clusters [<a href="https://www.cac.cornell.edu/about/pubs/a74-fischer.pdf">PDF</a>] [<a href="https://portal.xsede.org/knowledge-base/-/kb/document/bdwx">YUM</a>]

**ELK Playbook** <br />

Future plans are to create a playbook to deploy Elasticsearch, Logstash, and Kibana clusters to analyze public data sets on OSDC.
