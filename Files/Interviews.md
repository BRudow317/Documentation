# Interview Practice and Notes
- Context (what system / constraints)
- Your role (what you owned)
- Problem (what was broken / slow / risky)
- What you did (2–5 concrete actions)
- Result (numbers if possible: latency, cost, incidents, time saved)
- Tradeoff (what you chose not to do and why)


## Owning Each Question
If the question says “professional experience” and you don’t have production examples for that exact tech, do this:

Be explicit: “In my day job I was primarily Java/Oracle; for Node/React/Terraform/Python/AI I’ve built working systems in my lab and I can walk through them end-to-end.”

Then give an end-to-end example anyway (architecture + decisions + how you’d productionize it).

#### For Example Say you are asked:
`How have you used Terraform in your professional experience?`

If you have limited/no Terraform at work (honest version that still scores well)

Say this:

“In my professional role, infrastructure was mostly handled by platform teams, so I didn’t own Terraform in production. What I did own was deployment readiness: I partnered with infrastructure on requirements, security constraints, and troubleshooting. Separately, I’ve used Terraform (Infrastructure as Code) in my AWS lab to provision Amazon RDS (Relational Database Service) Postgres, networking, IAM, and app hosting, with remote state and environment separation. I can walk through that setup and how I would apply the same approach in a production team workflow.”

Then walk through:

What you provisioned (VPC, RDS, app runtime)

How you handled state, environments, and secrets

How you’d integrate it into PR review and releases