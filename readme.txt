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

----------------SONARQUBE----------------
Features:
Continuous Inspection of code
Centralized Quality Rules
Enforced Quaity Gate
Dig into the issues
DevOps integration
Vsualize history of project

Download and unzip community edition of sonarqube
set up java path in wrapper.conf
start sonarqube.bat : F:\My Software\sonarqube-6.7.7\sonarqube-6.7.7\bin\windows-x86-64>StartSonar.bat
browse - localhost:9000
default uid/pwd - admin/admin

Go to Maven project 
add sonarqube dependency-
<!-- https://mvnrepository.com/artifact/org.sonarsource.scanner.maven/sonar-maven-plugin -->
		<dependency>
			<groupId>org.sonarsource.scanner.maven</groupId>
			<artifactId>sonar-maven-plugin</artifactId>
			<version>3.5.0.1254</version>
		</dependency>

run - clean test sonar:sonar
now go to localhost:9000 - check the project scan status



For code coverage, need to add jacoco plugin:
<!-- https://mvnrepository.com/artifact/org.jacoco/jacoco-maven-plugin -->
	<build>
		<plugins>
			<plugin>
				<groupId>org.jacoco</groupId>
				<artifactId>jacoco-maven-plugin</artifactId>
				<version>0.8.2</version>
				<executions>
					<execution>
						<goals>
							<goal>prepare-agent</goal>
						</goals>
					</execution>
					<!-- attached to Maven test phase -->
					<execution>
						<id>report</id>
						<phase>prepare-package</phase>
						<goals>
							<goal>report</goal>
						</goals>
					</execution>
					<execution>
						<id>post-unit-test</id>
						<phase>test</phase>
						<goals>
							<goal>report</goal>
						</goals>
						<configuration>
							<dataFile>target/jacoco.exec</dataFile>
							<outputDirectory>target/jacoco-ut</outputDirectory>
						</configuration>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>

---------------------INTEGRATION WITH JENKINS - SONARQUBE--------------------------
Now go to jenins job - anothemavenjob - change the build as - clean test sonar:sonar
Build now and check the console output - sonarqube successfully run and o/p generated

------------
Now another way - need to add plugin sonarqube in jenkins
configure with default url - localhost:9000

now go to jenins job - anothemavenjob - change the build as - clean test
add post steps-sonarqube analysis with maven

now build and check console.
sonarqube integrated with maven sucessfully
------------
third way - Manager plugin - add sonarqube scanner
install automaticaly

now create a freestyle job - named- SonarQubJob
select execute sonarqube scanner -task : scan
Analysis properties- 
sonar.projectKey=jenkins
sonar.projectName=jenkins
sonar.projectVersion=0.0.1-SNAPSHOT
sonar.projectBaseDir=F:/Tutorial/jenkins/jenkins_workspace/jenkins
sonar.sources=src
sonar.java.binaries=target/classes

Now build now and check console

==============================================
--------------------------EMAIL--------------------
Configure email: Manage Jenkins->System Configuration -> Email
E-mail Notification - SMTP Server - smtp.gmail.com
Default user e-mail suffix - @gmail.com
Check Use SMTP Authentication - enter user name - awstests2020@gmail.com
enter password- *********
Use SSL and Use TLS 
SMTP port - 465
Reply-To Address - awstests2020@gmail.com
Now check by Test configuration by sending test e-mail

Now create a new freestyle job named-EmailConfigJob
exeute a command -  di
add post build steps - email notification - awstests2020@gmail.com
check Send e-mail for every unstable build & Send separate e-mails to individuals who broke the build

build now and check email

-----------------------------------------------------
To overcome some issue like edit subject, edit body of the messages, we need to do a different way:
Need to ad plugin - Extended E-mail Notification
then go to configure system - Extended E-mail Notification
setup SMTP server - smtp.gmail.com
SMTP port -465
SMTP username - awstests2020@gmail.com
password - ******
Use SSL and TLS
Default receients  -  awstests2020@gmail.com
Reply to list- awstests2020@gmail.com
We can configure default subject, default content, 
Now configure 	Default trigger - several options like - 
Aborted
Always
Before Build
Failure - 1st
Failure - 2nd
Failure - Any
Failure - Still
Failure - X
Failure -> Unstable (Test Failures)
Fixed
Not Built
Script - After Build
Script - Before Build
Status Changed
Success
Test Improvement
Test Regression
Unstable (Test Failures)
Unstable (Test Failures) - 1st
Unstable (Test Failures) - Still

Apply & save

Now configure emailjob
Post Build steps - send email for every unstable build
here we can enter any receipent list, reply to list, content, subject, attachment. 


=====================================INTEGRATION WITH SELENIUM AND TESTG==========================
Create a simple project and add below dependency:
<!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java -->
		<dependency>
			<groupId>org.seleniumhq.selenium</groupId>
			<artifactId>selenium-java</artifactId>
			<version>3.14.0</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/org.testng/testng -->
		<dependency>
			<groupId>org.testng</groupId>
			<artifactId>testng</artifactId>
			<version>6.14.3</version>
			<scope>test</scope>
		</dependency>
		
Now create a test case java file:
package com.mrinal.training.testng;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.testng.AssertJUnit;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

public class SampleSeleniumTest {
	
	WebDriver driver;
	
	@BeforeClass
	public void startBrowser() {
		System.setProperty("webdriver.chrome.driver", "C:\\Users\\mrinal\\Downloads\\chromedriver_win32\\chromedriver.exe");
		ChromeOptions chromeOptions = new ChromeOptions();
		chromeOptions.addArguments("--start-maximized");
		driver = new ChromeDriver(chromeOptions);
	}
	
	@Test
	public void validateGoogleId() throws Exception {
		System.out.println("Opening Browser");
		driver.get("http://www.google.com");
		System.out.println("Clicking Gmail Link");
		Thread.sleep(5000);
		driver.findElement(By.xpath("//*[@id=\"gbw\"]/div/div/div[1]/div[1]/a")).click();
		System.out.println("Clicking Sign In link");
		driver.findElement(By.xpath("/html/body/nav/div/a[2]")).click();
		System.out.println("Entering username");
		driver.findElement(By.xpath("//*[@id=\"identifierId\"]")).sendKeys("renju.jenkins.training");
		System.out.println("Clicking Next button");
		driver.findElement(By.xpath("//*[@id=\"identifierNext\"]/content/span")).click();
		Thread.sleep(5000);
		boolean textFound = driver.getPageSource().contains("Forgot password");
		AssertJUnit.assertTrue(textFound);
	}
	
	@AfterClass
	public void closeBrowser() {
		driver.quit();
	}
}


Now clean test package
Test completed
Test report  -F:\Tutorial\jenkins\jenkins_workspace\TestNG\target\surefire-reports
files: emailable-report.html
testng-results

Now go to jenkins
add plugin - TestNg
Now create a maven job named TestNGSeleniumJob
goto build -select the pom.xml location
goal - clean test package
advance- custom workspace -select directory
post build - publish testng result
select locaton of the tesng result - target\surefire-reports\

==========================Integrate Tomcat for deployment====================
Add plugin - Deploy to container plugin
Add users for jenkind auto deployment - tomcat-users
start tomcat

create a simple web project

create a maven job - tmcatdeploymentjob
select build - maven goal - clean package
advance - custom workspace - select the workspace
add post build action - deploy war/war to a container 
war - **/*war
contextpath - nameof the app
container -select tomcat8
userid/pwd
tomcat url

build the job
===============================================================================
===============================================================================
---------------Concept of Pipeline-------------
Pipeline - containes of pipes/jobs . each has own purpose.
Suppose - a job which gets the latest code from Git. 
A job which building the code and packing it as a deployable pipe.
A job which takes care of testing.
A job takes care of deploying it into server.
So all these jobs connects each other and forms pipelines that we achive continous delivery.
The code transfer to deployment is automated process, hence the keyword continuous.

Deliver Pipeline
Jenkins pipeline
Multi-branch pipeline

------------------------------------------------
Setting up delivery pipeline
Create three job - Build, Deploy, test
Now create delivery pipeline view - install delivery pipeline
Click on new view - select delivery pipeline view
View Name- DelPipeLineView
select all default setting
Pipeline - add -Select initial job - name and select Build job

Now build the initial job - build job
Now all three job are showing in DelPipelineview

Some more option - edit view:
Enable start of new pipeline build - this check box allows us to trigger build from pipeline view screen
Enable rebuild - it will gives us to rebuild one of the job.

---------------------------------------------------------------------
Setting up Build Pipeline
Install Build pipeline plugin

Its a better way to check logs, each and every job
some shortcut - run, add job, delete job , manager plugin
----------------------------------------------------------------------
Jenkins Pipeline
When we setup a large complex project delivery and build pipeline is not a good option, thus jenkins pipeline comes.
It is a suite of jenkins features, installed as plugins, which enable implementation of continuous delivery pipelines which are the automated processes for getting softeare from source control deployment to end users.

Supports building continous Delivery pipeline through either a web UI or scripted jenkins file. These are codeed in the groovy DSL.
2 ways of coding a jenkins pipeline - Declarative is a recent feature and very powerful.

Key features - Code your pipeline
Durability
Handles User input
Parallel Job execution
Complex Pipelines Possible

Diff declarative Pipeline VS Scripted Pipeline
Declarative: Recent features in jenkins and uses a simpler groovy syntax
Code written locally in a file & is checked in to the SCM.
Code is written within a pipeline block

Scripted: Traditional way writing jenkins pipeline with a stricter groovy syntax.
Code is written directly on the jenkins instance.
Code is written within a node block.

Pipeline concept:
Step: A Step refers to the single task that has to performed within a stage.
Stage: A stage block defines a conceptually distinct subset of tasks.
Pipeline: A Pipeline is a user defined model of a CD pipeline.
Node: A Node is a machine which is a part of jenkins environment.


------------------------------------------------------------------------------------------------

Create Scripted jenkins pipelin:
node {  
    stage('Build') { 
        echo "Inside the build stage" 
    }
    stage('Test') { 
       ech "Inside the Test stage" 
    }
    stage('Deploy') { 
       echo "Inside the deploy Stage"
    }
}

https://github.com/mrinaldutt/jenkinsrepo.git

node {
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git branch: 'main', url:'https://github.com/mrinaldutt/jenkinsrepo.git'
    }
    stage('Build') {
        // Run the maven build
        dir('TestNG'){
            
            bat "mvn clean test"
        }
    }
    stage('Package') {
        // Run the maven pcakgae
        dir('TestNG'){
                bat "mvn package"
        }
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'TestNG/target/*.jar'
    }
}



-----------------------------

=========================Pipeline===========================
Jenkinsfile (Declarative Pipeline): No code 
pipeline {
	agent any 
	
	environment{
		secret = credential('TEST')
	}
	stages {
		stage('example stage') {
			steps {
				sh 'echo $secret'			
				}	
			}
		stage('Build') {
			steps {
				
				}	
			}
		stage('Test'){
			steps {
				
				}
			}
		stage('Deploy') {
			steps {
				retry(3){
					 echo 'I am not going to work :c'	
					}
				
				timeout(time:3, unit: 'SECONDS') {
					sh 'sleep 5'
				}
			
				}
			}
		stage('Timeout') {
			steps {
				retry(3){
					  echo 'I am not going to work :c'	
					}
			
				}
			}	
		}
	}	

Scripted Pipeline: written code using groovy or java
node {  
    stage('Build') { 
        echo "Inside the build stage" 
    }
    stage('Test') { 
       echo "Inside the Test stage" 
    }
    stage('Deploy') { 
       echo "Inside the deploy Stage"
    }
}



------------------------------
Declarative Pipeline
Jenkinsfile:
pipeline{ 
  agent any
  stages{
    stage("Cleaning Stage") { 
        steps{
		       dir('TestNG'){
			       bat "mvn clean"
		       }
	      }
    }
    stage("Testing Stage") { 
       steps{
		        dir('TestNG'){
				bat "mvn test"
			}
	    }
    }
    stage("Packaging Stage") { 
       steps{
		       dir('TestNG'){
			       bat "mvn package"
		       }
	    }
    }
  }
}

-------------------------
takes user input/prompt in declaraive pipeline:
add below stage:
stage("Consolidate Results") {
			steps {
				input ("Do you want to capture results?")
				junit '**/target/surefire-reports/TEST-*.xml'
				archive 'TestNG/target/*.jar'
			}
		}
-------------------------
adding email:
stage("Email Build Status"){
			steps {
				mail body: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult} \n\nCheck console output at ${env.BUILD_URL} to view the results.", subject: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult}!!", to: 'awstests2020@gmail.com'
			}
		}

Complete Jenkinsfile:
pipeline{ 
  agent any
  stages{
    stage("Cleaning Stage") { 
        steps{
		       dir('TestNG'){
			       bat "mvn clean"
		       }
	      }
    }
    stage("Testing Stage") { 
       steps{
		        dir('TestNG'){
				bat "mvn test"
			}
	    }
    }
    stage("Packaging Stage") { 
       steps{
		       dir('TestNG'){
			       bat "mvn package"
		       }
	    }
    }
    stage("Consolidate Results") {
			steps {
				input ("Do you want to capture results?")
				junit '**/target/surefire-reports/TEST-*.xml'
				archive 'TestNG/target/*.jar'
			}
		}
    stage("Email Build Status"){
			steps {
				mail body: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult} \n\nCheck console output at ${env.BUILD_URL} to view the results.", subject: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult}!!", to: 'awstests2020@gmail.com'
			}
		}	  
  }
}
-------------------------
Submit Stages in parallel:
pipeline{ 
  agent any  
  stage("Parallel Execution") {
			steps {
				parallel(
				      a: {
					dir('TestNG'){
			       			bat "mvn clean"
		       			}
				      },
				      b: {
					dir('TestNG'){
						bat "mvn test"
					}
				      },
				      c: {
					dir('TestNG'){
					bat "mvn package"
					}
				      }
				)
			}
		}  
    stage("Consolidate Results") {
			steps {
				input ("Do you want to capture results?")
				junit '**/target/surefire-reports/TEST-*.xml'
				archive 'TestNG/target/*.jar'
			}
		}
    stage("Email Build Status"){
			steps {
				mail body: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult} \n\nCheck console output at ${env.BUILD_URL} to view the results.", subject: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult}!!", to: 'awstests2020@gmail.com'
			}
		}	  
  }
}








