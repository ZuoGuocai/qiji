

yum -y install elasticsearch-7.9.3-x86_64.rpm

vi /etc/elasticsearch/elasticsearch.yml

```
cluster.name: my-test-elastic
node.name: bj-ht-vm-17
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: 0.0.0.0
http.port: 9200
discovery.seed_hosts: ["172.24.126.15", "172.24.126.16","172.24.126.17"]
cluster.initial_master_nodes: ["172.24.126.15"]
xpack.security.transport.ssl.enabled: true
xpack.security.enabled: true
xpack.security.transport.ssl.verification_mode: certificate #认证方式使用证书
xpack.security.transport.ssl.keystore.path: certs/elastic-stack-ca.p12
xpack.security.transport.ssl.truststore.path: certs/elastic-stack-ca.p12
http.cors.enabled: true
http.cors.allow-origin: "*"
http.cors.allow-headers: "Authorization"
```
./elasticsearch-certutil ca -v

mv ../elastic-stack-ca.p12   /etc/elasticsearch/certs/

chown -R elasticsearch:elasticsearch /etc/elasticsearch/certs
 
scp elastic-stack-ca.p12  172.24.126.16:/etc/elasticsearch/certs/ 
scp elastic-stack-ca.p12  172.24.126.17:/etc/elasticsearch/certs/ 

/usr/share/elasticsearch/bin/elasticsearch-setup-passwords interactive


template

```
curl -u elastic:elastic -X PUT \
 http://127.0.0.1:9200/_template/backup-monitor_template \
 -H 'content-type:application/json' \
 -d '{
   "template": "backup-monitor*",
   "index_patterns": ["backup-monitor*"],
   "settings" : {
      "index" : {
         "number_of_replicas" : 1,
         "number_of_shards" : 3
      }
   },
   "mappings" : {
            "properties": { 
               "backup_project":{"type":"text"},
               "backup_method":{"type":"text"},
               "ip_addr":{"type":"ip"},
               "backup_path":{"type":"text"},
               "backup_status":{"type":"text"},
               "backup_time":{"type":"date"}
            }
   }
}'


```

pipeline

```
curl -u elastic:elastic  -X PUT \
 http://127.0.0.1:9200/_ingest/pipeline/backup-monitor-pipeline \
 -H 'content-type:application/json' \
 -d '{
  "description": "daily backup-monitor index naming",
  "processors": [
    {
      "date_index_name": {
        "field": "clock",
        "date_formats": ["UNIX"],
        "index_name_prefix": "backup-monitor-",
        "date_rounding": "d"
      }
    }
  ]
}'



```
