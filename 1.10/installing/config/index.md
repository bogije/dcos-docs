---
post_title: Configuration
menu_order: 0
---

Many [DC/OS installation methods](/docs/1.10/installing/) allow you to configure DC/OS using a YAML file (`config.yaml`). This file is generally provided to the installer during the first phase of DC/OS installation to generate customized immutable install artifacts.

**Warning:** Some installation methods automate the generation of `config.yaml` which may make it harder or impossible to manually modify (ex: AWS Cloud Formation templates).

**Important:** To modify the DC/OS configuration after installation, follow the [DC/OS upgrade process](/docs/1.10/installing/upgrading/) to upgrade to the same DC/OS version with a new `config.yaml`.

# Format

## Key-value pairs
The `config.yaml` file is formatted as a list of key-value pairs. For example:

```yaml
bootstrap_url: file:///opt/dcos_install_tmp
```

## Config blocks and lists
A config block is a group of settings. It consists of:

- A key followed by a colon (e.g. `agent_list:`). The key of the config block must be on its own line, with no leading space.
- A list of values formatted by using single dash (`-`) followed by a space; or an indented set of one or more key-value pairs. The indentation for each key-value pair must be exactly two spaces. Do not use tabs.
- Any number of empty lines or comment lines.

When a new config block appears in the file, the former config block is closed and the new one begins. A config block must only occur once in the file. For example:

```yaml
master_list:
- <master-private-ip-1>
- <master-private-ip-2>
- <master-private-ip-3>
```

## Comments
Comment lines start with a hash symbol (`#`). They can be indented with any amount of leading space.

Partial-line comments (e.g. `agent_list # this is my agent list`) are not allowed. They will be treated as part of the value of the setting. To be treated as a comment, the hash sign must be the first non-space character on the line. For example:

```yaml
master_list:
- <master-private-ip-1>
# here is a comment
- <master-private-ip-2>
- <master-private-ip-3>
```

## Dependencies
Some parameters are dependent on others. These dependent parameters are ignored unless all dependencies are specified. These dependencies are shown in the documentation by nesting within the parent. For example, `master_list` is required only if you specify ` master_discovery: static`.

# Basic settings

Most installations only need to set a few basic settings:

| Parameter                              | Description                                                                                                                                               |
|----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [agent_list](/docs/1.10/installing/config/reference/#agent_list)      | This parameter specifies a YAML nested list (`-`) of IPv4 addresses to your [private agent](/docs/1.10/overview/concepts/#private-agent-node) host names.                  |
| [bootstrap_url](/docs/1.10/installing/config/reference/#bootstrap_url)                          | This required parameter specifies the URI path for the DC/OS installer to store the customized DC/OS build files.                                         |
| [cluster_name](/docs/1.10/installing/config/reference/#cluster_name)                           | This parameter specifies the name of your cluster.    |
| [customer_key](/docs/1.10/installing/config/reference/#customer_key)                  | (Enterprise DC/OS Only) This parameter specifies the Enterprise DC/OS customer key.   |
| [exhibitor_storage_backend](/docs/1.10/installing/config/reference/#exhibitor_storage_backend)         | This parameter specifies the type of storage backend to use for Exhibitor.          |
| [master_discovery](/docs/1.10/installing/config/reference/#master_discovery)                          | This required parameter specifies the Mesos master discovery method.         |
| [public_agent_list](/docs/1.10/installing/config/reference/#public_agent_list)       | This parameter specifies a YAML nested list (-) of IPv4 addresses to your [public agent](/docs/1.10/overview/concepts/#public-agent-node) host names.    |
| [resolvers](/docs/1.10/installing/config/reference/#resolvers)       | This required parameter specifies a block of YAML nested list (`-`) of DNS resolvers for your DC/OS cluster nodes.   |
| [security](/docs/1.10/installing/config/reference/#security)                           | (Enterprise DC/OS Only) This parameter specifies the security mode: disabled, permissive, strict.  |
| [ssh_port](/docs/1.10/installing/config/reference/#ssh_port)                           | This parameter specifies the port to SSH to, for example 22.          |
| [ssh_user](/docs/1.10/installing/config/reference/#ssh_user)                           | This parameter specifies the SSH username, for example `centos`.     |
| [superuser_password_hash](/docs/1.10/installing/config/reference/#superuser_password_hash)            | (Enterprise DC/OS Only) This required parameter specifies the hashed superuser password.      |
| [superuser_username](/docs/1.10/installing/config/reference/#superuser_username)               | (Enterprise DC/OS Only) This required parameter specifies the user name of the superuser.    |
| [use_proxy](/docs/1.10/installing/config/reference/#use_proxy)        | This parameter specifies whether to enable the DC/OS proxy.     |


# Further reading

- For a full list of configuration options, see the [Configuration Reference](/docs/1.10/installing/config/reference/).
- For a list of example configurations, see [Configuration Examples](/docs/1.10/installing/config/examples/).