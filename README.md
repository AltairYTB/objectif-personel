<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Suivi des Objectifs Personnels</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* Global Styles */
        body {
            font-family: 'Roboto', sans-serif;
            background: #f4f7fc;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            flex-direction: column;
        }

        .container {
            background: #fff;
            width: 90%;
            max-width: 900px;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
        }

        h1 {
            font-size: 2.5rem;
            color: #333;
            text-align: center;
            margin-bottom: 30px;
        }

        .goal-container {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 20px;
            margin-top: 30px;
        }

        .goal-card {
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            color: #333;  /* Police noire */
        }

        .goal-card h3 {
            font-size: 1.5rem;
            margin-bottom: 10px;
        }

        /* Progress Bar */
        .progress-bar {
            background: #e0e0e0;
            border-radius: 10px;
            height: 20px;
            margin-bottom: 10px;
            width: 100%;
        }

        .progress-bar-fill {
            height: 100%;
            border-radius: 10px;
        }

        /* Button */
        .button {
            display: block;
            width: 100%;
            padding: 10px;
            font-size: 1.1rem;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: background-color 0.3s;
            background-color: #28a745;  /* Green background for the button */
            color: black;  /* Force the text to be black */
        }

        .button:hover {
            opacity: 0.9;
        }

        /* Add New Goal Button */
        .add-goal-btn {
            background: #007bff;
            padding: 12px 24px;
            font-size: 1.2rem;
            border-radius: 10px;
            color: white;
            margin-top: 30px;
            cursor: pointer;
        }

        .color-buttons {
            display: flex;
            justify-content: center;
            margin-top: 20px;
        }

        .color-button {
            margin: 0 10px;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
        }

        /* Color Options */
        .green { background-color: #28a745; }
        .pink { background-color: #e83e8c; }
        .red { background-color: #dc3545; }

        /* Responsive Design */
        @media screen and (max-width: 768px) {
            .goal-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Suivi de mes Objectifs Personnels</h1>
        <div class="goal-container" id="goalContainer">
            <!-- Les objectifs seront insérés ici -->
        </div>
        <button class="add-goal-btn" onclick="addGoal()">Ajouter un objectif</button>

        <div class="color-buttons">
            <div class="color-button green" onclick="setColor('green')"></div>
            <div class="color-button pink" onclick="setColor('pink')"></div>
            <div class="color-button red" onclick="setColor('red')"></div>
        </div>
    </div>

    <script>
        // Tableau vide au départ
        let goals = [];
        let currentColor = 'green'; // Couleur par défaut

        // Fonction pour afficher les objectifs
        function renderGoals() {
            const goalContainer = document.getElementById('goalContainer');
            goalContainer.innerHTML = '';

            if (goals.length === 0) {
                goalContainer.innerHTML = '<p style="text-align: center; font-size: 1.2rem;">Aucun objectif inscrit pour le moment. Ajoutez un objectif !</p>';
            }

            goals.forEach(goal => {
                const goalCard = document.createElement('div');
                goalCard.classList.add('goal-card');

                // Applique la couleur sélectionnée
                goalCard.classList.add(currentColor);

                goalCard.innerHTML = `
                    <h3>${goal.title}</h3>
                    <div class="progress-bar">
                        <div class="progress-bar-fill" style="width: ${goal.progress}%"></div>
                    </div>
                    <button class="button" onclick="updateProgress('${goal.title}')">Mettre à jour la progression</button>
                `;

                goalContainer.appendChild(goalCard);
            });
        }

        // Fonction pour ajouter un nouvel objectif
        function addGoal() {
            const title = prompt("Entrez le titre de votre objectif:");
            if (title) {
                goals.push({ title, progress: 0 });
                renderGoals();
            }
        }

        // Fonction pour mettre à jour la progression d'un objectif
        function updateProgress(goalTitle) {
            const goal = goals.find(g => g.title === goalTitle);
            if (goal) {
                const newProgress = prompt(`Progrès actuel pour "${goal.title}" (0 à 100):`);
                const progressValue = parseInt(newProgress, 10);

                if (progressValue >= 0 && progressValue <= 100) {
                    goal.progress = progressValue;
                    renderGoals();
                } else {
                    alert("Veuillez entrer une valeur entre 0 et 100.");
                }
            }
        }

        // Fonction pour changer la couleur des objectifs
        function setColor(color) {
            currentColor = color;
            renderGoals(); // Re-render les objectifs avec la nouvelle couleur
        }

        // Initialisation
        renderGoals();
    </script>

</body>
</html>
