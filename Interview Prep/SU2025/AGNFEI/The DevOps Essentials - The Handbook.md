202412161636
Meta Tags: #tutorial 
Tags: [[DevOps]] [[CI/CD]]

# The DevOps Essentials - The Handbook

## What is DevOps

- A software engineering culture that unifies development (Dev) and IT operations (Ops) teams
- Goal is shorter development cycles
- DevOps is **not**:
	- a set of tools, it is a culture, movement, and philosophy
		- Not Jenkins, Docker, Ansible, Kubernetes, DevOps is the cause
	- a standard
	- a product
	- 
- By practitioners, for practitioners

## Dev and Ops Teams - Their Targets

Traditional:
- Dev-Team
	- Deliver features quickly
	- Goal is speed
- Ops-Team
	- Maintain stability
- in opposition to each other

DevOps:
- One Team
	- Deliver features quickly
	- Maintain stability
	- Goal is speed
	- Shared Goals = Shared Accountability
		- Time to Market: time to develop and deploy to customers
		- Minimizing Production failures
		- Immediate Recovery from failures

## History

- DevOps spawned from Agile
	- Small frequent cycles of development vs. Waterfall's long planning phases

## What Happened in Silos

Traditional:
- Silos
	- Separated teams that have walls inbetween them
	- Dev, QA, Ops
	- Dev Code → QA
		- responsibility gone until code returns
	- QA → Ops
		- responsibility gone until code goes back to Dev
	- No cross-team visibility: "black box"
	- lengthy deployment

 DevOps:
- Dev Code → Automated Builds, Integration, Testing, Deployment
- Test while new features are being developed
- Automated Monitoring detects issues, rollback deployments

## Build Automation

- Automation of preparing code for deployment to a live environment
- Deployment → Build Automation → Production
	- Compilation
	- Transformation
	- Unit Tests
	- Scanning for Problems
	- Reporting Problems
	- Eliminating Defects
- Jenkins, Maven, Gradle, Travis CI, etc.
- Independent of IDE
- Machine agnostic
- Portable
- Consistent
- Efficient
## Continuous Integration

- Faster at finding bugs
- All changes are integrated
- Happier developers

- Frequently merge code changes
- Frequently release
- Encourages good coding practices
	- more modular, clear code

## Continuous Deployment

- Code → Source Control Manager → Build
- Build → QA → Stage → Production
- Every change that is passing through all the stages of production is released to customers.
- Excellent way to accelerate the feedback loop with customers to take pressure off the team
- Frequently deploying small code changes to production

## Continuous Delivery
- Code is always in a state to be deployed, becomes business decision rather than technical

## Infrastructure as Code

- IaC - managing and provisioning infrastructure using code
	- servers, instances, environments, containers, clusters
- With IaC, you can build complex infrastructures repeatedly
- Work with automation tools, configuration files, etc.
- Self Documenting
- Scalability of code
- Provision new resources / modify existing resources using code
- Replicate environments to Test, QA, and Prod

## Configuration Management

- Doing infrastructure changes in a maintainable way
- Minimizing configuration drift
	- accumulation of all the small changes that are made to a system over a period of time
	- Baseline of infrastructure components
- Maintaining and changing the state of various pieces of infrastructure in a consistent way
- Controlling the configuration/deployment
	- closely related with IaC
- managing configuration of all servers as a state encapsulated in code on a particular server
- identify the state of infrastructure

## Monitoring in DevOps

- Supports frequent deployments and quick response to problems
- Collect system metrics
- represent data in a presentable manner
- real time monitoring and notifications
- assists in troubleshooting
- collects lots of data during outage
- automated response
- visibility into production systems

## Microservices

- Software architecture: small but loosely coupled services
	- as opposed to monolithic designs with one large executable
- Interact using stable, standardized APIs
- Modular
	- individual pieces can become tightly coupled over time
- Flexible
	- separate pieces
- doesn't need to be build using the same programming language and technology
- optimized stability
	- scale separate pieces rather than one giant executable
- not always the best, for simple applications monolithic can be better
- for complex applications it is good

## Tools for Build Automation and CI

- Build automation: automated process of building code for deployment, depends on programming languages and frameworks
	- Maven, Gradle
- Continuous integration: continuously merging code into a single branch
- Jenkins: Java Servlet Web App
- Travis CI: GitHub Integration

## Tools for Configuration Management

- automated management and changing of infrastructure
- support IaC
- Ansible: declarative configuration, describe state rather than steps to get state. Uses YAML, doesn't require centralized server
	- Doesn't require agents (pieces of software to be installed on each machine)
- Puppet: declarative configuration, manage state through user interface
	- custom modules using puppet domain specific language
	- Uses control server agent architecture
- Chef: procedural configuration, scripts to get machine into state
	- Agent Server Model, Chef DSL
- Salt: Declarative, agentless, event-driven automation, uses YAML

## Tools for Virtualization and Containerization

- Virtualization - managing resources by creating virtual layer on top of physical hardware
	- hypervisor: program that runs on bare physical metal, allows management of virtual machines: VMware, Hyper-V, ESXI, etc.
- Containerization - next step beyond virtualization, lightweight, contain bare minimum required to run application. 
	- Docker
	- portable
- Orchestration - uses containers

## Tools for Monitoring

- Infrastructure Monitoring: data related to health of infrastructure (CPU usage, memory usage, networking statistics)
	- Sensu: client-server architeture, modern and sophisticated, scalable
	- New Relic: SaaS, supports wide variety of metrics
- Application Performance Monitoring: data related to performance and stability of apps on infrastructure (response time)
	- Appdynamics, data points about applications and centralized dashboard, code-level diagnostics
- Aggregation and analytics: what to do with the data after collecting it
	- Elastic Stack: quickly aggregate, detect, and diagnose problems

## Tools for Orchestration

- Orchestration: automation that supports processes and workflows - provisioning of resources
	- autoscale applications based on usage
	- create self healing systems
	- Docker Swarm
	- Kubernetes: gold standard
		- able to manage containerized apps
		- able to utilize pool of resources
	- ZooKeeper

---
# *References*