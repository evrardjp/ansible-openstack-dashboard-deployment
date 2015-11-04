openstack-dashboard-deployment
==============================

This role is used to deploy your new dashboards into your openstack environment

Requirements
------------

None, this is just a way to copy files into the correct folders.

Role Variables
--------------

The most important variable is openstack_dashboard_folder. It is the path where you'll have "enabled" and "dashboard" subfolders.
This points to the folders where the uploads will happen. The first derived variable is openstack_dashboard_enabled_folder (which is a subfolder of openstack_dashboard_folder).
The second derived variable is openstack_dashboard_dashboards_folder is the subfolder of openstack_dashboard_folder where all the dashbords are deployed.

Then dashboard_name is the name of the dashboard that will be used in openstack as installed app.
If you want to have multiple dashboards, create multiple role lines in your playbook.
This variable is mandatory. Running the playbook without it WILL FAIL.

Finally, openstack_dashboard_content_folder is the folder on the deployment host that holds all the files of the dashboard: the python logic, but also the css and js files for the views.
This variable is mandatory. Running the playbook without it WILL FAIL.
You should check on openstack documentation to know how to generate/write those files.
On devstack, I used the following commands:
  ``run_tests.sh -m startdash chargeback --target openstack_dashboard/dashboards/chargeback``
  ``run_tests.sh -m startpanel compute --dashboard=openstack_dashboard.dashboards.chargeback --target openstack_dashboard/dashboards/chargeback/compute``
Then I took all these files and uploaded them in my dashboard_content_folder.

If openstack_dashboard_use_custom_wiring_file is set to true, openstack_dashboard_use_custom_wiring_file_path will have to be set to a path to a file in the deployment host. This file will be used instead of the default template of this role.

Dependencies
------------

No other roles required.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: horizon_hosts
      roles:
         - { role: evrardjp.openstack-dashboard-deployment, openstack_dashboard_folder: "/usr/local/lib/python2.7/dist-packages/openstack_dashboard", dashboard_name: "chargeback", dashboard_content_folder: "/etc/openstack_deploy/files/dashboards/chargeback" }

License
-------

Apache2

Author Information
------------------

Jean-Philippe Evrard "<jean-philippe@evrard.me>"
