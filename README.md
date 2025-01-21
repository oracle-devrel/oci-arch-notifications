# oci-arch-notifications

[![License: UPL](https://img.shields.io/badge/license-UPL-green)](https://img.shields.io/badge/license-UPL-green) [![Quality gate](https://sonarcloud.io/api/project_badges/quality_gate?project=oracle-devrel_oci-arch-notifications)](https://sonarcloud.io/dashboard?id=oracle-devrel_oci-arch-notifications)

## Introduction

This repository contains the code created to illustrate how a custom application can generate and send OCI Notifications.  There is a detailed playbook that walks through the process execution of this solution, configuration of OCI Notifications and then receiving notifications with a Slack account and via a Mock Server REST API endpoint (the document assumes Postman). The playbook can be found **here**.

This functionality has been written so it can be run as a standalone solution and will generate simple notification messages or as a custom plugin to an open source tool called [LogGenerator](https://github.com/mp3monster/LogGenerator) - which has the ability to playback not only logs but structured logs but any textual record and substitute certain values such as timestamps so that the destination will perceive data as being presented as new current events.

The logic has been written using Groovy that remains compliant to Java 8 syntax and not dependent upon an Groovy custom libraries. This means that you can either immediately run the code using Groovy on top of your JDK or setup a Java build process with your preferred tool (Gradle, Maven etc.) and run it as you would prefer. This does mean you can also refactor the code into your own solution easily. Alternatively use Groovyc to generate class files and incorporate things that way.

Note - to keep dependencies as simple as possible for running with Groovy, logging is  simply to the console and controlled by an environment variable.

## Getting Started
Review the **playbook** and apply the prerequisites.

### Prerequisites
The following resources are needed to run this solution:

- [Java JDK 8](https://www.oracle.com/uk/java/technologies/javase/javase8-archive-downloads.html) or later
- [Groovy 3](https://groovy.apache.org/download.html) (or later)
- [OCI Java SDK](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/javasdk.htm)
- [Oracle Cloud Account](https://cloud.oracle.com)
- OCI configuration as described **here**.
- OCI SDK Configuration properties file

If you wish to run this as a pure Java solution. You will need to setup: your preferred means to build Java apps:

- [Gradle](https://gradle.org/) or [Maven](https://maven.apache.org/) etc
- Build configuration e.g. Maven POM

If you wish to leverage the logic as part of a more advanced [LogGenerator](https://github.com/mp3monster/LogGenerator) derived setup then the same prerequites are required, plus additional configuration data as detailed [here](https://github.com/mp3monster/LogGenerator). 

### Solution Specific Configuration

To configure the behavior the following environment variables need to be provided (in the LogGenerator solution these are taken from a properties file).

| Environment Variable Name | Description                                                  |
| ------------------------- | ------------------------------------------------------------ |
| BATCHSIZE                 | How many messages to be grouped into a single call to OCI Notifications. This defaults to 1. For OCI Notifications there isnt any reason to change this. |
| TOPICOCID                 | The OCID identifier for the Topic to be used.                |
| REGION                    | The OCI Region name e.g. us-ashburn-1 where the Topic has been setup. |
| OCICONFIGFILE             | The path to the file that will be used by the SDK to workout the URL and authenticate with OCI |
| JSONFmt                   | Whether the generated notification content should be plain text (default) and suited for Slack or as a JSON payload (necessary for the mock server or any other application consumer). Needs to have the value true to take effect. |
| verbose                   | Tells the logging whether it should write its output to console or not. If set to a value of true then the code will report what it is doing. |



## Notes/Issues

None at this time.

## URLs
* [cloud.oracle.com](https://oradocs-prodapp.cec.ocp.oraclecloud.com/documents/link/LDB5E5A64FC2812D39FB2B92C5B8A4023822A576F9DB/fileview/D3687C9FB8BE89832D7415A350DDF16ABB00D5A43B76/_using-ons-with-applications.docx)

## Contributing

This project is open source.  Please submit your contributions by forking this repository and submitting a pull request!  Oracle appreciates any contributions that are made by the open source community.

## License
Copyright (c) 2024 Oracle and/or its affiliates.

Licensed under the Universal Permissive License (UPL), Version 1.0.

See [LICENSE](LICENSE.txt) for more details.

ORACLE AND ITS AFFILIATES DO NOT PROVIDE ANY WARRANTY WHATSOEVER, EXPRESS OR IMPLIED, FOR ANY SOFTWARE, MATERIAL OR CONTENT OF ANY KIND CONTAINED OR PRODUCED WITHIN THIS REPOSITORY, AND IN PARTICULAR SPECIFICALLY DISCLAIM ANY AND ALL IMPLIED WARRANTIES OF TITLE, NON-INFRINGEMENT, MERCHANTABILITY, AND FITNESS FOR A PARTICULAR PURPOSE.  FURTHERMORE, ORACLE AND ITS AFFILIATES DO NOT REPRESENT THAT ANY CUSTOMARY SECURITY REVIEW HAS BEEN PERFORMED WITH RESPECT TO ANY SOFTWARE, MATERIAL OR CONTENT CONTAINED OR PRODUCED WITHIN THIS REPOSITORY. IN ADDITION, AND WITHOUT LIMITING THE FOREGOING, THIRD PARTIES MAY HAVE POSTED SOFTWARE, MATERIAL OR CONTENT TO THIS REPOSITORY WITHOUT ANY REVIEW. USE AT YOUR OWN RISK. 