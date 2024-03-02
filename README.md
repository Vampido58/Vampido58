<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
$ip = $_POST["ip"];
$ports = array();

// Scan common ports from 1 to 1024
for ($port = 1; $port <= 1024; $port++) {
$connection = @fsockopen($ip, $port, $errno, $errstr, 1);
if ($connection) {
fclose($connection);
$ports[] = $port;
}
}

if (!empty($ports)) {
echo "Open ports on $ip:<br>";
echo "<ul>";
foreach ($ports as $open_port) {
echo "<li>Port $open_port is open</li>";
}
echo "</ul>";
} else {
echo "No open ports found on $ip.";
}
}
?>

<!DOCTYPE html>
<html>
<head>
<title>Port Scanner</title>
</head>
<body>
<h1>Port Scanner</h1>
<form method="post">
<label for="ip">Enter IP Address:</label>
<input type="text" id="ip" name="ip" required>
<input type="submit" value="Scan Ports">
</form>
</body>
</html>
