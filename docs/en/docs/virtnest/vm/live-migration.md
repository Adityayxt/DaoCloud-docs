# Live Migration

This article will explain how to move a virtual machine from one node to another.

When a node needs maintenance or upgrades, users can seamlessly migrate running virtual machines to other nodes while ensuring business continuity and data security.

## Prerequisites

Before using live migration, the following prerequisites must be met:

- Only running virtual machines can use the live migration feature.
- If you need to use live migration, make sure that your PVC access mode is ReadWriteMany.
- The current cluster must have at least 2 nodes.

## Live Migration

1. Click `Container Management` on the left navigation bar, then click "Virtual Machines" to enter the list page. Click `︙` on the right side of the list to perform migration actions on running virtual machines. Currently, the virtual machine is on the node `virtnest-rook-ceph-2`.

    <!-- Add image later -->

2. A pop-up box will appear, indicating that during live migration, the running virtual machine instances will be moved to another node, but the target node cannot be determined. Please ensure that other nodes have sufficient resources.

    <!-- Add image later -->

3. After a successful migration, you can view the node information in the virtual machine list. At this time, the node has been migrated to `virtnest-rook-ceph-1`.

    <!-- Add image later -->
