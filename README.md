<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Zaszyfrowany Tablet</title>
<style>
  body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    transition: background-color 0.5s ease;
    background: linear-gradient(145deg, #222, #333);
  }
  .tablet {
    background: linear-gradient(145deg, #222, #333);
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
    width: 300px;
    text-align: center;
    color: #fff;
  }
  .tablet input[type="password"], .tablet button {
    padding: 10px;
    margin-top: 20px;
    margin-bottom: 5px; /* Adjust spacing */
    border-radius: 5px;
    border: none;
    width: calc(80% - 20px); /* Adjust width to compensate for padding */
    background-color: #555;
    color: #fff;
  }
  .tablet button {
    cursor: pointer;
  }
  .hidden {
    display: none;
  }
  .unlocked, .warning-message {
    margin-top: 20px;
    color: #4CAF50;
  }
  .warning-message {
    color: #FFC107;
  }
</style>
</head>
<body>
<div class="tablet">
  <h2>Zaszyfrowany Tablet</h2>
  <input type="password" id="passwordInput" placeholder="Wpisz hasło">
  <button id="unlockButton">Odblokuj</button>
  <div id="content" class="hidden">
    <p class="unlocked">Tablet odblokowany!</p>
    <a href="https://sites.google.com/view/gu-organized-crime-group/organized-crime-group" style="color: #4CAF50;">Nexum Obscurum</a>
  </div>
  <p id="warningMessage" class="warning-message hidden">Wiadomość ostrzegająca została wysłana do właściciela.</p>
</div>
<script>
  let attemptCounter = 0;
  const maxAttempts = 3;
  const lockDuration = 24 * 60 * 60 * 1000; // 24 hours in milliseconds

  function checkPassword() {
    const password = document.getElementById('passwordInput').value;
    if (password === "Fatum") {
      document.getElementById('content').classList.remove('hidden');
      document.body.style.background = "linear-gradient(145deg, #004d40, #009688)";
      document.getElementById('warningMessage').classList.add('hidden');
      attemptCounter = 0; // Reset attempt counter on successful unlock
    } else {
      attemptCounter++;
      if (attemptCounter >= maxAttempts) {
        document.getElementById('unlockButton').disabled = true;
        document.body.style.background = "linear-gradient(145deg, #8B0000, #B22222)";
        document.getElementById('warningMessage').classList.remove('hidden');
        
        setTimeout(() => {
          document.getElementById('unlockButton').disabled = false;
          document.body.style.background = "linear-gradient(145deg, #222, #333)";
          document.getElementById('warningMessage').classList.add('hidden');
          attemptCounter = 0; // Reset attempt counter after lock duration
        }, lockDuration);
        
        alert('Tablet zablokowany na 24 godziny. Wiadomość ostrzegająca została wysłana do właściciela.');
      } else {
        alert('Niepoprawne hasło! Pozostało prób: ' + (maxAttempts - attemptCounter));
      }
    }
  }

  document.getElementById('unlockButton').addEventListener('click', checkPassword);
</script>
</body>
</html>
