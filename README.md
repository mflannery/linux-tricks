# linux-tricks
collection of linux commands to help get stuff done

**Populate .ssh/known_hosts**
```
ANSIBLE_HOST_KEY_CHECKING=false ansible all -m ping -k
```
**Send keys to hosts with ansible**
```
ansible all -m authorized_key -a "user=root state=present key='<key>'" -k
```
**Attach subscription pool to hosts via ansible**
```
ansible all -a "subscription-manager attach --pool=8a85f98260c27fc50160c323263339ff"
ansible all -a "subscription-manager repos --disable='*' --enable=rhel-7-server-rpms --enable=rhel-7-server-extras-rpms --enable=rhel-7-server-ansible-2.4-rpms --enable=rhel-7-server-ose-3.9-rpms --enable=rhel-7-fast-datapath-rpms --enable=rh-gluster-3-client-for-rhel-7-server-rpms"
```
**Subscribe all hosts**
```
ansible all -a "subscription-manager register --username=<user> --password=<pass>"
```
**To find this or that with grep**
```
grep -i -E 'pool|openshift' subs.txt
```
**To output all lines that are not commented out**
```
grep "^[^#;]" smb.conf
```
**find a string in a file**
```
find . -type f -exec grep -HIi "search for something here" {} \;
```
**ipmitool examples**
```
ipmitool -I lanplus -H 172.18.173.14 -U ADMIN -P ADMIN sol activate
ipmitool -I lanplus -H 172.18.173.14 -U ADMIN -P ADMIN chassis power on
for pool in `rados lspools` ; do echo "POOL : " $pool; rbd ls -l $pool; echo "-----"; done
```
https://www.certdepot.net/rhel7-configure-io-schedulers/

**determine PV alignment**
```
pvs /dev/sda -o+pe_start
```
**Remove the old key(s) from known_hosts**
```
ssh-keygen -R $HOST
```
or
```
vi ~/.ssh/known_hosts
```
**Add the new key(s) to known_hosts**
```
ssh-keyscan $HOST >> ~/.ssh/known_hosts
```
**When an unexpected power outage occurs and Ceph OSDs are down, run this:**
```
for i in {1..6}; do ssh root@rhsn$i-mgmt "ceph-disk activate-all"; done
```
