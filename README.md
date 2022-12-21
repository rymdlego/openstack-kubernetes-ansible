# HA Kubernetes install and configuration

Install everything needed for a complete HA Kubernetes cluster.

All control planes will run *keepalived* and *haproxy* for HA functionality.

Control planes will run *etcd* in stacked mode.

The playbook is idempotent and can be run repeatedly, ie to join a new node at a later time.

## Usage
#### Prereqs
* ansible
* The public IP of the ssh-bastion
* The public IP for Kubernetes API access

#### Config

Make changes in the inventory file
- Set the correct IP of your bastion host
- Set your desired hostname for the api-server
- Make any network addresses changes if needed

#### Run
- Check that you are able to connect to your Openstack instances `ansible -m ping kubernetes`
- If everything looks good, run `ansible-playbook kubernetes.yml`

#### Post install
- Make sure that your kubernetes hostname resolves to the Kubernetes API IP (which you got from Terraform output). Create the DNS record or hack your /etc/hosts accordingly
- Test the kubeconfig file `kubectl --kubeconfig kube.conf get nodes`