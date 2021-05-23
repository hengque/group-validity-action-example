# Proof of concept for the group-validity-action

This repository serves as a proof of concept for the GitHub action **group-validity-action** that was made for the course *DD2482 Automated Software Testing and DevOps*, given at KTH. The action can be found in this repository: https://github.com/EleonoraBorzis/group-validity-action.

## Workflow and parameters showcased
The **group-validity-action** was specifically designed to be used in the course repository for the devops course. Therefore, this repo will follow a similar structure to that of the course repo and a similar workflow will be simulated. This means that:

1. Forks of this repository are made
2. Pull requests with project proposals are made from these forks
3. All valid proposal pull requests add one README in a descendent folder of the *contributions* folder.
    * The README of the proposal is added in a folder named after the KTH ID:s of the group members.
    * The added README must contain the KTH email-addresses of all group members

The parameters for the action will be set to the values used for the devops repository:
* Maximum group size is 3
* Maximum number of times two people are allowed to work together is 2. This is also the maximum number of times one is allowed to work alone.
* All file additions made outside of the *contributions* folder (and its subfolders) are ignored

Consequently, if there is not exactly one README added under *contributions* the pull request is assumed to not be a project proposal.

## Structure and scenarios
The root has two folders, *other* and *contributions*. The *other* folder simply represents the space outside of the *contributions* folder. The *contributions* folder has 3 subfolders: *demo*, *tutorial* and *presentation*, representing the categories of tasks one can do. Within these 3 folders the project folders of different groups are added. The *other* folder and the *presentation* folder are empty, so to force them to show up dummy files called *file.txt* have been added to them.

The following scenarios will be showcased and covers most cases that can be encountered:

1. A group of size 2 makes a project proposal pull request with a correct README. They have worked together 1 time before. Thus this group may work together.
    * The group members *aa* and *bb* have made a demo before, and now wants to make a tutorial.
    * This scenario is shown in pull request: [#1](https://github.com/hengque/group-validity-action-example/pull/1) 
2. A group of size 3 makes a project proposal pull request with a correct README. They have worked together 1 time before. Thus this group may work together. 
    * The group members *cc*, *dd* and *ee* have made a tutorial before, and now wants to make a demo.
    * This scenario is shown in pull request: [#2](https://github.com/hengque/group-validity-action-example/pull/2) 
3. A group of size 1 makes a project proposal pull request with a correct README. This person has worked alone 0 times before. Thus this person may work alone.
    * The group member is *ff* and they want to make a presentation.
    * This scenario is shown in pull request: [#3](https://github.com/hengque/group-validity-action-example/pull/3) 
4. A group of size 2 makes a project proposal pull request with a correct README. They have worked together 2 times before. Thus this group may NOT work together.
    * The group members *gg* and *hh* have made a demo and a tutorial before, and now want to make a presentation.
    * This scenario is shown in pull request: [#4](https://github.com/hengque/group-validity-action-example/pull/4) 
5. A group of size 4 makes a project proposal pull request with a correct README. Since this group is too big, they may NOT work together.
    * The group members *ii*, *jj*, *kk* and *ll* haven't done anything together before, and now want to make a presentation.
    * This scenario is shown in pull request: [#5](https://github.com/hengque/group-validity-action-example/pull/5) 
6. A group of size 2 makes a project proposal pull request with a correct README. They have worked together 2 times before, but as part of a group of 3. This group may NOT work together.
    * The group members *mm*, *nn* and *oo* have made a demo and a tutorial before, and now *mm* and *nn* want to make a presentation.
    * This scenario is shown in pull request: [#6](https://github.com/hengque/group-validity-action-example/pull/6) 
7. A group of size 2 makes a pull request for updating a README for one of their assignments. Since this is not a project proposal, it is ignored.
    * The group members *pp* and *qq* have made a tutorial before, and now want to update that README.
    * This scenario is shown in pull request: [#7](https://github.com/hengque/group-validity-action-example/pull/7) 
8. A pull request adds 2 README:s in folders under the contributions folder. This is assumed not to be a project proposal, and is ignored.
    * The README:s are added in category folders and directly in the contributions folder rather than in folders of a specific group, and thus might be added by for example a teacher's assistant.
    * This scenario is shown in pull request: [#8](https://github.com/hengque/group-validity-action-example/pull/8) 
9. A pull request adds 0 README:s in folders under the contributions folder. This is assumed not to be a project proposal, and is ignored. 
    * A grading criteria file is added in the *demo* folder, for example by a teacher's assistant.
    * This scenario is shown in pull request: [#9](https://github.com/hengque/group-validity-action-example/pull/9) 
10. A pull request adds 1 README outside of the contributions folder. This is assumed not to be a project proposal, and is ignored.
    * The README is added in the *other* folder, for example by a teacher's assistant.
    * This scenario is shown in pull request: [#10](https://github.com/hengque/group-validity-action-example/pull/10) 
11. A group of size 2 makes a project proposal pull request. They have worked together 1 time before. Their README does not contain KTH email-address matching the name of the folder containing the README. Thus the pull request is invalid, although the group may work together.
    * The group members *rr* and *ss* have made a demo before, and now want to make a presentation.
    * This scenario is shown in pull request: [#11](https://github.com/hengque/group-validity-action-example/pull/11) 
12. A group of size 2 makes a project proposal pull request. They have worked together 0 times before. One of the members has worked alone 2 times before. Working alone should count as a subgroup when considering if any subsets of the proposing group has worked together too many times. Thus this group may work together.
    * The group members *tt* and *uu* want to make a presentation. *tt* has made a demo and a tutorial before.
    * This scenario is shown in pull request: [#12](https://github.com/hengque/group-validity-action-example/pull/12) 
