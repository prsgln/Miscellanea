# MISCELLANEA
Those are useful command to have in the pocket like a swissknife :)

## WILDFLY Logging
Enabing the dumping of the HTTP requests in the Wldfly  - tested wildfly-16.0.0.Final
```bash
cat <<EOF>enable-request-dumping-handler.cli
batch
/subsystem=undertow/configuration=filter/custom-filter=request-logging-filter:add(class-name=io.undertow.server.handlers.RequestDumpingHandler,module=io.undertow.core)
/subsystem=undertow/server=default-server/host=default-host/filter-ref=request-logging-filter:add
run-batch
EOF

./wildfly-16.0.0.Final/bin/jboss-cli.sh --connect --file=enable-request-dumping-handler.cli
```
To verify 
```
 curl --show-error --fail --user "k8s-liveness:$(cat /opt/avaloq/config/K8S_LIVENESS_PASSWORD)" http://localhost:8080/AWS/dashboard/metrics
```

## Replicaset/Stetefulset scaling
  ```
  oc scale statefulset/avaloq-aws --replicas=1
  ```
  or
  ```
  oc scale replicaset/avaloq-aws --replicas=1
  ```