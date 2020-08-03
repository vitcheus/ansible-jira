# ansible-jira

Ansible role for install and configure [jira](https://www.atlassian.com/software/jira)

Limitation
----------

1. This role not install `java` you must first install them yourself
2. If you want to use revers proxy `apache` or `nginx` you must first install them yourself
3. If you want to use an external DB such as (Mysql/PostgreSQL) install the selected DB before the run role
4. This role not manage selinux permission

Requirements
------------
Tested on RHEL 7, CentOS 7/8

* ansible 2.8 or above
* java SDK 8 or 11

Role Variables
--------------
**It is not necessary to use all these variable blocks, you can use only the config options you really need.** 

Available variables are be listed below, along with default values. See [defaults/main.yml](defaults/main.yml).

You can change all variables by group_vars or host_vars

| Variable name | Required* | Description | Default Value |
| :---: | :---: | :---: | :---: |
| `jira_version` | **Yes** | Version of the installing jira software | 7.4.1 |
| `jira_manage_user` | **No** | Should this role manage the jira user? | true |
| `jira_user` | **No** | OS user name | jira |
| `jira_group` | **No** | OS group name | jira |
| `jira_database_type`| **Yes** | type of using database  | "postgres" |
| `jira_session_timeout` | **No** | session duration | 300 |
| `jira_bin_path` | **No** | jira binary dir | /opt/atlassian/jira |
| `jira_data_path` | **No** | jira data dir | /opt/atlassian/application-data/jira |
| `jira_jvm_minimum_memory` | **No** | JVM min memory | 1024m |
| `jira_jvm_maximum_memory` | **No** | JVM max memory | 2048m |

If you want use reverse proxy for jira you must set additional setting

| Variable name | Required* | Description | Default Value |
| :---: | :---: | :---: | :---: |
| `jira_catalina_connector_proxyname` | **Yes** | fqdn proxy host name | "" |
| `jira_catalina_connector_scheme` | **No** | used protocol | http |
| `jira_catalina_connector_proxyport` | **No** | used proxy port | depends on scheme(80 or 443) |
| `jira_catalina_connector_secure` | **No** | used secure connection | depends on scheme |
| `jira_catalina_context_path` | **No** | web path for jira | / |

****Required*** - if "yes", you need to set this parameter under your conditions.

Dependencies
------------
 
Example Playbook
------------

```yml
- name: Install Jira
  hosts: 
    - jira.example.com
  become: yes
  become_method: sudo
  roles:
    - vitcheus.jira
  vars:
    confuence_version: "8.11.0"
    confuence_manage_user: true
    jira_user: jira
    jira_jvm_maximum_memory: "4096m"
    jira_catalina_connector_proxyname: jira.example.com
    jira_catalina_connector_scheme: "https"
    jira_data_path: "/data/jira"
```