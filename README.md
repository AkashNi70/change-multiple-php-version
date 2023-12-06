INSTALL MULTIPLE PHP VERSION IN XAMPP

Lets set it up

Step 1: Download PHP ( https://windows.php.net/downloads/releases/archives/ )

You want to add an older PHP version to it (say PHP 5.6).Download the nts (Non Thread Safe) version of the PHP zip archive from php.net (see archive for older versions) and extract the files under c:\xampp\php56.

Step 2: Configure php.ini

Open the file c:\xampp\php56\php.ini in notepad. If the file does not exist, copy php.ini-development to php.ini and open it in notepad. Then uncomment the following line:

extension_dir = "ext"

Also if the following line exists in Apache config httpd-xampp.conf
add this line

SetEnv PHPRC "\\path\\to\\xampp\\php56"

Step 3: Configure apache

Open xampp control panel, click the config button for apache, and click Apache (httpd-xampp.conf). A text file will open. Put the following settings at the bottom of the file:

ScriptAlias /php56 "C:/xampp/php56"
Action application/x-httpd-php56-cgi /php56/php-cgi.exe
<Directory "C:/xampp/php56">
    AllowOverride None
    Options None
    Require all denied
    <Files "php-cgi.exe">
        Require all granted
    </Files>
</Directory>
S
Note: You can add more versions of PHP to your xampp installation following step 1 to 3 if you want.

Step 4 : [Run an older PHP version on a separate port]

Now to to set PHP v5.6 on port 8056, add the following code to the bottom of the config file (httpd-xampp.conf from Step 3).

Listen 8056
<VirtualHost *:8056>
    <FilesMatch "\.php$">
        SetHandler application/x-httpd-php56-cgi
    </FilesMatch>
</VirtualHost>
