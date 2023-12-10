#Run this command to execute the playbook

ansible-playbook -i inventory.ini kubectl_run.yml


#To login without  password run the ssh and ansible as "surajk"[user created with ssh setup]


# Run this as Root to copy the .kube/config

sudo su
cp -r $HOME/.kube /home/surajk
chown surajk:surajk /home/surajk/.kube/config


# Insall plugin for confirmation

ansible-galaxy collection install community.general
