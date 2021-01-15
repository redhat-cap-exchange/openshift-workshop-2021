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
* Gogs Git server


### Overview OpenShift & Cloud-Native Development

**LINK TO SLIDE DECK**


### Explore different ways to build & deploy an app 

#### Intermission: OpenShift Web Console orientation

#### Lab 1: Deploy a container from a registry, using the command line

#### Intermission: On-board the sample project into RH CodeReady Workspace

#### Lab 2: mvn install, using Fabric8

#### Lab 3: Using S2I, deploy from GitHub, anatomy of an S2I image, customize the build process


### CI/CD pipelines and GitOps (Tekton & ArgoCD)

#### Lab 6: OpenShift Pipelines Tutorial
https://github.com/openshift/pipelines-tutorial/tree/release-tech-preview-2

### Overview Operator Framework and Operator SDK

#### Lab 6: Install a simple Operator and self-provision instances