# WATcloud User Manual

Welcome to WATcloud! To get started, here are a few guidelines for using the cluster.

## General Guidelines

- Be [nice](https://man7.org/linux/man-pages/man2/nice.2.html)!
  - If you have a long-running non-interactive process, please [increase its niceness](https://www.tecmint.com/set-linux-process-priority-using-nice-and-renice-commands/) so that interactive programs don't lag.
  - Please be aware of the disk size constraints. We don't enforce disk quotas. A general rule of thumb is to leave small files in `$HOME` and put large files in `/mnt/wato-drive`.

## Resource-intensive and long-running workloads

- If your workload is resource-intensive or long-running, please request permissions by creating an issue using the “resource allocation request” template. State your use case and resource requirements. We periodically clean up unknown processes in the cluster.
- Unless exceptions are granted, long-running or resource-intensive workloads must be for student-design team projects only.

## Storage guidelines

- The home directory is a distributed filesystem (Ceph) and is accessible via any development VM in the cluster. Due to the limited size, it should be used for small files only. Datasets should be placed in `/mnt/wato-drive`
- `/mnt/wato-drive` is a NAS-HDD backed ZFS storage. It is intended for storing large files. It has a 1TB SSD cache. Combined with our 10Gbps cluster network it should have good performance.

## Maintenance and outages

- VMs in the server cluster may go down due to e.g. power outage, university network outage, and runaway processes. To check whether a machine is up, go to https://status.watonomous.ca
- Maintenance will be scheduled periodically. Notices will be posted in advance in the issues section and @WATonomous/teleport-users-terraform will be notified. Please ensure that you [enable notifications](https://docs.github.com/en/account-and-profile/managing-subscriptions-and-notifications-on-github/setting-up-notifications/configuring-notifications) to receive these notices.

## Tips and Tricks

### SSH Configuration Files

[Main resource](https://www.ssh.com/academy/ssh/config), this is just a quick reference.

A sample (and very simple) SSH configuration file for directly accessing a server in this cluster:

```ssh
Host bastion
  HostName bastion.watonomous.ca
  User <your username>
  IdentityFile <path to your WATonomous server private SSH keyfile>

Host workstation  # These names can be whatever you want.
  ProxyJump bastion
  User <your username>
  HostName <some server hostname>.watcluster.local
```

Then access the server directly with `ssh workstation`.
