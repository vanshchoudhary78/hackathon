# hackathon


live on - https://vanshchoudhary78.github.io/hackathon/


To connect your contact form to a database and store submissions, follow these steps:

1. Create the Database and Table (MySQL Example)
Run these SQL commands in your database management tool (e.g., phpMyAdmin):
sql:

CREATE DATABASE contact_form_db;
USE contact_form_db;

CREATE TABLE messages (
    id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(50) NOT NULL,
    message TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

2. Update Your PHP Form Handler (submit-form.php)
Create a file named submit-form.php in the same directory as your HTML file:
php:

<?php
// Database configuration
$servername = "localhost";
$username = "your_db_username"; // Replace with your database username
$password = "your_db_password"; // Replace with your database password
$dbname = "contact_form_db";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Sanitize and retrieve form data
$name = $conn->real_escape_string($_POST['name']);
$email = $conn->real_escape_string($_POST['email']);
$message = $conn->real_escape_string($_POST['message']);

// Insert data into database
$sql = "INSERT INTO messages (name, email, message) VALUES ('$name', '$email', '$message')";

if ($conn->query($sql) === TRUE) {
    echo "Message sent successfully!";
} else {
    echo "Error: " . $sql . "<br>" . $conn->error;
}

// Close connection
$conn->close();
?>
