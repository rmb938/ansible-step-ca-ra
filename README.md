# ansible-step-ca-ra
Ansible to deploy step-ca as a Registration Authority

## Requirements

* Tailscale installed and configured for ssh
    ```bash
    sudo tailscale up --hostname "$(hostname -f | awk -F"." '{print $3}')-$(hostname -f | awk -F"." '{print $2}')-$(hostname)" --ssh --advertise-tags "tag:servers,tag:cloud-$(hostname -f | awk -F"." '{print $3}')-region-$(hostname -f | awk -F"." '{print $2}'),tag:step-ca-ra"
    ```

## Run

```bash
ansible-playbook -i hosts site.yaml -v --diff
```