---
title: Introduction to Word Templates in Dynamics GP
description: Learn how to customize your customer-facing documents with Word templates in Dynamics GP."
keywords: "Word Template"
author: theley502

ms.prod: dynamics-gp
ms.topic: article
ms.reviewer: jswymer
ms.author: nihell
ms.date: 05/05/2022

---

# Introduction to Word Templates in Dynamics GP

Would you like to update the look and feel of your customer facing documents from the drab report writer formats?

Would you also like to email those documents directly out of Dynamics GP?

The Word Template functionality in Microsoft Dynamics GP is pretty awesome and it will do all of this as well as allow you to have separate document types for different companies and customers.

There are a few tricks to setting up and getting things functioning. It’s important to perform these steps in order.

You also will be working with the Template Configuration and Template Maintenance in Dynamics GP.

## Install and Configure Word Templates

You must have two applications installed before beginning this process:  

* Microsoft Dynamics GP Add-On for Word
* Open XML SDK 2.0 for Microsoft Office

Open XML will be installed when you install Dynamics GP. The Dynamics GP Add-On for Word is located on the Dynamics DVD.

To use Microsoft Word with Dynamics GP, you must add the “Developer” tab to your ribbon bar. In Microsoft Word navigate to Options \| Customize Ribbon and select “Popular Commands.” Add the Developer function to the Ribbon list and then check the box. Click “OK.”

### Add-in for Microsoft Word
Install
1. Using the Microsoft Dynamics GP installation media. Double click the setup.exe file.
2. Under Additional Products click on Microsoft Dynamics GP Add-in for Microsoft Word, then Install.
3. Click the radio button _I accept the terms in the License Agreement_, click Next.
4. Select the install location for the Microsoft Dynamics GP Add-in for Microsoft Word, click Install.

    > [!NOTE]
    > The default location is C:\Program Files (x86)\ Microsoft Dynamics\ Report Templates\

5. Once the Microsoft Dynamics GP Add-in for Microsoft Word is installed, click Finish.
6. Open Microsoft Word, select the Developer Tab, verify that the Microsoft Dynamics GP Templates group shows.

#### Developer Tab missing?
If you are missing the Developer tab, right click in the black space within the ribbon > click "Customize the Ribbon"
In the Word Options window check the Developer box, click OK.

#### Helpful Microsoft Word settings
The following settings in Microsoft Word will help you see the layout structure of the Word Template and make editing them easier.
To open the Microsoft Word Options, click the File menu in Microsoft Word and select Options.
Check the following options under the Display category:

* Paragraph marks
* Hidden text
* Object anchors
Check the following options under the Advanced category:
* Show bookmarks
* Show text boundaries

## Overview of Word Templates
Added in Microsoft Dynanmics GP 2010

### Template-enabled reports
Administration >> Reports >> Template Maintenance >> choose the Report Name drop-down list and select More Reports.

Template-enabled reports are Report Writer reports that have a Microsoft Word Template document associated with them. When enabled the option to print becomes available in the Report Destination window.
![Form](media/enabledtemplates01.png)

### Report definition

Word Templates are based on the Standard report definition in Report Writer. Report definition is needed for:

* Defining which tables are used for the report.  
* Specifying how data is sorted.  
* Determining which section, the report has  
* Specifying which fields are in each section.  
* Defining calculated values that appear on the report.  

Microsoft Word does not perform these actions; it simply displays the report that has been rendered.  

### Word template document

The word template document defines the layout of a report.  

It contains the report definition details such as sections in the report, fields in each section, and any static text values defined for the report. This information is gathered from the report definition, and then embedded into the word template when created.

### How Word Templates are processed

When you choose Template as the Report Type, the assigned Microsoft Word document will be used to generate the output of the report.

1. The Microsoft Dynamics GP runtime uses the report definition within Microsoft Dynamics GP to generate an XML file that contains both the report definition and the data for the report.  
2. The assigned Word Template document is then retrieved.  
3. The XML and Word Template are passed to the Template Processing Engine, which combines them to produce the completed Microsoft Word Template for the report.  

## Report Template Design

### Document structure

The Word Template document is a standard Microsoft Word document.
When rendered from Microsoft Dynamics GP, the additional information from the report definition is embedded into the document.
Several tables in the word template document define the overall structure. All content that is displayed in the generated Microsoft Word document is placed inside these tables.  

> [!NOTE]
> Any text that is not within one of these tables will not be included in the generated word template.
 
### Page header table

* Placed in the Header section of the Microsoft Word document.
* Corresponds to the Page Header section on the standard Report Writer report.
* Content is displayed at the top of every page of the generated report.
* Examples: report date, current user, page number, logo.  

### Report header table

* Located at the beginning of the Microsoft Word document.  
* Corresponds to the Report Header section on the standard Report Writer report.  
* Content is displayed only one time at the beginning of the report.  
* Examples: Company information, customer/vendor information such as address  

### Body table

* Located after the Report Header table in the Microsoft Word document.  
* Corresponds to the Body content and any additional Headers and/or Footers.  
* Contains main content ‘guts’ of the report.  
* Has multiple rows.  
* One row for the actual report body, then an additional nested row for each additional header/footer.  

  (example: item description, line-item comments)

### Report footer table

* Located at the end of the Microsoft Word document.  
* Corresponds to the Report Footer section on the standard Report Writer report.  
* Content is displayed only one time at the end of the report.  
* Examples. Document totals, document comments, terms/conditions  

### Page footer table

* Located in the footer of the Microsoft Word document.  
* Corresponds to the page footer for the standard Report Writer report.  
* Content is displayed at the bottom of every page of the generated report.  
* Examples: report page number, business address, etc.  

### Fields, captions, and legends

The fields, captions, and legends are the specific data points that link the word template to the report definition.

#### How to remove a field, caption, or legend from a word template.

1.Click on the item within the word template document.
The tag containing the name of the report definition field will be displayed.
2.Click on the tag to select it.
3.Remove the item by pressing the Delete or Backspace buttons.

### Displaying item properties

The item properties will show what section of the report data the item originated from.
To display the Content Control Properties, select by clicking the item in the word template.
In the Developer tab, click Properties under the Controls group.

> [!NOTE]
> The tag field in the Content Control Properties window indicates which section of the report definition the value is from.

### Bookmarks

A bookmark identifies and labels a specific section or location within a document that can be used to identify for future reference.  

In Microsoft Dynamics GP there are 5 default bookmarks. These bookmarks are used in conjunction with the XML on the template to determine where on the Microsoft Word document your report information should be placed.

#### Viewing Bookmarks

First, you will want to make sure that Bookmarks are visible on the document you are viewing.  

1. In Microsoft Word, File menu, Advanced tab, Show document content section.  
2. Check the box next to option **Show bookmarks**.  

    Now that we know bookmarks icon is enabled and you can see them on the word template, you can use the following direction to see which bookmarks on your document.

    > [!TIP]
    > Bookmarks appear as a grey capital I or roman numeral 1.

3. Open the Microsoft Dynamics GP Word Template via directly opening the .docx file or clicking Modify in Template Maintenance on the specific Word Template.  

4. In Microsoft Word, click into any of the tables that contain data on the template, go to the Insert menu, Links section, select Bookmark.

Reference the following “map” of a report template document to see where the bookmarks are located.
 
> [!NOTE]
> StartTemplateDocumentBookmark and EndTemplateDocumentBookmark are used only for calculating page numbers for report template document. They do not identify tables in the report template document.
>
> To be found by the template processing engine in Microsoft Dynamics GP, these bookmarks must not be located within the fields, captions, or legends used for the report.
>
> Word Templates that are generated via the Word Template generator may not necessarily have all these bookmarks. This varies based on what is included on the Report Writer report xml file used when generating a template.

### Company Logo

Each company in Microsoft Dynamics GP can have an image assigned that is to be displayed on the Microsoft Word template reports.
Assigned in the Image Assignment window (Administration >> Reports >> Template Configuration >> Images).
Typically, this logo is placed in the Page Header table for the word template.  

#### To add a company image to the word template

1. Create a cell to contain the image.  

    In the word template, create a table call in the location where you want the image to appear.  
2. Add a Picture Content Control.  

    Display the Developer ribbon in Microsoft Word. In the Controls group, choose to insert a Picture Content Control.  
3. Set the picture size.  

    Use the resize handles on the Picture Content Control to the size required for the word template document.  
4. Set the picture properties.  

    With the Picture Content Control selected, click Properties in the Controls group. Set the following properties:  

    |Property  |Value  |
    |---------|---------|
    |Title     |CompanyLogo |
    |Tag|globals.’Company.Logo’ |

> [!NOTE]
> You can opt to not have a Content Control field for the company logo and have the image directly on the template.

## Template patterns

### Form Characteristics

* The Body table in the layout is a single cell.  
* The body table has another nested in that, which contains the rows and columns that define the layout of the data.  
* Captions and fields for the report are placed in the cells of the nested table.  
* The StartTemplateSectionRepeating bookmark is placed in a cell of the nested table to indicate that the entire single-cell row of the Body table will be repeated for each record in the report.  
* The Body table may have rows for additional headers/footers.  
* Report Footer and Page Footer tables are option in this pattern.  

### Column Characteristics

* First row of the Body table is divided into columns that contains the captions for the values in the report.  
* Body table can contain rows for additional header/footer data.  
* Body table has a row that contains a nested table. The nested table is divided into columns, and the fields for the report are placed in these columns.  
* StartTemplateSectionRepeating bookmark is placed in a cell of the nested table to indicate that the entire row of the Body table will be repeated for each record in the report.  
* Report Footer and Page Rooter tables are optional.  

### Read-Only

1.	Open Report Template Maintenance.
Administration >> Reports >> Template Maintenance
2.	Select the template.
In Report Template Maintenance, select the report template for which you want to make a rea-only version, click Modify.
3.	In Microsoft Word, in the Review tab, click Protect, then Restrict Editing.

4.	Save the changes made to the word template.
5.	Close the modified report.
6.	Import the modified word template document into GP.
In the Report Template Maintenance window select the template you would like to import. 
Click Add Template (green plus)
A file dialog box will appear.
Select the word template document that you had just saved.
7.	Replace the existing report template document. 
A message will be displayed that indicates you are replacing an existing template. Click Yes to replace the existing word template document with the one you have just modified.

## Creating Report Templates

1.	Open Report Template Maintenance. 
Administration >> Reports >> Template Maintenance
2.	Select the original version of the report. 
3.	Create a new report template document. 
4.	Specify the details of the new word template document.

    In the New Template window, specify how the new report template document will be created. 
    For reports that have no existing report template documents, the new report template will be blank (no layout).
    For reports that have existing report template documents, the new template can be created based on the template you select.
5.	Supply a name for the word template you are creating, click Create.
6.	Modify the new report template. 
7.	Save the new report template.

    > [!NOTE]
    > Always check the box to Maintain compatibility with previous versions of Word before saving. Only available the first time the document is saved. 
8.	Close the new report template.
9.	Import the new report template. 
10.	Replace the existing report template document. 

### Report Templates for Modified Reports

#### To create a modified report template document

1.	Open Report Template Maintenance. 
Administration >> Reports >> Template Maintenance
2.	Select the modified version of the report. 
3.	Create a new report template document. 
4.	Specify the details of the new word template document.
In the New Template window, specify how the new report template document will be created. 
For reports that have no existing report template documents, the new report template will be blank (no layout).
For reports that have existing report template documents, the new template can be created based on the template you select.
5.	Supply a name for the word template you are creating, click Create.
6.	Modify the new report template. 
7.	Display the field list for the report. 
8.	View the additional resources for the report. 
9.	Make modifications to the report template layout.
10.	Save the new report template.  

    > [!NOTE]
    > Always check the box to Maintain compatibility with previous versions of Word before saving. Only available the first time the document is saved. 
11.	Close the new report template.
12.	Import the new modified report template. 
13.	Replace the existing report template document.
 
#### To use the modified report template document

1.	Open Report Template Maintenance
2.	Select the modified version of the report.
3.	Assign the modified report template.
4.	Verify Security is to modified report.
Administration >> Setup >> System >> Alternate/Modified Forms and Reports 

> [!NOTE]
> The status field in Template Maintenance correlates to the version of the report selected in Alternate/Modified Forms and Reports.

#### To update the data source for a report template

1.	Update the modified report.
Update the Report Writer report in Report Writer.
2.	Run the report for which you made modifications to.
3.	Export the report in XML format.
In the Report Destination Window, export the report as a file in XML format, click OK. 
4.	Open the report template document.
This can be done via the clicking Modify in the Report Template Maintenance window (Administration >> Reports >> Template Maintenance) or opening the report template document .docx file directly.
5.	In the Developer pane, select Field List from Microsoft Dynamics GP Templates group. 
6.	Select the XML Resource containing the report definition in the Custom XML Mapping pane. 
7.	In the Developer pane, select Remove Source from the Microsoft Dynamics GP templates group. 
8.	Click OK to Removing a data source may cause missing data on the template. 
9.	In the Developer pane, select Add Source from the Microsoft Dynamics GP Templates group. 
10.	Locate the XML Document file saved in Step 3, click Open. 
11.	In the Custom XML Mapping pane, you should now see a new XML Resource listed.

    > [!NOTE]
    > The naming convention should be the same as before. 
12.	Modify the word template as needed and Save As.
13.	Re-Import the word template document into Microsoft Dynamics GP.

## Word Template Generator

The Microsoft Dynamics GP Word Template Generator is a utility that can be used to help create a Word Template for Microsoft Dynamics GP reports.  

### Install

1. Service Packs and Hotfixes for the Word Template Generator for Microsoft Dynamics GP | Microsoft Docs
2. In the Downloads section, select MDGP2013_WordTemplateGenerator_FullInstall_R2.zip 
3. Click the radio button I accept the terms in the License Agreement, click Next.  
4. Select the install location for the Microsoft Dynamics GP 2013 Word Template Generator Tool, click install  

    The default install location is C:\Program Files (x86)\Microsoft Dynamics\Template Generator\
5. Once the Word Template Generator Tool is installed click Finish
6. The following screen capture shows what the Template Generator tool looks once installed.

#### How to use?

1. Run the report for which you want to create a template.
2. Export the report in XML format.

    In the Report Destination Window, export the report as a file in XML format, click OK.
3. Drag-and-drop the XML file over the TemplateGenerator.exe file.
4. In the location where the XML file was originally saved, a DOCX file will be created with the same name.
5. Add the template into Microsoft Dynamics GP.
6. Test the template.
7. Revise the template as needed.

## Troubleshooting Word Templates

### Word add-in issues

* If you experience issues with the Word add-in, best to uninstall/reinstall.  
* Incorrect data in Word document  

  * Verify that the Report Writer report generates as expected first.  
  * Verify that bookmarks are present and in correct location.  
  * Verify that all sections are available via the Report Definition.  
* Template processing does not complete.  

  If you run a report, choose to generate the output in Microsoft Word format, but the processing never completes, try the following:  

  * Be sure that the SQL Server Browser service is running on the machine. This service is necessary for template processing to complete successfully.  
  * The Template Processing Engine may have encountered an error and be in an unknown condition. Restart Microsoft Dynamics GP so the Template Processing Engine is re-initialized.  
  * Remove any non-typical controls that may have been added to the template layout. For example, templates cannot be processed if they contain the “Rich Text Control” that can be added from the Developer ribbon.  
  * If a specific report is causing problems, try simplifying the report template document to isolate the problem. For example, if a modified report will not generate the output in Microsoft Word format, try running the original version of the report. If the original report can generate the output in Microsoft Word format, the issue can be isolated to changes you made in the modified report template document.  
  * Add the following settings to the Dex.ini file:  

    ```
    KeepTemplateFiles=TRUE 
    TPELogging=TRUE 
    ```

    When you add these settings, a log file that has a name beginning with TemplateProcessing, as well as the intermediate template documents are stored in the current user’s temporary folder. To access the temporary folder, type the following in the Run command:

    ```explorer %temp%```

    Sort the contents of the temporary folder by the modified date. Examine to files related to the report that will not process. They will contain information that can be helpful when troubleshooting.

    Press and hold the Alt key when moving table boarders to prevent them from snapping to the grid in Microsoft Word.

Use the Design Mode which can be activated from the Developer tab to see quickly which sections the items in the word template comes from.

Make regular backup of your word template as you are working, in case you make a change that you’d like to revert.

## Create and Assign Word Templates

First, you need to determine what report we’re basing our template on and whether it’s an original report or a modified report.

Why?

Word Templates are based on the standard report writer report. In order to create and assign a template the system needs to know the name of the report and also whether the report is already modified.

Tip: We recommend always basing the template on a modified version of the report for greater flexibility in the future.

Why?

Remember that the template uses Report Writer to access data. If we ever want to add a new calculated field, we need to create it first in Report Writer for it to be available in our template, thus it’s a modified report.

Reports \| Template Configuration

In Dynamics GP, the configuration window allows you to enable a specific form(s) to work as a template. Mark the document(s) for which you want to create a template. At the bottom of the window, be sure to mark the ‘Enable Report Templates’ and, if desired, to ‘Allow use of the Standard form’ even though you’re using the template.

## See also

[System Administration Guide](SystemAdminGuide.md)  
[Understanding the Lifecycle Policies for Dynamics GP](../terms/lifecycle.md)  
