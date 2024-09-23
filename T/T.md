Provider
    Funds - MorningStar
    Fixed Income - Bloomberg
    Equity - Refinitiv


--------------------------
Consolidation:
    Checks the background rules for each field and consolidate the value.
    
Single conversion
    Via single conversion, the user can easily consolidate all data present in the system into one instrument.
    Therefore, the conversion of a genre covers the consolidation of every data record existing for that genre, e.g. master data record, conversion rates, general meetings, order-trade-clearing information etc.
     
    Important
    As a result, the processing time for a single conversion of a genre with many time limit or stock exchange data can be longer.
    The single conversion function allows the user to ensure that all current instrument data are stored in the CP and the end systems connected through segmentation.
    

    
-----------------------------
SOD Cockpit:
    Temenos DataSource offers an overview of the errors that occurred within a defined period in the various application areas 
    (consolidation, export, import, integration service, missing prices, price tolerance, unconfirmed MP records, VDPS XML import, vertical price export).
    This overview can be used within the Start of Day (SOD) as cockpit, so that the user knows which checks and possible adjustments should be performed. 

    The SOD cockpit overview is a "to do" screen, where users could check the individual items, correct them and set their status to completed. 
    
------------------------------
Rules:
    f- mapping with different tables
    h-hard code - constant value
    d-database query
    w-mapping with same tables
    r-rules using if block
    p-plugin
    b-boolean type
Sensitivity 
    Optionally indicates a sensitive field (i.e. a change of the field value during a consolidation will lead to a soft or hard error), along with its sensitivity. 
Plausibility 
    Optionally indicates the plausibility (field value validity check during a consolidation) that applies to the field. 
Both fields (Sensitivity and Plausibility) are only displayed if the field is a Consolidated Provider (CP) field. This information cannot be specified for fields of other providers. 

-------------------------------------
Export Definition:
    
    • "Consolidation" value = the export is started automatically after the field contents to be exported have been filled with data. 
    • "Scheduler" value = the export is performed on a timer via a cron job. 
    • "Manual" value = the export must be performed manually via the "Export // Call // Manually" menu item. 
    • "External" value = the export is started from a user's external system through relevant parameters that were passed on. 
----------------------------------------------------------------
Future Data:
    It will update the value for that particular field at the required time

-----------------------------------------------------------------
Jobs:
    It will run the particular job which is in job service.
    Like daily import and export data.
---------------------------------------------------------------------
CSV import configuration:
    Text quote(Mask) & Enclosing->
        a. Mask = \ 
Enclosing = no 
Import text: WKN2334;Header\;Text;12312,921; 
During the import, the following three columns/values will be read: 
1. WKN2334 
2. Header;Text 
3. 12312,921 
... since the second semicolon is interpreted as text and not as column separator due to the prefixed "\" character 
        b. Mask = " 
Enclosing = yes 
Import text:"WKN2334";"Header;Text";"12312,921"; 
In this example, the exact same three columns/values as before will be recognized. The second semicolon will be ignored as a control character, since it is placed within two double inverted commas. 
    Consolidation configuration : You may specify a consolidation configuration to be used during the consolidation of the change events generated via the CSV import 
    Instrument Pos: Here you can specify the position (column) in the CSV file to be imported, at which the standardized instrument definition can be found. The column count always starts from 0. Example: The securities number can be found in the first column, therefore the value 0 must be stored in the Instrument Pos field. 
    Log missing change events : If in course of the csv-import for a record a change event could not be created the record will also not be consolidated. A reason could be that the instrument is not marked as “active instrument” or the working area is not active. If the attribute “log missing change events” is set, a note is written in the import logging. 
Consider 4 eyes :This flag defines whether the activation of 4-eyes-principle according to system table TNT/5 should be considered. Hence it is possible to import records directly as “confirmed” (validated) even though such maintenance needs a validation as per TNT/5. 
Spool Change Events : If this attribute is activated the created change events from this import will not be consolidated. The created change events will be stored in PDB_CHANGE_EVENT with the flag “IMMEDIATE_CONSOLIDATION = -1”. Those will not be consolidated during a normal consolidation. The change events will be stored with a grouping id to consolidate them later together. 
Prevent storing NULLs : If this flag is set (default: it is not set) values which are NULL or contain an empty string will not be stored in the target provider. Therefore it is possible to prevent that an existing price will be overwritten with an empty price. Generally this will not happen as records with empty price fields are not part of the target file (exception: UBS_Mail!). 
    
------------------------------------------------------------------------
Context 	Color 
Four eyes principle 	yellow 
Obligatory field 	magenta 
Field search 	bright red 
MP-based CP fields 	light blue 
Historical field 	light green 
Context 	System variable key 	Default color value (RGB scheme) 
Four eyes principle 	FOUR_EYE_COLOR 	255,255,0 (yellow) 
Obligatory field 	MANDATORY_FIELD_COLOR 	255,0,255 (magenta) 
Field search 	SEARCH_RESULT_COLOR 	255,235,205 (bright red) 
MP-based CP fields 	MP_BASED_CP_FIELD_COLOR 	200,240,255 (light blue) 
Historical field 	HISTORIC_VALUE_COLOR 	200,255,220 (light green) 


-----------------------------------------------------------------------------------------------------------------------------------------Dynamic GUI's:
Panel Definition -> Create all panels for provider and consumer and also search.
GUI Definition-> Assign created panels whether its tabbed pane or search panel and also we can combine more than one panel.
GUI Assignments -> Here, we can assign which provider and working area for that GUI definitions.
GUI Rule -> Its for opening the records from the Data overview.


Enable 4-eye  validation:
1)Go to system table - TNT/5
2)Choose the table name which you want to enable
3)Change the reference 1 value -> 11 
4)clear cache



Create system properties for other environment:
    1. Create sql file.
    2. Add this query into the file
        a. insert into tnt_properties values('DELIVERY_UPDATE_EXPORT_RULES','true',1);
        b. commit;
    3. Pre installation.
        


Application Exception Properties file:
/apps/jboss/eap-7/standalone/tmp/vfs/temp/tempd7b53c11835dcf0a/content-b7d0709e785658c4/WEB-INF/classes/com/temenos/web/util/errors_en_US.properties

Add new rule errors:
    1. After adding errors then clear the caches



Edit which has customer BSP:
    1) Change the active customer to BSP.
    2) Clear cached
    3) Change as per ur requirement.
    4) Change back to SCB customer.
    5) Clear cache.

Auto TDS logg off:
    1. Edit this system variable
CLIENT_TIMEOUT_MINUTES

