- Standardized location under the domain root used to publish metadata and configuration information for specific services and protocols.
- Usually at /.well-known/
- Easy words they put all the public configuration in a globally-agreed upon spot

---
## Example

| URI                               | Purpose                           |
| --------------------------------- | --------------------------------- |
| /.well-known/security.txt         | Security contact information      |
| /.well-known/openid-configuration | OpenID Connect configuration      |
| /.well-known/assetlinks.json      | Android digital asset association |
| /.well-known/mta-sts.txt          | SMTP MTA-STS policy               |
