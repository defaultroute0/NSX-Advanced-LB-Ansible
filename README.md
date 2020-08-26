# NSX Advanced Load Balancer (AVI Networks) Ansible Example
Simple automation of load balancing and GSLB concepts.

The NSX Advanced load balancer (formerly https://avinetworks.com/ ) is highly automatable multi-cloud application services LB with elastic application delivery, security, and pervasive analytics across data centers and clouds. Its architectural advantages makes it easy to apply load balancing, web application firewall and container ingress to any application.

The ansible playbooks here will deploy the load balancing needed for a 3 tier application 
Some points on this ansible example:

- Its assumes you have pre existing, two sites each with a AVI controller(s) setup, DNS-VS, and subdomain delegation and owned by AVI GSLB function
- the 3 tier test app at each SITEA and SITEB
- At each site the app has: 
    2 x Web servers (load balanced)
    2 x App servers (load balanced)
    1 x DB servers, (no load balancer here)
- Ansible (avi_create_vs_pool.yml) will create the POOLS, VSVIP, and finally the VS in this order
- Ansible (avi_create_gslb.yml) will create the GSLB record which points to the above apps in each site

- Here's what Ansible will push as a demonstration:
  -  SiteA pools
  -  SiteA VSVIPS
  -  SiteA VS Web Tier  auto allocate VSVIP out of AVI IPAM
  -  SiteA VS App Tier  allocate VIP from static param
  -  SiteB pools
  -  SiteB VSVIPS
  -  SiteB VS Web Tier  auto allocate VSVIP out of AVI IPAM
  -  SiteB VS App Tier  allocate VIP from static param
  -  GSLB Pools for each site
  -  GSLB record for the app sync across both sites
  -  GSLB will direct traffic round robin between the two apps with very short TTL so we can see it in action

The scripts for 'nocloud' were used pre NSX-T Cloud connector available
The scripts for 'nsxtcloud' were used post NSX-T Cloud connector being GA

Installation of Ansible and AVI Networks SDK is here
https://avinetworks.com/docs/18.2/configuring-ansible-for-avi-vantage/configuring-ansible-for-avi-vantage.pdf

Configuring Ansible for AVI Vantage
https://avinetworks.com/docs/18.2/configuring-ansible-for-avi-vantage/

You can search for more info on how these ansible modules work on ansible site 
https://docs.ansible.com/ansible/latest/modules/avi_vsvip_module.html

and also AVI github devops repository or more example:
https://github.com/avinetworks/devops



