
# Step 1 - Create an Engine

Building an engine in Veritone begins with a few basic steps that define the general details about your technology and give scope to the services it will provide and the internal structures it will support. In this section, you&rsquo;ll learn how to create an engine in the Veritone Developer App &mdash; which serves as a container for your builds. Although an engine consists of some high-level details, it also includes important information about how your software works, including an Engine Category and Deployment Model. Once you&rsquo;ve finished creating your engine, we&rsquo;ll tour you through the different engine states to acquaint you with the workings of the engine lifecycle. Then we&rsquo;ll wrap things up by helping you find your Engine ID &mdash; a number that you&rsquo;ll want to have handy throughout the development process.

### Enter Basic Engine Details

When creating your engine, it's important to provide details that accurately and describe your engine. The information you enter is what users will see in the Veritone UI when they are selecting engines for processing.

| To create an Engine    |    |
| ---------------------- | -- |
| 1. Log into [Veritone Developer](https://developer.veritone.com). Click **Overview** in the upper left of the window and select **Engines** from the dropdown. The _Engines_ page opens. | <div style="width: 500px">![](VDA-Navigate-to-Engines.png)</div> |
| 2. Click **New Engine** in the upper right of the window. The new engine page opens to _Basic Engine Details_. | <div style="width: 500px">![](VDA-Create-Engine-1.png)</div>  |
| 3. Enter the following basic details to describe your engine: <br><ul><li>**Engine Name**: _(required)_ Enter the name of your engine as you would like it to appear to users.</li><li>**Engine Category**: _(required)_ Select the engine category from the drop-down that matches the type of service your engine will provide. (See [Engine Classes](engines/classes/) for more information.)</li><li>**Engine Description**: _(required)_ Describe what your engine does in a few sentences. This description displays to users in the engine selection table when hovering over your logo.</li><li>**Icon**: _(optional)_ Upload an icon for your engine from your local file system as a 128x128 png or jpg file. </li><li>**Logo**: _(required)_ Upload a logo image for your engine from your local file system as a 500x250 png or jpg file. The logo is used to identify your engine in the engine selection table of CMS. It's important to note that the logo is the only identifier users will see &mdash; your engine name will not display. To ensure your engine is easily identified, it's recommended to incorporate the engine name into your logo image.</li></ul> 4. Click **Next** to continue. The _Select your deployment model_ window opens. | <div style="width: 500px">![](VDA-Create-Engine-2.png)</div>     |

### Choose a Deployment Model

The deployment model indicates what type of network access your engine requires, after being installed by Veritone, which may affect whether your engine is eligible to run in private and secure servers. You must choose the deployment model that best represents your engine from the following four options:

* **Network Isolated**: The engine is fully isolated and runs solely within Veritone's infrastructure. It does not require network access.
* **External Access**: The engine performs processing within its container and does not send user data off the container. It requires internet access for tasks such as license checks and database updates.
* **External Processing**: The engine performs some or all of its processing outside of Veritone's infrastructure. User data is sent off the container to outside services for processing.
* **Human Review**: Some or all of the engine&rsquo;s processing is performed by humans outside of Veritone's infrastructure. (e.g., A human labeling service would fall into this category.)

Although the deployment model is set at the engine level, it&rsquo;s applied to a build at the time it&rsquo;s uploaded. For engines with multiple builds, the selected deployment model applies to each build and cannot be changed. If your engine can be deployed across multiple network access levels and you would like to assign it more than one deployment model, you'll want to create a separate engine container for each individual deployment model.

It&rsquo;s important to choose the deployment model best suited to the needs of your engine. When a build is uploaded, testing is performed to ensure that the build operates in accordance with the designated deployment model. If any discrepancies are detected, the build will not pass the testing. (e.g., A build with a network isolated deployment model that makes calls out to an external API will not pass.)

_Additional Notes About Deployment Models:_

* Engines that are exclusively public may have limited usage opportunities due to unsecured API.
* While many Veritone clients prefer our cloud-based software deployment, others require a network-isolated instance of the Veritone Platform due to regulation or security requirements.

| **To choose a deployment model** |     |
|--------------------------------- | --- |
| 1. Click a **deployment model option** to select it. The selected model&rsquo;s checkbox is enabled. </br> 2. Click **Submit** to save and create your engine. The new engine is created and displays under the _Engines List_ in the _Pending_ state. | <div style="width: 500px">![](VDA-Create-Engine-3.png)</div> |

### Engine States

The engine state allows you easily identify and track an engine&rsquo;s progression and regression through the workflow cycle. Veritone uses four different engine states to capture the most relevant aspects of an engine&rsquo;s lifecycle and operation.

Three engine states apply to workflow stages. They&rsquo;re automatically set by the system and transition from one to the next when certain functions are carried out. When an engine is newly created, it automatically enters the Pending state. From there, it progresses to Ready when a build is approved, and then Active when the engine is live in the Veritone Platform. The fourth state allows you to manually Disable an engine and stop it from processing new tasks. For added flexibility, each engine state offers optional actions that help you manage the engine&rsquo;s settings and operations.

The table below specifies the valid states, transitions, reasons for the transitions, and optional actions that can be performed for each.

|**Engine State**|**Description**|**Available Actions**|
|----------------|---------------|---------------------|
|**Pending**|The _Pending_ state is system-triggered and takes effect when the engine has been created but it does not have any _Approved_ builds.|Edit, Disable, Delete|
|**Ready**|The _Ready_ state is system-triggered and takes effect when an engine has at least one Approved build, but no builds that are deployed. |Edit, Disable, Delete|
|**Active**|The _Active_ state is system-triggered and takes effect when a build is deployed.|Edit, Disable, Delete|
|**Disabled**|The _Disabled_ state is user-enabled. Disabling an engine prevents it from running and processing new jobs. Any jobs that are in progress when the engine is disabled will finish processing. In addition, the _Deploy_ option will be removed _Approved_ builds . An engine can only be set to _Disable_ from the _Ready_ or _Active_ states.|Enable|

### Find Your Engine ID

When an engine is created, it&rsquo;s assigned a unique ID number. This ID will be used to identify your engine in various places throughout the development process, including uploading your build(s).

|**To locate an Engine ID**|   |
|--------------------------|---|
|Navigate to the _Engines_ page in Veritone Developer and click the desired **engine** in the list. The _Engine Details_ page opens to the _Builds_ tab.The _Engine ID_ is located under the engine name near the top of the window.|<div style="width: 500px">![](VDA-Find-Engine-ID.png)</div>|
