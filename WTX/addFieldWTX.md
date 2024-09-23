    1) Go to input folder.
    2) Copy the latest file and edit the file name with current date.
    3) Add the new fields in latest xsd file as per requirement.
    4) Import the new xsd file in input folder and then tds2tap12_input type tree.
    5) Please verify your new field is added in their respective place.
        a. 
    6) Analyze type tree on their respective mtt file.
    7) Go to respective map files tds2tap
    8) Go to tds_xm_message input card and change the new mtt file and save the map file.
    9) Then goto tds2tap_output.mtt file.
    10) Add fields in dataType,Fields
    11) Add the new fields from Fields category to record category.
    12) Analyze output type tree.
    13) Find the Functional mapping from backward
        a. 8th output card ->  -> Enter the rules as perrequiremnt from input card.
        b. Build the Map with linux if its any error resolve it.
    14) Login into tapuser ssh .
    15) Take the backup tds2tap.lnx file in this loc -> path
    16) Copy the file from project map folder to in this folder.
    17) Goto  in this "file.cfg" add the fields in their respective place.
    18) Check "ATT_LINE" in that check for respective "TAP table" ex:table 
        a. 
    19) Type "gwp" and enter.
    20) Go to this path  and run this script "GWPACK_Menu.sh"
Restart launcher.
