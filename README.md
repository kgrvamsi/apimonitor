apimonitor
==========

API Monitor is a NRPE Plugin where it Monitors the api at regular intervals as per the requirement.

Steps in creation

1)Create Bash Script:

We have created a Bash Script called check_api where it checks the Api through wget using the Spider option and checking if the url is sending a 
202 or 404

2)Modify NRPE Configuration:

Now we have to modify the nrpe.cfg file and add a line saying that check_api will be part of the monitoring execution

We have to give the execute permissions so that the script gets executed with in the process flow

command[check_api]=/usr/lib/nagios/plugins/check_api

3)Add Nagios Service

we have to make sure that the nrpe check_command executes so that we can add the plugin as a service in the nagios.

we have to check whether the services.cfg is been added in the nagios.cfg

/usr/local/nagios/etc/nagios.cfg

cfg_file=/usr/local/nagios/etc/hosts.cfg
cfg_file=/usr/local/nagios/etc/hostgroups.cfg
cfg_file=/usr/local/nagios/etc/services.cfg

After that create a file /usr/local/nagios/etc/services.cfg and add these lines inside it.

define service {
  service_description check_api
  use generic-service
  host_name some-server
  check_command check_nrpe!check_api
  contact_groups contact-users
  }

4)Confirm & Verify Nagios Alerts

Now go inside that plugins folder and check whether the script is running fine or not by showing us the result.

[root@vamsi plugins]# ./check_nrpe  -c check_api



