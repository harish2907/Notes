Find any text in folder using linux

grep -rnw '/path/to/somewhere/'-e 'pattern'
    • -r or -R is recursive,
    • -n is line number, and
    • -w stands for match the whole word.
    • -l (lower-case L) can be added to just give the file name of matching files.
    • -e is the pattern used during the search
Along with these, --exclude, --include, --exclude-dir flags could be used for efficient searching:
    • This will only search through those files which have .c or .h extensions:
grep --include=\*.{c,h} -rnw '/path/to/somewhere/'-e "pattern"
    • This will exclude searching all the files ending with .o extension:
grep --exclude=\*.o -rnw '/path/to/somewhere/'-e "pattern"
    • For directories it's possible to exclude one or more directories using the --exclude-dir parameter. For example, this will exclude the dirs dir1/, dir2/ and all of them matching *.dst/:
grep --exclude-dir={dir1,dir2,*.dst} -rnw '/path/to/search/'-e "pattern"



Force Kill Jboss server:
ps -ef | grep jboss | grep -v grep | awk '{print $2}' | xargs kill -9



Copy from one server to another server:
scp standalone.conf user@ip:/home/tdsuser/Hayabusa_Squad/Harish/

Join lines of every n rows
awk 'NR % 900 == 1 { print "" } { printf "%s",$0 } END { print "" }' RIC.txt > RIC_900.txt


Extract comma separated even if its in middle
awk -v FPAT='[^,]*|"[^"]+"' '{print $1,$2,$3,$8,$13,$43,$44}' OFS="," *.new


Match two file with different column:
awk -F'|' 'FNR==NR{arr[$1,$4]=1;next} arr[$2,$5]{print}' TE_SECURITIES_RES_SPD_delimited.csv FIN_SPEED_20230331201353188.csv 

awk -F'|' 'FNR==NR{arr[$2,$5]=1;next} !arr[$1,$4]{print $0}' FIN_SPEED_20230331201353188.csv TE_SECURITIES_RES_SPD_delimited.csv | cut -d'|' -f1,4Â  this will print not found isisn

Compare two files:
awk 'FNR==NR{arr[$0]=1;next} !arr[$0]{print}' file1 file2

Get duplicated values in that column:
cut -d',' -f1 filename | sort | uniq -d

Remove duplicates using n columns:
awk -F, '!a[$1,$3]++' $ALL_RT_FILES_DUPLICATES | sort -t, -k1,1 -k7,7r
sort -t, -u -k1,1 -k7,7r $ALL_RT_FILES_DUPLICATES

Get duplicates line or particular column:
awk -F, 'a[$0]++' RT_1457_20230510204326.csv.sort.cp_37

Get Null values in that Particular Column:
awk -F, '$3 == "" {print}' $ALL_RT_FILES

Join two file with matching nth column with First file and mth column in second file:
join -t',' -1 1 -2 1 -o '1.1,1.2,1.3,1.4,1.5,1.6,1.7,1.8,2.3' -a 1 $CP_37.sort $ALL_RT_FILES

Check particular column matches and then return output at the last column:
awk -F"," '{ if($1==""||$9=="") print $0",N/A"; else if ($6==$9) print $0",1"; else if ($6!=$9) print $0",0" }' $CP_37.sort.static


Remove first line in that file:
sed -i '1d' filename

Copy file from one sever to another server with same date:
scp -p username@ip:/apps/TDS/interfaces/online/RT/processed/SCB_STATIC_DATA.*.csv .

Add first line of the file:
sed -i '1s/^/Harish\n/' filename
s for substitute command -I for inplace editing which means changes will be directly to the file ^ for start of the line

Compare each consecutive columns:
awk -F'|' '{OFS="|";output=""; for (i=1;i<=26;i+=2) { if($i!=$(i+1)) output = output OFS $i OFS  $(i+1) OFS "0"; else output = output OFS $i OFS  $(i+1) OFS "1";} print output}' test.csv

Unique records:
awk 'NR==FNR{uu[$1]=1}NR!=FNR&&uu[$1]!=1{print}' file1 file2

Found that column is available or not:
awk -F'|' 'FNR==NR{arr[$2]=1;next} !arr[$2]{print $0}' file1 file2 | cut -d'|' -f2 > not_found

It will merge the line untill its empty:
Input -> 1 \n2\n3\n \n 4\n5\n \n 6\n7\n8\n 
Output -> 123\n 45\n 678\n
awk 'BEGIN {ORS=""} NF {print} NF==0 {print "\n"}' file1

ORS -> Output record separator
NF -> No of fields

Get count of blank line:
 grep -c '^$' file

^ -> start of line
$-> end of line

awk -F"," '{FS=OFS=",";if($2!="" && $2!="N.A.")if($4=="N.A.") print $1,$2,$3,"0",$5; else print $0;}' equity_price_full_id_bb.txt | awk -F, '!a[$0]++' | sort -t',' -k2,2 -k3,3 | sed 's/\.\([0-9]\)/0\.\1/'

Bash Trap Command:
trap command is used to register cleanup function to execute when script exits. cleanup function removes temporary file and prints a message to console. When script exits, either by completing its work or by encountering an error, cleanup function will execute, removing temporary file.

trap 'echo "Signal SIGINT caught"' SIGINT
 while true do echo "Press Ctrl-C to generate SIGINT signal" sleep 1 done

function finish()
{
    sed -i -e "s/${ISIN}/CHANGE_ISIN/g" $SQL_Query
}
trap 'rc=$?; finish; exit $rc' EXIT INT


Add Quotes for sql query:
awk '{ printf("%s%s", (NR==1? "" : ", "),"\x27"$0"\x27") } END { printf("\n") }' filename


 git shortlog --summary --numbered --all --no-merges --since="11 Jul 2023"  --before="24 Aug 2023"

 scp -i "/c/Users/user/.ssh/aws_key" -o StrictHostKeyChecking=no username@ip



To remove last line last char:
sed '$ s/.$//' 

To replace any char to single quote:
sed 's/char/'\''/g')

Change Password in one line:
echo 'user:password'| sudo chpasswd ; sudo su - tdsuser

Connect ssh using password in one line:
sshpass -p !4u2tryhack ssh username@host.example.com

Substitute in awk command:
awk -F, '/,/{gsub(/ /, "", $2); print$1","$2} ' input.txt
-F,            use comma as field separator 
               (so the thing before the first comma is $1, etc)
/,/            operate only on lines with a comma 
               (this means empty lines are skipped)
gsub(a,b,c)    match the regular expression a, replace it with b, 
               and do all this with the contents of c

Splitting every 100 line into files: 
split -l 100 -d -a 2 TOTAL_ISIN.TXT ISIN_PART_

pstree

./dbCompareTool.sh 3 > nohup.out 2>&1 & -> 82570
 disown
 ->  it will continue the background process even after we close the terminal or log out.
-> to detach it from the shell and preventing ot from receiving the hangup signal ('SIGHUP') when terminal exits.

counter=0;max=10;while true;do printf "\r$(date)....";sleep 1; ((counter++));if [ $counter -ge $max ]; then echo -e "\nExisting loop.."; break; fi; done

counter=0;max=10;while true;do printf "\r$(date)....$(ls | wc -l)....";sleep 1; done

./TDS_EQUITY_CONSOLIDATION.sh > nohup.out 2>&1 &
R21 Consolidation -> 42953

cd /apps/tmp/tds_performance_test/apache-jmeter-5.6.2/bin/TestPlans/FIOP
pdbcli -sfiop TDM 123 "NL00150023L4" null null null null null null 1 "PT-FIOP" null


./doit.sh > nohup.out 2>&1 & 

Ls -R, du -a path, find path -print  -> These commands will print dir recursively 

find archive/ -maxdepth 1 -type d -print -> find commands


find ./online -path ./online/TAP_T -prune -o -print

find ./online -type d -not -path "./online/TAP_T/*" -prune
