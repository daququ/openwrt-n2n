# openwrt-n2n
n2n Mod for MuJJnet project written by [Jason Tse](https://github.com/MuJJus) running on OpenWrt.  
forked from [original code](https://svn.ntop.org/svn/ntop/trunk/n2n/n2n_v2)

## Build

### Example for ar71xx and trunk.
```
wget http://downloads.openwrt.org/snapshots/trunk/ar71xx/generic/OpenWrt-SDK-ar71xx-generic_gcc-4.8-linaro_musl-1.1.11.Linux-x86_64.tar.bz2
tar jxf OpenWrt-SDK-ar71xx-generic_gcc-4.8-linaro_musl-1.1.11.Linux-x86_64.tar.bz2
cd OpenWrt-SDK-ar71xx-generic_gcc-4.8-linaro_musl-1.1.11.Linux-x86_64/package
git clone https://github.com/MuJJus/openwrt-n2n n2n
cd ..
make menuconfig # (selected Network -> VPN -> n2n-edge and n2n-supernode)
make package/n2n/compile V=s
```

### Example for 1900ac v1 

Env  ubuntu 18.04.1

wget https://downloads.openwrt.org/releases/18.06.1/targets/mvebu/cortexa9/openwrt-sdk-18.06.1-mvebu-cortexa9_gcc-7.3.0_musl_eabi.Linux-x86_64.tar.xz

....
make menuconfig # (selected Network -> VPN -> n2n-edge and n2n-supernode)
make package/n2n/compile V=s


/home/daququ/openwrt-sdk-18.06.1-mvebu-cortexa9_gcc-7.3.0_musl_eabi.Linux-x86_64/bin/packages/arm_cortex-a9_vfpv3/base/n2n-edge_2.1_git8347c66-1_arm_cortex-a9_vfpv3.ipk


scp  n2n-edge_2.1_git8347c66-1_arm_cortex-a9_vfpv3.ipk  to root@192.168.0.1:/tmp

opkg install n2n-edge_2.1_git8347c66-1_arm_cortex-a9_vfpv3.ipk

edge   -a  10.16.254.254 -c daququ-n2n-net -k key -l x.x.x.x:12321 -p 12321



## Usage
The `n2n` protocol options:

Name          | Type    | Required | Default | Description
--------------|---------|----------|---------|------------------------------------------------
server        | string  | yes      | (none)  | Supernode server
port          | int     | yes      | (none)  | Supernode port
server2       | string  | no       | (none)  | Supernode server of slave
port2         | int     | no       | (none)  | Supernode port of slave
community     | string  | yes      | (none)  | N2N community
key           | string  | no       | (none)  | The key of the community
mode          | string  | yes      | (none)  | For dhcp or static
ipaddr        | string  | no       | (none)  | IPv4 Address of the interface
netmask       | string  | no       | (none)  | Netmask of the interface
gateway       | string  | no       | (none)  | Gateway of the interface
ip6addr       | string  | no       | (none)  | IPv6 Address of the interface
ip6prefixlen  | int     | no       | (none)  | IPv6 Prefix Length of the interface
ip6gw         | string  | no       | (none)  | IPv6 Gateway of the interface
macaddr       | string  | no       | random  | MAC Address
mtu           | int     | no       | 1440    | Maximum Transmit Unit
forwarding    | boolean | no       | false   | Enable packet forwarding through n2n community
dynamic       | boolean | no       | false   | Periodically resolve supernode IP
localport     | int     | no       | random  | Fixed local UDP port
mgmtport      | int     | no       | (none)  | Management UDP Port (for multiple edges on a machine)
multicast     | boolean | no       | false   | Accept multicast MAC addresses
verbose       | boolean | no       | false   | Make more verbose

For supernode
```
# vi /etc/config/n2n
config supernode
        option enable '1'
        option port '80'

# /etc/init.d/n2n start
```

## LuCI
* edge [luci-proto-n2n](https://github.com/MuJJus/luci-proto-n2n)
* supernode [luci-app-n2n](https://github.com/MuJJus/luci-app-n2n)
