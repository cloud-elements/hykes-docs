# Cloud Requirements

## Hardware Requirements

### Minimum:
```
|-- all
  |-- 1x app (2 vCPU, 8GB RAM, 32GB HDD)
  |-- 1x cache (1 vCPU, 4GB RAM, 32GB HDD)
  |-- 1x database (2 vCPU, 8GB RAM, 64GB SSD)
  |-- 1x loadbalance (1 vCPU, 1GB RAM, 32GB HDD)
  |-- 1x logstore (1 vCPU, 4GB RAM, 96GB HDD)
  |-- 1x logpipe (1 vCPU, 2GB RAM, 32GB HDD)
  |-- 1x message (1 vCPU, 2GB RAM, 32GB SSD)
```

### Recommended:
```
|-- all
  |-- 3x app (4 vCPU, 8GB RAM, 64GB SSD)
  |-- 2x cache (1 vCPU, 4GB RAM, 64GB SSD)
  |-- 2x database (4 vCPU, 16GB RAM, 96GB SSD)
  |-- 2x loadbalance (1 vCPU, 2GB RAM, 64GB SSD)
  |-- 3x logstore (2 vCPU, 8GB RAM, 96GB SSD)
  |-- 2x logpipe (2 vCPU, 4GB RAM, 32GB SSD)
  |-- 2x message (1 vCPU, 4GB RAM, 64GB SSD)
```

### Consolidation:
It is possible to combine multiple roles onto fewer distinct servers. This approach is called
consolidation and can be approached in a myriad of ways, including combining all roles onto
single servers (which can still scale horizontally).

#### Minimum:
```
|-- 1x all (8 vCPU, 48GB RAM, 256GB HDD)
```

#### Recommended:
```
|-- 3x all (16 vCPU, 64GB RAM, 512GB SSD)
```

## OS Requirements
All servers are assumed to have Ubuntu 14.04, CentOS 7, or RHEL 7 installed. Additionally, it is
expected that a static IP be assigned, desired hostname configured, and at least one non-root admin
account to perform all operations. A single virtual IP is needed for a high-availability load
balancer setup.

## Firewall Requirements
Software firewalls (i.e. iptables) are used to provide baseline protection. Hardware firewalls
can be used in addition to, or in lieu of, software firewalls, providing the following rules
are met:

### Inbound:
```
|-- all (22 open to public)
  |-- app (8080 open to app/loadbalance)
  |-- cache (6379/11211 open to app/cache)
  |-- database (5432 open to app/database)
  |-- loadbalance (80/443 open to public, 81 open to app/loadbalance)
  |-- logstore (9200/9300 open to logpipe/logstore/loadbalance)
  |-- logpipe (none)
  |-- message (2181/9092 open to app/message)
```

## DNS Requirements

### Public endpoints:
| Record                  | Required | Example             | Purpose
| ----------------------- | -------- | ------------------- | -------
| `{{base_fqdn}}`         | No       | example.com         | Redirect `{{base_fqdn}}` traffic to `console.{{base_fqdn}}`
| `api.{{base_fqdn}}`     | Yes      | api.example.com     | REST endpoint
| `console.{{base_fqdn}}` | Yes      | console.example.com | UI endpoint

> __NOTE:__ All public endpoint records should point to the IP of `loadbalance[0]`

### Server endpoints:
| Record                         | Required | Example
| ------------------------------ | -------- | ------------------------
| `app[n].{{base_fqdn}}`         | Yes      | app0.example.com
| `cache[n].{{base_fqdn}}`       | Yes      | cache0.example.com
| `database[n].{{base_fqdn}}`    | Yes      | database0.example.com
| `loadbalance[n].{{base_fqdn}}` | Yes      | loadbalance0.example.com
| `logstore[n].{{base_fqdn}}`    | Yes      | logstore0.example.com
| `logpipe[n].{{base_fqdn}}`     | Yes      | logpipe0.example.com
| `message[n].{{base_fqdn}}`     | Yes      | message0.example.com

> __NOTE:__ All server endpoint records should point to the IP of the server the record refers to

## Certificate Requirements
TLS/SSL certificates are required to protect all [public endpoints](#public-endpoints). This can be
accomplished via one of three approaches:

### Wildcard Certificate:
* Wildcard certificate for `{{base_fqdn}}`

### SAN Certificate:
* SAN certificate for `api.{{base_fqdn}}`, `console.{{base_fqdn}}`, and optionally `{{base_fqdn}}`
(see [public endpoints](#public-endpoints) for details)

### Single Certificates:
* Single certificate for `api.{{base_fqdn}}`
* Single certificate for `console.{{base_fqdn}}`
* Optionally, a single certificate for `{{base_fqdn}}` (see [public endpoints](#public-endpoints)
for details)
