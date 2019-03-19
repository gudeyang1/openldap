### 1. build the image

### 2. load data

### 3. add password policy
ldapadd -c -x -H ldap://localhost -D  "cn=Manager,dc=starwave,dc=local" -f /usr/local/etc/openldap/password-policy.ldif -w uESJ5sDyv2rzxkPp

### 4. add user

```bash
dn: cn=shilei,ou=people,dc=starwave,dc=local
cn: shilei
uid: shilei
sn: shi
givenName: lei
displayName: shilei
objectClass: posixAccount
objectClass: top
objectClass: person
objectClass: shadowAccount
objectClass: inetOrgPerson
uidNumber: 1009
gidNumber: 1009
gecos: System Manager
loginShell: /bin/bash
homeDirectory: /home/shilei
userPassword: shilei
shadowLastChange: 17654
shadowMin: 0
shadowMax: 99999
shadowWarning: 7
shadowExpire: -1
employeeNumber: 18002
homePhone: 0531-xxxxxxxx
mobile: 152xxxxxxxxx
mail: shileizcc@126.com
postalAddress: BeiJing
initials: Test

```
ldapadd -c -x -H ldap://localhost -D  "cn=Manager,dc=starwave,dc=local" -f 1.ldif -w uESJ5sDyv2rzxkPp


#### 5. client configure
authconfig --enableldap --enableldapauth --ldapserver=ldaps://starwave.local:30636 --ldapbasedn="dc=starwave,dc=local" --enablemkhomedir --disableldaptls --update




#### 6. how to generate certs

```bash
openssl req -new -x509 -nodes -out ca-cert.pem -keyout ca-key.pem -days 7305
openssl req -new -nodes -out cert.csr -keyout key.pem
openssl req -new -nodes -out cert.csr -keyout key.pem

mv ca-cert.pem cert.pem key.pem contrib/config/certs/ 
```
