---
tags:
  - "#tailscale"
  - github
---
Create new [OAuth Client](https://login.tailscale.com/admin/settings/oauth)with Read+Write on the Devices scope, tied to a specified tag.

Ensure the tag is configured for [Tailscale SSH](https://tailscale.com/kb/1193/tailscale-ssh) in the ACL, and the ACL allows communication with another system on the tailnet. Also ensure desired username (`deploy` in this case) exists and is permitted login through Tailscale SSH.

Capture SSH public keys from the system GitHub will be connecting to:
```shell
ssh-keyscan -H $hostname
```

Create repository secrets:

| Secret Name            | Contents/Purpose                         |
| ---------------------- | ---------------------------------------- |
| `TS_API_CLIENT_ID`     | OAuth Client ID                          |
| `TS_API_CLIENT_SECRET` | OAuth Client secret                      |
| `TS_TAG`               | ACL tag                                  |
| `SSH_KNOWN_HOSTS`      | Text output from `ssh-keyscan`           |
| `REMOTE_HOST`          | TS node name of the remote host          |
| `REMOTE_PATH`          | Path on remote host to transfer files to |

Add steps to `.github/workflows/your-workflow.yaml`:
```yaml
      - name: Connect to Tailscale
        uses: tailscale/github-action@v2
        with:
          oauth-client-id: ${{ secrets.TS_API_CLIENT_ID }}
          oauth-secret: ${{ secrets.TS_API_CLIENT_SECRET }}
          tags: ${{ secrets.TS_TAG }}
      - name: Configure SSH known hosts
        run: |
          mkdir -p ~/.ssh
          echo "${{ secrets.SSH_KNOWN_HOSTS }}" > ~/.ssh/known_hosts
          chmod 644 ~/.ssh/known_hosts
      - name: Deploy Content
        run: |
          rsync -avz --delete -e ssh public/ deploy@${{ secrets.REMOTE_HOST }}:${{ secrets.REMOTE_PATH }}
```