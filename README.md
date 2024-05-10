# okta-workflows
## Group Sharding ##
### Intro ###
One of the ways we test configurations in Okta is creating a group and adding folks to it. Usually after the first few folks have been added, we need to increase the group to a certain percentage of users before evaluating if the configuration is ready to be applied to everyone.

Sharding is the idea of deploying a change to a large group, but doing it in small chunks. This Okta Workflow set is a bit over engineered and there's definitely a few more ways to accomplish this. Hopefully this helps folks when figuring out how to deploy a change.

### How it works ###

Using a config table (this is designed to be quickly templated), fill out test groups and group size limitation. Then a series of workflows pulls all active uses from a specific group. It adds a random number to each row to make picking fairly straight forward. Once that is complete, another workflow pulls users from the test group and subtracts them from the other group. This is all done in tables so you can see the progress. Once the setup work is done, a workflow runs that picks the first row from the active user group with that random number and adds it to the test group. Lastly, a bit of cleanup is done to make sure that user doesn't get picked again and to make sure the test group doesn't go over a certain number.

There are a few variables in these workflows that are designed to speed up or slow down group ads. For instance if you set the max size to 300, there will never be more than 300 users in the group. To expand testing, increase the max group size and the workflow gradually adds users,

### Table Config ###
Open the config table in the tables section of the folder.
![Config Table](/images/1.png)
- **Difference** : This was an attempt at doing some live math. I'm leaving that there for for now. One of the ideas I had with this was sending a notification such as "There are X number of people to add to the group".
- **Group ID** : Add the groupID of the group that is going to get the users
- **Maximum Number** : This is the max number of accounts in the group. Set this to whatever number you want.
- **Current Number** : This is the current number of people in the group. Leave this blank.
### Workflow Config ###
Each numbered section corresponds to the numbered workflow in the folder.



### Conclusion ###
