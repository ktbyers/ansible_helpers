# ansible_helpers
Ansible plugins and modules to make network automation easier.
<br>  
<br>  
### Using net_txtfsm_parse filter
  
*_Purpose_*
  
Convert unstructured data from Ansible core networking modules (like ios_command, eos_command, nxos_command) into structured data using TextFSM templates.  
  
  
*_Example Use_*

    # Send output through the filter (specify two arguments platform and command)
    - debug:
        msg: "{{ output | net_textfsm_parse('cisco_ios', 'show ip int brief') }}"
  
  
*_Setup_*

    # Clone this repository
    git clone https://github.com/ktbyers/ansible_helpers
    
    # Get ntc-templates
    git clone https://github.com/networktocode/ntc-templates
    
    # PIP install any of the dependencies specified in requirements.txt
    pip install -r /path/to/ansible_helpers/requirements.txt
    
    # Setup environment variable
    export NET_TEXTFSM=/path/to/ntc-templates/templates/
    
    # Copy /path/to/ansible_helpers/filter_plugins to either:
    1. ./filter_plugins directory relative to your playbook
    2. a central filter_plugins directory as specified in your .ansible.cfg
  
  
*_More Detailed Example_*

See https://github.com/ktbyers/ansible_helpers/blob/master/simple_example.yml
