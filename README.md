# moda_
moda
<?php
session_start();
if (isset($_SESSION['user'])) {
    header("Location: home.php");
    exit;
}

include 'app/Conect.php';
include 'app/Acciones.php';

$acciones = new Acciones($Conecta);
$error = '';

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $username = $_POST['username'];
    $password = $_POST['password'];

    $error = $acciones->login($username, $password);
    
    if ($error === null) {
        header("Location: home.php");
        exit;
    }
}
?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Iniciar Sesión</title>
</head>
<body>
    <h2>Iniciar Sesión</h2>
    <form method="POST" action="login.php">
        <label for="username">Usuario:</label>
        <input type="text" name="username" id="username" required>
        <br><br>
        <label for="password">Contraseña:</label>
        <input type="password" name="password" id="password" required>
        <br><br>
        <button type="submit">Ingresar</button>
    </form>

    <!-- Mostrar error si existe -->
    <?php if (!empty($error)): ?>
        <p style="color: red;"><?php echo htmlspecialchars($error); ?></p>
    <?php endif; ?>
</body>
</html>
