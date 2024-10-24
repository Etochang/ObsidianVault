202409110601
Meta Tags: #class
Tags:

# Zero Trust

## Introduction

- enterprise infrastructure has grown increasingly complex, outstripping legacy methods of perimeter-based network security
- perimeter-based network security is insufficient because it **doesn't prevent lateral movement** within the perimeter

This has led to **zero trust**, an approach primarily focused on data/service protection but also poised to include all enterprise assets (devices, infrastructure components, applications, virtual and cloud components) and subjects (end users, applications and other non-human entities that request information from resources).

ZT security models assume that an **attacker is present in the environment** and that an **enterprise-owned environment is no different/more trustworthy than any non-enterprise-owned environment**. As such, an enterprise must assume no implicit trust and continually analyze and evaluate the risks to its assets and business functions, and then enact protections to mitigate these risks. These protections usually involve minimizing access to resources (such as data and compute resources and applications/services) and continually authenticating and authorizing the identity and security posture of each access request.

A ZT architecture is based on ZT principles and is designed to prevent data breaches and limit internal lateral movement.

## Zero Trust Basics

ZT: focused on resource protection and continual evaluation rather than implicit trust

ZTA is an end-to-end approach to enterprise resource and data security that encompasses identity, credentials, access management, operations, endpoints, hosting environments, and the interconnecting infrastructure.

The initial focus should be on **restricting resources to those w/ a need to access** and **grant only the minimum privileges** (e.g., read, write, delete) needed to perform the mission. Traditionally, enterprise networks have focused on perimeter defense and authenticated subjects are given authorized access to a broad collection of resources once on the internal network. 

- *Zero Trust*: designed to minimize uncertainty in enforcing accurate, least privilege per-request access decisions in IT systems/services in the face of a network viewed as compromised
- *ZTA*: an enterprise's cybersecurity plan that utilizes ZT and encompasses component relationships, workflow planning, and access policies
- *ZT Enterprise*: the network infrastructure (physical and virtual) and operational policies that are in place for an enterprise as a product of a ZTA plan

The goal is to **prevent unauthorized access to data and services** as well as **make the access control enforcement as granular as possible**.

- authorized and approved subjects (combination of user, application/service, and device) can access data to the exclusion of all other subjects (i.e. attackers); data can be substituted with the word 'resource' so that ZT and ZTA are also about resource access (e.g., printers, compute resources, IoT actuators)

The main focus is on authentication, authorization, and shrinking implicit trust zones while maintaining availability and minimizing temporal delays in authentication mechanisms. Access rules are made as granular as possible to enforce least privileges needed to perform the action in the request.

![[Pasted image 20241006054648.png]]
 In the abstract model of access above, a subject needs access to an enterprise resource. Access is granted through a policy decision point (PDP) and corresponding policy enforcement point (PEP).

The system must ensure that the subject is authentic and the request is valid. The PDP/PEP passes proper judgment to allow the subject to access the resource. This implies that ZT applies to two basic areas: **authentication and authorization**.

- What is the level of confidence about the subject's identity for this unique request?
- Is access to the resource allowable given the level of confidence in the subject's identity?
- Does the device used for the request have the proper security posture?
- Are there other factors that should be considered and that change the confidence level (e.g., time, location of subject, subject's security posture)?

Overall, enterprises need to develop and maintain dynamic risk-based policies for resource access and set up a system to ensure that these policies are enforced correctly and consistently for individual resource access requests. This means that an enterprise should not rely on implied trustworthiness wherein if the subject has met a base authentication level, all subsequent resource requests are assumed to be equally valid.

>[!info] implicit trust zone
>Represents an area where all the entities are trusted to at least the level of the last PDP/PEP gateway. Consider the passenger screening model in an airport; all passengers pass through security (PDP/PEP) to access the boarding area, which is the implicit trust zone.

The PDP/PEP applies a set of controls so that all traffic beyond the PEP has a common level of trust. The PDP/PEP cannot apply additional policies beyond its location in the flow of traffic. To allow the PDP/PEP to be as specific as possible, the implicit trust zone must be as small as possible. 

ZT provides a set of principles and concepts around moving the PDP/PEPs closer to the resource. The idea is to explicitly authenticate and authorize all subjects, assets and workflows that make up the enterprise.

### Tenets of Zero Trust

Many definitions and discussions of ZT stress the concept of removing wide-area perimeter defenses (e.g., enterprise firewalls) as a factor. However, most of these definitions continue to define themselves in relation to perimeters in some way (such as micro-segmentation or micro-perimeters) as part of the functional capabilities of a ZTA. The following is an attempt to define ZT and ZTA in terms of **basic tenets that should be involved** **rather than what is excluded**. These tenets are the ideal goal, though it must be acknowledged that not all tenets may be fully implemented in their purest form for a given strategy. 

A ZTA is designed and deployed with adherence to the following zero trust basic tenets:

1. **All data sources and computing services are considered resources.** A network may be composed of multiple classes a devices. A network may also have small footprint devices that send data to aggregators/storage, SaaS, systems sending instructions to actuators, and other functions. Also, an enterprise may decide to classify personally owned devices as resources if they can access enterprise-owned resources. 
2. **All communication is secured regardless of network location.** Network location alone doesn't imply trust. Access requests from assets located on enterprise-owned network infrastructure must meet the same security requirements as access requests and communication from any other nonenterprise-owned network. *In other words, trust shouldn't be automatically granted based on the device being on enterprise network infrastructure.* All communication should be done in the most secure manner available, protect confidentiality and integrity, and provide source authentication. 
3. **Access to individual enterprise resources is granted on a per-session basis.** Trust in the requester is evaluated before the access is granted. Access should also be granted with the least privileges needed to complete the task. This could mean only "sometime recently" for this particular transaction and may not occur directly before initiating a session or performing a transaction with a resource. However, authentication and authorization to one resource will not automatically grant access to a different resource.
4. **Access to resources is determined by dynamic policy—including the observable state of client identity, application/service, and the requesting asset—and may include other behavioral and environmental attributes.** An organization protects resources by defining what resources it has, who its members are (or ability to authentication users from a federated community), and what access to resources those members need. For ZT, client identity can include the user account and any associated attributes assigned by the enterprise to the at account or artifacts to authenticate automated tasks. Requesting asset state can include device characteristics such as software versions installed, network location, time/date of request, previously observed behavior, and installed credentials. Behavioral attributes include, but are not limited to, automated subject analytics, device analytics, and measured deviations from observed usage patterns. Policy is the set of access rules based on attributes that an organization assigns to a subject, data asset, or application. Environmental attributes may include such factors as requestor network location, time, reported active attacks, etc. These rules and attributes are based on the needs of the business process and acceptable level of risk. Resource access and action permission policies can vary based on the sensitivity of the resource/data. Least privilege principles are applied to restrict both visibility and accessibility.
5. **The enterprise monitors and measures the integrity and security posture of all owned and associated assets.** No asset is inherently trusted. The enterprise evaluates the security posture of the asset when evaluating a resource request. An enterprise implementing a ZTA should establish a continuous diagnostics and mitigation (CDM) or similar system to monitor the state of devices and applications and should apply patches/fixes as needed. Assets that are discovered to be subverted, have known vulnerabilities, and/or aren't managed by the enterprise may be treated differently (including denial of all connections to enterprise resources) than devices owned by or associated with the enterprise that are deemed to be in their most secure state. This may also apply to associated devices (e.g., personally owned devices) that may be allowed to access some resources but not others. This, too, requires a robust monitoring and reporting system in place to provide actionable data about the current state of enterprise resources.
6. **All resource authentication and authorization are dynamic and strictly enforced before access is allowed.** This is a constant cycle of obtaining access, scanning and assessing threats, adapting, and continually reevaluating trust in ongoing communication. An enterprise implementing a ZTA would be expected to have Identity, Credential, and Access Management (ICAM) and asset management systems in place. This includes the use of MFA for access to some or all enterprise resources. Continual monitoring w/ possible reauthentication and reauthorization occurs throughout user transactions, as defined and enforced by policy (e.g., time-based, new resource requested, resource modification, anomalous subject activity detected) that strives to achieve a balance of security, availability, usability, and cost-efficiency.
7. **The enterprise collects as much info as possible about the current state of assets, network infrastructure and communications and uses it to improve its security posture.** An enterprise should collect data about asset security posture, network traffic and access requests, process that data, and use any insight gained to improved policy creation and enforcement. This data can also be used to provide context for access requests from subjects.

The above tenets attempt to be technology agnostic. For example, "user identification (ID)" could include several factors such as username/password, certificates, and onetime password. These tenets apply to work done within an organization or in collaboration with one or more partner organizations and not to anonymous public or consumer-facing business processes. An organization cannot impose internal policies on external actors (e.g., customers, or general internet users) but may be able to implement some ZT-based policies on nonenterprise users who have a special relationship with the organization (e.g. registered customers, employee dependents, etc.).

### A Zero Trust View of a Network

There are some basic assumptions for network connectivity for any organization that utilizes ZTA in network planning and deployment. Some of these apply to enterprise-owned network infrastructure, and some apply to enterprise-owned resources operating on nonenterprise-owned network infrastructure (e.g., public Wi-Fi or public cloud providers). These assumptions are used to direct the formation of a ZTA. The network in an enterprise implementing a ZTA should be developed with the ZTA tenets outlined above and w/ the following assumptions.

1. **The entire enterprise private network is not considered an implicit trust zone.** Assets should always act as if an attacker is present on the enterprise network, and communication should be done in the most secure manner available. This entails actions such as authenticating all connections and encrypting all traffic.
2. **Devices on the network may not be owned or configurable by the enterprise.** Visitors, contracted services, BYOD policies.
3. **No resource is inherently trusted.** Every asset must have its security posture evaluated via a PEP before a request is granted to an enterprise-owned resource. This evaluation should be continual for as long as the session lasts. Enterprise-owned devices may have artifacts that enable authentication and provide a confidence level higher than the same request coming from nonenterprise-owned devices. Subject credentials alone are insufficient for device authentication to an enterprise resource. 
4. **Not all enterprise resources are on enterprise-owned infrastructure.** Remote enterprise subjects, cloud services.
5. **Remote enterprise subjects and assets cannot fully trust their local network connection.** Remote subjects should assume that the local network is hostile. Assets should assume that all traffic is being monitored and potentially modified. All connection requests should be authenticated and authorized, and all communications should be done in the most secure manner possible (i.e., provide confidentiality, integrity protection, and source authentication). 
6. **Assets and workflows moving between enterprise and nonenterprise infrastructure should have a consistent security policy and posture.** Assets and workload should retain their security posture when moving to or from enterprise-owned infrastructure. This includes devices that move from enterprise networks to nonenterprise networks (i.e. remote users). This also includes workloads migrating from on-premises data centers to nonenterprise cloud instances. 

## Logical Components of ZTA

There are numerous logical components that make up a ZTA deployment in an enterprise. These components may be operated as an on-premises service or through a cloud-based service. 

![[Pasted image 20241006155150.png]]

In the above figure, the PDP is broken down into two logical components: the policy engine and policy administrator. The ZTA logical components use a separate control plane to communicate, while application data is communicated on a data plane.

- **Policy Engine (PE):** This component is responsible for the ultimate decision to grant access to a resource for a given subject. The PE uses enterprise policy as well as input from external sources (e.g., CDM systems, threat intelligence services described below) as input to a trust algorithm to grant, deny, or revoke access to the resource. The PE is paired with the PA component; the PE makes and log the decision (as approved, or denied), and the PA executes the decision.
- **Policy Administrator (PA):** This component is responsible for establishing and/or shutting down the communication path between a subject and a resource (via commands to relevant PEPs). It would generate any session-specific authentication and authentication token or credential used by a client to access an enterprise resource. It is closely tied to the PE and relies on its decision to ultimately allow or deny a session. If the session is authorized and the request authenticated, the PA configures the PEP to allow the session to start. If the session is denied (or a previous approval is countermanded), the PA signals to the PEP to shut down the connection. Some implementations may treat the PE and PA as a single service; here, it is divided into its two logical components. The PA communicates with the PEP when creating the communication path. This communication is done via the control plane.
- **Policy Enforcement Point (PEP):** This system is responsible for enabling, monitoring, and eventually terminating connections between a subject and an enterprise resource. The PEP communicates with the PA to forward requests and/or receive policy updates from the PA. This is a single logical component in ZTA but may be broken into two different components: the client (e.g., agent on a laptop) and resource side (e.g., gateway component in front of resource that controls access) or a single portal component that acts as a gatekeeper for communication paths. Beyond the PEP is the trust zone hosting the enterprise resource.

In addition to the core components in an enterprise implementing a ZTA, several data sources provide input and policy rules used by the policy engine when making access decisions. These include local data sources as well as external (i.e., nonenterprise-controlled or -created) data sources.

- **Continuous Diagnostics and Mitigation (CDM) System:** This gathers information about the enterprise asset's current state and applies updates to configuration and software components. An enterprise CDM system provides the policy engine with the information about the asset making an access request, such as whether it is running the appropriate patched OS, the integrity of enterprise-approved software components or presence of non-approved components and whether the asset has any known vulnerabilities. CDM systems are also responsible for identifying and potentially enforcing a subset of policies on nonenterprise devices active on enterprise infrastructure. 
- **Industry Compliance System:** This ensures that the enterprise remains compliant with any regulatory regime that it may fall under (e.g., FISMA, healthcare or financial industry information security requirements). This includes all the policy rules that an enterprise develops to ensure compliance. 
- **Threat Intelligence Feed(s):** This provides information from internal or external sources that help the PE make access decisions. These could be multiple services that take data from internal and/or multiple external sources and provide info about newly discovered attacks or vulnerabilities. This also includes newly discovered flaws in software, newly identified malware, and reported attacks to other assets that the policy engine will want to deny access to from enterprise assets. 
- **Network and System Activity Logs:** This enterprise system aggregates asset logs, network traffic, resource access actions, and other events that provide real-time (or near-real-time) feedback on the security posture of enterprise information systems.
- **Data Access Policies:** These are the attributes, rules, and policies about access to enterprise resources. This set of rules could be encoded in (via management interface) or dynamically generated by the policy engine. These policies are the starting point for authorizing access to a resource as they provide the basic access privileges for accounts and applications/services in the enterprise. These policies should be based on the defined mission roles and needs of the organization.
- **Enterprise Public Key Infrastructure (PKI):** This system is responsible for generating and logging certificates issued by the enterprise to resources, subjects, services and applications. This also includes the global certificate authority ecosystem and the Federal PKI, which may or may not be integrated with the enterprise PKI. This could also be a PKI that is not built upon X.509 certificates.
- **ID Management System:** This is responsible for creating, storing, and managing enterprise user accounts and identity records (e.g., lightweight directory access protocol (LDAP) server). This system contains the necessary subject information (e.g., name, email address, certificates) and other enterprise characteristics such as role, access attributes, and assigned assets. This system often utilizes other systems (such as a PKI) for artifacts associated w/ user accounts. This system may be part of a larger federated community and may include nonenterprise employees or links to nonenterprise assets for collaboration.
- **Security Information and Event Management (SIEM) System:** This collects security-centric information for later analysis. This data is then used to refine policies and warn of possible attacks against enterprise assets.

### Variations of Zero Trust Architecture Approaches

#### ZTA Using Enhanced Identity Governance

This approach uses the identity of actors as the key component of policy creation. If it were not for subjects requesting access to enterprise resources, there would be no need to create access policies. For this approach, enterprise resource access policies are based on identity and assigned attributes. The primary requirement for resource access is based on the access privileges granted to the given subject. Other factors such as device used, asset status, and environmental factors may alter the final confidence level calculation (and ultimate access authorization) or tailor the result in some way, such as granting only partial access to a given data source based on network location. Individual resources or PEP components protecting the resource must have a way to forward requests to a PE service or authenticate the subject and approve the request before granting access.

These are often employed using an open network model or an enterprise network w/ visitor access or frequent nonenterprise devices on the network. Network access is initially granted to all assets but access to enterprise resources are restricted to identities with the appropriate access privileges. There is a downside in granting basic network connectivity as malicious actors could still attempt network reconnaissance and/or use the network to launch DoS attacks either internally or against a third party. Enterprises still need to monitor and respond to such behavior before it impacts workflows.

The identity-driven approach works well with the resource portal model since device identity and status provide secondary support data to access decisions. Other models work as well, depending on policies in place. Identity-driven approaches also work well for enterprises that use cloud-based applications/services that may not allow for enterprise-owned or -operated ZT security components to be used (such as many SaaS offerings). the enterprise can use the identity of requestors to form and enforce policy on these platforms.

#### ZTA Using Micro-Segmentation

An enterprise may choose to implement a ZTA based on placing individual or groups of resources on a unique network segment protected by a gateway security component. In this approach, the enterprise places infrastructure devices such as intelligent switches (or routers) or next generation firewalls (NGFWs) or special purpose gateway devices to act as PEPs protecting each resource or small group of related resources. Alternatively (or additionally), the enterprise may choose to implement host-based micro-segmentation using software agents or firewalls on the endpoint asset(s). These gateway devices dynamically grant access to individual requests from a client, asset or service. Depending on the model, the gateway may be the sole PEP component or part of a multipart PEP consisting of the gateway and client-side agent.

This approach applies to a variety of use cases and deployment models as the protecting device acts as the PEP, with management of said devices acting as the PE/PA component. This approach requires an identity governance program (IGP) to fully function but relies on the gateway components to act as the PEP that shield resources from unauthorized access and/or discovery.

The key necessity to this approach is that the PEP components are managed and should be able to react and reconfigure as needed to respond to threats or change in the workflow. It is possible to implement some features of a micro-segmented enterprise by using less advanced gateway devices and even stateless firewalls, but the administration cost and difficulty to quickly adapt to changes make this a very poor choice. 

#### ZTA Using Network Infrastructure and Software Defined Parameters

The last approach uses the network infrastructure to implement a ZTA. The ZTA implementation could be achieved by using an overlay network. These approaches are sometimes referred to as software defined perimeter (SDP) approaches and frequently include concepts from Software Defined Networks (SDN) and intent-based networking (IBN). In this approach, the PA acts as the network controller that sets up and reconfigures the network based on the decisions made by the PE. The clients continue to request access via PEPs, which are managed by the PA component.

When the approach is implemented at the application network layer, the most common deployment model is the agent/gateway. In this implementation, the agent and resource gateway (acting as the single PEP and configured by the PA) establish a secure channel used for communication between the client and resource. There may be other variations of this model, as well for cloud virtual networks, non-IP based networks, etc.

### Deployed Variations of the Abstract Architecture

All of the above components are **logical components**. They do not necessarily need to be unique systems. A single asset may perform the duties of multiple logical components, and likewise, a logical component may consist of multiple hardware or software elements to perform the tasks. For example, an enterprise-managed PKI may consist of one component responsible for issuing certificates for devices and another used for issuing certificates to end users, but both use intermediate certificates issued from the same enterprise root certificate authority. In some ZT product offerings currently available on the market, the PE and PA components are combined in a single service.

#### Device Agent/Gateway-Based Deployment

In this deployment model, the PEP is divided into two components that reside on the resource or as a component directly in front of a resource. For example, each enterprise-issued asset has an installed device agent that coordinates connections, and each resource has a component (i.e., gateway) that is placed directly in front so that the resource communicates only with the gateway, essentially serving as a proxy for the resource. The agent is a software component that directs some (or all) traffic to the appropriate PEP in order for requests to be evaluated. The gateway is responsible for communicating with the PA and allowing only approved communication paths configured by the PA. 

![[Pasted image 20241007141846.png]]

In a typical scenario, a subject with an enterprise-issued laptop wishes to connect to an enterprise resource (e.g., human resources application/database). The access request is taken by the local agent, and the request is forwarded to the PA. The PA and PE could be an enterprise local asset or cloud-hosted service. The PA forwards the request to the PE for evaluation. If the request is authorized, the PA configures a communication channel between the agent and the relevant gateway via the control plane. This may include info such as an IP address, port information, session key, or similar security artifacts. The agent and gateway then connect, and encrypted application/service data flows begin. The connection between the device agent and resource gateway is terminated when the workflow is completed or when triggered by the PA due to a security event (e.g., session time-out, failure to reauthenticate).

This model is best utilized for enterprises that have a robust device management program in place as well as discrete resources that can communicate with the gateway. For enterprises that heavily utilize cloud services, this is a client-server implementation of the Cloud Security Alliance (CSA) Software Defined Perimeter (SDP). This model is also appropriate for enterprises that do not want a BYOD policy in place. Access is possible only via the device agent, which can be placed on enterprise-owned assets.

#### Enclave-Based Deployment

This deployment model is a variation of the device agent/gateway model above. In this model, the gateway components may not reside on assets or in front of individual resources but instead reside at the boundary of a resource enclave (e.g., on-location data center). Usually, these resources serve a single business function or may not be able to communicate directly to a gateway (e.g., legacy database system that doesn't have an API that can be used to communicate with a gateway). This deployment model may also be useful for enterprises that use cloud-based micro-services for a single business process (e.g., user notification, database lookup, salary disbursement). In this model, the entire private cloud is located behind a gateway.

![[Pasted image 20241007142630.png]]

It is possible for this model to be a hybrid with the device agent/gateway model. In this model, enterprise assets have a device agent that is used to connect to enclave gateways, but these connections are created using the same process as the basic device agent/gateway model. 

This model is useful for enterprises that have legacy applications or on-premises data centers that cannot have individual gateways in place. The enterprise needs a robust asset and configuration management program in place to install/configure the device agents. The downside is that the gateway protects a collection of resources and may not be able to protect each resource individually. This may also allow for subjects to see resources which they don't have privileges to access. 

#### Resource Portal-Based Deployment

In this deployment model, the PEP is a single component that acts as a gateway for subject requests. The gateway portal can be for an individual resource or a secure enclave for a collection of resources used for a single business function. One example would be a gateway portal into a private cloud or data center containing legacy applications.

![[Pasted image 20241007143009.png]]

The primary benefit of this model over the others is that a software component doesn't need to be installed on all client devices. This model is also more flexible for BYOD policies and inter-organizational collaboration projects. Enterprise administrators don't need to ensure that each device has the appropriate device agent before use. However, limited information can be inferred from devices requesting access. This model can only scan and analyze assets and devices once the connect to the PEP portal and may not be able to continuously monitor them for malware, unpatched vulnerabilities, and appropriate configuration.

The main difference w/ this model is there is no local agent that handles requests, and so the enterprise may not have full visibility or arbitrary control over assets as it can only see/scan them when they connect to a portal. The enterprise may be able to employ measures such as browser isolation to mitigate or compensate. These assets may be invisible to the enterprise between these sessions. This model also allows attackers to discover and attempt to access the portal or attempt a DoS attack against the portal. The portal systems. should be well-provisioned to provide availability against a DoS attack or network disruption.

#### Device Application Sandboxing

Another variation of the agent/gateway model is having vetted apps/processes run compartmentalized on assets. These compartments could be virtual machines, containers, or some other implementation, but the goal is the same: to protect the application or instances of applications from a possibly compromised host or other applications running on the asset.

![[Pasted image 20241007143535.png]]

The subject device runs approved, vetted apps in a sandbox. The apps can communicate with the PEP to request access to resources, but the PEP will refuse requests from other apps on the asset. The PEP could be an enterprise local service or a cloud service in this model. 

The main advantage of this model is that individual apps are segmented from the rest of the asset. If the asset cannot be scanned for vulnerabilities, these individual, sandboxed apps may be protected from a potential malware infection on the host asset. One of the disadvantages of this model is that enterprises must maintain these sandboxed apps for all assets and may not have full visibility into client assets. The enterprise also needs to make sure each sandboxed app is secure, which may require more effort than simply monitoring devices.

### Trust Algorithm

For an enterprise with a ZTA deployment, the PE can be thought of as the brain and the PE's trust algorithm as its primary thought process. The trust algorithm (TA) is the process used by the PE to ultimately grant or deny access to a resource. The PE takes input from multiple sources: the policy database w/ observable info about subjects, subject attributes and roles, historical subject behavior patterns, threat intelligence sources, and other metadata sources.

![[Pasted image 20241007143957.png]]

- **Access Request:** the actual request from the subject. The resource requested is the primary information used, but info about the requester is also used (OS version, software used, patch level, etc.). Depending on these factors and the asset security posture, access to assets might be restricted or denied.
- **Subject Database:** This is the "who" that is requesting access to a resource. This is the set of subjects (human and processes) of the enterprise or collaborators and a collection of subject attributes/privileges assigned. These subjects and attributes form the basis of policies for resource access. User identities can include a mix of logical identity (e.g., account ID) and results of authentication checks performed by PEPs. Attributes that can be factored into deriving the confidence level include time and geolocation. A collection of privileges given to multiple subjects could be though of as a role, but privileges should be assigned to a subject on an individual basis and not simply because they may fit into a particular role in the organization. This collection should be encoded and stored in an ID management system and policy database. This may also include data about past observed subject behavior is some (TA) variants.
- **Asset Database (and Observable Status):** This is the database that contains the known status of each enterprise-owned (and possibly known nonenterprise/BYOD) asset (physical and virtual). This is compared to the observable status of the asset making the request and can include OS version, software present, and its integrity, location (network and geo), and patch level. depending on the asset state compared with this database, access to assets might be restricted or denied.
- **Resource Requirements:** This set of policies complements the user ID and attributes database and defines the minimal requirements for access to the resource. Requirements may include authenticator assurance levels, such as MFA network location (e.g., deny access from overseas IP addresses), data sensitivity, and requests for asset configuration. These requirements should be developed by both the data custodian (i.e., those responsible for the data) and those responsible for the business processes that utilize the data (i.e., those responsible for the mission).
- **Threat Intelligence:** This is an info feed or feeds about general threats and active malware operating on the internet. This could also include specific info about communication seen from the device that may be suspect (such as queries for possible malware command and control nodes). these feeds can be external services or internal scans and discoveries and can include attack signatures and mitigations. this is the only component that will most likely be under the control of a service rather than the enterprise.

The final determination is passed to the PA for execution. The PA's job is to configure the necessary PEPs to enable authorized communication. Depending on how the ZTA is deployed, this may involve sending authentication results and connection configuration information to gateways and agents or resource portals. PAs may also place a hold or pause on a communication session to reauthenticate and reauthorize the connection in accordance with policy requirements. The PA is also responsible for issuing the command to terminate the connection based on policy (e.g., after a time-out, when the workflow has been completed, due to a security alert).

#### Trust Algorithm Variations

How are factors evaluated (binary decisions or weighted parts of a whole "score" or confidence level)?
How are requests evaluated in relation to other requests by the same subject, app/service, or device?

- **Criteria- vs. Score-based:** the former TA assumes a set of qualified attributes that must be met before access is granted to a resource or an action (e.g., read/write) is allowed. These criteria are configured by the enterprise and should be independently configured for every resource. Access is granted or an action applied to a resource only if all the criteria are met. The latter TA computes a confidence level based on values for every data source and enterprise-configured weights. If the score is greater than the configured threshold for the resource, access is granted, or the action is performed. Otherwise, the request is denied, or access privileges are reduced (e.g., read access is granted but not write access for a file).
- **Singular vs. Contextual:** A singular TA treats each request individually and doesn't take the subject history into consideration when making its evaluation. This can allow faster evaluations, but there is a risk that an attack can go undetected if it stays within a subject's allowed role. A contextual TA takes the subject or network agent's recent history into consideration when evaluating access requests. This means the PE must maintain some state info on all subjects and apps but may be more likely to detect an attacker using subverted credentials to access information in a pattern that is atypical of what the PE sees for the given subject. This also means that the PE must be informed of user behavior by the PA (and PEPs) that subjects interact w/ when communicating. Analysis of subject behavior can be used to provide a model of acceptable use, and deviations from this behavior could trigger additional authentication checks or resource request denials. 

The two factors are not always dependent on each other. It is possible to have a TA that assigns a confidence level to every subject/device and still considers every access request independently (i.e., singular). However, contextual, score-based TAs would provide the ability to offer more dynamic and granular access control, since the score provides a current confidence level for the requesting account and adapts to changing factors more quickly than static policies modified by human administrators.

Ideally, a ZTA TA should be contextual, but this may not always be possible with the infrastructure components available to the enterprise. A contextual TA can mitigate threats where an attacker stays close to a "normal" set of access requests for a compromised subject account or insider attack. It is important to balance security, usability, and cost-effectiveness when defining and implementing trust algorithms. Continually prompting a subject for reauthentication against behavior that is consistent w/ historical trends and norms for their mission function and role within the organization can lead to usability issues. For example, if an employee's access requests exceed their normal amount or if someone is making requests after normal business hours, a contextual TA may send an alert.

Developing a set of criteria or weights/threshold values for each resource requires planning and testing. Enterprise administrators may encounter issues during the initial implementation of ZTA where access requests that should be approved are denied due to misconfiguration. this will result in an initial "tuning" phase of deployment. Criteria or scoring weights may need to be adjusted to ensure that the policies are enforced while still allowing the enterprise's business processes to function. How long this tuning phase lasts depends on the enterprise-defined metrics for progress and tolerance for incorrect access denials/approvals for the resources used in the workflow.

### Network/Environment Components

In a ZT environment, there should be a separation (logical or possibly physical) of the communication flows used to control/configure the network and app/service communication flows used to perform the actual work of the organization. This is often broken down to a *control plane* for network control communication and a *data plane* for app/service communication flows.

The control plane is used by various infrastructure components (both enterprise-owned and from service providers) to maintain and configure assets; judge, grant, or deny access to resources; and perform any necessary operations to set up communication paths between resources. The data plane is used for actual communication between software components. This communication channel may not be possible before the path has been established via the control plane. For example, the control plane could be used by the PA and PEP to set up the communication path between the subject and the enterprise resource. The application/service workload would then use the data plane path that was established.

#### Network Requirements to Support ZTA

1. **Enterprise assets have basic network connectivity.** The LAN, enterprise controlled or not, provides basic routing and infrastructure (e.g., DNS). The remote enterprise asset may not necessarily use all infrastructure services.
2. **The enterprise must be able to distinguish between what assets are owned or managed by the enterprise and the devices' current security posture.** This is determined by enterprise-issued credentials and not using information that cannot be authenticated information (e.g., network MAC addresses that can be spoofed). 
3. **The enterprise can observe all network traffic.** The enterprise records packets seen on the data plane, even if it is not able to perform application layer inspection (i.e., OSI layer 7) on all packets. The enterprise filters out metadata about the connection (e.g., destination, time, device identity) to dynamically update policies and inform the PE as it evaluates access requests.
4. **Enterprise resources should not be reachable without accessing a PEP.** Enterprise resources don't accept arbitrary incoming connections from the internet. Resources accept custom-configured connections only after a client has been authenticated and authorized. These communication paths are set up by the PEP. Resources may not even be discoverable without accessing a PEP. This prevents attackers from identifying targets via scanning and/or launching DoS attacks against resources located behind PEPs. Note that not all resources should be hidden this way; some network infrastructure components (e.g., DNS servers) must be accessible. 
5. **The data plane and control plane are logically separate.** The PE, PA, and PEPs communicate on a network that is logically separate and not directly accessible by enterprise assets and resources. The data plane is used for app/service data traffic. The PE, PA, and PEPs use the control plane to communicate and manage communication paths between assets. The PEPs must be able to send and receive messages from both the data and control planes.
6. **Enterprise assets can reach the PEP component.** Enterprise subjects must be able to access the PEP component to gain access to resources. This could take the form of a web portal, network device, or software agent on the enterprise asset that enables the connection. 
7. **The PEP is the only component that accesses the PA as part of a business flow.** Each PEP operating on the enterprise network has a connection to the PA to establish communication paths from clients to resources. All enterprise business process traffic passes through one or more PEPs. 
8. **Remote enterprise assets should be able to access enterprise resources without needing to traverse enterprise network infrastructure first.** For example, a remote subject shouldn't be required to use a link back to the enterprise network (i.e., VPN) to access services utilized by the enterprise and hosted by a public cloud provider (e.g., email).
9. **The infrastructure used to support the ZTA access decision process should be made scalable to account for changes in process load.** The PE(s), PA(s), and PEPs used in a ZTA become the key components in any business process. Delay or inability to reach a PEP (or inability of the PEPs to reach the PA/PE) negatively impacts the ability to perform the workflow. an enterprise implementing a ZTA needs to provision the components for the expected workload or be able to rapidly scale the infrastructure to handle increased usage when needed.
10. **Enterprise assets may not be able to reach certain PEPs due to policy or observable factors.** For example, there may be a policy stating that mobile assets may not be able to reach certain resources if the requesting asset is located outside of the enterprise's home country. These factors could be based on location (geo or network), device type, or other criteria.

## Threats Associated with ZTA

### Subversion of ZTA Decision Process

The PE and PA are the key components of the entire enterprise. These components must be properly configured and maintained; any enterprise admin with configuration access to the PE's rules may be able to perform unapproved changes or make mistakes that can disrupt enterprise operations. Likewise, a compromised PA could allow access to resources that would otherwise not be approved (e.g., to a subverted, personally-owned device). Mitigating associated risks means the PE and PA components must be properly configured and monitored, and any configuration changes must be logged and subject to audit.

### DoS or Network Disruption

The PA is the key component for resource access. If an attacker disrupts or denies access to the PEP(s) or PE/PA (i.e., DoS attack or route hijack), it can adversely impact enterprise operations. Enterprises can mitigate this threat by having the policy enforcement reside in a properly secured cloud environment or be replicated in several locations following guidance on cyber resiliency.

Botnets produce massive DoS attacks, and it is possible that an attacker could intercept and block traffic to a PEP or PA from a portion or all of the user accounts within an enterprise. 

A hosting provider may also accidentally take a cloud-based PE or PA offline. 

Enterprise resources may not be reachable from the PA, so even if access is granted to a subject, the PA cannot configure the communication path from the network. This could happen due to a DDoS attack or simply due to unexpected heavy usage. 

### Stolen Credentials/Insider Threat

The ZT principle of no implicit trust based on network location means attackers need to compromise an existing account or device to gain a foothold in an enterprise. A properly developed and implemented ZTA should prevent a compromised account or asset from accessing resources outside its normal purview or access patterns. This means that accounts with access policies around resources that an attacker is interested in would be the primary targets for attackers.

Attackers may use phishing, social engineering, or a combination of attacks to obtain credentials of valuable accounts. Implementation of MFA for access requests may reduce the risk of information loss from a compromised account. However, an attacker with valid credentials (or a malicious insider) may still be able to access resources for which the account has been granted access. 

ZTA reduces risk and prevents any compromised accounts/assets from moving laterally throughout the network. If the compromised credentials are not authorized to access a particular resource, they will continue to be denied access to that resource. In addition, a contextual TA is more likely to detect and respond quickly to this attack, as it can detect access patterns that are out of normal behavior and deny the compromised account/insider threat access to sensitive resources.

### Visibility on the Network

Some (possibly the majority) of the traffic on the enterprise network may be opaque to layer 3 network analysis tools. The enterprise that cannot perform deep packet inspection or examine the encrypted traffic must use other methods to assess a possible attacker on the network. 

The enterprise can collect metadata (e.g., source and destination addresses, etc.) about the encrypted traffic and use that to detect an active attacker or possible malware communicating on the network. 

### Storage of System and Network Information

The analysis component itself is a threat itself. It stores monitor scans, network traffic, and metadata for building contextual policies, forensics, or later analysis. 

Another source of reconnaissance info for an attacker is the management tool used to encode access policies. 


---
# *References*
https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207.pdf