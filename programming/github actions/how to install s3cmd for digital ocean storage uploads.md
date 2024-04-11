```yaml
      - name: install dependencies
        run: |
          # install s3cmd and configure it
          sudo apt install -yqq s3cmd
          printf "[default]\naccess_key = %s\nsecret_key = %s\nhost_base = nyc3.digitaloceanspaces.com\nhost_bucket = %%(bucket)s.nyc3.digitaloceanspaces.com" "$DO_ACCESS_KEY" "$DO_SECRET_KEY" > ~/.s3cfg
        env:
          DO_ACCESS_KEY: ${{ secrets.DIGITAL_OCEAN_STORAGE_ACCESS_KEY }}
          DO_SECRET_KEY: ${{ secrets.DIGITAL_OCEAN_STORAGE_SECRET_KEY }}
```

To add the secrets to your repository, go to settings -> secrets and variables -> actions. The URL is `https://github.com/<user>/<repo>/settings/secrets/actions`

See also [[how to install doctl in a github action]]; after I upload stuff to digital ocean storage I run `doctl compute cdn flush` to make sure the new content gets served.

[[s3cmd]]