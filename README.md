# Welcome to Embedding a Single Dossier

## MicroStrategy 2021 Update 2 Feature

### REQUIREMENTS: The html file in this github must be hosted on a webserver to use or test this feature. You can not test hosting the html file on your local machine

Created: (07/26/2021)

1. You will need some metadata from your dossier. We need to obtain the visualizationKey to specify which vizualization you would like to embed. 

	Open:

	https://demo.microstrategy.com/MicroStrategyLibrary/api-docs/index.html 

	replacing `demo.microstrategy.com` with your env url

	For example

	https://env-			239777.customer.cloud.microstrategy.com/MicroStrategyLibrary/api-docs/index.html

2. First we will need to get an auth token by logging in. Open `/api/auth/login` and click the `try it out` button. Change the `username` and `password` field to the appropriate credentials and click the `execute` button. If successful the response code is 204 and will look like this

>cache-control: no-cacheno-storemax-age=0must-revalidate 
>date: Wed28 Jul 2021 14:38:42 GMT  
>expires: 0  pragma: no-cache  
>server: MicroStrategy x-mstr-authtoken: ==vi2k3iviqbgi10o500ri5mei3l==


3. For the next step you will need the authtoken which is hightlighted above, the `projectID` and `dossierID` You can get the `projectID` and `dosserID` a few different ways. The easiest way is to open the dossier using MicroStrategy Library. Here is the url of a dossier when opened using Library that contains the vizualization that we would like to embed 


https://env-239777.customer.cloud.microstrategy.com/MicroStrategyLibrary/app/==B7CA92F04B9FAE8D941C3E9B7E0CD754==/==A5EB1A9611EB6D59A1140080EF358A89==

The projectID is the first part of the URL that is highlighted. The dossierID is the second.

Using this data go to `/api/dossiers/{dossierID}/definition`, click `try it out` ,enter the three required fields and click `execute`.

```
{  "id":  "CD44B24111EB54FA4FDA0080EFA51096",  
   "name":  "South Example",  
   "chapters":  [  
      {  
         "key":  "K36",  
         "name":  "Chapter 1",  
         "pages":  [  
           {  
             "key":  "K53",  
             "name":  "Page 1",  
             "visualizations":  [  
               {  "key":  "K52",  
                  "name":  "Visualization 1"  
               },  
               {  
                 "key":  "W62",  
                 "name":  "Visualization 2"  
               },  
               {  
                 "key":  "W63",  
                 "name":  "Visualization 3"  
                }  
              ]  
            }  
         ],  
         "filters":  []  
       }  
     ]  
   }
```
4. The `key` under pages is the `vizualizationKey` that you will need to enter into the index.html file. The file is included in this github page.
5. You need to copy paste the index html file on a webserver. If you have a MicroStrategy env you can open the Remote Desktop Gateway, WinSCP navigate to 

`/opt/apache/tomcat/latest/webapps`

and create a folder and name is whatever you want. I will call my folder `kenny`

In folder:

`/opt/apache/tomcat/apache-tomcat-9.0.39/webapps/kenny`

create a index.html file and copy and paste the index.html file in this github.

Replace the credentials and anything between `<>` with the correct information. The URL to make sure that this feature is working is 

https://env-239777.customer.cloud.microstrategy.com/kenny/

where `kenny` is to be replace with the name of the folder that you created.