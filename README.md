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

The Synch Status screen will now show the progress of synching the repositories to Satellite.  Since this is the first time you are synching content, it will take a bit of time to complete.  You will likely want to look at creating a synch plan to schedule synchronizing content during times where your network traffic is less.  When a repository has completed synching, you will see a message next to the repo that says Synching Complete.  Note: for a lab practice run, you may want to only synch content for RHEL 7 or 8 and not both.

![Synch Status Screen in action](/images/sat24.png)

### Creating Content Lifecycles in Satellite
After your content has completed synching, we will create a content lifecycle.  Content lifecycles gives you the ability match RHEL errata to RHEL servers running in particular environment too match your SDLC.  You may simple or complex lifecycles for your RHEL servers, and Satellite give you the ability easily create and manage those RHE server lifecycles.   In the following section will you use the command to create the lifecyce environment in Satellite.

Lets create our first lifecyce environment and link it to the Operations Deparment
```
# hammer lifecycle-environment create --description le-ops-rhel8-prem-server --prior Library --name le-ops-rhel8-prem-server --organization "Operations Department"
Environment created.
```
You can list the any lifeccycle environements with the following command.
```
# hammer lifecyce-environment list
```  

If you want to only list information for a particular organization add the --organization <organziation name> to the command.  
  
Next we will add a content view to the lifecycle environment.  Content view allows to control the specific content made available to environments
```
# hammer content-view create --description cv-rhel8-prem-server --name cv-rhel8-prem-server --organization "Operations Department"
Content view created.
```

 We want to add the repositories to the content view.  For this we need the repository ID.  The following command provides "shorter" view of the repositories listing only the repository ID and name
 

 ```
# hammer repository list --fields THIN --organization-label operations
---|-----------------------------------------------------------------
ID | NAME                                                            
---|-----------------------------------------------------------------
5  | Red Hat Enterprise Linux 7 Server - Extras RPMs x86_64          
6  | Red Hat Enterprise Linux 7 Server - Optional RPMs x86_64 7Server
7  | Red Hat Enterprise Linux 7 Server RPMs x86_64 7Server           
2  | Red Hat Enterprise Linux 8 for x86_64 - AppStream RPMs 8        
3  | Red Hat Enterprise Linux 8 for x86_64 - BaseOS RPMs 8           
8  | Red Hat Satellite Maintenance 6 for RHEL 7 Server RPMs x86_64   
9  | Red Hat Satellite Tools 6.9 for RHEL 7 Server RPMs x86_64       
4  | Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 RPMs              
---|-----------------------------------------------------------------
```

For the RHEL content view we need IDs 2, 3 and 4.
```
# hammer content-view update --repository-ids 2,3,4 --name "cv-rhel8-prem-server" --organization "Operations Department"
Content view updated.
```
  
Next we will publish the repositories to the library.  This will take a few minutes while the content is being published to the content view.
```
# hammer content-view publish --name "cv-rhel8-prem-server" --organization "Operations Department" --async
Content view is being published with task c050e764-25da-43b2-8a23-9122af5a9120.
```
We can jump back to the Satellite console to view the content being published.  On the left side navigation bar chose Content -> Content View.
  
![Content -> Content View](/images/sat25.png)
  
On the Content Views screen click the link Content View name.
  
![Content View Name](/images/sat26.png)
  
You will now see the content being published to the Content View.
![Content View Publishing](/images/sat27.png)

Let's promote the repository from the Library to the...
```
# hammer content-view version promote \
--content-view "cv-rhel8-prem-server" \
--to-lifecycle-environment "le-ops-rhel8-prem-server" \
--organization "Operations Department" \
--async
Content view is being promoted with task bdf2dba3-c4dd-4a66-8e82-a9fbd71b4298.
```
When the update has completed, you will see two environments listed in the Satellite console under Content -> Content Views. In the Content Views page in the Environments section you will see Library and e-ops-rhel8-prem-server listed.
  
TO-DO ???  Add screen shots and notes about reviewing the content view page.....
  
  
## References  
[Understanding Red Hat Content Delivery Network Repositories and their usage with Satellite 6](https://access.redhat.com/articles/1586183)
