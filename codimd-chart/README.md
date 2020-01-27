# CodiMD

[CodiMD](https://codimd.org) is a realtime, multiplatform collaborative markdown note editor.

## Introduction

This chart bootstraps a [CodiMD](https://github.com/codimd/container) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

It also packages the [PostgreSQL](https://github.com/kubernetes/charts/tree/master/stable/postgresql) which is required for bootstrapping a PostgreSQL deployment for the database requirements of the CodiMD application.

## Prerequisites

- Kubernetes 1.8+
- PV provisioner support in the underlying infrastructure

## Install

```console
$ helm install .
```

## Configuration

The following configurations may be set. It is recommended to use values.yaml for overwriting the codimd config.

Parameter | Description | Default
--------- | ----------- | -------
`replicaCount` | How many replicas to run. | 1
`image.repository` | Name of the image to run, without the tag. | [codimd/server](https://github.com/codimd/server)
`image.tag` | The image tag to use. | 1.3.2-alpine
`image.pullPolicy` | The kubernetes image pull policy. | IfNotPresent
`service.name` | The kubernetes service name to use. | codimd
`service.type` | The kubernetes service type to use. | ClusterIP
`service.port` | Service port. | 3000
`ingress.enabled` | If true, Ingress will be created | `false`
`ingress.annotations` | Ingress annotations | `[]`
`ingress.hosts` | Ingress hostnames | `[]`
`ingress.tls` | Ingress TLS configuration (YAML) | `[]`
`resources` | Resource requests and limits | `{}`
`persistence.enabled` | If true, Persistent Volume Claim will be created | `true`
`persistence.accessModes` | Persistent Volume access modes | `[ReadWriteOnce]`
`persistence.annotations` | Persistent Volume annotations | `{}`
`persistence.existingClaim` | Persistent Volume existing claim name | `""`
`persistence.size` | Persistent Volume size | `2Gi`
`persistence.storageClass` | Persistent Volume Storage Class |  `unset`
`storage.s3.enabled` | Enable S3 Storage | ` false`
`storage.s3.region` | The region for the S3 API | `""`
`storage.s3.bucket` | The bucket name to use with S3 | `""`
`storage.amazon.enabled` | Enable the use of AWS S3 | `false`
`storage.amazon.access_key_id` | AWS S3 Access Key | `""`
`storage.amazon.secret_access_key` | AWS S3 Secret | `""`
`storage.minio.enabled` | Enable the use of Minio S3 | `false`
`storage.minio.access_key` | Minio S3 Access Key | `""`
`storage.minio.secret_access_key` | Minio S3 Secret | `""`
`storage.minio.endpoint` | Minio S3 Endpoint URL | `""`
`storage.minio.port` | Minio S3 Port for URL | `9000`
`storage.minio.secure` | Minio S3 Use SSL | `true`
`storage.azure.enabled` | Enable Azure Blob Storage | `false`
`storage.azure.connection_string` | Azure Connection String | `""`
`storage.azure.container` | Azure Container name (automatically created if not exists) | `""`
`storage.imgur.enabled` | Enable imgur Storage | `false`
`storage.imgur.clientid` | Clientid for imgur API | `""`
`storage.lutim.enabled` | Enable Lutim storage | `false`
`storage.lutim.url` | Lutim URL | `""`
`auth.email.enabled` | Allow E-Mail signin | `true`
`auth.email.allow_register` | Allow registration with E-Mails| `true`
`extraVars` | CodiMD's extra environment variables | `[]`
`podAnnotations` | Pod annotations | `{}`
`sessionSecret` | CodiMD's session secret | `""` (Randomly generated)
`postgresql.install` | Enable PostgreSQL as a chart dependency | `true`
`postgresql.imageTag` | The image tag for PostgreSQL | `9.6.2`
`postgresql.postgresUser` | PostgreSQL User to create | `codimd`
`postgresql.postgresHost` | PostgreSQL host (if `postgresql.install == false`)  | `nil`
`postgresql.postgresPassword` | PostgreSQL Password for the new user | random 10 characters
`postgresql.postgresDatabase` | PostgreSQL Database to create | `codimd`

### Use behind a TLS reverse proxy

If you use CodiMD behind a reverse proxy that does TLS decryption and forwards traffic in plain HTTP, you have to enable the following variables in your `values.yaml`:

```yaml
extraVars:
  - name: CMD_DOMAIN
    value: change.this.to.your.own.fqdn
  - name: CMD_PROTOCOL_USESSL
    value: "true"
  - name: CMD_URL_ADDPORT
    value: "false"
```
