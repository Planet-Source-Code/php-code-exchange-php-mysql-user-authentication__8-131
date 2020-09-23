﻿<div align="center">

## PHP/MySQL User Authentication


</div>

### Description

This script is a MySQL and PHP user authentication system. It stores everything in a MySQL database. You need to create a database called secretDB. Make a table called users. And add 5 fields to it. Name the 5 fields id, real_name, username, password, email. You can set all of the fileds to char255. If you have any questions, mail me at tyler.longren@midiowa.net by Tyler Longren
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[PHP Code Exchange](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/php-code-exchange.md)
**Level**          |Advanced
**User Rating**    |4.0 (44 globes from 11 users)
**Compatibility**  |PHP 3\.0, PHP 4\.0
**Category**       |[Complete Applications](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/complete-applications__8-7.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/php-code-exchange-php-mysql-user-authentication__8-131/archive/master.zip)





### Source Code

```
Script Note:
This script is a MySQL and PHP user authentication system. It stores everything in a MySQL database. You need to create a database called secretDB. Make a table called users. And add 5 fields to it. Name the 5 fields id, real_name, username, password, email. You can set all of the fileds to char255. If you have any questions, mail me at tyler.longren@midiowa.net
Name this file adduser.php
<!---Adduser html form begins here--->
<html>
<head><title>User Admin Page : Add a User</title></head>
<body bgcolor="#ffffff">
<table bgcolor=#000000 valign=top align=center border=0><tr><td
bgcolor=#000000><table cellpadding=4 bgcolor=#ffffff cellspacing=2 border=0>
<Tr><th>Add a User</th></tr><tr><td>
<FORM METHOD="post" ACTION="add.php">
Real Name: <INPUT TYPE=text MAXLENGTH=70 NAME="real_name" SIZE=20><Br>
Username: <INPUT TYPE=text MAXLENGTH=70 NAME="username" SIZE=20><Br>
Password: <Input Type=text Maxlength=70 Name="userpass" Size=10><Br>
E-mail address: <Input Type=text Maxlength=70 Name="email" Size=20><Br>
<INPUT TYPE=submit VALUE="Add"> <INPUT type=reset VALUE="Reset Form"></form>
</tr></td></table></tr></td></table>
</body>
</html>
<!---Adduser html form ends here--->
Name this file add.php
<!---Adduser php script begins here--->
<?
$ID = uniqid("userID");
$db = mysql_connect("localhost","root","$password");
mysql_select_db (secretDB);
$result = mysql_query ("INSERT INTO users (id, real_name, username, password, email)
        VALUES ('$ID', '$real_name', '$username', '$userpass',
'$email')       ");
if(!$result)
{
  echo "<b>User not added:</b> ", mysql_error();
  exit;
}
if($result)
	{
	mysql_close($db);
	print "User <b>$username</b> added sucessfully!";
	}
else
{
print ("Wrong Password");
}
?>
<!---Adduser php script ends here--->
Name this file deluser.php
<!---Deleteuser html form begins here--->
<html>
<head><title>User Admin Page : Add a User</title></head>
<body bgcolor="#ffffff">
<table bgcolor=#000000 valign=top align=center border=0><tr><td
bgcolor=#000000><table cellpadding=4 bgcolor=#ffffff cellspacing=2 border=0>
<Tr><th>Delete a User</th></tr><tr><td>
<FORM METHOD="post" ACTION="delete.php">
Real name: <INPUT TYPE=text MAXLENGTH=70 NAME="real_name" SIZE=20><Br>
Username: <INPUT TYPE=text MAXLENGTH=70 NAME="username" SIZE=20><Br>
<br>
<INPUT TYPE=submit VALUE="Delete"> <INPUT type=reset VALUE="Reset Form"></form>
</tr></td></table></tr></td></table>
</body>
</html>
<!---Deleteuser html form ends here--->
Name this file delete.php
<!---Deleteuser php script begins here--->
<?
$connection = mysql_connect("localhost","root","F0AA2pa8") or die ("Unable to
connect to MySQL server.");
mysql_select_db("secretDB",$connection)
or die ("Unable to select requested database.");
$deleteresult = mysql_query
("DELETE FROM users WHERE real_name = '$real_name' AND username = '$username'");
 $result=mysql_query($deleteresult, $connection);
 $affected_rows=mysql_affected_rows( $connection);
echo "<b>$username</b> was probably deleted sucessfully.";
?>
<!---Deleteuser php script ends here--->
Name this file form.php
<!---Login html form begins here--->
<html>
<head><title>Login form</title></head>
<body bgcolor="#ffffff">
<form action="login.php" method="post">
<table border="0">
<tr>
<td><strong>Username</strong></td>
<td><input type="text" name="username" size="10" maxsize="50"></td>
</tr>
<tr>
<td><strong>Password</strong></td>
<td><input type="password" name="password" size="10" maxsize="50"</td>
</tr>
<tr>
<td colspan="2" align="center">
<input type="submit" value="Auth me">
</td>
</tr>
</table>
</form>
</body>
</html>
<!---Login html form ends here--->
Name this file login.php
<!---Login php srcipt begins here--->
<?
mysql_connect("localhost", "root", "F0AA2pa8")
	or die ("Unable to connect to server.");
mysql_select_db("secretDB")
	or die ("Unable to select database.");
$sql = "SELECT id
	FROM users
	WHERE username='$username' and password='$password'";
$result = mysql_query($sql)
	or die ("Unable to get results.");
$num = mysql_numrows($result)
	or die ("You're not authorized to be here. If you feel you have recieved this
message in error, please contact the <a
href=\"mailto:tyler.longren@midiowa.net\">webmaster</a>");
if ($num == 1) {
echo "<p>You can be here<br>";
echo "Your username is $username</p>";
}
?>
<!---Login php script ends here--->
Name this file print.php
<!---View users php script begins here--->
<?php
echo "<html><head><title>User Information</title></head><body
bgcolor=#ffffff>";
$connection = mysql_connect("localhost","root","F0AA2pa8")
or die ("Unable to connect to MySQL server.");
$db = mysql_select_db("secretDB", $connection) or die ("Unable to select
database.");
$sql = "SELECT id, real_name, username, email
		FROM users
		ORDER BY id ASC";
$sql_result = mysql_query($sql,$connection) or die ("Couldn't execute SQL
query");
echo "<center><b><u>List of users</u></b><br><Br>";
echo "<table bgcolor=#000000><Tr><td bgcolor=#000000><table cellpadding=4
cellspacing=0 bgcolor=#ffffff>"; echo "<Tr><th>ID</th><th>Full
Name</th><th>Username</th><th>E-mail</th></tr>"; while ($row =
mysql_fetch_array($sql_result)) { $id = $row["id"];
$real_name = $row["real_name"];
$username = $row["username"];
$email = $row["email"];
echo
"<tr><td>$id</td><td>$real_name</td><td>$username</td><td>
<a href=\"mailto:$email\">$email</a></td></tr>"; }
echo "</table></td></tr></table>";
echo "</center>";
mysql_free_result($sql_result);
mysql_close($connection);
echo "</body></html>";
?>
<!---View users php script ends here--->
```

