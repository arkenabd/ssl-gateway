

oc login -u developer https://paas.pajak.go.id
oc project api

oc new-app fuse7-java-openshift:1.3 --code=. --name=ssl-gateway-efaktur --strategy=source
mvn clean package

oc start-build ssl-gateway-efaktur --from-file=target/ssl-gateway-1.0.0-SNAPSHOT.jar --follow

oc delete dc/ssl-gateway
oc delete bc/ssl-gateway
oc delete svc/ssl-gateway
oc delete route/ssl-gateway