# Threat Modeling

Threat Modeling Questions to ask before your next Agile sprint

1.  Are you changing the attack surface? 
2.  Are you changing the technology stack? 
3.  Are you changing application security controls?
4.  Are you adding confidential/sensitive data?
5.  Are you modifying high-risk code?

## Rapid Risk Assessment (RRA) - Helping you to know what you don't know

It never will happen, but if there is no threat, there is no risk.  Know the threat...know the risk... 

So what is the threat?  What is the risk?  How do we know or what do we need to know; who knows, who needs to know...you Know?  No. So let's find out.

[Template in Markdown](template_RRA.md)

> Consider using a commit hook to ensure that the RRA is completed before a new project is added to the repo.
> Also Consider building a hook to ensure that the RRA is updated, changes are reviewed, and the RRA is re-approved by somebody who has the authority to accept risk before a new release is deployed

Examples:

- PayPal risk questionnaire for new apps/services  
- Mozilla Rapid Risk Assessment (RRA) model: 30-minute review  
- Slack goSDL for questions to determine initial risk rating  


## Resources

Quick overview of threat modeling: [Threat Modeling Fundamentals](https://www.youtube.com/watch?v=Uz2Vnp5ZW4c) by Adam Shostack.

[Synopsis (Cigital) "4 threat modeling questions to ask before your next Agile sprint"](https://www.synopsys.com/blogs/software-security/threat-modeling-questions)

[SAFECodes Tactical Threat Modeling Guide for how and when to do threat modeling in Agile and DevOps environments](https://safecode.org/resource-secure-development-practices/tactical-threat-modeling/84)



