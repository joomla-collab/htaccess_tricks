# Useful HTACCESS techniques

How to redirect all queries to a new domain, but retaining images, css and js queries.  
Very useful when migrating a website, but not sure you caught all absolute links (especially if you didn't build the website yourself).

```
##### RewriteEngine enabled - BEGIN
RewriteEngine On
##### RewriteEngine enabled - END

# First, check if a specific type is being requested
RewriteCond %{REQUEST_URI} !\.(png|jpg|gif|jpeg|bmp|css|js|less|coffee)$ [NC]
# Second, check if the request is for an existing file
RewriteCond %{REQUEST_FILENAME} -f
# If both conditions are true, then skip rewriting
RewriteRule ^ - [L]

# Otherwise, continue:
RewriteRule ^(.*)$ http://yourdomain.com/$1 [R=301,L]
```

------

## Disallow access to rogue PHP files throughout the site, unless they are explicitly allowed
The below htaccess rule, allows you to disallow access of unknown php files. By default 3 php files should be allowed in Joomla! If you wish to allow more php files, you can add them.
```
RewriteCond %{REQUEST_FILENAME} (\.php)$
# Exclude index.php of front-end
RewriteCond %{REQUEST_FILENAME} !(/path/to/joomla/root/folder/index.php)$
# Exclude index.php of back-end (administrator)
RewriteCond %{REQUEST_FILENAME} !(/path/to/joomla/root/folder/administrator/index.php)$
# below file is need to be excluded for updating joomla
RewriteCond %{REQUEST_FILENAME} !(/path/to/joomla/root/folder/administrator/components/com_joomlaupdate/restore.php)$
RewriteCond %{REQUEST_FILENAME} -f
RewriteRule (.*\.php)$ - [F]
```
