# Secure-Your-Kubernetes

## Your Kubernetes Clusters Are NOT Secure
Wild guess, you've been told you have to run Kubernetes, but don't quite know where to start right? This repo is meant as a way to help you secure your cluster in the more efficient COST EFFECTIVE way. There are plenty of solutions that will secure your Kubernetes clusters, but this is for you to start with before talking to those groups. 

I am also open to feedback and pull requests from other K8s practitioners. This is meant to help those in need.

## Table of Contents
1. Cluster Setup & Hardening (RBAC / Controlplane / Kubelet)
2. Supply Chain
3. Runtime Security
4. Monitoring & Logging


## Cluster Setup & Hardening

### RBAC (Role Based Access Control)
When you deploy workloads into Kubernetes clusters, by default the users will have access to everything they can touch. Because of this, you want to give each user only the specific amount of privileges needed for them to do their job. 
Pulling this from [Okta's website](https://www.okta.com/identity-101/minimum-access-policy/#:~:text=A%20minimum%20access%20policy%20restricts,employees%20to%20do%20their%20jobs.) 
```
"A minimum access policy restricts a user to only the least amount of access to privileged resources and permissions that are needed to perform an authorized activity or activities, such as those necessary for employees to do their jobs."
```

What are the benefits of utilizing RBAC?
* Least Privilege: Users only have access to what they need.
* Reduced Attack Surface: Limits damage from compromised accounts.
* Improved Auditability: Tracks who has access to what.
* RBAC Components: Because of this, we need to learn about the components of RBAC in Kubernetes. 

Roles/ClusterRoles: Define sets of permissions for resources within a namespace (Roles) or across the entire cluster (ClusterRoles).
Subjects: Describe the entities (Users, Groups, Service Accounts) that RBAC manages access for.
RoleBindings/ClusterRoleBindings: Explain how these bind Roles/ClusterRoles to Subjects, granting them specific permissions.

Two examples to look at, Role and ClusterRole:
Role
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```
Cluster Role
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  # "namespace" omitted since ClusterRoles are not namespaced
  name: secret-reader
rules:
- apiGroups: [""]
  #
  # at the HTTP level, the name of the resource for accessing Secret
  # objects is "secrets"
  resources: ["secrets"]
  verbs: ["get", "watch", "list"]
```

A ClusterRole | Role defines a set of permissions and where it is available, in the whole cluster or just a single Namespace.

A ClusterRoleBinding | RoleBinding connects a set of permissions with an account and defines where it is applied, in the whole cluster or just a single Namespace.

Because of this there are 4 different RBAC combinations:

Role + RoleBinding (available in single Namespace, applied in single Namespace)
ClusterRole + ClusterRoleBinding (available cluster-wide, applied cluster-wide)
ClusterRole + RoleBinding (available cluster-wide, applied in single Namespace)
Role + ClusterRoleBinding (NOT POSSIBLE: available in single Namespace, applied cluster-wide)



## Supply Chain

## Runtime Security

## Monitoring / Logging


https://overcast.blog/13-docker-tricks-you-didnt-know-47775a4f678f

https://krew.sigs.k8s.io/plugins/

https://overcast.blog/18-kubernetes-security-tools-you-should-know-f3f13425df7b

https://faun.pub/kubernetes-the-right-way-security-checklist-c38650898807

https://collabnix.github.io/kubetools/#cost-optimisation

https://collabnix.github.io/kubetools/#cost-optimisation

Karpenter
https://karpenter.sh/docs/
