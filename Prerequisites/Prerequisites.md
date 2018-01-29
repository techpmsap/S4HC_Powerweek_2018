<table width=100% border=>
<tr><td colspan=2><h1>PREREQUISITES</h1></td></tr>
<tr><td><h3>SAP Partner Workshop</h3></td><td><h1><img src="images/clock.png"> &nbsp;30 min</h1></td></tr>
</table>


## Description
In this exercise, you’ll go through the basic steps of setting up the development environment required for S/4HANA Cloud extension workshop.


## Target group

* Application Developers
* People interested in learning about S/4HANA extension and SDK  


## Goal

The goal of this exercise is to have your workstation well prepared in order to attend to the S/4HANA Cloud extension workshop.


## Prerequisites
  
Here below are prerequisites required for the exercises in this workshop.

1. [Install Eclipse Oxygen](#install-eclipse-oxygen)
1. [Install SAP Cloud Platform Eclipse Oxygen Plugins](#install-cp-oxygen-plugin)
1. [Install Java JDK](#install-java-jdk)
1. [Configure Eclipse Oxygen Java preference](#configure-eclipse-java)
1. [Install SAP Cloud Platform SDK](#install-cp-sdk)
1. [Create New Runtime Environment](#create-runtime-environment)
1. [Sign up for SAP Cloud Platform Neo trial account](#sign-up-neo)
1. [Sign up for SAP Cloud Platform Cloud Foundry trial account](#sign-up-cf)
1. [Install latest LTS version of NodeJS ](#install-nodejs)
1. [Install Cloud Foundry CLI](#install-cf-cli)
1. [Install Apache Maven for Windows/Mac](#install-maven)
1. [Check if Eclipse/Maven is installed and Java set-up is done correctly](#check-eclipse-maven)


### <a name="install-eclipse-oxygen"></a>Install Eclipse Oxygen
Eclipse Oxygen IDE is required for Java application development during the workshop.

1.	Download and install **Eclipse Oxygen IDE for Java EE Developers**

	#### For Windows:
	<http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/oxygen/1a/eclipse-jee-oxygen-1a-win32-x86_64.zip>  
	![](images/01.png)

	#### For Mac:
	<https://www.eclipse.org/downloads/download.php?file=/oomph/epp/oxygen/R/eclipse-inst-mac64.tar.gz>  
	![](images/02.png)


### <a name="install-cp-oxygen-plugin"></a>Install SAP Cloud Platform Eclipse Oxygen Plugins
Install SAP Cloud Platform Eclipse Oxygen Plugins

1.	Open **Eclipse Oxygen**
1. Click on **Help -> Install New Software…**  
	![](images/02_02.png)
1. Enter this link <https://tools.hana.ondemand.com/oxygen/> and hit <ENTER>, type a description for this repsitory and click **OK**  
	![](images/02_03.png)
1. Select **SAP Cloud Platform Tools** and click **Next**   
	![](images/02_04.png)
1. Click **Next**  
	![](images/02_05.png)
1. Accept the license agreement and click **Finish**  
	![](images/02_06.png)
1. Select **Install anyway**  
	![](images/02_07.png)
1. Click **Restart Now** to restart Eclipse  
	![](images/02_08.png)


### <a name="install-java-jdk"></a>Install Java JDK
Eclipse IDE needs Java JDK.

1.	Download and install Java JDK from this link <http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>  
	![](images/04.png)


### <a name="configure-eclipse-java"></a>Configure Eclipse Oxygen Java preference
Make sure Eclipse IDE uses right JREs.

1.	Click on **Window->Preferences**. This should open the Preferences window. If you are on MAC you can find Preferences item under the Eclipse menu  
	![](images/04_02.png)
1. Search for **Installed JREs**
	![](images/05.png)

> NOTE: Make sure that the location is pointing your Java JDK 1.8 instead of your Java JRE
![](images/06.png)

	 
### <a name="install-cp-sdk"></a>Install SAP Cloud Platform Neo Environment SDK
Neo commands used during S/4HANA extension development are part of SAP Cloud Platform SDK.

1. Download the latest version of Java Web Tomcat 8 Neo Environment SDK from here <https://tools.hana.ondemand.com/#cloud>
	![](images/07.png)
1. Extract it in a folder on your disk

 
### <a name="create-runtime-environment"></a>Create New Runtime Environment
During Java application deployment to SAP Cloud Platform, you will be using Java EE 6 Web Server runtime.

1. Download the latest version of Java EE 6 Web Profile from here <https://tools.hana.ondemand.com/#cloud>  
	![](images/07_02.png)
1. Extract it in a folder on your disk
1.	From Eclipse Oxygen, go to **Preferences** window. Search for **runtime** and, under the path **Server->Runtime Environments** click **Add**  
	![](images/08.png)
1.	Under **SAP** catalog, select **Java EE 6 Web Profile** and click **Next**  
	![](images/09.png)
1.	Browse to the location of the Java EE 6 Web Profile SDK folder you have just extracted and click **Finish**  
	![](images/10.png)
1.	Java EE 6 Web Profile is installed. Click on **Apply and Close**    
	![](images/10_02.png)


 

### <a name="sign-up-neo"></a>Sign up for SAP Cloud Platform Neo trial account
You need Neo trial SAP Cloud Platform to complete standalone hands-on exercise for Workflow Service and Business Rules Service. 

1.	Sign up for SAP Cloud Platform trial account from <https://account.hanatrial.ondemand.com/>
	![](images/11.png)
> NOTE: If you don’t have an account on SAP Cloud Platform yet, go to the Sign up for a free trial account tutorial, and then come back to this step.

1. After you have logged in, click on **Home**.  Then, click on **Neo Trial**  
	![](images/12.png)
1. This will take you to the **Overview** page of the SAP Cloud Platform Cockpit for Neo stack
	![](images/13.png)
1.	From SAP Cloud Platform Cockpit, click on Services. Enable the following services
	- Portal	 
	- SAP Web IDE Full-Stack
	- Workflow
	- Business Rules
	![](images/14.png)
	
> **NOTE**: Please, if possible, enable Portal as first service.
        
### <a name="sign-up-cf"></a>Sign up for SAP Cloud Platform Cloud Foundry trial account
Sign up also for SAP Cloud Platform Cloud Foundry trial account.

1.	From SAP Cloud Platform Cockpit, click on Home.  Then, click on **Cloud Foundry Trial**. Select a **Region**, for example, US East (VA) or Europe (Frankfurt)  
	![](images/15.png)
1.	Select the Global account that matches your login. Next, select the trial sub-account.
	![](images/16.png)	 
1.	Make sure you have **2GB Memory** for the space.  If you don’t have 2GB Memory, please register a new account.
	![](images/17.png)


### <a name="install-nodejs"></a>Install latest LTS version of NodeJS
Install latest LTS version of NodeJS: it will be required in exercise 11.

1.	From Building Latest LTS version of NodeJS download it here
	![](images/18.png)


### <a name="install-cf-cli"></a>Install Cloud Foundry CLI
Install Cloud Foundry CLI  

1.	Cloud Foundry CLI download it here <https://github.com/cloudfoundry/cli#downloads>
	![](images/19.png)


### <a name="install-maven"></a>Install Apache Maven for Windows/Mac
You might need Maven tool installed on you workstation. Here are the steps to install Maven.

#### WINDOWS

1.	Install Chocolatey (a package manager for Windows)

```sh	
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

2.	Install Maven

```sh
	choco install maven
```

#### MAC

1.	Install HomeBrew (a package manager for Mac)

```sh	
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2.	Install Maven

```sh
	brew update
	brew install maven
```


### <a name="check-eclipse-maven"></a>Check if Eclipse/Maven is installed and Java set-up is done correctly
Check if eclipse/Maven is installed and Java set-up is done correctly. 
Building successfully a Maven-based Java project in your Eclipse is a prerequisite.
Now you are ready to test if can build and run a Java Web application project with Maven in your Eclipse IDE. For this test we prepared a Maven-based HelloWorld Java project as follows.

1. Download the archive file [helloworld.zip](https://sap.github.io/cloud-s4ext/week-1/unit-5/imports/java/helloworld.zip?raw=true).
1. Extract the *helloworld.zip* archive to a directory of your choice
1. From the Eclipse menu, choose **File->Import…** to open the Import wizard  
	![](images/20.png)
1. Choose **Maven->Existing Maven Projects** and click **Next**  
	![](images/21.png)
1. In the Import Maven Projects dialog:
	- Click **Browse** and select the helloworld directory where you have extracted the *helloworld.zip*
	- The *helloworld/pom.xml* will be listed in the Projects section
	- Select the checkbox of this *pom.xml*
	- Choose **Finish** to start importing the Maven project into your Eclipse workspace
	![](images/22.png)  
	
	> **Info**: POM is an acronym for Project Object Model. It is an XML representation of a Maven project held in a file named pom.xml. For more information see the Maven documentation

1. In the Project Explorer view of the Java EE Perspective you should find now the imported *helloworld*  
	![](images/23.png)
1. Right-click on the *helloworld* project node to open the Context Menu. Choose **Run As->Maven install** to start the Maven build for the *helloworld* project  
	![](images/24.png)
1. The Eclipse IDE will open a Console Tab that displays the build progress. You should see **BUILD SUCCESS**. If your build was not successful, please check the troubleshooting guide for Maven  
	![](images/25.png)
1. In Project Explorer view expand the project node **helloworld->target** to find the built *helloworld.war* file.

	> Note: To see it you might have to refresh the project by right-clicking on the project-node and press Refresh  
	
	![](images/26.png)
	
1.  Maven has build successfully the *helloworld* Java web application and created a *helloworld.war* file (see console output for the location).


## Summary
You have successfully completed the prerequisites installation.
