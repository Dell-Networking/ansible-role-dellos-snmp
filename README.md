# SNMP role for Dell EMC Networking OS
The SNMP role facilitates configuration of global SNMP attributes. This role supports SNMP server attribute configurations including user, group, community, location, traps, and so on. This role is abstracted for dellos9, dellos6, and dellos10.


## Installation

    ansible-galaxy install Dell-Networking.dellos-snmp

## Requirements
This role requires an SSH connection for connectivity to your Dell EMC Networking device. You can use any of the built-in Dell EMC Networking OS connection variables, or the ``provider`` dictionary.

## Role variables
Any role variable with a corresponding state variable set to absent negates the configuration of that variable. For variables with no state variable, setting an empty value for the variable negates the corresponding configuration.

> **NOTE**: The variables and values are case-sensitive.

#### ``dellos_snmp`` keys

| Key | Type | Notes |
|--|--|--|
| ``snmp_contact`` | string | Configures SNMP contact information. |
| ``snmp_server_vrf`` | boolean: true, false* | Enables SNMP-SERVER VRF globally. |
| ``snmp_location`` | string | Configures SNMP location information. |
| ``snmp_community`` | list | Configures the SNMP community information (see snmp_community.* keys for each list item). |
| ``snmp_community.name`` | string (required) | Configures the SNMP community string. |
| ``snmp_community.access_mode`` | string, choice(ro, rw) | Configures the access mode for the community. |
| ``snmp_community.state`` | string, choice(absent, present*) | If set to absent, deletes the SNMP community information. |
| ``snmp_host`` | list | Configures SNMP hosts to receive SNMP traps (see snmp_host.* keys for each list item) — key is not supported for dellos10 devices. |
| ``snmphost.ip`` | string | Configures IP address of the SNMP trap host in dellos6 devices. |
| ``snmp_host.ipv4`` | string | Configures IPV4 address for the SNMP trap host in dellos9 devices. |
| ``snmp_host.ipv6`` | string | Configures IPV6 address for the SNMP trap host in dellos9 devices. |
| ``snmp_host.communitystring`` | string | Configures SNMP community string of the trap hosts. |
| ``snmp_host.udpport`` | string | Configures UDP number of the SNMP trap host — value range is 0-65535 for dellos9 devices. |
| ``snmp_host.version`` | string (required) | Specifies SNMP version of the host — it can be either 1 or 2c or 3 in dellos9 devices. |
| ``snmp_host.vrf`` | list | Configures SNMP VRF traps for the SNMP host — specifies list of VRF names. |
| ``snmp_host.state`` | string, choice(absent, present*) | If set to absent, deletes the SNMP trap host. |
| ``snmp_traps`` | list | Configures SNMP traps (see snmp_traps.* keys for each list item) — key is not supported on dellos10 devices. |
| ``snmp_traps.name`` | string | Enables SNMP traps. |
| ``snmp_traps.state`` | string, choice(absent, present*) | If set to absent, deletes the SNMP trap. |
| ``snmp_engine_id`` | string | Configures SNMPv3 engineID for the local agent — key is not supported on dellos6 and dellos10 devices. |
| ``snmp_view`` | list | Configures SNMPv3 view information (see snmp_view.* keys for each list item) — key is not supported on dellos10 and dellos6 devices. |
| ``snmp_view.name`` | string | Configures view name — can be up to 20 characters maximum. |
| ``snmp_view.oid_subtree`` | integer | Configures OID subtree for the view. |
| ``snmp_view.include`` | boolean(true, false) | Specifies whether the MIB family has to be included or excluded from the view. |
| ``snmp_user`` | list | Configures SNMP users for each group name (see snmp_user.* for each list item) — key is not supported on dellos6 and dellos10 devices. |
| ``snmp_user.name`` | string (required) | Configures SNMP user name. |
| ``snmp_user.group_name`` | string(required) | Configures SNMP group name for the user. |
| ``snmp_user.version`` | string, choice(1, 2c, 3) (required) | Configures user entry with the specified SNMP version — can be either 1 or 2c or 3 in dellos9 devices. |
| ``snmp_user.access_list`` | dict | Configures access list details — if any of the fields are defined, it is required to configure or negate. |
| ``snmp_user.access_list.access`` | string | Configures access list associated with the user. |
| ``snmp_user.access_list.ipv6`` | string | Configures ipv6 access-list associated with the user. |
| ``snmp_user.encryption`` | boolean(true, false*) | Specifies encryption for SNMP user if set to true on dellos9 devices. |
| ``snmp_user.auth_algorithm`` | string, choice(md5, sha) | Configures authorization algorithm for the SNMP user. |
| ``snmp_user.auth_pass`` | string | Configures authentication password for the user. |
| ``snmp_user.state`` | string, choice(absent, present*) | If set to absent, deletes the SNMP user. |
| ``snmp_group`` | list | Configures SNMP groups (see snmp_group.* for each list item) — key is not supported on dellos6 and dellos10 devices. |
| ``snmp_group.name`` | string (required) | Configures SNMP group name. |
| ``snmp_group.version`` | string (required) | Configures group entry with the specified SNMP version — can be either 1 or 2c or 3 in dellos9 devices. |
| ``snmp_group.access_list`` | dict | Configures access list entries for the group — if any of the fields are defined, it is required to configure or negate. |
| ``snmp_group.access_list.access`` | string | Configures access list associated with the group. |
| ``snmp_group.access_list.ipv6`` | string | Configures IPv6 access-list associated with the group. |
| ``snmp_group.view`` | dict | Configues view entries for the group — if any of the fields are defined, it is required to configure or negate. |
| ``snmp_group.view.notify`` | string | Configures notify view associated with the group. |
| ``snmp_group.view.read`` | string | Configures read view associated with the group. |
| ``snmp_group.view.write`` | string | Configures write view associated with the group. |
| ``snmp_group.context`` | list | Configures context list entries (see snmp_group.context.* for each list item). |
| ``snmp_group.context.context_name`` | string | Configures snmp-group entries with specified context name. |
| ``snmp_group.context.access_list`` | dict | Configures access list entries for the group with context. |
| ``snmp_group.context.access_list.access`` | string | Configures access-list associated with the group. |
| ``snmp_group.context.access_list.ipv6`` | string | Configures IPv6 access-list associated with the group. |
| ``snmp_group.context.view`` | dict | Configues view entries for the group with context. |
| ``snmp_group.context.view.notify`` | string | Configures notify view associated with the group. |
| ``snmp_group.context.view.read`` | string | Configures read view associated with the group. |
| ``snmp_group.context.view.write`` | string | Configures write view associated with the group. |
| ``snmp_group.context.state`` | choice(absent, present) | If set to absent, deletes the context entries with the group. |
| ``snmp_group.state`` | string, choice(absent, present*) | If set to absent, deletes the associated SNMP group. |


> **NOTE**: Asterisk (*) denotes the default value if none is specified. 

## Connection variables
Ansible Dell EMC Networking roles require the following connection information to establish communication with the nodes in your inventory. This information can exist in the Ansible group_vars or host_vars directories, or in the playbook itself.

| Key | Required | Choices | Description |
| -- | -- | -- | -- |
| host | yes | | Hostname or address for connecting to the remote device over the specified ``transport`` — value of this key is the destination address for the transport. |
| port | no | | Port used to build the connection to the remote device — if the value of this key does not specify the value, the value defaults to 22 |
| username | no | | Configures the username that authenticates the connection to the remote device. The value of this key authenticates the CLI login. If this key does not specify a value, the value of environment variable ANSIBLE_NET_USERNAME is used instead. |
| password | no | | Specifies the password that authenticates the connection to the remote device. If this key does not specify the value, the value of environment variable ANSIBLE_NET_PASSWORD is used instead. |
| authorize | no | yes, no*  | Instructs the module to enter Privileged mode on the remote device before sending commands. If this key does not specify the value, the value of environment variable ANSIBLE_NET_AUTHORIZE is used instead. If not specified, the device attempts to execute all commands in non-Privileged mode.|
| auth_pass | no | | Specifies the password to use if required to enter Privileged mode on the remote device. If ``authorize`` is set to no, this key is not applicable. If this key does not specify the value, the value of environment variable ANSIBLE_NET_AUTH_PASS is used instead. |
| transport | yes  | cli* | Configures the transport connection to use when connecting to the remote device. This key supports connectivity to the device over CLI (SSH).  |
| provider | no |  | Convenient method that passes all of the above connection arguments as a dictonary object. All constraints (such as required, choices) must be met either by individual arguments or values in this dictonary. |

> **NOTE**: Asterisk (*) denotes the default value if none is specified.

## Dependencies
The ``dellos-snmp`` role is built on modules included in the core Ansible code, version 2.2.0.

## Example playbook
The following example uses the dellos.dellos-snmp role to completely set up the SNMP server attributes. The example creates a ``hosts`` file with the switch details and corresponding variables. It writes a simple playbook that only references the dellos-snmp role. 

> **NOTE**: You automatically get access to all tasks to configure SNMP features by including this role.

#### Sample ``hosts`` file
 
    leaf1 ansible_host= <ip_address> ansible_net_os_name= <OS name(dellos9/dellos10/dellos6)>

#### Sample ``host_vars/leaf1``

    hostname: leaf1
    provider:
      host: "{{ hostname }}"
      username: xxxxx 
      password: xxxxx
      authorize: yes
      auth_pass: xxxxx 
      transport: cli
	  
    dellos_snmp:
      snmp_contact:  test
      snmp_location: chennai
      snmp_server_vrf: test
      snmp_community:
        - name: public
          access_mode: ro
          state: present
        - name: private
          access_mode: rw
          state: present
      snmp_host:
        - ipv6: 2001:4898:f0:f09b::2000
          version: "3"
          security_level: auth
          communitystring:
          udpport:
          state: absent
      snmp_traps:
        - name: config
          state: present
      snmp_engine_id: 1234567890
      snmp_view:
        - name: view_1
          oid_subtree: 2
          include: false
          state: absent
      snmp_user:
        - name: user_1
          group_name: grp1
          version: 3
          access_list:
            access: a1
            ipv6: ip1
          encryption: true
          auth_algorithm: md5
          auth_pass: 12345678
          state: present
      snmp_group:
        - name: group_1
          version: 2c
          access_list:
            access: a1
            ipv6: ip1
          state: absent
        - name: group_2
          version: 3
          security_level: priv
          access_list:
            access: a1
            ipv6: ip1
          context:
            - context_name: c1
              state: present
            - context_name: c2
              access_list:
                access: a1
              view:
                read: r1
              state: present 
          state: present

#### Simple playbook to setup SNMP ``leaf.yaml``

    - hosts: leaf1
      roles:
         - Dell-Networking.dellos-snmp

#### Then run with

    ansible-playbook -i hosts leaf.yaml

## License
Copyright © 2017 Dell EMC. All rights reserved.
 
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0.
 
Unless required by applicable law or agreed to in writing, software 
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
