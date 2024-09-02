config.php
<pre><?php
$host = "localhost";
$uesr = "root";
$pass = "";
$dbmana = "small";

$con = new mysqli($host, $uesr, $pass, $dbmana);
if ($con->connect_error) {
    die("some error" . $con->connect_error);
}
</pre>











add.php
<pre>
<?php include 'config.php'
?>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <form action="add.php" method="post">
        <h2>add data</h2>
        <lable>id</lable>
        <input type="text" name="id">
        <lable>name</lable>
        <input type="text" name="name">
        <lable>age</lable>


        <input type="text" name="age">
        <input type="submit" value="submit" name="submit">
    </form>
    <?php
    if (isset($_POST['submit'])) {
        $id = $_POST['id'];
        $name = $_POST['name'];
        $age = $_POST['age'];
        $sql = "INSERT INTO data (id,name,age) VALUES ('$id','$name','$age')";
        if ($con->query($sql) === TRUE) {
            echo "new recored add";
        }
    } ?>
</body>

</html>
</pre>




delete.php
<pre>
<?php include 'config.php'
?>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <form action="delet.php" method="post">
        <h2>Delete Data</h2>
        <label for="delete_id">ID</label>
        <input type="text" name="delete_id" id="delete_id">
        <input type="submit" value="Submit" name="delete">
    </form>
    <?php
    if (isset($_POST['delete'])) {
        $id = $_POST['delete_id'];
        $sql = "DELETE FROM data WHERE id='$id'";

        if ($con->query($sql) === TRUE) {
            echo "Record deleted successfully";
        } else {
            echo "Error deleting record: " . $con->error;
        }
    }
    ?>
    
</body>

</html>
</pre>


search.php
<pre>
<?php include 'config.php'; ?>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Data Management</title>
</head>

<body>
    <h2>Data Management</h2>
    <form action="" method="post">
        <label for="id">ID</label>
        <input type="text" name="id" id="id" value="<?php echo isset($_POST['id']) ? htmlspecialchars($_POST['id']) : ''; ?>">
        <br>
        <label for="name">Name</label>
        <input type="text" name="name" id="name" value="<?php echo isset($name) ? htmlspecialchars($name) : ''; ?>">
        <br>
        <label for="age">Age</label>
        <input type="text" name="age" id="age" value="<?php echo isset($age) ? htmlspecialchars($age) : ''; ?>">
        <br>
        <input type="submit" value="Search" name="search">
        <input type="submit" value="Update" name="update">
    </form>

    <?php
    // Initialize variables
    $name = $age = '';

    // Search functionality
    if (isset($_POST['search'])) {
        $id = $con->real_escape_string($_POST['id']);
        $result = $con->query("SELECT * FROM data WHERE id='$id'");
        if ($result->num_rows > 0) {
            $row = $result->fetch_assoc();
            $name = $row['name'];
            $age = $row['age'];
            echo "Record found!";
        } else {
            echo "No records found";
        }
    }

    // Update functionality
    if (isset($_POST['update'])) {
        $id = $con->real_escape_string($_POST['id']);
        $name = $con->real_escape_string($_POST['name']);
        $age = $con->real_escape_string($_POST['age']);
        $sql = "UPDATE data SET name='$name', age='$age' WHERE id='$id'";
        if ($con->query($sql) === TRUE) {
            echo "Record updated successfully";
        } else {
            echo "Error updating record: " . $con->error;
        }
    }
    ?>
</body>

</html>
</pre>


show.php
<pre>
<?php include 'config.php'
?>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <?php
    $sql = "SELECT * FROM data";
    $result = $con->query($sql);
    if ($result->num_rows > 0) {
    ?>
        <table border="2" width="55%">
            <tr bgcolor="#C45786">
                <th>id</th>
                <th>name</th>
                <th>age</th>
            </tr>
            <?php
            while ($row = $result->fetch_assoc()) {
            ?>
                <tr>
                    <td><?php echo htmlspecialchars($row['id']) ?></td>
                    <td><?php echo htmlspecialchars($row['name']) ?></td>
                    <td><?php echo htmlspecialchars($row['age']) ?></td>
                </tr>
            <?php
            }
            ?>
        </table>
    <?php
    } else {
        echo "error" . $conn->error;
    }
    ?>
</body>

</html></pre>
