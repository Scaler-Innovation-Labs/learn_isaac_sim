## Troubleshooting Guide

### Common Issues and Resolutions

#### Issue: selected interface "lo" is not multicast-capable: disabling multicast
**Resolution:**
1. Occurs if the local loopback interface that is used for simulations doesn't support multicast.
2. You can also run the following commands,
```
# allow multicast in firewall
sudo ufw allow in proto udp to 224.0.0.0/4
sudo ufw allow in proto udp from 224.0.0.0/4
# enable multicast on loopback interface
sudo ifconfig lo multicast
# add route to multicast address space to the loopback interface
route add -net 224.0.0.0 netmask 240.0.0.0 dev lo

```


#### Issue: unitree_mujoco C++ simulate throwing mpr_tolerance not present error
**Resolution:** HACK
1. Reason: upstream mujoco source code has the latest version which is incompatible with latest version of unitree_mujoco due to breaking changes. Install 3.2.2 version of mujoco to avoid this.


#### Issue: unitree_mujoco/simulate/build/unitree_mujoco C++ giving segmentation fault
**Resolution:**  PENDING
1. 


#### Issue: 
**Resolution:**  PENDING
1. 


#### Issue: 
**Resolution:**  PENDING
1. 


#### Issue: 
**Resolution:**  PENDING
1. 