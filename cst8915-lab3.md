
1. Recording lab3 Youtube link: https://youtu.be/Kno1w70DvMw


2. Reflection Questions:

1. What challenges did you encounter when configuring environment variables in the GitHub Actions workflow?
I encountered a region restriction error (RequestDisallowedByAzure) that blocked deployment, so I had to run my storefront app in a VM instead of a static web app. Another issue was switching from HTTP (local) to HTTPS (Azure domain), which caused some delays.

2. How does deploying microservices on Azure Web App Service differ from running them locally?
Running locally required more manual setup (VM configuration, networking), while Azure Web App Service automated most steps. By setting environment variables and pushing code to GitHub, deployment became faster and easier.

3. Why is it important to use environment variables for configurations in a cloud environment?
Environment variables separate configuration from code, making apps more portable and secure. This allows quick changes (e.g., database strings or ports) without modifying or redeploying the application itself.

Full error code:[{ "code": "InvalidTemplateDeployment", "message": "The template deployment failed because of policy violation. Please see details for more information.", "details": [ { "code": "RequestDisallowedByAzure", "target": "Store-Front-app", "message": "Resource 'Store-Front-app' was disallowed by Azure: This policy maintains a set of best available regions where your subscription can deploy resources. The objective of this policy is to ensure that your subscription has full access to Azure services with optimal performance. Should you need additional or different regions, contact support.." } ] }].