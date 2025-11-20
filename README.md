PING ALL HOSTS

Ping All Hosts
- hosts: all
  tasks:
    - ansible.builtin.ping:
      
========================================================
PRINT MESSAGE

- hosts: all
  tasks:
    - debug:
        msg: "Hello from Ansible!"

=======================================================
Check Uptime

- hosts: all
  tasks:
    - shell: uptime
      register: out
    - debug:
        var: out.stdout

      
===========================================================

Run Multiple commands at same time

METHOD 1:

- hosts: all
  tasks:
    - name: Check uptime
      shell: uptime
      register: uptime_out

    - name: List files
      shell: ls -l
      register: ls_out

    - name: Show outputs
      debug:
        msg:
          - "Uptime: {{ uptime_out.stdout }}"
          - "Files: {{ ls_out.stdout }}"

OR

- hosts: all
  tasks:
    - name: Run multiple shell commands
      shell: |
        uptime
        ls -l
        df -h
      register: output

    - debug:
        var: output.stdout_lines
=================================================================
