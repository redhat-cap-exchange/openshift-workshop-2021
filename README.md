# Openshift Workshop 2021

Guides, links and code snippets for the Red Hat OpenShift Cloud Native Developer workshop

This document is not a "walk-through" or tutorial but more like a an "annotated" agenda that shows the outline of the workshop. The agenda, on a high-level, looks like this:

* Overview OpenShift & Cloud-Native Development
* Explore different ways to build & deploy a cloud native app on OpenShift
* CI/CD pipelines and GitOps (Tekton & ArgoCD)
* Operator Framework and Operator SDK

The intention of the workshop is to explain how to use Red Hat OpenShift to build and deploy cloud-native applications, using the platform itself as the underlying development and CI/CD infrastructure.

It is not the goal of the workshop to teach e.g. how to develop Java Spring Boot applications or such. The example application used in the workshop are not in focus and are only used to explain build, CI/CD and other OpenShift related concepts.

### Workshop Environment

The workshop uses Red Hat OpenShift cluster as the sole environment. All demos and lab activities use the cluster. Red Hat CodeReady workspaces is used as a hosted development environment and there is no need to install any development tools locally.

Details on how to access the hosted OpenShift environment will be provided before the workshop.

However, if someone wants to run the labs from her/his personal laptop, the following tools are required:

* VSCodium (or VisualStudio Code)
* OpenShift CLI (oc)
* Kubectl
* Tekton CLI (tkn)

#### OpenShift CLI and Kubectl

* https://docs.openshift.com/container-platform/4.6/cli_reference/openshift_cli/getting-started-cli.html

#### Tekton CLI

* https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/0.13.1/tkn-macos-amd64-0.13.1.tar.gz
* https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/0.13.1/tkn-windows-amd64-0.13.1.zip


### Hosted development and CI/CD tools

To support the workshop, the following OpenShift add-ons will be used:

* Red Hat CodeReady Workspaces
* Red Hat Pipelines
* GitOps tools (ArgoCD)
* Sonatype Nexus 3
* Gitea Git server


### Overview OpenShift & Cloud-Native Development

**LINK TO SLIDE DECK**

### Explore different ways to build & deploy an app 

#### Intermission: OpenShift Web Console orientation

#### Lab 1: Deploy a container from a registry, using the command line

```shell

oc new-project lab1

oc new-app sonatype/nexus3

oc rollout pause deployment/nexus3 

oc expose service/nexus3

oc set probe deployment/nexus3 --liveness --failure-threshold 3 --initial-delay-seconds 180 -- echo ok
oc set probe deployment/nexus3 --readiness --failure-threshold 3 --initial-delay-seconds 120 --get-url=http://:8081/nexus/content/groups/public

oc rollout resume deployment/nexus3 

```

#### Intermission: On-board the sample project into RH CodeReady Workspace

##### Step 1: Create a workspace

* Get Started -> Custom Workspace -> Select 'Java Spring Boot'

* Modify the devfile

Look for (ca. line 7):

```yaml
type: zip
location: 'https://devfile-registry-openshift-workspaces.apps.cluster-ccp-6e5e.ccp-6e5e.example.opentlc.com/resources/spring-boot-http-booster-spring-boot-http-booster-sb-2.3.x.zip'
```

Replace with:

```yaml
type: git
location: 'https://github.com/redhat-capgemini-exchange/spring-boot-http-booster.git'
```

##### Step 2: Configure mvn

* Local build & run

In the workspace, open a new terminal:

```shell
cp /projects/spring-boot-http-booster/.m2/settings.xml /home/jboss/.m2/settings.xml
```


#### Lab 3: mvn install, using Fabric8

* Deploy to OpenShift
* Log into OpenShift from the workspace console

```shell
oc logout

oc login <OPENSHIFT API URL>

oc new-project userXXX-lab3

```

```shell
mvn fabric8:deploy -Popenshift -DskipTests
```

#### Lab 4: Using S2I, deploy from GitHub, anatomy of an S2I image, customize the build process

* Deploy from GitHub
https://github.com/redhat-capgemini-exchange/spring-boot-http-booster
Builder Image Version: openjdk-11-ubi8

#### Lab 5: Modify the S2I process

see https://docs.openshift.com/container-platform/4.6/builds/build-strategies.html#builds-strategy-s2i-build_build-strategies

```shell
oc new-project userXXX-lab5

oc create -f secrets.yaml


```

Create a new deployment like in Lab 4, but use branch 's2i'

### CI/CD pipelines and GitOps

#### Lab 6: OpenShift Pipelines Tutorial

#### Create and run a pipeline

https://github.com/openshift/pipelines-tutorial/tree/release-tech-preview-2

```shell
oc new-project pipelines-tutorial

oc get serviceaccount pipeline

oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/release-tech-preview-2/01_pipeline/01_apply_manifest_task.yaml

oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/release-tech-preview-2/01_pipeline/02_update_deployment_task.yaml

tkn task ls

tkn clustertasks ls

oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/release-tech-preview-2/01_pipeline/04_pipeline.yaml

tkn pipeline ls

oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/release-tech-preview-2/01_pipeline/03_persistent_volume_claim.yaml

tkn pipeline start build-and-deploy \
    -w name=shared-workspace,claimName=source-pvc \
    -p deployment-name=vote-api \
    -p git-url=http://github.com/openshift-pipelines/vote-api.git \
    -p IMAGE=image-registry.openshift-image-registry.svc:5000/pipelines-tutorial/vote-api

tkn pipeline start build-and-deploy \
    -w name=shared-workspace,claimName=source-pvc \
    -p deployment-name=vote-ui \
    -p git-url=http://github.com/openshift-pipelines/vote-ui.git \
    -p IMAGE=image-registry.openshift-image-registry.svc:5000/pipelines-tutorial/vote-ui

tkn pipeline list

tkn pipelinerun ls

tkn pipeline logs -f
```

To repeat the last pipeline run:

```shell
tkn pipeline start build-and-deploy --last
```

#### Add triggers

```shell
oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/release-tech-preview-2/03_triggers/02_template.yaml

oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/release-tech-preview-2/03_triggers/01_binding.yaml

oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/release-tech-preview-2/03_triggers/03_event_listener.yaml

```


### Overview Operator Framework and Operator SDK

Wait for day 2 !
