<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Álbum de Krisma</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #fdf4ff;
            color: #4a235a;
            text-align: center;
        }

        header {
            background-color: #9b59b6;
            color: white;
            padding: 20px;
            font-size: 2em;
        }

        .login {
            margin: 50px auto;
            max-width: 400px;
            background: #f9ebff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .login input[type="password"],
        .login input[type="text"],
        .login button {
            width: 100%;
            margin: 10px 0;
            padding: 10px;
            border: none;
            border-radius: 4px;
            font-size: 1em;
        }

        .show-password {
            text-align: left;
            margin-bottom: 10px;
        }

        .login button {
            background-color: #8e44ad;
            color: white;
            cursor: pointer;
        }

        .login button:hover {
            background-color: #732d91;
        }

        .album {
            display: none;
            animation: fadeIn 1s ease-in-out;
        }

        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
            padding: 20px;
        }

        .gallery img {
            width: 100%;
            border: 5px solid #8e44ad;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
        }

        .gallery img:hover {
            transform: scale(1.1);
        }

        .download-button {
            margin-top: 10px;
            display: inline-block;
            padding: 10px 20px;
            background-color: #8e44ad;
            color: white;
            text-decoration: none;
            border-radius: 4px;
            font-size: 0.9em;
            transition: background-color 0.3s ease;
        }

        .download-button:hover {
            background-color: #732d91;
        }

        .like-button {
            margin-top: 10px;
            display: inline-block;
            padding: 10px 20px;
            background-color: #ff5733;
            color: white;
            text-decoration: none;
            border-radius: 4px;
            font-size: 0.9em;
            transition: background-color 0.3s ease;
            cursor: pointer;
        }

        .like-button:hover {
            background-color: #c43d22;
        }

        .comment-section {
            margin-top: 20px;
            text-align: left;
            padding: 10px;
            border-top: 2px solid #8e44ad;
        }

        .comment-section textarea {
            width: 100%;
            padding: 10px;
            border-radius: 4px;
            border: 1px solid #8e44ad;
            margin-bottom: 10px;
        }

        .comment-section button {
            background-color: #8e44ad;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        .comment-section button:hover {
            background-color: #732d91;
        }

        .comments {
            margin-top: 10px;
            background: #f9ebff;
            padding: 10px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .comments p {
            margin: 5px 0;
            font-size: 0.9em;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
    </style>
</head>
<body>
    <header>
        Álbum de Krisma
    </header>

    <div class="login" id="login">
        <h2>Inicia sesión</h2>
        <p>Ingresa la contraseña o palabra secreta:</p>
        <input type="password" id="password" placeholder="Contraseña o palabra secreta">
        <div class="show-password">
            <input type="checkbox" id="toggle-password"> Mostrar contraseña
        </div>
        <button onclick="checkPassword()">Entrar</button>
        <p id="error-message" style="color: red; display: none;">Contraseña incorrecta</p>
    </div>

    <div class="album" id="album">
        <header>Mis Recuerdos</header>
        <div class="gallery" id="gallery">
            <div>
                <img src="https://via.placeholder.com/200" alt="Foto 1">
                <a class="download-button" href="https://via.placeholder.com/200" download="foto1.jpg">Descargar</a>
                <button class="like-button" onclick="likePhoto(this)">❤️ Me gusta</button>
            </div>
            <div>
                <img src="https://via.placeholder.com/200" alt="Foto 2">
                <a class="download-button" href="https://via.placeholder.com/200" download="foto2.jpg">Descargar</a>
                <button class="like-button" onclick="likePhoto(this)">❤️ Me gusta</button>
            </div>
            <div>
                <img src="https://via.placeholder.com/200" alt="Foto 3">
                <a class="download-button" href="https://via.placeholder.com/200" download="foto3.jpg">Descargar</a>
                <button class="like-button" onclick="likePhoto(this)">❤️ Me gusta</button>
            </div>
        </div>
        <div class="comment-section">
            <h3>Deja un comentario:</h3>
            <textarea id="comment-input" placeholder="Escribe un comentario..."></textarea>
            <button onclick="addComment()">Enviar</button>
            <div id="comments" class="comments">
                <!-- Los comentarios aparecerán aquí -->
            </div>
        </div>
    </div>

    <script>
        const correctPassword = "Krisma";
        const secretWord = "gatitos negros";

        function checkPassword() {
            const input = document.getElementById("password").value.trim();
            const login = document.getElementById("login");
            const album = document.getElementById("album");
            const errorMessage = document.getElementById("error-message");

            if (input.toLowerCase() === correctPassword.toLowerCase() || input.toLowerCase() === secretWord.toLowerCase()) {
                login.style.display = "none";
                album.style.display = "block";
            } else {
                errorMessage.style.display = "block";
            }
        }

        function likePhoto(button) {
            const likes = button.getAttribute("data-likes") || 0;
            const newLikes = parseInt(likes) + 1;
            button.setAttribute("data-likes", newLikes);
            button.innerText = `❤️ ${newLikes} Me gusta`;
        }

        function addComment() {
            const commentInput = document.getElementById("comment-input");
            const commentText = commentInput.value.trim();
            const commentsContainer = document.getElementById("comments");

            if (commentText) {
                const commentElement = document.createElement("p
