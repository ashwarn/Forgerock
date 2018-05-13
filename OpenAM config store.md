---


---

<h3 id="setup-configuration-store">Setup configuration store</h3>
<p>Prepare LDIF file</p>
<p><strong>openam-ds-admin-account.ldif</strong></p>
<pre><code>export BASE_DOMAIN="dc=example,dc=com"
export OPENAM_LDAP_ADMIN_PWD="Admin@123"
export OPENDJ_ADMIN_PWD="password"
export PATH=$PATH:/opt/opendj/bin
mkdir /tmp/ldif

cat &lt;&lt; EOF &gt; /tmp/ldif/openam-ds-admin-account.ldif
dn: ou=admins,$BASE_DOMAIN
objectClass: top
objectClass: organizationalunit
ou: AM Administrator

dn: uid=openam,ou=admins,$BASE_DOMAIN
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: AM Administrator
sn: AM
userPassword: $OPENAM_LDAP_ADMIN_PWD
ds-privilege-name: update-schema
ds-privilege-name: subentry-write
ds-privilege-name: password-reset
ds-privilege-name: proxied-auth
EOF
</code></pre>
<p>Run ldapmodify</p>
<pre><code>ldapmodify \
 --hostname opendj.example.com \
 --port 1389 \
 --bindDN "cn=Directory Manager" \
 --bindPassword $OPENDJ_ADMIN_PWD \
/tmp/ldif/openam-ds-admin-account.ldif
</code></pre>
<p>–</p>

