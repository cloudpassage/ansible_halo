#### Ansible playbook to install, upgrade, and uninstall Halo agent onto debian and rpm based OSes.

#### Install instructions on MAC OS X

1. Install Ansible `brew install ansible` (If you don't have brew preinstalled, then follow https://valdhaus.co/writings/ansible-mac-osx/ to install ansible)

#### Playbook configurations

1. Inside the halo directory, there are 2 things you need to configure:
    - list of server's ip addresses and their corresponding login usernames
    - Halo agent key

2. To add the list of connecting ip addresses and their login usernames, open the file named `hosts`
    

    Sample file content
    
    ```
        [all]
        10.10.10.123 ansible_user=ubuntu
        10.10.10.124 ansible_user=ec2-user
    ```
    
3. Open the file `all` located in `group_vars/all` and paste in your Halo agent key.

    Sample File content
    
    ```
        agent_key: abcabcabcabc12345
    ```

#### Program Usage (Commands) install, upgrade, uninstall, start, stop, restart

1. Run the following command to install Halo.
    `ansible-playbook -i hosts halo.yml --private-key=<ssh_key_path> --sudo -t install`

2. Run the following command to upgrade Halo.
    `ansible-playbook -i hosts halo.yml --private-key=<ssh_key_path> --sudo -t upgrade`

3. Run the following command to uninstall Halo.
    `ansible-playbook -i hosts halo.yml --private-key=<ssh_key_path> --sudo -t uninstall`

4. Run the following command to start Halo.
    `ansible-playbook -i hosts halo.yml --private-key=<ssh_key_path> --sudo -t start`

5. Run the following command to stop Halo.
    `ansible-playbook -i hosts halo.yml --private-key=<ssh_key_path> --sudo -t stop`

6. Run the following command to restart Halo.
    `ansible-playbook -i hosts halo.yml --private-key=<ssh_key_path> --sudo -t restart`


<!---

#CPTAGS:community-supported deployment
#TBICON:images/partner-supported.png

-->
