# Re-create and prepare the ZIP file with the project structure for the user to download again.

import zipfile
import os

# Define folder structure and placeholder files
base_dir = "/mnt/data/game_project"
os.makedirs(base_dir, exist_ok=True)

# Recreate HTML structure
html_content = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juego Interactivo</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #fce4ec;
            color: #880e4f;
        }
        .welcome, .reasons, .final {
            margin-top: 20px;
        }
        .reason {
            display: none;
        }
    </style>
</head>
<body>
    <div class="welcome">
        <h1>Bienvenida, Jazzmin</h1>
        <p>Prepárate para un recorrido por nuestro amor.</p>
        <audio controls autoplay>
            <source src="music/si_no_estas.mp3" type="audio/mpeg">
            Tu navegador no soporta el elemento de audio.
        </audio>
    </div>
    <div class="reasons">
        <h2>30 Razones</h2>
        <p>Haz clic para descubrir cada razón:</p>
        <ul>
            <li><button onclick="showReason(1)">Razón 1</button></li>
            <li><button onclick="showReason(2)">Razón 2</button></li>
            <!-- Add more buttons here -->
        </ul>
        <div id="reason-1" class="reason">Porque eres la razón de mi sonrisa cada día.</div>
        <div id="reason-2" class="reason">Porque tu risa ilumina mi vida.</div>
    </div>
    <div class="final">
        <h2>Acta de Matrimonio</h2>
        <p>Gracias por todo este amor.</p>
        <audio controls>
            <source src="music/mi_persona_favorita.mp3" type="audio/mpeg">
            Tu navegador no soporta el elemento de audio.
        </audio>
        <img src="images/acta_matrimonio.png" alt="Acta de Matrimonio">
    </div>
    <script>
        function showReason(id) {
            document.querySelectorAll('.reason').forEach(el => el.style.display = 'none');
            document.getElementById(`reason-${id}`).style.display = 'block';
        }
    </script>
</body>
</html>
"""

with open(f"{base_dir}/index.html", "w") as f:
    f.write(html_content)

# Create folders for images and music
os.makedirs(f"{base_dir}/images", exist_ok=True)
os.makedirs(f"{base_dir}/music", exist_ok=True)

# Placeholder files
with open(f"{base_dir}/music/si_no_estas.mp3", "wb") as f:
    f.write(b"")  # Placeholder
with open(f"{base_dir}/music/mi_persona_favorita.mp3", "wb") as f:
    f.write(b"")  # Placeholder
with open(f"{base_dir}/images/acta_matrimonio.png", "wb") as f:
    f.write(b"")  # Placeholder

# Create ZIP file
zip_path = "/mnt/data/game_project.zip"
with zipfile.ZipFile(zip_path, "w") as zipf:
    for root, dirs, files in os.walk(base_dir):
        for file in files:
            zipf.write(os.path.join(root, file), os.path.relpath(os.path.join(root, file), base_dir))

zip_path
