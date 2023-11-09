direnv not [dotenv](https://twitter.com/kaihendry/status/1721931150313087058)!

Actually direnv doesn't make sense in a CI pipeline.

https://github.com/aws-actions/aws-secretsmanager-get-secrets

https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions

<img src="https://s.natalian.org/2023-11-09/secrets-manager.png">

# Delivering secrets

1. Locally - via environment
2. In the pipeline - via environment (secrets normally protected)
3. At runtime - er... [not via environment](https://12factor.net/config)?!

## At runtime?!

Loading secrets at runtime from a secure parameter store is deemed the safest
way to do secrets. Since environments can be inspected by the AWS Web
console or via some exception.

> The issue here is the GetFunctionConfiguration permission is very broad. It
> is the only way to get the lambda config like runtime ect but is a very broad
> permission. Also the fact that envs are normally configured in your CI tool
> means you have another place where you store secret information which can
> complicate compliance processes if you don't use AWS for that.

The big problem with fetching secrets at runtime is:

1. Setting up the permissions
2. The expense of doing a call everytime the code is invoked (code complexity and AWS charges!)
3. Setting up caching to mitigate point 2
