# ansible-gitdeploy
A set of ansible scripts, to set up basic server for project, with git auto-deployment.

## Install

First of all you need [ansible](http://www.ansible.com/home)

    brew/apt-get/yum/whatever install ansible

Also, you need an inventory file, and configure all the hosts you wish to install this setup to:

    cat << EOF > ansible-inventory
    [local]
    123.234.345.456 ansible_ssh_user=root
    some.other.host.com ansible_ssh_user=root
    EOF

See [ansible documentation](http://docs.ansible.com/intro_inventory.html) for more details. If you wish to use
`ansible_ssh_user=root` like in example above, don't forget to put your public key to `/root/.ssh/authorized_keys` on
the remotes.

Next, you need to configure your new system(s) variables:

    vi roles/autodeploy/vars/main.yml

And you're ready to rock!

    ansible-playbook -s -i ansible-inventory main.yml

As a two last results, Ansible will output your Webhook URL and deploy key (if you need it):

    TASK: [autodeploy | Your deploy key] ******************************************
    ok: [1.2.3.4] => {
        "msg": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDVi3DnsWAnuKaML3eR9j16IEKCcW8qRr1lxNPaNR1R3/W92km+Kfmgsy71O9uNDoHXGb64XrYMkB2PkHmsQxzUx3A2slrtl/OxaC9GpWmDV1pQYHSpuILP+f6hTBvWkUFG16oK90jyCcLNr7eSDy22iJualqQsj8TcMxygm49vMWHAick+/rbw7Dthsnl0UKjAJDKlN+T/hHzU4om87qDim8eIuRVRgFaZXchR6AuvUfA7ebfmUOh0wpfPWfbyssqLyu0wSYKPFpfJOGIXD6bZJ5K1NRcL10froy7AZ90d8j+qsmC8pkphyBxwGulEnJrGcsjbdwuD0UAcl5MIY5Q5 deploy@gitdeploy"
    }

    TASK: [autodeploy | Your webhook] *********************************************
    ok: [1.2.3.4] => {
        "msg": "http://gitdeploy:tiePeeweuh3bae3kuoxai6Yo@1.2.3.4/_autodeploy"
    }

Have fun!
