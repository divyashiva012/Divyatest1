


Discover Financial Services





Design Document 

Draft Version: 0.1

Version	Date	Change Summary	Created/Updated By
0.1	03/15/2020	Initial version	Sagar Valagerehally Shankaraiah
			
			





 
	Table of Context	
 
BRANCHES FOR APPLICATIONS
Monitor the quality of branches in your Applications, after choosing which branches to track in underlying projects.

Why Use Branch Analysis in SonarQube?
Issue metadata shared across branches
Focus on issues created within each branch
Branch-specific Quality Gates and Leak Periods

BRANCH TYPES
Main
Default branch
Must be scanned first (ex. ‘master’)

Long-Lived
Exist until removed
Configurable leak period
May be a parent branch 
Can be included in Applications (ex. ‘develop’, ‘release’)

Short-Lived
Exist until inactive 
One leak period (ex. feature branches, pull requests, hotfixes)

BRANCH DESIGNATION 
Main branch 
First branch scanned without sonar.branch.name is ‘master’ and main 
Rename via UI or API 
Long-lived branches 
Controlled by regex, if sonar.branch.namematches are long-lived 
Global Setting @ Administration > General > Branches 
Project Setting @ Project > Administration > Branches & Pull Requests 
Short-lived branches 
Everything else... 

PULL REQUEST ANALYSIS
Adding to the analysis of feature and maintenance branches, you can now check the quality of your Pull Requests. Only commit clean, safe code.

PR analysis allows users to:
See PR's Quality Gate status in the SonarQube UI.
Automatically decorate PRs with SonarQube issues in your SCM provider's interface.
Focuses on new code – The PR quality gate only uses your project's quality gate conditions that apply to "on New Code" metrics.
Assigns a status – Each PR shows a quality gate status reflecting whether it Passed (green) or Failed (red).
When PR decoration is enabled, SonarQube publishes the status of the analysis (Quality Gate) on the PR.
PR analyses on SonarQube are deleted automatically after 30 days with no analysis. 


GITHUB ENTERPRISE INTEGRATION
Configuring sonarqube instance on GitHub Enterprise to enable Pull Request 
https://docs.sonarqube.org/latest/instance-administration/github-application/ 

APPLICATIONS
An Application is an aggregation of projects into a synthetic project. Assume you have a set of projects which has been split for technical reasons, but which shares a lifecycle; they interact directly in production and are always released together. With an Application, they can be treated as a single entity in SonarQube with a unified Project Homepage, Issues list, Measures space, and most importantly: Quality Gate.

PORTFOLIO
The Portfolio Home Page is the central place for managers and tech leads to keep an eye on the Releasability of the projects under their supervision. Releasability is based on the project's quality gate: Passed is releasable and Failed is not. Each Portfolio home page offers an aggregate view of the releasability of all projects in the Portfolio.
At the top of the page, you can easily see whether the overall Portfolio is currently rated as releasable and if any projects in the Portfolio have failed their Quality Gate. And the Reliability, Security Vulnerabilities, Security Review, and Maintainability ratings show the overall health of the Portfolio in these three domains, along with an indicator of the worst-performing project(s) in each domain.
For each domain, you'll see:
•	the rating (see Metric Definitions for more details about how they are computed)
•	an indicator of when the rating last changed
•	an indicator of the worst-performing project(s) in the domain

Projects Quality Gate Ratio	Releasability Rating
>80%	
E
>60%	
D
>40%	

>20%	
B
<=20%	


Reliability, Security Vulnerabilities, Security Review, and Maintainability Ratings
The Reliability, Security Vulnerabilities, Security Review, and Maintainability ratings for a Portfolio are calculated as the average of the ratings for all projects included in the Portfolio. 
SonarQube converts each project's letter rating to a number (see conversion table below), calculates an average number for the projects in the portfolio, and converts that average to a letter rating. Averages ending with .5 are rounded up resulting in the "lower" of the two possible ratings, so an average of 2.5 would be rounded up to 3 and result in a "C" rating).
This gives an "problem density" measure on the four axes of Reliability, Security Vulnerabilities, Security Review, and Maintainability for your Portfolio.
Rating conversion:
E : 5
D : 4
C : 3
B : 2
A : 1

APPLICATIONS VS. PORTFOLIOS
Applications and Portfolios are both aggregations of projects, but they have different goals and therefore different presentations. A Portfolio is designed to be a very high-level, executive overview that shows how a package of projects that may only be tangentially related are doing quality-wise, and what the trends are. Applications allow you to see your set of projects as a larger, overall meta-project. For instance, because all the projects in an application ship together, if one of them isn't releasable then none of them are, and an Application's consolidated Quality Gate gives you an immediate summary of what must be fixed across all projects in order to allow you to release the set.

KEY CONCEPTS
1.	RULES
Language-specific
Many are common across multiple languages 
Delivered via plug-ins 
Explored via the Rule section 
Grouped in Quality Profiles 
2.	ISSUES
Created when a Rule is violated during a scan 
Assigned to user using SCM account + blame data via QC or GitHub Integration
Issues can be Resolved by... 
Fixing the code and close the defect
Defer the defect
3.	QUALITY PROFILES
Set of Rules to be applied to a language
Built in “Sonar Way” available for all languages
May be customized or extended for other profiles
Severity is customizable
Assigned to Projects
Requires “Administer Quality Profile” privilege
4.	KEY METRICS
Bugs, Vulnerabilities, Code Smells and associated Ratings 
Coverage 
Duplications 
Complexity (Cognitive preferably) 


5.	SECURITY AND RELIABILITY RATING
Severity	Rating
Blocker	
E
Critical	
D
Major	

Minor	
B
Info	



6.	Maintainability Rating 
Tech Debt (TD): Total effort to fix all CODE SMELL issues 
TD Ratio: Tech Debt / Effort to entirely rewrite the code 
Example: 1 project with 
120 issues - Technical Debt: 1120 min = 18.6 h = 2.3 days 
1500 LoC - Total rewrite effort = 1500 x 30 min = 45000 min 
Tech Debt Ratio = 1120 / 45000 = 2.5% 

Maintainability Rating:  

Tech Debt Ratio	Maintainability Rating
0-5%	
E
5-10%	
D
10-20%	

20-50%	
B
>50%	



7.	QUALITY GATE
FIVE levels of Quality Gates will be defined, each level will have linear growth of rules to maximise the Quality of application. Quality Gates will be categories from A to E. Where A will be the Highest achivable and E will be the lowest achivable. 

R A C I
 

ONBOARD NEW APPLICATIONS 

Generic / Process ID will be used to process all SonarQube Adminstrative tasks which will have all required permission to create Application, Portfolio, Project, Branch, etc,..

A series of tasks needs to be performed to onboard a new application to SonarQube

Task 0 – Pre-requisite 
Create LAN Group “<LAN_Group_Sonar>” – App Team’s Responsibility

Create the LDAP group with the <LAN_Group_Sonar> (Ex:)

Step 1
Create Group in Sonar

Step 2
Create Permission Template

Step 3
Create Application

Key must be 3-Char App code followed by underscore Application. (Ex: ABC_Application)
Application name must be 3-Char App Code followed by space hyphen space followed by Application full name. 

Step 4
Add project to Application

Step 5
Create Porfolio

Step 6
Add project to portfolio


Step 7
Make Application Private

Step 8
Make Portfolio Private


Step 9
Execute Project Analysis with Master Branch (No Code Scan)
All application projects which correcsponse to Git Repo created must be added to Application. 

Step 10
Make project private

Step 11
Create Branch(s)


Step 12
Apply permission to the projects, Application and Portfolio








 



EXECUTE ANALYSIS 

Analysis will be linked between GitHub Branch to SonarQube Branch

Project Version should be trackable details

Scanner Configuration
All Jobs (All are mandatory)
sonar.projectKey
sonar.sources
sonar.projectVersion
sonar.branch.name 
sonar.branch.target

INTEGRATION
 
SCANNER ECOSYSTEM

LAUNCHING SCANS
      
     

SCANNING C/C++/OBJECJIVE-C
 
Examples: 
        build-wrapper-linux-x86-64 --out-dir mytempdir make -f makefile clean all
        sonar-scanner -Dsonar.cfamily.build-wrapper-output=mytempdir
        build-wrapper-macos-x86 --out-dir bw xcodebuild
        sonar-scanner -Dsonar.cfamily.build-wrapper-output=bw
        build-wrapper-win-x86-32 --out-dir “my temp dir” msbuild /t:rebuild
        sonar-scanner -Dsonar.cfamily.build-wrapper-output=”my temp dir”


SCANNER FOR JENKINS

	Pre-Configure pipeline jobs
NARROWING THE FOCUS
Don’t scan generated code or code from 3rd-party libraries
Excluding code - sonar.exclusions/sonar.test.exclusions
Including only specified code - sonar.inclusions/sonar.test.inclusions
# Exclude all classes ending by "Bean"
# Matches org/sonar/api/MyBean.java, org/sonar/util/MyOtherBean.java, org/sonar/util/MyDTO.java, etc.
sonar.exclusions=**/*Bean.java,**/*DTO.java
# Exclude all classes in the "src/main/java/org/sonar" directory
# Matches src/main/java/org/sonar/MyClass.java, src/main/java/org/sonar/MyOtherClass.java
# But does not match src/main/java/org/sonar/util/MyClassUtil.java
sonar.exclusions=src/main/java/org/sonar/*
# Exclude all COBOL programs in the "bank" directory and its sub-directories
# Matches bank/ZTR00021.cbl, bank/data/CBR00354.cbl, bank/data/REM012345.cob
sonar.exclusions=bank/**/*
# Exclude all COBOL programs in the "bank" directory and its sub-directories whose extension is .cbl
# Matches bank/ZTR00021.cbl, bank/data/CBR00354.cbl
sonar.exclusions=bank/**/*.cbl
NAMING STANDARDS  
Application teams must adhere to naming conventions for project naming. The framework for naming your resources and spaces is designed in a way that allows identification, describes the application name. 
General rules: 
All lowercase characters
– By default, use underscores for spaces and collon as separator unless noted otherwise
– By default, {descriptor} length is 30 characters unless noted otherwise 
Resource naming formats: 
–{project-id}_{projectname} for Project Key
–{appid}_{projectname} for Project Name
–{project-id}_Application for Application Key
–{project-id}_{appname} for Appliaction Name
–{project-id}_Portfolio for Portfolio Key
–{project-id}_{appname}_Portfolio for Protfolio Name


Additional Information:

  
Escalation of Non-Compliance:
First Level: CDI@discover.com
Second Level: 
Third Level: 
Hell broke loose: 

APPENDIX

https://docs.sonarqube.org


Key Term Definitions and Acronyms:


