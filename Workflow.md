# Table of Content
1. [Issues](https://github.com/daodc/Front-End-Develop-Technical/wiki/WorkFlow#issues)
  1. [Issue Type Labels](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#type-labels-required) 
  2. [Ranking Labels](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#rank-labels-optional) 
  3. [Component Labels](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#component-labels-always-required) 
  4. [Status Labels](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#status-required) 
2. [Branches](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow##branches)
  1. [Hotfix Branch](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#hotfix)
  2. [Feature Branch](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#feature)

3. [Pull-Request](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#pull-request-pr)
  1. [PR Status Workflow](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#pr-status-workflow)
  2. [PR Labeling](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#pr-labeling)
  3. [PR Code Review](https://github.com/daodc/Front-End-Develop-Technicals/edit/master/WorkFlow#pr-code-review)

***


# Github Workflow
## Issues 

### Type Labels (required)
_Only 1 per issue._

`type-Feature` is for task that affect directly the functions of a product for example: creating a new page, form, api fix, etc.

`type-Bug` is for bugs raised by QC or internal team.

`type-BugClient` is for bugs raised by the Client.

`type-Task` is for task that do not contribute directly to the functions of the product for example: Deployment script, database cleaning, investigation etc.

### Rank Labels (optional)
_Only 1 per issue. Only required by type-Bug or type-BugClient_

`rank-A-High` For Feature: Important feature on its own but may not have many dependencies. For Bug: important function and need to be fixed within 1 day. 

`rank-B-Normal` For Feature: a single web page? For Bug: should be fixed within 3 days.

`rank-C-Low` For Feature: lowest priority. For Bug: minor bugs, lowest priority, allowed time is 1 week.

### Component Labels (always REQUIRED)
_Can be multiple component._

`comp-Frontend` is for HTML/CSS/JS related tasks


1 Issue or PullRequest can have as many component Labels as long as they are related to the issue.

### Status (required)
_Only 1 per issue._

`status-01-New` every Issue should be always created with this status.

`status-02-InProgress` Once someone starts working on this issue, it must be in this state. PM will use this state to check who's working on what at the moment. This is set by the **developer**.

`status-03-Fixed` Once developer have referenced this issue in a PullRequest then it's set to Fixed by **developer**.

`status-04-Reviewed` Once someone reviewed and merged the PR into major branch (master/develop) then the  referenced issues must be set to reviewed by the **Reviewer**.

`status-05-Deployed` Once someone deploy to **Edge** server for Phase 2 or **STG** for Phase 1 Maintenance then all the issues with label status-04-reviewed must be set to status-05-deployed by the **Deployer**.

`status-06-Reopened` Issues deployed will be verified by QC and will be set to reopened if it can not pass the QC check. This status is treated similar to status-01-New and will go through the steps like a new issue. This status is set by **QC**.

`status-07-Done` If QC approve the issue then this issue is set to Done. This is set by **QC**. If it's inside a normal Phase Milestone then it will be Closed. If it's inside a Maintenance Milestone then it will be closed once the Release to Production is finished by the Deployer.

`status-08-Pending` If a ticket is waited for answer from Client or BA. Once you have the answer back please update the status of this ticket right away. BA please update the answer in the comment section. Avoid using this status and discuss with BA/QC/PM/TL right away.

## Branches
Only PM or TLs (with permission from PM) are allowed to delete branch, even the merged ones.

**Branch Naming Convention**

### Hotfix
* To be created from `origin/master` branch.
* Pull requests must also merge back into `master`.

`hotfix/YYYYMMDD-firstname-long_description#issueNumber` For fixing bugs in Maintenance Milestone

_For example: hotfix/20151225-daodc-fix_IE_footer_item_detail#343_

### Feature
* To be created from `origin/develop` branch.
* Pull requests must also merge back into `develop`.

`feature/YYYYMMDD-firstname-long_description#issueNumber` For new feature during normal Milestone

_For example: feature/20151225-daodc-create_page_rental_item_list#2394_

_For example: feature/20151225-daodc-FIX1_create_page_rental_item_list#2394_ (reopened)

_For example: feature/20151225-daodc-FIX2_create_page_rental_item_list#2394_ (reopened 2 times)

## Pull Request (PR)
### PR Status workflow
```
Best case      : [status-01-New] -> [status-02-InProgress] -> [status-04-Reviewed]
Reopen case    :                                           -> [status-06-Reopened] -> [status-03-Fixed] -> [status-04-Reviewed]
2 Reviewer case:                                           -> [status-04-Reviewed + status-01-New] -> [status-04-Reviewed + status-02-InProgress] -> [status-04-Reviewed]
```
Once a Pull Request is in status "Reviewed", it's safe to merge unless there's merge conflicts.

* `status-01-New` New PR just got **created** by Developer
* `status-02-InProgress` PR being **reviewed** by Reviewer
* `status-04-Reviewed` PR has been **approved** by Reviewer(s)
* `status-06-Reopened` PR has been **rejected** by Reviewer(s)
* `status-03-Fixed` PR has been **fixed** by Developer after rejection and waiting for reviewing again.

### PR Labeling
* Every Pull Request must be assigned to someone.
* Every PR **must have:**
  * 1+ `comp-` label (multiple if references issues belong to multiple components)
  * 1+ `status-` label
  * 1+ `type-` label (multiple depends on referenced)
  * 1 `rank-` label (get the highest rank of the referenced issues)
  * `Milestone` must be assigned. (Set/updated by **Developer/Reviewer**)

### PR Code Review
* Developer assign `comp-frontend` PR to @daodc 
* Developer must make sure no Robot error message before assigning the PR to someone to review.
* Developer must comment directly on these comments if he refuse to fix.

* Reviewer must test the PR on his local deployment and make line comment. 
* Reviewer in case you have finished reviewing, please reassign the PR back to the final reviewer below:
  * Only @daodc or @name1, @name2 is allowed to merge/close for `comp-frontend`. 
