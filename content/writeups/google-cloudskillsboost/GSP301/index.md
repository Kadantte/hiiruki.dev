---
title: "[GSP301] Deploy a Compute Instance with a Remote Startup Script"
description: ""
summary: "Quest: Cloud Architecture: Design, Implement, and Manage"
date: 2023-05-22T04:13:03+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["writeups", "challenge", "google-cloudskillsboost", "gsp301", "google-cloud", "cloudskillsboost", "juaragcp", "google-cloud-platform", "gcp", "cloud-computing", "cloud", "cloud-architecture"]
canonicalURL: ""
showToc: true
TocOpen: false
TocSide: 'right'  # or 'left'
weight: 2
# aliases: ["/first"]
hidemeta: false
comments: false
disableHLJS: true # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
# UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/blob/main/content/writeups/google-cloudskillsboost/GSP301/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

### GSP301

![Lab Banner](https://cdn.qwiklabs.com/GMOHykaqmlTHiqEeQXTySaMXYPHeIvaqa2qHEzw6Occ%3D#center)

- Time: 1 hour<br>
- Difficulty: Intermediate<br>
- Price: 5 Credits

Lab: [GSP301](https://www.cloudskillsboost.google/focuses/1735?parent=catalog)<br>
Quest: [Cloud Architecture: Design, Implement, and Manage](https://www.cloudskillsboost.google/quests/124)<br>

## Challenge scenario

You have been given the responsibility of managing the configuration of your organization's Google Cloud virtual machines. You have decided to make some changes to the framework used for managing the deployment and configuration machines - you want to make it easier to modify the startup scripts used to initialize a number of the compute instances. Instead of storing startup scripts directly in the instances' metadata, you have decided to store the scripts in a Cloud Storage bucket and then configure the virtual machines to point to the relevant script file in the bucket.

A basic bash script that installs the Apache web server software called `install-web.sh` has been provided for you as a sample startup script. You can download this from the Student Resources links on the left side of the page.

## Your challenge

Configure a Linux Compute Engine instance that installs the Apache web server software using a remote startup script. In order to confirm that a compute instance Apache has successfully installed, the Compute Engine instance must be accessible via HTTP from the internet.

### Task 1. Confirm that a Google Cloud Storage bucket exists that contains a file

Go to cloud shell and run the following command:

```bash
gsutil mb gs://$DEVSHELL_PROJECT_ID
gsutil cp gs://sureskills-ql/challenge-labs/ch01-startup-script/install-web.sh gs://$DEVSHELL_PROJECT_ID
```

### Task 2. Confirm that a compute instance has been created that has a remote startup script called install-web.sh configured

```bash
gcloud compute instances create example-instance --zone=us-central1-a --tags=http-server --metadata startup-script-url=gs://$DEVSHELL_PROJECT_ID/install-web.sh
```

### Task 3. Confirm that a HTTP access firewall rule exists with tag that applies to that virtual machine

```bash
gcloud compute firewall-rules create allow-http --target-tags http-server --source-ranges 0.0.0.0/0 --allow tcp:80
```

### Task 4. Connect to the server ip-address using HTTP and get a non-error response

After firewall creation (Task 3) just wait and then check the score

## Congratulations!

![Congratulations Badge](https://cdn.qwiklabs.com/%2FaI3EMiHeGZc46u89ueTTAEgmRSGj5krSwhpzllr88w%3D#center)
