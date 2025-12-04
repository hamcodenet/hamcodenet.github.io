+++
title = 'Run GitLab CI Jobs on a Specific Runner'
date = 2024-10-31T00:00:00+00:00
draft = false
tags = ['gitlab', 'ci-cd', 'devops', 'runner', 'deployment']
+++

I have two runners in my project. One is on Microsoft Azure for Azure deployments, and the other is on DigitalOcean for its deployments. Today, I realized that all of my jobs are being handled by the Azure runner, causing our tests to take too much time due to significant network delay when connecting to the database across data centers.

Therefore, I needed to configure specific jobs to run on designated runners. Here, I'll explain how to do that.

To assign a specific GitLab Runner to a job in your GitLab CI/CD pipeline, use the `tags` keyword in the job definition in your `.gitlab-ci.yml` file. You'll need to add a unique tag to the runner configuration in GitLab and then reference that tag in the job configuration. Here's how:

## Step 1: Add a Tag to the Runner

1. Go to your project's **Settings > CI / CD**.
2. Under **Runners**, locate the runner you want to assign to your job.
3. Click on **Edit** (pencil icon) next to the runner and add a unique tag (for example, `azure-runner`).

## Step 2: Use the Tag in Your `.gitlab-ci.yml`

Add the same tag to your job definition in the `.gitlab-ci.yml` file:

```yaml
job_name:
  stage: build
  script:
    - echo "Running job on an Azure runner"
  tags:
    - azure-runner
```

## Explanation

**tags**: By specifying the `azure-runner` tag, GitLab ensures this job will only be picked up by runners that have this tag.

![GitLab Runner Tags](/images/gitlab-runner-tags.webp)

Now, if you take a look at your job on GitLab, you will see that it is assigned to the specific runner you specified.
