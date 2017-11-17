# Satellite-6-Demo

Demo Prep
Delete serverc from Satellite
Hosts->Content Hosts
Select serverc and click Unregister Host.  Choose “Completely” option.

High Level Walkthrough
Talk about Context menu

Show Subscription and Manifest Info
 Content->Red Hat Subscriptions
Show Product Details, Consumed, Start/End Dates, Provided Products.
Show Associations->Activation Keys and Content Hosts.
Show “Manage Manifest”, Upload.  Note the local CDN URL.
Lab environment is disconnected Satellite server.  So content ISOs are used to populate the repositories.
Show Repo and Sync Info

Content → Red Hat Repositories, then the RPMs tab.
Expand the Red Hat Enterprise Linux Server section, then expand the Red Hat Enterprise Linux 7 Server (RPMs) subsection.  Note that it is enabled.  You might not want to enable all repositories available as that will consume storage.

Content → Products
When Red Hat repositories are enabled on Satellite Server using the Content → Red Hat Repositories page in the Satellite web UI, a product will be created and will appear on the Content → Product page.

Show sync plans and sync status for the repositories and products.

Content → Sync Status then click the Expand All link.
Click the checkbox next to the Red Hat Enterprise Linux 7 Server RPMs x86_64 7Server repository enabled earlier then click the Synchronize Now button to begin the repository synchronization.
Content Views
Show the “Base” content view for Operations.  This content view has a filter set to include only the packages in the Base package group.

Show how to create a new package group filter.

Show details for content host servera.  Detail tab, note the Base content view.  Errata tab, change the “Show From” parameters to compare installable errata from different content views.

Switch to Finance organization and show the Security Errata content view and filter.

Errata List
Content->Errata
Show the search.  Search for cve = CVE-2016-1762
type = bugfix and title ~ sos

Show Activation Keys
Content->Activation Keys     Operations Servers
Talk through all the tabs.

Unregister servera and re-register it with the Activation key
# subscription-manager unregister
# subscription-manager register --org='Operations' --activationkey='OperationsServers'
Show Administer Menu
Users - email prefs
LDAP Authentication

Show Host Search Capabilities
Hosts->All Hosts



Satellite and Capsule status and data usage

Show Satellite / Capsule
Infrastructure->Capsules->satellite.lab.example.com



Provision New Server
Select Operations@Boston location and organization

Show Domains and Subnet settings
Infrastructure->Domains->boston.lab.example.com->Domain tab

Show mapping between DNS domain and satellite/capsule server.  Any hosts provisioned for this domain will be directed to get A records from the satellite server.

Infrastructure->Subnets->Boston Data Center->Subnet tab

Show network, gateway, DNS and DHCP settings.

	Capsules tab - shows capsule server settings for various infrastructure services

Walk through Hosts->Provisioning Setup section
Architectures
Hardware Models
Installation Media
Operating Systems
Installation Media
Hosts->Installation media
Hosts->Partition Tables
Provision New Host
 Hosts->New Hosts                       MAC = 52:54:00:00:fa:0c

Register Host
katello-ca-consumer-latest.noarch.rpm will only make changes to /etc/rhsm/rhsm.conf and provide the necessary cert and move them to appropriate place, but it won't allow any access to satellite content until unless registration performed via subscription-manager
Creating Products with Repository Discovery
Content->Products
Click Repo Discovery button
Enter http://content.example.com
Select rhel7.1/x86_64/dvd and click Create Selected.
Change repository name if desired.
Click Create button.
Click check box next to RHEL 7.1 repository, then click Sync Now.



Notes
In network environments where DHCP and TFTP protocols are allowed, Satellite can work in conjunction with an organizations existing and TFTP infrastructure, or it can host and manage those services directly.  In network environments where DHCP and TFTP protocols are not allowed, system deployment can be carried out using boot disk (image-based) provisioning.

# ethtool -P eth0                     # return MAC address

On the Satellite server, /var/www/html/pub can be used to store files which can then be accessed via HTML at http://satellite.lab.example.com/pub/<filename>

The "RHEL 5 Server" channel will always contain the latest RHEL 5. If you require to stay on a specific minor version, then we do provide an Extended Update Support [1] channel for some RHEL 5 releases (and all RHEL6), however 5.8 is not an EUS release so that wouldn't have done much good here.
With our Satellite product, you're able to clone a channel to a certain date. You could create a clone of the "RHEL 5 Server" channel say the day before RHEL 5.9 goes GA (check dates at [2]) then use that custom channel as your "RHEL 5.8 Channel".
As the above posters have indicated, we have an ABI guarantee [3] which extends to all components of the OS. Third-party software should should work fine across all minor releases (5.x) of a major release (5). A userspace application probably has no awareness of the kernel version you are running, a kernelspace component will probably just need a recompile. If such a thing stops working, then please open a support case to let us know, as we put a huge amount of development and testing effort into compatibility, and we will usually fix regressions as a priority.
[1] https://access.redhat.com/support/policy/updates/errata/
[2] https://access.redhat.com/knowledge/articles/3078
[3] https://access.redhat.com/knowledge/articles/119073

Provisioning
system administrator can also boot blank hosts to use the Satellite Server’s discovery service, which creates a pool of ready-to-provision hosts. Systems can also boot and be provisioned through PXE-less methods.


