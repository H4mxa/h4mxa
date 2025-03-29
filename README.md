<div id="terminal">
  <div id="output"></div>
  <div class="input-line">
    <span class="prompt">>> </span><input type="text" id="input" autocomplete="off" spellcheck="false">
  </div>
</div>

<script>
  const input = document.getElementById('input');
  const output = document.getElementById('output');

  const commands = {
    'help': 'Display available commands',
    'whoami': 'Display profile information',
    'projects': 'Display featured projects',
    'skills': 'Display technical skills',
    'clear': 'Clear the terminal',
    'credits': 'Show the credits',
    'neofetch': 'Display system information (simulated)',
    'echo': 'Display text',
    'ls': 'List files (simulated)',
  };

  function typeWriter(text, element, speed = 20) {
    return new Promise(resolve => {
      let i = 0;
      const interval = setInterval(() => {
        if (i < text.length) {
          element.innerHTML += text.charAt(i);
          i++;
        } else {
          clearInterval(interval);
          resolve();
        }
      }, speed);
    });
  }

  function executeCommand(command) {
    const commandParts = command.split(' ');
    const baseCommand = commandParts[0];
    const args = commandParts.slice(1);

    switch (baseCommand) {
      case 'help':
        output.innerHTML += '<div class="output-line">Available commands:</div>';
        for (const cmd in commands) {
          output.innerHTML += `<div class="output-line"><span class="command">${cmd}</span>: ${commands[cmd]}</div>`;
        }
        break;
      case 'whoami':
        typeWriter('H4mxa - A passionate developer with a love for creative coding.', output).then(() => {
          output.innerHTML += '<div class="output-line">[Insert Avatar/Name SVG Here]</div>';
        });
        break;
      case 'projects':
        output.innerHTML += '<div class="output-line">Loading projects...</div>';
        setTimeout(() => {
          output.innerHTML += '<div class="output-line">...</div>';
        }, 1000);
        break;
      case 'skills':
        output.innerHTML += '<div class="output-line">Skills:</div>';
        const skills = ['Typescript', 'Python', 'Rust'];
        skills.forEach(skill => output.innerHTML += `<div class="output-line">- ${skill}</div>`);
        break;
      case 'clear':
        output.innerHTML = '';
        break;
      case 'credits':
        output.innerHTML += '<div class="output-line">Created by: H4mxa</div>';
        output.innerHTML += '<div class="output-line">Inspired by: Cool Open-Source Projects</div>';
        break;
      case 'neofetch':
        output.innerHTML += '<div class="output-line">System: H4mxa\'s Laptop</div>';
        output.innerHTML += '<div class="output-line">OS: Arch Linux (Simulated)</div>';
        output.innerHTML += '<div class="output-line">Shell: Zsh</div>';
        output.innerHTML += '<div class="output-line">CPU: Intel i7 (Simulated)</div>';
        output.innerHTML += '<div class="output-line">Memory: 16GB (Simulated)</div>';
        break;
      case 'echo':
        const textToEcho = args.join(' ');
        output.innerHTML += `<div class="output-line">${textToEcho}</div>`;
        break;
      case 'ls':
        output.innerHTML += '<div class="output-line">README.md  projects/  skills/  (Simulated)</div>';
        break;
      default:
        output.innerHTML += `<div class="output-line">Command not found: ${baseCommand}</div>`;
    }
  }

  input.addEventListener('keydown', (event) => {
    if (event.key === 'Enter') {
      const command = input.value.trim().toLowerCase();
      output.innerHTML += `<div class="output-line"><span class="prompt">>> </span>${command}</div>`;
      input.value = '';
      executeCommand(command);
    }
  });

  typeWriter('Welcome to H4mxa\'s GitHub Profile!', output, 30).then(()=> {
    setTimeout(()=> {
      output.innerHTML += `<div class="output-line">Type "help" to see available commands.</div>`;
    }, 500);
  });
</script>

<style>
  #terminal {
    background-color: #000;
    color: #eee;
    font-family: monospace;
    padding: 20px;
    border-radius: 10px;
    border: 2px solid #0f0;
    box-shadow: 0 4px 8px rgba(0, 255, 0, 0.3);
    max-width: 800px;
    margin: 0 auto;
    overflow-x: auto;
    position: relative;
    min-height: 200px;
  }

  #output {
    margin-bottom: 30px;
  }

  .prompt {
    color: #00ff00;
  }

  .input-line {
    display: flex;
    position: absolute;
    bottom: 10px;
    left: 10px;
    right: 10px;
  }

  input {
    background-color: transparent;
    border: none;
    color: #eee;
    flex-grow: 1;
    font-family: monospace;
    outline: none;
    padding: 0;
    margin-left: 5px;
  }

  .output-line {
    margin-bottom: 5px;
    white-space: pre-wrap;
  }

  .command {
    color: #00ffff;
  }
</style>
