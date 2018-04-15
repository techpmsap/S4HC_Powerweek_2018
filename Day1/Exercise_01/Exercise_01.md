<table width=100% border=>
<tr><td colspan=2><h1>EXERCISE 01 - CREATE A CUSTOM BUSINESS OBJECT</h1></td></tr>
<tr><td><h3>SAP Partner Workshop</h3></td><td><h1><img src="images/clock.png"> &nbsp;15 min</h1></td></tr>
</table>


## Description
In this exercise, you’ll learn how 

* to create a custom business object that has a simple data structure and publish it
* to define the data structure and create the database persistence of a custom business object


For further reading on S/4HANA cloud in-app extension, click link below.
<https://jam4.sapjam.com/groups/m8lprEZwfU3zPoX0myj1Xu/overview_page/RfBJ6ix9q00bbSseaxm4zW>


## Target group

* Developers
* People interested in learning about S/4HANA Cloud extension and SDK  


## Goal

The goal of this exercise is to create a custom business object.


## Prerequisites
  
Below are the prerequisites for this exercise.

* Google Chrome: Please complete this exercise using the Google Chrome browser
* **Authorizations:** Your user needs a business role with business catalog **Extensibility** (ID: `SAP_CORE_BC_EXT`)


## Steps

1. [Starting Custom Business Objects application](#starting-custom-business-objects-application)
1. [Creating a new Custom Business Object](#creating-a-new-custom-business-object)
1. [Defining the data structure](#defining-the-data-structure)
1. [Adding standard data to the structure](#Adding-standard-data-to-the-structure)
1. [Creating the database persistence](#creating-the-database-persistence)



### <a name="starting-custom-business-objects-application"></a> Starting Custom Business Objects application

A several tutorials spanning example will show extensibility along custom Bonus Management applications.
As applications are based on business objects, it all starts with custom business object creation.

In the first parts a Manager wants to define business objects "Bonus Plan" for employees. A Bonus Plan is there to save employee specific rules for bonus entitlement.

**Start** with checking the prerequisite role.

1. Logon to the S/4HANA Cloud system.  The presenter will provide you the logon user and password.  The **XX** is the nuber that you have been assigned to use for the exercise. ![Maintain Business Users application tile](images/CBO_logon.png)
1. Click on the **Maintain Business Users** tile. 

	![Maintain Business Users application tile](images/tile_mbu.png)
1. Type in the User in the User Name Field and hit enter to search.  Your user will be displayed. Click on the error at the end of your user row to show the detail.  ![Maintain Business Users application tile](images/CBO_userrole1.png) 
1. On the "Assigned Business Roles" session.  Check if you have the Extensibility Business Role.  If you don't see the role, click on "Add" at the right hand side of the "Assigned Business Roles" to add the role.  ![Maintain Business Users application tile](images/CBO_userrole2.png)
1. Search for "Extensibility".  Click on the checkbox for Extensibility and click OK.  ![Maintain Business Users application tile](images/CBO_userrole3.png)
1. You will see the Extensibility business role added.  Click on "Save".  ![Maintain Business Users application tile](images/CBO_userrole4.png)
1. Go back to the Launchpad Home page by clicking on the Home icon.  ![Maintain Business Users application tile](images/FLP_Home.png)
1. Refresh the browser.  You will see more applications for the catalog of Extensibility.  ![Maintain Business Users application tile](images/CBO_extend1.png)

### <a name="creating-a-new-custom-business-object"></a> Creating a new Custom Business Object

1. **Create** the Custom Business Object's application by clicking its tile 

	![Custom Business Objects application tile](images/tile_CBO.png)
1. Press the **New** action to start creation of a Custom Business Object  ![Press New](images/CBO_pressNew.png)
1. In the opening Pop Up **fill** in the Name "Bonus PlanXX". The other editable fields will get proposals automatically but can be changed.  

	![Creation Pop Up](images/CBO_createNew.png) 
1. Execute the **Create** action.

### <a name="defining-the-data-structure"></a> Defining the data structure

1. In the following view for editing the custom business object **Go to Fields and Logic** of the root node "Bonus PlanXX".  ![Go to Fields and Logic](images/CBO_go2FieldsAndLogic_detail.png) 
1. Click on **New** to create new field for the object. ![Creation Pop Up](images/CBO_createNew1.png) 
1. Enter "ID" for the Naming. Choose "Numeric Identifier" for the Type. Keep 10 for the Length. Check the Key checkbox. ![Creation Pop Up](images/CBO_createNew2.png)
1. Repeat the above 2 steps to **create** following fields by clicking on **New** for each field.

	| Field Name     | Field Properties             | Tooltip     |
	| :------------- | :--------------------------- | :-----------|
	| ID             | Numeric Identifier of length 10, key field |             |   
	| Validity Start Date | Date    | |
	| Validity End Date | Date | |   
	| Target Amount | Amount with Currency | |   
	| Low Bonus Assignment Factor | Number of length 4, decimals 2 | Actual revenue must meet target more than that many times |
	| High Bonus Assignment Factor | Number of length 4, decimals 2 | Actual revenue must meet target more than that many times |
	| Low Bonus Percentage | Quantity with Unit | |   
	| High Bonus Percentage | Quantity with Unit  | |
	| Is Consistent | Checkbox, Read Only  | |
	| Employee ID | Text of length 12  | |
	| Employee Name | Text of length 40, Read Only   | |

1. The UI for maintaining fields looks as follows. ![Custom Business Object's Field List View](images/CBO_Fieldlist_partly.png)
1. Go back via the application's **Back** button. 

	![Fiori Application's Back Button](images/AppBackButton.png)


### <a name="Adding-standard-data-to-the-structure"></a> Adding standard data to the structure

1. Back in the business Object's definition overview, **check** the System Administrative Data box to add standardized fields for `Created On`, `Created By`, `Last Changed On` and `Last Changed By`.  ![Check System Administrative Data](images/CBO_checkSysAdminData.png)
	By checking this box the four fields also appear as uneditable in the field list.  These fields will be filled and updated automatically, so that you do not need to implement logic for this. Logic implementations for these fields even would be ignored.

### <a name="creating-the-database-persistence"></a> Creating the database persistence

1. **Publish** the Business Object `Bonus PlanXX`.  ![Press Publish](images/CBO_pressPublish.png)
	This creates the database persistence of the Business Object.
	
1. You will **Published** in green for this object when the publishing is completed. ![Press Publish](images/CBO_complePublish.png)


## Summary
This concludes the exercise. You should have learned how to create a custom business object that has a simple data structure and publish it. At the end there will exist a database table for the business object. Please proceed with exercise 01B.
