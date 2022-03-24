# Home infrastructure

This is a gitops approach to my home lab.
Currently the philosophy is that bootstrap is the ansible playbooks to deal with a 'null' state.
This will take newly imaged raspberry pis, and then install argocd, which manages most of the applications
on the platform

The philosophy is that gitops should be used as much as posisble (argocd), but for manual steps, we use
ansible (more procedural). Manual intervention is more likely in the ansible stage, whereas the argocd stage should
be more self-healing and consistent.

## Secrets

Secrets are depoyed/managed using passwordstore, and which is thus out of band of this repo,
and encrypted. Ansible is able to look this up, thus convert secrets into k8s secrets as appropriate.

This is part of the bootstrap stage, and is core infrastructure.

## Storage

Storage is managed using NFS to an external nas. This is also very procedural, so falls under bootstrap.


## Cluster

Any cluster specific configuration that argocd can manage is run from here. At the moment
this is mainly creating roles (this might make more sense in bootstrap).

## Projects

In projects is the definition of argocd projects, and then links to the applications

## Apps

This is the k8s deployments and other manifests to run an application. Usually using kustomize
