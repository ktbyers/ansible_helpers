# ansible_helpers
Ansible plugins and modules to make network automation easier.


### Using net_txtfsm_parse filter

Setup

    # Get ntc-templates
    git clone https://github.com/networktocode/ntc-templates
    
    # PIP install any of the filter's requirements
    pip install git+https://github.com/ktbyers/ansible_helpers.git
    
    # Setup environment variable
    export NET_TEXTFSM=/path/to/ntc-templates/templates/
    
    # Copy https://github.com/ktbyers/filter_plugins/ to either:
    1. ./filter_plugins directory relative to your playbook
    2. Central filter_plugins dir as specified in your .ansible.cfg
