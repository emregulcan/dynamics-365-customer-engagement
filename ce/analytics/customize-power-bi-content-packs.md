---
title: "Customize Dynamics 365 Power BI content packs (Dynamics 365 Customer Engagement)| MicrosoftDocs"
ms.custom: ""
ms.date: 09/30/2017
ms.reviewer: ""
ms.service: "crm-online"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "Dynamics 365 (online)"
  - "Dynamics 365 Version 9.x"
ms.assetid: 424d7f29-de44-4ce0-94f1-be8777ad6485
caps.latest.revision: 16
author: "Mattp123"
ms.author: "matp"
manager: "amyla"
tags: 
 - "MigrationHO"
---
# Customize Dynamics 365 Power BI content packs

[!INCLUDE[cc-applies-to-update-9-0-0](../includes/cc_applies_to_update_9_0_0.md)]

[!INCLUDE[pn_microsoft_power_bi](../includes/pn-microsoft-power-bi.md)] is a comprehensive collection of services and  tools that you use to visualize your business data.  Content packs are available that make it easy to visualize and analyze the [!INCLUDE[pn_crm_shortest](../includes/pn-crm-shortest.md)] data with [!INCLUDE[pn_power_bi](../includes/pn-power-bi.md)] based on a standard data model. The content packs are built with a set of [!INCLUDE[pn_crm_shortest](../includes/pn-crm-shortest.md)] entities and fields that are useful for most sales, service, or marketing reporting scenarios.  
  
 Instances of [!INCLUDE[pn_crm_shortest](../includes/pn-crm-shortest.md)] are often extended with custom fields. These custom fields don’t automatically show up in the [!INCLUDE[pn_power_bi](../includes/pn-power-bi.md)] model. This topic describes the different ways that you can edit or extend the reports included in a content pack to include custom fields in the [!INCLUDE[pn_power_bi](../includes/pn-power-bi.md)] model.  
    
<a name="PBI_edit_first"></a>   
## Do this before you customize a Dynamics 365 content pack for Power BI reports  
 Before you customize a content pack, read  the information here and perform each task  as necessary.  
  
### Meet the requirements  
  
-   [Power BI service registration](http://powerbi.com/).  
  
-   [Power BI Desktop](https://powerbi.microsoft.com/desktop) application for editing [!INCLUDE[pn_power_bi](../includes/pn-power-bi.md)] reports.  
  
-   PBIX file for the content pack that you want to customize.  
  
    -   [Download the Dynamics CRM Online Sales Manager .PBIX](http://download.microsoft.com/download/9/2/B/92BCBDCE-CE01-4BC9-A306-2A92653B683E/Sales%20Manager.pbix)  
  
    -   [Download the Dynamics CRM Online Service Manager .PBIX](http://download.microsoft.com/download/9/2/B/92BCBDCE-CE01-4BC9-A306-2A92653B683E/Customer%20Service%20Manager.pbix)  
  
    -   [Download the Dynamics 365 Process Analyzer .PBIX](http://download.microsoft.com/download/9/2/B/92BCBDCE-CE01-4BC9-A306-2A92653B683E/Process%20Analyzer%20-1.34b.pbix)  
  
 [!INCLUDE[pn_crm_online_shortest](../includes/pn-crm-online-shortest.md)] content packs are currently only supported in the U.S. English language.  
  
### Prepare a content pack for customization  
  
> [!IMPORTANT]
>  To connect the OData feed to your [!INCLUDE[pn_crm_online_shortest](../includes/pn-crm-online-shortest.md)] instance you must follow the steps described here before you customize the content pack.  

> Currently, the [!INCLUDE[pn_power_bi](../includes/pn-power-bi.md)] service isn’t compatible with the [!INCLUDE[pn_crm_online_shortest](../includes/pn-crm-online-shortest.md)] version 9.0 OData endpoint. When you try to use the version 9.0 OData endpoint with the [!INCLUDE[pn_power_bi](../includes/pn-power-bi.md)] service the error message “The feed's metadata document appears to be invalid” is displayed. To work around this incompatibility, use the [!INCLUDE[pn_crm_online_shortest](../includes/pn-crm-online-shortest.md)] version 8.2 OData endpoint.For more information about the different endpoint versions, see [Web API URL and versions](../developer/webapi/compose-http-requests-handle-errors.md).
  
1.  Start [!INCLUDE[pn_power_bi_desktop](../includes/pn-power-bi-desktop.md)].  
  
     Click **File** > **Open**,  open a content pack, such as Sales Manager.bpix,  and then click **Open**.  
  
     Several pages of reports within the content pack are loaded and displayed in [!INCLUDE[pn_power_bi_desktop](../includes/pn-power-bi-desktop.md)].  
  
2.  On the [!INCLUDE[pn_power_bi_desktop](../includes/pn-power-bi-desktop.md)] ribbon, click **Edit Queries**.  
  
3.  In the left navigation pane of the Edit Queries window, under **Queries**, click the **CRMServiceUrl** query, and then on the ribbon, click **Advanced Editor**. In the source definition, replace **base.crm.dynamics.com** with your [!INCLUDE[pn_crm_online_shortest](../includes/pn-crm-online-shortest.md)] instance URL. For example, if the organization name is *Contoso*, the URL looks like this:  
  
     Source = "https://*contoso*.crm.dynamics.com/api/data/v8.0/"  
  
4.  Click **Done**, and then click **Close & Apply** in the Query Editor.  
  
5.  When the Access an OData feed dialog appears, click **Organizational account**, and then click **Sign-in**.  
  
 ![Access an OData Feed dialog](../analytics/media/pbi-odata-signin.PNG "Access an OData Feed dialog")  
  
6.  When the sign-in page appears, enter your credentials to authenticate to your [!INCLUDE[pn_crm_online_shortest](../includes/pn-crm-online-shortest.md)] instance.  
  
7.  In the Access an Odata feed dialog, click **Connect**.  
  
     The content pack queries are updated. This may take several minutes.  
  
<a name="PBI_edit_report"></a>   
## Customize a Dynamics 365 content pack  
 [Change the date format that is displayed in a report](#PBI_edit_date)  
  
 [Add a custom field to a report for any entity except Account](#PBI_edit_field)  
  
 [Add a custom field to a report for the Account entity](#PBI_field_Account)  
  
 [Add an option set field to a report](#PBI_optionset_field)  
  
 [Increase the number of rows queried](#BPI_increaserows)  
  
<a name="PBI_edit_date"></a>   
### Convert a DateTime field to a Date field for reporting  
 In [!INCLUDE[pn_dynamics_crm](../includes/pn-dynamics-crm.md)], some dates are saved in a Date/Time/Timezone format, which may not be the preferred format for aggregating data in  a report. You can convert the date displayed in reports for an entity field. For example, the Opportunity Created On field can be converted to a date to report the Opportunities created by day.  
  
1.  In Power BI Desktop, click **Edit Queries**.  
  
2.  In the left navigation pane of the Query Editor, under Queries, click the query that has the date field that you want to change, such the **Estimated Close Date** in the **Opportunity** entity query.  
  
3.  Right-click the column heading, such as *Estimated Close Date*, point to **Change Type**, and then select another date type, such as **Date**.  
  
 ![Change data type in Power BI Desktop](../analytics/media/pbi-changeformat.PNG "Change data type in Power BI Desktop")  
  
4.  Click **Close & Apply** to close the Query Editor.  
  
5.  On the main Power BI page, click **Apply Changes** to update the associated reports.  
  
<a name="PBI_edit_field"></a>   
### Add a custom field to a report  
 The following procedure describes how to add a custom field that is a date, string, or number to a report for all available entities except the Account entity.  
  
> [!NOTE]
>  To add a field to the Account entity, see [Add a custom field to a report for the Account entity](#PBI_field_Account). To add a field that is an option set type, see [Add an option set field to a report](#PBI_optionset_field).  
  
1.  In Power BI Desktop, click **Edit Queries**.  
  
2.  In the  left navigation pane of the Query Editor, under Queries, click the query that has the custom field that you want to make available for reports, such as the **Opportunity** entity query.  
  
3.  In the right pane, under APPLIED STEPS, click the settings button ![Settings button](../analytics/media/mp-ua-r16-settings.png "Settings button") next to **Removed Other Columns**.  
  
4.  The Choose Columns list shows all fields for the entity, including custom fields. Select the custom field that you want, and then click **OK**.  
  
     The entity query is updated and a column is added in the entity table for the custom field that you selected.  
  
5.  In the right pane, under APPLIED STEPS, click **Lang – Renamed Columns** and then click **Advanced Editor** to add the mapping for the field to the entity query. For example, if the custom field name for the Opportunity entity is *int_forecast* and the display name is *Forecast*, the entry should appear like this.  
  
    ```  
    {"int_forecast","Forecast"}  
    ```  
  
 ![Add mapping for a custom field on a report](../analytics/media/pbi-addfieldmapping.png "Add mapping for a custom field on a report")  
  
6.  After you add your field mapping, make sure there are no syntax errors displayed at the bottom of the Advanced Editor. Also, make sure the field name appears exactly as it appears in the column heading, including the correct letter case. If no syntax or table errors are detected, click **Done**.  
  
7.  Click **Close & Apply** in the Query Editor.  
  
     The custom field is now available in the right pane under **Fields** for the entity, and can be added to new or existing reports.  
  
<a name="PBI_field_Account"></a>   
## Add a custom field to a report for the Account entity  
 Because the Account query uses Fetch XML to filter the query, the steps to add a field are different than for other entity queries that use OData. To add a custom field to the OData queried  entities, see [Add a custom field to a report](#PBI_edit_field).  
  
1.  Copy the encoded Fetch XML query for the Account entity. To do this, follow these steps:  
  
    1.  In Power BI Desktop, click **Edit Queries**.  
  
    2.  In the  left navigation pane of the Query Editor, under Queries, click the **Account** entity query,  and then on the ribbon, click **Advanced Editor**.  
  
    3.  From the first line, beginning with %3Cfetch and ending with fetch%3E, copy the entire encoded Fetch XML.  
  
    4.  The encoded Fetch XML that you copy  should look similar to this:  
  
         %3Cfetch%20version%3D%221.0%22%20output-format%3D%22xml-platform%22%20mapping%3D%22logical%22%20distinct%3D%22true%22%3E%3Centity%20name%3D%22account%22%3E%3Cattribute%20name%3D%22territorycode%22%20%2F%3E%3Cattribute%20name%3D%22customersizecode%22%20%2F%3E%3Cattribute%20name%3D%22owningbusinessunit%22%20%2F%3E%3Cattribute%20name%3D%22ownerid%22%20%2F%3E%3Cattribute%20name%3D%22originatingleadid%22%20%2F%3E%3Cattribute%20name%3D%22revenue%22%20%2F%3E%3Cattribute%20name%3D%22sic%22%20%2F%3E%3Cattribute%20name%3D%22marketcap%22%20%2F%3E%20%3Cattribute%20name%3D%22parentaccountid%22%20%2F%3E%3Cattribute%20name%3D%22owninguser%22%20%2F%3E%3Cattribute%20name%3D%22accountcategorycode%22%20%2F%3E%3Cattribute%20name%3D%22marketcap_base%22%20%2F%3E%3Cattribute%20name%3D%22customertypecode%22%20%2F%3E%3Cattribute%20name%3D%22address1_postalcode%22%20%2F%3E%3Cattribute%20name%3D%22numberofemployees%22%20%2F%3E%3Cattribute%20name%3D%22accountratingcode%22%20%2F%3E%3Cattribute%20name%3D%22address1_longitude%22%20%2F%3E%3Cattribute%20name%3D%22revenue_base%22%20%2F%3E%3Cattribute%20name%3D%22createdon%22%20%2F%3E%3Cattribute%20name%3D%22name%22%20%2F%3E%3Cattribute%20name%3D%22address1_stateorprovince%22%20%2F%3E%3Cattribute%20name%3D%22territoryid%22%20%2F%3E%3Cattribute%20name%3D%22accountclassificationcode%22%20%2F%3E%3Cattribute%20name%3D%22businesstypecode%22%20%2F%3E%3Cattribute%20name%3D%22address1_country%22%20%2F%3E%3Cattribute%20name%3D%22accountid%22%20%2F%3E%3Cattribute%20name%3D%22address1_latitude%22%20%2F%3E%3Cattribute%20name%3D%22modifiedon%22%20%2F%3E%3Cattribute%20name%3D%22industrycode%22%20%2F%3E%3Clink-entity%20name%3D%22opportunity%22%20from%3D%22parentaccountid%22%20to%3D%22accountid%22%20alias%3D%22ab%22%3E%3Cfilter%20type%3D%22and%22%3E%3Ccondition%20attribute%3D%22opportunityid%22%20operator%3D%22not-null%22%20%2F%3E%3Ccondition%20attribute%3D%22modifiedon%22%20operator%3D%22last-x-days%22%20value%3D%22365%22%20%2F%3E%3C%2Ffilter%3E%3C%2Flink-entity%3E%3C%2Fentity%3E%3C%2Ffetch%3E  
  
2.  Decode the encoded Fetch XML. It must be valid encoded Fetch XML and, once encoded, should look similar to this:  
  
     \<fetch version="1.0" output-format="xml-platform" mapping="logical" distinct="true"> \<entity name="account"> \<attribute name="territorycode" /> \<attribute name="customersizecode" /> \<attribute name="owningbusinessunit" /> \<attribute name="ownerid" /> \<attribute name="originatingleadid" /> \<attribute name="revenue" /> \<attribute name="sic" /> \<attribute name="marketcap" />  \<attribute name="parentaccountid" /> \<attribute name="owninguser" /> \<attribute name="accountcategorycode" /> \<attribute name="marketcap_base" /> \<attribute name="customertypecode" /> \<attribute name="address1_postalcode" /> \<attribute name="numberofemployees" /> \<attribute name="accountratingcode" /> \<attribute name="address1_longitude" /> \<attribute name="revenue_base" /> \<attribute name="createdon" /> \<attribute name="name" /> \<attribute name="address1_stateorprovince" /> \<attribute name="territoryid" /> \<attribute name="accountclassificationcode" /> \<attribute name="businesstypecode" /> \<attribute name="address1_country" /> \<attribute name="accountid" /> \<attribute name="address1_latitude" /> \<attribute name="modifiedon" /> \<attribute name="industrycode" /> \<link-entity name="opportunity" from="parentaccountid" to="accountid" alias="ab"> \<filter type="and"> \<condition attribute="opportunityid" operator="not-null" /> \<condition attribute="modifiedon" operator="last-x-days" value="365" /> \</filter> \</link-entity> \</entity> \</fetch>  
  
    > [!TIP]
    >  Many URL encoder and decoder tools are freely available on the web.  
  
3.  In the Fetch XML, add your custom entity  as an attribute node between the \<entity> nodes. For example, to add a custom field named *customclassificationcode*, add the node after another attribute node, such as **industrycode**.  
  
    ```  
  
    <attribute name="industrycode" />  
    <attribute name=" customclassificationcode "/>  
    <link-entity name="opportunity" from="parentaccountid" to="accountid" alias="ab">  
    ```  
  
4.  URL encode the updated Fetch XML. The Fetch XML that includes the new custom attribute must be encoded and then used to replace the existing OData feed query that comes with the content pack. To do this, copy the updated FetchXML to the clipboard and paste it into a URL encoder.  
  
5.  Paste the encoded Fetch XML URL into the OData feed. To do this, paste the encoded URL between the quotation marks after the **Query=[fetchXml=** text, replacing the existing encoded FetchXML, and then click **Done**.  
  
     The screen shot below indicates where the left-most quotation is located.  
  
 ![Paste encoded URL into OData feed](../analytics/media/pbi-acct-encoded-url.PNG "Paste encoded URL into OData feed")  
  
6.  In the right pane, under APPLIED STEPS, click the settings button ![Settings button](../analytics/media/mp-ua-r16-settings.png "Settings button") next to **Removed Other Columns**.  
  
7.  The Choose Columns list shows all fields for the entity, including custom fields. Select the custom field, such as *customclassificationcode*, that you added to the Fetch XML query earlier, and then click **OK**.  
  
    > [!NOTE]
    >  The field name that you select in the Column Chooser and the field name that you add to the FetchXML query must match.  
  
     The entity query is updated and a column is added in the entity table for the custom field that you selected.  
  
8.  Click **Close & Apply** in the Query Editor.  
  
     The custom field is now available in the right pane under **Fields** for the entity and can be added to new or existing reports.  
  
<a name="PBI_optionset_field"></a>   
## Add a custom option set field to a report  
 Option set fields allow you to choose from multiple values. Examples of out-of-box option set fields are the Rating and Sales Stage fields for an opportunity. Imagine you have  a custom option set field on the main Opportunity form that has the following values and labels.  
  
 ![Custom option set example](../analytics/media/pbi-custom-option-set-example.PNG "Custom option set example")  
  
 To add the custom option set field to a report, follow these steps.  
  
1.  Add the custom field column.  
  
    -   In the left navigation pane of the Query Editor, under Queries, click the entity that has the associated custom option set, such as the Opportunity entity.  
  
    -   In the right pane, under APPLIED STEPS, click the settings button ![Settings button](../analytics/media/mp-ua-r16-settings.png "Settings button") next to **Removed Other Columns**.  
  
    -   The Choose Columns list shows all fields for the entity, including custom fields. Select the custom field, such as *new_customoptionset*, and then click **OK**.  
  
    -   Click **Save**, and then when prompted, click **Apply**.  
  
         The column for the custom field appears in the entity table.  
  
2.  Create the option set query.  
  
    1.  In Power BI Desktop, click **Edit Queries**.  
  
    2.  In the left navigation pane of the Query Editor. under Queries, click the query under the **Make Tables** group that has the option set field that is the most similar to the option set you want to add to a report. For this example, the **SalesStageOptionSet** query has four options so is a good choice.  
  
    3.  Click **Advanced Editor**.  
  
         The option set query is displayed.  
  
 ![Create an option set query](../analytics/media/pbi-makeoptionsetquery.png "Create an option set query")  
  
    4.  Copy the entire query to the clipboard. You can paste it in to a text editor, such as Notepad, for later reference.  
  
    5.  In the Query Editor, right-click the **Make Tables** group, click **New Query**, and then click **Blank Query**.  
  
    6.  In the right pane, under Name enter a name, such as *CustomOptionSet*, and then press Enter.  
  
    7.  Click **Advanced Editor**.  
  
    8.  In the Advanced Editor, paste in the query you copied earlier.  
  
    9. Replace the existing values and options with your custom values and options. In this example, you change this.  
  
        ```  
        let  
            Source = #table({"Value","Option"},{{0,"Qualify"},{1,"Develop"},{2,"Propose"},{3,"Close"}})  
        in  
            Source  
  
        ```  
  
         To this.  
  
        ```  
        let  
            Source = #table({"Value","Option"},{{0,"A"},{1,"B"},{2,"C"},{3,"D"},{4,"E"}})  
        in  
            Source  
  
        ```  
  
    10. Make sure there are no syntax errors, and then click **Done** to close the Advanced Editor. The table of values and options appears in the Query Editor.  
  
 ![New option set query](../analytics/media/pbi-optionsetquerycreated.png "New option set query")  
  
    11. Click **Save**, and then when prompted, click **Apply**.  
  
3.  Insert a merge query for the entity and custom option set tables.  
  
    1.  In the left pane of the Query Editor, under Entities, click the entity that includes the custom option set. For this example, the **Opportunity** entity query is selected.  
  
    2.  On the Ribbon click **Merge Queries** and, when you are prompted to insert a step, click **Insert**.  
  
    3.  In the Merge dialog, click the column heading for the custom option set, such as *new_optionset*. In the drop-down list, select the corresponding option set  query that you created earlier.  When the option set table appears, click the **Value** column heading to select it.  
  
 ![Merge table selections](../analytics/media/pbi-merge-tables.png "Merge table selections")  
  
    4.  Leave the join kind as **Left Outer (all from first, matching from second)**, and then click **OK**.  
  
        > [!TIP]
        >  Rename the merge query. Under APPLIED STEPS, right-click the merge query that you created,  click **Rename**, and enter a descriptive name, such as *Merge CustomOptionSet*.  
  
4.  Define the column so that only the labels display.  
  
    1.  In the left pane of the Query Editor, under Entities, click the entity that includes the custom option set. For this example, the **Opportunity** entity query is selected.  
  
    2.  In the right pane, under APPLIED STEPS, click one of the expanded queries to reveal the merged columns, such as **Expanded SalesStage**.  
  
    3.  Locate and click the column heading for the new column that was created as part of the earlier merge query step.  
  
    4.  On the Transform tab, click **Expand**.  
  
    5.  In the Expand new column dialog, clear the column that corresponds to the values (because only the labels should appear in the column). Click **Done**.  
  
 ![Choose the column that represents the label](../analytics/media/pbi-expand-column.png "Choose the column that represents the label")  
  
    6.  Click **Save**, and then when prompted, click **Apply**.  
  
5.  Change the column name for report building.  
  
    1.  In the left pane of the Query Editor, under Entities, click the entity that includes the custom option set. For this example, the **Opportunity** entity query is selected.  
  
    2.  Click **Advanced Editor**.  
  
    3.  Add a renamed column line item, make sure there are no syntax errors, and then click **Done**. In this example, the custom option set column name that you created earlier is **NewColumn** that is being renamed to *Custom Option Set*.  
  
 ![Rename a column to display in reports](../analytics/media/pbi-rename-column.png "Rename a column to display in reports")  
  
    4.  Click **Save**, and then when prompted, click **Apply**.  
  
6.  Click **Close & Apply** to close the Query Editor.  
  
     The custom option set can now be used to build [!INCLUDE[pn_power_bi](../includes/pn-power-bi.md)] reports.  
  
<a name="BPI_increaserows"></a>   
## Increase the number of rows queried  
 By default, all [!INCLUDE[pn_power_bi](../includes/pn-power-bi.md)] entity queries in the [!INCLUDE[pn_dynamics_crm](../includes/pn-dynamics-crm.md)] content packs cannot exceed 100,000 rows. To increase the number of rows that can be queried, follow these steps.  
  
> [!IMPORTANT]
>  Increasing the row count limit can significantly impact the time it takes for a report to refresh. Additionally, the [!INCLUDE[pn_power_bi](../includes/pn-power-bi.md)] service has a 30-minute limit for running queries. Use caution when increasing the row count limit.  
  
1.  In [!INCLUDE[pn_power_bi_desktop](../includes/pn-power-bi-desktop.md)], click **Edit Queries**.  
  
2.  In the  left navigation pane of the Query Editor, under Queries, click the entity query that you want to increase the  row count limit, such as the **Lead** entity.  
  
3.  In the right pane, under APPLIED STEPS, click **Kept First Rows**.  
  
4.  Increase the filtered row number. For example to increase to 150,000, change Table.FirstN(#"Filtered Rows",100001) to Table.FirstN(#"Filtered Rows",150000)  
  
5.  In the right pane, under APPLIED STEPS, click **Check Row Count**.  
  
6.  Locate the **>100,000** part of the step.  
  
 ![Increase row count value](../analytics/media/pbi-increaserowcount.png "Increase row count value")  
  
7.  Increase the value to a larger number, such as *150,000*.  
  
8.  Click **Close & Apply** in the Query Editor.  
  
<a name="BPI_publish"></a>   
## Publish your report to the Power BI service  
 Publish your report for organizational sharing and access from anywhere on most any device.  
  
1.  On the [!INCLUDE[pn_power_bi_desktop](../includes/pn-power-bi-desktop.md)] main page **Home** tab ribbon, click **Publish**.  
  
2.  If you are prompted to sign in to the Power BI service, click Sign in.  
  
3.  If multiple destinations are available, select the one you want, and then click **Publish**.  
  
### See also  
 [Use Power BI with Dynamics 365](../admin/use-power-bi.md)
