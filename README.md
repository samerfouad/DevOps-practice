# Sample Express DevOps App

Practive DevOps using IBM Cloud continous delivery service, Build and Deploy cloud foundry applications with DevOps service.

Create your own custom DevOps toolchain to go from your source code to a running application in a minutes.

**Steps**

1. Fork/Clone this github repo by using the following command: `git clone https://github.com/samerfouad/sample-express-app.git`

2. Login to IBM Cloud using the following link: `https://cloud.ibm.com/login`

- From the left side menu scroll down to the DevOps section.

![DevOps Button](https://user-images.githubusercontent.com/18283745/59562339-ad7aa400-902b-11e9-845f-eaef328df35e.png)

- Click on the blue button - **Create a Toolchain Button**

![Create a Toolchain Button](https://user-images.githubusercontent.com/18283745/59562340-afdcfe00-902b-11e9-8062-ec5a43c216fe.png)

- Click on the blue button - **Add a Tool**

![Add a Tool Button](https://user-images.githubusercontent.com/18283745/59562510-e9af0400-902d-11e9-8a6f-11fc266c3b96.png)

- Search and Locate Github from the Tools Menu - **locate Github**

![Github](https://user-images.githubusercontent.com/18283745/59562561-604c0180-902e-11e9-8f0e-b9a143234196.png)

Note: If this is the first time using this tool, you will need to authorize IBM Cloud to use your GitHub credentials. Click on Authorize and log into Github.

For the GitHub server option, leave the default GitHub (https://github.com/) value.
For the Repository type option, choose Existing.
For the Repository URL option, type in the forked GitHub repo value, for example: https://github.com/samerfouad/DevOps-practice.
Ensure both the Enable GitHub Issues and Track deployement of code changes options are selected.
Click the Create Integration button.

![Adding Github](https://user-images.githubusercontent.com/18283745/59562610-e8320b80-902e-11e9-9100-7b54e6fce159.png)

Now, You should see this screen after clicking create


![Delivery Pipeline](https://user-images.githubusercontent.com/18283745/59562632-42cb6780-902f-11e9-858d-7fbd7903cc55.png)

Add a Build stage.

Click the Add Stage button.

Name it Build.

The options for the INPUT tab should be correct by default, but we’ll list them here for completeness:

![Delivery Pipeline stages](https://user-images.githubusercontent.com/18283745/59562699-23810a00-9030-11e9-848f-679b79f3fc03.png
)


- Click the Add a Tool button on top right corner.

- Search for “Delivery Pipeline”.

- Click the Delivery Pipeline option.

- Name the pipeline and click Create.

- Your toolchain page now should look like this.

We’ll be adding two stages: a “Build” stage and a “Deploy” stage. It is while configuring these stages that we’ll be referencing the application code, the repository we forked earlier, to build and deploy.



1. `git clone YOUR_REPO_URL`

```javascript
var express = require('express');
var bodyParser = require('body-parser');
var port = process.env.PORT || 3000;
var app = express();
app.use(bodyParser.text());
function convertToCaps(str) {
    return str.toUpperCase();
}
app.get('/', function(req,res) {
    res.end('Hello Cloud Native Developers');
});
app.post('/api/capitalise', function(req, res) {
    res.send(convertToCaps(req.body));
})
if (require.main === module) {
    app.listen(port, function() {
        console.log('Server listening on port: ' + port);
    });
}
```


