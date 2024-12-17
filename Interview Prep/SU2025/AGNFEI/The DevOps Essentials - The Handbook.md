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
- 



---
# *References*