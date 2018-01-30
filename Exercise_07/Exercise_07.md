<table width=100% border=>
<tr><td colspan=2><h1>EXERCISE 07 - RETRIEVING DATA FROM S/4HANA SYSTEM AND SETTING INTEGRATION TESTS</h1></td></tr>
<tr><td><h3>SAP Partner Workshop</h3></td><td><h1><img src="images/clock.png"> &nbsp;30 min</h1></td></tr>
</table>


## Description
In this exercise, you’ll learn how 

* to retrieve the list of Business Partners from a S/4HANA backend by adding a couple of new Java classes to the application which will be consuming the S/4HANA Cloud SDK framework 
* to set a new Java class in the integration test module to check that the response received from server when calling the new servlet, is a correct JSON output

For further reading on S/4HANA Cloud SDK, click link below.
<https://www.sap.com/germany/developer/topics/s4hana-cloud-sdk.html>


## Target group

* Developers
* People interested in learning about S/4HANA extension and SDK  


## Goal

The goal of this exercise is to retrieve some business partners data from the S/4HANA back-end using the S/4HANA Cloud SDK and check that the response is a valid JSON output.


## Prerequisites
  
Here below are prerequisites for this exercise.

* A trial account on the SAP Cloud Platform. You can get one by registering here <https://account.hanatrial.ondemand.com>
* Apache Maven
* Java JDK 8
* The source code created in the previous exercise
* A S/4HANA system with a working communication arrangment for the Business Partners collection


## Steps

1. [Retrieve Business Partner data from S/4HANA](#retrieve-bp-data)
1. [Setting an integration test for the Business Partners API](#integration-test)




### <a name="retrieve-bp-data"></a> Retrieve Business Partner data from S/4HANA
In this chapter you are going to see how to implement a couple of new JAVA classes to retrieve Business Partners data from a S/4HANA system.

1. Open Eclipse IDE and load the project created in the previous exercise  
	![](images/01.png)
1. Double click the *pom.xml* file in the **application** module to open it  
	![](images/02.png)
1. Select the pom.xml tab and paste the following dependency into this file among the other dependencies

	```xml
	<dependency>
		<groupId>org.projectlombok</groupId>
	   <artifactId>lombok</artifactId>
	</dependency>
	```

	![](images/03.png)
1. Save the file.
1. Right click on the application module and select **New -> Class** to create a new Java class  
	![](images/04.png)
1. Check that the Package name is still *com.sap.sample.bprcf\_dev\_xx* (**xx** must be replaced with your workstation id) and enter the name **BPDetails** for this new class. Click **Finish**  
	![](images/05.png)
1. A new empty Java class is created  
	![](images/06.png)
1. Replace the entire current content with the following (remember that **xx** must be replaced with your workstation ID)

	```java
	package com.sap.sample.bprcf_dev_xx;
	
	import lombok.Data;
	import com.sap.cloud.sdk.result.ElementName;
	
	@Data
	public class BPDetails
	{
	    @ElementName( "BusinessPartner" )
	    private String bpId;
	
	    @ElementName( "BusinessPartnerName" )
	    private String bpName;
	
	    @ElementName( "BusinessPartnerCategory" )
	    private String bpCategory;
	
	    @ElementName( "BusinessPartnerGrouping" )
	    private String bpGrouping;
	
	    @ElementName( "LastName" )
	    private String bpLastName;
	
	    @ElementName( "FirstName" )
	    private String bpFirstName;
	}
	```

	![](images/07.png)

1. Save the file
1. At the same way, create a new Java Class named **BPServlet** and click **Finish**  
	![](images/08.png)
1. Replace the entire current content with the following (remember that **xx** must be replaced with your workstation ID)

	```java
	package com.sap.sample.bprcf_dev_xx;
	
	import com.google.gson.Gson;
	import org.slf4j.Logger;
	import javax.servlet.ServletException;
	import javax.servlet.annotation.WebServlet;
	import javax.servlet.http.HttpServlet;
	import javax.servlet.http.HttpServletRequest;
	import javax.servlet.http.HttpServletResponse;
	import java.io.IOException;
	import java.util.List;
	import com.sap.cloud.sdk.odatav2.connectivity.ODataException;
	import com.sap.cloud.sdk.odatav2.connectivity.ODataQueryBuilder;
	import com.sap.cloud.sdk.s4hana.connectivity.ErpConfigContext;
	import com.sap.cloud.sdk.s4hana.connectivity.ErpDestination;
	import com.sap.cloud.sdk.s4hana.connectivity.ErpEndpoint;
	import com.sap.cloud.sdk.s4hana.serialization.SapClient;
	import com.sap.cloud.sdk.cloudplatform.logging.CloudLoggerFactory;
	
	@WebServlet("/businesspartners")
	public class BPServlet extends HttpServlet {
	
	    private static final long serialVersionUID = 1L;
	    private static final Logger logger = CloudLoggerFactory.getLogger(BPServlet.class);
	
	    @Override
	    protected void doGet(final HttpServletRequest request, final HttpServletResponse response)
	            throws ServletException, IOException
	    {
	        final SapClient sapClient = new SapClient("100"); // adjust SAP client to your respective S/4HANA system
	        try {
	            final ErpEndpoint endpoint = new ErpEndpoint(new ErpConfigContext(ErpDestination.getDefaultName(), sapClient));
	            final List<BPDetails> businessPartners = ODataQueryBuilder
	                    .withEntity("/sap/opu/odata/sap/API_BUSINESS_PARTNER", "A_BusinessPartner")
	                    .select("BusinessPartner", "BusinessPartnerName", "BusinessPartnerCategory", "BusinessPartnerGrouping", "LastName","FirstName")
	                    .top(100)
	                    .build()
	                    .execute(endpoint)
	                    .asList(BPDetails.class);
	            response.setContentType("application/json");
	            response.getWriter().write(new Gson().toJson(businessPartners));
	        } catch(final ODataException e) {
	            logger.error(e.getMessage(), e);
	            response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR);
	            response.getWriter().write(e.getMessage());
	        }
	    }
	}
	```
	
	![](images/09.png)

1. Save the file
1. Expand the **root** module of your project and select the *pom.xml* file. Then click on the small play button on the toolbar. Select the **Maven build** goal and click **OK**  
	![](images/10.png)
1. Specify the **clean install** goals if required and click **Run**  
	![](images/10_2.png)
1. Building should end with a BUILD SUCCESS message  
	![](images/11.png)
1. Open a terminal window and go to the project folder folder. Type in the `cf push` command to deploy the application to Cloud Foundry  
	![](images/12.png)
1. The push operation should finish successfully
	![](images/13.png)
1. Before we can execute our Cloud Foundry application you need to setup the destination which points to our back-end system. The destination you are creating is named **ErpQueryEndpoint**: this is the default name the ODataQueryBuilder searches for in order to get a connection with backend. It can be changed, but let's keep the default one here. Remaining in the Terminal pane, run the command

	```sh
	cf set-env bprcf_dev_xx destinations "[{name: 'ErpQueryEndpoint', url: 'https://my300098-api.s4hana.ondemand.com', username: 'SIMMACO_CU_LM', password: 'Admin123!'}]"
	```
this will configure the destination with the endpoint and credentials we have prepared for this workshop
	![](images/14.png) 
1. In order to let the application taking into account the new changes, we need to restage the app with the command 

	```
	cf restage bprcf_dev_xx
	``` 

	where **xx** must be replaced with your workstation ID
	![](images/15.png)
1. Open the browser and type in the URL <https://bprcf_dev_xx.cfapps.eu10.hana.ondemand.com/businesspartners> (replace **xx** with your workstation ID). You should be able to see the Business Partners list
	![](images/16.png)
1. Congratulation! You have successfully retrieved Business Partners data from the S/4HANA back-end using the S/4HANA Cloud SDK.


### <a name="integration-test"></a> Setting an integration test for the Business Partners API
In this chapter you are going to implement a new Java class to test if the response coming from the backend system is a valid JSON output and if the response contains the mandatory fields **bpId** and **bpName**.

1. Open Eclipse IDE, expand the **integration-tests** module and double click on the *pom.xml* file you can find under this branch. When a new tab opens, click on the **pom.xml** tab
	![](images/17.png)
1. Add a new dependency to this module for the **Json Schema Validator**. Copy this code and paste it among all the other dependencies. Then **save** the file

	```xml
	<dependency>
	    <groupId>io.rest-assured</groupId>
	    <artifactId>json-schema-validator</artifactId>
	    <version>3.0.3</version>
	    <scope>test</scope>
	</dependency>
	``` 
    
	![](images/18.png)
1. Right click on the **integration-tests** and choose **New --> Class**  
	![](images/19.png)
1. Create a new Java Class named **BPServiceTest** and click **Finish**  
	![](images/20.png)
1. Paste in the following content and **save** the file (remember that **xx** must be replaced with your workstation ID)

	```java
	package com.sap.sample.bprcf_dev_xx;
	
	import com.jayway.restassured.RestAssured;
	import com.jayway.restassured.http.ContentType;
	import io.restassured.module.jsv.JsonSchemaValidator;
	import org.jboss.arquillian.container.test.api.Deployment;
	import org.jboss.arquillian.junit.Arquillian;
	import org.jboss.arquillian.test.api.ArquillianResource;
	import org.jboss.shrinkwrap.api.spec.WebArchive;
	import org.junit.Before;
	import org.junit.BeforeClass;
	import org.junit.Test;
	import org.junit.runner.RunWith;
	import org.slf4j.Logger;
	
	import java.net.URL;
	import java.net.URISyntaxException;
	
	import com.sap.cloud.sdk.cloudplatform.logging.CloudLoggerFactory;
	import com.sap.cloud.sdk.testutil.MockUtil;
	
	import static com.jayway.restassured.RestAssured.given;
	
	@RunWith( Arquillian.class )
	public class BPServiceTest
	{
	    private static final MockUtil mockUtil = new MockUtil();
	    private static final Logger logger = CloudLoggerFactory.getLogger(BPServiceTest.class);
	
	    @ArquillianResource
	    private URL baseUrl;
	
	    @Deployment
	    public static WebArchive createDeployment()
	    {
	        return TestUtil.createDeployment(BPServlet.class);
	    }
	
	    @BeforeClass
	    public static void beforeClass() throws URISyntaxException
	    {
	        mockUtil.mockDefaults();
	        mockUtil.mockErpDestination();
	    }
	
	    @Before
	    public void before()
	    {
	        RestAssured.baseURI = baseUrl.toExternalForm();
	    }
	
	    @Test
	    public void testService()
	    {
	        // JSON schema validation from resource definition
	        final JsonSchemaValidator jsonValidator = JsonSchemaValidator.matchesJsonSchemaInClasspath("businesspartners-schema.json");
	
	        // HTTP GET response OK, JSON header and valid schema
	        given().
	                get("/businesspartners").
	                then().
	                assertThat().
	                statusCode(200).
	                contentType(ContentType.JSON).
	                body(jsonValidator);
	    }
	}
	```

1. Right click on the **integration-tests** module and choose **New --> File**  

<<Note: this should be under resources folder >>
	![](images/21.png)
1. Select **General -> File** and click **Next**    
	![](images/22.png)
1. Create a new JSON file named *businesspartners-schema.json* and click **Finish**
	![](images/23.png)
1. Paste in this JSON fragment and **save** the file  

	```json
	{
	  "$schema": "http://json-schema.org/draft-04/schema#",
	  "title": "Business Partners List",
	  "type": "array",
	  "items": {
	    "title": "Business Partner Item",
	    "type": "object",
	    "javaType": "com.sap.sample.BPDetails",
	    "required": ["bpId", "bpName"]
	  }
	}
	```
	
	![](images/24.png)
1. Staying in the same path, create a new JSON file named *systems.json* as you have done in the previous step  
1. Paste in the following content and save the file. As URI string we are using the API Endpoint of the S/4HANA backend system   

	```json
	{
	  "erp": {
	    "default": "ERP",
	    "systems": [
	      {
	        "alias": "ERP",
	        "uri": "https://my300098-api.s4hana.ondemand.com"
	      }
	    ]
	  }
	}
	```

	![](images/25.png)
1. Remaining in the same path, create again a new JSON file named *credentials.json*  
1. Paste in the following content and save the file: the credentials used here are the ones for the URI specified in the previous step   

	```json
	{
	  "credentials": [
	    {
	      "alias": "ERP",
	      "username": "SIMMACO_CU_LM",
	      "password": "Admin123!"
	    }
	  ]
	}
	```

	![](images/26.png)

1. Remember to save all the files you have created so far
1. Now, in order to run just the Maven **test** goal, expand the **root** module, right click on the *pom.xml* file and select the **Run As -> Maven test** goal  
	![](images/27.png)
1. At the end of the execution, you should receive a BUILD SUCCESS message. This means that your data source output has been verified against the conditions we have set  
	![](images/28.png)
1. For example, if you want to verify that the integration test is working, try by replacing in the *businesspartners-schema.json* file, the string **bpName** with **bpNickName**. In this way we are telling to the integration-test phase that we are expecting as mandatory fields **bpId** and **bpNickName**. Since this last field doesn't exist, the integration test should fail  
	![](images/29.png)
1. Save the file and execute the Maven **test** goal again 
	![](images/30.png)
1. The test, as expected, fails and if you scroll up the Terminal pane, you see the message informing you that an object is missing required properties  
	![](images/31.png)
1. Restore the original **bpName** value and save the file  
	![](images/32.png)
1. Expand the **root** module of your project and select the *pom.xml* file. Then click on the small play button on the toolbar. Select the **Maven build** goal and click **OK**  
	![](images/10.png)
1. Specify the **clean install** goals if required and click **Run**  
	![](images/10_2.png)
1. Build should succeed  
	![](images/34.png)
1. In the Terminal pane, run again a `cf push` command to Cloud Foundry  
	![](images/35.png)
1. Check that the application is still providing the expected results    
	![](images/36.png)
1. Congratulation! You have successfully implemented integration tests into your application using the S/4HANA Cloud SDK.


## Summary
This concludes the exercise. You should have learned how to retrieve data from a S/4HANA back-end system and how to implement integration testing using the S/4HANA Cloud SDK. Please proceed with exercise 08.
