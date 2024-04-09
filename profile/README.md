# Introduction

The evolution of network connectivity management has been significantly influenced by the integration of cloud technologies, CI/CD/GitpOps and container orchestration platforms, such as Kubernetes.

Traditionally, core network operations have been the purview of network operations (NetOps) teams, who have specialized in the configuration, maintenance, monitoring, and automation of physical and virtual network components.
While we don't see NetOps/SecOps roles changing much in managing network infrastructure, the shift towards cloud-native applications and microservices architecture necessitates a shift left outlook for vendor provided core networking and security.
This integration is imperative to provision connectivity and control access within the network in an automated and efficient manner. The goal here is to provide an open interface for connectivity and access control through  a plugin based architecture. Vendors are encouraged to write their plugin and implement the open interface that would allow an application developer to connect network domains and application components.

ANI (Application Network Interface) will enable application administrators to interact directly with core network components, facilitating automated provisioning, configuration, and security enforcement based on application needs.
This interface abstracts the complexity of the network operations, allowing CloudOps and Dev(Sec)Ops teams to provision connectivity, access control, certain connection, observability and security policies to ensure application performance and security without in-depth networking knowledge. AWI (Application WAN Interface) is a subset of the overall vision of ANI.

AWI (Application WAN Interface) provides an application centric programmable interface for WAN controllers. This interface allows DevOps and CloudOps to program enterprise WAN solutions to provision connectivity with “network SLA (Service Level Agreements)” and define workload access policy across networking domains. It is a vendor agnostic interface that has provisions for vendors to write their controller program logic as a plugin into AWI interface.  

# Repositories


+ [[awi-grpc](https://github.com/app-net-interface/awi-grpc)] 

    This repository has the interface definition for 1) network domain connectivity and access control.  2) Application Access Control. The interfaces are defined both in YAML and through protobuf. Connection related YAML files can be found [[here](https://github.com/app-net-interface/awi-grpc/tree/main/yaml/connection-schema)]
+ [[awi-infra-guard](https://github.com/app-net-interface/awi-infra-guard)]

    This repository allows discovery of resources in a cloud provider (AWS/GCP/Azure) environment that can be used in the connext of a connection. A resource could be a VPC, subnet, instance, a kubernetes service, namespace etc. This is used within kube-awi. It can also run independently on MacOS/Linux . 

+ [[kube-awi](https://github.com/app-net-interface/kube-awi)]
    AWI k8s operator. With AWI operator installed, user can connect VPCs and VRF in multi-cloud environment using kubectl. 
+ [[awi-install](https://github.com/app-net-interface/awi-install)]

    Helm chart(s) to install kubernetes operator. Also has script to do a full stack implementation. 

+ [[awi-cli](https://github.com/app-net-interface/awi-cli)]
    AWI CLI allows users to leverage AWI eco-system from a non-kubernetes envrionment. 
+ [[awi-grpc-catalyst-sdwan](https://github.com/app-net-interface/awi-grpc-catalyst-sdwan)]
    AWI GRPC plugin for Cisco Catalyst SDWAN controller. This plugin is used within kube-awi. It can also run independently on MacOS/Linux . 

+ [[catalyst-sdwan-app-client](https://github.com/app-net-interface/catalyst-sdwan-app-client)]
    Catalyst SDWAN controller application client. This is not officially supported by Cisco Catalyst SDWAN team. It's used as a package from within Catalyst SDWAN controller plugin. 
+ [[kubernetes-discovery](https://github.com/app-net-interface/kubernetes-discovery)]
    Allows discovery of kubernetes clustsers , pods and services. It also watches resources for changes and has notifiers. This is used within AWI Infra Guard as a library to discover kubernetes resources, but can be used independently as well.

# Contribution Guidelines

Thank you for your interest in contributing to awi-infra-guard! Please
make sure you read the full [code of conduct](code-of-conduct.md) before making
any contribution.

Before contributing to this repository, please first create an issue discussing
the change you wish to make or discuss about it via email with one of the
owners of the project.

We kindly ask you to follow the following code of conduct in all your
interactions with the project.

## Forking the project

Before doing any work, please make sure you are working on a local fork of the
project. For more information and instructions on how to do so, please refer to
[GitHub's contributing guide](https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project).

## Reporting Issues

Before reporting a new issue, please ensure that the issue was not already
reported or fixed by searching through our
[issues list](https://github.com/app-net-interface/awi-infra-guard/issues).

When creating a new issue, please be sure to include a **title and clear
description**, as much relevant information as possible, and, if possible, a
test case.

**If you discover a security bug, please do not report it through GitHub.
Instead, please see security procedures in [SECURITY.md](SECURITY.md).**

## Pull Request Process

1. Ensure any install or build dependencies are removed before asking to merge
   your code.
2. Update the `README.md` with details of changes to the interface, including
   new environment variables, exposed ports, file locations and container
   parameters.
3. Increase the version numbers in any examples files and the `README.md` to the
   new version that this Pull Request would represent. The versioning scheme we
   use is [SemVer](http://semver.org/). Alternatively
4. You may ask one (or more) of the code owners to review and merge your Pull
   Request.

## Other Ways to Contribute

We welcome anyone that wants to contribute to awi-infra-guard to triage and
reply to open issues to help troubleshoot and fix existing bugs.
Here is what you can do:

- Help ensure that existing issues follows the recommendations from the
  _[Reporting Issues](#reporting-issues)_ section, providing feedback to the
  issue's author on what might be missing.
- Review and update the existing content of our documentation with up-to-date
  instructions and code samples.
- Review existing pull requests, and testing patches against real existing
  applications that use awi-infra-guard.
- Write a test, or add a missing test case to an existing test.
