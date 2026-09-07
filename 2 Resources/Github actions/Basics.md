**Workflows**, yaml files that include steps for the workflow. 

**On** - trigger for the workflow, you can have multiple for eks pull request to the main branch.
Workflow_dispatch - allows to trigger jobs manually
**Jobs** - jobs that will run as part of current pipeline, pipeline should have at least one job.
**Runner** - machine that will run pipeline
**Steps** - describe what should run inside the runner
-uses, name, run

Github has marketplace for different actions.

-How to trigger workflow manually, and add params
workflow_dispatch -> inputs: name, description, default, required

