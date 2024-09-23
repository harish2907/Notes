Map Designer File Name Extensions.....
The following is a list of the file name extensions used in the Map Designer: Extension File type description.
bak Map source backup
.fnl Master work file
.Ixx Input work
.log Audit log
.mopt Map source options file
.mmc Compiled map
.mme Map build analysis result
.mms Map source
.mtr Trace
.omm Backup of a 1.4.x map source
.Oxx Output work
.tmp Temporary map work files
Note: Zero-byte temporary map work files might not be deleted if the Map Designer application is not gracefully disconnected.


Settings:
For Trace log -> Turn on all in Map Settings -> Map Trace
For Checking input and output file -> "Spectacle button"



                                                                                 INPUT TYPE TREE

Properties of Item(fields):
    1) Item subclass -> 
        a. define data type and lengths.
        b. Padding
        c. Restrictions -> Rule
Properties of Category:
    1) If you want to group all the number fields or character(String) fields, then use category and include all the fields in that category.
Properties of Group(Record):
    1) Format ->
        a. Implicit - based on each character count, it moved to next column.
        b. Explicit - It will split column by delimiter
            i. Component Syntax - Delimited
                1) Chose the delimiter value like "| , : "
    2) Type Syntax ->
        a. Initiator -> Start of the record
        b. Terminator -> End of the record{ ex: cr,lf}
        c. Literal: known value
        d. Variable: one of a set of values defined in type tree item
        e. Delimiter location
        Prefix delimiter appears before each object (^A^B^C)
        Infix delimiter appears between objects (A^B^C)
        Postfix delimiter appears after each object (A^B^C^)
    Release Character Properties....
        Indicates characters that follow should be interpreted as data, not as another syntax property.
        Example:
        Release character = Ampersand (&) Delimiter = Comma (,)
        Miller&, MD,Harkin Hospital,1996
        Data of component 1 = Miller, MD
        Data of component 2 = Harkin Hospital
        Data of component 3 = 1996
        
        
        
    3) Once everything done
        a. Arrange the field as per our order in "component tab"
        b. Set whether it is mandatory or not for that we need to "set range".
            i. Right click -> set range in "component tab"
            ii. If 1:1 -> mandatory,0:1 -> optional,
        c. Then create one more "group" for accepting multiple records like "File".
            i. It should always implicit mode.
            ii. Now drag and drop the "Record" into the "File" component tab
            iii. Set the Range for file Which tells how much records should be in file.
                1) 1:s -> infinity -> it will hold how much record in that file.
        d. Analyze the structure which u created.
            i. In menu -> Tree-> Analyze -> 

Mapping .mms file

Go to outline
    1) Create new map under .mms file
    2) Skyblue color -> its an function or some other but not an executable one. 
        a. To make an executable - fill the file path in the input and output cards 
    
MMC Configuration:

STP vs non-STP (TDS definition)
- in TDS, STP refers to listed security, fixed income, funds
- non-STP refers to DP/PE, generic template, specific template
 
TDS-TAP messages
- issuer message - 1 message
- 2 instrument messages for STP (listed securities, fixed income, and funds) - core and custom
- 1 instrument message for non-STP (generic template, specific template, DP/PE) - custom
- 1 instrument message for index - core
 
TDS-TAP instrument message
- 2 types of messages - core and custom
- core message - generated for listed securities, fixed income, funds, index. contains instrument information.
- custom message - generates distribution, compo, corporate action info for listed securities, fixed income, and funds
    - generates instrument + distribution info for generic template, specific template, dp/pe
 
Core message
- generally split into 2 parts
- tap-fipms-* -> core maps containing TAP core fields. if any change is needed in here, it has to raised through PACS. used maps are tap-fipms-bond, conv-bond, fundshare, stock, index.
- core maps call the custom maps containing instrument UDF mappings. tap-*-udf. these can be modified in the project and this where you will add any new instrument UDFs to be generated in the TDS core XML.
- if the UDF is applicable for stock, then add it only to stock-udf. if applicable for bond, then add to bond-udf and conv-bond-udf.
- core message is consumed/processed by the TAP GWP core maps. in order to instruct GWP to process the new UDFs, you'll need to add the UDFs into the gwp/config/UDF_Attfile.att, depending on which instrument type. restart gwp after updating the file.
- after making changes to the mmc, jboss needs to be restarted for changes to take effect.
 
Custom message
- tap-scb-custom -> main map containing the corporate action, compo, rating attributions, notepads, ptcc issuer etc for STP instruments. contains chronos, compos, synonyms for non-STP instruments.
- 2 main sections - one for STP and one for non-STP. STP section is only generated if the instrument is an STP instrument in TDS. non-STP section is only generated if the instrument is a non-STP instrument in TDS.
- STP and non-STP segments will call another message mapping fragment for the business entity entries
    - STP segment will call tap-cust-stp-dist
    - non-STP segment will call tap-cust-nonstp-dist
- unlike core UDF maps where adding a new UDF only requires copying the "add" structure, adding a new field into the custom message requires modification of the XSD - schema that defines the structure of the TDS XML
    - this can be found in export -> integration framework -> generic adapter releases. select the TAP entry, select the tds-tap entry, you will find the TdsTAPMessage.xsd
    - if there is any new UDF to be added, this has to be added to the corresponding section where the UDF has to be created. for example, if a new distribution field is to be added, you'll need to add a new element into ScbDistributionDetails-L1. 
    - after modifying the XSD, upload the new XSD to TDS. highly suggest to keep a backup of the previous version/working XSD in case the modified XSD does not work. restart jboss after uploading the new XSD.
    - after jboss restart, go to the affected custom map (either tap-scb-custom, or tap-cust-stp-dist, or tap-cust-nonstp-dist) and click on the "Update configuration for current basic class" button. This is the button that looks like a refresh icon. if there is nothing that has changed on the XSD, it will say "Nothing to change". if there are changes to the XSD, it will show the changes to the XSD and then you can select which ones should be added into the MMC. after accepting the new changes, the MMC will be updated and the new components will appear on the mmc. then you can proceed to map the new component with the corresponding value from TAP segmentation.
    - after changing the MMC, restart jboss for changes to take effect.
- custom message is processed by custom WTX which is created for SCB. in order to process the new TDS XML, the WTX map has to be updated as well.
 
WTX
- when building the wtx map, select Linux (Intel Processor)
- import the new XSD by right clicking on "Type Trees" -> import. then select the new XSD. this will create an mtt file. update the type tree of the input cards to refer to this new mtt. after updating the input cards, the WTX map should now be able to recognize the new XML structure that is generated by TDS.
 
CMD INSUPD instr_compo
ATT parent_instr_id instr_id begin_d end_d quantity_n
DAT 100 500 20210901 KEEP_DV 5
 
KEEP_DV
    - if there is a value already existing in a field, just keep the value of that field
    - e.g. if end_d has value 20210930, and the instruction is KEEP_DV, TAP will keep the value 20210930
NULL_DV
    - sets a field to null, or to the default value of the field
    - e.g. TAP has a default value for end_d of 20991231. if the instruction is NULL_DV, and previously there was a value of 20210930, TAP will set the value from 20210930 to 20991231.
    - e.g. if a field has no default value, then it gets set to null in TAP.
NULL
    - sets a field to null, regardless of DV











