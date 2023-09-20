---
title: Piaras Hoban - Weaveworks
date: Dublin Kubernetes Meetup | MMMM dd, YYYY
paging: "%d / %d"
---
# Secure Delivery to Restricted Environments

# with the Open Component Model & Flux

<br>

<br>

<br>

<br>

Piaras Hoban - Weaveworks 

piaras@weave.works -  phoban01

https://ocm.software

slides @ https://github.com/phoban01/dkm-20.09.2023

---

# what is the open component model?

- specification for describing delivery & deployment artifacts   
- enables bundling & automatic deployment process for any kind software
- can be thought of as a **Software Bill of Delivery**

---

# what does it look like?

```yaml
# component-file.yaml
name: acme.io/server
version: v1.0.0
provider:
  name: acme.io
resources:
- name: server
  type: ociImage
  input:
    type: docker
    path: docker.io/nginx:1.25.2
- name: manifests
  type: dir
  input:
    type: dir
    path: manifests/
    compress: true
```
---

# problems ocm is trying to address

- technology agnostic packaging
- consistent compliant delivery across clouds
- automated deployment

---

# what does ocm consist of?

## packaging
  - specificiation (https://ocm.software/spec/) 
  - tooling to build, sign and examine components (https://github.com/open-component-model/ocm)

## delivery
  - support for different storage contexts (filesystem, archives, OCI registry)
  - tooling to support hermetic movement of components between storage backends

## deployment
  - Kubernetes controllers that leverage Flux to deploy components

---

# flux

- Kubernetes native GitOps tool (https://fluxcd.io)
- CNCF graduated project
- first-rate support for Kustomize, Helm
- deploy from Git, OCI or S3
- secure, lightweight & scalable 
- composable & extensible

---

# what do we mean by restricted environment?

- access to public internet is not guarenteed
- access to external registries is not guarenteed
- deployment from internal registries is mandated

---

# why is ocm helpful?

- ocm enables one time description of software artifacts & their deployment mechanism
- hermitic transfer including transitive dependencies
- tooling to support deployment when the storage context has changed
- gitops integration enables straightforward install & seamless updates

---

# demo

try it yourself: https://github.com/open-component-model/demo-secure-delivery

two hats: software provider & software consumer

provider (release automation):
- describe product that contains 2 components
- publish these components to an OCI registry

consumer (GitOps deployment automation):
- can only deploy from "internal" registry
- subscribes to provider registry
- pulls newly released compnents into "internal" registry
- components are automatically deployed using flux & ocm-controller

---

# more info

https://ocm.software

https://fluxcd.io

https://github.com/open-component-model
