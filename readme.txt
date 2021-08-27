Before Jenkins:
Developers - >checkin <- source code repo - Integration and Build - Testing and Validation - Release -> Bugs <- Developer

Drawback: 
No Constant Feedback
Bug Fixing - Costly
Slow Software Delivery

Jenkins help by continuous intergation and delivery
Benefit:
Constant Feedback
Bug Fixing - Effective - time to identify the cause of the bugs reduces drastically
Fast software delivery

-------------------------------------
Continuous Integration: Its a development practice where developers integrate code into shared repo frequently, preferably several times a day. Each integration can then be verified by an automated build and automated tests.
Benefit: detect errors quickly

Continous deployment and delivery: Keep your applicataion deployable at any time.

-------------------------------------

CI / CD:
Continous Integration: This is the practice of integrating changes from different developers in the team into mainline as early as possible, in best cases several times a day. Each integration can then be verified by an automated build and automated tests.

Continous Delivery: This is the practice of keeping your codebase deployable at any point. Beyond making sure your application passes automated tests.

Continous deployment: This closele related with contious integration and refers to keeping your application deployable at any point of time or even automatically releasing to a test or production environment if the latest verison passes all automated tests.

continuous delivery VS continuous deployment: code checkin, unit testing, code quality, build and deployment, acceptance testing, production deployment.
All process are automated except manual production deployment in case of delivery where automated for deployment.

-------------------------
Benefits of CI:
Reduces Risk
Better communication
faster iterations
Earlier detection
reduces overhead
---------------------------
CI Principles:
Maintain a single source repo
autoamted build
make your build self testing
every commit sould build on an interation machine
keep the build fast
test a clone of the production environment
make it easy for anyone to get the latest executable version
everyone can see what is happening
autoamted deployment

CI Practices:
Developers chcek out the code into private workspcaes
when done, commit the changes into repo
the CI server monitors the repo and check out changes when they occur
the ci server build the system and runs unit and integration test
the ci server releases deployable artifacts for testing
the ci server assign a build label to the version of the code it just built
the ci server informs the team of the succesful build
if the build or tests fail, the ci server alerts the team
the team fixes the isue at the earliest
---------------------------------
Jenkins Plugin:
plugin are the heart of how jenkins functions in achieving CICD. Jenkins interconnected with well over 1000 plugin that allow it to integrate with most of the development, testing and deployment tools.
---------------------------------
Features:
Open source tool
Easy installation
Easy Configuration
Rich plugin ecosystem
Extensiblity
Distributed builds

----------------------------------
Architecture: 
Master -Slave concept: master is managing the slaves. Scheduling and Dispatching jobs to slaves, monitor the slaves, records and present job results, execute some jobs directly

Slave: handles all the requests from the jenkins master instance. Each slave in an independent entity running on its own OS.

		Jenkins Master 
Jenkins Slave	Jenkins Slave	Jenkins Slave

--------------------------------
Pipeline: its a suite of plugin which supports implementing and integration contious delivery pipelines into jenkins.
---------------------------------
---------------------------------

Jenkins install: war extract and install inside tomcat deploy folder.
install exe/

start jenkins:
F:\Tutorial\jenkins>java -jar jenkins.war --httpPort=8091

Jenkins terms:
Job/project: Refer runnable tasks that are configured in jenkins
Node: Each machine that are part of jenkins grid(can be master or slave)
Executor: Thread or slot for execution of jobs
Build: Result got after executing a job
plugin: Software that extends core functionality of jenkins


Manager Jenkins-> Manager User : Authorization -> Matrix based sucerity: manager user permision in jenkins

How to create users in jenkins?
diff authorization and authentication in jenkins?
used matrix base athorization to grant user acces?
user role based strategy plugin to create roles and grant user access?





