# Habana-Brown-
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Habanabrown</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Bienvenido a Habanabrown</h1>
    </header>
    <main>
        <section id="imagen-ia">
            <h2>Generador de Imágenes</h2>
            <input type="text" id="prompt" placeholder="Describe la imagen que deseas generar">
            <button onclick="generarImagen()">Generar Imagen</button>
            <img id="imagen-generada" src="" alt="Imagen Generada">
        </section>
        <section id="noticias">
            <h2>Noticias</h2>
            <div id="noticias-contenido"></div>
        </section>
    </main>
    <script src="scripts.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
}

header {
    background-color: #8B4513; /* Color marrón habana */
    color: white;
    padding: 1em;
    text-align: center;
}

main {
    padding: 2em;
}

section {
    margin-bottom: 2em;
}

#imagen-generada {
    max-width: 100%;
    margin-top: 1em;
}
async function generarImagen() {
    const prompt = document.getElementById('prompt').value;
    const apiKey = 'TU_API_KEY'; // Reemplaza con tu clave de API
    const response = await fetch('https://api.generadordeimagenes.com/generate', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${apiKey}`
        },
        body: JSON.stringify({ prompt })
    });

    const data = await response.json();
    document.getElementById('imagen-generada').src = data.imageUrl;
}

async function cargarNoticias() {
    const response = await fetch('https://api.noticias.com/latest?categories=cine,musica,videojuegos');
    const data = await response.json();
    const noticiasContenido = document.getElementById('noticias-contenido');
    noticiasContenido.innerHTML = data.articles.map(article => `
        <div>
            <h3>${article.title}</h3>
            <p>${article.description}</p>
        </div>
    `).join('');
}

// Cargar noticias al cargar la página
cargarNoticias();
