# OS Upgrades

- Use `kubectl drain <node-name>` this will terminate the pod on this node and create them on other node, making this node available for maintenance.
- After necessary maintainance, we have to do `kubectl uncordon <node-name>` to make it available for pod scheduling again.
- `kubectl cordon <node-name>` makes the node non-schedulable. does not terminate pods and stuff like drain.
- When the node is cordoned, the pods are moved (Not technically moved but terminated on that node & started on other) from that node to another.
- When the node is uncordoned the pods are **are not** moved back and **only newly created** pods will be placed on that node.
- If the node is forcefully drained, then the pod that is not part of repliaset will be **lost permanently** (So insted of draining it, we cordon it)
- When we drain the node, it is first cordoned and the pods are terminated.
- drain - Unschedulable & terminate pods
- cordon - Unschedulable
- uncordon - Make is schedulable again