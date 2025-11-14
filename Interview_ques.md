Basic / Foundation Level (≈ 70 questions)

These focus on fundamentals, scripting, tooling, concepts, your experience.

**1. What does “automation” mean in a DevOps/infrastructure context?**

Answer:
In a DevOps or infrastructure context, automation refers to using scripts, tools, or systems to perform tasks that would otherwise be done manually — especially repetitive, error-prone, time-consuming tasks. It includes automating provisioning of resources (servers, containers, networks), deployments of applications, configuration management, monitoring, scaling, and rollback. The goal is consistency, speed, repeatability and reducing human error.

**2. How do you approach writing an automation script (from requirement → design → test → maintain)?**
Answer:
A good approach is:

Requirement gathering: Understand what task needs automating (e.g., “Deploy this microservice every midnight”, or “Clean up old logs every week”). Know inputs, outputs, failure modes, rollback expectations.

Design: Choose the scripting language/tools (Bash, Python, PowerShell, Ansible, etc). Think through the logic, parameterisation, error handling, idempotency. Plan for logging, notifications, and maintenance-ease.

Implementation: Write the script with clear structure, modular functions, configurable variables, proper comments. Ensure it has exit codes / error messaging.

Testing: Run in dev/staging environment; simulate normal & failure cases; test idempotency (running twice should not cause harm), test edge cases (resource unavailable, permissions denied).

Deployment/Integration: Integrate into pipeline or scheduler; ensure proper permissions, monitoring.

Maintenance: Document the script, version control it, ensure peer-review, handle future enhancements. Monitor its performance, adjust based on logs/errors.

**3. Which scripting languages have you used (e.g., Bash, Python, PowerShell)? Explain a sample script you wrote.

Answer:
(Your answer would detail your experience; here’s a generic example.)
I have used Bash for Unix/Linux automation and Python for more complex automation (logic, API calls).
Sample script example: I wrote a Bash script that nightly checks all web servers in a pool for disk usage > 80 %, logs the output, sends an email if any server exceeds threshold, and triggers a cleanup job. It used ssh to remote check, df -h, logs in a central location, and used mailx for alerts. Then I refactored into Python for better error handling and JSON parsing of server list.

**4. What are the pros & cons of using Bash vs Python for automation?

Answer:

Language	Pros	Cons
Bash	Very simple for shell commands, widely available on *nix systems, quick to write for simple tasks.	Harder to scale for complex logic, error-handling is weaker, libraries limited, harder to maintain large scripts, readability suffers.
Python	Rich libraries (HTTP, JSON, SSH, API client libraries), better structuring for logic, easier to maintain, strong error-handling.	Requires interpreter (though usually present), may be slower for simple tasks, overhead for trivial shell operations, some sysadmin teams may resist new languages.

Choice depends on the complexity: for “run this command nightly” Bash is fine; for “call APIs, parse results, make decisions, integrate logs”, Python is preferable.

**5. Explain version control (e.g., Git) and why it’s important for infrastructure code.

Answer:
Version control is a system (like Git) that tracks changes to code or files over time; it allows you to commit changes, view history, revert to previous versions, branch for features/experiments, merge changes with review. For infrastructure code (scripts, IaC templates, automation workflows) it is important because:

You get a history of who changed what and why, which supports auditing.

You can roll back to a previous known-good state if something breaks.

Collaboration: multiple team members can work on templates, scripts safely (branching, pull requests).

You can review changes (code review) before they are applied (important for automation).

It promotes repeatability: the same code deployed in dev/test/prod; drift is minimised.

**6. What branching strategies in Git have you used (feature branch, trunk-based, GitFlow)?

Answer:
I have used:

Feature-branch workflow: developers create branches like feature/xyz, work there, then do pull request to main or develop. Good for isolating work.

GitFlow: primarily master/main, develop, feature/*, release/*, hotfix/*. Useful for teams with structured releases.

Trunk-based development: developers commit frequently (often daily) to main (or trunk), with short-lived feature toggles or branches. I used this when the organisation emphasised rapid CI/CD and frequent production releases.
I prefer trunk-based for DevOps automation because it aligns with continuous delivery: simpler merges, fewer long-lived branches.

**7. Explain the term “Infrastructure as Code (IaC)”.

Answer:
Infrastructure as Code (IaC) is the practice of defining and managing infrastructure (servers, networks, databases, load-balancers, etc.) using machine-readable definition files (code) rather than manual configuration. This means you write templates or scripts that describe the desired state of your infrastructure, commit them into version control, and deploy them via automated tools. IaC ensures: reproducibility of environments, consistency between dev/test/prod, traceability, automation of provisioning and changes, and reduction of human error. 

**8. Which tools have you used for IaC (e.g., Terraform, Ansible, CloudFormation)?

Answer:
(Your answer would reflect your experience; here’s a sample.)
I have used:

Terraform: for multi-cloud infrastructure (AWS + Azure) provisioning, defining VPCs, subnets, IAM roles, compute fleets.

CloudFormation (AWS): to manage AWS stacks internally for certain teams.

Ansible: partly as configuration management, partly for infrastructure bootstrapping (installing packages, configuring services).
I find Terraform strong for declarative provisioning across clouds; Ansible is great for configuration after VMs/instances are live.

**9. What are the benefits of using IaC compared to manual configuration?

Answer:
Key benefits include:

Consistency: The same code deploys the same infrastructure; reduces “works on my machine” or environment drift.

Speed: Environments can be spun up quickly (minutes instead of hours/days).

Versioning/Audit trail: Changes to infrastructure are tracked in code, can be reviewed and reverted.

Repeatability: Dev/test/prod can be set up the same way; reduces configuration divergence.

Scalability: Large infrastructures managed via code can scale better than manual efforts.

Reduced human error: Fewer manual steps means fewer mistakes and misconfigurations.

Disaster recovery: You have code to rebuild environments quickly.

Better collaboration: Development/operations teams work on the same definitions.

**10. What is a CI/CD pipeline?

Answer:
CI/CD stands for Continuous Integration and Continuous Delivery/Deployment. A CI/CD pipeline is an automated workflow that takes code from commit (integration) through build, test, and deployment steps to deliver software. Typically: a developer commits code → version control triggers build → automated tests run → if successful artifact is created → deployment is triggered (to dev/staging/prod) → monitoring/feedback. The pipeline ensures frequent, reliable releases and rapid feedback loops. 

**11. Which tools have you used for CI/CD (e.g., Jenkins, GitLab CI, CircleCI)?

Answer:
(Your answer would reflect your experience.)
I have used:

Jenkins: for on-prem and cloud builds with pipelines defined in Jenkinsfiles; used for building, testing, artifact creation, and triggering deployments.

GitLab CI: for the repository + integrated pipeline in the GitLab environment, especially for smaller projects.

CircleCI: for certain selected microservices where we wanted quick cloud-based pipeline setup.

Azure DevOps Pipelines: when working in Azure-based environment.
I prefer Jenkins when we have complex needs/integrations, GitLab CI for tighter version control + pipeline integration.

**12. How would you structure a basic CI pipeline from commit to test to deployment?

Answer:
A basic pipeline may look like:

Source: Developer commits to main or a feature branch → triggers pipeline.

Build: Compile code (if applicable), assemble artifacts (e.g., JAR, Docker image).

Unit Test: Run fast unit tests; if failure, pipeline stops and reports to developer.

Static Analysis / Code Quality: Optional – run tools like SonarQube, linting.

Package / Artifact Store: Store built artifact into artifact repository (e.g., Nexus, Artifactory, Docker Registry).

Integration / Acceptance Tests: Deploy to a QA/staging environment; run integration tests.

Security/Compliance Scans: (Optional) run vulnerability scans.

Deployment: Deploy to production or a production-adjacent environment (canary, blue/green).

Verification & Monitoring: Validate deployment, smoke tests, monitor metrics/logs for health.

Notification: Notify relevant teams of success/failure.

Rollback/Remediation: If deployment fails, rollback or trigger remediation.
This ensures a controlled, automated path from code change to production.

**13. What is the difference between Continuous Delivery and Continuous Deployment?

Answer:

Continuous Delivery means that code changes are automatically built, tested, and prepared for production deployment, but the actual release to production may be manual (approval step).

Continuous Deployment takes this one step further — every change that passes all stages (build, test, etc) is automatically deployed into production without human intervention.
Thus, Continuous Deployment is a more mature/automated state; with Continuous Delivery you still have manual gating or approval before production.

**14. Explain the concept of “immutable infrastructure”.

Answer:
Immutable infrastructure is the paradigm where once an infrastructure component (server, container, instance) is deployed, it is never modified (not patched in place, not reconfigured manually). Instead, when updates are needed (patches, configuration changes), you build a new version of the infrastructure component and replace the old one. Benefits: consistency, fewer configuration drift issues, easier rollback (by reverting to the previous version), predictable behaviour. Drawbacks: may require more up-front investment in automation and orchestration; you need robust replacement/blue-green strategies.

**15. What is containerisation (e.g., Docker) and why is it useful?

Answer:
Containerisation is the technique of packaging an application and all its dependencies (libraries, runtime, configuration) into a lightweight, portable unit (a container) that can run in any environment that supports the container runtime (e.g., Docker). It is useful because:

Ensures consistency across environments (dev, staging, prod) — “it works the same everywhere”.

Enables fast startup and efficient resource use (containers share the host OS kernel).

Simplifies deployment of microservices or distributed architectures (you can run multiple containers across machines).

Facilitates scaling and orchestration via tools like Kubernetes.

Reduces complexity of environment/cross-dependency issues.

**16. What is container orchestration (e.g., Kubernetes) and when would you use it?

Answer:
Container orchestration is the management of container deployment, scaling, networking, load-balancing, service discovery, health-monitoring, and lifecycle across a cluster of machines. Kubernetes is a popular orchestration platform. You would use orchestration when you have multiple containers/services running (microservices architecture), need to scale dynamically, ensure high-availability, manage container health, roll-out/rollback updates, handle networking between services. Without orchestration, managing many containers manually becomes complex and error-prone.

**17. Describe a typical deployment process for a containerised application.

Answer:
Typical steps for deploying a containerised application:

Developer pushes code to repository.

CI pipeline builds the application and produces a container image (Docker build).

The image is tagged (version, environment) and pushed to a container registry (e.g., Docker Hub, ECR).

Automated tests (unit, integration) run on the image.

In staging environment, the image is deployed to a container orchestration platform (Kubernetes/other), via deployment descriptor (YAML) or Helm chart.

The platform ensures correct number of pods, load-balancers are configured, health-checks defined.

Smoke tests / acceptance tests run in staging; monitoring tools check health, logs, etc.

When validated, promotion to production: maybe a blue/green or canary deployment strategy.

Monitor logs, metrics (CPU/memory, latency, errors).

On issues, rollback to previous image version.

Document deployment runbooks; update monitoring dashboards.

**18. How do you handle configuration management across multiple environments (dev, staging, production)?

Answer:
Good practices for configuration management across environments:

Keep environment-specific variables/configuration separate from the code (e.g., using environment variables, config files, secrets stores).

Use the same automation scripts or IaC templates for each environment, with parameterisation for dev/staging/prod (so environments remain consistent).

Use version control for all configuration.

Use tools like Ansible, Puppet, Chef to apply configurations declaratively, ensuring idempotency.

Keep drift minimal: manual changes in production should be avoided; if done, they should be captured in configuration code.

Use infrastructure as code so dev/staging/prod are defined via the same templates but with different variable inputs.

Implement approval or gating mechanisms before promotions to production.

Use secrets management for production credentials; audit access.

**19. Explain the principle of least privilege in system administration.

Answer:
The principle of least privilege means giving users, systems, or services only the minimum permissions they need to perform their required tasks — no more. In system administration and DevOps, applying least privilege reduces risk by limiting the potential damage in case of compromise, accidental misuse or configuration errors. For example: an automation script deploying an application doesn’t need full root access on all servers; instead, it gets just enough privileges (e.g., write access to the service directory, ability to restart the service). Similarly, IAM roles in cloud infrastructure should restrict permissions and should be regularly reviewed and audited.

**20. What is SSH and how is it used in automation?

Answer:
SSH (Secure Shell) is a network protocol that provides secure encrypted communication between two systems (client/server). It's commonly used to log into remote machines and execute commands. In automation:

Scripts can use SSH to connect to remote servers and run commands (e.g., install packages, run deployments).

Configuration management tools (like Ansible) use SSH (agentless) to execute tasks across many servers.

It supports key-based authentication, which is important for automation (no manual password prompt).

SSH tunnels/port-forwarding are used for securely connecting to internal systems.
Because automation involves remote servers, SSH is a foundational tool/method for securely executing tasks in infrastructure.

**21. When would you use agent-based vs agentless configuration management?

Answer:

Agent-based tools install a persistent software agent on each target machine (e.g., Puppet agent). These agents periodically poll a central server or accept commands, enabling management, reporting, and state enforcement. Use agent-based if you need rich reporting, scheduled enforcement, complex orchestration, compliance features.

Agentless tools (e.g., Ansible over SSH) do not require an installed agent; they connect to target machines and execute commands/tasks. Use agentless if infrastructure is simpler, you prefer minimal footprint, or you have environments where installing agents is undesirable (e.g., restricted systems).
In summary: Agentless often simpler and lighter; agent-based gives more features/control — choice depends on environment complexity, security policy, network restrictions.

**22. How do you monitor logs and metrics in production systems?

Answer:
Monitoring logs and metrics typically involves:

Metrics: Set up monitoring tools (e.g., Prometheus, Grafana, CloudWatch) to capture numerical data (CPU, memory, disk I/O, network traffic, request latency, error rates). Create dashboards and alerts when thresholds are breached.

Logs: Use a centralized logging system (e.g., ELK stack — Elasticsearch, Logstash, Kibana) or managed services (Cloud Logging) to aggregate, index, and search logs. Configure log shipping from servers/containers, set log retention, use structured logs (JSON) if possible.

Correlation and alerting: Link logs and metrics to detect anomalies (e.g., spike in errors + high latency), set up alerting on key signals.

Ownership & dashboards: Ensure teams have dashboards summarising health, trends; runbooks defined for common events.

Automation: Use automation to respond to certain alerts (auto-remediation), and use logs/metrics as feedback for tuning automation.
This enables visibility, faster detection of issues, root-cause analysis.

**23. How would you troubleshoot a failure in an automated deployment?

Answer:
Troubleshooting steps might include:

Gather context: Which stage of pipeline failed (build, test, deploy)? What error message? What changed recently?

Check logs: Look at pipeline logs, deployment logs, application logs, system logs for errors/stack traces.

Rollback or snapshot: If production is impacted, consider rollback to last stable version.

Reproduce in staging: Try to reproduce the failure in a non-production environment to isolate the issue.

Check infrastructure health: Are servers/containers healthy? Resources (CPU, memory, disk) adequate? Network connectivity ok?

Check configuration drift or mismatches: Maybe config differs between staging and production.

Check script/automation changes: Did someone change the automation script or IaC template? Version control history helps.

Simplify and isolate: disable parts of pipeline to isolate which sub-step causes failure.

Apply fix and test: Once root cause is found, fix the automation (script, configuration, resource), test thoroughly, then re-run.

Post-mortem: After resolution, document what happened, how it will be prevented in future (runbook update, alerting, improved test).

**24. Explain how you would roll back a failed release.

Answer:
A rollback strategy might include:

Pre-planning: Before deployment, take snapshot/backups of databases, containers, VM images or retain previous versions of artifact/container image.

Blue/green or canary deployment: Use architecture where you deploy a new version (green) while old version (blue) still serves; if new fails, switch traffic back to blue.

Version control: Have previous stable release version in registry; deployment automation should support selecting previous version and promoting it.

Automated rollback script: The pipeline may include a rollback step triggered by failures or alerts (e.g., if error rate > threshold in new version).

Database handling: If schema changes were applied, you must ensure that rollback does not corrupt data; either have backward-compatible changes or a way to revert schema changes safely.

Communication: Notify stakeholders of rollback, update status in runbook.

Post-rollback verification: Confirm that the old version is healthy, metrics/logs are normal; then root-cause the failure of the new version.

Update automation/process: After rollback, improve the pipeline to avoid repeat of same failure.

**25. What are the key networking concepts a DevOps engineer should know (e.g., TCP/UDP, load balancing, DNS)?

Answer:
Key networking concepts include:

TCP vs UDP: Understanding connection-oriented vs connection-less protocols, state, reliability.

IP addressing and subnets: How networks are segmented, CIDR notation, public vs private subnets.

DNS: How domain names map to IPs, TTLs, record types (A, CNAME), impact on deployment and blue/green switches.

Load balancing: Distributing traffic across multiple servers, types of load-balancers (layer 4 vs layer 7), health checks.

Routing and NAT: Traffic between networks, internet gateway, NAT gateway, VPNs.

Firewall/security groups: Controlling inbound/outbound traffic, ports, protocols — especially in cloud environments.

Network latency/bandwidth: Impact on distributed systems, microservices communication, and on-premise vs cloud.

Service discovery: How services find each other in dynamic environments (via DNS, etcd, Consul).

High-availability networking: Multi-AZ, multi-region failover, DNS failover, load-balancer redundancy.
Having a sound networking foundation helps a DevOps engineer design resilient, secure infrastructure and troubleshoot connectivity/performance issues.

**26. What is RESTful API and how is it relevant in automation tasks?

Answer:
A RESTful API (Representational State Transfer) is a style of web service interface that uses standard HTTP methods (GET, POST, PUT, DELETE) to operate on resources, often returns data in JSON or XML, and is stateless. In automation tasks:

You often call cloud provider APIs (for provisioning, configuration) which are RESTful.

Tools/scripts integrate with REST APIs of services (e.g., monitoring, ticketing) to trigger workflows or retrieve data.

Using REST APIs allows automation of tasks like “create server”, “deploy container”, “trigger pipeline”, “retrieve logs”.

Understanding API endpoints, authentication (tokens, OAuth), error handling makes automation robust.
Thus, RESTful APIs are key for programmatic control of infrastructure, pipelines and services.

**27. How do you integrate APIs into automation workflows (e.g., retrieving data, triggering workflows)?

Answer:
Steps for integrating APIs into automation workflows:

Identify the API endpoint and purpose: e.g., “Trigger deployment”, “Get current deployment status”, “Retrieve metrics”.

Handle authentication/authorization: Use API keys, OAuth tokens, service principals. Ensure credentials stored securely (not hard-coded).

Write code or script: Use Python (requests library), Bash (curl), PowerShell (Invoke-RestMethod) to call the API, pass parameters.

Parse response: Extract relevant fields from JSON/XML response; handle errors/status codes.

Use data: Based on API response, decide next step in workflow (e.g., if status is ‘failed’, trigger alert or rollback).

Chain workflows: Use APIs to trigger other systems (e.g., after provisioning infra, call API to configure it, then call API to notify team).

Logging & monitoring: Log API calls, responses, performance. Set alerts for failed API calls or unexpected responses.

Security & rate-limits: Respect rate limits, use retries/backoffs, secure secrets, rotate credentials.
By integrating APIs you make automation dynamic, data-driven, and capable of interacting with multiple systems and services.

**28. Describe the difference between synchronous and asynchronous operations in automation.

Answer:

Synchronous operations: The automation workflow waits for an operation to complete before moving to the next step. The caller is blocked until response is received. Example: a script executes “deploy service” and waits for success/failure before continuing.

Asynchronous operations: The operation is initiated and the workflow doesn’t wait; it may continue to next tasks or monitor for completion via callback, polling, or event. Example: You trigger a large data move, immediately continue with other tasks, and later check for completion or get an event/notification.
In automation: synchronous is simpler but can slow pipeline (waiting). Asynchronous is more scalable (you trigger many operations and proceed), but you must handle eventual consistency, monitoring for completion, error handling for delayed failures. Knowing when to use each is important for efficient workflows.

**29. How do you maintain documentation (architecture diagrams, runbooks, workflows)?

Answer:
Maintaining documentation involves:

Version-control: Store documents (diagrams, runbooks, markdown) in Git or other VCS so changes are tracked.

Standard templates: Use templates for architecture diagrams (Visio/Draw.io), workflows, runbooks so they are consistent.

Keep it up-to-date: After any change to automation/infrastructure, update the documentation immediately (or as part of change process).

Accessible location: Store docs in a shared repository/wiki (e.g., Confluence, GitLab wiki) where team members can easily find them.

Clear audience and use-cases: Different docs for different audiences (operations runbook for support teams, architecture overview for architects, step-by-step workflow for team members).

Include diagrams, steps, decision trees: For runbooks especially, include what to do when something fails.

Review & audit: Periodically review documentation for relevance, completeness; remove obsolete docs.

Link to automation code: For example, link a runbook to the script it refers to; include version numbers.
Proper documentation ensures maintainability, better handover, faster incident resolution, and knowledge sharing.

**30. Why is documenting your automation scripts and workflows important?

Answer:
Documenting scripts and workflows is important because:

Knowledge transfer: Other team members (or future you) can understand what the script does, how it works, how to maintain it.

Maintainability: Scripts evolve; without documentation you risk losing context, making the code brittle or unmaintainable.

Troubleshooting: When something fails, documentation (like comments, descriptions, runbooks) helps you quickly understand expected behaviour and deviation.

Audit & compliance: Many organisations require documentation for infrastructure, automation, especially in regulated sectors.

Scalability and team collaboration: When automation is shared across teams, documentation ensures clarity of responsibilities, input/output, dependencies.

Risk reduction: If someone leaves, changing the automation becomes harder without documentation; you may lose institutional knowledge.

Consistency: If workflows are documented, new scripts can follow standard conventions, versioning, naming, making the environment more consistent.

**31. What is the role of cross-functional collaboration in DevOps / automation?

Cross-functional collaboration is central to DevOps because it breaks down traditional silos between development, operations, QA, security, and business teams. When different teams work together:

You get shared ownership of code, infrastructure, and processes.

Dev and Ops can jointly define automation workflows, ensuring that deployments, monitoring, and failure recovery make sense across both sides.

It enables faster feedback loops: developers hear about operational pain points; operations teams understand the business and architecture goals.

Collaboration improves reliability and ensures automation isn’t built in a vacuum — business and operations needs (like compliance, performance, uptime) are baked in.

It fosters a culture of continuous improvement: teams can identify and eliminate bottlenecks, redundancies, or manual steps together.

According to WithCoherence, building shared processes (CI/CD), using shared tools, active communication, and mapping out work responsibilities helps teams avoid misalignment. 
withcoherence.com

**32. Explain how you would gather requirements from a business or operations team for an automation solution.

Here’s a structured approach:

Stakeholder Identification: First, identify who needs to be involved — business owners, product managers, operations leads, support teams, QA, security.

Workshops / Meetings: Conduct discovery workshops or meetings to understand current pain points. Ask questions like:

What repetitive tasks are consuming most time?

Which manual operations are error-prone?

What are the uptime, performance, security, or compliance requirements?

What are “business as usual” vs “peak / incident” scenarios?

User Stories: Translate these into user stories or use-cases. For example: “As an operations engineer, I want to trigger infrastructure provisioning for a new microservice with one command so that I don’t manually configure VMs each time.”

Prioritisation: Work with stakeholders to prioritise automation tasks based on ROI, risk, frequency, and business value.

Define Metrics: Agree on key metrics / KPIs (deployment time, errors reduced, manual hours saved) to measure success.

Design & Prototype: Propose a prototype or POC (Proof of Concept) automation flow. Review this with stakeholders.

Feedback & Iteration: Once the POC is done, demonstrate it, collect feedback, and refine — making sure that the final automation aligns with business needs and team workflows.

Documentation & Training: Document the requirement decisions, runbooks, flows, and train the operations team / business team to use and maintain the automation.

**33. What is production support and how does it differ from development?

Production Support refers to the ongoing operational support, monitoring, maintenance, and troubleshooting of live systems. The goal is to keep production stable, performant, and available.

Development, on the other hand, focuses on building new features, improvements, or fixes in a non-production (or staging) environment. The risks, priorities, and processes are different.

Key differences:

Risk: Production support works in a high-risk environment – changes must be carefully tested or rolled out with minimal disruption.

Time sensitivity: Support often demands quick reactions (incidents, outages) and may happen after hours; development usually works on planned schedules.

Testing: In development you use dev / QA / staging to test changes; in production support, changes may need careful validation, rollback plans, or hotfix approach.

SLA commitments: Support teams often operate under Service Level Agreements (SLAs) for uptime, MTTR (Mean Time to Recovery), etc.

Collaboration: Support engineers must closely coordinate with operations, site reliability, business to communicate status, do root-cause analysis, and provide runbooks for future incidents.

**34. How have you handled “after-business hours” releases? What precautions do you take?

Here are the best practices / precautions (and how I would / have implemented them):

Planning & Schedule: Schedule the release during low-traffic windows. Confirm timing with business stakeholders.

Backup & Rollback: Before the release, take backups (databases, configurations). Prepare a rollback plan (or blue/green / canary cutover) so that if something fails, you can revert quickly.

Automated Tests: Ensure automated smoke tests, health checks, and post-deployment validations are in place.

Runbooks: Have a detailed runbook / deployment playbook, including manual intervention steps, rollback steps, and hotfix procedures.

Communication: Inform all stakeholders (Dev, Ops, Business, Support) about the release plan, potential risks, escalation points, and contact persons.

On-call Team: Have a small on-call deployment / SRE team ready; ensure people know how to reach each other (chat, phone).

Monitoring & Alerting: Monitor metrics (CPU, memory, error rates), logs, application health, and set up alerts to detect regression / failure early post-release.

Change Control: Use change management procedures (if applicable), ensure approvals, and maintain logs of changes executed, commands run, and who ran them.

Post-deployment Review: After the release, run a post-mortem / review meeting: check what went well, what failed, what can be improved. Update runbooks accordingly.

**35. How do you ensure minimal downtime during a deployment?

A few strategies to minimize downtime:

Blue/Green Deployment: Deploy the new version to a separate environment (green), validate it, then switch traffic from the old (blue) environment to green. This allows rollback by switching back. 
Wikipedia

Canary Deployment: Roll out the change to a small subset of users / servers, monitor for issues, and then gradually increase traffic.

Rolling Update: Update nodes / servers in batches; take a few out of service, patch them, bring them back, then move to the next batch.

Feature Flags: Deploy code with flags that can turn features on/off; switch on new features only after validation.

Database Migration Strategies: Use backward-compatible migrations, versioned schemas; deploy code that works with old and new schema; avoid breaking changes.

Health Checks & Pre-Traffic Validation: Before cutting over traffic, run smoke tests, health checks, synthetic transactions, and validate performance.

Load Balancer Management: Use load balancers intelligently to drain traffic from servers under update, then bring them back.

Monitoring & Metrics: Monitor critical metrics (latency, error rate, throughput) during and after deployment to detect regressions quickly.

Automated Rollback: In case of failure thresholds (error rate, health check failures), automate rollback to previous stable version.

**36. Explain blue/green and canary deployment strategies.

Blue/Green Deployment: As mentioned, you have two identical environments: Blue (current production) and Green (new version). You deploy changes to the green environment, test it thoroughly, and then switch all traffic from blue to green. If anything goes wrong, you can switch back. Benefits include quick rollback, minimal disruption. 
Wikipedia

Canary Deployment: Here, you release the new version to a small subset of your infrastructure (or a subset of users) first (the canary), monitor performance and stability, and gradually increase the rollout if things look good. This minimizes risk by limiting exposure and giving you time to detect any problems in production.

**37. What is the difference between horizontal and vertical scaling?

Horizontal Scaling (scale out): Adding more machines/instances/containers to your system. E.g., adding more web server instances behind a load balancer. This improves capacity, fault tolerance, and redundancy.

Vertical Scaling (scale up): Increasing the capacity of a single machine by adding more CPU, memory, or storage. This can improve performance for a single node but has limits (hardware limits) and may introduce a single point of failure.

**38. How would you tune performance of an automated workflow or infrastructure system?

Performance tuning involves:

Measure Baseline: Use monitoring to gather baseline metrics (latency, CPU, memory, pipeline times, task durations).

Identify Bottlenecks: Find stages in automation workflows that take longest: build time, test time, deployment, infrastructure provisioning.

Optimize Scripts / Workflows: Refactor scripts to make them more efficient (e.g., parallel tasks, caching dependencies, reusing artifacts).

Resource Tuning: For infrastructure, adjust instance sizes, autoscaling policies, load-balancer settings.

Caching: Use caching for dependencies, container layers, build artifacts to reduce repeated work.

Parallelization: Run independent jobs or tasks in parallel wherever possible (tests, builds).

Improve Tests: Eliminate slow or redundant tests; use lighter-weight tests in early stages, run heavier tests later.

Use Efficient Tools: Choose faster build tools, optimized container builds, or more efficient IaC tooling.

Autoscaling / Dynamic Provisioning: Use autoscaling so infrastructure scales out/in automatically based on the load.

Feedback Loop: Continuously monitor, tune, and re-evaluate after each change; build dashboards, set alerts for performance regressions.

**39. What is drift in infrastructure configuration and how do you detect / prevent it?

Drift (configuration or infrastructure drift) is when the actual state of your infrastructure diverges from the desired state defined in your IaC (Infrastructure as Code) scripts. 
Spacelift
+2
Medium
+2

Causes: manual changes in the cloud console, emergency fixes, inconsistent team practices, or resources being changed outside IaC. 
Medium
+1

Detection:

Use IaC health-assessment tools: e.g., Terraform’s health assessments. 
HashiCorp Developer

Use drift-detection tools like driftctl which compares Terraform state vs real infra. 
infoq.com

Use provisioning pipelines that run “plan-refresh-only” to detect drift. 
Harness Developer Hub

Prevention / Remediation:

Use strict access controls, minimize manual changes, use GitOps (treat IaC as the single source of truth). 
Spectro Cloud

Periodic reconciliation: run automated checks and if drift is detected, either alert or automatically apply corrective IaC changes. Tools like Firefly help by codifying drift back into your IaC and alerting teams. 
Firefly

Use policy-as-code to enforce guardrails (e.g., disallow non-codified changes). 
DevOps.com

**40. How do you secure secrets (passwords, tokens, keys) in automation workflows?

Use a secrets management system: HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, etc.

Avoid hard-coding credentials in scripts or IaC.

Use role-based access control (RBAC) for secrets: only allow automation systems or service accounts to access secrets.

Use dynamic secrets when possible: just-in-time secrets that rotate on use.

Use encryption: secrets should be encrypted at rest and in transit.

Audit & rotate: regularly rotate keys/secrets, maintain audit logs of who accessed what secret and when.

Inject secrets securely into runtime (e.g., via environment variables, in-memory, or service injection) rather than storing locally.

Explain the concept of “shift-left” in DevSecOps.

“Shift-left” means integrating security (and testing) earlier in the software development lifecycle — essentially moving security practices (like vulnerability scanning, code analysis, compliance checks) to earlier phases (e.g., during code design, build, unit tests) rather than at the end (just before production). Benefits: you detect and fix security issues early (when they’re cheaper to fix), reduce risk, and embed security into CI/CD pipelines.

**41. What is the difference between Waterfall and Agile methodologies?

Waterfall: A linear, sequential development model. Phases like requirements → design → development → testing → deployment happen one after the other. Changes are harder to incorporate once a phase is completed.

Agile: Iterative and incremental. Work is broken into sprints / iterations; frequent feedback, continuous planning, and adaptation. Teams deliver small chunks of functionality regularly and adjust based on stakeholder feedback or changing priorities.

**42. Have you worked in Agile teams? How does DevOps complement Agile?

Answer (example):
Yes — I have worked in Agile teams where we followed 2-week sprints, planning, daily standups, sprint reviews, and retrospectives. DevOps complements Agile in many ways:

Continuous Delivery: With DevOps automation, we can release features developed in Agile sprints more frequently and reliably.

Feedback Loop: DevOps enables faster feedback (via CI/CD, monitoring) which aligns with Agile’s principle of inspect & adapt.

Cross-functional Teams: Agile encourages cross-functional teams; DevOps brings Dev and Ops closer, improving collaboration.

Quality & Stability: Automation ensures code quality, testing, and deployment processes are consistent — this helps Agile teams maintain quality even with fast releases.

Responsiveness: When agile backlogs change, automated pipelines let you adjust deployments quickly, without manual ops bottlenecks.

**43. How would you present risk or issue escalation to stakeholders?

Identify Risks Early: Document potential risks (deployment failures, rollback, data loss, security) during planning.

Risk Assessment: For each risk, assess likelihood and impact. Create a risk matrix or register.

Communication Plan: Establish who needs to be informed, when, and how (email, chat, dashboard).

Mitigation Strategy: For each risk, define mitigation: e.g., pre-release testing, canary rollout, back-ups.

Escalation Process: Define and document escalation paths: who handles what level of failure, who is on-call, who approves rollbacks.

Status Updates: During deployment / automation, provide real-time visibility via dashboards or updates. If a risk materializes, escalate immediately with context (what failed, impact, rollback plan).

Post-Incident Review: After risk event or issue, run a post-mortem, document root cause, lessons, and actions to avoid recurrence.

Describe a time when you identified an improvement opportunity in automation / infrastructure.

Sample Answer (you can adapt):
In my previous role, I noticed that our nightly patching process was manual: we SSHed into servers, installed updates, and verified services one by one. This was time-consuming and error-prone. I proposed and built an Ansible playbook that automated the patching: it connected to all servers, applied updates, restarted services, performed health checks, and sent a summary report. This reduced the time taken from ~3 hours to 45 minutes and nearly eliminated patch-related failures. After rollout, I documented the process in a runbook and handed it over to the operations team. I also set up a weekly schedule so the playbook runs automatically.

**44. What are KPIs or metrics you would track for an automated system?

Some useful KPIs / metrics:

Build Success Rate: Percentage of builds that succeed vs fail.

Deployment Frequency: How often you deploy to staging / production.

Deployment Lead Time: Time from code commit to deployment.

Mean Time to Recovery (MTTR): How quickly you recover from failures.

Change Failure Rate: Percentage of deployments that cause failures / require rollback.

Automated Task Success Rate: For automated operational tasks, how often they run successfully.

Infrastructure Cost Utilisation: Cost per environment, resource wastage, autoscaling efficiency.

Resource Performance Metrics: CPU, memory, I/O, latency for systems.

Drift Events: Number of drift incidents detected + resolved.

Security Metrics: Number of vulnerabilities found or remediated via automation, time to remediate.

On-call Metrics: Number of incidents / alerts in hour, frequency of manual overrides, time to respond.

**45. How do you ensure your automation solution is scalable and maintainable?

Modularization: Write modular code / scripts: reusable functions, templates, roles (in Ansible), modules in Terraform.

Parameterisation: Use variables / parametrized templates so the same automation can be used across environments.

Version Control: Keep automation code in Git / version control with reviews.

Documentation: Maintain clear documentation (runbooks, architecture, workflows) for maintainers.

Testing: Write unit tests, integration tests, and infrastructure tests (IaC plan / apply in non-prod).

CI for IaC: Use pipelines to validate IaC changes (linting, terraform plan, etc).

Scalable Architecture: Use autoscaling, containerization, partitioning, microservices where needed, so that automation scales as load increases.

Governance: Use policy-as-code / guardrails to enforce standards, prevent drift, and maintain compliance.

Monitoring and Feedback: Continuously monitor performance, failures, and usage; iterate and refactor as needed.

Explain the difference between push vs pull configuration management.

Push-based: A central server (or controller) “pushes” configuration changes to target machines. The controller initiates the connection to each node and applies the configuration.

Pull-based: Each target machine (node) periodically “pulls” configuration from a central source (e.g., a Git repo or configuration server), and applies what’s needed.

Trade-offs:

Push: more control, immediate enforcement; but scaling to many nodes can be harder; security (controller needs credentials) is a concern.

Pull: nodes are more autonomous, better for scaling, and often more resilient, but changes are not instantaneous (depends on pull interval).

What is event-driven automation? Give an example.

Event-driven automation means triggering automation workflows based on events rather than schedules. An event could be a webhook, a message in a queue, a change in resource state, or a system alert.

Example:

When a new image is pushed to a Docker registry, a webhook triggers a CI/CD pipeline that runs tests, builds a container, and deploys it.

Or: an AWS CloudWatch alarm for CPU usage > 80% triggers a Lambda function that automatically scales up (auto-provisions) another instance, updates load balancers, and registers the new instance, based on the event.

**46. How do you ensure high availability (HA) in infrastructure deployments?

Redundancy: Deploy multiple instances of services / servers across different availability zones (AZ) or regions.

Load Balancing: Use load balancers to distribute traffic among healthy instances.

Auto-Scaling: Use autoscaling policies to add/remove instances based on metrics (CPU, latency, request count).

Health Checks: Regularly check instance health; remove or replace unhealthy nodes.

Failover Strategy: Implement failover between zones / regions for disaster recovery.

Database HA: Use database clustering, replication, or managed HA databases (read replicas, multi-AZ).

Stateless Design: Prefer stateless services that can be spun up easily; use external state storage (like managed DB, distributed cache).

Backups: Maintain regular backups, snapshots, and disaster recovery plans.

Immutable Infrastructure: Use immutable deployments so new versions replace old reliably.

Monitoring & Alerts: Monitor availability metrics, set alerts, have runbooks for failover and recovery.

**47. What is a load balancer and when is it used?

A load balancer is a network component that distributes incoming traffic across multiple backend servers or instances to ensure no single server is overwhelmed, improving scalability, reliability, and availability.

When to use:

When you have multiple servers serving the same application.

To scale out horizontally.

To provide redundancy / availability (if one node fails, traffic is routed to others).

To perform health checks and remove unhealthy nodes automatically.

To manage traffic across different zones or regions, or to handle SSL termination, routing rules, etc.

**48. How would you manage versioning of infrastructure code?

Use Git (or any version control system) to track IaC (Terraform, CloudFormation, Ansible) as code.

Use branches for features, bugfixes, and separate environments (dev, staging, prod).

Tag / label releases of IaC (e.g., v1.0, v1.1) so you know which version corresponds to which infrastructure state.

Use state locking and backend for Terraform (e.g., remote state backend with locking) to avoid concurrent changes.

Maintain change logs in commits or in a separate CHANGELOG file.

Use CI pipelines to validate changes (plan, lint, test) before applying.

Use branch promotions: once IaC changes are validated in dev / staging, merge into a “prod” branch and apply.

Use immutable modules: version your Terraform / Ansible modules so changes are tracked in module versions.

**49. How do you test infrastructure changes before applying them to production?

Terraform Plan / Preview: Use terraform plan (or equivalent in other IaC tools) to preview changes and see what will be created/modified/destroyed.

CI Pipeline Validation: Integrate the plan & validation in the CI pipeline (linting, compliance checks, plan analysis).

Test Environments: Apply the IaC in a staging / test environment first.

Automated Tests: Use infrastructure tests (e.g., terraform validate, Terratest, or other framework) to test resource creation, configuration.

Integration Tests: Once infrastructure is created, run integration tests (e.g., deploy application, run smoke tests).

Drift Detection: Use drift detection in non-prod to ensure applied infra matches code.

Manual Validation: After deployment to test env, manually inspect key resources (networking, security groups, IAM, etc).

Peer Review: Use code review for IaC changes (pull requests) to catch risky or incorrect changes.

Rollback Strategy: Always plan for rollback — have snapshots, backups or a previous version of infrastructure ready in case something goes wrong.

**50. Explain the concept of a “runbook”.

A runbook is a documented set of procedures or operations that outlines step-by-step instructions to handle routine or emergency tasks. It serves as a guidebook for operational teams (on-call, support, SRE) to respond to incidents, perform deployments, or conduct maintenance. A runbook typically includes:

What the problem is / scenario (incident, deployment).

Preconditions or checks (what to verify before starting).

Step-by-step steps (commands, scripts, workflows).

Expected outcomes and validations (how to verify the action succeeded).

Rollback steps (if something goes wrong).

Escalation path (who to contact, when).

Concluding steps (clean-up, post-mortem, documentation).

**51. How do you design a runbook for an incident?

Define the Incident Scenario: Clearly describe what kind of incident the runbook covers (e.g., “High CPU on web server”, “Database connection failure”, “Service crash”).

Detection / Trigger: Specify how the incident is detected (alert name, metric thresholds, log message).

Pre-Checks: List initial checks to perform (e.g., check instance health, CPU/memory, logs, network connectivity).

Action Steps: Provide detailed steps (commands, scripts) to remediate: restart service, scale up, rollback, reconfigure.

Verification: After performing the action, define how to verify that the issue is resolved (health checks, metrics, logs).

Escalation Path: Describe who to escalate to if the issue is not resolved or if there are secondary failures. Include contact details, on-call rotations.

Rollback / Alternative Actions: If the primary action fails, describe fallback steps (rollback, failover, patch).

Post-Incident / Post-Mortem: Instructions for documenting the incident, root cause analysis, updates to the runbook, and lessons learned.

Safety Precautions: Warnings or caveats (e.g., “Don’t run this command on prod unless traffic is drained”, “Take backup before applying patch”).

Review & Update: Include a periodic review schedule to keep the runbook current.

**52. What is rollback vs “hotfix”?

Rollback: Reverting to a previous stable version of your application or infrastructure. This is typically used when a deployment fails or introduces unacceptable issues.

Hotfix: A small, off-cycle fix directly applied to production to patch a bug or security vulnerability. It’s usually more targeted than a full deployment, and may be applied urgently without going through the full normal release cycle.

Describe how you would handle a security vulnerability discovered in production automation pipeline.

Assessment: Quickly assess the severity, impact, and scope of the vulnerability.

Isolation / Mitigation: If possible, isolate the vulnerable component or disable the affected automation temporarily.

Patch or Fix: Develop or apply a fix (patch code, update script, rotate credentials).

Testing: Test the fix in a safe environment (staging / test) to ensure it does not break other automation flows.

Rollout: Deploy the fix via a controlled release (canary or limited rollout) or as a hotfix if urgent.

Validation: Run security tests, automated scans, runbooks, and monitoring to validate that vulnerability is resolved.

Secrets Rotation: If the vulnerability involves credentials / tokens, rotate them securely.

Post-Mortem: Document the incident, root cause, and preventive measures in a post-mortem.

Policy Update: Update security policy, documentation, and runbooks to prevent recurrence.

Communicate: Inform stakeholders (security team, dev, operations) about the fix, steps taken, and new safeguards.

**53. What is container image registry and how do you manage it in CI/CD?

A container image registry is a storage and distribution system for container images (e.g., Docker Hub, Amazon ECR, Google Container Registry).

Management in CI/CD:

Build the container image in the CI pipeline.

Tag the image appropriately (version, commit SHA).

Push the image to the registry from the pipeline.

Pull the image from registry in the deployment pipeline / orchestration (Kubernetes, etc).

Clean up / prune old images (automate deletion of unused/bad images).

Secure registry: enforce access control, image signing, and vulnerability scanning.

Use immutable tags (avoid latest in production), so you can roll back to a known image.

**54. How do you handle dependency management in an infrastructure / automation context?

IaC Modules / Packages: Use reusable modules (Terraform modules or Ansible roles) to encapsulate shared infra logic.

Version Pinning: Pin versions of modules, libraries, and tools to avoid unexpected breaking changes.

Dependency Files: Use dependency management (like requirements.txt for Python, go.mod, ansible-galaxy roles) to declare and manage versions.

CI Checks: In pipelines, validate dependencies (lint, security scan) before using them.

Regular Updates: Periodically review and upgrade dependencies in a controlled way (test in staging before prod).

Isolation: Use containerised environments or virtual environments to isolate dependencies.

Auditing: Maintain visibility over what dependencies are used where (via dependency graphs or manifest files).

**55. When would you choose an imperative vs declarative approach in infrastructure configuration?

Imperative: You explicitly define how things should be done — the steps to reach the desired state. Use this when:

Tasks are procedural and sequential (e.g., “run this script, then that”).

You have complex logic, conditional steps, or custom workflows that are easier to express in scripts.

Rapid prototyping, one-off jobs, or tasks not suited for IaC.

Declarative: You define what the desired state is, and the tool figures out how to achieve it. Use this when:

Using IaC tools like Terraform, CloudFormation, Ansible (in idempotent mode), Kubernetes manifests, etc.

You want reproducibility, version-controlled infrastructure, and drift detection.

You want to maintain state, perform reconciliation, and have a source-of-truth code for resources.

**56. Explain service discovery and why it matters in distributed systems.

Definition: Service discovery is the process by which services (microservices, APIs, etc.) in a distributed system dynamically locate and communicate with each other. Rather than hard-coding IP addresses or endpoints, services register themselves in a service registry, and other services query this registry to find available instances. 
GeeksforGeeks
+2
DEV Community
+2

Why it matters:

Dynamism: In a dynamic environment (containers, auto-scaling), instances come up and down. Service discovery handles this dynamically. 
Medium
+2
technoscriber.com
+2

Load Balancing & Fault Tolerance: Discovery systems often include health checks. Failed instances are removed, traffic is routed to healthy ones. 
GeeksforGeeks
+2
Medium
+2

Scalability: As your system scales horizontally, new instances register automatically, making scaling seamless. 
algomaster.io
+1

Decoupling: Services don’t need to know concrete addresses of other services. They use logical names, enabling more flexible architectures. 
Medium

Mechanisms:

Client-side discovery: Clients query registry, pick instance. 
GeeksforGeeks

Server-side discovery: A load balancer or proxy queries registry and routes requests. 
blog.algomaster.io
+1

Tools / Patterns: Service registries like Consul, etcd, Zookeeper, or using built-in discovery in container orchestration (e.g., Kubernetes DNS). 
Medium
+1

**56. What is an orchestration tool vs a configuration management tool?

Configuration Management (CM) tools: Focus on ensuring each machine or node is in a desired state. For example: which packages are installed, which services run, which config files are present. Tools: Ansible, Puppet, Chef. 
PHP China

Orchestration: Coordinates workflows across systems or services — managing dependencies, deployments, scaling, order of operations. It handles how and when things happen across many systems. 
Wikipedia

**57. How they complement each other:

Use orchestration to spin up or scale environments (e.g., create infrastructure, deploy services).

Then use configuration management to ensure each node is correctly configured and continues to maintain its desired state. 
PHP China

Example: Use Terraform or Kubernetes (orchestration) to deploy new instances, then Ansible (CM) to install software and configure these instances.

**58. How have you handled system updates or patching in an automated infrastructure?

A typical / best-practice approach:

Baseline & Inventory: Maintain infrastructure inventory via IaC (e.g., Terraform) + CM tool so you know what systems exist.

Automated Patching Pipeline:

Use configuration management (e.g., Ansible) to write playbooks for patching OS, applying security updates.

Use scheduling (cron / Jenkins / pipeline) to run patching during maintenance windows.

Testing: First apply patches to a staging / test group, validate that services work, run regression tests.

Health Checks & Monitoring: After patching, run automated health checks to ensure no service breaks.

Rollout Strategy:

Rolling updates: patch servers in small batches so not all go down at once.

Or use blue/green for critical systems: build a green environment with patched servers, test, then switch.

Rollback: If a patch causes a problem, have a rollback plan (e.g., undo configuration, restore snapshot).

Documentation: Maintain runbooks for patching, including steps, alerts, and rollback.

Audit & Reporting: Keep logs of patches applied, versions of patched systems, and provide reports.

**59. What is the importance of tagging/labeling resources (in cloud/on-prem) for cost / management / automation?

Cost management: Tags (like env:prod, team:dev, project:XYZ) allow you to attribute cloud costs to teams, projects, or cost centers. This helps in cost allocation and chargebacks. 
Aziro

Resource management: Tags help you identify what a resource is for (e.g., “web-server”, “db-server”), which environment it belongs to, who owns it. This improves clarity and governance.

Automation: Automation scripts / IaC templates can use tags to filter resources (e.g., “only patch resources tagged env=prod”), enforce policies, or apply configurations specifically.

Compliance & Governance: Tags can denote compliance, security zones, or lifecycle states (e.g., “to-be-archived”) — enabling automated policies.

Monitoring & Reporting: Tagged resources can be aggregated in dashboards (by project, team, cost, environment), making reporting easier and more meaningful.

**60. How do you monitor and report on infrastructure cost / usage in automated systems?

Cloud-native cost tools: Use cloud provider cost monitoring / billing dashboards (AWS Cost Explorer, Azure Cost Management, GCP Billing) to get visibility.

Tag-based allocation: As above, use tagging to group resources by cost center / team / project, and then pull cost reports by tags.

Automation: Build automated cost reporting pipelines (e.g., daily or weekly scripts that query cost APIs and generate reports).

FinOps practices: Adopt FinOps — cross-functional responsibility for cost optimization: set budgets, track usage, alert on overspend, enforce policies.

Alerts and Budgets: Set up budget thresholds and alerts in cloud billing tools to notify teams when spending is trending higher than expected.

Optimization: Use automation for rightsizing (scale-down underutilized resources), turning off non-prod environments during idle times, using reserved instances / spot instances where appropriate.

Dashboarding: Build dashboards (Grafana, cloud dashboards) to visualize cost vs usage, growth trends, projected usage.

**61. What happens when you hit API limits when automating with cloud provider SDKs?

Rate limiting: If you hit API rate limits, your automation calls may be throttled or rejected.

Retry logic: Implement exponential backoff + retry in your automation code to handle transient throttling.

Batching: Where possible, batch API calls instead of triggering many individual calls.

Caching: Cache metadata (e.g., instance lists) to reduce repeated API calls.

Paging / Pagination: Use paginated API responses to handle large data sets efficiently.

Request Quotas: Monitor usage / quota and request quota increases in the cloud provider console if needed.

Fallback Strategy: If the API is unavailable, have fallback or fallback automation paths (e.g., queue tasks, use local state).

Monitoring & Alerts: Instrument your automation to alert when API errors or rate limits are being hit, so you can proactively address.

What logging strategy would you use for microservices deployed via automated pipelines?

Centralized Logging: Use a centralized logging system (ELK stack: Elasticsearch, Logstash, Kibana) or managed services (Cloud Logging) to aggregate logs from all services.

Structured Logging: Log in a structured format (e.g., JSON) so logs can be parsed, filtered, and analyzed easily.

Correlation IDs: Use request IDs / correlation IDs to trace a single request across microservices.

Log Levels: Define log levels (INFO, DEBUG, WARN, ERROR) and use them appropriately; avoid flooding with DEBUG in production unless needed.

Retention and Archival: Set up log retention policies (how long logs are stored), archive old logs, and possibly compress / move them to cheaper storage.

Alerting: Build alerts on logs (e.g., error rate spikes, specific error patterns).

Access Control: Secure logs so that sensitive information (PII, credentials) is not exposed; control who can view or query logs.

**62. How do you handle secrets rotation in an automated system?

Secrets Manager: Use a centralized secrets store like HashiCorp Vault, AWS Secrets Manager, or Azure Key Vault.

Automated Rotation: Use automated rotation mechanisms — secrets rotate at defined intervals, and automation pipelines pull the latest versions.

Least Privilege Access: Limit who / which services can access which secrets. Use roles / policies.

Dynamic Secrets: Use dynamic secrets when possible (e.g., Vault can generate time-limited credentials).

Audit: Enable audit logging on secrets access and rotation operations.

Secure Injection: At runtime, inject secrets securely (e.g., via environment variables, or in-memory) rather than storing secrets in code or config.

Fallback / Rollback: Have a mechanism to roll back if a secrets change breaks something (e.g., pipeline fetches version, tests, then deploy).

**63. What is your approach to learning a new tool or technology for automation?

Identify Use Case First: Understand why you need the tool: what problem does it solve, what benefit does it bring.

Prototype / POC: Set up a small proof-of-concept; build a minimal pipeline / automation flow using the tool.

Documentation & Tutorials: Read official docs, follow tutorials, sample projects.

Hands-on Labs: Use sandbox / dev environment to experiment. Break things, fix things, run failure scenarios.

Community & Best Practices: Look at community examples, GitHub repos, blog posts, talks to learn how others design for production.

Integrate with Existing Stack: Try integrating the tool with your existing CI/CD or IaC pipelines to see real-world challenges.

Measure: Evaluate based on metrics: how much time it saves, how reliable it is, how maintainable.

Document & Share: After learning, document how you used it (runbooks, patterns), and share with the team (brown-bag sessions).

Iterate: Based on the POC, refine your approach: add error handling, testing, security, etc.

Automation Workflow / Infrastructure
**64. Describe an end-to-end automation workflow you designed (from code commit → build → test → deploy → monitor).

Here’s a sample (you can adjust to your real project):

Code Commit: Developer pushes application code + IaC (Terraform) to Git.

CI Build: Jenkins (or GitLab CI) pipeline triggers → build application → run unit tests → run terraform plan on IaC.

Integration Tests: Deploy application to a test / staging environment via CI pipeline. Run integration tests (API, UI) to validate.

Security / Compliance: Run vulnerability scan (SAST / container scanning) on artifact.

Deployment: If tests pass, deploy to production using a deployment strategy (e.g., canary or blue/green) orchestrated via Terraform + Kubernetes (or other orchestration).

Verification: Run smoke tests post-deployment, health checks, automated validation.

Monitoring & Logging: Once deployed, metrics (CPU, memory, latency) are collected via Prometheus / CloudWatch; logs are shipped to ELK / logging service.

Alerting & Dashboard: Dashboards in Grafana; alerts on error rate, latency, resource saturation.

Runbook / Recovery: If there’s a failure, runbook steps are triggered — rollback, scale up, or hotfix.

Feedback Loop: Use deployment metrics (failure rate, lead time) to improve pipeline, optimize tests, and refine process.

**65. How did you gather requirements for an automation project – what questions did you ask stakeholders?

To gather requirements:

What are the pain points? Which tasks are currently manual, repetitive, or error-prone?

What business / operations goals should the automation support (e.g., reduce downtime, increase deployment frequency, reduce cost)?

What are the non-functional requirements (SLAs, performance, security, compliance)?

Which environments need automation (dev, test, staging, prod)? Are there different levels of risk in each?

What deployment strategy is acceptable (blue/green, canary, rolling)?

Do we need rollback / recovery capabilities? What are the rollback criteria?

What monitoring, logging, and alerting do stakeholders want post-deployment?

Who will own the automation (Dev, Ops, SRE)? Who will maintain runbooks, scripts?

What is the frequency of change? How often do we anticipate updates?

What secrets or credentials will the pipeline need? How should they be managed and rotated?

Is there a budget or cost constraint? Should infrastructure scaling be optimized?

Are there regulatory or compliance constraints (audit logging, encryption)?

What rollback or error scenarios do stakeholders consider most critical?

What role-based access / permissions are needed (who can trigger deployments, who can approve, etc.)?

How would you automate infrastructure configuration for both on-premise and cloud-based environments?

Use IaC tools that support both environments (e.g., Terraform, Ansible) to define infrastructure in code.

Create modular templates / playbooks: modules for cloud resources (VMs, networking) and modules for on-prem (bare-metal, VMs, local networks).

Use inventory abstraction: maintain dynamic inventory in Ansible for both cloud and on-prem, so playbooks run transparently.

Use configuration management (e.g., Ansible) to configure both on-prem servers and cloud servers consistently (installing software, setting config).

Use provisioning pipelines: pipelines that detect whether target is cloud or on-prem and run proper IaC + config tasks.

Integrate secrets management and credentials for both environments in a unified way (Vault or secrets manager).

Use monitoring / logging that aggregates from both on-prem and cloud into a central system.

Test on both types of infrastructure (dev-on-prem, dev-cloud) to validate that automation works in both contexts.

Maintain documentation and runbooks specific to each environment but using the same logical structure.

What are the challenges of automating hybrid on-prem + cloud infrastructure, and how do you address them?

Differences in API / Capabilities: On-prem may not have cloud-style APIs; you might need different tools or scripts. → Solution: Use abstraction in IaC and modular code to isolate cloud-specific vs on-prem logic.

Network Connectivity & Security: On-prem may have different security, network architecture, firewalls. → Solution: Define secure networking modules, VPN / direct connect, firewalls in IaC.

Credential Management: Managing secrets for both environments. → Solution: Use centralized secrets store with controlled access.

Compliance / Governance Differences: On-prem may have stricter controls; cloud may have different compliance posture. → Solution: Use policy-as-code, tagging, and governance automation.

Tooling Mismatch: Some tools are cloud-native and may not work on-prem; others may not support dynamic features. → Solution: Choose tools (like Ansible, Terraform) that support both or use a hybrid toolset.

Resource Scaling: Cloud scales easily, on-prem has capacity constraints. → Solution: Plan capacity, autoscaling in cloud, and reserve capacity / use virtualization on-prem.

Visibility & Monitoring: Monitoring on-prem and cloud might require different solutions. → Solution: Use unified monitoring (Prometheus, ELK, or central logging) that supports both.

State Management: Keeping track of infrastructure state across both worlds. → Solution: Use IaC with remote state backends and locking (e.g., Terraform remote state) so teams don’t conflict.

Describe how you would implement a CI/CD pipeline that deploys both infrastructure and application code.

Repository Structure:

infra/ folder for IaC (Terraform, CloudFormation)

app/ folder for application code

Shared pipeline config (Jenkinsfile / GitLab CI YAML)

Pipeline Stages:

Lint / Validate: Validate IaC (terraform fmt/validate) and app code (lint, static analysis)

Plan / Build:

IaC: terraform plan to preview infrastructure changes

App: build artifact (jar, container image)

Test:

IaC: optionally deploy to test sandbox and run terraform apply in a staging workspace

App: run unit tests, integration tests

Infra Deployment: If plan is OK, apply IaC to create/update infrastructure (staging or prod)

App Deployment: Deploy app artifact to target environment (VMs, containers) on the infrastructure just created or updated

Validation: Run smoke tests, health checks, perhaps canary rollout

Monitoring & Alerts: Once deployed, enable monitoring of deployed resources / app, gather metrics

Approval / Promotion: For production, include manual approval gates if needed

Rollback: If anything fails, run rollback steps (IaC rollback or destroy + recreate, or version revert for app)

Notification: Notify teams of pipeline status (success / failure) via Slack / email

Secrets & Credentials: Use secrets manager in pipeline to inject credentials securely (e.g., cloud API keys, DB credentials).

State Management: Use a remote state backend for IaC (Terraform) so team members don’t conflict and state is consistent.

Versioning & Tagging: Tag app artifacts (git commit, version) and infrastructure (terraform module versions), so deployments are traceable and repeatable.

How do you handle secrets and credentials across the pipeline, including production?

Use a central secrets store (Vault, Secrets Manager) to store credentials.

In CI/CD pipeline, fetch secrets at runtime (not store in plain text).

Use least-privilege IAM roles / permissions to access secrets.

Implement secret versioning and rotation: use the latest version of secrets, rotate periodically or on schedule.

Log access: pipeline should log when secrets are accessed, for audit.

For production: use environment-specific secrets, separate staging vs prod credentials, and inject securely.

Use secure variables / secret injection features of CI tools (e.g., GitLab CI masked variables, Jenkins credentials plugin).

Explain how you would use Ansible (or another CM tool) to provision servers, install application code, and deploy configuration changes.

Inventory Management: Define inventory (hosts) — either static (INI, YAML) or dynamic (cloud-based, via API).

Playbook / Roles: Create Ansible roles for:

Provisioning: Create users, set up SSH, base OS config

Application Deployment: Copy application code, configure service, start/stop service

Configuration: Apply config files, templates (e.g., using Jinja2) for app config, system config

Idempotency: Ensure tasks are idempotent (run multiple times without unintended changes).

Secrets: Use Ansible Vault to encrypt secrets (e.g., DB credentials, API keys) so that they are not plain in playbooks. 
Wikipedia

Execution: Run playbooks via CI pipeline or Ansible Tower / AWX.

Validation / Health Checks: After deployment tasks, run checks (e.g., service is up, response check) inside playbook.

Rollback / Versioning: Use tags or versioned roles; have tasks to revert config or redeploy previous version if needed.

Monitoring: Optionally, at end of playbook, trigger monitoring alerts or report to monitoring system.

How do you manage state in Terraform when multiple team members are working on the same infrastructure?

Use a remote state backend (e.g., Terraform Cloud, S3 + DynamoDB for locking, or GCS) so state is stored centrally and not on local machines.

Enable state locking: prevent concurrent terraform apply or terraform plan from corrupting state.

Use workspaces or environments: separate state for dev, staging, production.

Use version control: keep Terraform code in Git, with pull requests and code review.

Use state versioning / snapshots: maintain backups of state so you can roll back if something breaks.

Use state modules: break infrastructure into logical modules to reduce conflicts and make independent changes safer.

Define policy checks / guards before state change (CI pipeline terraform plan → review → apply).

What strategies do you use to avoid drift after deployment (especially when teams make manual changes)?

Enforce IaC as source of truth: All provisioning and configuration changes must go through IaC / automation.

Periodic reconciliation: Run automation (CM) periodically (e.g., daily) to re-apply desired state.

Drift detection tools: Use tools that detect drift (e.g., Terraform plan refresh, driftctl) and alert or remediate.

Access controls: Limit manual access to infrastructure (via console or SSH), enforce permissions, and require change via automation.

Policy-as-code: Use policies (with tools like OPA) to prevent unauthorized configurations.

Audit and logging: Log all configuration changes (manual or automated). Review drift events in runbooks.

Documentation & Training: Educate teams about the importance of not making manual changes, and how to use the automated process.

How do you monitor the efficiency of your automated systems (e.g., pipeline times, failure rates)?

Pipeline Metrics: Track metrics like build time, test time, deployment time, and the trend over time.

Failure Rates: Measure how often builds or deployments fail. Calculate change failure rate.

Lead Time for Changes: How long does it take from commit to production deployment?

Recovery / Rollback Time: Mean Time to Recovery (MTTR) — how quickly do you recover after a failure.

Success Rate of Automation Tasks: For automated operational tasks (patching, scaling), track how often they succeed vs fail.

Resource Utilization: For the infrastructure that automation spins up / manages, monitor CPU, memory, auto-scaling behavior, cost.

Alert Volume: Number of alerts triggered during or after deployment (could indicate unstable automation).

Throughput: Number of deployments per day/week/month — are you increasing deployment velocity?

Quality Metrics: After deployment, monitor error rates, failure in production, performance regressions.

Feedback & Post-Mortems: After incidents, evaluate root cause (was it automation issue, test gap, or environment issue) and refine pipeline accordingly.

1. Explain how you would set up rollback mechanisms in a Kubernetes-based deployment.

Use Kubernetes Deployment revision history: When you deploy using a Deployment, Kubernetes stores previous ReplicaSets. You can run kubectl rollout undo deployment/<name> to rollback to a prior version. 
cnpl.io
+1

Use Blue/Green deployment: Maintain two deployments (blue = current, green = new). When green is ready and validated, switch traffic via a Service. If something goes wrong, switch back. 
nirmalnaveen.com

Use Canary deployment: Gradually shift a small percentage of traffic to the new version. Monitor for errors; if they escalate, rollback (or pause) before full rollout. 
cnpl.io

Automate health checks: Before shifting traffic, have pre-traffic health probes. After switching, run post-traffic validation; if problems show up, automate rollback or cut traffic back.

CI/CD integration: In your pipeline, after applying a new version, run kubectl rollout status to monitor progression. If status fails or timeout, trigger a kubectl rollout undo. 
Reddit
+1

Use GitOps: If you manage your cluster via GitOps (e.g., ArgoCD, Flux), you can revert the Git commit to a previous manifest state, and let the operator apply that (effectively rolling back). 
Reddit

2. How do you ensure your Kubernetes cluster is resilient and fault-tolerant?

High-Availability Control Plane: Use multiple control-plane (master) nodes (e.g., 3+) so you can tolerate loss of one. 
Tigera - Creator of Calico
+1

Distributed etcd: Use an external or multi-node etcd cluster so that data store isn’t a single point of failure. 
Tigera - Creator of Calico

Pod Replicas & Auto-scaling: Deploy multiple replicas for each microservice so that pod failure doesn’t bring the service down; use autoscaling for load. 
Komodor

Pod Disruption Budgets (PDBs): Define PDBs to limit how many pods can be voluntarily disrupted (e.g., during maintenance), ensuring certain minimum are always running. 
Komodor

Topology Spread / Anti-Affinity: Use topology constraints so pods are spread across failure domains / nodes, avoiding single-node or single-zone failure. 
Komodor

Network Policies: Restrict east-west traffic, enforce least-privilege communication, isolate components.

Regular Backups: Backup etcd regularly; automate snapshot integrity checks. 
Tigera - Creator of Calico

Chaos Testing: Use tools like Chaos Mesh or LitmusChaos to simulate failures and verify resilience proactively. 
WafaTech

3. Describe how you would design an automated deployment for a microservices architecture with minimal downtime.

Use a canary or blue/green strategy (as above) to reduce risk.

Maintain separate Deployment objects for each microservice in Kubernetes.

Use CI/CD pipeline that:

Builds container images for each microservice

Pushes to a container registry with versioned tags

Deploys to a staging / pre-prod cluster for smoke tests

Runs integration tests (API contracts, e2e)

Deploys to production progressively (canary) or via blue/green

Validates via health checks / synthetic requests

Shifts traffic only when new versions are verified

Monitors logs and metrics, and triggers rollback if anomalies (error rate, latency) occur

Use feature flags when possible so that new functionality can be toggled on/off without total redeploy.

Automate database migrations carefully (see next answer) to avoid compatibility issues.

Maintain runbooks and automated rollback logic so that in case of failure, recovery is quick and reliable.

4. How would you handle database schema changes (migrations) in a CI/CD pipeline?

Use backward-compatible migrations: Design schema changes such that older and newer versions of the service can run against both old & new schema (e.g., add columns, don’t drop).

Use a migration job: Run migrations via a Kubernetes Job or a pre-deployment hook (Helm pre-upgrade hook) before deploying the new version.

Use migration tools: Liquibase, Flyway, or ORM-based migrations.

In the pipeline:

First run migration job in a staging / test environment

Verify migrations are successful (run smoke tests / liveness)

Deploy the application version that depends on the new schema

For production: you may run migration in a controlled window (maintenance period) or use canary rollout of database + app

Maintain rollback plan: For dangerous migrations (dropping columns), have a rollback strategy (e.g., backup data, run reverse migration) — but ideally, schema changes are non-destructive first.

In some setups, don’t fully automate production migration — require a manual gate if risk is high. Real-world practitioners sometimes run migrations manually or semi-automatically. 
Reddit

5. What logging & monitoring architecture would you set up for a distributed microservices environment?

Centralized Logging: Use ELK stack (Elasticsearch, Logstash, Kibana) or managed solution (e.g., cloud logging) to aggregate logs from all microservice pods.

Structured Logging: Have your application logs in structured format (JSON) so you can query, filter, and correlate easily.

Correlation / Tracing: Use correlation IDs (e.g., request IDs) so that you can stitch logs across microservices. Optionally use distributed tracing (Jaeger, Zipkin) for request paths.

Metrics / Monitoring: Use Prometheus for metrics (latency, error rate, request count, resource usage), Grafana for dashboards.

Alerts: Set up alerting on key metrics (error rate spikes, latency degradation, resource saturation).

Health Checks: Use liveness & readiness probes in Kubernetes; expose health endpoints in microservices.

Log Retention & Archival: Define log retention policies; archive older logs to cheaper storage if needed.

Access Control: Secure and control access to logs (RBAC for Kibana or logging console) so sensitive data is not exposed.

6. Describe how you wrote a script that automatically fixed a repeated operational task (ex: cleanup, scaling, patching).

Sample Answer (you can adapt):
In my previous role, we had a problem where old Docker images and unused Kubernetes resources (like stale PVCs) accumulated over time. I wrote a Python script that:

Lists all images in our registry and compares with images currently running on clusters.

Finds unused (or old) image tags based on retention policy (e.g., older than 30 days or not used in any running pods).

Uses the container registry API to delete those images (taking care of registry quotas).

In the Kubernetes cluster, lists PersistentVolumeClaims (PVCs) with no bound or no associated pod, and deletes them after a safety check.

Sends a daily summary report via Slack / email with details of what was removed and any failures.
This automation reduced manual cleanup tasks from hours to zero, prevented buildup of unused data, and reduced storage cost.

7. How would you decide whether to automate a particular operational task? What are the trade-offs?

Decide based on Frequency: If a task is done often (daily / weekly), automation pays off. For very rare tasks, manual might be fine.

Complexity and Risk: Highly risky tasks (like patching or DB migration) need careful automation + rollback. If risk is high and manual intervention is needed, automation should include safety checks.

ROI: Evaluate the time / cost saved, risk reduction, and error rate improvement.

Stability: If the workflow is stable (not changing much), automation is more beneficial; if it's very ad-hoc, you may wait.

Maintenance Overhead: Automation itself must be maintained; building automation for a task might introduce technical debt if not designed well.

Visibility and Audit: Automated tasks provide logs, audit trails, and reproducibility; manual tasks may lack that.

Trade-offs:

Automation cost vs benefit: Time to build + test automation vs the time saved.

Risk of automation bugs: An automated script could have a bug that causes damage faster than a manual error.

Flexibility: Manual operations can adapt to edge cases; automation might struggle unless well-parameterized.

I typically run a small POC, estimate cost & risk, and then decide whether to fully automate and integrate into the CI / operations pipeline.

8. Describe a time when your automation failed — what happened, how you debugged, what you learnt?

Sample Answer (example):
In a previous role, I built an automation pipeline to scale up a service based on CPU usage. I wrote a script that watched CPU metrics and triggered a Kubernetes HorizontalPodAutoscaler scale-up via kubectl commands. However, during a load test, the automation triggered too aggressively, scaling out to too many pods and overshooting our quota, which caused resource exhaustion and degraded performance.
Debugging: I looked at Prometheus metrics, logs from the autoscaler script, and Kubernetes events. I realized my scaling thresholds were too low (> 50% CPU sustained for 30 s), and the script had no rate-limiter.
Fix: I introduced a debounce mechanism (only scale if CPU > threshold for a continuous window), rate-limited scale events, and capped the maximum number of replicas. I added logging and alerting (if scaling actions exceed a certain limit) and tested in staging.
Learning: Automation needs safeguards — rate limits, throttling, and good observability. I also added runbook steps for manual override and alert escalation in case of runaway scaling.

9. How would you secure a Kubernetes cluster (RBAC, network policies, pod security policies)?

RBAC (Role-Based Access Control): Define granular roles for users, service accounts, and namespaces. Give only minimal privileges.

Network Policies: Use Kubernetes NetworkPolicies (or CNI with policy support like Calico) to restrict traffic between pods/namespaces — e.g., only allow pods in a namespace to talk to specific services.

Pod Security / Admission Controls: Use Pod Security Policies (or the newer Pod Security Admission) to enforce constraints (e.g., disallow privileged containers, restrict hostPath, enforce seccomp/memory limits).

TLS / mTLS: Use mutual TLS between services (via service mesh or manually) to secure pod-to-pod communication.

Secrets Management: Don’t bake secrets into container images — use Kubernetes Secrets or external secrets stores, and mount them securely.

Audit Logging: Enable Kubernetes audit logging to track who did what in the cluster.

Image Security: Use image scanning (vulnerability scan) before deployment; restrict images to trusted registries.

Pod Security Contexts: Define runAsNonRoot, readOnlyRootFilesystem, resource limits for pods.

Regular Updates: Keep control-plane and worker nodes patched. Use secure node provisioning, restrict SSH access.

10. Explain how you integrate multiple teams (developers, operations, QA) into the automation workflow.

Shared CI/CD Pipelines: Use a common pipeline repo (or monorepo) that all teams contribute to (microservices, infrastructure) so pipelines are standard.

Collaboration in Design: Conduct requirement-gathering workshops involving dev, ops, and QA to design automation workflows (deploy, rollback, monitoring).

Automated Testing Layers: Include unit tests, integration tests, and end-to-end tests in the pipeline; QA should own / write regression suites.

Gates & Approvals: Use manual approval gates in CI/CD (for production) where QA or operations must approve before deployment.

Runbooks & Training: Document automation workflows, runbooks, and share with all teams. Conduct sessions / demos.

Feedback Loop: After deployment, capture metrics (failure rate, MTTR, incidents) and review with all teams in retrospectives. Use feedback to improve pipelines.

Cross-Functional Roles: Assign DevOps champions in each team; encourage peer review on IaC, pipeline scripts, automation code.

11. How do you maintain documentation of your automation solutions, workflows and runbooks so that others can follow / operate them?

Keep documentation versioned in Git alongside code (in the same repo if possible) so it evolves with the automation.

Use markdown or structured text (or a wiki) for runbooks, architecture diagrams, workflows.

Define templates for runbooks: include sections like “pre-checks”, “commands to run”, “validation”, “rollback”, “escalation”.

Automate generation of runbook artifacts where possible (for example, from pipeline definitions or IaC code).

Regularly review and update documentation: after each deployment, incident, or change, run a documentation review to update runbooks.

Organize knowledge sharing: hold brown-bag sessions, runbook training for on-call / support teams.

Make documentation easily accessible: store in centralized place (GitLab / Confluence / shared repo) with appropriate permissions for edit / read.

12. What is the difference between declarative and imperative for provisioning and configuration? Give examples.

Imperative: You specify how to do something step-by-step (commands). For example, a script that says: “create VM, install package A, copy files, start service.”

Declarative: You specify what the desired state should be, and the system figures out how to reach that state. For example, a Kubernetes Deployment manifest or Terraform file that says “3 replicas of this container image,” and Kubernetes / Terraform ensures that the state matches.

Example:

Imperative: kubectl run nginx --image=nginx:1.21 → then kubectl scale deployment nginx --replicas=3

Declarative: A deployment.yaml file:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 3
  template:
    spec:
      containers:
      - name: nginx
        image: nginx:1.21


When you kubectl apply -f deployment.yaml, Kubernetes reconciles to that state.

13. Explain the concept of “infrastructure testing” (unit tests, integration tests for infrastructure).

Infrastructure testing means treating your IaC like application code — you write tests to validate that your infrastructure definitions work correctly, don’t produce unintended changes, and meet requirements.

Types:

Unit tests: Test small modules of IaC (for example, a Terraform module) in isolation. Use tools like Terratest to spin up resources in a test environment and validate properties.

Integration tests: Deploy a more complete stack (network, VPC, servers) in a sandbox, then validate connectivity, resource configuration, security groups, IAM, etc.

Policy tests / compliance tests: Use policy-as-code (e.g., Open Policy Agent) to enforce that your infrastructure meets security or organizational rules.

Drift tests: After infrastructure is applied, run drift detection (e.g., terraform plan / refresh) to verify no manual changes have diverged.

This reduces risk, catches misconfigurations early, ensures reproducible, testable infrastructure.

14. How would you implement unit testing or verification for infrastructure code before deployment?

Use Terratest (or similar) to write Go / Python tests that: spin up a small infrastructure component, check that it was created correctly, and tear it down.

Use terraform validate and terraform fmt in CI to check syntax, formatting, and basic structural correctness.

After plan, run terraform plan in a "check" mode (plan -out=plan.out), then parse the plan for unexpected changes (e.g., resource deletions).

Use policy-as-code (OPA, Terraform Sentinel) to enforce rules (no public S3 bucket, tagging, encryption) as part of CI pipeline.

Use a staging / ephemeral environment: apply the IaC in a non-prod environment, run tests (connectivity, resource count, configurations), then destroy.

Integrate into CI/CD pipeline: fail the pipeline if tests don't pass, plan shows dangerous changes, or policy is violated.

15. What is a “canary release” and how would you implement one using automation?

A canary release is a deployment strategy where you roll out a new version to a small subset of users or infrastructure first, monitor behavior, and then gradually increase percentage / footprint if stable.

Implementation in Kubernetes:

Create a Deployment for the new version (canary) with fewer replicas.

Use maxSurge / maxUnavailable in your Deployment strategy to control rollout.

Use service mesh (Istio) or traffic controller (Flagger) to shift a small percentage of traffic to the canary pods.

Monitor key metrics (latency, error rate, resource usage) for canary pods.

If metrics are healthy, automate further rollout (increase traffic or replicas) to full. Otherwise, rollback.

Use CI/CD pipeline that supports traffic splitting, validation, and rollback.

16. How would you perform capacity planning for your automated infrastructure?

Use historical metrics: Analyze metrics (CPU, memory, request load) from monitoring (Prometheus, Grafana) to understand usage patterns.

Autoscaling policies: Define Horizontal Pod Autoscaler (HPA) for microservices and cluster autoscaler for nodes, based on observed load.

Peak planning: Estimate peak load scenarios (traffic surges, seasonal spikes) and model required capacity.

Buffer / headroom: Maintain buffer capacity (some spare nodes) for resilience and unexpected load.

Cost vs performance trade-off: Evaluate cost of over-provisioning vs risk of under-provisioning; decide on acceptable risk.

Forecasting: Use trend analysis to project future growth, then automate scale-up of infrastructure ahead of demand.

Load testing: Perform load tests to validate that your planned capacity can handle expected / worst-case load.

Review & Iteration: Regularly revisit capacity plans based on usage, performance, and cost data; adjust autoscaling rules accordingly.

17. Explain how you would integrate security scanning (SAST / DAST) into your CI/CD pipeline.

SAST (Static Application Security Testing): Integrate SAST tools into the build stage of the CI pipeline to scan source code (e.g., SonarQube, Checkmarx, Snyk) for vulnerabilities, code smells, and security issues.

Container Scanning: After building a container image, scan it for vulnerabilities (using tools like Trivy, Clair) before pushing to registry.

DAST (Dynamic Application Security Testing): In the pipeline’s test stage, deploy to a staging environment, then run DAST tools (e.g., OWASP ZAP) to simulate attacks against running application.

Infrastructure Security: Use infrastructure-as-code security scanning (e.g., terraform validate, policy-as-code) to detect misconfigured or insecure resources.

Gating: Fail the pipeline if critical security vulnerabilities are found, or require manual approval.

Policy / Compliance: Enforce security policy through code; use policy-as-code to ensure only compliant resources are deployed.

Continuous Monitoring: Even after deployment, keep scanning in production (container security, runtime protection) and feed results back to development.

18. Describe handling a zero-downtime deployment for a web application with high traffic.

Use Blue/Green or Canary deployment strategy in Kubernetes.

Use readiness and liveness probes: New pods should only receive traffic once their readiness probe passes.

Use service mesh or traffic routing: Shift traffic gradually (canary) or switch after green is tested.

Use database migration strategy: Use backward-compatible migrations; run migration jobs before switching traffic; ensure that old and new code can run with both old and new schema.

Use feature flags: Deploy new features behind flags so you can enable them when ready without a full redeploy.

Use pod disruption budgets (PDBs): Ensure that during deployment, a minimum number of pods stay running so you don’t knock out service. 
Komodor

Monitor during rollout: Use metrics, logs, health checks during and after cutover; if problems, rollback or stop rollout.

Automate rollback logic in pipeline or operator (e.g., if error rate exceeds threshold, revert to previous version).

19. How would you measure & improve the deployment frequency and lead time for changes in your team?

Metrics to track:

Lead Time for Changes: Time between code commit and production deployment.

Deployment Frequency: How many deployments per day/week/month.

Change Failure Rate: Percentage of deployments that lead to failures or rollbacks.

Mean Time to Recovery (MTTR): Time taken to recover from a failure.

Time in CI / Pipeline Duration: Build + test + deploy times.

Improvement Strategies:

Automate more pipeline steps (parallelize tests, caching, artifact reuse).

Reduce bottlenecks (slow tests, long reviews, manual gates) by refining tests, implementing fast feedback.

Introduce smaller, more frequent releases (micro-batches) to reduce risk and lead time.

Use feature flags or canary deployments to decouple code merge from feature release.

Conduct regular retrospectives to identify pipeline pain points and make improvements.

Provide feedback to developers: give metrics about how long their changes take to go live; encourage practices that shorten lead time.

20. Explain how you might architect a multi-region deployment with automated fail-over.

Deploy Kubernetes clusters in multiple regions (or zones) to host redundant services.

Use global load balancing / DNS-based routing to send traffic to the closest / healthiest region (e.g., via a global load balancer or DNS with health checks).

Use state replication: For databases, use multi-region replication (or geo-replicated managed DB) to ensure data is available in failover region.

Use infrastructure as code (IaC) to define clusters, networking, failover configurations, routing policies.

Use CI/CD pipelines that can deploy to all regions in a coordinated way.

Implement health checks / monitoring per region, and define automated failover logic in case a region goes down (e.g., shift traffic to secondary region).

Use backups and disaster recovery: frequent backups, cross-region backups, and test restore procedures.

Ensure config consistency: use GitOps or centralized config so infrastructure and application are consistent across regions.

Use service mesh / gateway: to handle inter-region service communication, and API gateways for entry-point traffic management.

21. How do you handle versioning of container images and rolling back to a previous version?

Use semantic version tags or commit-SHA tags when building container images.

Store images in a container registry (Docker Hub, ECR, GCR) with immutable tags for production.

In deployment manifests (Kubernetes), reference image versions by tag / SHA, not latest.

For rollback: when a deployment fails or a canary shows issues, update the Deployment to point to the previous version tag and apply.

Optionally, use GitOps or Helm: revert the Git / Helm chart version to a stable release, then let the operator rollout that version.

Automate rollback in CI/CD: if rollout fails or health checks / metrics degrade, pipeline triggers a rollback to prior image version.

22. Explain how you would debug a pipeline with intermittent failures and nondeterministic behavior.

Add Logging / Traceability: Improve logging in pipeline steps — capture detailed logs (stdout, stderr), timestamps, and context.

Record Pipeline State: Use --record in Kubernetes deployments so rollout history is recorded and you can inspect what exactly changed. 
kumorilabs.com

Retry & Back-off: Add retry logic for flaky steps (e.g., API calls, network operations) with exponential back-off.

Isolate & Reproduce: Try to reproduce the failure in a similar environment (sandbox or staging) to isolate if it's an environment issue or code issue.

Instrumentation / Metrics: Emit pipeline metrics (step duration, failure counts) and correlate failures with time / commit / environment.

Use Canary / Rollout Tools: Use deployment tools (Argo Rollouts, Flagger) that provide detailed rollout steps, pauses, and canary promotions; inspect rollout history.

Parallel Runs: Run parallel pipeline runs to see if failures are tied to concurrency or overlapping runs.

Version Pinning: Ensure pipeline dependencies are pinned; nondeterminism can arise from dependency version changes.

Post-Mortem: After each failure, conduct a root-cause analysis, document findings, and patch the pipeline (add tests, retries, safety checks).

23. Describe your approach to monitoring performance bottlenecks in production automation workflows.

Instrument your pipeline / automation tool to emit metrics: execution times, errors, queue times, throughput.

Use a metrics store (like Prometheus) to collect these metrics over time.

Build dashboards (Grafana) showing pipeline latency, success vs failure, time spent in each stage.

Set alerts on anomalies: if a stage’s duration suddenly increases (say 2× typical); or failure rate spikes.

Do periodic pipeline performance reviews: analyse which stages are slowest, where bottlenecks are recurring.

Refactor: optimize slow stages — e.g., cache dependencies, parallelize tests, break monolithic steps into smaller ones.

Run load tests on pipeline: simulate many concurrent runs to see how performance degrades / where capacity is insufficient.

Capture pipeline logs and correlate failures / slowdowns with external infrastructure events (network outage, API rate limits) to identify systemic causes.

24. How do you keep your automation code modular, reusable, and maintainable across teams?

Structure your code into modules / reusable components: for example, Terraform modules, Helm charts, Kubernetes manifests, shared libraries.

Use versioning for modules, so teams can depend on stable versions and upgrade in a controlled manner.

Enforce coding standards / linting: use linters, configuration checks for IaC, YAML, scripts.

Use documentation: each module should have README, usage examples, parameter descriptions, versioning notes.

Use CI pipelines to validate modules: test that modules render correctly, pass validation, don’t produce breaking changes.

Encourage code review: all IaC / automation changes should go through reviews so teams maintain quality and shared knowledge.

Provide templates: boilerplate module templates or scaffold generators so new teams can start consistent code.

Maintain a module registry or shared repo: a place where teams publish and share modules.

Regular refactoring: schedule periodic cleanup, deprecation of old modules, and refactoring based on usage / feedback.

25. What metrics would you present to leadership to show the value of automation you implemented?

Deployment Frequency: How often we deploy (daily / weekly) vs before automation.

Lead Time for Changes: Time from commit → production.

Mean Time to Recovery (MTTR): How quickly we recover from deployment failures.

Change Failure Rate: Percentage of deployments that result in rollback or incidents.

Manual Effort Saved: Estimate hours saved per week/month because of automation (e.g., tasks automated, outages avoided).

Operational Cost Savings: Reduced cloud or compute costs due to autoscaling, cleanup, optimization.

Infrastructure Stability: Number of incidents / outages before vs after automation, or reduction in configuration drift.

Error Rate / Incident Count: Reduction in manual errors, misconfigurations, or post-deploy bugs due to automated validation.

ROI: Ratio of time (or money) saved to cost invested in automation (tooling, effort).

On-call Burden: Reduction in after-hours incidents, reduced manual on-call load, faster incident resolution.

26. Explain how you would manage secrets across multiple environments (dev, QA, prod) and across clouds.

Use a centralized secrets management system (HashiCorp Vault, AWS Secrets Manager, Azure Key Vault) to store secrets securely.

Define environment-specific scopes: store separate secrets for dev, QA, and prod (not reusing prod secrets in dev).

Use role-based access: assign access to secrets only to service accounts or IAM roles that need them, segregated by environment.

Use versioning and rotation: automatically rotate secrets periodically (or on-demand) and keep versions to allow rollback if needed.

Use dynamic secrets (if supported): for example, Vault can generate database credentials at runtime.

For cross-cloud: use the same secrets store (if possible) or replicate secrets securely via automation; or use cloud-native secrets stores but sync secrets via a secure CI pipeline.

Secure injection: inject secrets into pods / pipelines at runtime (e.g., via environment variables, Kubernetes Secrets) rather than hard-coding.

Audit: enable audit logs on secrets access, monitor usage, and alert on suspicious access.

27. How do you define and enforce configuration standards across the infrastructure you manage?

Use policy-as-code tools (like Open Policy Agent / OPA) to define allowed configurations, enforce guardrails (e.g., no public S3 buckets, encryption enabled, resource tagging).

Write baseline IaC modules / templates that adhere to organizational standards (networking, naming, tagging, security).

Use CI / pipeline validation: integrate terraform validate, linting, policy checks, compliance tests into CI.

Use code reviews: ensure all Infrastructure-as-Code changes go through peer review, checking for compliance with standards.

Maintain documentation / style guide: have a shared guide for naming conventions, resource tags, best practices, module usage.

Automate drift detection: periodically identify non-compliant resources and remediate or alert.

Training: run internal workshops / knowledge-sharing so teams understand and adopt standard practices.

28. Describe how you worked with an offshore vendor or remote team in delivering automation solutions.

Sample Answer:
In a previous project, we collaborated with an offshore DevOps team to build our infrastructure automation. We did the following:

Kickoff & Alignment: Held a detailed kickoff with stakeholders (onshore + offshore) to align on architecture, tools (Terraform, Kubernetes), coding standards, and delivery timelines.

Shared Repositories: We used a shared Git repository for IaC and pipeline code; all work was done via feature branches and pull requests.

Regular Syncs: Weekly video calls to review progress, demo new automation, resolve blockers, and get feedback.

Code Review Process: Both teams participated in code reviews; we defined review checklists (style, security, compliance).

Documentation: We maintained runbooks, style guides, and architecture diagrams in a shared wiki. Offshore team contributed to documentation too.

CI Pipeline: We set up a CI pipeline that ran tests, terraform plan, linting, and policy checks. Offshore team could validate their changes in this pipeline.

Knowledge Transfer: We did knowledge-sharing sessions (brown-bags) where offshore team taught us their modules, and we taught them production practices.

Feedback Loop: After each sprint, we had retrospective sessions to improve collaboration, clarify responsibilities, and refine processes.

29. How do you align automation workflows with business priorities and deadlines?

Requirement Gathering: Work closely with business stakeholders to understand key initiatives, what automation can drive (cost saving, uptime, faster releases).

Prioritization: Prioritize automation tasks based on ROI, risk, alignment with business goals (e.g., automating a deployment pipeline might be higher priority than cleaning up logs).

Roadmap: Build a roadmap for automation initiatives aligned with business release planning, major product goals, or operations strategy.

Incremental Delivery: Deliver automation in incremental phases (MVP first, then enhancements) so business can start realizing value early.

Measure & Report: Use metrics (deployment frequency, failure rates, time saved) and report to business on how automation is impacting business goals.

Regular Syncs: Have cross-functional sync meetings (DevOps, Engineering, Product) to ensure automation backlog stays aligned to business roadmap.

Governance & Change Control: Use change approval processes that map automation changes to business impact; involve stakeholders for high-risk automation.

30. How do you escalate issues or risks when automation fails or doesn’t meet SLAs?

Define Escalation Paths: Before deployment, define and document escalation procedures: who to contact (on-call, SRE, lead), severity levels, communication channels.

Real-Time Monitoring: Have alerts set up for automation failures (pipeline errors, rollback, health check failures) so issues are detected immediately.

Runbooks: Use runbooks that include escalation steps: check status, trigger rollback, notify stakeholders, etc.

Communication: Use communication tools (Slack / PagerDuty / email) to notify stakeholders (Dev, Ops, Product) when a failure occurs, along with context (what happened, potential impact).

Temporary Mitigation: If possible, trigger automated rollback or failback to stable version while your team investigates.

Root-Cause & Post-Mortem: After the incident, conduct a post-mortem. Document what went wrong, why it wasn’t caught, and what actions you’ll take to prevent recurrence.

Continuous Improvement: Update automation workflows, pipelines, and runbooks based on lessons learned. Ensure risk mitigation (tests, checks, validation) is strengthened.

Explain how you would handle a situation where a deployment is running during after-business hours and something goes wrong.

What is a “pipeline as code” and how do you implement it?

How do you handle rollback of infrastructure when a new version causes issues?

Describe how you would monitor infrastructure cost and optimize spending via automation.

How do you manage secret rotation, auditing and access controls in automated systems?

Explain how you would integrate container lifecycle management (build → test → push → deploy → deprecate) into your automation.

How do you handle schema migrations, multi-version apps, and backward compatibility in your deployment pipeline?

What is blue/green vs rolling vs canary vs A/B deployment – and how would you choose between them?

Describe how you have tuned the performance of an automated system (e.g., reduced build time, deployment time).

How do you design a runbook for failure scenarios in automated workflows?

What is a “post-mortem” and what role does it play after a failed release?

Explain how you build collaboration with software dev, QA, Ops teams when automating deployment workflows.

How would you implement multi-channel (on-premise + cloud) automation for high-volume, high-transaction systems?

How do you ensure your automation solution is secure (data at rest/in transit, credentials, audit logs)?

Explain handling of authentication and authorization for APIs in automation workflows.

How have you handled logging and monitoring of automated deployments in production?

Describe how you would perform a performance review of an automated deployment pipeline.

How do you ensure compliance (security/regulatory) in your automated infrastructure and pipelines?

How would you choose between a managed service vs self-managed for automation/infrastructure tools?

How do you keep up-to-date with new tools/trends in automation and DevOps?

Describe a project where you worked in both Agile and Waterfall methodologies for automation/delivery.

Explain a case where you designed a resilient infrastructure solution (automated) for fail-over and disaster recovery.

What monitoring alerts or dashboards did you create for an automated system?

How did you hand over an automation solution to operations (documentation, training, support)?

What are some common mistakes you have seen in automation pipeline design, and how do you avoid them?

How do you debug issues with infrastructure provisioning (e.g., Terraform apply fails mid-way)?

How do you ensure your infrastructure code is reviewed, tested, versioned (in same way as application code)?

What is “configuration drift” and what tools do you use to detect/handle it?

How do you handle secrets or keys in container images and pipelines (to avoid credentials leakage)?

How do you measure service level objectives (SLOs) for automated systems?

Describe your experience working with Kubernetes in production (cluster setup, upgrades, pod scheduling).

How do you manage stateful vs stateless applications in an automated deployment pipeline?

How would you automate the monitoring of infrastructure health and automatically remediate (self-healing)?

Explain the difference between orchestration and choreography in microservices automation.

How did you participate in UAT (User Acceptance Testing) or CIT (Component Integration Testing) in automation projects?

What has been your role in writing technical specifications and documentation for automation solutions?

Describe how you worked under a deadline to deliver an automation solution and what you did to ensure success.

How do you ensure your automation solution supports change management and roll-forward/roll-back?

How do you handle legacy systems when designing a new automation pipeline?

Describe a time when you improved operational efficiency via automation in your previous role.

🧠 Advanced / Architect / Edge Cases Level (≈ 50 questions)

These dig into architecture design, trade-offs, scaling, deep troubleshooting, strategic decisions.

Architect an end-to-end system supporting millions of transactions per hour, with both on-premise and cloud components, using automation – how would you design it?

How would you migrate an existing monolithic on-prem application to a containerised microservices architecture with automated deployments?

What are the key considerations in designing an automated pipeline for a multi-tenant environment?

How would you design the automation solution for high-availability, multi-region deployment with automatic failover and disaster recovery?

Explain how you would integrate security (DevSecOps) into every phase of the automation lifecycle — from code to deployment to operations.

What are “pipeline anti-patterns” in CI/CD and how would you avoid them?

How would you optimise your deployment pipeline to reduce lead time and build/test/deploy time?

How do you handle “database migrations” for live systems where downtime needs to be minimal and roll-back is risky?

How do you build observability (metrics, logs, tracing) into an automated system such that you can detect performance issues, root-cause them, and fix them via automation?

How do you deal with “infrastructure as code” at scale (hundreds/thousands of resources across regions) – versioning, state management, security, drift, cost control?

Describe how you would implement a “self-healing” infrastructure that automatically remediates common failures (e.g., unhealthy instance replaced).

What trade-offs do you consider when choosing between managed services (e.g., managed Kubernetes) vs self-managed for critical automation systems?

How would you design a “zero-downtime” deployment for a large-scale global system including database, stateful and stateless components?

Explain “immutable infrastructure” in the context of patching and updates and how you would implement it.

How do you handle secrets management, rotation, and audit in a highly regulated environment (e.g., financial services, healthcare)?

Describe a situation where you had cascading automation failures (e.g., one automated task triggered by another) and how you resolved the root cause.

What are the key metrics you would include in a dashboard to show leadership that automation is delivering business value?

How do you balance speed (fast deliveries) with stability (low risk) in an automated deployment pipeline?

How would you handle a scenario where your automated deployment introduced a critical yet subtle bug in production and you didn’t catch it in tests?

Explain how you would manage infrastructure cost in cloud automation when workloads are highly variable (auto-scaling, spot instances, reserved instances).

How do you incorporate “shift-left” testing and security into your automation workflows?

How would you architect a hybrid (on-prem + cloud) automation solution where data sovereignty, compliance, and latency matter?

What is “policy as code” (e.g., OPA, Terraform Sentinel) and how would you use it in an automation context?

Explain how you would ensure “infrastructure drift” remains zero or minimal in a fast-changing environment.

How would you implement controlled deployments across many teams (microservices) while ensuring consistency and compliance?

Describe how you would carry out post-implementation triage and support of a business software solution you helped automate.

What steps would you take when you must support after-business hours deployment/releases regularly to minimise risk and ensure coverage?

How do you design automation solutions that are maintainable by teams outside of you (i.e., hand-over, documentation, runbooks, training)?

Describe how you would work with vendors (offshore, application, service) to deliver an automation project – what coordination, documentation, metrics would you define?

What is the difference between having a “pipeline” and “workflow orchestration” (e.g., Jenkins vs Airflow-type systems) in automation – when would you choose one?

Explain how you would debug a situation where a Kubernetes cluster upgrade script failed silently and caused production instability.

How do you track and manage configuration changes, releases, and dependencies when you have thousands of services and pipelines?

What is “observability debt” and how would you pay it down in a mature automation environment?

Discuss how you would handle multi-cloud automation where each cloud has different APIs, tooling, and constraints.

What is the role of “service mesh” in automated microservices deployments and what challenges does it bring?

How do you measure the return on investment (ROI) for automation initiatives in infrastructure and operations?

How would you design an alerting and incident response automation system that automatically escalates and triggers runbooks for common failures?

Explain how you would build capacity for disaster recovery in a deployed automated system (e.g., backup automation, region fail-over).

How do you ensure code quality, review, and testability of your automation scripts/infrastructure code the same way as application code?

Describe a time you discovered a process improvement in your automation workflow that saved significant resources/time and how you implemented it.

What are the typical risks involved in automating production deployments and how do you mitigate them?

How would you design a workflow where operations teams could safely override or intervene in automated tasks without breaking the overall automation logic?

Explain how you would integrate business continuity/disaster recovery (BC/DR) into your automation solution for a high-transaction system.

How do you decide when not to automate something (i.e., manual is better) and why?

How do you ensure your automation solution is future-proof (modular, versioned, supports new tools/changes)?

What are the best practices for writing automation scripts that will be maintained for years and by different teams?

Explain how you would provide after-hours support for deployment-automation, including on-call, runbooks, alerts, and handover.

How do you ensure cross-functional teams understand the automation workflows, dependencies, and responsibilities?

What are the challenges of combining Waterfall and Agile practices in a DevOps context, and how would you harmonise them?

Imagine you inherited a legacy automation pipeline full of scripts, manual steps, no documentation – how would you approach cleaning it up/improving it systematically?
