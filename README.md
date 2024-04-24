# fortiadc-ansible-roles

## Descriptions

My collections (?) of Fortinet's FortiADC Ansible roles. All of them based on FortiADC HTTP REST API, utilized by `ansible.builtin.uri` module.

## List of Roles

| Role Name                              | Repository                                                                                  | Workflow                                                                                                                                   |
|------------------------|---------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| ndkprd.fortiadc_backup                 | [Link](https://github.com/ndkprd/ansible-role-fortiadc-backup)                        | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-backup/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-backup/actions/workflows/release.yaml)
| ndkprd.fortiadc-dns-policy             | [Link](https://github.com/ndkprd/ansible-role-fortiadc-dns-policy)                    | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-dns-policy/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-dns-policy/actions/workflows/release.yaml) |
| ndkprd.fortiadc-dns-zones              | [Link](https://github.com/ndkprd/ansible-role-fortiadc-dns-zones)                     | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-dns-zones/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-dns-zones/actions/workflows/release.yaml) |
| ndkprd.fortiadc-glb-data-centers       | [Link](https://github.com/ndkprd/ansible-role-fortiadc-glb-data-centers)              | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-glb-data-centers/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-glb-data-centers/actions/workflows/release.yaml) |
| ndkprd.fortiadc-glb-hosts              | [Link](https://github.com/ndkprd/ansible-role-fortiadc-glb-hosts)                     | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-glb-hosts/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-glb-hosts/actions/workflows/release.yaml) |
| ndkprd.fortiadc-glb-servers            | [Link](https://github.com/ndkprd/ansible-role-fortiadc-glb-servers)                   | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-glb-servers/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-glb-servers/actions/workflows/release.yaml) |
| ndkprd.fortiadc-glb-vs-pools           | [Link](https://github.com/ndkprd/ansible-role-fortiadc-glb-vs-pools)                  | [![Release](https://github.com/ndkprd/ansible-role-fortiadc-glb-vs-pools/actions/workflows/release.yaml/badge.svg)](https://github.com/ndkprd/ansible-role-fortiadc-glb-vs-pools/actions/workflows/release.yaml) |

## Roles Dependency

Because of FortiADC nature, some roles is dependent to another, kinda looks like this:

```
glb-data-centers <-- glb-servers <-- glb-vs-pools <-- glb-hosts
dns-policy <-- glb-hosts
dns-policy <-- dns-zones
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

Some limitation that I'd like to tackle in the future:
- I've only tested these roles against FortiADC running firmware 7.0;
- Each single file in `tasks/` except `main.yaml` basically act like their own module, which makes these roles kinda have LOTS of tasks especially if you have lots of resource entries. And since I'm looping them using `include_tasks`, I haven't found a real good way to run the tasks in parallel.

## About Tags

Almost all roles have tasks tagged with `debug` on them, which can be used to print out the value before and after each "action" tasks (usually either POST or PUT). If you already sure, you can skip them with `--skip-tags debug` args.
