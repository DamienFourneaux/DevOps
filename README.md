# DevOps
Repository for the  DevOps project

Question 3.3 : Is it really safe to deploy automatically every new image on the hub ? explain. What can I do to make it more secure?

Automatically deploying every new image pushed to Docker Hub can be risky, as one might download and run untested or malicious code. Images could contain vulnerabilities or backdoors that are immediately promoted to production. To secure this process, it would be better to use a trusted or private registry (or require image signing and verification), enable automated vulnerability scanning on each image before deployment, and add a manual approval or testing stage in the CI/CD pipeline so that only vetted tags (for example, after passing security checks and integration tests) are actually deployed to production.