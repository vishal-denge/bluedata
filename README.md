# REST APIs

## 1.	Login and Session Creation
  __API-URI__: /api/v1/login

  __Curl command__:

      curl -i -X POST -d@login.json http://<controller-ip>/api/v1/login

  __API Type__: `POST`

  __Example__:

      curl -i -X POST -d@login.json http://10.36.0.17:8080/api/v1/login

 __Json-file__: login.json:

  		    {
            "name" : "admin",
            "password": "admin123"
          }

  __Response__:

      HTTP/1.1 201 Created
      Server: BlueData EPIC 2.6
      Location: /api/v1/session/ad93b4bb-8908-4af9-8c36-ea4f92f29277
      Date: Thu, 18 May 2017 23:35:05 GMT
      Content-Length: 13


## 2.	Retrieve available cluster images:

  __API-URI__: /api/v1/catalog

  __Curl command__:

      curl -X GET -H "X-BDS-SESSION:<session-id>" http://<controller-ip>/api/v1/catalog/

  __API Type__: `GET`

  __Example__:

      curl -X GET -H "X-BDS-SESSION:/api/v1/session/985585be-685d-4a6a-a0f0-0c563ae32e56" http://10.36.0.17:8080/api/v1/catalog/

  __Response__:

     {"_links":{"self":{"href":"/api/v1/catalog/"},"feed":[{"href":"http://10.36.0.17:8080/api/v1/feed/local","name":"Feed generated from l	ocal bundles."},{"href":"http://10.2.12.27:8080/build/catalog-bundles/external-epic/feed/feed-centos-debug.json.nas3","name":"Official 	   BlueData EPIC Catalog"},{"href":"http://10.2.12.27:8080/build/catalog-bundles/internal-epic/feed/feed-centos-debug.json.nas3","name":"     Internal BlueData EPIC catalog"}]},"catalog_api_version":2,"feeds_refresh_period_seconds":86400,"feeds_read_counter":124,"catalog_writ	 e_counter":124,"_embedded":{"independent_catalog_entries":[{"_links":{"self":{"href":"/api/v1/catalog/1"}



## 3.   Retrieve available tenants:

  __API-URI__: /api/v1/tenant

  __Curl command__:

      curl -X GET -H "X-BDS-SESSION:<Session-ID>" http://<Controller-ID>/api/v1/tenant

  __API Type__: `GET`

  __Example__:

      curl -X GET -H "X-BDS-SESSION:/api/v1/session/985585be-685d-4a6a-a0f0-0c563ae32e56" http://10.36.0.17:8080/api/v1/tenant

  __Response__:

      {"_links":{"self":{"href":"/api/v1/tenant"}},"_embedded":{"tenants":[{"_links":{"self":{"href":"/api/v1/tenant/2"}},"label":{"name":"	 Demo Tenant","description":"Demo Tenant for BlueData Clusters"},"member_key_available":"all_admins","status":"ready","tenant_type":"d	    ocker","qos_multiplier":1,"quota":{},"inusequota":{"cores":44,"memory":102400,"disk":552960},"tenant_storage_quota_supported":true,"e      xternal_user_groups":[]},{"_links":{"self":{"href":"/api/v1/tenant/1"}},"label":{"name":"Site Admin","description":"Site Admin Tenant 	  for BlueData clusters"},"member_key_available":"all_admins","status":"ready"}



## 4.   Retrieve tenant information such as resources, security, and other settings

  __API-URI__: /api/v1/tenant/<tenant-id>

  __Curl command__:

      curl -X GET -H "X-BDS-SESSION:<session-id>" http://<controller-ip>/api/v1/tenant/<tenant-id>

  __API Type__: `GET`

  __Example__:

      curl -X GET -H "X-BDS-SESSION:/api/v1/session/985585be-685d-4a6a-a0f0-0c563ae32e56" http://10.36.0.17:8080/api/v1/tenant/3

  __Response__:

      {"_links":{"self":{"href":"/api/v1/tenant/3"},"all_tenants":{"href":"/api/v1/tenant"}},"label":{"name":"Active Directory","description":"All clusters with AD integration"},"member_key_available":"all_admins","status":"ready","tenant_type":"docker","qos_multiplier":1,"quota":{"cores":15,"memory":47104,"disk":561152,"tenant_storage":582},"inusequota":{"cores":4,"memory":8192,"disk":30720},"tenant_storage_quota_supported":true,"external_user_groups":[{"group":"CN=Eng,OU=Engineering,DC=BLUEDATA,DC=local","role":"/api/v1/role/2"}],"kdc_type":"Active Directory","kdc_host":"10.2.12.106","kdc_admin_user":"admin@BLUEDATA.LOCAL","kdc_admin_password":"Layer42!","kdc_realm":"BLUEDATA.LOCAL","krb_enc_types":["rc4-hmac","aes256-cts-hmac-sha1-96","aes128-cts-hmac-sha1-96","des3-cbc-sha1","arcfour-hmac","des-hmac-sha1","des-cbc-md5"],"kdc_ad_prefix":"ActiveDir","kdc_ad_suffix":"ou=Engineering,dc=BLUEDATA,dc=local"}


## 5.   Retrieve tenant virtual clusters

  __API-URI__: /api/v1/cluster

  __Curl command__:

      curl -X GET -H "X-BDS-SESSION:<session-id>" http://<controller-ip>/api/v1/cluster

  __API Type__: `GET`

  __Example__:

      curl -X GET -H "X-BDS-SESSION:/api/v1/session/985585be-685d-4a6a-a0f0-0c563ae32e56" http://10.36.0.17:8080/api/v1/cluster

  __Response__:

      {"result":"Success","objects":[{"result":"Success","uuid":"65","cluster_name":"Spark-Nifi-test","cluster_type":"Spark","distro_name":"Spark 1.6.0","distro_version":"1.8","distro_state":"installed","cluster_context":"Persistent","master_flavor":{"root_disk_size":100,"label":{"name":"Medium","description":"system-created example flavor"},"cores":4,"memory":12288},"slave_count":2,"slave_flavor":{"root_disk_size":30,"label":{"name":"Small","description":"system-created example flavor"},"cores":4,"memory":8192},"status_message":"","error_info":"","ha_enabled":false,"apps_installed":false,"include_spark_installation":false,"mr_type":"","kerberos_enabled":false,"log_url":"http://10.36.0.17:8080/Logs/65.txt","client_config_xml":"","client_config_java":"","status":"ready","tenant_id":"/api/v1/tenant/2","tenant_name":"Demo Tenant","tenant_type":"docker"}



## 6.   Retrieve a virtual cluster configuration(image type, size, IPs and nodes)



  __API-URI__: /api/v1/cluster/?nodelist

  __Curl command__:

      curl -X GET -H "X-BDS-SESSION:<session-id>" http://<controller-ip>/api/v1/cluster/?nodelist

  __API Type__: `GET`

  __Example__:

      curl -X GET -H "X-BDS-SESSION:/api/v1/session/985585be-685d-4a6a-a0f0-0c563ae32e56" http://10.36.0.17:8080/api/v1/cluster/?nodelist

  __Response__:

      {"result":"Success","objects":[{"result":"Success","uuid":"65","cluster_name":"Spark-Nifi-test","cluster_type":"Spark","distro_name":"Spark 1.6.0","distro_version":"1.8","distro_state":"installed","cluster_context":"Persistent","master_flavor":{"root_disk_size":100,"label":{"name":"Medium","description":"system-created example flavor"},"cores":4,"memory":12288},"slave_count":2,"slave_flavor":{"root_disk_size":30,"label":{"name":"Small","description":"system-created example flavor"},"cores":4,"memory":8192},"status_message":"","error_info":"","ha_enabled":false,"apps_installed":false,"include_spark_installation":false,"mr_type":"","kerberos_enabled":false,"log_url":"http://10.36.0.17:8080/Logs/65.txt","client_config_xml":"","client_config_java":"","status":"ready","tenant_id":"/api/v1/tenant/2","tenant_name":"Demo Tenant","tenant_type":"docker"}


## 7.   Get created DataTap in a certain Tenant



  __API-URI__: /api/v1/cluster/?nodelist

  __Curl command__:

      curl -X GET -H "X-BDS-SESSION:<session-id>" http://<controller-ip>/api/v1/dataconn

  __API Type__: `GET`

  __Example__:

      curl -X GET -H "X-BDS-SESSION:/api/v1/session/985585be-685d-4a6a-a0f0-0c563ae32e56" http://10.36.0.17:8080/api/v1/dataconn

  __Response__:

      {"_links":{"self":{"href":"/api/v1/dataconn"}},"_embedded":{"data_connectors":[{"_links":{"self":{"href":"/api/v1/dataconn/1"},"query":{"href":"/api/v1/dataconn/1{?query}","templated":true}},"_embedded":{"label":{"_links":{"self":{"href":"/api/v1/dataconn/1?label"}},"name":"TenantStorage","description":"Protected DataTap for a tenant-specific sandboxed storage space."},"endpoint":{"_links":{"self":{"href":"/api/v1/dataconn/1?endpoint"}},"type":"hdfs","host":"yav-114.lab.bluedata.com","kdc_data":[{"host":"10.36.0.17","port":88}],"keytab":"datasrvr.headless.keytab","realm":"BLUEDATA.SITE","client_principal":"datasrvr/yav-114.lab.bluedata.com@BLUEDATA.SITE","service_id":"hdfs"},"bdfs_root":{"_links":{"self":{"href":"/api/v1/dataconn/1?bdfs_root"}},"path_from_endpoint":"/2/default"},"flags":{"_links":{"self":{"href":"/api/v1/dataconn/1?flags"}},"read_only":false},"is_protected":true}}]}}


## 8.   Create a new cluster



  __API-URI__: /api/v1/cluster

  __Curl command__:

      curl -X POST -d@hadoop_cluster.json -H "X-BDS-SESSION:<session-id>" http://<controller-ip>:8080/api/v1/cluster

  __API Type__: `POST`

  __Example__:

      curl -X POST -d@hadoop_cluster.json -H "X-BDS-SESSION:/api/v1/session/446468df-6869-4e42-bbba-c8cc11cb4a54" http://127.0.0.1:8080/api/v1/cluster

 __Json-file__: hadoop_cluster.json:

        {
            "ha_enabled":false,
            "cluster_name":"Hadoop test",
            "cluster_type":"Hadoop",
            "distro_name":"CDH 5.4.3 with Cloudera Manager",
            "master_flavor":"/api/v1/flavor/2",
            "slave_count":2,
            "slave_flavor":"/api/v1/flavor/2",
            "spark_installed":false,
            "apps_installed":true,
            "mr_type":"YARN",
            "config_nondefaults":[
              {
                  "namespace":"yarn-site.xml",
                  "value":"2046",
                  "property_name":"yarn.nodemanager.resource.memory-mb"
              },
              {
                  "namespace":"mapred-site-yarn.xml",
                  "value":"1364",
                  "property_name":"mapreduce.reduce.memory.mb"
              },
              {
                  "namespace":"mapred-site-yarn.xml",
                  "value":"1364",
                  "property_name":"yarn.app.mapreduce.am.resource.mb"
              },
              {
                  "namespace":"mapred-site-yarn.xml",
                  "value":"682",
                  "property_name":"mapreduce.map.memory.mb"
              },
              {
                  "namespace":"mapred-site-yarn.xml",
                  "value":"272",
                  "property_name":"mapreduce.task.io.sort.mb"
              },
              {
                  "namespace":"yarn-site.xml",
                  "value":"false",
                  "property_name":"yarn.nodemanager.vmem-checkenabled"
              }
            ]


        }

  __Response__:

      201 Created


## 9.   Create a cluster DataTap



  __API-URI__: /api/v1/dataconn

  __Curl command__:

      curl -X POST -d@datatap.json -H "X-BDS-SESSION:<session-id>" http://<controller-ip>:8080/api/v1/dataconn

  __API Type__: `POST`

  __Example__:

      curl -X POST -d@datatap.json -H "X-BDS-SESSION: /api/v1/session/230fe122-da47-47ab-bcd7 3431efb69cae" http://127.0.0.1:8080/api/v1/dataconn

 __Json-file__: datatap.json:

        {
          "bdfs_root": {
                          "path_from_endpoint": "/tmp/nanda"
                       },
          "endpoint": {
                          "host": "bd-045.lab.bluedata.com",
                          "type": "hdfs",
                          "port": 8020
                      },
          "label":    {
                          "name": "StagingDataLake",
                          "description": "External Staging Datalake"
                      }
        }

  __Response__:

      201 Created


## 10.   Enable virtual cluster Kerberos



  __API-URI__: /api/v1/tenant/<tenant-id>?tenant_kdc

  __Curl command__:

      curl -X PUT -d@kerberos.json -H "X-BDS-SESSION:<session-id>" http://<controller-ip>:8080/api/v1/tenant/<tenant-id>?tenant_kdc

  __API Type__: `PUT`

  __Example__:

      curl -X PUT -d@kerberos.json -H "X-BDS-SESSION:/api/v1/session/021a76e2-083d-42b2-afb1-b7f1de2cb72e" http://10.36.0.17:8080/api/v1/tenant/5?tenant_kdc

 __Json-file__: kerberos.json:

        {
        "kdc_host": "10.12.102.16",
        "kdc_admin_password": "***",
        "krb_enc_types": ["rhmac-type"],
        "kdc_realm": "BLUEDATA.LOCAL",
        "kdc_admin_user": "admin@BLUEDATA.LOCAL",
        "kdc_type": "MIT KDC"
        }

  __Response__:

      None


## 11.   Delete an existing cluster



  __API-URI__: /api/v1/cluster/<uuid>

  __Curl command__:

      curl -v -X DELETE -H "X-BDS-SESSION:<session-id>" http://<controller-ip>:8080/api/v1/cluster/<uuid>
  
  __API Type__: `DELETE`

  __Example__:

      curl -v -X DELETE -H "X-BDS-SESSION: /api/v1/session/46f80cd5- 972d-41df-bcba-61c809b5470f" http://<IP_address>:8080/api/v1/cluster/72

  __Response__:

      {"result":"Success"}


## 12.   Delete an existing DataTap



  __API-URI__: /api/v1/dataconn/<datatap-id>

  __Curl command__:

      curl -v -X DELETE -H "X-BDS-SESSION:<session-id>" http://<controller-ip>/api/v1/dataconn/<datatap-id>
  
  __API Type__: `DELETE`

  __Example__:

      curl -v -X DELETE -H "X-BDS-SESSION:/api/v1/session/6a917f50-776b-4eea-8eaf-f1be402c8ea1" http://10.36.0.17:8080/api/v1/dataconn/5

  __Response__:

      {"result":"Success"}
