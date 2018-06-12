# test_task_fff
Check hosts file before provision.
#
Check user name in ssh-auth role before provision.
#
Check ip-range, subnets and interface type before provision.
#
In Debian 9.4.0 I had a small problem.
NFS Folders do not works until "exportfs -a" will be executed.
#
#
So, the algorithm is:
1. "vagrant up"
2. waiting nfs folder connecting
2.1 "exportfs -a" in parallel terminal
3. If you are slowly, watch the errors
4. "vagrant halt"
5. "exportfs -a"
6. "vagrant up"
7. Profit!
