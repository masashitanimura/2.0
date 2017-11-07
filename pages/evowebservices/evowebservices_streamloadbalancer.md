---
title: Stream Load Balancer
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_streamloadbalancer.html
folder: evowebservices
toc: true
---

The Load Balancer web service ensures that a group of EMS instances maintain the same collection of inbound (source) streams.

When a new stream is created on one EMS, this web service will tell all the other EMS instances to also to and get that stream.

The list of EMS instances the Load Balancer will maintain is defined in the config.ini file:

1. **destination_ems_apiproxies**. The array of ip address where the inbound streams would be replicated to. The details in this parameter is seen in the webconfig.json of the address to be used.

   ```
       "StreamLoadBalancer": {
           "plugin_switch": "enabled",
           "parameters": {
               "destination_ems_apiproxies": [
                   {
                       /* for Enabled API Proxy */
                       "enable" : true,
                       "authentication": "basic",
                       "pseudoDomain": "apiproxy",
                       "address": "192.168.2.3",
                       "ewsPort": 8888,
                       "userName": "username",
                       "password": "password"
                   },
                   {
                       /* for Disabled API Proxy */
                       "enable" : false,
                       "address": "192.168.2.4",
                   },
                   {
                       "enable" : true,
                       "authentication": "basic",
                       "pseudoDomain": "apiproxy",
                       "address": "192.168.2.6",
                       "ewsPort": 8888,
                       "userName": "username",
                       "password": "password"
                   }
               ]
           }
       }, 
   ```

   - **enable** - the api proxy configuration in webconfig.json
   - **authentication** - the authentication type used
   - **pseudoDomain** - apiproxy
   - **address** - the address where the stream would be replicated to
   - **ewsPort** - the EWS port of the address
   - **userName** - the username of the address used in api proxy
   - **password** - the password of the address used in api proxy

In this configuration, all the server IPs listed *(192.168.2.3, 192.168.2.4)* will have the same pulled streams as the host EMS.

To verify, do `listconfig` in all destination IPs. All pulled streams from the host EMS should also be pulled by the destination servers.

------

## Notes

- You can use disabled and enabled configuration at the same time

- Make sure that the username and password is correct

- Do not forget to add "," at the end of "}" if you will add another set of value

- You can use v1.7.1 load balancer to v2.0.0 prior that the API Proxy for 2.0.0 is disabled

  ​



