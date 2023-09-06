These are the following errors we faced throughout the deployment:

1. Unable to install packages like `ninja`, `gc-devel`, `guile-devel`, `libconfig-devel`, `pkgconf-pkg-config`, `blas-devel` & `lapack-devel` through `sudo yum install`

Solution: 
Manually search for packages through internet. Checkout: https://vault.centos.org/centos/8/PowerTools/x86_64/os/Packages/

2. Sometimes kernel version does update to `rhel 8.8` after installing `rtk`.

Solution:
After installing rtk 
```bash
sudo yum update -y
```

3. Unable to install some packages even after manually downloading the packages:

Solution:

There is a particular order to install these packages which is given in the specific order in the [README](./README.md) itself.

4. unable to synchronize through linuxptp

Solution:

In the new_liteon.cfg file: 
* dataset_comparison should be G.8275.x
* domain number should be 24


5. Unprivilidged virtual functions trying to configure promiscuous mode

Solution:

We need to add `trust on`, like in the following command:
```bash
sudo ip link set ens1f0 vf 0 mac 00:11:22:33:44:66 vlan 564 spoofchk off trust on 
```

6. Vlan Stripping warning:

Solution:

 Make sure the i40 driver version is default and upgraded.

7. Radio unable to give `Du Connected: Ready` state

Solution:

Sometimes vf are unable to work as they are supposed to. In that case turn the radio on and let all of its state be ready other than `DU Connected`. which include state like DPD and RF state and then create virtual functions again and bind it vfio-pci and then run the nr-softmodem command.

8. `Invalid eCPRI message type` error in the logs

Solution:

Make sure the DU mac address configured in the radio is exactly: `00:11:22:33:44:66`