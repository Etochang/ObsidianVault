202406022033
Meta Tags: #class
Tags: [[software engineering]]

# Process Improvement and Maturity

## Measuring the Maturity of the Software Process

- The existence of a software process is no guarantee that software will be delivered on time, that it will meet the customer's needs, or that it will exhibit the technical characteristic that will lead to long term characteristics.
- Process patterns must be coupled with solid software engineering practice

## Process Improvement

- Many companies have turned to software process improvement as a way of enhancing the quality of their software, reducing costs/accelerating their dev process.
- Process improvement means understanding existing processes and changing them to increase product quality and/or reduce costs/dev time.

## Approaches to Improvement

- The process maturity approach, which focuses on improving process and project management and introducing good software engineering practice
	- The level of process maturity reflects the extent to which good technical and management practice has been adopted in organizational software dev processes.
- The agile approach, which focuses on iterative development and the reduction of overheads in the software process

## The process improvement cycle

![[Pasted image 20240602203759.png]]

## Process Measurement and Matrices

- Wherever possible, quantitative process data should be collected.
	- However, w/o clearly defined process standards this is very difficult because of the lack of knowledge about what to measure
- Process measurements should be used to assess process improvements
	- But this doesn't mean that measurements should drive the improvement. The improvement driver should be the organizational objectives.
- Examples:
	- Time taken for process activities to be completed
	- Resources required for processes/activities
	- Number of occurrences of a particular event

## Capability Maturity Levels (CMMI)

![[Pasted image 20240602204054.png]]

- Application of process management and quality improvement concepts to software dev and maintenance
- A guide for evolving toward a culture of engineering excellence
- A model for organizational improvement
- Underlying structure for reliable and consistent software process assessments and software capability evaluation

# CMMI Levels

![[Pasted image 20240602204227.png]]

## 5 CMM Levels

Each process area is rated according to the following capability levels:
- Level 0: Incomplete
	- The process area (e.g., requirements management) is either not performed or doesn't achieve all goals and objectives defined by the CMMI for level 1 capability
- Level 1: Performed/Initial
	- All of the specific goals of the process area (as defined by the CMMI) have been satisfied
	- Work tasks required to produce defined work products are being conducted
	- **Characteristics:** Chaotic - unpredictable cost, schedule, and quality performance
	- Typical organization doesn't provide stable environment for developing and maintaining software
	- Difficult to make commitments that the staff can meet with an orderly engineering process, resulting in a series of crises
	- Even a strong engineering process cannot overcome the instability created by the absence of sound management practices
	- Success at this level depends on competence and heroics of people in an organization and normally cannot be repeated
	- Capability is a characteristic of individuals, not organizations
	- **Needed Actions:** 
		- Planning (size, cost estimates and schedules)
		- Performance tracking
		- change control
		- Commitment management
		- Quality assurance
- **Note: both L0 and L1 are considered as one level as CMMI awards start from level 2**
- **Level 2: Managed/Repeatable**
	- All L1 criteria have been satisfied
	- In addition, all work associated with the process area conforms to an organizationally define policy
	- All people doing the work have access to adequate resources to get the job done; stakeholders are actively involved in the process area as required
	- All work tasks and products are monitored, controlled and reviewed; and are evaluated for adherence to the process description
	- **Characteristics:** intuitive - cost and quality highly variable, reasonable control of schedules, informal and ad hoc process methods and procedures
	- Policies for managing a software project and procedures to implement those policies are established in this level
	- The planning and management of new projects is based on experience with similar projects
	- Project standards are defined and followed
	- Process capability can be summarized as discipline because project planning and tracking are stable and earlier successes can be repeated
	- **Needed Actions:**
		- Develop process standards and definitions
		- Assign process resources
		- Establish methods (requirements, designs, inspections, and tests)
- **Level 3: Defined**
	- All L2 criteria have been achieved
	- In addition, the process is tailored from the organization's set of standard processes according to the organization's tailoring guidelines, and contributes work products, measures, and other process-improvement information to the organizational process assets.
	- **Characteristics:** Reliable costs and schedules, improving but unpredictable quality performance
	- A typical process for developing and maintaining software across a organization is documented and works as its standard
	- Project teams tailor an organization's standard software process to develop their own defined process, which takes into account project's unique characteristics
	- A defined process contains a coherent, integrated set of well-defined software-engineering and management processes
	- Process capability summarized as standard and consistent due to stable and repeatable software engineering and management activities
	- **Needed Actions:**
		- Process measurements
		- quantitative quality goals
		- plans
		- tracking
- **Level 4: Quantitively Managed**
	- All L3 criteria has been achieved
	- In addition, the process area is controlled and improved using measurement and quantitative assessment. Quantitative objectives for quality and process performance are established and used as criteria in managing the process.
	- **Characteristics:** Reliable statistical control over product quality
	- Organization sets quantitative quality goals for both products and processes. Software processes are instrumented with well-defined and consistent measurements.
	- An organization-wide process database is used to collect and analyze data available from a aproject's defined processes for evaluating a project's processes and products
	- Productivity and quality are measure for important process activities across all projects
	- The process capability can be summarized as being quantifiable and predictable because the process is measured and operates within measurable limits.
	- **Needed Actions:**
		- Quantitative productivity plans and tracking
		- Instrumented process environment
		- Economically justified tech investments
- **Level 5: Optimizing**
	- All L4 criteria have been achieved
	- In addition, the process area is adapted and optimized using quantitative (statistical) means to meet changing customer needs and to continually improve the efficacy of the process area under consideration
	- **Characteristics:** Quantitative basis for continued capital investment in process automations and improvement
	- The entire organization is focused on continuous process improvement
	- Organization has the means to identify weakness and improve the process capability with the goal of preventing defects
	- Data on process effectiveness is used to perform cost-benefit analyses of new tech and propose changes to process
	- Project team analyzes defects to determine their causes, evaluate the process to prevent known types of defects
	- Process capability is continuously improving
	- **Needed Actions:**
		- Continued emphasis on
			- Process measurement
			- Process methods for error prevention

![[Pasted image 20240602210536.png]]




---
# *References*
https://canvas.asu.edu/courses/185762/assignments/5104424?module_item_id=13399325