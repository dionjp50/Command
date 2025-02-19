# Recon
1. ```bash
   subfinder -d [example.com](http://example.com) -all -recursive -o url1.txt
2. ```bash
   assetfinder -subs-only  [example.com](http://example.com) > url2.txt
3. ```bash
   export PATH=$PATH:~/go/bin
4. ```bash
   amass enum -passive -d [example.com](http://example.com/) -o out.txt
5. ```bash
   cat url1.txt url2.txt | anew all_subs.txt
6. ```bash
   cat all_subs.txt | httpx -silent -td -title -sc -ip | anew urls.txt
7. ```bash
   cat urls.txt | awk ‘{print $1}’ > live_subs.txt
8. ```bash
   nuclei -list live_subs.txt -rl 10 -bs 2 -c 2 -as -silent -s critical,high,medium
9. ```bash
   cat urls.txt | grep 403
10. ```bash
    cat urls.txt | grep -v -i -E ‘Cloudflare|imperva|Cloudfront’ > nowaf_subs.txt
11. ```bash
    cat urls.txt | grep -v -i -E cloudflare|imperva|cloudfront
12. ```bash
    cat nowaf_subs.txt | grep 403 | awk ‘{print $1}’ > 403_nowaf.txt

# Start Nuclei for list all domain
1. ```bash
   nuclei -list live_subs.txt -t ~/nuclei-templates/http/exposures -o output_live_subs.txt
2. ```bash
   nuclei -list live_subs.txt -t ~/nuclei-templates/http/misconfiguration -o output_msc.txt
3. ```bash
   nuclei -list live_subs.txt -t ~/nuclei-templates/http/exposed-panels -o output_ep-live_subs.txt
4. ```bash
   nuclei -list live_subs.txt -t ~/nuclei-templates/dns -o output_dns.txt
5. ```bash
   nuclei -list live_subs.txt -t ~/nuclei-templates/http/default-logins -o output_deflog.txt

