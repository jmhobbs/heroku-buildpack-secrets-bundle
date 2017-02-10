Secrets don't belong in your repository, but sometimes they are too large or unwieldy for envornment variables.  This provides a simple way to securely drop a bundle of files into your Heroku application on deploy.

__This is experimental, and not 12-Factor compliant__

# Usage

1. Tar-Gzip your secrets
  * `cd secrets/ && tar -c * | gzip > ../secrets.tar.gz`
1. Encrypt with OpenSSL AES-256-CBC
  * `openssl enc -aes-256-cbc -salt -in secrets.tar.gz -out secrets.tar.gz.enc`
1. Host it somewhere (Dropbox public folder is an easy option)
1. Set `SECRET_BUNDLE_URL` and `SECRET_BUNDLE_PASSPHRASE` accordingly
1. Add the buildpack to your Heroku app
  * `heroku buildpacks:add -i 1 https://github.com/getflywheel/heroku-buildpack-secrets-bundle`
1. Deploy your app to Heroku
1. Your app should now have a `secrets/` directory to use

# Cache

After you deploy once with a secrets bundle, you can clear `SECRET_BUNDLE_URL` and `SECRET_BUNDLE_PASSPHRASE` and it will still load the secrets from cache.  If you want to replace the cache, just set them again and it will overwrite.

If you want to completely flush your cache, set `SECRET_BUNDLE_URL` to `DELETE` and run a deploy.
