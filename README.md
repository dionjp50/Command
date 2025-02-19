# Recon
1. ```subfinder -d [example.com](http://example.com) -all -recursive -o url1.txt``` (Mencari Sub Domain)
2. assetfinder -subs-only  [example.com](http://example.com) > url2.txt
3. export PATH=$PATH:~/go/bin
4. amass enum -passive -d [example.com](http://example.com/) -o out.txt
5. cat url1.txt url2.txt | anew all_subs.txt
6. cat all_subs.txt | httpx -silent -td -title -sc -ip | anew urls.txt
7. cat urls.txt | awk ‘{print $1}’ > live_subs.txt
8. nuclei -list live_subs.txt -rl 10 -bs 2 -c 2 -as -silent -s critical,high,medium
9. cat urls.txt | grep 403
10. cat urls.txt | grep -v -i -E ‘Cloudflare|imperva|Cloudfront’ > nowaf_subs.txt  ( No WAF Filtering)
11. cat urls.txt | grep -v -i -E cloudflare|imperva|cloudfront
12. cat nowaf_subs.txt | grep 403 | awk ‘{print $1}’ > 403_nowaf.txt

# Start Nuclei for list all domain
1. nuclei -list live_subs.txt -t ~/nuclei-templates/http/exposures -o output_live_subs.txt
2. nuclei -list live_subs.txt -t ~/nuclei-templates/http/misconfiguration -o output_msc.txt
3. nuclei -list live_subs.txt -t ~/nuclei-templates/http/exposed-panels -o output_ep-live_subs.txt
4. nuclei -list live_subs.txt -t ~/nuclei-templates/dns -o output_dns.txt
5. nuclei -list live_subs.txt -t ~/nuclei-templates/http/default-logins -o output_deflog.txt

