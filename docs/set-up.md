# Setting up Summit Events app in salesforce

## Create a site subdomain

If your org does not already have a site to display public visual force pages you will need to set one up. You may use an existing site if one has been set up previously.

1. In Setup go to User Interface -> Sites and Domains -> Sites
2. Select a subdomain that is available.
3. Click "Register My Salesforce Site Domain"

Once your domain has been registered continue:

1. Click the "New" button next to the site header
2. Select "Guest" as the "Type of New Site"
3. Enter the following data in the form (label, name, and homepage can be adjust to what makes sense for your site)
    * Site Label: Summit Events 
    * Site Name: Summit_Events
    * Active Site Home Page:
        * Select the magnifying glass look-up icon and in the dialog select SummitEvents
    * Leave all other settings at their defaults
5. Click "Save"
6. Click the "Active" link under Action next to the site you just created
7. Right click on the site URL and copy the URL to your clipboard. You will need it in the next stage of installation.

## Set Custom Settings

Since each installation can have a different site URL we need to define that URL for the event application to use as it's root web presence. This is used for feed URLs for external sites to access and a host of other things.

1. In Setup go to User Custom Code -> Custom Settings

2. Click on the "Manage" link for the custom setting "Summit Events Settings"

3. Click "New" button just before the "Default Organization Level Value." There are two "New" buttons on the page. You will know you are on the wrong one if you are asked to assign a user or a profile. You should only need to enter the URL in the follow step.

4. From step 7 in the "Create a site record" use the URL you copied there and enter it into the Community Based URL field.

5. Click "Save"

6. Once you hit "Save" the "New" button will be replaced with "Edit." This is what you will need to hit to make future adjustments to this setting.

## Set Sharing Rules

Salesforce winter '20 and Spring '20 releases will begin to severely limit Guest User access to objects.
Sharing rules will limit the Guest User to insert access only by default. The Summit Events application requires
that the Guest user be able to read, and upsert to it's custom objects. In order to align this application with 
the new security rules we need to set a sharing rule to allow the application to read it's objects. Code has also
been adjust to allow for the required upserts. The following instructions will help you set up the required sharing rules.
Unfortunately, we are not able to automate these steps yet due to limitations in SFDX.

### Set Sharing Object Access

1. Type "Sharing" in the quick-find box in Setup and click on "Sharing Settings".

2. Click "Edit" to expose sharing option settings for editing

3. In the "Manage sharing settings for:" picklist choose "Summit Events"

5. Make sure the Summit Events object is "Public Read/Write" in the "Organization-Wide Defaults". Edit if needed.

2. Under the "Sharing Rules" header click the "New" button in the "Summit Events Sharing Rules" section.

4. Label your rule "Guest User Read Access" with rule name "Guest_User_Read_Access"

5. Set the radio button for "Rule Type" to "Guest user access, based on criteria"

6. Set "Criteria" to Field => Event Name, Operator => "not equal to", Value => null  (type the world null for the value)

7. Share with can only be set to "Summit Events Site Guest User"

8. Set Access Level to "Read Only"

9. Click "Save"

## Apply Permission Sets

There are two permission sets tracked in this application. These permission sets can be applied 

**Summit Events Admin**: 
Apply to admin users that need to create and maintain events.

**Summit Events Registrant**: Needs to be applied to the Guest User of your site for public access to registration forms.


#### Apply Summit Events Registrant premission set to the Guest User of your site

1. Go to Sites in Setup

2. Click on the name of the site that you Summit Events to be active in.

3. Click on the "Public Access Settings" button at the top of the site definition page.

4. On the site details page click on the "View Users" button.

5. On the user list find your guest user and click on the name of that user.

6. Go to Permission Set Assignment and assign "Summit Events Registrant" permission set.

At this point you should have a functioning Summit Events Package. You only need to set up some events and instances (see other Wiki pages).
