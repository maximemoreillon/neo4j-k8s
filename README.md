# Neo4J K8s

This is a Kubernetes manifest for a Neo4J instance.
Bolt connection to the instance is secured using SSL.
The SSL certificates are obtained using cert-manager.

## Restoring a backup

1. Deploy the content of the manifest in the Kubernetes cluster
2. Copy the .dump of the database to import in Neo4J's persistent volum

```
kubectl cp ./neo4j_backup.dump yournamespace/neo4j-7b95c4ccfb-jhh6x:/data/
```

3. Uncomment the import commands from the deployment
```
command: ["neo4j-admin"]
args: ["load", "--from=/data/neo4j_backup.dump", "--force"]
```

4. Re-apply the manifest
5. Once the import has succeeded, recomment the lines uncommented in 3.
6. Re-apply the manifest