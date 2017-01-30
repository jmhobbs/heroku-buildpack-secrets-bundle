1. Tar-Gzip your secrets as a directory
1. Encrypt with `openssl enc -aes-256-cbc -salt -in secrets.tar.gz -out secrets.tar.gz.enc`
1. Host it somewhere
1. Set `SECRETS_BUNDLE_URL` and `SECRETS_BUNDLE_PASSPHRASE`
1. Deploy to heroku
