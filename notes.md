# Intro 
-	Who and why
    - Why do we use Powershell 
    - Its objects
    - Microsoft backing
    - Training
    - Command discovery
        - Get-command *rest* .. hey look this is how we see all the cmdlets with rest in them
        - Get-help invoke-restmethod -show windows
    - Ubiquity with many vendors ( if you don’t look at linux )
    - Great dev tools 
        - ISE
    - Visual studio code
    - DSC 
    - Makes it easy to automate build new puppet code!
# why ps over curl / bash / jq

  ## OK, I know what objects are but why is this better than bash? (for some things, please don’t throw any chairs)
    - why dealing with objects in the command line is so much easier 
    - how you play with data but not have to keep hitting your server
    - examples 
        - status endpoint 
        - config change to enable http endpoint 
        - see https://docs.puppet.com/pe/2017.1/status_api.html
        - show how to do it in curl, and the results
        - show how to take what I have in curl to powershell
        - demo the difference on how easy it is to work with what powershell returns vs curl ( at least for a windows guy)
    - that’s great but I need SSL 
    - no problem… if you know where to look
    - depends on how your certs are signed 
    - probably using the puppet ca
    - your puppet ca server is probably not a trusted ca
    - code snipit to allow non trusted ca! 
# create an api cert( really name it what you want) 
    - On master... 
    - Generate key 
    - puppet cert generate api
    - You can call it anything .. api is just an example
    - Openssl to convert to pfx 
    - openssl pkcs12 -export -out /home/jxj3505/api-pupcert.pfx -inkey /etc/puppetlabs/puppet/ssl/private_keys/api.pem -in /etc/puppetlabs/puppet/ssl/certs/api.pem -certfile /etc/puppetlabs/puppet/ssl/certs/ca.pem
    - Copy the cert from the linux server to your windows box or wherever you need it
    - Don't forget to change ownership if you are a linux newbie!
    - i. chown <userid> <pfxfile>
## On puppetdb 
    - vim /etc/puppetlabs/puppetdb/certificate-whitelist
    - ( add the cert name you created) "api" is the example we used
    - Restart puppetdb
    - service pe-puppetdb restart
## On puppet console 
    - vim /etc/puppetlabs/console-services/rbac-certificate-whitelist
    - ( add the cert name you created)
    - Restart puppet console services 
        - service pe-console-services restart
## Run the commands you need!
    - Return to the status endpoint but this time with SSL
# Classifier code example 
    - Show all your roles!
# Puppetdb querey 
    - Look how few linux boxes we have
# Using Tokens 
    - Just a brief thing as we are running out of time
    - Forcing a code sync 
        - Show how to use tokens to force a sync
    - If we have time 
    -Quick puppet status check script.
