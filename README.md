# The Unicorn Factory Site

## Adding a portfolio

Simple add it into "_posts" directory

Refer to the existing entries.

### Image Specs

* For best results, must be at least 900x650

## Building

### Install all dependencies

Because this is a ruby site you need to install all the dependencies

```bash
bundle install
```

### Install the server

```bash
jekyll serve
```

## SSL Certificate Maintenance

### Run the letsencrypt scripts

Run the letsencrypt scripts and generate the certificate (they are in [nolim1t/docker-letsencrypt](https://github.com/nolim1t/docker-letsencrypt))

#### Configuration

**S3 Bucket Name** ssl-challenge.theunicornfactory.is

### Copy the certificate from the container to local file system

If it doesn't exist locally

```bash
docker cp CONTAINERNAME:/etc/letsencrypt/archive/DOMAINNAME .
```

### Upload the certificates

Where **cert1.pem** is the certificate, **privkey1.pem** is the private key, **chain1.pem** is the certificate chain, and **YYYYMMDDHHMM** is the timestamp.

```bash
aws --profile=uftechadmin \
--server-certificate-name=theunicornfactoryYYYYMMDDHHMM \
--certificate-body=file://./cert1.pem \
--private-key=file://./privkey1.pem \
--certificate-chain=file://./chain1.pem \
--path=/cloudfront/
```

### Go into Cloudfront control panel

Go into control panel and switchover the certificate.

Optionally you should delete the old certificate run you're done.
