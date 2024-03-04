# Using deploy api

deploy hook usage:

https://github.com/acmesh-official/acme.sh/wiki/deployhooks

## Deploy the cert to your AliCDN account

You must specify the aliyun account credentials in order to deploy the certificate, optionally specify the prefix of your domain if you use wildcard in cdn domain, through the following environment variables:
```sh
export DEPLOY_CDN_Ali_Key="AK"
export DEPLOY_CDN_Ali_Secret="SK"
export DEPLOY_CDN_Ali_Prefix=""
```

After the first deployment, these values will be stored in your domain deploy conf. You may now deploy the certificate like this:

```sh
acme.sh --deploy -d example.com --deploy-hook cdn_ali
```

If your cdn domain is cdn.example.com and cert domain is also cdn.example.com, you can leave the prefix empty in deployment: 
```sh
export DEPLOY_CDN_Ali_Key="AK"
export DEPLOY_CDN_Ali_Secret="SK"
export DEPLOY_CDN_Ali_Prefix=""
acme.sh --deploy -d cdn.example.com --deploy-hook cdn_ali
```

If your cdn domain is cdn.example.com but cert domain is example.com(subject alternative names: example.com,\*.example.com), you must specify the prefix in deployment: 
```sh
export DEPLOY_CDN_Ali_Key="AK"
export DEPLOY_CDN_Ali_Secret="SK"
export DEPLOY_CDN_Ali_Prefix="cdn."
acme.sh --deploy -d example.com --deploy-hook cdn_ali
```

If your cdn domain is \*.example.com (added wildcard domain in AliCDN console) but cert domain is example.com(subject alternative names: example.com,\*.example.com), you must specify the prefix only a dot(.) in deployment: 
```sh
export DEPLOY_CDN_Ali_Key="AK"
export DEPLOY_CDN_Ali_Secret="SK"
export DEPLOY_CDN_Ali_Prefix="."
acme.sh --deploy -d example.com --deploy-hook cdn_ali
```
