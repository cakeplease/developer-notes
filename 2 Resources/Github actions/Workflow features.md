
Reusable workflows:
- reusing workflows avoids duplication
- - easier to maintain
- -developing new workflows is faster than reusing the existing ones
- creates central library for workflows where best practices are applied

limitations:
- you can connect up to four levels of workflows
- workflows stored within private repo can only be used by workflows within same repo
- any env vars set in an env context defined at the workflow level in the caller workflow are not propagated to the called workflow

Workflow_call: inputs, secrets, token, jobs

![[Screenshot 2026-09-07 at 09.50.38.png]]

![[Screenshot 2026-09-07 at 09.52.05.png]]