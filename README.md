# ROLE dginhoux.repos



## DESCRIPTION

This role configure linux repos for apt/yum/dnf packages management systems.<br /><br />
It use two principes for setups repos : <br />
* with `repos_list` by settings each parameters with hand
* with `repos_dl_pkgs_list` for installing from pkg (like rpmfusion who provide rpm file)



## REQUIREMENTS

#### SUPPORTED PLATFORMS

| Platform | Versions |
|----------|----------|
| Debian | all |
| EL | all |
| Fedora | all |
| Ubuntu | all |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.repos
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.repos dginhoux.repos
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.repos
      ansible.builtin.include_role:
        name: dginhoux.repos
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
repos_list:
  debian:
    buster:
      - name: debian-system
        repo: deb https://ftp.debian.org/debian buster main contrib non-free
        state: present
        filename: debian-system
        key_install: "True"
        key_state: present
        key_url: http://ftp.debian.org/debian/dists/buster/Release.gpg
  fedora:
    "36":
      - name: fedora
        description: Fedora $releasever - $basearch
        # baseurl: http://download.example/pub/fedora/linux/releases/$releasever/Everything/$basearch/os/
        metalink: https://mirrors.fedoraproject.org/metalink?repo=fedora-$releasever&arch=$basearch
        file: fedora
        enabled: "yes"
        gpgcheck: "yes"
        gpgkey: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-$releasever-$basearch
        skip_if_unavailable: "no"

repos_dl_pkgs_list:
  fedora:
    "36":
      - name: rpmfusion-free-release
        url: https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-36.noarch.rpm
      - name: rpmfusion-nonfree-release
        url: https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-36.noarch.rpm
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`


## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
