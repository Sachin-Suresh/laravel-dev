# Commonly Used Libraries in Kstych Framework

<font color='#7540EE'>

1. [PHP Libraries in Kstych Framework](#profile-menu)
1. [JS Libraries in Kstych Framework](#admin-menu)

</font>
- - - -

## PHP Libraries in Kstych Framework

Kstych provides you with some of the most widely used PHP libraries. Let's take a look at some of the scenarios.

**Use Case 1:** To generate PDF from URLs, you can view the `KChromePDF.php` file from the `/home/Kstych/Framework/application/app/Kstych/Browser/` directory.

``` php
<style type="text/css" media="print">
@page {
    size: A4;
    margin: 0;
}
@media print {
    html, body {
        width: 1200px;
        height: 297mm;
    }
}
</style>

$p=new \App\Kstych\Browser\KChromePDF();
$pdf=$p->urlToPdf("https://google.com");

header("Content-type:application/pdf");
header("Content-Disposition:attachment;filename='downloaded.pdf'");
echo $pdf;
```

## JS Libraries in Kstych Framework

Following are some of the built-in JS libraries in Kstych.

1. THe following ajax function provides details of upload and download, like the amount of data uploaded, downloaded.

        kstych.ajax.do=function(varUrl,data,targetDiv,handleStr,ajaxType,ajaxtype,kcallback,kcallbackerr)

1. The Kstych application has a built-in error handler which can handle JS, PHP, or any *500* exception error, where an email with error log is automatically sent to the confirgured email addresses.

    You can configure the email address from the **Designer**->**Env** page; add the key `app_developer` which can take a comma seperated email addresses.

    <img src="../images/configure_email.png"/>

1. You can submit a form by div id using the following JS function:

        kstych.form.save=function(container,idsarr,url,type,retdiv,successurldiv,routestr,successcb)

    Similarly, you can set an attribute to a field and the field can be submitted using the below function:

        kstych.form.saveAttr=function(attr,url,type,retdiv,routestr,cb)

1. The following are the Kstych functions for handling notifications for success, failure, warnings, etc.

        kstych.notify.default=function(msg)
        {
            kstych.notify.notify("Notification",msg,{addclass:"bg-default",iconbar:"left"});
        }

        kstych.notify.error=function(msg)
        {
            kstych.notify.notify("Error",msg,{addclass:"bg-danger",iconbar:"left"});
        }

        kstych.notify.success=function(msg)
        {
            kstych.notify.notify("Success",msg,{addclass:"bg-success",iconbar:"left"});
        }

        kstych.notify.notice=function(msg)
        {
            kstych.notify.notify("Notice",msg,{addclass:"bg-info",iconbar:"left"});
        }

        kstych.notify.warning=function(msg)
        {
            kstych.notify.notify("Warning",msg,{addclass:"bg-warning",iconbar:"left"});
        }


