# ansible-step-ca-ra
Ansible to deploy step-ca as a Registration Authority

## Requirements

* Tailscale installed and configured for ssh
    ```bash
    sudo tailscale up --ssh --advertise-tags "tag:servers,tag:step-ca-ra"
    ```
* Create SmallStep Provisioner for the RA
    ```bash
    wget https://dl.smallstep.com/cli/docs-cli-install/latest/step-cli_amd64.deb
    dpkg -i step-cli_amd64.deb
    rm -f step-cli_amd64.deb
    STEPPATH=/etc/step step ca bootstrap --ca-url https://cuboid-topi.rmb1993-gmail-com.ca.smallstep.com --fingerprint eb136a5118931a2306964469705323521dda8c43d26ec67e1c5508eb123f9c70
    STEP_CONSOLE=true STEPPATH=/etc/step step ca provisioner add $(hostname -f) --type JWK --create --password-file /etc/ssh/ssh_host_ed25519_key --disable-ssh-ca-user --disable-ssh-ca-host --x509-min-dur=2190h --x509-max-dur=2190h --x509-default-dur=2190h --ssh=false --admin-subject dummy@example.com
    STEP_CONSOLE=true STEPPATH=/etc/step step ca policy provisioner x509 allow dns '*.rmb938.me' --provisioner $(hostname -f) --admin-subject dummy@example.com
    ```

## Run

```bash
ansible-playbook -i hosts site.yaml -v --diff
```