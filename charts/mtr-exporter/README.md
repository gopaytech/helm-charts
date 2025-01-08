# mtr-exporter Helm Chart

Installs the [mtr-exporter](https://github.com/mgumz/mtr-exporter)

## Get Repository Info

```shell
helm repo add gopaytech https://gopaytech.github.io/helm-charts
helm repo update
```

## Install Chart

```shell
helm show values gopaytech/mtr-exporter > default.yaml
# adjust the default.yaml
helm install <release-name> gopaytech/mtr-exporter -f default.yaml [flags]
```

## Jobs Configuration

See [jobs-file-syntax](https://github.com/mgumz/mtr-exporter?tab=readme-ov-file#jobs-file-syntax) for more detail

```yaml
jobs:
  globalConfig:
    schedule: "@every 60s"
    flags: "--tcp --port 443 -c 10"
  config:
    9.9.9.9:
      schedule: "@every 120s"
      flags: "-I ven1 -n"
    example.com: 
      schedule: "@every 45s"
      flags: "-I ven2 -n"
    foobar.io: {}
```

Will be resulting in

```plaintext
9.9.9.9 -- @every 120s -- -I ven1 -n 9.9.9.9
example.com -- @every 45s -- -I ven2 -n example.com
foobar.io -- @every 60s -- --tcp --port 443 -c 10 foobar.io
```
