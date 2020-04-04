## config
1. ldap配置
    ```
    1. 添加ldap_base:ou=users,dc=kid17,dc=com
    2. ou=users中添加成员
    3. 创建cn=gitlab,ou=devops,dc=test,dc=com，gitlab为groupOfUniqueNames
    5. 添加uniqueMember，从ou=users中选择
    ```
2. gitlab charts 配置
    ```
    - name: LDAP_ENABLED
    value: 'true'
    - name: LDAP_HOST
    value: ldap-openldap
    - name: LDAP_BIND_DN
    value: 'cn=admin,dc=test,dc=com'
    - name: LDAP_PASS
    value: xxx
    - name: LDAP_UID
    value: uid
    - name: LDAP_ALLOW_USERNAME_OR_EMAIL_LOGIN
    value: 'false'
    - name: LDAP_BASE
    value: 'ou=users,dc=test,dc=com'
    - name: LDAP_USER_FILTER
    value: 'memberOf=cn=gitlab,ou=devops,dc=test,dc=com'
    ```