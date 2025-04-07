guiand888.swapiness
===

# Purpose
Ansible role to configure `vm.swappiness` and restart swap devices to apply the change.  This role helps optimize memory management on a Linux system by controlling how aggressively the kernel swaps memory to disk.  

# Features
- Configures the `vm.swappiness` setting in `/etc/sysctl.conf`.
- Applies the new `vm.swappiness` value immediately using `sysctl -p`.
- Restarts all swap devices to ensure the new `vm.swappiness` setting is active.
- Includes assertions to verify that the setting is applied correctly.
- Customizable `vm.swappiness` value.

# Instructions
## Required Variables
None.  

## Optional Variables

- `swapiness_value`:  The desired `vm.swappiness` value (0-100).  Defaults to `1`.  A lower value (closer to 0) reduces swapping; higher values increase swapping.  

## Example Configuration

```yaml
swapiness_value: 10
```

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: guiand888.swapiness
      swapiness_value: 10 # Set swappiness value
```

## Execution

No specific tags are required. Simply include the role in your playbook.  

# Compatibility
- Ubuntu
- RHEL
- SUSE / OpenSUSE

# Notes and Warnings
- **OOM Killer:**  Setting `swapiness_value` to a very low level (e.g., 1) can lead to increased risk of the Out-of-Memory (OOM) killer being invoked. The system will aggressively try to avoid using swap, leading to process termination if memory is exhausted.
- Use this role with caution on systems with limited RAM.

# License
- GPLv3  

# Maintainers
Guillaume A.  
  - Contact: [mail@guillaumea.fr](mailto:mail@guillaumea.fr)  
  - Blog: https://blog.guillaumea.fr  
