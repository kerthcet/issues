## ES集群
1. 启动es集群，发现无法启动.0/6 nodes are available: 3 Insufficient cpu, 3 node(s) had taints that the pod didn't tolerate.
```
    elasticsearch antiAffinity是hard，改为“”就可以了。
```

2. es启用xpack.(helm install elastic/elasticsearch)
   ```
   1. 设置elasticsearch.yml(yml不是yaml)
        esConfig:
            elasticsearch.yml: |
                xpack.security.enabled: true
                xpack.security.transport.ssl.enabled: true
                xpack.security.transport.ssl.verification_mode: certificate
                xpack.security.transport.ssl.keystore.path: /usr/share/elasticsearch/config/certs/elastic-certificates.p12
                xpack.security.transport.ssl.truststore.path: /usr/share/elasticsearch/config/certs/elastic-certificates.p12
                xpack.security.http.ssl.enabled: true
                xpack.security.http.ssl.truststore.path: /usr/share/elasticsearch/config/certs/elastic-certificates.p12
                xpack.security.http.ssl.keystore.path: /usr/share/elasticsearch/config/certs/elastic-certificates.p12
    2. 设置env
        entraEnvs:
          - name: ELASTIC_PASSWORD
            valueFrom:
                secretKeyRef:
                name: elastic-credentials
                key: password
          - name: ELASTIC_USERNAME
            valueFrom:
                secretKeyRef:
                name: elastic-credentials
                key: username

   3. 创建secret
      1. git clone elastic repository
      2. cd elasticsearch/examples/security
      3. make install
   ```

