Synopsis
========

Apply this role right after a new host has been installed.


    $ ansible-playbook --limit <host> apply-after-install.yml --extra-vars "ansible_become_pass=<pass>"

The role provides:

* preinstall the following packages
* a password-less `sudo` (w/ resetting `HOME` environment variable)
* for localhost it can be useful to use
    export ANSIBLE_ASK_SUDO_PASS=True
* current usage
    $ source bin/activate
    $ ansible-playbook playbooks/basic-configuration.yml
* TODO: post_tasks, delegate_to, run_once: True, with_items: "{{ groups['vpn-client'] }}"

Testing
=======
Run these commands below

    > docker build -t sshd conf/
    > for i in ca:5555 vpnd:5556 vpnc1:5557 vpnc2:5558 vpnc3:5559; do docker container run --name ${i%:*} --rm -dp 0.0.0.0:${i#*:}:22 --expose 22 sshd; done
    > ansible-playbook -i inventory/test-hosts playbooks/basic-configuration.yml --ssh-extra-args="-oStrictHostKeyChecking=no"

