# Chef Pipelines

### Description
All pipelines are written in `groovy` and stored in a `Jenkinsfile` which can be displayed in Jenkins with the Blue Ocean plugin.

---
## InSpec Pipeline
InSpec is a framework for testing and auditing your applications and infrastructure. InSpec works by comparing the actual state of your system with the desired state that you express in easy-to-read and easy-to-write InSpec code. InSpec detects violations and displays findings in the form of a report, but puts you in control of remediation.

### Description
This pipeline takes an InSpec profile and performs syntax and lint checking to produce an archive that can be used by an Audit Cookbook to validate images, OS's and Middleware.  It produces a signed artifact that is consumed by the Policyfile pipeline.

### Depends On (Up stream)
- Other InSpec Pipelines (Optional)

### Depends On It (Down stream)
- Policyfile Pipeline (Mandatory)

![InSpec Pipeline](/images/inspec_pipeline.png)

### Code
https://github.com/anthonygrees/inspec_pipeline

---
## Cookbook Pipeline
A cookbook is the fundamental unit of configuration and policy distribution. A cookbook defines a scenario and contains everything that is required to support that scenario:
- Recipes that specify the resources to use and the order in which they are to be applied
- Attribute values
- File distributions
- Templates
- Extensions to Chef, such as custom resources and libraries

### Description
The cookbook pipeline takes the cookbook and it's recipies, tests them using kitchen, performs lint and syntax checks and then publishes it for the policyfile pipeline to consume.

### Depends On (Up stream)
- Other Cookbook Pipelines (Optional)

### Depends On It (Down stream)
- Policyfile Pipeline (Mandatory)

![Cookbook Pipeline](/images/cookbook_pipeline.png)

### Code
https://github.com/anthonygrees/cookbook_pipeline

---
## Policyfile Pipeline
A Policyfile is an optional way to manage role, environment, and community cookbook data with a single document that is uploaded to the Chef server. The file is associated with a group of nodes, cookbooks, and settings. When these nodes perform a Chef client run, they utilize recipes specified in the Policyfile run-list.

### Description
The policyfile pipeline takes input from both `cookbooks` and `inspec` and then resolves dependencies.  The versions, attributes and runlist are all handeled by the policyfile.

### Depends On (Up stream)
- InSpec Pipeline (Mandatory)
- Cookbook Pipeline (Mandatory)

### Depends On It (Down stream)
- Image Pipeline (Mandatory)
- Existing Brownfields Recovery Pipeline (Mandatory)

![Cookbook Pipeline](/images/policyfile_pipeline.png)

### Code
https://github.com/anthonygrees/policyfile_pipeline

---
## Image Pipeline

### Description

### Depends On (Up stream)
- Policyfile Pipeline (Mandatory)

### Depends On It (Down stream)
- All Provisioning Pipelines (Mandatory)

![Cookbook Pipeline](/images/image_pipeline.png)

### Code
https://github.com/anthonygrees/image_pipeline

---
## Existing Brownfields Recovery Pipeline

### Description

### Depends On (Up stream)
- Policyfile Pipeline (Mandatory)

### Depends On It (Down stream)
- All Pipelines for Existing OS's and Middleware (Mandatory)

![Brownfields Pipeline](/images/brownfields_pipeline.png)

### Code
https://github.com/anthonygrees/existing_brownfields_pipeline

---
## License and Author

* Author:: Matt Ray <matt@chef.io>
*       :: Anthony Rees <anthony@chef.io>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
