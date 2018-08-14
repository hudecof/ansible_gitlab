# Gitlab Omnibus

Install nad configure gitlab omnibus packages

## Requirements

Extenal roles:
  - `hudecof.filter-plugins`
 

## Role Variables

### Package variables

These variables are used t install the omnibus package. Mostly you do not need to change them.

- `gitlab_packages`: list of packages to install. For various distribution see **vars/os-{{ ansible_os_family }}.yml**
- `gitlab_install_packages` lisf of packages form gitlab repository to install. For various distribution see **vars/os-{{ ansible_os_family }}.yml**
- `gitlab_gpg` link to the GPG key
- `gitlab_config_file` is path the configuration file **gitlab.rb** For various distribution see **vars/os-{{ ansible_os_family }}.yml** 
- `gitlab_bin_ctl` is path the **giltab-ctl** binary. For various distribution see **vars/os-{{ ansible_os_family }}.yml**

### Configuration varables

There are 4 type of variables in the configuration file

- **hash** is dictionary, **key/value**, looks like `gitlab_rails['gitlab_shell_ssh_port'] = 22`
- **hash merge** is dictionary, but with nested keys, looks like `default['gitlab']['postgresql']['archive_mode'] = "off"`
- **function**, looks like `git_data_dirs({'default' => {'path' => '/var/opt/gitlab/git-data'}})`
- **scalar** is the standalone variable, looks like `external_url = 'https://source.cnc.sk'`

#### Configuration variables (hash)
For each **hash** type variable there is **gitlab_cfg_<hash_name>** variable in **defaults/mian.yml**. The value will be converted to the ruby langeuage format.

```
gitlab_cfg_gitlab_rails:
  gitlab_ssh_host: 'source.example.com'
  ldap_enabled: false
```

#### Configuration variables (hash merge)
For each **hash merge** type variable there is **gitlab_cfg_<hash_name>** variable in **defaults/mian.yml**. The value will be converted to the ruby langeuage code.


#### Configuration variables (scalar)

For scalars there is variable name **gitlab_cfg_scalar** which should be dict. **Key** is the scalar name, **value** will be converted the the ruby langurage code.

```
gitlab_cfg_scalar:
  external_url: 'https://source.example.com'
  pages_external_url: 'http://pages.example.com/'
```

#### Configuration variables (function)
For function there is variable name **gitlab_cfg_function** which should be dict. **Key** is the scalar name, **value** will be converted as firt paramters.

```
gitlab_cfg_function:
  git_data_dirs:
    default:
      path: '/var/opt/gitlab/git-data'
```

## Dependencies

- `hudecof.filter-plugins`

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: git
      roles:
         - hudecof.filter-plugins
         - hudecof.gitlab
           gitlab_cfg_scalar:
             external_url: 'https://source.example.com
           
## License

BSD

## Author Information

Peter Hudec