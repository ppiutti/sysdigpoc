# sysdigpoc
Image signing and validation and integration testing with Sysdig, Connaisseur and Notary

This repository contains the YAML and JSON files required to enable the validation of signed, approved images in Kubernetes clusters through the Connaisseur Admission Controller.

The objective is to selectively enforce the validation of signed images on designated namespaces and send notifications to the Sysdig Secure UI for both approved and rejected deployments. The full reasoning / PoC flow behind this is available on Google Drive at

https://docs.google.com/document/d/181odH2sK_oeFFLKoZEUep_xBLMgZQmnvwC1TBP2jVoE/edit?usp=sharing

Comments are welcome.

The values.yaml file is a HELM configuration file for Connaisseur.

It is configured to:

a) allow the deployment of images signed with your own private key and uploaded to Docker Hub/Notary (just replace the public key with yours)

b) enable the deployment of Sysdig agents by whitelisting the quay.io repository

c) set namespaced validation to enforce signature checking only on specific namespaces (and allow without checking anywhere else)

d) send notifications to the Sysdig Secure UI when validation events happen


The sysdig.json file is a customizable template that can be used to craft the notifications being sent to Sysdig Secure and it is referenced in the values.yaml file. Further customization for the notification template can be achieved referencing to the Sysdig api/v1/eventsDispatch/ingest specification.
