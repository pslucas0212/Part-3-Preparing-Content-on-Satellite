# Part 3: Preparing Content on Satellite  

Part 3: Preparing Content on Satellite

In the section we will learning about managing content for our RHEL environment.  We will enable RHEL repositories on Satellite and define RHEL patching lifecycles.  

### Adding Software Repositories to Satellite. 

For our tutorial we will enable both RHEL 7 and RHEL 8 repositoires to Satellite.  

Loging to the Satellite console and on the right menu navigate to Conent -> Red Hat Repositories.  Make sure that your organization and location is set Operations Department and moline.  Remember Organization and Location are located in the upper left area of the Satellite console

![Content -> Red Hat Repositories](/images/sat15.png)

We will first searh for RHEL 8 repositories.  Enter RHEL 8 x86_64 in the search field, click the Search button and then toggle Recommended Repositories swith to On.  

![Red Hat Repositories Search](/images/sat16.png)

You will now see a smaller set of repositories.  We will be enabling three RHEL 8 Repositories:

Name | Repository
---- | ----------
Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs) | rhel-8-for-x86_64-appstream-rpms
Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs) | rhel-8-for-x86_64-baseos-rpms
Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 (RPMs) | satellite-tools-6.9-for-rhel-8-x86_64-rpms

![Red Hat Repositories Search Results RHEL 8](/images/sat17.png)

To enable a repository, click the twisty icon to the left of the repository name and then click the blue plus icom. If you hover over the blue plus icon you will see a pop up text that says enable.  It is recommended to enable the version release of a RHEL repository and not the point release.  We chose the version release of the RHEL repository as it contains all errata from GA until that release is no longer supported.

![Expand Twisty](/images/sat18.png)

After you click the blue plus sign, you will see the selected repository is now in the right column titled Enabled Repositories.

![Enabled Repositories](/images/sat19.png)

Repeat the steps above to enable the other RHEL 8 repositories.  When you are finished, the Satellite console should look like the screen shot below.

![All RHEL 8 Enabled Repositories](/images/sat20.png)

We will now enable some RHEL 7 repositories.  This time enter RHEL 7 in the search field, click the Search button and then toggle Recommended Repositories switch to On.  

![Red Hat Repositories Search Results RHEL 7](/images/sat21.png)

See the following table for the RHEL 7 repositories we will enable.  Follow the steps above to enable each repository. 

Name | Repository
---- | ----------
Red Hat Enterprise Linux 7 Server - Extras (RPMs) | rhel-7-server-extras-rpms
Red Hat Enterprise Linux 7 Server - Optional (RPMs) | rhel-7-server-optional-rpms
Red Hat Enterprise Linux 7 Server (RPMs) | rhel-7-server-rpms
Red Hat Satellite Maintenance 6 (for RHEL 7 Server) (RPMs) | rhel-7-server-satellite-maintenance-6-rpms
Red Hat Satellite Tools 6.9 (for RHEL 7 Server) (RPMs) | rhel-7-server-satellite-tools-6.9-rpms

We have chosen the content we need to manage for our RHEL environment.  Now we need to synch that content to Satellite.  We will "manually" synch the content.  You can create synch plan, but we won't be covering creating a synch plan in this tutorial.  

On the right naviagtion bar click Content -> Synch Status

![Content -> Synch Status](/images/sat22.png)

On the Synch Status page click on the Expand All and Select All links.  And click the Synchronize Now button.

![Synch Status Screen](/images/sat23.png)

The Synch Status screen will now show the progress of synching all of the repositories to Satellite.  Since this is the first time you are synching content, it take a bit of time to complete.  You will likely want to investigate creating a synch plan to schedule synchronizing content during times where your network traffic is less.

![Synch Status Screen in action](/images/sat24.png)


## References
[Understanding Red Hat Content Delivery Network Repositories and their usage with Satellite 6](https://access.redhat.com/articles/1586183)
