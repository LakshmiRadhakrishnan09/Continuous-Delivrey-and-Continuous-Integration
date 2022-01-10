# Continuous-Delivery-and-Continuous-Integration

Continuous Delivery and Continuous Integration

1. Developmenet envt should be similar as prod envt - No surprises

2. Able to recreate production envt exactly in an automated fashion - Virtualization

3. Automated Frequent

4. Changes - executable code, configuration, host environment, and data. If any of these is changing, it should be verified and audited.

5. The practice of building and testing your application on every check-in is known as continuous integration.

6. Build should work, Unit test should pass, test-coverage should met, functional acceptance must pass, non functional tests must pass(availability, security), exploratory testing and demonstration to customers.

7. Deployment pipeline is resource intensive. Optimize human resource usage.

8. test on commit stage of pipeline - fast, any failure should not realease test on later stages -slow(need parallelization), test can fail(performance drop) wait for the "good build" of the application should be removed. 

Can a single team handle multiple microservices?

Can a library be shared between multiple microservices?

               Microservices should have independent development life cycle and deployment independence. "Shared libary" defeats that.

               Shared library changes make sure that it is not breaking other services and all the dependent services should be redeployed.

               If a library is shared it should be like a 3rd part libary. Development of library and testing is independent of microservice. Corresponding microservice team decides which version of library to use.

               Accept code repetition between services. Sharing DTOs is against bunded context.              

               Split the library based on business domain. Maybe you need to split the library in different libraries with different responsibilities, if that responsability is unique and can't be splited, you should wonder if those two services should be only one. And if that library has business logic that feels weird on those two services, most likely that library should be a service in his own right. 

               Shared libary makes sense

               Cross cutting concerns - like http retry, connection pool

               Debate between DRY and loose coupling.

               Shared libraries support DRY but introduce coupling between service and library. It is better to duplicate code than introduce coupling issues. 

               Federated microservices?

 

Continuous Integration

Every check-in leads to a potential release Continuous integration detects any change that breaks the system or does not fulfill the customer’s acceptance criteria at the time it is introduced into the system.  Teams then fix the problem as soon as it occurs (this is the first rule of continuous integration). When this practice is followed,then the software is always in a working state. If your tests are sufficiently comprehensive and you are running tests on a sufficiently production-like environment,then the software is in fact always in a releasable state.

Create a Repeatable, Reliable Process for Releasing Software

As simple as pressing a button

Realease of MY_SOFTWARE cannot be done in one button click.
               Why? Services are tighly coupled. They are dependent . This is against microservice rule. Microservice should be an independent deployable unit.

              

Deming cycle: plan, do, study, act.
 

Keep Absolutely Everything in Version Control - In MY_SOFTWARE we are not keeping application properties.

               Keep requirement documents, release plan, automated test scripts in version control. - in MY_SOFTWARE we use confluence.

               We can store postman scripts in version control!!

Check In Regularly to Trunk - Debatable - master branch and feature branch. Author thinks we should commit directly to master.

               Create one branch for feature and developers merge to same branch.

               In my_project, branches are created per story, instead we can create branch for a feature, multiple developers can checkin and once satisfied merge to master.

               In this case, before u checkin,

                              run your commit test suite before the check-in. pretested commit

Use Meaningful Commit Messages - link to story/defect - lock the commit if it is not linked.

Managing External libraries -

We recommend that you keep copies of your external libraries somewhere locally (in the case of Maven, you should create a repository for your organization

containing approved versions of libraries to use).

Specify exact version of library

Binary dependencies - ??

Configuration Issues can be captured by smoke tests.

 

Configurations can be

               Build script can pull configuration and incoperate it into binaries at build time.- Not good. we want different configration for different envt.

               Deployment script can pass at deployment time. MY_PROJECT is doing this.

               Application can fetch configuration at start up time through configuration files(In app service application.properties), envt variables(in openshift).

               Don’t Check Passwords into Source Control or Hard-Code them in Your Application.

 

An open source tool called ESCAPE [apvrEr] makes it easy to manage and access configuration information via a RESTful interface. 

Deployment script should fail if external service ur application is depending on is not avilable. 

It should always be cheaper to create a new environment than to repair an old one - MY_PROJECT is not following this.


Puppet and CfEngine are two examples of tools that make it possible to manage operating system configuration in an automated fashion.

If your configuration management process is sound, you should be able to answer “yes” to the following questions:

• Could you completely re-create your production system, excluding produc[1]tion data, from scratch from the version-controlled assets that you store? - Yes

• Could you regress to an earlier, known good state of your application? - Yes

• Can you be sure that each deployed environment in production, in staging, and in test is set up in precisely the same way? - Yes

 

CI Servers: Atlassian’s Bamboo, Zutubi’s Pulse, Hudson, CruiseControl, ThoughtWorks Studios and TeamCity from JetBrains
 

Unit test - 10 mits

Component test -

Acceptance test - production like envt
 

compile and test that you run prior to check-in and on your CI server should take no more than a few minutes . Max 10 mits.
 

2 stages:

commit stage: compile, run unit test case, create  a binary. Before check-in.

second stage: take the binary, run acceptance test and integratio test . Run this in parallel
 

https://medium.com/javarevisited/top-10-books-experienced-java-programmers-should-read-73481356d279

https://www.baeldung.com/cs/microservices-db-design
