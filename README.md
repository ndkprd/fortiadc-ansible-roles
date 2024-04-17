# fortiadc-ansible-roles

My collections (?) of Fortinet's FortiADC Ansible roles. All of them based on FortiADC HTTP REST API, utilized by `ansible.builtin.uri` module.

## List of Roles

| Role Name                              | Repository                                                                                  | Workflow                                                                                                                                   |
|------------------------|---------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| ndkprd.fortiadc-dns-policy             | [Link](https://github.com/ndkprd/ansible-role-fortiadc-dns-policy)                    | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-dns-policy/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-dns-policy/actions/workflows/release.yaml) |
| ndkprd.fortiadc-dns-zones              | [Link](https://github.com/ndkprd/ansible-role-fortiadc-dns-zones)                     | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-dns-zones/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-dns-zones/actions/workflows/release.yaml) |
| ndkprd.fortiadc-glb-data-centers       | [Link](https://github.com/ndkprd/ansible-role-fortiadc-glb-data-centers)              | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-glb-data-centers/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-glb-data-centers/actions/workflows/release.yaml) |
| ndkprd.fortiadc-glb-hosts              | [Link](https://github.com/ndkprd/ansible-role-fortiadc-glb-hosts)                     | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-glb-hosts/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-glb-hosts/actions/workflows/release.yaml) |
| ndkprd.fortiadc-glb-servers            | [Link](https://github.com/ndkprd/ansible-role-fortiadc-glb-servers)                   | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-glb-servers/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-glb-servers/actions/workflows/release.yaml) |
| ndkprd.fortiadc-glb-vs-pools           | [Link](https://github.com/ndkprd/ansible-role-fortiadc-glb-vs-pools)                  | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-glb-vs-pools/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-glb-vs-pools/actions/workflows/release.yaml) |

## Roles Dependency

The roles kinda dependent to each other, kinda looks like this:

```
glb-data-centers <-- glb-servers <-- glb-vs-pools <-- glb-hosts
dns-policy <-- glb-hosts
dns-policy <-- dns-zones
```

## About Tags

Almost all roles have tasks tagged with `debug` on them, which can be used to print out the value before and after each "action" tasks (usually either POST or PUT). If you already sure, you can skip them with `--skip-tags debug` args.