# General Questions

This file is for speaking practice.
The goal is not just to memorize answers.
The goal is to learn a repeatable structure for answering common interview questions clearly.

## The 3 Most Important Questions

### 1. Tell me about yourself.

What to memorize:
- one short opening sentence

Example opening:
I’m a backend engineer with experience at Zoom and Amazon, mainly working on distributed backend systems, APIs, and OAuth-related services.

How to structure the answer:
1. current / most recent role
2. strongest technical themes
3. what you want next

What a good answer should sound like:
- 30 to 60 seconds
- Zoom + Amazon
- backend / distributed systems / APIs / OAuth
- what he wants next

Example answer:
I’m a backend engineer with experience at Zoom and Amazon, mainly working on distributed backend systems, APIs, and OAuth-related services. At Zoom, I worked on public APIs, OAuth workflows, production reliability, and storage migrations like moving scope data from S3 to MySQL. What I’m looking for next is a backend role where I can keep building scalable production systems and grow in system design and reliability.


### 2. Tell me about an issue you handled.

What to memorize:
- start with the symptom or problem

Example opening:
One example was an issue that affected reliability, and I handled it by narrowing down the scope first before jumping into a fix.

How to structure the answer:
1. what the issue was
2. how you investigated it
3. what the root cause was
4. what you changed

What a good answer should sound like:
- can be production or non-production
- clear symptom
- step-by-step investigation
- fix and result

Helpful follow-ups:
- What was the symptom first?
- How did you narrow it down?
- What was the actual fix?
- What changed afterward?

Example answer:
One example was an issue that affected reliability in a backend flow. I started by narrowing down the symptom using logs and service behavior, then traced the request path to identify where the failure was happening. After confirming the root cause, I fixed the issue and also improved visibility so similar problems would be easier to detect and diagnose in the future.


### 3. Can you walk me through the S3 to MySQL migration?

What to memorize:
- old system, problem, change, rollout, impact

How to structure the answer:
1. what the old system was
2. what problem it caused
3. why MySQL was better
4. how the migration was done safely
5. impact

What a good answer should sound like:
- why S3 was not enough
- what problem needed to be fixed
- why MySQL helped
- rollout / migration safety
- result / impact

Helpful follow-ups:
- What was wrong with the original setup?
- Why was MySQL a better fit here?
- How did you avoid breaking production?

Example answer:
Originally the scope data lived in S3, which worked for basic storage but became limiting as the platform grew. It was not a great fit for more structured access patterns and service-side consistency. I worked on moving that data into MySQL with a more structured schema, and we rolled it out in stages so we could validate behavior safely in production before fully switching over.


## Additional Important Questions

### Walk me through your resume.

How to structure the answer:
1. company by company
2. spend most time on Zoom
3. only mention 2 or 3 strongest bullets per role

Example answer:
I started as an intern at Amazon, where I worked on a distributed backend workflow system and built a plugin for publishing merchant contribution entities through SNS. After that I joined Zoom full-time, where I worked on Zoom Phone APIs and core OAuth platform components. My work there focused on backend reliability, workflow automation, observability, and a migration from S3 to MySQL to improve consistency and performance.


### Which project on your resume best represents your backend engineering skills?

How to structure the answer:
1. pick one project only
2. explain why it shows ownership
3. explain technical depth
4. explain impact

Example answer:
The project that best represents my backend engineering skills is the OAuth scope storage migration from S3 to MySQL. It required understanding the old design, identifying scaling and consistency limitations, changing the service layer, planning a safe rollout, and thinking about production impact. I like that example because it combines system design, implementation, and operational thinking.


### Why was S3 not enough for that use case?

How to structure the answer:
1. what S3 was doing
2. what limitations appeared
3. why those limitations mattered

Example answer:
S3 was fine as basic object storage, but it was not a great fit for data that needed more structured access and stronger consistency in service logic. As the system evolved, query flexibility and update patterns became more important, and MySQL was a better fit for that kind of workload.


### What improved after moving to MySQL?

How to structure the answer:
1. performance
2. consistency
3. service simplicity

Example answer:
The main improvements were lower lookup latency, better consistency across services, and a data model that was easier to work with in the application layer. It also made the backend behavior more predictable as the system scaled.


### How did you make sure the migration was safe?

How to structure the answer:
1. avoid hard cutover
2. rollout in stages
3. validate and monitor

Example answer:
The main thing was to avoid a hard cutover. We rolled the change out in stages, verified behavior in production, and monitored the new path carefully before fully switching traffic. The goal was to reduce risk while still moving the system forward.


### How do you usually debug distributed issues?

How to structure the answer:
1. start with user-visible symptom
2. narrow scope
3. use logs / dashboards / service boundaries
4. validate with data

Example answer:
I usually start by identifying the user-visible symptom and the scope of impact. Then I use logs, dashboards, and service boundaries to narrow down whether the issue is in our service, a dependency, or a particular request path. Once I have a likely failure point, I validate the hypothesis with data instead of guessing.


### Tell me about your PagerDuty / on-call experience.

How to structure the answer:
1. what services you supported
2. what kind of alerting / monitoring work you did
3. what you learned operationally

Example answer:
I built monitoring and alerting for OAuth services and participated in on-call rotations across related platform services. That work taught me how to think about production visibility, what signals are worth paging on, and how to respond quickly without overreacting to noise.


### Tell me about the OAuth workflow automation work.

How to structure the answer:
1. what was manual before
2. what got automated
3. what changed operationally

Example answer:
There were workflows in the OAuth platform that involved a lot of manual coordination and multi-team dependencies. I worked on redesigning and automating parts of that process so the flow became much faster and less dependent on manual handling. That reduced turnaround time dramatically and made the overall process more scalable.


### Tell me about the event-driven pipeline you built.

How to structure the answer:
1. what event moved
2. why event-driven helped
3. what manual process it replaced

Example answer:
I built an internal event-driven pipeline to automate propagation of OAuth scope updates across services. Before that, parts of the workflow were more manual. Moving to a pub-sub style flow helped the system react more automatically and reduced operational overhead.


### Tell me about your Amazon internship project.

How to structure the answer:
1. one clear project
2. what you built
3. why it mattered

Example answer:
At Amazon I worked on a distributed backend workflow system and built a modular plugin that published merchant contribution entities through SNS. That helped downstream systems consume the data in a more scalable way and supported the team’s longer-term move toward more decoupled workflows.


### Why did the team use SNS?

How to structure the answer:
1. what needed to be shared
2. why decoupling helped
3. why it scaled better

Example answer:
SNS was useful because it let the system publish events in a way that downstream consumers could handle independently. That made the workflow more decoupled and more scalable than tighter service-to-service coupling.


### Why are you interested in this role?

How to structure the answer:
1. tie role to your background
2. tie role to what you want to grow in
3. keep it forward-looking

Example answer:
I’m interested in this role because it matches the kind of backend work I’ve been doing and want to keep growing in, especially around distributed systems, APIs, and production engineering. I’m looking for a team where I can contribute to real backend systems while continuing to deepen my system design and reliability skills.


### Why are you interested in our company?

How to structure the answer:
1. team or engineering culture
2. product or problem space
3. why it fits your background

Example answer:
What stands out to me is the combination of the engineering work and the team. From what I’ve learned so far, this role feels strongly aligned with my background in backend systems, APIs, and production reliability, and it seems like the kind of environment where I could contribute and keep growing.


### What kind of work energizes you the most?

How to structure the answer:
1. mention 1 or 2 themes only
2. tie them to real work
3. keep it positive

Example answer:
The work that energizes me most is backend work where I can combine implementation with real system impact. At Zoom, I especially enjoyed projects that improved reliability, automated workflows, or made backend systems easier to operate.


### What kind of team or environment helps you do your best work?

How to structure the answer:
1. communication
2. ownership
3. clarity

Example answer:
I do my best work on teams where people communicate clearly, have strong ownership, and care about building reliable systems. I’ve found that I work especially well in environments where expectations are clear and engineers are trusted to improve both features and the underlying system.


### Looking back at your recent experience, what do you want to do more of in your next role?

How to structure the answer:
1. connect to strengths
2. say what you want more of
3. keep it positive

Example answer:
In my next role, I’d like to do more backend platform and production-facing work, especially around distributed systems, APIs, reliability, and system design. My recent experience helped me realize that I really enjoy work where I can both build features and improve the long-term behavior of the system.


## AI-Related Questions

### Have you used AI tools in your work or learning?

How to structure the answer:
1. yes, in a practical way
2. where it helped
3. where you still verify carefully

Example answer:
Yes. I’ve found AI tools useful for speeding up repetitive work, exploring unfamiliar code, summarizing information, and giving me a starting point for implementation ideas. I still verify the output carefully, especially for production code and anything correctness-sensitive.


### What parts of AI tools have been genuinely useful to you?

How to structure the answer:
1. repetitive work
2. unfamiliar code
3. summarization / starting point

Example answer:
The most useful part has been speeding up repetitive work, helping me understand unfamiliar code, and giving me a starting point for implementation ideas. I treat it as a helper, not something I trust blindly.


### Where do you think AI tools are less helpful or less reliable?

How to structure the answer:
1. correctness-heavy areas
2. security-sensitive logic
3. subtle edge cases

Example answer:
I think AI tools are less reliable in situations where correctness matters a lot, especially in production logic, security-sensitive code, or areas with subtle edge cases. In those cases, I see them as useful for generating ideas or a starting point, but not as a source of truth.


### If you were integrating an LLM API into a backend service, what would you think about?

How to structure the answer:
1. latency and failure handling
2. rate limits and cost
3. logging and privacy
4. fallback if the response is bad

Example answer:
I would think about latency, retries, failure handling, rate limits, cost, logging, and data privacy. I would also think about what should happen if the model response is slow, incorrect, or unavailable, because in production the integration needs to be reliable even if the model is not.
