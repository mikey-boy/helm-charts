# AKS RBAC

This chart is used to deploy Kubernetes RBAC objects (rolebinding, serviceaccounts) and also track namespaces within the cluster. The default values file is empty, meaning no objects are created by default. Each tenant should specify a custom values file populated with the following pieces of information:

1. Namespaces they control (and whether they exist already or should be installed)
2. RBAC policies binding AAD security groups to the above namespaces
3. Any service accounts needed by their deployed applications

## Values file example

A file named *values.example.yaml* can be referenced for how to setup a values file for this chart.

## Chart parameters

Name                                        | Description                                                        | Value Type
--------------------------------------------|--------------------------------------------------------------------|------------
namespaces                                  | Namespaces controlled by this tenant                               | {}
namespaces.install                          | Namespaces that will be created                                    | []
namespaces.exists                           | Namespaces that are "tracked"                                      | []
groups                                      | List of AAD groups and their associated binding in the cluster     | []
groups[i].name                              | Name of the (Cluster)RoleBinding to be created in the AKS          | ""
groups[i].id                                | ObjectID of the Azure security group                               | ""
groups[i].bindings                          | List of bindings that give the AAD group privileges                | []
groups[i].bindings[j].role                  | ClusterRole given to the AAD group                                 | ""
groups[i].bindings[j].scope                 | Scope of the binding, "cluster" or "namespace"                     | ""
groups[i].bindings[j].namespaces            | Namespaces for the RoleBinding (if namespace-scoped)               | []
serviceAccounts                             | List of service accounts to be created                             | []
serviceAccounts[i].name                     | Name of the service account                                        | ""
serviceAccounts[i].namespace                | Namespace of the service account                                   | []
serviceAccounts[i].bindings                 | List of bindings that give the service account privileges          | []
serviceAccounts[i].bindings[j].role         | ClusterRole given to the service account                           | ""
serviceAccounts[i].bindings[j].scope        | Scope of the binding, "cluster" or "namespace"                     | ""
serviceAccounts[i].bindings[j].namespaces   | Namespaces for the RoleBinding (if namespace-scoped)               | []
