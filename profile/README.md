# Introduction

In the world of network connectivity management, we're witnessing a transformation, fueled by the rise of cloud computing, the proliferation of CI/CD and GitOps practices, and the massive adoption of container orchestration platforms like Kubernetes. 
Traditionally, core network or security  operations have been the purview of NetOps and SecOps teams, who have specialized in the configuration, maintenance, monitoring, and automation of physical and virtual network and security components.
While we don't see NetOps, or SecOps roles changing much in managing infrastructure, configuration and policy, the shift towards cloud-native applications and microservices based architecture necessitates a shift left outlook for network and security vendors for exposing connectivity and security provisioning workflows.This shift is crucial for enabling automated and efficient network connectivity and access control from the application owner side.

**ANI** (Application Network Interface) will enable application administrators to interact directly with core network components, facilitating automated resource provisioning, configuration, and security enforcement based on application needs. This interface would abstracts the complexity of the certain network operations, allowing CloudOps and Dev(Sec)Ops teams to provision connectivity, access control, and certain connection, observability and security configurations to ensure application performance and security without in-depth networking knowledge. AWI (Application WAN Interface) is a subset of the overall vision of ANI.

**AWI** (Application WAN Interface) can be considered as a subset of ANI. It provides an application centric programmable interface for [SD]WAN controllers. This interface allows DevOps and CloudOps to program enterprise WAN solutions to provision connectivity with “network SLO (Service Level Objectives)” and define workload access policy at layer 4 across networking domains. It is a vendor agnostic interface and has provisions for networking([SD]WAN) vendors to write their controller program logic as a plugin into AWI interface.

The overarching objective is to foster an open, plugin-based ecosystem for networking connectivity and access control. By inviting vendors to contribute their plugins and leverage this open interface, the initiative aims to simplify how application developers bridge network domains and interconnect application components, paving the way for more streamlined and secure network management in the era of cloud operations and DevSecOps.


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
reported or fixed by searching through a repo specific  
[issues list](https://github.com/app-net-interface/awi-infra-guard/issues)

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

# FAQ 


## What problem does **AWI** solve for cloud native users ?  

Below are the  problems we are trying to address:  

### DevOps(developer) Productivity:  

Distributed applications have connectivity needs that span across multiple networking domains such as datacenter, VPCs (public cloud), campus and co-location. Line of Business (LOB) product teams, IT business application teams need to talk to NetOps team to provision connectivity across these sites for their distributed application deployment. These teams express their connectivity requirements to NetOps team via email, slack messages, service tickets or shared documents, adding considerable toil and making the overall process tedious. Most DevOps teams have adopted Agile development process and use CI/CD pipelines to deploy product artifacts. Today, connectivity provisioning is an impediment for their productivity as it slows the deployment process. Sometimes, they prefer taking short-cuts (e.g., Hosting many different LoB apps in a single VPC) to avoid dynamic connectivity provisioning, and thereby compromising on security and operational efficiency. Please see customer conversation section for details  

AWI solves this problem by providing a open and standard connectivity interface for DevOps to provision connectivity across networking domains from within compute infrastructure such as Kubernetes, using tools like Kubectl that DevOps teams are already familiar with.  

### Workload Access Control:  

Once connectivity is provisioned, AWI data models allow Dev (Sec)Ops teams to do workload segmentation across networking domains. Only ABAC (Attribute Based Access Control) and segmentation-based security are supported at this moment. 


### Connectivity with network SLA 

AWI allows development teams to provision connectivity for a specific workload. In the backend networking infrastructure, traffic for a specific workload could be routed through an underlay provider network (such as Megaport/Equinix) and end-to-end network SLA can be maintained.  

## What problem does it solve in the industry?  

Cloud native ecosystem is fragmented with proprietary networking domains, compute clusters, Container Network Interfaces (CNIs) and service meshes. There is no standard way of provisioning connectivity across heterogenous compute clusters. We believe an SDWAN, or cloud networking controller is the glue that can help enterprises connect cloud-native compute clusters.  

A standard based connectivity interface exposed through Cloud Networking / SDWAN connectivity domain would help enterprises adopt the controller software as the connectivity provider across their distributed compute clusters and workloads. 

## Is AWI only for DevOps and the application domain? What about DevOps access and authorization process?  

AWI is being designed for DevOps consumption, so that inter cluster workload connections can be provisioned from within application domain.  

SDWAN/Cloud WAN Controller vendor implementations would need to create mechanisms to create DevOps authorization flow, so that NetOps teams are in complete control of the SDWAN functions and services. This is to ensure that DevOps automation happens in the context of networking and security policy set up by NetOps team. This authorization process is outside of AWI scope. We have created an authorization mechanism for Cisco SDWAN. 

NetOps admins can also use the intent-based interface to provision connectivity should they choose to. Controller , or API Access & Authorization is based on the user credentials that's provisioned within AWI operator or CLI. AWI inherintly does not specify who can or cannot use the API (Application Programmer Interface).

## Why the need for an open system and standardization?  

An open eco-system and standardization would accelerate adoption across the industry, and adoption by networking vendors would put hybrid/multi cloud network controllers in the front and center as the default multi-network domain connectivity infrastructure provider. 

Today’s SDWAN/Cloud Network vendor controllers are proprietary and have proprietary interfaces. Compute infrastructure automation systems like Kubernetes have no integration with vendor controllers for external connectivity because of the need to deal with different proprietary interfaces. AWI would provide a vendor agnostic interface that can be used from within Kubernetes, so that connectivity can be provisioned using Kubectl. This would remove the need for Kubernetes maintainers to integrate with each vendor controller.  
