# Dev Collaboration Standards, Guidelines, and Ideas

How we work together, track progress, and make estimations

* The Architecture Determines the Organization
* The Importance of Modularity
* Unit Testing
* Team Structure
* Pilots and Copilots
* Coach and Team Captain
* Improving Estimations
* References
* Documentation
* The Workbook
* Self-Documenting Code
* The Product Roadmap
* The Backlog

## The Architecture Determines the Organization
### The Importance of Modularity

The architecture of a system determines the roles, intercommunication, morale, and productivity of its developers. If the codebase for a product is monolithic, prone to failure, interdependent, and legacy, then the development team will reflect this in their habits and values. If the codebase is modular, decoupled, and innovative, then the development team will behave likewise.

Developers often reminisce about side projects or early-stage startups when development was fast and creative. This is known as “garage development”, and is only fast because the code does not have to work within a larger system for serious stakeholders. The productivity of garage programmers can be greatly reduced when they are moved into a large system, because the extra work of larger systems can sometimes increase the burden exponentially. Using decoupled, modular services (known as “microservices”) is a way to move back towards “garage programmer” productivity while still satisfying large-system and large-stake goals.

Examples of these modular systems include:

* A single database that holds all fundraising data, with a single gateway interface for all fundraising products
* Separate services for media, payments, analytics, etc. extracted into their own codebases.
* Purely front-end fundraising products that are simply clients to the above services
* Generalized, embeddable fundraising widgets (such as the donation flow) that can be optimized and used across many products (think of the Facebook “Like” button)
* Business intelligence dashboards (also clients to shared, generalized services)
* Fundraising page designs, templates, and themes
* Content management for sales and marketing that doesn’t require extra burden on the engineers
* Libraries and utilities (Ruby Gems and NPM modules)

Some of the benefits of this approach include:

* The ability to roll out new, experimental fundraising projects in a relatively short amount of time (only design and front-end work, with little to no back-end work).
* Microservices have a smaller contract, so can be tested and improved more quickly
* Modular codebases can be worked on in parallel, without developers butting heads
* These modules can have less coupling and interdepencies; improving one module, while maintaining the integrity of its interface, does not affect the rest of the system
* Existing systems would not limit the ability to roll out new ideas and technologies in new modules


## Unit Testing

Japanese car companies are famous for having both high quality and productivity without one sacrificing the other, which stems from the attitude that all efforts towards increased quality should also inherently and necessarily be beneficial to productivity. In software, unit testing and test-driven development fit this concept well.

Unit testing is contrasted with “integration” testing in that it has a very narrow focus (usually a single function) with few inter-dependencies. These tests run very quickly (usually in sub-milliseconds), and have little data setup. In test-driven development, you write and run tests as you work on the actual code. The benefits of this approach are:

* Greatly increased codebase maintainability, and a drastic reduction in the “irreducible bugs” problem (where fixing bugs causes more bugs). Any small change to the product can be validated against the full suite of tests in a very short amount of time (unit tests should always be fast).
* The act of making code unit-testable improves the code itself, because unit tests require the code to have few dependencies and setup requirements. This produces simpler designs (see these papers).
* There is an initial learning curve in adopting test-driven development, but once learned, it can actually increase developer productivity by a large margin.
* The elimination of side effects, mutation, and globals in support of better unit tests.

Not all programming tasks are suitable for test-driven development, but nearly all are suitable for some kind of unit testing. A minimum standard for unit test coverage for all new code should be adopted.

## Team Structure

### Pilots and Copilots

There should be a single, lead programmer for each project who implements all the core specifications. This developer can be labeled the “pilot”, and there should be only one pilot per discrete thread in a project. Discrete threads are able to be worked independently by separate developers with no intercommunication or interdependency. Most projects have very few discrete threads, or only a single one.

Only one developer should be chosen as the “pilot” for each thread. Each project should have 1-5 “copilots” that assist in documentation, code review, debugging, and writing tests. If copilots are not assigned to a pilot, then each of the additional, non-core programming tasks should increase the estimation significantly (sometimes by up to six times). The reasoning for this setup includes:

* Software development is highly sequential. Most steps can only be worked on by one developer and each subsequent step depends on the completion of the previous step.
* Most features and optimizations require very strong conceptual integrity. This conceptual integrity is ruined when several developers are modifying and debating each other’s work.
* Developers are slowed down most by an increase in communication requirements. The more developers added to a project, the bigger the communication requirement and the higher the probability of communication mishaps.
* The copilot/pilot relationship is the perfect opportunity to apprentice junior developers.

Sometimes, even whole projects cannot be worked in parallel. In this case, the strongest “pilot” developer should be assigned the core programming, while all others serve as copilots until the project is completed. More commonly, several projects with several pilots can be worked simultaneously.

### Coach and Team Captain

A good approach for two types of leadership in an engineering department is to emulate the coach and team captain positions on any sports team. The coach plans strategy for the season, interfaces with others in the league, and is savvy about the sport from a high level but does not play the sport. On the other hand, the team captain plays the sport very well, leads by example, works with the coach on strategy, and manages day to day tactics.

The engineering coach:

* Is responsible for project planning, estimations, and communication with business owners
* Can be a project manager and does not need to code, but needs strong technical savvy
* At a quarterly level, is responsible for the performance of the development team

The engineering team captain:

* Has strong programming skills (with productivity 5x-10x above the average) and inspires the rest of the team into generating new ideas and advancing their skills and knowledge
* Participates in the planning of projects with the managers and is the main interface to the most hands-on technical issues
* Leads by example and produces at least as much code as any other developer. Drives all high-level architecture decisions
* Is very familiar with each developer’s technical strengths and is able to leverage those strengths in new projects
* Works with managers to create accurate estimations for projects.

A single person should not fill both roles, and their may be multiple captains and coaches in a larger org, with the "head coach" being the CTO.

## Improving Estimations

A very common problem with estimations is when developers only think about the time they will take to write the core feature code, but not the time taken for planning the project, getting the code to work within a larger system, training other developers, dealing with side effects, creating tests, writing documentation, fixing bugs, having meetings, and iterating on requests. 

The time to write the core code is often only ⅙ of the rest of the work. Also, we can often assume that developers do actual engineering work for only 50% of any given workday. As a baseline, plan for only 20 hours per week of engineering time for core tasks per person (don’t forget to balance commitments to support and maintenance as well). This number can be made more accurate by tracking it.

Developers will often pad their estimation by some multiple in order to reduce their own liability. Instead of determining estimations out of fear, use them to refine and limit the specifications of the project to help its planning and scope. The goal of estimates is not to have the best predictive ability, but to support project success. Rather than trying to predict an outcome, use estimates to determine whether a project’s targets are realistic enough to allow the project to be controlled and to meet its targets.

The first and best way to estimate new projects is to use the actual recorded time taken for similar, completed projects. This requires a detailed history for each project (see “The Workbook”).

The second technique is to have the “pilot” programmer break down every specification into a list of tasks, and then break down each of those tasks into a atomic, actionable pieces that takes less than 8 hours. 

Add up all the hours for every subtask and divide it by an hours-per-week baseline for the pilot, weighing their other obligations (start conservatively with at most 20 hours per week). Cross reference the number of weeks with the actual time taken for previous, similar projects to validate the estimate.

Estimations rely on assumptions about team performance, including engineering hours per week and time for QA and debugging. These assumptions can be refined over time, starting with some baselines. These metrics can be generally used to evaluate and compare developer performance, but should not be taken as the sole authority.

The most important piece of the process is to keep a record of the time taken for every project, and to refer to that data for future estimations. In addition to workbooks, keep a spreadsheet where each row is a different estimation with columns for "estimated time", "actual time taken", who the developer was, and a note about the category/type of work. For large orgs, keep a spreadsheet for each developer separately.

Developers should never estimate time on-the-spot. The only in-the-moment estimates should be “t-shirt sizes”: small, medium, large, and extra-large. Timeframe estimates should only be made after an approved product definition and full list of requirements are made.

Projects should be estimated prior to and independent of the planning stage. The planning for a project should use the estimation, not the other way around.

For projects without deadlines, do not estimate an exact date, but instead estimate a range with the first date being a low probability, optimistic estimate, and the second date being the highest probability, most conservative estimate. For example, instead of estimating “18 weeks”, estimate a probability range starting at 12 weeks (we are 50% sure we can deliver in 12 weeks) to 24 weeks (we are 90% sure we can deliver in 24 weeks).

## Documentation

### The Workbook

The Workbook comes from the early days of large systems programming projects, where teams would compile memos and references for a single project into a binder, and each programmer and manager would have a copy for their own reference. Workbooks provide a way to take the decisions and ideas made in conversation and email and translate them into a more concrete and organized plan that can be referenced and modified as the project progresses. Workbooks track larger features and objectives, not fine-grained tweaks. These workbooks do not replace issue-tracking systems, but are higher level, less technical, and readable by business owners. Besides being a specification reference, they are useful for tracking estimates.

These days, Google Docs is the perfect way to implement this system. The project manager and lead engineer would have write access to this document; all others would have comment and suggestion access. The teams would have a template workbook document that they can copy and use for future projects. They can refine this template after each project.

The workbook records the personnel, estimations, specifications, and references for a single project. It is continuously edited with tweaks and results as the project advances. When the project is completed, the workbook must be updated to list the actual times taken. The project manager and development team should commit to reviewing and revising the workbook once per week during the project.

### Self-Documenting Code

All code can be self-documenting, with standardized comments and type declarations that can be used to generate readable documentation for the architecture. Ruby can use YARD to automatically generate HTML pages based on comments and type annotations from the source code. Similarly, Javascript code can use ESDoc in the same way. A standard can be defined for minimum requirements in the documentation, and pull-requests should only be accepted when this standard is met.

In a JSON API, every endpoint can have a set of parameters, each with a built-in description and type constraint that can be used to generate documentation for that endpoint. Clients to the API can use the OPTIONS request to see all the documentation about any endpoint. A documentation website for the API can be automatically generated and formatted from these requests.

### The Product Roadmap

There should be one high-level roadmap document per product, listing the current biggest development priorities tied to the highest value business goals. This roadmap should be simple and presentable, no more than 1-2 pages, and best presented as a formatted document readable for non-engineers. It can be private and internal by default.

Most importantly, the project manager(s) on a project should commit to reviewing and revising the roadmap once per month, bringing in any business owners and engineers for feedback.

### The Backlog

The Scrum backlog is a graveyard of ideas. It is a way for engineers to gently lie to feature requesters that they will implement their idea soon, but actually will ignore it indefinitely. The backlog can be made useful by following these guidelines:

* Only allow new tickets to be entered into the backlog and not the current todos. Only pull from the backlog into the current todos, regarding every item in the backlog before pulling a new task into the todos.
* Annotate items in the backlog according to “t-shirt size” ratings (small, medium, large, and extra-large) for three points: business value, development estimation, and client urgency. The importance of the item can be seen as the ratio of these points: an item with a “small” estimation and an “extra-large” business value is pushed to the top.
* Schedule and commit to a once-per-month window of time where a project manager reviews all items in the backlog, re-rates them according to current company priorities, eliminates irrelevant items, and pushes highly important items to the current schedule. * This review can be done right after the once-per-month roadmap review, when business priorities are fresh in mind.

## Reading List and References

### Books

* Peopleware - Tom DeMarco
* The Mythical Man Month - Fred Brooks
* Rapid Development: Taming Wild Software Schedules - Steve McConnell
* Slack - Tom DeMarco
* Software Estimation: Demystifying The Black Art - Steve McConnell

## Papers, Studies, and Articles

* Evidence Based Scheduling - Joe Spolsky
* Studies of Test-Driven Development - Various
* On the Sustained Use of a Test-Driven Development Practice at IBM - Various
