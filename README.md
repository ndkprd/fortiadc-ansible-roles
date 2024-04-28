# fortiadc-ansible-roles

## Descriptions

My collections (?) of Fortinet's FortiADC Ansible roles. All of them based on FortiADC HTTP REST API, utilized by `ansible.builtin.uri` module.

## List of Roles

| Role Name                              | Repository                                                                                  | Workflow                                                                                                                                   |
|------------------------|---------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| ndkprd.fad_backup                 | [Link](https://github.com/ndkprd/ansible-role-fad-backup)                        | [![Release](https://github.com/ndkprd/ansible-role-fad-backup/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fad-backup/actions/workflows/release.yaml)
| ndkprd.fad_dns_policy             | [Link](https://github.com/ndkprd/ansible-role-fad-dns-policy)                    | [![Release](https://github.com/ndkprd/ansible-role-fad-dns-policy/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fad-dns-policy/actions/workflows/release.yaml) |
| ndkprd.fad_dns_zone              | [Link](https://github.com/ndkprd/ansible-role-fad-dns-zone)                     | [![Release](https://github.com/ndkprd/ansible-role-fad-dns-zone/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fad-dns-zone/actions/workflows/release.yaml) |
| ndkprd.fad_health_check          | [Link](https://github.com/ndkprd/ansible-role-fad-health-check)                  | [![Release](https://github.com/ndkprd/ansible-role-fad-health-check/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fad-health-check/actions/workflows/release.yaml)
| ndkprd.fad_glb_data_center       | [Link](https://github.com/ndkprd/ansible-role-fad-glb-data-center)              | [![Release](https://github.com/ndkprd/ansible-role-fad-glb-data-center/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fad-glb-data-center/actions/workflows/release.yaml) |
| ndkprd.fad_glb_host              | [Link](https://github.com/ndkprd/ansible-role-fad-glb-host)                     | [![Release](https://github.com/ndkprd/ansible-role-fad-glb-host/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fad-glb-host/actions/workflows/release.yaml) |
| ndkprd.fad_glb_servers            | [Link](https://github.com/ndkprd/ansible-role-fad-glb-servers)                   | [![Release](https://github.com/ndkprd/ansible-role-fad-glb-servers/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fad-glb-servers/actions/workflows/release.yaml) |
| ndkprd.fad_glb_vs_pool           | [Link](https://github.com/ndkprd/ansible-role-fad-glb-vs-pool)                  | [![Release](https://github.com/ndkprd/ansible-role-fad-glb-vs-pool/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fad-glb-vs-pool/actions/workflows/release.yaml) |

## Roles Dependency

Because of FortiADC nature, some roles is dependent to another, kinda looks like this:

```
glb_data_centers < glb_servers < glb_vs_pools < glb_hosts
dns_policy < glb_hosts
dns_policy < dns_zones
```

## IaC Implementation

To implement Infrastructure as Code for FortiADC using these roles, you can just directly use the right-most roles from the above dependency diagram, since it will automatically run the dependent role(s) first.

Though to be noted, since I composed these roles for my personal (and corporate) use, I make them to my need, hence why I've only composed DNS-related configuration from FortiADC and not SLB.

## About Idempotency

I tried to make the roles as idempotent as possible. I probably missed some of them (just create an issue if you found one), but most of the time the tasks works like this:

```
if resource is undefined:
    do POST task
if resource is defined AND existing_resource_value != desired_resource_value:
    do PUT task
else
    skip tasks
```

## Limitation

I've only tested these roles against FortiADC running firmware 7.0

## About Tags

Almost all roles have tasks tagged with `debug` on them, which can be used to print out the value before and after each "action" tasks (usually either POST or PUT). If you already sure, you can skip them with `--skip-tags debug` args.
