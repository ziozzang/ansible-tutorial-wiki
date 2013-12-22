[戻る](ansible-note)

# サーバーの情報を利用する (GATHERING FACTS)

playbook を実行するとまずサーバの情報を収集します。 実行時に `GATHERING FACTS` を表示されている部分です。次のような情報が収集され、これを task の中で利用することができます

```
$ ansible -m setup -i hosts 192.168.33.12
192.168.33.12 | success >> {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "10.0.2.15", 
            "192.168.33.12"
        ], 
        "ansible_all_ipv6_addresses": [
            "fe80::a00:27ff:fec9:399e", 
            "fe80::a00:27ff:fed5:dab6"
        ], 
        "ansible_architecture": "x86_64", 
        "ansible_bios_date": "12/01/2006", 
        "ansible_bios_version": "VirtualBox", 
        "ansible_cmdline": {
            "KEYBOARDTYPE": "pc", 
            "KEYTABLE": "us", 
            "LANG": "en_US.UTF-8", 
            "SYSFONT": "latarcyrheb-sun16", 
            "quiet": true, 
            "rd_LVM_LV": "VolGroup/lv_root", 
            "rd_NO_DM": true, 
            "rd_NO_LUKS": true, 
            "rd_NO_MD": true, 
            "rhgb": true, 
            "ro": true, 
            "root": "/dev/mapper/VolGroup-lv_root"
        }, 
        "ansible_date_time": {
            "date": "2013-08-08", 
            "day": "08", 
            "epoch": "1375968652", 
            "hour": "13", 
            "iso8601": "2013-08-08T13:30:52Z", 
            "iso8601_micro": "2013-08-08T13:30:52.873665Z", 
            "minute": "30", 
            "month": "08", 
            "second": "52", 
            "time": "13:30:52", 
            "tz": "UTC", 
            "year": "2013"
        }, 
        "ansible_default_ipv4": {
            "address": "10.0.2.15", 
            "alias": "eth0", 
            "gateway": "10.0.2.2", 
            "interface": "eth0", 
            "macaddress": "08:00:27:c9:39:9e", 
            "mtu": 1500, 
            "netmask": "255.255.255.0", 
            "network": "10.0.2.0", 
            "type": "ether"
        }, 
        "ansible_default_ipv6": {}, 
        "ansible_devices": {
            "sda": {
                "holders": [], 
                "host": "SATA controller: Intel Corporation 82801HM/HEM (ICH8M/ICH8M-E) SATA Controller [AHCI mode] (rev 02)", 
                "model": "VBOX HARDDISK", 
                "partitions": {
                    "sda1": {
                        "sectors": "1024000", 
                        "sectorsize": 512, 
                        "size": "500.00 MB", 
                        "start": "2048"
                    }, 
                    "sda2": {
                        "sectors": "1047549952", 
                        "sectorsize": 512, 
                        "size": "499.51 GB", 
                        "start": "1026048"
                    }
                }, 
                "removable": "0", 
                "rotational": "1", 
                "scheduler_mode": "cfq", 
                "sectors": "1048576000", 
                "sectorsize": "512", 
                "size": "500.00 GB", 
                "support_discard": "0", 
                "vendor": "ATA"
            }, 
            "sr0": {
                "holders": [], 
                "host": "IDE interface: Intel Corporation 82371AB/EB/MB PIIX4 IDE (rev 01)", 
                "model": "CD-ROM", 
                "partitions": {}, 
                "removable": "1", 
                "rotational": "1", 
                "scheduler_mode": "cfq", 
                "sectors": "2097151", 
                "sectorsize": "512", 
                "size": "1024.00 MB", 
                "support_discard": "0", 
                "vendor": "VBOX"
            }, 
            "sr1": {
                "holders": [], 
                "host": "IDE interface: Intel Corporation 82371AB/EB/MB PIIX4 IDE (rev 01)", 
                "model": "CD-ROM", 
                "partitions": {}, 
                "removable": "1", 
                "rotational": "1", 
                "scheduler_mode": "cfq", 
                "sectors": "2097151", 
                "sectorsize": "512", 
                "size": "1024.00 MB", 
                "support_discard": "0", 
                "vendor": "VBOX"
            }
        }, 
        "ansible_distribution": "CentOS", 
        "ansible_distribution_release": "Final", 
        "ansible_distribution_version": "6.4", 
        "ansible_domain": "localdomain", 
        "ansible_eth0": {
            "active": true, 
            "device": "eth0", 
            "ipv4": {
                "address": "10.0.2.15", 
                "netmask": "255.255.255.0", 
                "network": "10.0.2.0"
            }, 
            "ipv6": [
                {
                    "address": "fe80::a00:27ff:fec9:399e", 
                    "prefix": "64", 
                    "scope": "link"
                }
            ], 
            "macaddress": "08:00:27:c9:39:9e", 
            "module": "e1000", 
            "mtu": 1500, 
            "type": "ether"
        }, 
        "ansible_eth1": {
            "active": true, 
            "device": "eth1", 
            "ipv4": {
                "address": "192.168.33.12", 
                "netmask": "255.255.255.0", 
                "network": "192.168.33.0"
            }, 
            "ipv6": [
                {
                    "address": "fe80::a00:27ff:fed5:dab6", 
                    "prefix": "64", 
                    "scope": "link"
                }
            ], 
            "macaddress": "08:00:27:d5:da:b6", 
            "module": "e1000", 
            "mtu": 1500, 
            "type": "ether"
        }, 
        "ansible_form_factor": "Other", 
        "ansible_fqdn": "localhost.localdomain", 
        "ansible_hostname": "localhost", 
        "ansible_interfaces": [
            "lo", 
            "eth1", 
            "eth0"
        ], 
        "ansible_kernel": "2.6.32-358.el6.x86_64", 
        "ansible_lo": {
            "active": true, 
            "device": "lo", 
            "ipv4": {
                "address": "127.0.0.1", 
                "netmask": "255.0.0.0", 
                "network": "127.0.0.0"
            }, 
            "ipv6": [
                {
                    "address": "::1", 
                    "prefix": "128", 
                    "scope": "host"
                }
            ], 
            "mtu": 16436, 
            "type": "loopback"
        }, 
        "ansible_machine": "x86_64", 
        "ansible_memfree_mb": 323, 
        "ansible_memtotal_mb": 458, 
        "ansible_mounts": [
            {
                "device": "/dev/mapper/VolGroup-lv_root", 
                "fstype": "ext4", 
                "mount": "/", 
                "options": "rw", 
                "size_available": 497491697664, 
                "size_total": 525282689024
            }, 
            {
                "device": "/dev/sda1", 
                "fstype": "ext4", 
                "mount": "/boot", 
                "options": "rw", 
                "size_available": 448802816, 
                "size_total": 507744256
            }, 
            {
                "device": "/vagrant", 
                "fstype": "vboxsf", 
                "mount": "/vagrant", 
                "options": "uid=501,gid=501,rw", 
                "size_available": 72607436800, 
                "size_total": 117461032960
            }
        ], 
        "ansible_os_family": "RedHat", 
        "ansible_pkg_mgr": "yum", 
        "ansible_processor": [
            "Intel(R) Core(TM) i3-3217U CPU @ 1.80GHz"
        ], 
        "ansible_processor_cores": "NA", 
        "ansible_processor_count": 1, 
        "ansible_product_name": "VirtualBox", 
        "ansible_product_serial": "NA", 
        "ansible_product_uuid": "NA", 
        "ansible_product_version": "1.2", 
        "ansible_python_version": "2.6.6", 
        "ansible_selinux": false, 
        "ansible_ssh_host_key_dsa_public": "...", 
        "ansible_ssh_host_key_rsa_public": "...", 
        "ansible_swapfree_mb": 2559, 
        "ansible_swaptotal_mb": 2559, 
        "ansible_system": "Linux", 
        "ansible_system_vendor": "innotek GmbH", 
        "ansible_user_id": "vagrant", 
        "ansible_userspace_architecture": "x86_64", 
        "ansible_userspace_bits": "64", 
        "ansible_virtualization_role": "guest", 
        "ansible_virtualization_type": "virtualbox", 
        "facter_architecture": "x86_64", 
        "facter_augeasversion": "0.9.0", 
        "facter_blockdevice_sda_model": "VBOX HARDDISK", 
        "facter_blockdevice_sda_size": 536870912000, 
        "facter_blockdevice_sda_vendor": "ATA", 
        "facter_blockdevice_sr0_model": "CD-ROM", 
        "facter_blockdevice_sr0_size": 1073741312, 
        "facter_blockdevice_sr0_vendor": "VBOX", 
        "facter_blockdevice_sr1_model": "CD-ROM", 
        "facter_blockdevice_sr1_size": 1073741312, 
        "facter_blockdevice_sr1_vendor": "VBOX", 
        "facter_blockdevices": "sda,sr0,sr1", 
        "facter_facterversion": "1.7.0", 
        "facter_filesystems": "ext4,iso9660", 
        "facter_hardwareisa": "x86_64", 
        "facter_hardwaremodel": "x86_64", 
        "facter_hostname": "localhost", 
        "facter_id": "vagrant", 
        "facter_interfaces": "eth0,eth1,lo", 
        "facter_ipaddress": "10.0.2.15", 
        "facter_ipaddress_eth0": "10.0.2.15", 
        "facter_ipaddress_eth1": "192.168.33.12", 
        "facter_ipaddress_lo": "127.0.0.1", 
        "facter_is_virtual": "true", 
        "facter_kernel": "Linux", 
        "facter_kernelmajversion": "2.6", 
        "facter_kernelrelease": "2.6.32-358.el6.x86_64", 
        "facter_kernelversion": "2.6.32", 
        "facter_macaddress": "08:00:27:C9:39:9E", 
        "facter_macaddress_eth0": "08:00:27:C9:39:9E", 
        "facter_macaddress_eth1": "08:00:27:D5:DA:B6", 
        "facter_memoryfree": "366.08 MB", 
        "facter_memoryfree_mb": "366.08", 
        "facter_memorysize": "458.64 MB", 
        "facter_memorysize_mb": "458.64", 
        "facter_memorytotal": "458.64 MB", 
        "facter_mtu_eth0": "1500", 
        "facter_mtu_eth1": "1500", 
        "facter_mtu_lo": "16436", 
        "facter_netmask": "255.255.255.0", 
        "facter_netmask_eth0": "255.255.255.0", 
        "facter_netmask_eth1": "255.255.255.0", 
        "facter_netmask_lo": "255.0.0.0", 
        "facter_network_eth0": "10.0.2.0", 
        "facter_network_eth1": "192.168.33.0", 
        "facter_network_lo": "127.0.0.0", 
        "facter_operatingsystem": "CentOS", 
        "facter_operatingsystemmajrelease": "6", 
        "facter_operatingsystemrelease": "6.4", 
        "facter_osfamily": "RedHat", 
        "facter_path": "/usr/local/bin:/bin:/usr/bin", 
        "facter_physicalprocessorcount": 1, 
        "facter_processor0": "Intel(R) Core(TM) i3-3217U CPU @ 1.80GHz", 
        "facter_processorcount": "1", 
        "facter_ps": "ps -ef", 
        "facter_puppetversion": "3.1.1", 
        "facter_rubysitedir": "/usr/lib/ruby/site_ruby/1.8", 
        "facter_rubyversion": "1.8.7", 
        "facter_selinux": "false", 
        "facter_sshdsakey": "...", 
        "facter_sshfp_dsa": "SSHFP 2 1 ...\nSSHFP 2 2 ...", 
        "facter_sshfp_rsa": "SSHFP 1 1 ...\nSSHFP 1 2 ...", 
        "facter_sshrsakey": "...", 
        "facter_swapfree": "2.50 GB", 
        "facter_swapfree_mb": "2559.99", 
        "facter_swapsize": "2.50 GB", 
        "facter_swapsize_mb": "2559.99", 
        "facter_timezone": "UTC", 
        "facter_uniqueid": "007f0100", 
        "facter_uptime": "1:09 hours", 
        "facter_uptime_days": 0, 
        "facter_uptime_hours": 1, 
        "facter_uptime_seconds": 4195, 
        "facter_virtual": "virtualbox"
    }, 
    "changed": false
}
```

templates で IP address を埋める場合には `{{ ansible_eth0["ipv4"]["address"] }}` と書けます。 `{{ ansible_eth0.ipv4.address }}` でも可。
`{{ ansible_processor_count * 5 }}` として計算結果を利用することもできます。次に説明する条件付き実行の条件としても使えます。

この収集処理にはそこそこ時間がかかるため、このデータを利用しない場合は playbook で `gather_facts: no` と指定することで省略することが可能です。
