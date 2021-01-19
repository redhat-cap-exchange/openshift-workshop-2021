# Sonatype Nexus 3

### Install a Nexus 3 instance:

* [Sonatype/Nexus3](https://hub.docker.com/r/sonatype/nexus3)
* [Nexus and Maven](https://blog.sonatype.com/using-nexus-3-as-your-repository-part-1-maven-artifacts)

```shell
export NAMESPACE=openshift-workspaces

oc project $NAMESPACE

oc new-app sonatype/nexus3 -n $NAMESPACE

oc rollout pause deployment/nexus3 

oc expose service/nexus3
oc set probe deployment/nexus3 --liveness --failure-threshold 3 --initial-delay-seconds 180 -- echo ok
oc set probe deployment/nexus3 --readiness --failure-threshold 3 --initial-delay-seconds 120 --get-url=http://:8081/nexus/content/groups/public
oc set volume deployment/nexus3 --add --name 'nexus3-volume-1' --type 'pvc' --mount-path '/nexus-data/' --claim-name 'nexus-data' --claim-size '10G' --overwrite

oc rollout resume deployment/nexus3 

```

### Credentials

Get the admin password from the pod's terminal:

```shell
cat /nexus-data/admin.password
```

### Configure workspace

```shell
cp /projects/spring-boot-http-booster/.m2/settings.xml /home/jboss/.m2/settings.xml
```
