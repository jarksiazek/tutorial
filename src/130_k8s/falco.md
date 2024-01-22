* filter - container with filters that detect newly spawning and executing processes
```bash
- rule: shell_in_container
  desc: notice shell activity within a container
  condition: >
    spawned_process and container   
  output: >
    %evt.time,%user.name,%proc.name    
  priority: ERROR
```
