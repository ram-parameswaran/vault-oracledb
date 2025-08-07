1. Vault license - 


# vault license get -format=json | jq .data
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
    "license_id": "3dea5a15-0e91-f133-6f80-e78bcd8c772d",
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

Plugin location - 

# ls -la /vault/plugin/vault-plugin-database-oracle_0.12.3_linux_amd64/
total 47580
drwxr-xr-x 1 501 dialout      256 Aug  6 06:15 .
drwxr-xr-x 1 501 dialout      416 Aug  6 06:17 ..
-rw-rw-r-- 1 501 dialout    31486 Jun 13 21:38 EULA.txt
-rw-rw-r-- 1 501 dialout     9518 Jun 13 21:38 TermsOfEvaluation.txt
-rw-rw-r-- 1 501 dialout     1097 Jun 13 21:39 metadata.json
-r-------- 1 501 dialout      832 Jun 13 21:39 metadata.json.sig
-rwxr-xr-x 1 501 dialout 32747296 Jun 13 21:38 vault-plugin-database-oracle
-rw-r--r-- 1 501 dialout 15911672 Aug  6 06:14 vault-plugin-database-oracle_0.12.3+ent_linux_amd64.zip
root@492a430bf3a6:/#

register plugin - 

vault plugin register -sha256=${SHASUM256} -version=0.12.3 
-env VAULT_LICENSE=<license_string> database vault-plugin-database-oracle
Success! Registered plugin: vault-plugin-database-oracle


# vault write database/config/my-oracle-database      plugin_name=vault-plugin-database-oracle      connection_url="{{username}}/{{password}}@oracle-xe:1521/XEPDB1"      username="vault"      password="vaultpasswd"      allowed_roles=my-role      max_connection_lifetime=60s
Error writing data to database/config/my-oracle-database: Error making API request.

URL: PUT http://127.0.0.1:8200/v1/database/config/my-oracle-database
Code: 400. Errors:

* error creating database object: unable to initialize: rpc error: code = Internal desc = failed to initialize: the Oracle Database Secrets Engine feature requires a licensed Vault Enterprise server


vault      | 2025-08-07T02:06:47.236Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:47.760Z [DEBUG] secrets.database.database_b39f246a: pinning "vault-plugin-database-oracle" database plugin version "v0.12.3" from candidates [{database vault-plugin-database-oracle v0.12.3   eef0864b88e6bf99044fb44b15905604d6f04a6289029bb4d2ed91de8da5f776 false  0.12.3}]
vault      | 2025-08-07T02:06:47.767Z [DEBUG] core: spawning a new plugin process: plugin_name=vault-plugin-database-oracle id=TW1YUqoKbw
vault      | 2025-08-07T02:06:48.496Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:49.457Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:50.207Z [INFO]  secrets.database.database_b39f246a.vault-plugin-database-oracle: configuring client automatic mTLS
vault      | 2025-08-07T02:06:50.284Z [DEBUG] secrets.database.database_b39f246a.vault-plugin-database-oracle: starting plugin: path=/vault/plugin/vault-plugin-database-oracle_0.12.3_linux_amd64/vault-plugin-database-oracle args=["/vault/plugin/vault-plugin-database-oracle_0.12.3_linux_amd64/vault-plugin-database-oracle"]
vault      | 2025-08-07T02:06:50.344Z [DEBUG] secrets.database.database_b39f246a.vault-plugin-database-oracle: plugin started: path=/vault/plugin/vault-plugin-database-oracle_0.12.3_linux_amd64/vault-plugin-database-oracle pid=367
vault      | 2025-08-07T02:06:50.350Z [DEBUG] secrets.database.database_b39f246a.vault-plugin-database-oracle: waiting for RPC address: plugin=/vault/plugin/vault-plugin-database-oracle_0.12.3_linux_amd64/vault-plugin-database-oracle
vault      | 2025-08-07T02:06:50.605Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:51.655Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=1
vault      | 2025-08-07T02:06:51.773Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:06:51.773Z [DEBUG] replication.index.periodic: starting WAL GC: from=13068 to=13071 last=13327
vault      | 2025-08-07T02:06:51.988Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:52.621Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:53.825Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:54.816Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:55.949Z [INFO]  secrets.database.database_b39f246a.vault-plugin-database-oracle.vault-plugin-database-oracle: configuring server automatic mTLS: timestamp=2025-08-07T02:06:55.945Z
vault      | 2025-08-07T02:06:56.023Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:56.134Z [DEBUG] secrets.database.database_b39f246a.vault-plugin-database-oracle.vault-plugin-database-oracle: plugin address: address=/tmp/plugin2820072675 network=unix timestamp=2025-08-07T02:06:56.133Z
vault      | 2025-08-07T02:06:56.137Z [DEBUG] secrets.database.database_b39f246a.vault-plugin-database-oracle: using plugin: version=6
vault      | 2025-08-07T02:06:56.473Z [TRACE] secrets.database.database_b39f246a.vault-plugin-database-oracle.stdio: waiting for stdio data
vault      | 2025-08-07T02:06:56.654Z [DEBUG] secrets.database.database_b39f246a: got database plugin instance: type=oci8
vault      | 2025-08-07T02:06:56.656Z [TRACE] secrets.database.database_b39f246a.vault-plugin-database-oracle: initialize: transport="" status=started
vault      | 2025-08-07T02:06:56.671Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:06:56.705Z [TRACE] secrets.database.database_b39f246a.vault-plugin-database-oracle: initialize: transport="" status=finished verify=true err="unable to initialize: rpc error: code = Internal desc = failed to initialize: the Oracle Database Secrets Engine feature requires a licensed Vault Enterprise server" took=49.108225ms
vault      | 2025-08-07T02:06:56.706Z [TRACE] secrets.database.database_b39f246a.vault-plugin-database-oracle: close: transport="" status=started
vault      | 2025-08-07T02:06:56.733Z [DEBUG] core.vault-plugin-database-oracle: cleaning up plugin client connection: id=TW1YUqoKbw
vault      | 2025-08-07T02:06:56.737Z [DEBUG] core: removed plugin client connection: id=TW1YUqoKbw
vault      | 2025-08-07T02:06:56.751Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:06:56.754Z [DEBUG] replication.index.periodic: starting WAL GC: from=13072 to=13076 last=13332
vault      | 2025-08-07T02:06:56.805Z [DEBUG] secrets.database.database_b39f246a.vault-plugin-database-oracle.stdio: received EOF, stopping recv loop: err="rpc error: code = Unavailable desc = error reading from server: EOF"
vault      | 2025-08-07T02:06:56.869Z [INFO]  secrets.database.database_b39f246a.vault-plugin-database-oracle: plugin process exited: plugin=/vault/plugin/vault-plugin-database-oracle_0.12.3_linux_amd64/vault-plugin-database-oracle id=367
vault      | 2025-08-07T02:06:56.870Z [DEBUG] secrets.database.database_b39f246a.vault-plugin-database-oracle: plugin exited
vault      | 2025-08-07T02:06:56.870Z [DEBUG] core: killed external multiplexed plugin process: plugin=/vault/plugin/vault-plugin-database-oracle_0.12.3_linux_amd64/vault-plugin-database-oracle pluginID=367
vault      | 2025-08-07T02:06:56.871Z [TRACE] secrets.database.database_b39f246a.vault-plugin-database-oracle: close: transport="" status=finished err=<nil> took=164.103068ms
vault      | 2025-08-07T02:06:57.050Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:58.250Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:06:59.200Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:00.205Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:01.413Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:01.599Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:07:01.637Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:07:01.637Z [DEBUG] replication.index.periodic: starting WAL GC: from=13077 to=13081 last=13337
vault      | 2025-08-07T02:07:02.398Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:03.399Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:04.608Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:05.598Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:06.613Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=1
vault      | 2025-08-07T02:07:06.673Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:07:06.674Z [DEBUG] replication.index.periodic: starting WAL GC: from=13082 to=13085 last=13341
vault      | 2025-08-07T02:07:06.771Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:07.810Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:08.799Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:10.020Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:11.006Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:11.607Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:07:11.664Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:07:11.665Z [DEBUG] replication.index.periodic: starting WAL GC: from=13086 to=13090 last=13346
vault      | 2025-08-07T02:07:12.001Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:13.007Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:14.211Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:15.206Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:16.218Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
vault      | 2025-08-07T02:07:16.610Z [DEBUG] replication.index.perf: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:07:16.665Z [DEBUG] replication.index.local: saved checkpoint: num_dirty=0
vault      | 2025-08-07T02:07:16.665Z [DEBUG] replication.index.periodic: starting WAL GC: from=13091 to=13095 last=13351
vault      | 2025-08-07T02:07:17.211Z [DEBUG] replication.index.perf: flushed dirty pages: pages_flushed=1 pages_outstanding=0
