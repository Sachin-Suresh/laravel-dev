# Menus in the Kstych Application

The Kstych application has different menus within the Admin dashboard.
<font color='#7540EE'>

1. [Admin Menu](#admin-menu)
1. [Designer Menu](#designer-menu)
1. [Help Menu](#help-menu)
1. [About Menu](#about-menu)

</font>
- - - -

## Admin Menu

In this menu, you can create users, roles, access controls, and other general administrative activities. To access the Admin dashboard, click the **Admin** menu on the top-right and then click **Admin**.

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
- **UIMode**: *windows* or *default*. If the *windows* option is selected, which is a default option, all screens, if opened within the application are independent (separate draggable screens). If the *default* option is selected, the screen gets maximized.
- **Wallpaper**: *No* or *Role*. You can have a common wallpaper for all users or a role/user-specific wallpaper.

    <img src="../markups/role-wallpaper.svg">

- **Modules**: As an admin, you can add/remove modules that a particular user can have. In the example below, the admin role has access to the following modules:

    <img src="../images/admin_role_modules.png" width="450" height="200"/>


<font color='#7540EE'>
### 3. **Group module**
</font>

Suppose you want to isolate clients' data in a multi-tenant environment, then you can use the *Groups* module. A group can be assigned while you are assigning a role to a user. Currently, the system has a **Default** group.

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

You can use the ACL module to limit the access of a user/role to only a few models/columns in a table. You can restrict a user to view only specific models.


<font color='#7540EE'>
### 5. **Sequences module**
</font>

A sequence is a set of integers/numeric values that are generated in ascending or descending order at defined intervals. To ensure that each row in your table contains a unique value, the Sequence module is used.

<img src="../images/sequences.png"/>

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
### 7. **Access Logs**
</font>

Displays the different user actions by average time. For example, the below graph displays what routes are accessed within the application and its average time of usage.

<img src="../images/access_logs.png"/>

The table below displays requests information on the different actions performed by different users, the status code of the action, HTTP method, its URL, etc.

For debugging purposes, you can click the access log ID in the table to get more details of events that are triggered for that request cycle and the time taken for that action to complete in milliseconds. You can also expand the events to see what queries are executed.

<img src="../images/access_log_table.png"/>

<font color='#7540EE'>
### 8. **Mail Logs**
</font>

If the application sends any mails, then all the mail logs are displayed here.

<img src="../images/mail_logs.png"/>

<font color='#7540EE'>
### 9. **Form Logs**
</font>

Form logs display any logs whenever there is a change in any columns of your models. The table below displays the logs for different models, model ID, and the user who modified the model.

<img src="../images/form_logs.png"/>

<font color='#7540EE'>
### 10. **File Logs**
</font>

The logs of any files that you upload to the application are stored in the File Logs module. The table below displays the file logs, source of the file, MIME type, etc.

<img src="../images/file_logs.png"/>


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
### 13. **Workflow Logs**
</font>

<img src="../images/workflow_logs.png"/>

## Designer Menu

In the *Designer* menu, you can create **Modules** and **Models** for your application.

<img src="../images/designer_modules.png" width="150" height="200"/>

Let's see how you can create them.

### Creating a Module

<img src="../markups/module-creation.svg">
The following are the fields used while you are creating your Module.

- **Module Name:** The name of your Module (e.g., BlogPost)
- **Display Name:** (optional) A brief one-line description for your Module.
- **Module Icon:** The class name of the Font Awesome icon.
- **Route Hash:** Generated automatically by the application when you type the Module name.
- **Access User:** Access that you want to specify for a Module—**Auth** or **Guest**.

To create a new Module:

1. Enter the name of the Module in the **Module Name** field.
1. (Optional) Enter the Display Name for the Module.
1. Create *Models* if you have not created one. See [Creating Models](/Kstych-menus/#creating-models).
1. Click **Save Settings**.

<img src="../images/create-module.png"/>

#### Creating Models

For demonstration, let's create a Model named *Blog* as shown below and click **Save Settings**.

<img src="../images/create-models.png"/>

### Editing a Module

To edit a Module, you must have first created a Module.

To edit a Module:

- Go to the **Designer**-> **Module**.
- Select the Module that you want to edit from the **Modules** drop-down.

    <img src="../images/edit-module.png"/>

#### Editing and Defining Models

**Prerequisite**:

You must have a Model created. See [Creating Models](/Kstych-menus/#creating-models).

To edit and define the Model:

1. Go to the **Designer**-> **Models**.
1. Select the Module and Models that you want to edit from the respective drop-down.
1. You can now modify the table name, columns, etc.

    <img src="../images/edit-models.png"/>


Following are the columns from the below *Schema* table:

1. **SchemaKey**: Name of the column
1. **Type**: Database Type
1. **UIType**: The type displayed by the system
1. **Display**: Label name of the column
1. **Validation**: <a href="https://laravel.com/docs/8.x/validation#available-validation-rules" target="_blank">Laravel validation</a>
1. **Modifier**: If you need to use *unique* index or *foreign* index.
1. **Storage**: Columns managed by the system.

<img src="../images/def_column_names.png" />

All Models by default have the below six columns predefined by the system.

- **id**: Automatically generated by the system
- **created_at**: Created Date
- **updated_at**: Updated Date
- **deleted_at**: Used for soft delete
- **data**: Used to handle JSON columns
- **igroup_id**: To manage multi-tenant IDs

**Relationships**:

<img src="../images/relationships.png" />


See <a href="https://laravel.com/docs/8.x/eloquent-relationships" target="_blank">Laravel relationships</a> for more information.



### Adding Menus to Your Application

In this section, you can add menus to your application. To add a new menu to your application:

1. Enter the name of the new menu in the text field and select the type of the menu (e.g., **Vertical**) from the drop-down.

    - **Vertical:** Aligns the menu vertically.
    - **Horizontal:** Aligns the menu horizontally.
    - **RightIcon:** Example: The chat icon on the top-right of the application.

        <img src="../images/menu-topright.png" width="350" height="200"/>

    - **TopQuick:** Example: The bell and task list icons on the top-left of the application.

        <img src="../images/menu-topquick.png" width="350" height="200"/>

1. Click **Save Menus**.

    <img src="../images/menu-1.png"/>

1. In the *Modules Section Key* field, enter the module key (e.g., New Menu).

1. Select the modules from the drop-down where this new menu should be displayed.

1. click **Save Menus**.

    <img src="../images/menu-2.png"/>

1. Reload the page/application, you should now see the new vertical menu created.

    <img src="../images/menu-3.png" width="350" height="200"/>

Similarly, you can add a new **Horizontal**, **RightIcon**, **TopQuick** style menus. An example of the **Horizontal** menu is shown below:

   <img src="../images/menu-4.png" />

### Commands

You can activate or stop different console commands-CRON, Daemon, or Manual and add parameters to those commands. You can also verify the active status of the system commands.

<img src="../images/commands.png" />


### Environment Configuration

You can use this section if you want to composer install any packages that have dependencies in your application or if you want to install any package that is not already installed. To install any package(s), you can provide an `app_require` key followed by the package name and its version, as shown in the below format:

    app_require="nesbot/carbon": "^1.39|^2.0"

For more information, refer Laravel documentation on <a href="https://laravel.com/docs/8.x/configuration#environment-configuration" target="_blank">Environment Configuration</a>

### Workflows

Workflows are sequence of steps that is executed by the system. These steps can then be designed later by the end-users without having to know much of the application code.

For example, in an Employee Onboarding application, the major process handled by the HR involve paperwork preparation, orientation stage, integration, engagement, etc. These sequence of steps can be designed in this Workflow module.

To add a new Workflow for your application:

1. Go to **Admin**->**Designer**->**Workflows**.
1. Click **Add New**.

    <img src="../images/add_workflow.png" />

    <img src="../images/new_workflow.png" />

1. In the first column, provide the workflow details like name of your workflow, its version, whether you want to activate or disable the workflow, etc.

    <img src="../images/workflow_col1.png"  width="350"/>

1. In the second column, you can link the workflow to a specific Module, Model. The **Type** drop-down consists of events (manual and automatic) that defines how or when you want the workflow to be triggered.

    <img src="../images/workflow_col2.png" width="350"/>

    For example, *Ext.Get*, *Ext.Post* are events that needs to be manually provided a value. Similarly, *Cron.At* requires a cron sequence value for the workflow to trigger; which is to be provided in the **Value** field.

1. In the third column, in the **Multiple** field, you can configure a single workflow to run in multiples (e.g., setting **Multiple** field to '0' means you can run that workflow "unlimited" number of times).

    **ExpireMin** field: The expiry time if your workflow does not complete in specific time.

    **Log** field: If set to **Yes**, it saves the Workflow log–completed or failed. Workflow logs can be access from <a href="/kstych-menus/#13-workflow-logs" target="_blank">here</a>.

    **Custom** field: Accepts full class path including namespace. It is used if you want to trigger a class before your workflow triggers.

    <img src="../images/workflow_col3.png" width="350"/>

    Some example of Workflows can be seen below:

    **Example 1: Work permit application**

    <img src="../images/workflow_example_workpermit.png"/>

    **Example 2: Salary deduction approval**

    <img src="../images/workflow_salary_ded_approval.png"/>





### Custom

Displays the directory structure. Provides a way to access your files and directories easily from within the application.

<img src="../images/custom_dir.png" width="550"/>

### Tinker

Tinker is a command-line interface that allows you to interact with your entire Kstych application through a console window without the need of accessing the web interface. Some of the major benefits of using tinker are you can test relationships, debug data, and access Eloquent ORM, jobs, tests, events, etc.

### Creating Custom Help

In this section, you can create custom self-help documentation specific to your application. This helps your customers understand the modules that you have developed and let them know how to use them. To create custom help documentation:

1. Go to **Designer**->**Help** menu.
1. Select the `index` option from the **List** drop-down.
1. Create the structure for the help documentation (for example, for a *BlogPost* module) as shown below as in the `.ini` format.
1. Click **Save Help**.

You can see the documentation you created for the *BlogPost* Module from the **Help** menu as shown in the below screenshot:

<img src="../images/help-1.png"/>


## Help Menu

The contents that you added from the [**Help** menu](/kstych-menus/#creating-custom-help) will be displayed on the left pane.


## About Menu

The license information about the Kstych application is displayed.

<img src="../images/about.png"/>
