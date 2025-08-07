1. Testing success with Vault 1.19.7+ent,Vault 1.20.0+ent, Vault 1.20.1+ent

2. Vault license - 


# vault license get -format=json | jq .data
```
{
  "autoloaded": {
    "expiration_time": "2025-09-10T00:00:00Z",
    "features": [
      "HSM",
      "Performance Replication",
      "DR Replication",
      "MFA",
      "Sentinel",
      "Seal Wrapping",
      "Control Groups",
      "Performance Standby",
      "Namespaces",
      "KMIP",
      "Entropy Augmentation",
      "Transform Secrets Engine",
      "Lease Count Quotas",
      "Key Management Secrets Engine",
      "Automated Snapshots",
      "Key Management Transparent Data Encryption",
      "Secrets Sync"
    ],
    "license_id": "hkhkjhkjhkjhkjhkjhkj",
    "performance_standby_count": 9999,
    "start_time": "2025-07-11T00:00:00Z",
    "termination_time": "2027-08-10T00:00:00Z"
  },
  "autoloading_used": true,
  "persisted_autoload": {
    "expiration_time": "2025-09-10T00:00:00Z",
    "features": [
      "HSM",
      "Performance Replication",
      "DR Replication",
      "MFA",
      "Sentinel",
      "Seal Wrapping",
      "Control Groups",
      "Performance Standby",
      "Namespaces",
      "KMIP",
      "Entropy Augmentation",
      "Transform Secrets Engine",
      "Lease Count Quotas",
      "Key Management Secrets Engine",
      "Automated Snapshots",
      "Key Management Transparent Data Encryption",
      "Secrets Sync"
    ],
    "license_id": "3dea5a15-0e91-f133-6f80-e78bcd8c772d",
    "performance_standby_count": 9999,
    "start_time": "2025-07-11T00:00:00Z",
    "termination_time": "2027-08-10T00:00:00Z"
  }
}
```

3. Plugin location - **Named the folder to be exactly the name of the zip file**

# ls -la /vault/plugin/vault-plugin-database-oracle_0.12.3+ent_linux_amd64/
```
total 47580
drwxr-xr-x 1 501 dialout      256 Aug  6 06:15 .
drwxr-xr-x 1 501 dialout      416 Aug  6 06:17 ..
-rw-rw-r-- 1 501 dialout    31486 Jun 13 21:38 EULA.txt
-rw-rw-r-- 1 501 dialout     9518 Jun 13 21:38 TermsOfEvaluation.txt
-rw-rw-r-- 1 501 dialout     1097 Jun 13 21:39 metadata.json
-r-------- 1 501 dialout      832 Jun 13 21:39 metadata.json.sig
-rwxr-xr-x 1 501 dialout 32747296 Jun 13 21:38 vault-plugin-database-oracle
-rw-r--r-- 1 501 dialout 15911672 Aug  6 06:14 vault-plugin-database-oracle_0.12.3+ent_linux_amd64.zip
```

4. register plugin - Using command in the zip file tab [here](https://developer.hashicorp.com/vault/docs/plugins/register#step-2-update-the-plugin-catalog )
The version of the plugin should be exactly same as the version in the folder name i.e version for vault-plugin-database-oracle_0.12.3+ent_linux_amd64 will be 0.12.3+ent
```
vault plugin register -version=0.12.3+ent database vault-plugin-database-oracle
Success! Registered plugin: vault-plugin-database-oracle
```

5. Logs from plugin registration test
```
vault      | 2025-08-07T03:46:34.552Z [DEBUG] core: attempting to load database plugin as v5: name=vault-plugin-database-oracle
vault      | 2025-08-07T03:46:34.556Z [DEBUG] core: spawning a new plugin process: plugin_name=vault-plugin-database-oracle id=gTvt9rwKxy
vault      | 2025-08-07T03:46:34.605Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:46:35.670Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:46:36.770Z [INFO]  configuring client automatic mTLS
vault      | 2025-08-07T03:46:36.812Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:46:37.194Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=0
vault      | 2025-08-07T03:46:37.284Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T03:46:37.284Z [DEBUG] replication.index.periodic: starting WAL GC: from=17722 to=17726 last=17982
vault      | 2025-08-07T03:46:37.797Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:46:39.003Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:46:40.026Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:46:41.206Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:46:42.105Z [INFO]  vault-plugin-database-oracle: configuring server automatic mTLS: timestamp=2025-08-07T03:46:42.101Z
vault      | 2025-08-07T03:46:42.183Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=1
vault      | 2025-08-07T03:46:42.236Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T03:46:42.237Z [DEBUG] replication.index.periodic: starting WAL GC: from=17727 to=17730 last=17986
vault      | 2025-08-07T03:46:42.384Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:46:42.579Z [DEBUG] core: removed plugin client connection: id=gTvt9rwKxy
vault      | 2025-08-07T03:46:42.614Z [INFO]  plugin process exited: plugin="/vault/plugin/vault-plugin-database-oracle_0.12.3+ent_linux_amd64/vault-plugin-database-oracle" id=592
vault      | 2025-08-07T03:46:42.617Z [DEBUG] core: killed external multiplexed plugin process: plugin="/vault/plugin/vault-plugin-database-oracle_0.12.3+ent_linux_amd64/vault-plugin-database-oracle" pluginID=592
```

6. Testing the database config setup
```
vault write database/config/my-oracle-database      plugin_name=vault-plugin-database-oracle      connection_url="{{username}}/{{password}}@oracle-xe:1521/XEPDB1"      username="vault"      password="vaultpasswd"      allowed_roles=my-role      max_connection_lifetime=60s
Success! Data written to: database/config/my-oracle-database
```

7. Logs from Testing the database config setup
```
vault      | 2025-08-07T03:48:55.262Z [DEBUG] secrets.database.database_ad70adf2: pinning "vault-plugin-database-oracle" database plugin version "v0.12.3+ent" from candidates [{database vault-plugin-database-oracle v0.12.3+ent   eef0864b88e6bf99044fb44b15905604d6f04a6289029bb4d2ed91de8da5f776 false  0.12.3+ent}]
vault      | 2025-08-07T03:48:55.271Z [DEBUG] core: spawning a new plugin process: plugin_name=vault-plugin-database-oracle id=USXAV9ipkO
vault      | 2025-08-07T03:48:56.279Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:48:57.361Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=1
vault      | 2025-08-07T03:48:57.469Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T03:48:57.469Z [DEBUG] replication.index.periodic: starting WAL GC: from=17859 to=17862 last=18118
vault      | 2025-08-07T03:48:57.817Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:48:58.676Z [INFO]  secrets.database.database_ad70adf2.vault-plugin-database-oracle: configuring client automatic mTLS
vault      | 2025-08-07T03:48:58.716Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:48:58.824Z [DEBUG] secrets.database.database_ad70adf2.vault-plugin-database-oracle: starting plugin: path="/vault/plugin/vault-plugin-database-oracle_0.12.3+ent_linux_amd64/vault-plugin-database-oracle" args=["/vault/plugin/vault-plugin-database-oracle_0.12.3+ent_linux_amd64/vault-plugin-database-oracle"]
vault      | 2025-08-07T03:48:58.918Z [DEBUG] secrets.database.database_ad70adf2.vault-plugin-database-oracle: plugin started: path="/vault/plugin/vault-plugin-database-oracle_0.12.3+ent_linux_amd64/vault-plugin-database-oracle" pid=616
vault      | 2025-08-07T03:48:58.921Z [DEBUG] secrets.database.database_ad70adf2.vault-plugin-database-oracle: waiting for RPC address: plugin="/vault/plugin/vault-plugin-database-oracle_0.12.3+ent_linux_amd64/vault-plugin-database-oracle"
vault      | 2025-08-07T03:48:59.950Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:01.020Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:02.080Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:02.268Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=0
vault      | 2025-08-07T03:49:02.363Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T03:49:02.363Z [DEBUG] replication.index.periodic: starting WAL GC: from=17863 to=17867 last=18123
vault      | 2025-08-07T03:49:03.285Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:04.264Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:05.850Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:06.655Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:07.216Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=0
vault      | 2025-08-07T03:49:07.340Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T03:49:07.341Z [DEBUG] replication.index.periodic: starting WAL GC: from=17868 to=17871 last=18127
vault      | 2025-08-07T03:49:07.851Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:08.800Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:08.958Z [INFO]  secrets.database.database_ad70adf2.vault-plugin-database-oracle.vault-plugin-database-oracle: configuring server automatic mTLS: timestamp=2025-08-07T03:49:08.935Z
vault      | 2025-08-07T03:49:09.188Z [DEBUG] secrets.database.database_ad70adf2.vault-plugin-database-oracle: using plugin: version=6
vault      | 2025-08-07T03:49:09.189Z [DEBUG] secrets.database.database_ad70adf2.vault-plugin-database-oracle.vault-plugin-database-oracle: plugin address: address=/tmp/plugin2861550028 network=unix timestamp=2025-08-07T03:49:09.186Z
vault      | 2025-08-07T03:49:09.506Z [TRACE] secrets.database.database_ad70adf2.vault-plugin-database-oracle.stdio: waiting for stdio data
vault      | 2025-08-07T03:49:09.804Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:09.905Z [DEBUG] secrets.database.database_ad70adf2: got database plugin instance: type=oci8
vault      | 2025-08-07T03:49:09.910Z [TRACE] secrets.database.database_ad70adf2.vault-plugin-database-oracle: initialize: transport="" status=started
vault      | 2025-08-07T03:49:11.026Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:49:12.118Z [TRACE] secrets.database.database_ad70adf2.vault-plugin-database-oracle: initialize: transport="" status=finished verify=true err=<nil> took=2.208717726s
vault      | 2025-08-07T03:49:12.127Z [DEBUG] secrets.database.database_ad70adf2: created database object: name=my-oracle-database plugin_name=vault-plugin-database-oracle
vault      | 2025-08-07T03:49:12.133Z [DEBUG] secrets.database.database_ad70adf2: Deregistering rotation job: mount=database/config/my-oracle-database
vault      | 2025-08-07T03:49:12.133Z [DEBUG] rotation-job-manager: attempting deregistering rotation job with ID if it exists (nil op otherwise): rotationID=database/config/my-oracle-database
```

8. Testing the database role setup
```
vault write database/roles/my-role     db_name=my-oracle-database     creation_statements='CREATE USER {{username}} IDENTIFIED BY "{{password}}"; GRANT CONNECT TO {{username}}; GRANT CREATE SESSION TO {{username}};'     default_ttl="1h"     max_ttl="24h"
Success! Data written to: database/roles/my-role
```

9. Testing the database role creds
```
vault read database/creds/my-role
Key                Value
---                -----
lease_id           database/creds/my-role/UXlnk1sJ5843LToNa4lRqw8Q
lease_duration     1h
lease_renewable    true
password           8oDe1BYQ3Xkh1iRQaqv-
username           V_ROOT_MY_ROLE_5ZMHLWKHEPFAPQI
```
10. Logs from database role creds test
```
vault      | 2025-08-07T03:50:58.009Z [TRACE] secrets.database.database_ad70adf2.vault-plugin-database-oracle: create user: transport="" status=started
vault      | 2025-08-07T03:50:58.814Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:51:00.019Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T03:51:00.778Z [TRACE] secrets.database.database_ad70adf2.vault-plugin-database-oracle: create user: transport="" status=finished err=<nil> took=2.769119672s
```
