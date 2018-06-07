<table width=100% border=>
<tr><td colspan=2><h1>EXERCISE 32 - Machine Learning APIs Exploration</h1></td></tr>
<tr><td><h3>SAP Partner Workshop</h3></td><td><h1><img src="images/clock.png"> &nbsp;50 min</h1></td></tr>
</table>


## Description
In this exercise, you’ll learn how 

* to consume pretrained SAP Leonardo Machine Learning services from SAP API Business Hub sandbox in a SAPUI5 application

## Target group

* Developers
* People interested in SAP Leonardo and Machine Learning 


## Goal

In this exercise you can experience how easy it is to use the available SAP Leonardo Machine Learning foundation services on SAP API Business Hub. The models are already pre-trained and can be tried out on the web page.


## Prerequisites
  
Here below are prerequisites for this exercise.

* A trial account on the SAP Cloud Platform. You can get one by registering here <https://account.hanatrial.ondemand.com>
* Download the files [Topic_Detection.zip](files/Topic_Detection.zip?raw=true) and [test_images.zip](files/test_images.zip?raw=true) and save them in a proper location: they will be used later in this document.

>NOTE: only *test\_images.zip* file must be extracted in your folder


## Steps

1. [Use SAP Leonardo ML Topic Detection on API Business Hub](#topic-detection)
1. [Use SAP Leonardo ML Image Classification on API Business Hub](#image-classification)
1. [Setup the Development Environment](#setup-dev-env)
1. [Use SAP Leonardo ML Image Classification with SAPUI5](#image-classification)
1. [Adjust the prepared SAPUI5 application to access your ML foundation services](#adjust-app)

 

### <a name="topic-detection"></a> Use SAP Leonardo ML Topic Detection on API Business Hub
1. Open SAP Business Hub in your browser <https://api.sap.com>  
	![](images/01.png)

	>NOTE: Please use Firefox to avoid the SSO login [for SAP Employees only].

1. 	Click on **Try New Design** so that you can start trying the new design has been rolled out for the API Hub  
	![](images/02.png)

1. 	Enter the text "Leonardo" in the search box, hit ENTER and choose **SAP Leonardo Machine Learning - Functional Services**  
	![](images/03.png)

1. 	Enter the text "Topic" in the search box, hit ENTER and choose **Topic Detection API**  
	![](images/04.png)

1. We need to login to test the service: click on the **Log On** button at the top right corner  
	![](images/05.png)

1. Enter the credentials of your SAP Cloud Platform trial account and click **Continue**  
	![](images/06.png)

1. Expand the **POST** request **/inference_sync**  
	![](images/07.png)

1. Scroll down to the **PARAMETERS** and under **options**, paste the following parameters  
	
	```json
	{"numTopics":3, "numTopicsPerDoc":2, "numKeywordsPerTopic":15}
	```	
	![](images/08.png)

1. Under **files** press the **Browse** button  
	![](images/09.png)

1. Choose the *Topic_Detection.zip* file (you have already downloaded it in the prerequisites section) containing text files about computer science and pies  
	![](images/10.png)

1. The name of the selected file appears aside the **Browse** button. Click on  **Try out** button  
	![](images/11.png)

1. You should receive a **Response Code** of **200**. Check the result in the **Response Body**: you should see a content like this  
	![](images/12.png)

1. Try again by changing the values for **numTopics** to **2** and **numTopicsPerDocs** to **1**  
	![](images/13.png)

1. What has changed? You should receive an answer similar to this  
	![](images/14.png)

1. You have completed the exercise! You have successfully used the Topic Detection API service to find **numKeywordsPerTopic** keywords and **numTopics** topics across all documents. The topics get a number, starting with 0. So, if you define 3 Topics, they will be numbered with 0, 1, 2. With **numTopicsPerDoc** you define how many of the topics of the entire document corpus can be found in one document. The algorithm chooses the number of topics which fits best and assigns them a score which is not normalized to 1.  


### <a name="image-classification"></a> Use SAP Leonardo ML Image Classification on API Business Hub

1. Go back to <https://api.sap.com/shell/discover/contentpackage/SAPLeonardoMLFunctionalServices/Artifacts>
	![](images/15.png)

1. 	Enter the text "image" in the search box, hit ENTER and choose **Image Classifier Service**  
	![](images/16.png)

1. Expand the **POST** request **/inference_sync**  
	![](images/17.png)

1. Click on the **Browse...** button for the **files** parameter  
	![](images/18.png)

1. Select one of the images you have in the folder where you have extracted the test_images.zip file given in the prerequisites. For example choose the *tennis\_ball.jpg* file. then click on the **Try out** button  
	![](images/19.png)

1. Look at the response code: it should be 200, meaning that the request was successful. Then look at the response body: you should be able to read the predictions against the image you uploaded with their scores  
	![](images/20.png)

1. Congratulations! You have completed the exercise.

### <a name="setup-dev-env"></a> Setup the Development Environment
For the exercises where we develop SAPUI5 and Java applications, we will work with the SAP WebIDE in SAP Cloud Platform. To save time, we prepared a project for you so that we can focus on the ML Foundation parts. This project needs to be imported into your SAP Web IDE workspace. You will extend the applications included in the project to test the SAP Leonardo ML services. 
In this chapter, you will initialize the SAP Web IDE and import the given project. It will be used later in the corresponding exercises.

Required resources for this step:

* [MLFSAPUI5\_Project\_Exercise.zip](files/MLFSAPUI5_Project_Exercise.zip?raw=true)
* [MLFSAPUI5\_Project\_Solution.zip](files/MLFSAPUI5_Project_Solution.zip?raw=true) (only required if you get stuck with the exercise and you want to go straight to the solution)

1. Open Firefox, as Chrome will use SSO for SAP Employees, and navigate to SAP Cloud Platform Cockpit via <http://cloudplatform.sap.com>  
	![](images/01b.png)

1. Login with your given e-Mail 
**ml-train+XX@sap.com**, where **XX** must be replaced by your workstation ID, and the password provided by the trainer. 
	![](images/02b.png)

1.	Click on **Neo Trial**

	![](images/03b.png)

	> NOTE: The SAP Web IDE Full-Stack version is provided with the SAP CP Neo environment, but it can deploy to both SAP CP Cloud Foundry and Neo. 

1.	In the left menu bar, navigate to **Services** and search for "web". You will get two flavours of the SAP Web IDE. We will use the **SAP Web IDE Full-Stack** version as this is the one which supports both SAP Cloud Foundry and Neo 
	![](images/04b.png)

1.	Click on **Go to Service**  
	![](images/05b.png)

1. This will open up the SAP Web IDE. 
	![](images/06b.png)

1. Click on the **Development** tab on the left toolbar. If you see that there is already a project named *MLFSAPUI5\_Project\_Exercise* in the workspace, please right click on its name and choose **Delete**  
	![](images/07b.png)

1. You should start with a completely empty workspace like the one in the picture  
	![](images/08b.png)

1.	From the **File** menu click on **Import -> File or Project**  
	![](images/09b.png)

1.	Browse in your file system for the file you have already downloaded in the prerequisites section (*MLFSAPUI5\_Project\_Exercise.zip*), keep the proposed folder in the "Import to" field, make sure that the **Extract Archive** option is selected and click **OK**  
	![](images/10b.png)

	We will need this project later in the next exercises when you develop SAPUI5 apps to call ML Foundation services

1.	You should see a files and folder structure similar to the one shown on this screenshot

	![](images/11b.png)

1. You have successfully imported the exercise project in SAP Web IDE.


### <a name="image-classification"></a> Use SAP Leonardo ML Image Classification with SAPUI5
In this exercise you will learn how to quickly integrate in a SAPUI5 application the Image Classification provided by the SAP Leonardo Machine Learning Functional Services and published in the SAP API Business Hub sandbox. These will be the steps you will go through:

* Import a SAPUI5 application calling a REST service (see prerequisites)
* Create a destination in SCP Cockpit to your ML Service endpoint in API Business Hub
* Use the API Key for the image and product image classification from SAP API Business Hub
* Adjust your prepared SAPUI5 application
* Run the SAPUI5 application and test your ML Services.

1.	Open a new tab in your Firefox web browser and go to SAP Cloud Platform Cockpit <http://account.hanatrial.ondemand.com/cockpit>. Login in case you are not already logged in by using the given credentials and not SSO  
	![](images/12b.png)

1.	Click on the **Neo Trial** tile  
	![](images/13b.png)

1.	On the left side bar, select **Connectivity -> Destinations**. You need now to install the webide_di destination: if this destination is already existing, please continue with step 10  
	>NOTE: This destination is only required by SAP Web IDE to run applications in Web Preview mode: it's not related to ML

	![](images/14b.png)

1. Download the destination from by right clicking [here](files/webide_di.txt?raw=true) and choosing save to disk

1. Once the destination has been downloaded, click on **Import Destination**, browse for the file you have just downloaded and import it  
	![](images/15b.png)

1. Replace the account in the destination URL with your account  
	![](images/16b.png)

1. Save the destination  
	![](images/17b.png)

1. Once you have imported it you should have only this destination in your system. Click on **Check Connection** to test if the destination is working fine  
	>NOTE: If you see any other destination in your system please delete it

	![](images/18b.png)

1. You should receive a status code of **200**   
	![](images/19b.png)

1.	Click on **New Destination**  
	![](images/20b.png)

1.	Enter the following information and click on the **New Property** button   

	|Parameter|Value|
	|---------|-----|
	|Name|sapui5ml-api|
	|Type|HTTP|
	|Description|SAP Leonardo Machine Learning APIs|
	|URL|https://sandbox.api.sap.com/ml|
	|Proxy Type|Internet|
	|Authentication|NoAuthentication|

	![](images/21b.png)

1. Add the property **WebIDEEnabled = true** to the destination and click **Save**
	![](images/22b.png)

1.	You can use the **Check Connection** button to validate that the URL can be accessed 
	![](images/23b.png)

1. The response should be `Connection to "sapui5ml-api" established. Response returned: "404: Not Found"`  
	![](images/24b.png)





### <a name="adjust-app"></a> Adjust the prepared SAPUI5 application to access your ML foundation services
For the exercises where we develop SAPUI5 and Java applications, we will work with the SAP WebIDE in SAP Cloud Platform. To save time, we prepared a project for you so that we can focus on the ML Foundation parts. This project needs to be imported into your SAP Web IDE workspace. You will extend the applications included in the project to test the SAP Leonardo ML services. 

1.	Go to your SAP Web IDE Full-Stack edition and open the file  *MLFSAPUI5\_Project\_Exercise/neo-app.json*  
	![](images/25b.png)

1. Add a new route to the new destination named **sapui5ml-api**, we previously created in the SAP CP cockpit. You can copy the following code into the file (pay attention to the first comma which separates this from the previous resources)

	```json
	,
	    {
	    	"path": "/ml",
	    	"target": {
	    		"type": "destination",
	    		"name": "sapui5ml-api"
	    	},
	    	"description": "ML API description"
	    }
	```
	![](images/26b.png)

1.	Scroll to the end of the *neo-app.json* file and add the String **"APIKey",** (pay attention to include the comma) to the **headerWhiteList** section and then **save** the file. This is how the file should look after these operations  
	![](images/27b.png)

1.	Open the file *MLFSAPUI5\_Project\_Exercise/webapp/model/settings.json*
	![](images/28b.png)

1. Before we proceed with editing the *settings.json*, we need to get the **API Key** for the ML services from the API Business Hub, explained in the next steps

1.	Go to <https://api.sap.com> and click on **Try New Design**
	![](images/29b.png)

1.	Click on the **Log On** button on the top right corner and login with the credentials provided by your instructor  
	![](images/30b.png)

1.	Once logged in, click on the drop down list in the top right corner of the screen and choose **Preferences**  
	![](images/31b.png)

1.	Click on **Show API key**
	![](images/32b.png)

1. Click on **Copy Key and Close**: the API key gets copied in your clipboard  
	![](images/33b.png)

1. Now go back to your SAP Web IDE in SAP Cloud Platform, where the *settings.json* is still open.
For the two urls "Image Classification" and "Product Image Classification" replace the 
**<<<< COPY YOUR API KEY >>>>**  with the API key you copied in the clipboard and **save** the file
	![](images/34b.png)

1.	Click on the **Run** icon on the toolbar to execute the application   
	![](images/35b.png)

1. An application with two tiles comes up. Select the tile with the title **Image Classification**
	![](images/36b.png)

1. Extract the 4 images contained in the zip file ([test_images.zip](files/test_images.zip?raw=true)) you have downloaded already as explained in the prerequisites  

1. Select the *tennis_ball.jph* image and drag & drop it onto the camera icon
	![](images/37b.png)

1. The application charts the 5 most probable classifications for the image. To see the actual response from the server you can press the "View JSON" Button 
	![](images/38b.png)

1. Do the same for the other images by either dragging & dropping the selected image onto the icon or pressing the icon itself to open a file select dialog. Analyze the results

1. This concludes the exercise.




## Summary
This concludes the exercise. You should have learned how to use the available SAP Leonardo Machine Learning foundation services on SAP API Business Hub.

You are now able to:

* Browse through API Business Hub to find the latest functional and business services of SAP Leonardo ML foundation
* Test SAP Leonardo ML foundation services directly on API Business Hub
* Understand the Topic Detection Model.
* Use the SAP Web IDE to import a SAPUI5 application
* Create a destination that points to your ML service API endpoint in SAP API Business Hub
* Adjust a prepared project using a configured destination calling REST services from ML foundation

