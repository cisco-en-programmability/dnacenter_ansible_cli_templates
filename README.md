# Cisco DNA Center Ansible CLI Templates

This repo is for an Ansible Playbook that will use the Cisco DNA Center Ansible Modules to deploy CLI templates to network devices:

This Playbook will:

- Find out if Cisco DNA Center has an existing project with the pre-defined name, and create a new one if not
- Find the project id
- Create and commit a new template in the project
- Identify if the device to be configured is managed by Cisco DNA Center
- Find out the CLI Template deployment status

This playbook will require these vars files:
- "credentials.yml" or "vault.yml" to provide the Cisco DNA Center user credentials
- "params.yml" to provide:
    - Project name
    - Template name
    - Device name
    - CLI template
    
Sample "params.yml" file:
```
project_name: Ansible_Project
template_name: Ansible_Template
device_name: PDX-RN
cli_template: |
  interface loopback200
   description created_by_ansible
   ip address 10.10.10.10 255.255.255.255
```

Sample "credentials.yml" file:
```
dnac_host: your_Cisco_DNA_Center
username: username
password: password
```

**Cisco Products & Services:**

- Cisco DNA Center

**Tools & Frameworks:**

- Ansible environment to run the playbook. 
  Information about how to get started with the Cisco DNA Center Ansible collection may be found here:
  https://galaxy.ansible.com/cisco/dnac, or here: https://github.com/cisco-en-programmability/dnacenter-ansible
- Cisco DNA Center Python SDK: https://github.com/cisco-en-programmability/dnacentersdk

**Usage**

Sample output:
```
(venv) gzapodea@GZAPODEA-M-G7G6 dnacenter_ansible_cli_templates % ansible-playbook  ansible_cli_templates.yml

PLAY [Ansible CLI Templates] ****************************************************************************************************************************************************************************

TASK [Get start timestamp from the system] **************************************************************************************************************************************************************
changed: [localhost]

TASK [Print playbook start timestamp] *******************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Playbook start time: 2022-01-26T14-27-54"
}

TASK [Verify if existing project with the name: Ansible_Project] ****************************************************************************************************************************************
ok: [localhost]

TASK [Project not found] ********************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Project with the name: Ansible_Project, not found"
}

TASK [Create new project] *******************************************************************************************************************************************************************************
changed: [localhost]

TASK [Print create project task id] *********************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Create a new project, task id is: befe9e76-1a59-43fe-ac08-f489492258a7"
}

TASK [Sleep for 10 seconds to create project and continue with play] ************************************************************************************************************************************
ok: [localhost]

TASK [Get the project id] *******************************************************************************************************************************************************************************
ok: [localhost]

TASK [Parse project id] *********************************************************************************************************************************************************************************
ok: [localhost]

TASK [Print project id] *********************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Project id is: ca6530ca-9091-4dd3-9cb6-019dfc2b0feb"
}

TASK [Create new CLI Template with the name: Ansible_Template-2022-01-26T14-27-54] **********************************************************************************************************************
ok: [localhost]

TASK [Parse the create template task id] ****************************************************************************************************************************************************************
ok: [localhost]

TASK [Print create template task id] ********************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Create a new template, task id is: afa0142f-65c2-41ad-8a0b-5f697631755a"
}

TASK [Sleep for 10 seconds to create template and continue with play] ***********************************************************************************************************************************
ok: [localhost]

TASK [Get the template id] ******************************************************************************************************************************************************************************
ok: [localhost]

TASK [Parse the template id] ****************************************************************************************************************************************************************************
ok: [localhost]

TASK [Print template id] ********************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Template id is: ff7f15aa-f38c-49e8-9e09-328bf7a6fe4a}"
}

TASK [Commit template] **********************************************************************************************************************************************************************************
ok: [localhost]

TASK [Sleep for 5 seconds to commit template and continue with play] ************************************************************************************************************************************
ok: [localhost]

TASK [Verify if the device PDX-RN is managed by Cisco DNA Center] ***************************************************************************************************************************************
ok: [localhost]

TASK [Device not found] *********************************************************************************************************************************************************************************
skipping: [localhost]

TASK [Deploy template Ansible_Template to device PDX-RN] ************************************************************************************************************************************************
ok: [localhost]

TASK [Parse the deployment task id] *********************************************************************************************************************************************************************
ok: [localhost]

TASK [Print template deployment task id] ****************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Deployment task id: 3a9b68cf-81e6-456e-a12c-937f04cd6521"
}

TASK [Sleep for 10 seconds to deploy template and continue with play] ***********************************************************************************************************************************
ok: [localhost]

TASK [Verify the template deployment result] ************************************************************************************************************************************************************
ok: [localhost]

TASK [Parse the deployment task result] *****************************************************************************************************************************************************************
ok: [localhost]

TASK [Print successful template deployment result] ******************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Template deployment was successful"
}

TASK [Print unsuccessful template deployment result] ****************************************************************************************************************************************************
skipping: [localhost]

TASK [Get end timestamp from the system] ****************************************************************************************************************************************************************
changed: [localhost]

TASK [Print timestamp] **********************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Playbook end time: 2022-01-26T14-28-43"
}

PLAY RECAP **********************************************************************************************************************************************************************************************
localhost                  : ok=29   changed=3    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   

(venv) gzapodea@GZAPODEA-M-G7G6 dnacenter_ansible_cli_templates % 


```


**License**

This project is licensed to you under the terms of the [Cisco Sample Code License](./LICENSE).


