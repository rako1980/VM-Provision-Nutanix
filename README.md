This ansible code deploys VMs in Nutanix environment. It leverages nutanix APIs. While working on Nutanix API, you would need to consider which API to use. The Prism Central uses api v3 while prism element uses api v2. While APIv2 is great, there are much more functionalities and things that can be done using APIv3. Further, nutanix recommends using api v3 wherever possible.
While working on automating the VM creation using Nutanix APIs, I find they lack the documentation on how certain things are done. But they have a great tool available in Nutanix API explorer for both v2 and v3 which you can use to check for desired API call. This automation task uses both apiv2 and apiv3. When I started, I only had an access through apiv2 (nutanix prism central), but certain things like VM creation with serial port, disk expansion etc is not available through apiv3. That is when I gained access to apiv3 and added the call to apiv3 to make the things that are missing on apiv2. If you start from scratch, I recommend to do everything using apiv3 as nutanix recommends.

I have presented this as an ansible role which includes number of tasks. The playbook to provision VM provision_vms.yml uses these tasks on this nutanix role
```
InfrastructureAsCode/
└── roles
    └── nutanix
        ├── defaults
        │   └── main.yml
        ├── playbooks
        │   └── provision_vms.yml
        ├── README.md
        ├── tasks
        │   ├── create_vm.yml
        │   ├── get_image_facts.yml
        │   ├── get_network_facts.yml
        │   ├── get_session_cookies.yml
        │   ├── get_vm_facts.yml
        │   ├── get_vm_ipaddress.yml
        │   └── load_credentials.yml
        └── templates
            ├── cloud_init.j2
            └── vm_specs.j2
```
All the defaults are provides in defaults.yml, which you can override with variable while calling the role.

It uses a ubuntu cloud vmdk available from Ubuntu https://cloud-images.ubuntu.com/bionic/current/. The cloudInit specs are provided in the cloud_init.j2 template.
If any questions shhot me an email or comments here. 

