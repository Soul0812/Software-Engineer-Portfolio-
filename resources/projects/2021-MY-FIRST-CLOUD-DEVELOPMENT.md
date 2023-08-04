### 2021 - My first Cloud Development

![picture](../pictures/projects/Cloud-Email-Microservice.PNG)

I joined USA Enterprise project, and I was assigned to scrum team that was on initial phase of a Microservice development.
There was a goal to build cloud service for Email sending and Delivery Status processing that is based on Spring API and AWS components.
There were Team Lead and Tech Lead occupied with other tasks and less experienced Java Developer.
My contribution was expected to speed up development process and achieve app release.
My **task** was to find implementation way for email status processing, finalize POC, improve REST API, and support deployment automation.

Working simultaneously in Dev and DevOps teams, I had challenges with development and deployment:

- Specifically for development, I found way to get delivery status
  and configured email flow on AWS so that concept was proved
- Then, I was working on REST microservice improvements,
  including codebase refactoring to meet development principles like SOLID.
  For entire service, I redesigned data flow to get away
  from the quick working implementation to the right solution in terms of architecture.
- Also, I crated integration tests for local running.
  It was not easy as several AWS components are remote only.
  I managed to automate some manual work, so developer testing became faster.
- In DevOps team, I was working on deployment automation using Terraform.
  I implemented and integrated modules for SQS and Lambda.
  Also supported deployment for other AWS components