<pre>
  <?php
$host = "localhost";
$user = "root";
$pass = "";
$dbname = "docmanagment";
$conn = new mysqli($host, $user, $pass, $dbname);
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

?>

</pre>



<pre><?php include 'config.php'; ?>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Add Doctor</title>
    <style>
        /* General styles for the page */
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        /* Container for the main content */
        .container {
            width: 80%;
            margin: auto;
            overflow: hidden;
        }

        /* Styling for the header */
        h2 {
            color: #333;
            text-align: center;
            padding: 20px 0;
        }

        /* Styling for the navigation bar */
        nav {
            background: #333;
            color: #fff;
            padding: 10px 0;
            text-align: center;
        }

        nav a {
            color: #fff;
            text-decoration: none;
            margin: 0 15px;
            font-weight: bold;
        }

        nav a:hover {
            text-decoration: underline;
        }

        /* Styling for the form */
        form {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin: 20px auto;
            max-width: 600px;
        }

        form label {
            display: block;
            margin-bottom: 10px;
            font-weight: bold;
        }

        form input[type="text"],
        form input[type="email"],
        form input[type="submit"],
        form select {
            padding: 10px;
            width: calc(100% - 22px);
            /* Full width minus padding and border */
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
            margin-bottom: 10px;
        }

        form input[type="submit"] {
            background: #333;
            color: #fff;
            border: none;
            cursor: pointer;
        }

        form input[type="submit"]:hover {
            background: #555;
        }

        form input[type="radio"] {
            margin-right: 5px;
        }

        /* Additional styling for the form groups */
        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
        }

        /* Optional: Responsive adjustments */
        @media (max-width: 768px) {
            .container {
                width: 95%;
            }

            form {
                padding: 15px;
            }

            form input[type="text"],
            form input[type="email"],
            form input[type="submit"],
            form select {
                width: calc(100% - 20px);
                /* Full width minus padding */
            }
        }
    </style>
</head>

<body>
    <h2>Add Doctor</h2>
    <!-- Form for adding a new doctor -->
    <nav>
        <a href="showdoc.php">Show Doctors</a> |
        <a href="addoc.php">Add Doctor</a> |
        <a href="searchdoc.php">Search Doctor</a> |
        <a href="deletedoc.php">Delete Doctor</a>
    </nav>
    <form action="addoc.php" method="post">
        <!-- Input field for Doctor ID -->
        <label for="drid">Doctor ID:</label>
        <input type="text" id="drid" name="drid" required><br>

        <!-- Input field for Doctor Name -->
        <label for="drname">Doctor Name:</label>
        <input type="text" id="drname" name="drname" required><br>

        <!-- Input field for Doctor Email -->
        <label for="dremail">Doctor Email:</label>
        <input type="email" id="dremail" name="dremail" required><br>

        <!-- Input field for Doctor Phone -->
        <label for="drphone">Doctor Phone:</label>
        <input type="text" id="drphone" name="drphone" required><br>

        <!-- Input field for Doctor Address -->
        <label for="draddress">Doctor Address:</label>
        <input type="text" id="draddress" name="draddress" required><br>

        <!-- Radio buttons for Doctor Speciality -->
        <label>Doctor Speciality:</label><br>
        <input type="radio" id="anesthesiologists" name="drSpeciality" value="anesthesiologists">
        <label for="anesthesiologists">Anesthesiologists</label><br>

        <input type="radio" id="cardiologists" name="drSpeciality" value="cardiologists">
        <label for="cardiologists">Cardiologists</label><br>

        <input type="radio" id="criticalcare" name="drSpeciality" value="criticalcare&medicine">
        <label for="criticalcare">Critical Care & Medicine</label><br>

        <input type="radio" id="dermatologists" name="drSpeciality" value="dermatologists">
        <label for="dermatologists">Dermatologists</label><br>

        <input type="radio" id="emergencyspecialists" name="drSpeciality" value="emergencyspecialists">
        <label for="emergencyspecialists">Emergency Specialists</label><br>

        <!-- Submit button -->
        <input type="submit" name="submit" value="Add Doctor">
    </form>

    <?php
    // Check if the form has been submitted
    if (isset($_POST['submit'])) {
        // Get form data
        $drid = $_POST['drid'];
        $drname = $_POST['drname'];
        $dremail = $_POST['dremail'];
        $drphone = $_POST['drphone'];
        $draddress = $_POST['draddress'];
        $drSpeciality = $_POST['drSpeciality'];

        // Prepare SQL query to insert data into the database
        $sql = "INSERT INTO dr (drid, drname, dremail, drphone, draddress, drSpeciality) VALUES ('$drid', '$drname', '$dremail', '$drphone', '$draddress', '$drSpeciality')";

        // Execute the query and check for success
        if ($conn->query($sql) === TRUE) {
            echo "New doctor added successfully.";
        } else {
            // Display error if query fails
            echo "Error: " . $sql . "<br>" . $conn->error;
        }
    }
    ?>
</body>

</html></pre>
<pre>
  <?php include 'config.php'; ?>

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Delete Doctor</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        /* Container for the main content */
        .container {
            width: 80%;
            margin: auto;
            overflow: hidden;
        }

        /* Styling for the header */
        h2 {
            color: #333;
            text-align: center;
            padding: 20px 0;
        }

        /* Styling for the navigation bar */
        nav {
            background: #333;
            color: #fff;
            padding: 10px 0;
            text-align: center;
        }

        nav a {
            color: #fff;
            text-decoration: none;
            margin: 0 15px;
            font-weight: bold;
        }

        nav a:hover {
            text-decoration: underline;
        }

        /* Styling for the search form */
        form {
            display: flex;
            justify-content: center;
            margin: 20px 0;
        }

        form input[type="text"] {
            padding: 10px;
            width: 300px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }

        form input[type="submit"] {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background: #333;
            color: #fff;
            font-size: 16px;
            cursor: pointer;
            margin-left: 10px;
        }

        form input[type="submit"]:hover {
            background: #555;
        }

        /* Styling for the table */
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }

        table,
        th,
        td {
            border: 1px solid #ddd;
        }

        th,
        td {
            padding: 10px;
            text-align: left;
        }

        th {
            background: #333;
            color: #fff;
        }

        tr:nth-child(even) {
            background: #f2f2f2;
        }

        tr:hover {
            background: #e0e0e0;
        }

        /* Styling for the action links */
        td a {
            color: #333;
            text-decoration: none;
            font-weight: bold;
        }

        td a:hover {
            text-decoration: underline;
        }
    </style>
</head>

<body>
    <h2>Delete Doctor</h2>
    <!-- Navigation links to other pages -->
    <nav>
        <a href="showdoc.php">Show Doctors</a> |
        <a href="addoc.php">Add Doctor</a> |
        <a href="searchdoc.php">Search Doctor</a> |
        <a href="deletedoc.php">Delete Doctor</a>
    </nav>
    <br>

    <?php
    // Check if the doctor ID is provided in the URL
    if (isset($_GET['drid'])) {
        $drid = $_GET['drid'];

        // Fetch the record to display the details
        $sql = "SELECT * FROM dr WHERE drid='$drid'";
        $result = $conn->query($sql);

        // Check if a record is found
        if ($result->num_rows == 1) {
            $row = $result->fetch_assoc();
    ?>

            <!-- Form to confirm deletion of the doctor -->
            <form action="deletedoc.php" method="post">
                <!-- Hidden input to pass the doctor ID -->
                <input type="hidden" name="drid" value="<?php echo htmlspecialchars($drid); ?>">
                <!-- Display doctor details -->
                Doctor ID: <?php echo htmlspecialchars($row['drid']); ?><br>
                Name: <?php echo htmlspecialchars($row['drname']); ?><br>
                Email: <?php echo htmlspecialchars($row['dremail']); ?><br>
                Phone: <?php echo htmlspecialchars($row['drphone']); ?><br>
                Address: <?php echo htmlspecialchars($row['draddress']); ?><br>
                Speciality: <?php echo htmlspecialchars($row['drSpeciality']); ?><br>
                <!-- Submit button to confirm deletion -->
                <input type="submit" name="delete" value="Delete">
            </form>

    <?php
        } else {
            // Display message if no record is found
            echo "No doctor found with the given ID.";
        }
    }

    // Check if the delete form has been submitted
    if (isset($_POST['delete'])) {
        $drid = $_POST['drid'];

        // Prepare and execute the delete query
        $sql = "DELETE FROM dr WHERE drid='$drid'";

        // Check if the query was successful
        if ($conn->query($sql) === TRUE) {
            echo "Doctor deleted successfully!";
        } else {
            // Display error message if the query fails
            echo "Error deleting record: " . $conn->error;
        }
    }
    ?>
</body>

</html>
</pre>
<pre><?php include 'config.php'; ?>

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Search Doctors by ID</title>
    <link rel="stylesheet" href="css/styles.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        /* Container for the main content */
        .container {
            width: 80%;
            margin: auto;
            overflow: hidden;
        }

        /* Styling for the header */
        h2 {
            color: #333;
            text-align: center;
            padding: 20px 0;
        }

        /* Styling for the navigation bar */
        nav {
            background: #333;
            color: #fff;
            padding: 10px 0;
            text-align: center;
        }

        nav a {
            color: #fff;
            text-decoration: none;
            margin: 0 15px;
            font-weight: bold;
        }

        nav a:hover {
            text-decoration: underline;
        }

        /* Styling for the search form */
        form {
            display: flex;
            justify-content: center;
            margin: 20px 0;
        }

        form input[type="text"] {
            padding: 10px;
            width: 300px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }

        form input[type="submit"] {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background: #333;
            color: #fff;
            font-size: 16px;
            cursor: pointer;
            margin-left: 10px;
        }

        form input[type="submit"]:hover {
            background: #555;
        }

        /* Styling for the table */
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }

        table,
        th,
        td {
            border: 1px solid #ddd;
        }

        th,
        td {
            padding: 10px;
            text-align: left;
        }

        th {
            background: #333;
            color: #fff;
        }

        tr:nth-child(even) {
            background: #f2f2f2;
        }

        tr:hover {
            background: #e0e0e0;
        }

        /* Styling for the action links */
        td a {
            color: #333;
            text-decoration: none;
            font-weight: bold;
        }

        td a:hover {
            text-decoration: underline;
        }
    </style>
</head>

<body>
    <h2>Search Doctors by ID</h2>
    <!-- Navigation links to other pages -->
    <nav>
        <a href="showdoc.php">Show Doctors</a> |
        <a href="addoc.php">Add Doctor</a> |
        <a href="searchdoc.php">Search Doctor</a> |
        <a href="deletedoc.php">Delete Doctor</a>
    </nav>
    <br>

    <!-- Search Form -->
    <form action="searchdoc.php" method="post">
        <input type="text" name="search_id" placeholder="Enter ID" required>
        <input type="submit" name="search" value="Search">
    </form>
    <br>

    <?php
    // Check if the form has been submitted
    if (isset($_POST['search'])) {
        $searchId = $_POST['search_id'];

        // Escape user input to prevent SQL injection
        $searchId = $conn->real_escape_string($searchId);

        // SQL query to search for doctors by ID
        $sql = "SELECT * FROM dr WHERE drid = '$searchId'";
        $result = $conn->query($sql);

        // Check if any records were returned
        if ($result->num_rows > 0) {
    ?>
            <!-- Display results in an HTML table -->
            <table border="1"> <!-- Added border for better visibility -->
                <tr>
                    <!-- Table headers -->
                    <th>ID</th>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Phone</th>
                    <th>Address</th>
                    <th>Speciality</th>
                    <th>Actions</th>
                </tr>
                <?php
                // Loop through each record and display it
                while ($row = $result->fetch_assoc()) {
                ?>
                    <tr>
                        <!-- Display each field of the record -->
                        <td><?php echo htmlspecialchars($row['drid']); ?></td>
                        <td><?php echo htmlspecialchars($row['drname']); ?></td>
                        <td><?php echo htmlspecialchars($row['dremail']); ?></td>
                        <td><?php echo htmlspecialchars($row['drphone']); ?></td>
                        <td><?php echo htmlspecialchars($row['draddress']); ?></td>
                        <td><?php echo htmlspecialchars($row['drSpeciality']); ?></td>
                        <td>
                            <!-- Links for updating and deleting the record -->
                            <a href="updatedoc.php?drid=<?php echo htmlspecialchars($row['drid']); ?>">Update</a> |
                            <a href="deletedoc.php?drid=<?php echo htmlspecialchars($row['drid']); ?>" onclick="return confirm('Are you sure you want to delete this record?');">Delete</a>
                        </td>
                    </tr>
                <?php
                }
                ?>
            </table>
    <?php
        } else {
            // Message displayed if no results are found
            echo "No results found.";
        }
    }
    ?>
</body>

</html></pre>
<pre><?php include 'config.php'; ?>

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Show Doctors</title>
    <!-- <link rel="stylesheet" href="css/styles.css"> -->
    <!-- Uncomment the line above to include global CSS styles -->
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        /* Container for the main content */
        .container {
            width: 80%;
            margin: auto;
            overflow: hidden;
        }

        /* Styling for the header */
        h2 {
            color: #333;
            text-align: center;
            padding: 20px 0;
        }

        /* Styling for the navigation bar */
        nav {
            background: #333;
            color: #fff;
            padding: 10px 0;
            text-align: center;
        }

        nav a {
            color: #fff;
            text-decoration: none;
            margin: 0 15px;
            font-weight: bold;
        }

        nav a:hover {
            text-decoration: underline;
        }

        /* Styling for the search form */
        form {
            display: flex;
            justify-content: center;
            margin: 20px 0;
        }

        form input[type="text"] {
            padding: 10px;
            width: 300px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }

        form input[type="submit"] {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background: #333;
            color: #fff;
            font-size: 16px;
            cursor: pointer;
            margin-left: 10px;
        }

        form input[type="submit"]:hover {
            background: #555;
        }

        /* Styling for the table */
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }

        table,
        th,
        td {
            border: 1px solid #ddd;
        }

        th,
        td {
            padding: 10px;
            text-align: left;
        }

        th {
            background: #333;
            color: #fff;
        }

        tr:nth-child(even) {
            background: #f2f2f2;
        }

        tr:hover {
            background: #e0e0e0;
        }

        /* Styling for the action links */
        td a {
            color: #333;
            text-decoration: none;
             font-weight: bold;
        }

        td a:hover {
            text-decoration: underline;
        }
    </style>
</head>

<body>
    <h2>Show Doctors</h2>
    <!-- Navigation links to other pages -->
    <nav>
        <a href="showdoc.php">Show Doctors</a> |
        <a href="addoc.php">Add Doctor</a> |
        <a href="searchdoc.php">Search Doctor</a> |
        <a href="deletedoc.php">Delete Doctor</a>
    </nav>
    <br>

    <?php
    // SQL query to select all records from the 'dr' table
    $sql = "SELECT * FROM dr";
    $result = $conn->query($sql);

    // Check if there are any records in the result set
    if ($result->num_rows > 0) {
    ?>
        <!-- Display records in an HTML table -->
        <table border="1"> <!-- Added border for better visibility -->
            <tr>
                <!-- Table headers -->
                <th>ID</th>
                <th>Name</th>
                <th>Email</th>
                <th>Phone</th>
                <th>Address</th>
                <th>Speciality</th>
                <th>Actions</th>
            </tr>
            <?php
            // Loop through each record and display it in a table row
            while ($row = $result->fetch_assoc()) {
            ?>
                <tr>
                    <!-- Display each field of the record -->
                    <td><?php echo htmlspecialchars($row['drid']); ?></td>
                    <td><?php echo htmlspecialchars($row['drname']); ?></td>
                    <td><?php echo htmlspecialchars($row['dremail']); ?></td>
                    <td><?php echo htmlspecialchars($row['drphone']); ?></td>
                    <td><?php echo htmlspecialchars($row['draddress']); ?></td>
                    <td><?php echo htmlspecialchars($row['drSpeciality']); ?></td>
                    <td>
                        <!-- Links for updating and deleting the record -->
                        <a href="updatedoc.php?drid=<?php echo htmlspecialchars($row['drid']); ?>">Update</a> |
                        <a href="deletedoc.php?drid=<?php echo htmlspecialchars($row['drid']); ?>" onclick="return confirm('Are you sure you want to delete this record?');">Delete</a>
                    </td>
                </tr>
            <?php
            }
            ?>
        </table>
    <?php
    } else {
        // Message displayed if no records are found
        echo "No records found.";
    }
    ?>
</body>

</html></pre>
<pre><?php include 'config.php'; ?>

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Update Doctor</title>
    <style>
        /* General styles for the page */
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        /* Container for the main content */
        .container {
            width: 80%;
            margin: auto;
            overflow: hidden;
        }

        /* Styling for the header */
        h2 {
            color: #333;
            text-align: center;
            padding: 20px 0;
        }

        /* Styling for the navigation bar */
        nav {
            background: #333;
            color: #fff;
            padding: 10px 0;
            text-align: center;
        }

        nav a {
            color: #fff;
            text-decoration: none;
            margin: 0 15px;
            font-weight: bold;
        }

        nav a:hover {
            text-decoration: underline;
        }

        /* Styling for the form */
        form {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin: 20px auto;
            max-width: 600px;
        }

        form label {
            display: block;
            margin-bottom: 10px;
            font-weight: bold;
        }

        form input[type="text"],
        form input[type="email"],
        form input[type="submit"],
        form select {
            padding: 10px;
            width: calc(100% - 22px);
            /* Full width minus padding and border */
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
            margin-bottom: 10px;
        }

        form input[type="submit"] {
            background: #333;
            color: #fff;
            border: none;
            cursor: pointer;
        }

        form input[type="submit"]:hover {
            background: #555;
        }

        form input[type="radio"] {
            margin-right: 5px;
        }

        /* Additional styling for the form groups */
        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
        }

        /* Optional: Responsive adjustments */
        @media (max-width: 768px) {
            .container {
                width: 95%;
            }

            form {
                padding: 15px;
            }

            form input[type="text"],
            form input[type="email"],
            form input[type="submit"],
            form select {
                width: calc(100% - 20px);
                /* Full width minus padding */
            }
        }
    </style>
</head>

<body>
    <h2>Update Doctor</h2>
    <!-- Navigation links to other pages -->
    <nav>
        <a href="showdoc.php">Show Doctors</a> |
        <a href="addoc.php">Add Doctor</a> |
        <a href="searchdoc.php">Search Doctor</a> |
        <a href="deletedoc.php">Delete Doctor</a>
    </nav>
    <br>

    <?php
    // Check if the form has been submitted
    if (isset($_POST['update'])) {
        // Get form data
        $drid = $_POST['drid'];
        $drname = $_POST['drname'];
        $dremail = $_POST['dremail'];
        $drphone = $_POST['drphone'];
        $draddress = $_POST['draddress'];
        $drSpeciality = $_POST['drSpeciality'];

        // Prepare SQL update query
        $sql = "UPDATE dr SET drname='$drname', dremail='$dremail', drphone='$drphone', draddress='$draddress', drSpeciality='$drSpeciality' WHERE drid='$drid'";

        // Execute the query and check if it was successful
        if ($conn->query($sql) === TRUE) {
            echo "Doctor updated successfully!";
        } else {
            // Display error message if the query fails
            echo "Error updating record: " . $conn->error;
        }
    }

    // Check if the Doctor ID is provided in the URL
    if (isset($_GET['drid'])) {
        $drid = $_GET['drid'];

        // Prepare SQL query to fetch doctor details
        $sql = "SELECT * FROM dr WHERE drid='$drid'";
        $result = $conn->query($sql);

        // Check if a record was found
        if ($result->num_rows == 1) {
            $row = $result->fetch_assoc();
    ?>

            <!-- Display the form with existing data for editing -->
            <form action="updatedoc.php" method="post">
                <!-- Hidden input to pass the Doctor ID -->
                <input type="hidden" name="drid" value="<?php echo htmlspecialchars($row['drid']); ?>">

                <!-- Input field for Doctor Name -->
                <label for="drname">Name:</label>
                <input type="text" id="drname" name="drname" value="<?php echo htmlspecialchars($row['drname']); ?>" required><br>

                <!-- Input field for Doctor Email -->
                <label for="dremail">Email:</label>
                <input type="email" id="dremail" name="dremail" value="<?php echo htmlspecialchars($row['dremail']); ?>" required><br>

                <!-- Input field for Doctor Phone -->
                <label for="drphone">Phone:</label>
                <input type="text" id="drphone" name="drphone" value="<?php echo htmlspecialchars($row['drphone']); ?>"><br>

                <!-- Input field for Doctor Address -->
                <label for="draddress">Address:</label>
                <input type="text" id="draddress" name="draddress" value="<?php echo htmlspecialchars($row['draddress']); ?>"><br>

                <!-- Radio buttons for Doctor Speciality -->
                <label>Speciality:</label><br>
                <input type="radio" id="anesthesiologists" name="drSpeciality" value="anesthesiologists" <?php echo $row['drSpeciality'] == 'anesthesiologists' ? 'checked' : ''; ?>>
                <label for="anesthesiologists">Anesthesiologists</label><br>

                <input type="radio" id="cardiologists" name="drSpeciality" value="cardiologists" <?php echo $row['drSpeciality'] == 'cardiologists' ? 'checked' : ''; ?>>
                <label for="cardiologists">Cardiologists</label><br>

                <input type="radio" id="criticalcare" name="drSpeciality" value="criticalcare&medicine" <?php echo $row['drSpeciality'] == 'criticalcare&medicine' ? 'checked' : ''; ?>>
                <label for="criticalcare">Critical Care & Medicine</label><br>

                <input type="radio" id="dermatologists" name="drSpeciality" value="dermatologists" <?php echo $row['drSpeciality'] == 'dermatologists' ? 'checked' : ''; ?>>
                <label for="dermatologists">Dermatologists</label><br>

                <input type="radio" id="emergencyspecialists" name="drSpeciality" value="emergencyspecialists" <?php echo $row['drSpeciality'] == 'emergencyspecialists' ? 'checked' : ''; ?>>
                <label for="emergencyspecialists">Emergency Specialists</label><br>

                <!-- Submit button -->
                <input type="submit" name="update" value="Update Doctor">
            </form>

    <?php
        } else {
            // Display message if no record was found for the given ID
            echo "No doctor found with the given ID.";
        }
    } else {
        // Display message if no Doctor ID was provided in the URL
        echo "No Doctor ID provided.";
    }
    ?>

</body>

</html></pre>
