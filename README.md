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

<br>  
<br>  

### Using confparse_parent filter
  
*_Purpose_*

Allow use of CiscoConfParse to parse space-based hierarchical configurations and to make logical decisions from the results.  
  
  
*_Example Use_*

    - name: Use confparse_parent filter to find 3DES crypto maps
      set_fact:
        crypto_list: "{{ show_run | confparse_parent(parent='^crypto map CRYPTO', child='3DES-SHA') }}"


The returned data structure looks as follows where element[0] is a boolean indicating whether the child condition was found. Element[1] is the matching parent configuration line. Element[2] is the matching child configuration line (or null if not found).

        "crypto_list": [
            [
                false, 
                "crypto map CRYPTO 10 ipsec-isakmp ", 
                null
            ], 
            [
                true, 
                "crypto map CRYPTO 20 ipsec-isakmp ", 
                " set transform-set 3DES-SHA "
            ], 
            [
                true, 
                "crypto map CRYPTO 30 ipsec-isakmp ", 
                " set transform-set 3DES-SHA "
            ], 
            [
                false, 
                "crypto map CRYPTO 40 ipsec-isakmp ", 
                null
            ], 
            [
                false, 
                "crypto map CRYPTO 50 ipsec-isakmp ", 
                null
            ]
        ]

  
  
*_Setup_*

    # Clone this repository
    git clone https://github.com/ktbyers/ansible_helpers
    
    # PIP install any of the dependencies specified in requirements.txt
    pip install -r /path/to/ansible_helpers/requirements.txt
    
    # Copy /path/to/ansible_helpers/filter_plugins to either:
    1. ./filter_plugins directory relative to your playbook
    2. a central filter_plugins directory as specified in your .ansible.cfg
  
  
*_More Detailed Example_*

See https://github.com/ktbyers/ansible_helpers/blob/master/example_confparse.yml


