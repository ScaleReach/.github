# ScaleReach - OCBC Ignite 2024

Problem statement: How can we reduce call volumes to OCBC hotlines?

Problem agitator: Long wait time results in frustrated clients.

The goal of ScaleReach is to reduce wait times at hotlines to virtually zero, reducing the number of callers that require assistance from a human provider.

Featuring Jane, our first call bot agent packed with many functionality, mimicing a real customer support officer at OCBC's hotline.

Jane was created for the sole purpose - reduce call volumes at OCBC's hotlines.
![Screenshot of interface hosted live on https://scalereach.team](/public/mock-portrait.png)

## Jane
Powered by an intent service, knowledge database, authentication service, and LLM model, Jane can mimic the function of a real customer support officer to a great extent.

With Jane, ScaleReach hopes to resolve mundane enquiries and help provide faster, more efficient support to clients in need.

In the event Jane faces challenges communicating with the caller, it will escalate the call to a human provider.

![Jane architecture diagram](/public/jane-big.png)

### Intent service
For queries that require more time to be resolved (i.e. reach out to relevant departments), Jane can capture the details of the intent, authenticate the user via a separate service, and finally file the intent to be completed by a staff.

A staff can work to resolve the intents (e.g. submission of tracer to check remittance status) without having to contact the caller. This reduces the stall time arised from awaiting responses from the client. All in all, increasing efficiency.

![Screenshot of intent dashboard](/public/dashboard.png)


### Knowledge database
To ensure the repsonses and help provided by Jane is accurate, RAG is implemented with a custom vector database to query for the top three most relevant answers.

This will help ensure the LLM only provide responses that has been verified (within the knowledge database) and not provide hallucinated responses.

Therefore, the power of Jane is only limited by the size of this knowledge database. Gradually, with a big knowledge database, mundane and common enquiries can be resolved by Jane amicably.

View the SQL script to setup the PostgreSQL database: [gist.github.com](https://gist.github.com/ballgoesvroomvroom/47db0c9e9d3a064873367ac43d62b6c2).

### Data governance
Utilising LLM provided by third-party providers such as OpenAI may be the most feasible option when on-premise infrastructure lacks the capability.

Therefore, Jane will authenticate the caller through a separated, indepedent service. It will redact all personal identifiers and details (bank account numbers, user id etc) before passing it into the LLM to generate a response.

The authentication service works in a structured manner, making the redaction possible.

### Deployment
Jane is deployed as a combination of many services, made easy with Docker containers and compose.
Hosted and deployed on AWS infrastructure (EC2, behind a VPC) with Cloudfare DNS (https://scalereach.team).

A docker ochestrator can be brought into play, further amplifying ScaleReach's reach by allowing it to handle multiple calls at once.

View sped up (x1.5) demo here (no audio due to privacy controls on capturing device - no voice call audio can be captured): ![Sped up 1.5x demo of ScaleReach hosted live on https://scalereach.team](/public/demo.mp4)


## Crowd control
An interactive map that features wait times with their respective colour indicators.

This can allow OCBC's clients to make an even more informed decision on their choice of branch when visting, effectively serving as a load balancer that balances the load equally throughout the branches and their operating hours.