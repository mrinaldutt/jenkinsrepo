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
--------------------------------------------
Remote access:
crte a token: abcdefghijkl12345
localhost:8091/job/HelloWorld/build?token=abcdefghijkl12345

Access java files:
set PATH="C:\Program Files\Java\jdk1.8.0_301\bin"
javac -version
cd /d F:\Tutorial\jenkins
javac HelloWorld.java
java HelloWorld

GIT:
Install ngrok.
run the batch file& fire command: ngrok http 8091
access ngrok: http://localhost:4040/
you can find public url for jenkins

Now go to gitub repo and click on setting and find the webhook.
Add webhook: payload url.

Now go to jenkins dashboard and click on helloworld task and click configure.
click on build trigger and click on Github hook trigger for GItScm pooling.

POOL SCM | Webhooks
Resource Intensive: Heave Operation & need to be fird requently | Not costly, no constant checking involved
Wait for builds:Have to wat in the order of minutes for the build to happen | Instant builds(Build are triggered immediately whenever a checking happens.
Safer Option: Safer as jenkins is communicating to code repo | Security concern (Opening up jenkins to the outside world)

If we have build cyce is very short exampe few mins, then webhook is perfet solution. If our build cycle is longer may be 30 mins and we dont need build for each and every commit then Pool SCM is suitable solution.

-----------------------------MAVEN INTEGRATION----------------------------
setup maven local repo: setting.xml
<localRepository>C:\software\maven_repo</localRepository>


----------Integration maven with jenkins-------------
One way:
Create a job for maven :
create job named MavenJob
select build -  Goal : clean test package
POM: select pom path (F:\Tutorial\jenkins\jenkins_workspace\jenkins\pom.xml)
Apply & save
execute build now and check console output- jar created (Building jar: F:\Tutorial\jenkins\jenkins_workspace\jenkins\target\jenkins-0.0.1-SNAPSHOT.jar)

Another way:
install Maven Integration plugin
create job and select as maven project
select build- select root pom - pom.xml
goal- clean test package
advance - custom workspace - F:\Tutorial\jenkins\jenkins_workspace\jenkins (as we dont download anything from github thus tell where is the workspace)

Now go to global tool configuration to tell jenkins where maven is installed:
update maven installation path - C:\software\apache-maven-3.8.1
------------------------------------------------------




