---
updated: '2023-10-30T12:41:12Z'
created: '2023-10-30T12:41:12Z'
---
```yaml
      - name: install dependencies
        run: |
          # install doctl
          wget -q https://github.com/digitalocean/doctl/releases/download/v1.100.0/doctl-1.100.0-linux-amd64.tar.gz
          tar xf ./doctl-1.100.0-linux-amd64.tar.gz
          sudo mv ./doctl /usr/local/bin
          doctl auth init -t "$DO_API_TOKEN"
        env:
          DO_API_TOKEN: ${{ secrets.DIGITAL_OCEAN_API_TOKEN }}
```

To add the secrets to your repository, go to settings -> secrets and variables -> actions. The URL is `https://github.com/<user>/<repo>/settings/secrets/actions`

See also [[how to install s3cmd for digital ocean storage uploads]]