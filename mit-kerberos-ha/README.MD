
1. Install MIT Kerberos:
On each server, install the MIT Kerberos software:
sudo yum install krb5-kdc krb5-admin-server

2. Configure krb5.conf:
On each server, edit the /etc/krb5.conf file to include the Kerberos realm information. Ensure that all servers have the same configuration.

3. Configure kdc.conf:
On each server, edit the /etc/krb5kdc/kdc.conf file. Specify the master and slave KDCs. Ensure consistency across servers.

4. Create the KDC Database:
On the master KDC, initialize the KDC database:
sudo krb5_newrealm

5. Configure KDC Master and Slave:
On the master KDC, add the slave KDC to the realm:
sudo kadmin.local -q "addprinc -randkey krbtgt/YOUR_REALM@YOUR_REALM"
sudo kadmin.local -q "addprinc -randkey kadmin/changepw"
sudo kadmin.local -q "ktadd -k /etc/krb5kdc/kadm5.keytab kadmin/changepw"

Transfer the keytab to the slave KDC.

6. Start Services:
Start the Kerberos services on both the master and slave KDCs:

7. Testing:
Ensure that the KDCs are working and can communicate:

kinit admin/admin@MOEI.COM
klist


All the configs files mentioned are there in the repo
