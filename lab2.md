# openshift-workshop-2021 - Lab 2

Guides and code snippets for Lab 2

https://docs.openshift.com/container-platform/4.6/pipelines/creating-applications-with-cicd-pipelines.html

Install the OpenShift Pipelines Operator

Install the CLI

https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/0.13.1/tkn-macos-amd64-0.13.1.tar.gz
https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/0.13.1/tkn-windows-amd64-0.13.1.zip

```shell
export TKN_VERSION=0.13.1

cd /tmp
wget https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/$TKN_VERSION/tkn-linux-amd64-$TKN_VERSION.tar.gz

tar -xzf tkn-linux-amd64-$TKN_VERSION.tar.gz
mv tkn /home/jboss

echo "export PATH=/home/jboss:$PATH" >> .bash_profile

cd
. .bash_profile
```

Pipelines Tutorial
https://github.com/openshift/pipelines-tutorial/tree/release-tech-preview-2
