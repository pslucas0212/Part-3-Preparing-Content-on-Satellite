# Part 3: Preparing Content on Satellite  

Part 3: Preparing Content on Satellite

In the section we will learning about managing content for our RHEL environment.  We will add RHEL repositories to Satellite and define RHEL patching lifecycles.  

### Adding Software Repositories to Satellite. 

For our tutorial we will enable both RHEL 7 and RHEL 8 repositoires to Satellite.  

Loging to the Satellite console and on the right menu bart navigate to Conent -> Red Hat Repositories.  Make sure that your organization and location is set Operations Department and moline.  Remember Organization and Location are located in the upper left area of the Satellite console

![Content -> Red Hat Repositories](/images/sat15.png)

We will first searh for RHEL 8 repositories.  Enter RHEL 8 x86_64 in the search field, click the Search button and then toggle Recommended Repositories swith to On.  

![Red Hat Repositories Search](/images/sat16.png)

You will now see a smaller set of repositories.  We will be enabling three RHEL 8 Repositories:

Name | Repository
---- | ----------
Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs) | rhel-8-for-x86_64-appstream-rpms
Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs) | rhel-8-for-x86_64-baseos-rpms
Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 (RPMs) | satellite-tools-6.9-for-rhel-8-x86_64-rpms

![Red Hat Repositories Search Results](/images/sat17.png)

To enable a repository, click the twisty to the left of the repository name and the click the blue plus. If you hover over the blue plus you will see pop up that says enable.  It is recommended enable the version release of a RHEL repository and not the point release.

![Expand Twisty](/images/sat18.png)

After you click the blue plus sign, you will see the selected repository is now in the right column titled Enabled Repositories.

![Enabled Repositories](/images/sat19.png)

Repeat the steps above to enable the other RHEL 8 repositories

![All RHEL 8 Enabled Repositories](/images/sat20.png)



## References
[Understanding Red Hat Content Delivery Network Repositories and their usage with Satellite 6](https://access.redhat.com/articles/1586183)
