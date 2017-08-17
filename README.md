#### Ansible playbook to install, upgrade, and uninstall Halo agent onto debian and rpm based OSes.

#### Install instructions on MAC OS X

1. Install Ansible `brew install ansible` (If you don't have brew preinstalled, then follow https://valdhaus.co/writings/ansible-mac-osx/ to install ansible)

#### Playbook configurations (Linux)

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

#### Playbook configurations (Windows)

Below instructions are for linux control machine.

1. Install winrm on your linux control machine

    ```
        pip install "pywinrm>=0.2.2"
    ```

2. Add the list of connecting ip addresses, open the file named `hosts`

    Sample file content

    ```
        [all]
        10.10.10.123 ansible_user=ubuntu
        10.10.10.124 ansible_user=ec2-user

        [windows]
        windows.local.com
    ```
3. Add Windows login information, open the file named `group_vars\window.yml`

    Sample file content

    ```
        ansible_user: Administrator
        ansible_password: password # Windows host password
        ansible_port: 5986
        ansible_connection: winrm
        ansible_winrm_server_cert_validation: ignore
        halo_package_version: 4.1.0    # Halo Daemon version
        destination_dir: tmp           # Halo Daemon download desitanation
    ```

4. Make sure port `5986` is open on your Windows server.

5. Open the file `all` located in `group_vars/all` and paste in your Halo agent key.

    Sample File Content

    ```
        agent_key: abcdefghij123456
    ```

6. Make sure to enable and configure PowerShell remoting. To automate the setup of WinRM, you can run the examples/scripts/ConfigureRemotingForAnsible.ps1 (https://github.com/ansible/ansible/blob/devel/examples/scripts/ConfigureRemotingForAnsible.ps1) script on the remote machine in a PowerShell console as an administrator

7. If you are using AWS for your windows servers, you can automate the PowerShell remoting configuration by specifying the below powershell script before launching the AWS windows server. Please paste the below text in Step 3: Configure Instance Details -> Advanced Details -> User Data

```
<powershell>
Invoke-Expression ((New-Object System.Net.Webclient).DownloadString('https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1'))
</powershell>

```
Please reference (http://blog.rolpdog.com/2015/09/manage-stock-windows-amis-with-ansible.html) for more information.

#### Program Usage (Commands) install, upgrade, uninstall, start, stop, restart for Linux servers

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

#### Program Usage (Commands) install, upgrade, uninstall, start, stop, restart for Windows servers

1. Run the following command to install Halo.
    `ansible-playbook -i hosts halo.yml -t install`

2. Run the following command to uninstall Halo.
    `ansible-playbook -i hosts halo.yml -t uninstall`

3. Run the following command to start Halo.
    `ansible-playbook -i hosts halo.yml -t start`

4. Run the following command to stop Halo.
    `ansible-playbook -i hosts halo.yml -t stop`

5. Run the following command to restart Halo.
    `ansible-playbook -i hosts halo.yml -t restart`

6. To upgrade Halo agent version. Provide the later agent version in group_vars/windows.yml and run the following command.
    `ansible-playbook -i hosts halo.yml -t install`

<!---

#CPTAGS:community-supported archive

-->
