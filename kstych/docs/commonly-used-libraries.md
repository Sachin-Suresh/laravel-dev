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

<font color='#7540EE'>
---Pending: To get other Use cases from Siddhart---
</font>