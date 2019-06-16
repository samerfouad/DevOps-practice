# Create your own custom DevOps toolchain to go from your source code to a running application in a minutes.

Practive DevOps using **IBM Cloud Continous Delivery Service**, In this tutorial we will **Build** and **Deploy** cloud foundry applications to IBM Cloud using its DevOps service.



**Steps**

1. **Fork/Clone** this github repo by using the following command: `git clone https://github.com/samerfouad/DevOps-practice.git`

2. **Login** to IBM Cloud using the following link: `https://cloud.ibm.com/login`

- From the left side menu scroll down to the **DevOps section**.

![DevOps Button](https://user-images.githubusercontent.com/18283745/59562339-ad7aa400-902b-11e9-845f-eaef328df35e.png)

- Click on the blue button - **Create a Toolchain Button**.

![Create a Toolchain Button](https://user-images.githubusercontent.com/18283745/59562340-afdcfe00-902b-11e9-8062-ec5a43c216fe.png)

- Click on the blue button - **Add a Tool**.

![Add a Tool Button](https://user-images.githubusercontent.com/18283745/59562510-e9af0400-902d-11e9-8a6f-11fc266c3b96.png)

- Search and Locate Github from the Tools Menu - **locate Github**.

![Github](https://user-images.githubusercontent.com/18283745/59562561-604c0180-902e-11e9-8f0e-b9a143234196.png)

Note: If this is the first time using this tool, you will need to authorize IBM Cloud to use your GitHub credentials. Click on Authorize and log into Github.

For the **GitHub server option**, leave the default GitHub (https://github.com/) value.
For the Repository type option, choose **Existing**.
For the Repository URL option, type in the **forked GitHub repo** value, for example: https://github.com/samerfouad/DevOps-practice.
Ensure both the **Enable GitHub Issues and Track deployement of code changes options are selected**.
Click the **Create Integration** button.

![Adding Github](https://user-images.githubusercontent.com/18283745/59562610-e8320b80-902e-11e9-9100-7b54e6fce159.png)

Now, You should see this screen after clicking **create**.


![Delivery Pipeline](https://user-images.githubusercontent.com/18283745/59562632-42cb6780-902f-11e9-858d-7fbd7903cc55.png)

Add a **Build stage**.

Click the **Add Stage button**.

Name it **Build**.

The options for the INPUT tab should be correct by default, but we’ll list them here for completeness:


- Click the **Add a Tool** button on top right corner.

- Search for “**Delivery Pipeline**”.

- Click the **Delivery Pipeline option**.

- Name the pipeline and click **Create**.

- Your toolchain page now should look like this.

- We’ll be adding **two stages**: a “**Build**” stage and a “**Deploy**” stage.
- It is while configuring these stages that we’ll be referencing the application code, the repository we forked earlier, to **build** and **deploy**.

![Delivery Pipeline stages](https://user-images.githubusercontent.com/18283745/59562699-23810a00-9030-11e9-848f-679b79f3fc03.png
)

**Add a Build stage**

Click the **Add Stage** button.

Name it **Build**.

The options for the **INPUT tab** should be correct by default, but we’ll list them here for completeness:

```javascript
"Input type": "Git repostory"
"Git repository": "DevOps-practice"
"Branch": "master"
```
- Ensure **the Run jobs whenever a change is pushed** to Git radio button is selected.

- Select the **JOBS** tab.

- Click **Add Job** and select **Build** as the job type.

- Select **Simple** as the **Builder type**.

- Ensure the **Stop running this stage** if this job fails is **selected** as well.

- Click **Save**.

**Add a Deploy stage**

Click the **Add Stage** button.

Name it **Deploy**.

The options for the INPUT tab should be correct by default, but we’ll list them here for completeness:

```javascript
"Input type": "Build artifacts"
"Stage": "Build"
"Job": Build"
```

Ensure the **Run jobs when previous stage is complete** radio button is selected.


- Select the **JOBS** tab.

- Click **Add Job** and select **Deploy** as the job type.

- Select **Cloud Foundry** as the **Deployer type**.

- Select the **appropriate IBM Cloud region**, **organization**, and **space** where application will be **deployed**.

- Ensure the **Stop running this stage** if this job **fails** is selected also.

```javascript
"Deployer type" : "Cloud Foundry"
"Application name": "DevOps-practice"
```

Select the **ENVIRONMENT PROPERTIES** tab.

Add a **new property** with type **text property**. Configure it with the following key-value pair:

```javascript
"CF_APP": "DevOps-practice"
```

Click **Save**.

The delivery pipeline should now look like this:

![Delivery Pipeline stages](https://user-images.githubusercontent.com/18283745/59563052-1f0b2000-9035-11e9-9a7c-ae2e1bbdb95a.png)

Click the **Play button** on the **Build** stage to **manually trigger a build** and **watch pipeline automatically** start the **Deploy** stage. After the **Deploy** stage is completed successfully, you can return to your dashboard and see your application under **The Cloud Foundry apps heading**.

