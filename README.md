# ansible-step-ca-ra
Ansible to deploy step-ca as a Registration Authority

## Requirements

* Tailscale installed and configured for ssh
    ```bash
    sudo tailscale up --ssh --advertise-tags "tag:servers,tag:step-ca-ra"
    ```

## Run

```bash
ansible-playbook -i hosts setup.yaml -v --diff
ansible-playbook -i hosts site.yaml -v --diff
```