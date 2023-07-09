# ChifoumieV2

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chifoumie</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">
    

</head>
<body>
    <nav>
        <ul>
            <li><a href="application.html">Accueil</a></li>
            <li><a href="asitepresentation.html">Exercice</a></li>
        </ul>
    </nav>
    <h1 class="title">Pierre - Feuille - Ciseaux</h1>
    <div class="scoreboard">
        <span class="player-score"><i class="fas fa-hand-rock"></i> <span id="joueur-score">0</span></span>
        <span class="vs">VS</span>
        <span class="computer-score"><i class="fas fa-hand-rock"></i> <span id="ordinateur-score">0</span></span>
    </div>
    <div class="result">
        <div class="message" id="resultat"></div>
        <div class="play-again" onclick="rejouer()">Rejouer</div>
    </div>
    <div id="actions">
        <button onclick="jouer('rock')"><i class="fas fa-hand-rock icon rock"></i></button>
        <button onclick="jouer('paper')"><i class="fas fa-hand-paper icon paper"></i></button>
        <button onclick="jouer('scissors')"><i class="fas fa-hand-scissors icon scissors"></i></button>
    </div>
    
 
    
    <script>
        let joueurScore = 0;
        let ordinateurScore = 0;
    
        function jouer(choixJoueur) {
            const choixOrdinateur = genererChoixOrdinateur();
    
            const resultat = comparerChoix(choixJoueur, choixOrdinateur);
    
            afficherResultat(resultat);
    
            if (resultat === 'joueur') {
                joueurScore++;
            } else if (resultat === 'ordinateur') {
                ordinateurScore++;
            }
    
            miseAJourScore();
    
            if (joueurScore === 5 || ordinateurScore === 5) {
                afficherGagnant();
                desactiverBoutons();
            }
        }
    
        function genererChoixOrdinateur() {
            const choixAleatoire = Math.floor(Math.random() * 3);
            if (choixAleatoire === 0) {
                return 'rock';
            } else if (choixAleatoire === 1) {
                return 'paper';
            } else {
                return 'scissors';
            }
        }
    
        function comparerChoix(choixJoueur, choixOrdinateur) {
            if (
                (choixJoueur === 'rock' && choixOrdinateur === 'scissors') ||
                (choixJoueur === 'paper' && choixOrdinateur === 'rock') ||
                (choixJoueur === 'scissors' && choixOrdinateur === 'paper')
            ) {
                return 'joueur';
            } else if (choixJoueur === choixOrdinateur) {
                return 'égalité';
            } else {
                return 'ordinateur';
            }
        }
    
        function afficherResultat(resultat) {
            const resultatDiv = document.getElementById('resultat');
            if (resultat === 'joueur') {
                resultatDiv.innerHTML = '<span class="message win">Vous avez gagné !</span>';
            } else if (resultat === 'égalité') {
                resultatDiv.innerHTML = '<span class="message draw">Égalité !</span>';
            } else {
                resultatDiv.innerHTML = '<span class="message lose">L\'ordinateur a gagné !</span>';
            }
        }
    
        function miseAJourScore() {
            const joueurScoreSpan = document.getElementById('joueur-score');
            const ordinateurScoreSpan = document.getElementById('ordinateur-score');
    
            joueurScoreSpan.textContent = joueurScore;
            ordinateurScoreSpan.textContent = ordinateurScore;
        }
    
        function afficherGagnant() {
            const resultatDiv = document.getElementById('resultat');
            if (joueurScore > ordinateurScore) {
                resultatDiv.innerHTML = '<span class="message win">Vous avez gagné la partie !</span>';
            } else {
                resultatDiv.innerHTML = '<span class="message lose">L\'ordinateur a gagné la partie !</span>';
            }
        }
    
        function desactiverBoutons() {
            const boutons = document.querySelectorAll('#actions button');
            boutons.forEach(function (bouton) {
                bouton.disabled = true;
            });
        }
    
        function rejouer() {
            joueurScore = 0;
            ordinateurScore = 0;
            miseAJourScore();
            document.getElementById('resultat').textContent = '';
            const boutons = document.querySelectorAll('#actions button');
            boutons.forEach(function (bouton) {
                bouton.disabled = false;
            });
        }
    </script>
</body>
</html>
<style>
    body {
        font-family: Arial, sans-serif;
        text-align: center;
        background-color: #292f3f;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        flex-direction: column;
        margin: 0;
        padding: 0;
    }

    h1 {
        color: #292f3f;
        font-size: 36px;
        margin-bottom: 20px;
    }

    #score {
        font-size: 24px;
        margin-bottom: 20px;
        color: #292f3f;
    }

    #resultat {
        font-size: 36px;
        font-weight: bold;
        margin-bottom: 40px;
        color: #292f3f;
    }

    #actions {
        display: flex;
        justify-content: center;
        margin-bottom: 40px;
    }

    button {
        padding: 10px 20px;
        margin: 0 10px;
        font-size: 20px;
        background-color: #ffffff;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }

    button:hover {
        background-color: #ebebeb;
    }

    #resultat {
        font-size: 24px;
        margin-top: 20px;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }

    #resultat span {
        margin-bottom: 10px;
    }

    #resultat span.green {
        color: green;
    }

    #resultat span.red {
        color: red;
    }

    nav {
        background-color: #292f3f;
        padding: 10px;
        position: absolute;
        top: 10px;
        left: 10px;
        right: 10px;
        display: flex;
        justify-content: center;
        z-index: 1;
    }

    nav ul {
        list-style-type: none;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
    }

    nav li {
        margin: 0 10px;
    }

    nav a {
        color: #fff;
        text-decoration: none;
        font-size: 18px;
    }

    nav a:hover {
        color: #007bff;
    }

    .icon {
        font-size: 60px;
        margin-bottom: 10px;
    }

    .rock {
        color: #8b8b8b;
    }

    .paper {
        color: #f9d85b;
    }

    .scissors {
        color: #dc3545;
    }

    .vs {
        font-size: 36px;
        margin-bottom: 20px;
        color: #292f3f;
    }

    .scoreboard {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 300px;
        margin: 0 auto 40px;
        padding: 10px;
        background-color: #fff;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        border-radius: 5px;
    }

    .scoreboard .player-score,
    .scoreboard .computer-score {
        font-size: 24px;
    }

    .scoreboard .player-score::before,
    .scoreboard .computer-score::before {
        font-family: 'Font Awesome 5 Free';
        font-weight: 900;
        margin-right: 5px;
    }

    .scoreboard .player-score::before {
        content: "\f007";
        color: #007bff;
    }

    .scoreboard .computer-score::before {
        content: "\f544";
        color: #dc3545;
    }

    .result {
        font-size: 24px;
        margin-bottom: 40px;
        color: #292f3f;
    }

    .result .message {
        margin-bottom: 10px;
    }

    .result .message.win {
        color: green;
    }

    .result .message.lose {
        color: red;
    }

    .result .message.draw {
        color: #d1d3d8;
    }

    .result .play-again {
        font-size: 18px;
        color: #007bff;
        text-decoration: underline;
        cursor: pointer;
    }

    @media screen and (max-width: 600px) {
        h1 {
            font-size: 28px;
        }

        .icon {
            font-size: 40px;
        }

        .scoreboard {
            font-size: 18px;
            width: 250px;
        }

        .scoreboard .player-score,
        .scoreboard .computer-score {
            font-size: 20px;
        }

        .result {
            font-size: 20px;
        }

        .result .play-again {
            font-size: 16px;
        }
    }
    .title{
        color: white;
    }
</style>
