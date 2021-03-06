# ucvelocity-POT-France

* [Creating an Azure and UrbanCode Deploy (UCD) Value Stream](https://urbancode.github.io/velocity-info/workbooks/azureUcdValueStreams.html#11-create-workbook-project)
* [Steps to create a simple Azure DevOps pipeline](#steps-to-create-a-simple-azure-devOps-pipeline)
* [Steps to create an Azure access token](#steps-to-create-an-azure-access-token)
* [Steps to configure resources in UrbanCode deploy](#steps-to-configure-resources-in-urbancode-deploy)
* [Steps to create the VSM Json file on the VM](#steps-to-create-the-vsm-json-file-on-the-vm)
* [Basic Velocity administration](#basic-Velocity-administration)
* [IBM Rational Azure DevOps Extension](#IBM-Rational-Azure-DevOps)

## Steps to create a simple Azure DevOps pipeline

![create azure devops pipeline](./images/createPipeline.jpg)

![create azure devops pipeline](./images/connectRepo.jpg)

![create azure devops pipeline](./images/SelectRepo.jpg)

![create azure devops pipeline](./images/configurePipeline.jpg)

![create azure devops pipeline](./images/ReviewPipeline.jpg)

## Steps to create an Azure access token
In the User Settings, there is a Personal Access Tokens option:
![create azure access token](./images/azureUserSettings.jpg)

![create azure access token](./images/PersonalAccessToken.jpg)

## Steps to configure resources in UrbanCode deploy

In UCD, navigate to home -> Ressources.
Click on **create Top-Level Group** and call it **urbancode.com**

![configure UCD](./images/configureUCD-1.jpg)

Define a common deployment target for all environments:
*	Click the Actions drop-down menu to the right of **UrbanCode.com**. Click Add Agent then choose **datacenter** (our local agent).
* Click the Actions drop-down menu to the right of **datacenter**. Click Add component and choose the component **WorkBookComp**.

Assign that resource to each environment of the application.
* In UCD, navigate to the environment of the WorkBook application: **Home > Applications > WorkBook > Environments > DEV**.
* From the Resources tab, click the Add Base Resources button. Select the **WorkBookComp** resource and click OK

![configure UCD](./images/configureUCD-2.jpg)

Repeat that last step for all the other environments.

## Steps to create the VSM Json file on the VM

You can either create the VSM Json file on the VM using gedit, or download the json file stored in github using a browser running on the VM.

The json file can be found here : [AzureWorkbook.json](https://github.com/VialeMuriel/ucvelocity-demo-france/blob/master/materials/AzureWorkbook.json "UCVelocity Demo France")

To create the Json file on the VM, open gedit editor in Applications -> Accessories -> gedit

![create JSON](./images/createJson-1.jpg)

Go back to the azure Workbook web page, and select the content of the json file.

![create JSON](./images/createJson-2.jpg)

Go back to the VM and paste the content into the clipboard of the emulator:

![create JSON](./images/createJson-3.jpg)

![create JSON](./images/createJson-4.jpg)

The text can now be pasted into the editor. It is just an other Ctrl+v, but in the editor window this time.

![create JSON](./images/createJson-5.jpg)

Save the document as AzureWorkbook.json, in the sysadmin Documents folder :

![create JSON](./images/createJson-6.jpg)

The Json file can now be uploaded in the Velocity VSM, using the upload button.

## Basic Velocity administration
Stop Velocity:
```
$ cd /opt/velocity/<version>"
$ sudo docker-compose stop
```
Start Velocity:
```
$ cd /opt/velocity/<version>
$ sudo docker-compose up -d
```

List container process:
```
$ docker ps
```
Get the log of a specifi container:
```
$ docker logs <container> > output.log
```
Containers:
- velocity_continuous-release-ui
- velocity_reporting-consumer
- velocity_release-events-ui
- release-events-api

## IBM Rational Azure DevOps Extension

We can integrate IBM Rational Test Automation Server with Azure DevOps so that we can run tests in Azure DevOps pipelines. The entire procedure is documented [here](https://help.blueproddoc.com/rationaltest/rationaltestautomationserver/10.1/com.hcl.test.server.tester.doc/topics/t_run_tests_azurdvops_pipeline.html)

The IBM RTAS Server for the demo : [IBM RTAS server](https://rtas.apps.myrtascluster-e638aca3e25c28b781014ca81b1b35b2-0000.eu-de.containers.appdomain.cloud/#/project/1100/execute/execution)
![visualstudio](./images/visualstudio-2.jpg)

First we need to install the IBM Rational Test Workbench extension in Azure DevOps from the [Visual Studio Market Place](https://marketplace.visualstudio.com/items?itemName=IBMDevOps.build-release-task-IBM)
![visualstudio](./images/visualstudio-1.jpg)

Then we need to create an azure pipeline and include a task to run a test in our Azure DevOps pipeline. ![visualstudio](./images/visualstudio-3.jpg)

At the first time, we need to create a new server connection and provide the following details to add an IBM Rational Test Automation Server service connection, and then save the connection details:
![visualstudio](./images/visualstudio-4.jpg)
