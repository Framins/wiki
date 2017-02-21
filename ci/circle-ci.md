Circle CI
===

Primary sections
---
    # circle.yml

    machine: adjusting the VM to your preferences and requirements
    checkout: checking out and cloning your git repo
    dependencies: setting up your project’s language-specific dependencies
    database: preparing the databases for your tests
    test: running your tests
    deployment: deploying your code to your web servers

* [Sample circle.yml file](https://circleci.com/docs/config-sample/)

Concepts
---
- Each command is run in a separate shell. If you’d like to set an environment variable globally, you can specify them in the `machine` section
- Cannot read UI environment variables during the `machine: pre`
- Caching happens after the dependency step, so the directories that are specified in cache_directories must be available before then.
- A non-zero exit code during the setup sections (machine:, checkout:, dependencies:, database:) will cause the build to fail early. But all test commands will run, even if one fails.
- Deployment sections are triggered only after a successful (green) build.

Default
---
- Base image: Ubuntu 12.04
- Timezone: UTC
- Databases: Postgres, MySQL, Redis and MongoDB
- Testing parallel directories: test/unit, test/integration, and test/functional

Reference
---

- [Circle CI](https://circleci.com/)
- [Environment variables](https://circleci.com/docs/environment-variables/)
- [Start background processes](https://circleci.com/docs/background-process/)
