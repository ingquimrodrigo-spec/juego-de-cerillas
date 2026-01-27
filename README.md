<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Juego de Organizar Cerillas</title>
  <style>
    .container {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .game-area {
      position: relative;
      width: 400px;
      height: 400px;
      background-color: #f0f0f0;
      border: 1px solid #000;
    }
    .match {
      position: absolute;
      width: 4px;
      height: 60px;
      background-color: #d88f3a;
      cursor: move;
    }
    #message {
      text-align: center;
      margin-top: 20px;
      font-size: 18px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="game-area" id="gameArea">
      <!-- Las cerillas dispuestas en forma de cruz -->
      <div class="match" id="match1" style="top: 150px; left: 170px; transform: rotate(0deg);"></div> <!-- horizontal -->
      <div class="match" id="match2" style="top: 150px; left: 240px; transform: rotate(0deg);"></div> <!-- horizontal -->
      <div class="match" id="match3" style="top: 150px; left: 110px; transform: rotate(0deg);"></div> <!-- horizontal -->
      <div class="match" id="match4" style="top: 80px; left: 170px; transform: rotate(90deg);"></div>  <!-- vertical -->
      <div class="match" id="match5" style="top: 220px; left: 170px; transform: rotate(90deg);"></div> <!-- vertical -->
    </div>
  </div>
  <div id="message">Reorganiza las cerillas para formar una figura</div>

  <script>
    // Hacer que las cerillas se puedan mover
    const matches = document.querySelectorAll('.match');
    matches.forEach(match => {
      match.addEventListener('mousedown', dragStart);
    });

    let selectedMatch = null;

    function dragStart(e) {
      selectedMatch = e.target;
      const offsetX = e.clientX - selectedMatch.getBoundingClientRect().left;
      const offsetY = e.clientY - selectedMatch.getBoundingClientRect().top;

      function dragging(e) {
        selectedMatch.style.left = `${e.clientX - offsetX}px`;
        selectedMatch.style.top = `${e.clientY - offsetY}px`;
      }

      function dragEnd() {
        document.removeEventListener('mousemove', dragging);
        document.removeEventListener('mouseup', dragEnd);
      }

      document.addEventListener('mousemove', dragging);
      document.addEventListener('mouseup', dragEnd);
    }

    // Verificar si las cerillas están en la posición correcta
    function checkWin() {
      const match1 = document.getElementById('match1');
      const match2 = document.getElementById('match2');
      const match3 = document.getElementById('match3');
      const match4 = document.getElementById('match4');
      const match5 = document.getElementById('match5');

      // Chequea si las cerillas están en posiciones cerca de las correctas
      if (Math.abs(parseInt(match1.style.left) - 170) < 10 && Math.abs(parseInt(match1.style.top) - 150) < 10 &&
          Math.abs(parseInt(match2.style.left) - 240) < 10 && Math.abs(parseInt(match2.style.top) - 150) < 10 &&
          Math.abs(parseInt(match3.style.left) - 110) < 10 && Math.abs(parseInt(match3.style.top) - 150) < 10 &&
          Math.abs(parseInt(match4.style.left) - 170) < 10 && Math.abs(parseInt(match4.style.top) - 80) < 10 &&
          Math.abs(parseInt(match5.style.left) - 170) < 10 && Math.abs(parseInt(match5.style.top) - 220) < 10) {
        document.getElementById('message').textContent = '¡Felicidades! Has completado la figura.';
      }
    }

    // Agregar un evento para verificar si las cerillas están en la posición correcta
    setInterval(checkWin, 100);
  </script>
</body>
</html>
