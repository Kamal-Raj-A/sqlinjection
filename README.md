# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2
# OUTPUT
<img width="1036" height="516" alt="image" src="https://github.com/user-attachments/assets/ced909cf-fe07-44c0-adbb-7b9394b2c4a1" />


Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.
##  OUTPUT
<img width="748" height="488" alt="image" src="https://github.com/user-attachments/assets/f7147fe3-a745-4213-a062-11cbb0893c15" />


Select Multidae from the menu listed as shown above. The page is displayed as below:
##  OUTPUT
<img width="1037" height="495" alt="image" src="https://github.com/user-attachments/assets/0b8e01f1-2848-4f55-b52b-98fe3879b95d" />


Click on the menu Login/Register and register for an account
##  OUTPUT
<img width="1037" height="502" alt="image" src="https://github.com/user-attachments/assets/f4aa441b-80f9-4bd7-afdf-7b88f2befe11" />


Click on the link “Please register here”
##  OUTPUT
<img width="1033" height="503" alt="image" src="https://github.com/user-attachments/assets/db505d13-b993-4587-adca-34990659c92d" />



Click on “Create Account” to display the following page:
##  OUTPUT
<img width="1037" height="432" alt="image" src="https://github.com/user-attachments/assets/a8581009-09df-41c7-aaeb-bb0187551e99" />


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:


($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
##  OUTPUT
<img width="1042" height="502" alt="image" src="https://github.com/user-attachments/assets/ca1c938f-b3be-40ee-86f1-8a7432643278" />



Click “Login”. The logged in page will show as below:
##  OUTPUT
<img width="1192" height="747" alt="image" src="https://github.com/user-attachments/assets/ff39997c-be96-46bf-8883-a9b266c7eb18" />



If error faced in registration follow the following steps in metasploitable 2:


This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:
##  OUTPUT
<img width="1035" height="502" alt="image" src="https://github.com/user-attachments/assets/5c032d99-b7fe-4292-a923-bc5e32db96ae" />


Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure
##  OUTPUT
<img width="1027" height="352" alt="image" src="https://github.com/user-attachments/assets/4d90c921-1492-4b2c-ad3f-8937a734f93e" />


Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload
##  OUTPUT
<img width="1037" height="481" alt="image" src="https://github.com/user-attachments/assets/d4349c7c-b1d3-4918-a541-f35a11c40492" />


# Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.
##  OUTPUT
<img width="1037" height="492" alt="image" src="https://github.com/user-attachments/assets/ce177d57-4235-4f43-88c0-dcde6a52b830" />


# Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 
# OUTPUT
<img width="1040" height="527" alt="image" src="https://github.com/user-attachments/assets/d7e02279-1a81-4524-a780-58de2872c74f" />



Now after logging out you will see the login page. In the login page give ganesh’ # (myusername). You can see the page now enters into the administrator page as before when giving the password.
# OUTPUT
<img width="1040" height="527" alt="image" src="https://github.com/user-attachments/assets/cf3f3af4-c555-4aa2-a479-d9fe15507176" />


Click the login button and you will see it enter into the administrator page.
# OUTPUT
<img width="1036" height="570" alt="image" src="https://github.com/user-attachments/assets/9369d8ec-aa36-4265-bcae-13de0e50a8f7" />


## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
##  OUTPUT

<img width="1027" height="352" alt="image" src="https://github.com/user-attachments/assets/bc7cc580-328f-477b-9135-c58dc1423a2a" />


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
##  OUTPUT

<img width="1035" height="405" alt="image" src="https://github.com/user-attachments/assets/e952bb96-1a2b-4db7-8cdc-4a7c7490bfd9" />


Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
##  OUTPUT

<img width="1037" height="502" alt="image" src="https://github.com/user-attachments/assets/c4b93054-c80f-4766-86ff-26c172156544" />



After adding the order by 6 into the existing url , the following error statement will be obtained:
##  OUTPUT
<img width="1041" height="517" alt="image" src="https://github.com/user-attachments/assets/8cdb0c37-ccd2-4949-91f7-6780fb40643a" />




When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
#OUTPUT




 As it is having 5 columns the query worked fine and it provides the correct result
##  OUTPUT
<img width="1518" height="783" alt="image" src="https://github.com/user-attachments/assets/1b663470-90b2-42ca-96b8-cd4c5b4bc137" />




Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
##  OUTPUT
<img width="1772" height="365" alt="image" src="https://github.com/user-attachments/assets/aa0e1e9e-4170-42e4-944d-09507ac126d0" />



As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
##  OUTPUT
<img width="1275" height="705" alt="image" src="https://github.com/user-attachments/assets/45cf3f66-49a8-467c-8133-aea415859d97" />



Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
##  OUTPUT
<img width="1681" height="838" alt="image" src="https://github.com/user-attachments/assets/b87ad921-ac1d-4289-b9b7-e6c7f8dbf2cc" />



The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
##  OUTPUT
<img width="1681" height="838" alt="image" src="https://github.com/user-attachments/assets/043ff064-1e22-4972-aad5-9497ecb8c41a" />




The url once executed will  retrieve table names from the “owasp 10” database.
##Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
##  OUTPUT
<img width="1907" height="885" alt="image" src="https://github.com/user-attachments/assets/e2f2f193-6d8b-4cd5-9383-220311552023" />



The column names of the accounts is displayed below for the following url:


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).
##  OUTPUT
<img width="1920" height="900" alt="image" src="https://github.com/user-attachments/assets/8d9d2498-c37d-4f41-b0f7-550c69987baf" />



## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).


##  OUTPUT
<img width="1918" height="908" alt="image" src="https://github.com/user-attachments/assets/6d15c4da-6859-41f9-85d6-f3e6f9cde017" />


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
