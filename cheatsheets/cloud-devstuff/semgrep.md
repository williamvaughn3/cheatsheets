# SemGrep

![](https://github.com/semgrep/semgrep/raw/develop/images/semgrep-logo-light.svg)

> Opensource Static Analysis tool designed with automation and CI/CD integration

[Git](https://github.com/returntocorp/semgrep)  

[Semgrep.dev](https://semgrep.dev/explore)  

Cmd Line Scanner
Supports Multiple Rulesets: r2c-security-audit, r2c-ci, and many others
https://semgrep.dev/rulesets

In Dir...
`semgrep --config "p/r2c-security-audit`

## Custom Rules

```yaml
rules:
  - id: wildcard_permissions_s3
  pattern: |
    { "Id": "S3-Acct-Permissions",
       "Statement": [
        { "Effect": "Allow",
           Action: "s3:*"
          }
        ]
      }
message: match found
severity: WARNING

```


