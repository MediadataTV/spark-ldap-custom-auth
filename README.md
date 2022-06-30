# Custom LDAP login class for Spark Thrift Server

Due to a missing config management in Spark Thrift Server implementation

(see: https://issues.apache.org/jira/browse/SPARK-32570)

Spark version 3.2.1 is no t able to login to ldap with custom use/group queries.

This class is the same submitted to master Spark and can be used with custom authentication

* Include the released jar
* Configure `hive-site.xml` with custom authentication

```xml
 <property>
        <name>hive.server2.authentication</name>
        <value>CUSTOM</value>
        <description>
            Expects one of [nosasl, none, ldap, kerberos, pam, custom].
            Client authentication types.
            NONE: no authentication check
            LDAP: LDAP/AD based authentication
            KERBEROS: Kerberos/GSSAPI authentication
            CUSTOM: Custom authentication provider
            (Use with property hive.server2.custom.authentication.class)
            PAM: Pluggable authentication module
            NOSASL: Raw transport
        </description>
    </property>
    <property>
        <name>hive.server2.custom.authentication.class</name>
        <value>org.apache.hive.service.auth.LdapCustomAuthenticationProviderImpl</value>
    </property>
    <property>
        <name>hive.server2.authentication.ldap.url</name>
        <value>ldap://ldapserver:389</value>
    </property>
    <property>
        <name>hive.server2.authentication.ldap.baseDN</name>
        <value>dc=example,dc=org</value>
    </property>
    <property>
        <name>hive.server2.authentication.ldap.userDNPattern</name>
        <value>cn=%s,ou=users,dc=example,dc=org</value>
    </property>
```