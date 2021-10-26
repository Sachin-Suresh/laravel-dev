# Menus in the Ksytych Application

The Ksytych application has different menus within the Admin dashboard.
<font color='#7540EE'>

1. [Profile Menu](#profile-menu)
1. [Admin Menu](#admin-menu)
1. [Designer Menu](#designer-menu)
1. [Help Menu](#help-menu)
1. [About Menu](#about-menu)

</font>
- - - -

## Profile Menu



## Admin Menu

In this menu, you can create users, roles, access controls, and other general administrative activities. To access the Admin dashboard, click **Admin** menu on the top-right and then click **Admin**.

<img src="../images/admin-menu.png" width="150" height="200"/>

Let's take a look at each of the modules in detail.

<font color='#7540EE'>
### 1. **User module**
</font>

You can use the User module to add a new user, assign a role to that user.

- To add a new user, go to the **Admin** -> **User** menu, click **Add New** and enter the user details like User Name, Password, FullName, Email, and click **Save User**.

    <img src="../images/user_module.png"/>

- To assign a role to this user, go to the **Admin** -> **User** menu, double-click the user that you want to assign the role to.

- Under the **Roles** field, click **Create New** and select the User and Role, and then click **Save UserRole**.

    <img src="../images/user_module-role-assign.png" width="350" height="200"/>

- To verify the new user, log out of the current `admin` user and log in with the new user.

**What to do if I accidentally deleted the default **admin** account?**

You can restore the **admin** account from the below code. Copy the below code to any Route or View that does not require any Admin role and then run the below code.

```php
$RM = kmodel('RoleModule');
$rm = $RM::withTrashed()->where('role_id','=',2)->where('acl','=','Admin')->where('igroup_id','=',1)->where('module','=','Admin')->first();
if($rm)
{
    $rm->restore();
}
else
{
    $rm=new $RM();
    $rm->role_id=2;
    $rm->acl='Admin';
    $rm->igroup_id=1,
    $rm->module='Admin';
    $rm->save();
}
```

<font color='#7540EE'>
### 2. **Role module**
</font>
You can create any number of roles and assign them to any number of users. This application has by default two roles—**Admin** and **User**. As an admin user, you can modify the roles for the following:

- **Status**: *Active* (default) or *disabled*. When a new user is created, by default that user is not given the Admin role.
- **Default**: *Yes* or *No* (default).
- **ShowMenu**: Displays the top menu if *Yes* is selected which is default or hides the top menu if *No* is selected.
- **UIMode**: *windows* or *default*. If the *windows* option is selected, which is a default option, all screens, if opened within the application are independent (seperate dragable screens). If the *default* option is selected, screens gets maximized.
- **Wallpaper**: *No* or *Role*. You can have a common wallpaper for all users or a role/user specific wallpaper.

    <img src="../markups/role-wallpaper.svg">

- **Modules**: As an admin, you can add/remove modules that a particular user can have. In the example below, the admin role has access to the following modules:

    <img src="../images/admin_role_modules.png" width="450" height="200"/>


<font color='#7540EE'>
### 3. **Group module**
</font>

Suppose you want to isolate clients data in a multi-tenant environment, then you can use *Groups* module. A group can be assigned while you are assigning a role to a user. Currently, the system has **Default** group.

To create a new group:

1. Go to the **Admin** -> **Group** menu.
1. Click **Add New**.
1. Enter the group details and click **Save Group**.

<img src="../images/add_groups.png"/>

You can also add multiple groups to a role.

1. Go to the **Admin** -> **Role** menu.
1. Select the role that you want to assign the group to.
1. Click **Create New** to assign a new group(s) to this role.

<img src="../images/assign_groups.png" width="450" height="200"/>

<font color='#7540EE'>
### 4. **ACL module**
</font>

You can use the ACL module to limit the access of a user/role to only a few models/columns in a table. You can restrict a user to view only specfic models.

<font color='#7540EE'>
---Pending: Require ACL table format from Siddhart---
</font>


<font color='#7540EE'>
### 5. **Sequences module**
</font>

A sequence is a set of integers/numeric values that are generated in ascending or decending order at defined intervals. To ensure that each row in your table contains a unique value, the Sequence module is used.

To understand more about sequences, refer the <a href="https://laravel.com/docs/8.x/database-testing#sequences" target="_blank">Laravel's Sequences</a> documentation.

<font color='#7540EE'>
### 6. **KSettings**
</font>

If you do not want to hard code/display any confidential data (e.g. API keys) in your application, then you can configure them in the JSON using the KSettings module.

To add a new configuration:

1. Go to the **Admin** -> **KSettings** menu.
1. Click **Add New**.
1. Enter the JSON data and the name of the configuration.
1. Click **Save KSetting**.

<img src="../images/Ksetting.png"/>

<font color='#7540EE'>
---Pending: To get sample json values from Siddhart---
</font>


<font color='#7540EE'>
### 7. **Access Logs**
</font>

Displays the different user actions by average time. For example, the below graph displays what routes are accessed within the application and its average time of usage.

<img src="../images/access_logs.png"/>

The table below displays request information on the different actions peformed by different users, the status code of the action, HTTP method, its URL, etc.

For debugging purpose, you can click the access log ID in the table to get more details of events that are triggered for that request cycle and the time taken for that action to complete in milliseconds. You can also expand the events to see what queries are executed.

<img src="../images/access_log_table.png"/>

<font color='#7540EE'>
### 8. **Mail Logs**
</font>

If the application sends any mails, then all the mail logs are displayed here.

<img src="../images/mail_logs.png"/>

<font color='#7540EE'>
---Pending: To get sample mail logs from Siddhart---
</font>

<font color='#7540EE'>
### 9. **Form Logs**
</font>

Form logs displays any logs whenever there is a change in any columns of your models. The table below displays the logs for different models, model ID, and the user who modified the model.

<img src="../images/form_logs.png"/>

<font color='#7540EE'>
### 10. **File Logs**
</font>

The logs of any files that you upload to the application is stored in the File Logs module. The table below displays the file logs, source of the file, MIME type etc.

<img src="../images/file_logs.png"/>

<font color='#7540EE'>
---Pending: To get sample file logs from Siddhart---
</font>


<font color='#7540EE'>
### 11. **Call Logs**
</font>

Any calls made from within the application is logged in the Call logs

<img src="../images/call_logs.png"/>

<font color='#7540EE'>
### 12. **User Logs**
</font>

Displays the list of users who logged in/logged out from the application.

<img src="../images/user_logs.png"/>

<font color='#7540EE'>
---Pending: To get sample users logs from Siddhart---
</font>


<font color='#7540EE'>
### 13. **Workflow Logs**
</font>

<font color='#7540EE'>
---Pending: To discuss with Siddhart---
</font>

## Designer Menu



## Help Menu



## About Menu