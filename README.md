<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cuenta Regresiva</title>
    <link rel="icon" href="corazon.png" type="image/png"> <!-- Ícono del corazón -->
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #ffcccc; /* Fondo rojo más bajo */
            position: relative;
            overflow: hidden;
        }
        .container {
            text-align: center;
            background-color: white; /* Fondo del contenedor blanco */
            color: black; /* Texto negro */
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
            z-index: 1;
            position: relative;
        }
        h1 {
            font-size: 2.5em;
            margin-bottom: 20px;
        }
        .subtitle {
            font-size: 1.5em;
            margin-bottom: 10px;
        }
        .countdown {
            font-size: 2em;
        }
        .countdown div {
            margin: 10px 0;
        }

        /* Estilos para los corazones */
        .heart, .girasol {
            position: absolute;
            width: 50px;
            height: 50px;
            top: 100%;
            animation: float 6s infinite;
            z-index: 0;
        }
        .heart {
            background-color: red;
            transform: rotate(-45deg);
        }
        .heart::before,
        .heart::after {
            content: "";
            position: absolute;
            width: 50px;
            height: 50px;
            background-color: red;
            border-radius: 50%;
        }
        .heart::before {
            top: -25px;
            left: 0;
        }
        .heart::after {
            left: 25px;
            top: 0;
        }

        /* Animación flotante para corazones y girasoles */
        @keyframes float {
            0% {
                transform: translateY(0);
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh);
                opacity: 0;
            }
        }

        /* Diferentes tamaños y posiciones de los corazones */
        .heart:nth-child(2) {
            left: 20%;
            animation-duration: 8s;
        }
        .heart:nth-child(3) {
            left: 50%;
            animation-duration: 10s;
            animation-delay: 2s;
        }
        .heart:nth-child(4) {
            left: 80%;
            animation-duration: 7s;
            animation-delay: 1s;
        }

        /* Girasoles animados */
        .girasol {
            width: 80px;
            height: 80px;
            background-image: url('https://cdn.pixabay.com/photo/2016/08/09/21/03/sunflower-1588336_960_720.png');
            background-size: cover;
        }
        .girasol:nth-child(5) {
            left: 10%;
            animation-duration: 9s;
            animation-delay: 2s;
        }
        .girasol:nth-child(6) {
            left: 70%;
            animation-duration: 12s;
            animation-delay: 4s;
        }

    </style>
</head>
<body>

<!-- Corazones flotantes -->
<div class="heart"></div>
<div class="heart"></div>
<div class="heart"></div>
<div class="heart"></div>

<!-- Girasoles flotantes -->
<div class="girasol"></div>
<div class="girasol"></div>

<div class="container">
    <div class="subtitle">Joss & Sebas</div> <!-- Texto agregado "Joss & Sebas" -->
    <h1>Falta para nuestro primer mes</h1>
    <div class="countdown">
        <div id="dias">0</div>
        <div id="horas">0</div>
        <div id="minutos">0</div>
        <div id="segundos">0</div>
    </div>
</div>

<script>
    // Verificar si ya hay una fecha límite guardada en localStorage
    let fechaLimite = localStorage.getItem('fechaLimite');

    // Si no existe, calcularla (4 días desde ahora) y guardarla en localStorage
    if (!fechaLimite) {
        fechaLimite = new Date().getTime() + (4 * 24 * 60 * 60 * 1000); // 4 días en milisegundos
        localStorage.setItem('fechaLimite', fechaLimite);
    }

    // Convertir la fecha de límite a número (milisegundos)
    fechaLimite = parseInt(fechaLimite);

    // Actualizar la cuenta regresiva cada segundo
    const intervalo = setInterval(() => {
        const ahora = new Date().getTime();
        const diferencia = fechaLimite - ahora;

        // Cálculo de días, horas, minutos y segundos
        const dias = Math.floor(diferencia / (1000 * 60 * 60 * 24));
        const horas = Math.floor((diferencia % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
        const minutos = Math.floor((diferencia % (1000 * 60 * 60)) / (1000 * 60));
        const segundos = Math.floor((diferencia % (1000 * 60)) / 1000);

        // Mostrar el resultado en los respectivos elementos HTML
        document.getElementById("dias").innerHTML = dias + " Días";
        document.getElementById("horas").innerHTML = horas + " Horas";
        document.getElementById("minutos").innerHTML = minutos + " Minutos";
        document.getElementById("segundos").innerHTML = segundos + " Segundos";

        // Si la cuenta ha llegado a 0, detener el intervalo y borrar la fecha de localStorage
        if (diferencia < 0) {
            clearInterval(intervalo);
            document.querySelector('.countdown').innerHTML = "¡Tiempo terminado!";
            localStorage.removeItem('fechaLimite');
        }
    }, 1000);
</script>

</body>
</html>
