# ansible_helpers
Ansible plugins and modules to make network automation easier.


### Using net_txtfsm_parse filter

*_Setup_*

    # Get ntc-templates
    git clone https://github.com/networktocode/ntc-templates
    
    # PIP install any of the filter's requirements
    pip install git+https://github.com/ktbyers/ansible_helpers.git
    
    # Setup environment variable (and to your shell initialization to permanently set)
    export NET_TEXTFSM=/path/to/ntc-templates/templates/
    
    # Copy https://github.com/ktbyers/ansible_helpers/filter_plugins/ to either:
    1. ./filter_plugins directory relative to your playbook
    2. Central filter_plugins directory as specified in your .ansible.cfg

*_Example Use_*

    tasks:
      # Retrieve output using an Ansible core platform_command module
      - ios_command:
          provider: "{{ creds }}"
          commands: show ip int brief
        register: output
      
      # Send output through the filter (specify two arguments platform and command)
      # Platform follows ntc-template convention of vendor_type (for example, cisco_ios,
      # arista_eos, juniper_junos, et cetera).
      - debug:
          msg: "{{ output | net_textfsm_parse('cisco_ios', 'show ip int brief') }}"

      - debug:
          msg: "{{ output | net_textfsm_parse(platform, command) }}"
