# Link
---
https://learn.microsoft.com/en-us/training/modules/cloud-adoption-framework/

1 hr, 47 minutes

# Overview
---
The Cloud Adoption Framework includes eight methodologies:

* Strategy
* Plan
* Ready
* Migrate
* Innovate
* Govern
* Manage
* Secure

# Strategy
---
The Strategy methodology helps organizations define their business justification for cloud adoption and align their cloud adoption strategy with their business goals. This includes identifying the desired outcomes of cloud adoption, assessing the current state of the organization, and defining the business case for cloud adoption.

## Assess your strategy
---
The first step in the Strategy methodology is to assess your current strategy. This includes identifying the business drivers for cloud adoption, assessing the current state of the organization, and defining the desired outcomes of cloud adoption.

You can use the Cloud Adoption Framework's Strategy Assessment tool to help you assess your current strategy and identify areas for improvement.

https://learn.microsoft.com/en-us/assessments/8fefc6d5-97ac-42b3-8e97-d82701e55bab/

Determine your motivation, mission and objectives for cloud adoption.
- Motivation: Why are you adopting cloud technologies? (e.g., cost savings, agility, innovation)
- Mission: What is your organization's mission and how does cloud adoption support it?
- Objectives: What specific objectives do you want to achieve through cloud adoption? (e.g., improve customer experience, increase operational efficiency)

Define specific Key Performance Indicators (KPIs) to measure the success of your cloud adoption strategy.

Assign accountability for each key result and review progress regularly to ensure alignment with business goals.

Define Your Team:
- Cloud Strategy Team: Responsible for defining and executing the cloud adoption strategy.
- Cloud Center of Excellence (CCoE): A cross-functional team that provides governance, best practices, and support for cloud adoption across the organization.
- Executive Sponsors: Senior leaders who provide support and resources for cloud adoption initiatives.

Continually seek input from other areas such as HR or marketing outside of the normal IT stakeholders.

Prepare your organization:
You need to ensure your leadership collectively supports the strategies you plan to implement and your vision.

Assess your organization's current capabilities across people, process, technology and partners. 

Understand your project delivery model vs a product delivery model.
- Project: 
- Product:
Shift from task driven projects and towards outcome driven products.

Inform your strategy: 
After you complete the first 4 steps, you can use the insights you gathered to inform your cloud adoption strategy.
- Financial efficency
- AI
- Resiliency
- Security
- Sustainability

# Plan
---
So to review, Strategy, Plan...
The Plan methodology helps organizations create a detailed plan for cloud adoption. This includes identifying the workloads to be migrated, defining the migration approach, and creating a roadmap for cloud adoption.

Prepare your organization for cloud adoption by defining the necessary skills, processes, and tools.

- Map your cloud adoption journey based on your organization type. Startups are different than enterprises. They might use cloud native solutions, while enterprises might have a hybrid approach involving on-premises and cloud resources and a migration strategy.
- Choose the management model that fits your organization. Centralized, decentralized, or federated. My organization will use decentralized for sure.
- Plan cloud responsibilities across governance, security and management functions. Establish governance teams to assess risks, embed security, develop AI strategy and build appropriate teams for AI adoption.
- Document Cloud Responsibilities with clear ownership. Define Partner roles and communicate to all stakeholders.

Prepare your people for the cloud.
- Assess required skills for Cloud Adoption
- Teams need governance, security, and management skills.
- Identify skill gaps and create a training plan.
- Leverage Microsoft Learn, certifications, and hands-on labs.
- Establish a Cloud Center of Excellence (CCoE) to provide guidance, best practices, and support for cloud adoption.
- Sandbox environments for experimentation and learning.
- Encourage a culture of continuous learning and improvement.

Discover existing workload inventory.
- Systemic documentation of existing workloads.
- Prioritize workloads based on business impact, complexity, and dependencies.
- Identify migration candidates and plan migration waves.

Select Migration Strategies:
- Identify business drivers to establish migration priorities.
- Choose migration strategies: Rehost, Refactor, Rearchitect, Rebuild, Replace. More on this later :)
- Create a migration roadmap with timelines, milestones, and resource requirements.
- Apply strategy specific criteria to validate decisions. Compare your chosen strategies against workload stabiity, Azure Compatibility, tech debt levels, architectural limitations and operational requirements.
- Make timing decisions based on resource availability - take into consideration the entire teams and their workload - KTLO vs build build build.
- Communicate with stakeholders - define success metrics, document decisions, coordinate with cloud strategy teams and review strategies as your org evolves. 

Assess your workloads for migration
- Learn your workload architecture to understand dependencies. Assessment tools sucn as Azure Migrate can help.
- Assess application code and data dependencies.
- Assess database data architecture and migration requirements.
- Create a risk register to track and mitigate potential migration risks.
- Identify potential risks such as data loss, downtime, security vulnerabilities, and compliance issues.
- Develop mitigation strategies for each identified risk.
- Continuously monitor and update the risk register throughout the migration process.
-  Engage stakeholders to ensure alignment and support for the migration plan.

Estimate Total Cost of Ownership (TCO)
- Use the Azure TCO Calculator to estimate costs.
- Plan architecture based on business and technical requirements by documenting constraints and compliance needs. Plan Landing zone architecture.
- Estimate costs based on that planned architecture. Estimate operational costs including training, support, and maintenance.
Read through this: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/plan/prepare-organization-for-cloud

# Ready
---
Strategy, Plan, Ready...
The Ready methodology helps organizations prepare their cloud environment for adoption. This includes setting up the necessary infrastructure, configuring security and governance policies, and establishing operational processes.
- Set up your Azure Environment
- Define your cloud operating model
- Implement Landing Zones
- Consider Operational aspects
- Develop necessary skills. 

Use the Azure Setup Guide: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-setup-guide/

## Define a cloud operating model
---
Define your cloud operating model to align with your organization's structure and culture. Use change management, operations management, governance and compliance and security.

Shift your focus from hardware to digital assets and worikloads.

Read the comparison of operating models. https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/operating-model/compare

Implement Landing Zones
- Landing zones are pre-configured environments that provide a foundation for cloud adoption. They include networking, security, governance, and management components.
- After implementation, optimize your landing zones as you scale your cloud adoption.

Continuous Optimization includes:
- Identify and eliminate unnecessary expenses
- Enhance the performance of applications and services
- Improve security and compliance posture and vulnerability management
- Ensure scalability of your landing zone architecture
- Maintain compliance with industry standards and regulations
- Create reliable and resilient systems.

Develop necessary skills
- Provide training and resources to develop the skills needed for cloud adoption.
- Encourage continuous learning and improvement.
- Leverage Microsoft Learn, certifications, and hands-on labs.

Warning! Avoid antipatterns:
- Overcomplicating landing zones with unnecessary components.
- Inadequate preparation
- lack of knowledge about cloud provider operations. 
- Neglecting security and compliance requirements.

# Migrate
---
Plan, Strategy, Ready, Migrate...
The Migrate methodology helps organizations move their workloads to the cloud. This includes executing the migration plan, validating the migration, and optimizing the migrated workloads.
- Execute your migration plan
- Validate your migration
- Optimize migrated workloads

Tips:
1. Assess migration readiness and skills.
2. Choose the right migration path. Expressroute, Data Box for offline data transfer, Azure Migrate for assessment and migration.
3. Determine the migrations sequence. Prioritize based on business impact, complexity, and dependencies.
4. Choose the migration method for each workload. Near-zero downtime, offline migration, phased migration.
5. Define a rollback plan in case of issues during migration.
6. Engage stakeholders on the migration and communicate progress regularly.

Prepare workloads for the cloud:
1. Fix compatibility issues. Deploy in test subscriptions, migrate hardcoded configurations to Azure Key Vault, refactor applications to use cloud-native services.
2. Validate workload functionality. Test performance, security, and compliance. Networking and auth flows are also key here. Use Azure Load Testing for performance testing.
3. Create reusable infrasttructure as code (IaC) templates using ARM, Bicep, or Terraform.
4. Create deployment documentation for future reference.
5. Train operations teams on managing workloads in the cloud.

Execute Migrations:
1. Prepare stakeholds for migrations
2. Implement a change freeze
3. Finalize the production environment
4. Cutover.
5. Maintain rollback and fale back
6. Validate migration success
7. Support the workload during rightsizing and optimization
8. Conduct a post-migration review to identify lessons learned and areas for improvement.
9. Document.

Optimize workloads after migration:
1. Finetune workload configurations. Apply Azure Advisor recommendations, cost, security, performance.
2. Validate critical configurations. Test backups and HA
3. Collect and analyze user feedback. Document issues and improvements.
4. Schedule regular workload reviews to ensure continued optimization and alignment with business goals.
5. Optimize hybrid and multicloud dependencies. Azure Arc and Azure PaaS replacement opportunities.
6. Share migration outcomes. Track cost savings, measure performance improvements, and present these outcomes to stakeholders.

Decommission source workloads:
1. Document stakeholder approval for decommissioning. CYA. :)
2. Reclaim and optimize software licenses.
3. Preserve data for compliance and recovery needs. Don't delete data too soon!
4. Update documentation to reflect the new cloud environment.
Read this: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/migrate/plan-migration

# Innovate - Modernize
---
1. Define modernization strategy for your organization. Establish a common definition of modernization and align it with business goals and communicate to everyone. 
2. Assess modernization readiness and skills. Identify skill gaps and create a training plan that involves certification
3. Prioritize workloads for modernization. Use business impact, complexity, and dependencies as criteria.
4. Understand HOW to modernize. Use the Well Architected Framework to guide your modernization efforts. Consider cost optimization, operational excellence, performance efficiency, reliability, security, and sustainability. Enable teams to make decisions by providing business context. 

## Plan your cloud modernization
---
1. Choose a modernization strategy. Replatform for quick wins, rearchitect or rebuild for long-term benefits, or replace with SaaS solutions.
2. Plan modernization in phases. Break workloads into smaller pieces. Communicate and document clear success criteria.
3. Plan for modernization governance. Establish formal change approval workflows with CAB or create your own review board structure if it is missing. 
4. Define your deployment strategy. In Place deployment, parallel deployment or some type of canary releases
5. Plan to mitigate modernization risks. Data loss, downtime, security vulnerabilities, compliance issues.
6. Secure Stakeholder approval and buy-in. Regular updates and demos to showcase progress and gather feedback.

# Execute Modernizations in the cloud
---
1. Prepare stakeholders for modernization - announce deployment windows, change freezes, and support plans. Define rollback and fallback procedures. 
2. Develop in non-prod environment. Follow the Well Architected Framework. Use DevOps practices and tools for CI/CD, testing, and monitoring. Implment changes incrementally with source control. 
3. Validate modernization changes with extensive testing - functional, performance, security, compliance, user acceptance. Use automated testing tools to streamline the process.
4. Use reusable infrastructure as code (IaC) templates for consistent deployments.
5. Create deployment documentation for future reference. Include Rollback and validation procedures.
6. Deploy modernization. Use CI/CD pipelines for automated deployments. Monitor deployments closely and be ready to execute rollback if needed. App Splitting, deployments using app service slots and gradually increasing to full traffic. Parallel deployments created carefully using repeatable IaC templates. Perform final cutover using DNS or load balancer configuration. Keep the old environment as a HOT standby until you are sure everything is working well.
7. Validate modernization success - monitor performance, security, and compliance. Collect user feedback and document issues and improvements.
8. Support Workload during this stabilization. Shorter SLAs, increased monitoring, dedicated support teams, more training for operations teams.

## Optimize Workloads after Modernization
---
1. Optimize for the cloud. Review Azure Advisor recommendations for cost, security, performance. Continuously monitor and adjust configurations. Use Microsoft Defender to resolve critical findings.
2. Validate operational readiness. Ensure that Azure Monitor logs, metrics, alerts, etc are configured correctly. Reduce these as the workload stabilizes. Test backup and HA configurations. Use Cost Management + Billing to monitor and control costs.
3. Collectu user feedback. Document issues and improvements.
4. Establish continuous modernization practices. Schedule regular workload reviews to ensure continued optimization and alignment with business goals. Use Azure Policy and set up cost anomaly alerts to enforce governance.
Read this: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/modernize/prepare-organization-cloud-modernization

# Cloud Native
---
Cloud native is an approach to building and running applications that fully exploit the advantages of the cloud computing delivery model. Cloud native applications are designed to be scalable, resilient, and manageable in dynamic environments such as public, private, and hybrid clouds.

1. Define business objectives for cloud native solutions. Start with clear measurable goals, constraints, success criteria.
2. Define requirements for cloud native solutions. Functional and non-functional requirements, technical constraints, compliance needs. In Scope vs Out of Scope.
3. Plan the cloud native architecture. Microservices, containers, serverless, event-driven, APIs, data management, security, monitoring. In place upgrades for minor, blue-green or canary for major changes.
4. Plan the cloud native deployment strategy. DevOps practices, automated CI/CD pipelines, testing, monitoring, rollback procedures.
5. Define rollback plan. Recover from failures during deployment or operation.

Build Cloud Native Solutions
1. Apply Well Architected Framework principles. Cost optimization, operational excellence, performance efficiency, reliability, security, sustainability. Implement source control with CI/CD pipelines for automated builds, tests, and deployments. Use Infrastructure as Code (IaC) for consistent and repeatable deployments. Implement Azure Monitor and Application Insights right from the start. Set clear expectations.
2. Again, create reusable infrastructure. Load in blueprint architectures and use IaC.
3. Create deployment documentation. Include rollback and validation procedures.

Deploy Cloud Native Solutions
1. Prepare stakeholders for deployment. Announce deployment windows, change freezes, and support plans.
2. Execute deployment using automated CI/CD pipelines. Monitor deployments closely and be ready to execute rollback if needed. Expose new systems to small groups first.
3. Validate deployment success. Monitor performance, security, and compliance. Collect user feedback and document issues and improvements. React and build on feedback quickly.
4. And again, Support workload during stabilization. Shorter SLAs, increased monitoring, dedicated support teams, more training for operations teams. Define clear exit strategy for stabilization phase.

Optimize Cloud Native Solutions
1. Fine tune the configurations. Review Azure Advisor recommendations for cost, security, performance. Well Architected Framework for design considerations, address security using Defender for Cloud recommendations.
2. Validate operational readiness. Ensure that Azure Monitor logs, metrics, alerts, etc are configured correctly. Reduce these as the workload stabilizes. Test backup and HA configurations. Document for later user onboarding.
3. Cost monitoring and optimization using Cost Management + Billing. Automate and review utilization patterns. Shut off what is not needed during off hours. 
4. Test backup and recovery procedures regularly. Perform trial restorations in non prod environments
5. Collect user feedback. Document issues and improvements.
6. Establish continuous improvement practices. Schedule regular workload reviews to ensure continued optimization and alignment with business goals.
Read this: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/cloud-native/plan-cloud-native-solutions

# Govern
---
Build a governance team to maintain consistent control. Govern methodology helps organizations establish and maintain governance policies for cloud adoption. This includes defining governance roles and responsibilities, implementing governance policies, and monitoring compliance with governance policies.
- Establish a governance team
- Define governance roles and responsibilities
- Implement governance policies
- Monitor compliance with governance policies

Important: Ensure your organization supports your cloud governance team. 

Assess Cloud Risks
- identify risks and catalog them - Use Azure tools to list assets and discover risks.
- Analyzie risks and assign a value to each risk based on potential impact and likelihood.
- Determine the impact of a risk - financial, operational, reputational, business impact
- Document Risks and communicate
- Review risks regularly and update the risk register as needed.

# Document Policies
---
Healthy cloud governance strategy starts with sound cloud governance policies. Document policies that address:
- Cost Management
- Security
- Compliance
- Resource Management
- Identity and Access Management
- Data Management

## Enforce Policies
---
Incorporate controls and procedures to align wiht your cloud governance policies.
- Use Azure Policy to create, assign, and manage policies that enforce rules and effects for your resources.
- Use Azure Blueprints to define a repeatable set of Azure resources that implement and adhere to your cloud governance policies.
- Implement role-based access control (RBAC) to manage access to resources based on user roles and responsibilities.
- Use Azure Security Center to monitor and enforce security policies across your cloud environment.
- Regularly review and update your governance policies and enforcement mechanisms to ensure they remain effective and aligned with business goals.

For a smooth transition:
- Delegate governance responsibilities
- Adopt an inheritance model for policies
- Apply tagging and naming conventions
- Implement a monitor first approach

## Monitor Compliance
---
Monitor those that lack compliance with your governance policies.
Develop a remediation plan to quickly address violations and prioritize high risk problems.

# Monitor
---
Strategy, Plan, Ready, Migrate, Innovate, Govern, Manage...
The Manage methodology helps organizations monitor and manage their cloud environment. This includes setting up monitoring tools, configuring alerts, and establishing operational processes.

1. Identify management responsibilites - Distinguish between central responsibilities and those delegated to teams. Define clear ownership for governance, security, and management functions.
2. Establish Operations team - centralized management for small, shared management for diverse. Form dedicated teams for platform tasks and then assign ownership of specific workloads to application teams.
3. Document Operational prcedures - Create standardized procedures for change management, deployments, disaster recovery. Step by step guides for common tasks, store runbooks in a central accessible repository.
4. Manage daily operations - Establish 24/7 monitoring and support. Use Azure Monitor and Azure Security Center for proactive monitoring. Implement incident management processes for timely resolution.
5. Improve continuously - Regularly review and update operational procedures. Conduct post-incident reviews to identify lessons learned. Encourage a culture of continuous improvement and learning via MS certifications and Azure training resources. 

## Administer Azure Cloud Estate
---
1. Define administrative scope - Responsibilities, focus on areas you control
2. Control changes - ticketing tools, CAB, Azure Policy and IaC
3. Secure your environment - Entra ID RBAC, MFA, Conditional Access, Defender for Cloud
4. Maintain Compliance - Align to NIST and ISO
5. Govern Data - Classify data using Purview, isolate workloads
6. Control Costs - Budgets, Cost Management + Billing, Azure Advisor
7. Manage Code and Runtime - WAF's Operational Excellence checklist
8. Manage resources - IaC, CI/CD, maintain configuration drift
9. Handle Relocations - user proximity, data residency, compliance
10. Maintain Operating Systems - automate patching, monitor changes

## Monitor your Azure Cloud Estate
---
1. Define Monitoring Scope - Focus on service health, security, complaiance, cost and data management
2. Plan monitoring strategy - test, alert, inventory, log, analyze
3. Design the monitoring solution - Azure Monitor with Azure Arc, centralize data storage and automate via Azure Policy
4. Configure comprehensive monitoring - Set up metrics, logs, health checks, security alerts, cost alerts
5. Set up alerting on the above - integrate with ITSM tools, define escalation paths, avoid alert fatigue
6. Create visualizations - Tailor views for technical teams and management audiences

## Protect your cloud estate
---
1. Ensure reliability - backup, disaster recovery, business continuity
2. Protect data - replication and backup supporting RPO and RTO, cross region, encryption. 
3. Build Resilience - design for failure, auto-scaling, load balancing, health monitoring
4. Deploy Redundancy - geo-redundant storage, multi-region deployments, failover mechanisms
5. Business Continuity - develop and test plans, train staff, review regularly, test scenarios
6. Operate Security - threat protection, vulnerability management, security monitoring, incident response

Read this: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/manage/ready

# Secure
---
Strategy, Plan, Ready, Migrate, Innovate, Govern, Manage, Secure...
The Secure methodology helps organizations protect their cloud environment from security threats. This includes implementing security controls,monitoring for security threats, and responding to security incidents.
- Implement security controls
- Monitor for security threats
- Respond to security incidents

All recommendations adhere to Zero Trust principles:
- Cloud Adoption Framework Secure Methodology - https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/secure/overview
- Azure Well Architected Framework - security guidance - https://learn.microsoft.com/en-us/azure/well-architected/security/
- MS Cloud Security Benchmark - https://learn.microsoft.com/en-us/security/benchmark/azure/
- Zero Trust Guidance - https://learn.microsoft.com/en-us/security/zero-trust/ 

## CIA Triad Model
---
The CIA Triad model is a widely used framework for understanding and implementing information security. It consists of three core principles: Confidentiality, Integrity, and Availability.
- Confidentiality: Ensuring that sensitive information is only accessible to authorized users and systems. This involves implementing access controls, encryption, and data classification.
- Integrity: Ensuring that data is accurate and reliable. This involves implementing data validation, checksums, and version control.
- Availability: Ensuring that information and systems are accessible when needed. This involves implementing redundancy, backup, and disaster recovery

Ways to use the CIA triad model in cloud security:
- Data protection
- Business Continuity
- Customer Trust

Assign roles
- Shared responsibility model - RACI
- Security Operations Center (SOC) - monitor, detect, respond
- Incident Response Team - handle security incidents
- Compliance Team - ensure adherence to regulations and standards
- Governance Team - define and enforce security policies





