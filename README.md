<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI Voice Assistant - Alexa</title>
  <style>
    /* ====== BASIC PAGE STYLING ====== */
    body {
      background: linear-gradient(135deg, #2b1055, #7597de);
      color: white;
      font-family: "Poppins", sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }

    h1 {
      font-size: 2.5em;
      margin-bottom: 10px;
      text-shadow: 2px 2px 8px rgba(0,0,0,0.4);
    }

    .assistant-container {
      background: rgba(255, 255, 255, 0.1);
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.3);
      text-align: center;
      width: 350px;
      max-width: 90%;
    }

    .output {
      background: rgba(255,255,255,0.2);
      padding: 10px;
      border-radius: 10px;
      height: 100px;
      margin-top: 20px;
      overflow-y: auto;
      font-size: 1em;
      text-align: left;
    }

    button {
      margin-top: 20px;
      background-color: #00b4d8;
      color: white;
      border: none;
      border-radius: 50%;
      width: 70px;
      height: 70px;
      font-size: 30px;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 0 15px rgba(0,180,216,0.8);
    }

    button:hover {
      background-color: #0077b6;
      transform: scale(1.1);
    }

    .listening {
      animation: pulse 1s infinite;
    }

    @keyframes pulse {
      0% { box-shadow: 0 0 5px #90e0ef; }
      50% { box-shadow: 0 0 25px #00b4d8; }
      100% { box-shadow: 0 0 5px #90e0ef; }
    }

    footer {
      position: absolute;
      bottom: 15px;
      font-size: 0.8em;
      color: #eee;
    }
  </style>
</head>
<body>
  <h1>Alexa Voice Assistant</h1>
  <div class="assistant-container">
    <p><strong>Click the mic and speak:</strong></p>
    <button id="micBtn">🎤</button>
    <div class="output" id="output">Say something...</div>
  </div>
  <footer>Made with ❤️ using HTML, CSS & JavaScript</footer>

  <script>
    // ====== SPEECH RECOGNITION SETUP ======
    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    const recognition = new SpeechRecognition();
    const output = document.getElementById('output');
    const micBtn = document.getElementById('micBtn');

    recognition.continuous = false;
    recognition.lang = 'en-US';
    recognition.interimResults = false;

    // ====== START LISTENING ======
    micBtn.addEventListener('click', () => {
      recognition.start();
      micBtn.classList.add('listening');
      speak("Listening...");
    });

    recognition.onresult = (event) => {
      const transcript = event.results[0][0].transcript.toLowerCase();
      output.innerHTML = "<b>You said:</b> " + transcript;
      processCommand(transcript);
    };

    recognition.onend = () => {
      micBtn.classList.remove('listening');
    };

    // ====== SPEECH FUNCTION ======
    function speak(text) {
      const speech = new SpeechSynthesisUtterance(text);
      speech.lang = 'en-US';
      speech.pitch = 1;
      speech.rate = 1;
      window.speechSynthesis.speak(speech);
      output.innerHTML += `<br><b>Alexa:</b> ${text}`;
    }

    // ====== COMMAND HANDLER ======
    function processCommand(command) {
      console.log('Command:', command);

      if (command.includes('hello')) {
        speak("Hello there! How can I help you today?");
      }
      else if (command.includes('your name')) {
        speak("I am your voice assistant, Alexa!");
      }
      else if (command.includes('time')) {
        const time = new Date().toLocaleTimeString();
        speak(`The current time is ${time}`);
      }
      else if (command.includes('date')) {
        const date = new Date().toDateString();
        speak(`Today’s date is ${date}`);
      }
      else if (command.includes('open google')) {
        speak("Opening Google");
        window.open('https://www.google.com', '_blank');
      }
      else if (command.includes('open youtube')) {
        speak("Opening YouTube");
        window.open('https://www.youtube.com', '_blank');
      }
      else if (command.includes('open facebook')) {
        speak("Opening Facebook");
        window.open('https://www.facebook.com', '_blank');
      }
      else if (command.includes('how are you')) {
        speak("I’m doing great! Thanks for asking. How are you?");
      }
      else if (command.includes('thank you')) {
        speak("You’re welcome! Happy to help.");
      }
      else if (command.includes('bye')) {
        speak("Goodbye! Have a great day!");
      }
      else {
        speak("Sorry, I didn’t understand that. Please try again.");
      }
    }
  </script>
</body>
</html>
