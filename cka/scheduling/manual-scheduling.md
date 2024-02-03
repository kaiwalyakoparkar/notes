# Manual Scheduling

- We can define the `nodeName` in the pod definition file to tell the scheduler what node you want the pod to be on.
- if the pod is already created then you can't edit it.
- One thing you can do here is make a bind object yaml file and make `post` request to pod's binding API.