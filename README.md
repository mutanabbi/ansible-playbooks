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
