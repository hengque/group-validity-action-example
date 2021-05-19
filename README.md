# Proof of concept for the group-validity-action

This repository serves as a proof of concept for the GitHub action **group-validity-action** that was made for the course *DD2482 Automated Software Testing and DevOps*, given at KTH. The action can be found in this repository: https://github.com/EleonoraBorzis/group-validity-action.

## Workflow and parameters showcased
The **group-validity-action** was specifically designed to be used in the course repository for the devops course. Therefore, this repo will follow a similar structure to that of the course repo and a similar workflow will be simulated. This means that:

1. Forks of this repository are made
2. Pull requests with project proposals are made from these forks
3. All valid proposal pull requests add one README in a descendent foldor of the *contributions* folder.
    * The README of the proposal is added in a folder named after the KTH ID:s of the group members.
    * The added README must contain the KTH email-addresses of all group members

The parameters for the action will be set to the values used for the devops repository:
* Maximum group size is 3
* Maximum number of times two people are allowed to work together is 2. This is also the maximum number of times one is allowed to work alone.
* All file additions made outside of the *contributions* folder (and its subfolders) are ignored

Consequently, if there is not exactly one README added under *contributions* the pull request is assumed to not be a project proposal.

## Scenarios
These following scenarios will be showcased and covers most cases that can be encountered:

* A group of size 2 makes a project proposal pull request with a correct README. They have worked together 1 time before. Thus this group may work together.
* A group of size 3 makes a project proposal pull request with a correct README. They have worked together 1 time before. Thus this group may work together. 
* A group of size 1 makes a project proposal pull request with a correct README. This person has worked alone 0 times before. Thus this person may work alone.
* A group of size 2 makes a project proposal pull request with a correct README. They have worked together 2 times before. Thus this group may NOT work together.
* A group of size 4 makes a project proposal pull request with a correct README. Since this group is too big, they may NOT work together.
* A group of size 2 makes a project proposal pull request with a correct README. They have worked together 2 times before, but as part of a group of 3. This group may NOT work together.
* A group of size 2 makes a pull request for updating a README for one of their assignments. Since this is not a project proposal, it is ignored.
* A pull request adds 2 README:s in folders under the contributions folder. This is assumed not to be a project proposal, and is ignored.
* A pull request adds 0 README:s in folders under the contributions folder. This is assumed not to be a project proposal, and is ignored. 
* A pull request adds 1 README outside of the contributions folder. This is assumed not to be a project proposal, and is ignored.
* A group of size 2 makes a project proposal pull request. They have worked together 1 time before. Their README does not contain KTH email-address matching the name of the folder containing the README. Thus the pull request is invalid, although the group may work together.
