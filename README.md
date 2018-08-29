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
