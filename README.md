<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Tech Savvy Guy's Digital Hub</title>
  <style>
    /* Desktop Setup */
    body {
      background-image: url('bg.jpg');
      background-color: #0b457f;
      background-size: cover;
      background-position: center;
      background-attachment: fixed;
      font-family: "Segoe UI", Tahoma, Arial, sans-serif;
      margin: 0;
      padding: 50px 20px;
      display: flex;
      justify-content: center;
      min-height: 100vh;
      overflow-x: hidden;
    }

    /* YOUR EXACT MAIN WINDOW (Windows 7 Basic) */
    .win7-window {
      width: 100%;
      max-width: 550px; 
      background-color: #f0f0f0; 
      border: 1px solid #7592b0;
      border-radius: 6px 6px 0 0;
      box-shadow: 0px 5px 15px rgba(0,0,0,0.5);
      overflow: hidden;
      height: fit-content;
      z-index: 1;
      transition: all 0.2s ease-in-out;
    }

    /* Maximize Logic */
    .maximized {
      max-width: 100% !important;
      width: 100vw !important;
      height: calc(100vh - 40px) !important; /* Leaves room for the taskbar */
      position: fixed; 
      top: 0; 
      left: 0; 
      z-index: 9999;
      border-radius: 0; 
      margin: 0;
    }
    
    .title-bar {
      background: linear-gradient(to bottom, #d9eafd 0%, #b8d2eb 100%);
      padding: 4px 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      color: #000;
      font-size: 12px;
      border-bottom: 1px solid #ffffff;
      text-shadow: 1px 1px 0px rgba(255, 255, 255, 0.8);
    }
    
    .controls { display: flex; gap: 1px; }
    .control-btn { height: 20px; width: 28px; border: 1px solid #aeb2b9; border-radius: 3px; background: linear-gradient(to bottom, #f2f5f9 0%, #d4dbe4 100%); cursor: pointer; }
    .close { width: 45px; background: linear-gradient(to bottom, #e4a29a 0%, #c64b3c 100%); border-color: #9b392e; color: white; font-weight: bold; }
    
    .window-content { background-color: #ffffff; border: 1px solid #abadb3; margin: 10px; padding: 20px; color: #000; font-size: 13px; }
    .window-content h1 { font-size: 22px; color: #003399; margin-top: 0; margin-bottom: 15px; border-bottom: 1px solid #eee; padding-bottom: 8px; }
    .window-content p { line-height: 1.5; margin-bottom: 15px; }
    
    .win7-button { display: block; width: 90%; text-align: center; text-decoration: none; color: #000; padding: 8px 10px; margin: 12px auto; background: linear-gradient(to bottom, #f2f2f2 0%, #e1e1e1 100%); border: 1px solid #abadb3; border-radius: 3px; }
    .win7-button:hover { background: linear-gradient(to bottom, #eaf6fd 0%, #d9f0fc 100%); border: 1px solid #3c7fb1; }
    .win7-text-display { display: block; width: 90%; text-align: center; padding: 8px 10px; margin: 12px auto; background: #fdfdfd; border: 1px solid #abadb3; border-radius: 3px; user-select: all; }
    
    hr { border: 0; height: 1px; background: #dfdfdf; margin: 20px 0; }
    .center-img { display: block; margin: 10px auto; max-width: 100px; }

    /* TASKBAR (Windows 7 Basic) */
    .taskbar {
      position: fixed; bottom: 0; left: 0; width: 100%; height: 40px;
      background: linear-gradient(to bottom, rgba(217,234,253,0.85) 0%, rgba(184,210,235,0.85) 100%);
      border-top: 1px solid #ffffff; display: flex; align-items: center; padding: 0 10px; box-sizing: border-box; z-index: 10001; backdrop-filter: blur(4px);
    }
    .start-btn { width: 34px; height: 34px; background: radial-gradient(circle, #5e97ff, #1a56c4); border-radius: 50%; border: 2px solid #fff; cursor: pointer; box-shadow: 0 0 5px rgba(0,0,0,0.3); }
    .system-tray { margin-left: auto; color: #003399; font-size: 11px; text-align: right; font-weight: bold; }

    /* ERROR BOX (Windows Classic Theme) */
    #errorBox {
      display: none; position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%);
      width: 320px; background-color: #c0c0c0; border: 2px solid; border-color: #ffffff #808080 #808080 #ffffff;
      padding: 2px; z-index: 10005; box-shadow: 2px 2px 0px #000;
    }
    .error-title { background-color: #000080; color: white; padding: 3px 5px; font-weight: bold; font-size: 12px; display: flex; justify-content: space-between; font-family: "MS Sans Serif", "Tahoma", sans-serif; }
    .error-body { padding: 20px; display: flex; align-items: center; gap: 15px; font-size: 11px; color: black; font-family: "MS Sans Serif", "Tahoma", sans-serif; }
    .error-icon-classic { width: 32px; height: 32px; background: #cc0000; color: white; border-radius: 50%; display: flex; justify-content: center; align-items: center; font-weight: bold; font-size: 22px; border: 2px solid #fff; flex-shrink: 0; }
    .classic-btn { padding: 4px 25px; background: #c0c0c0; border: 2px solid; border-color: #ffffff #808080 #808080 #ffffff; cursor: pointer; font-family: "MS Sans Serif", "Tahoma", sans-serif; font-size: 11px; outline: none; }
    .classic-btn:active { border-color: #808080 #ffffff #ffffff #808080; }
  </style>
</head>
<body>

  <div class="win7-window" id="mainApp">
    <div class="title-bar">
      <span>Tech Savvy Guy's Website</span>
      <div class="controls">
        <button class="control-btn" onclick="minimizeWindow()">_</button>
        <button class="control-btn" onclick="maximizeWindow()">□</button>
        <button class="control-btn close" onclick="closeWindow()">X</button>
      </div>
    </div>
    <div class="window-content">
      <h1>Welcome to the Tech Savvy Guy's Website!</h1>
      <p>Hello! I'm the Tech Savvy Guy. I like reviving old phones, like listening to music, making youtube videos and playing games like minecraft and roblox.</p>
      <p>I am a hardcore fan of Techzaster, DankPods, Michael MJD and frokfrdk!</p>
      <p>I hope you like my website! If you want to contact me, links are at the bottom!</p>
      <p><a href="https://www.reddit.com/r/androidafterlife/" target="_blank">Check out r/androidafterlife! It is a great place for reviving old phones!</a></p>
      <p><a href="https://dsc.gg/old-youtube-layout" target="_blank">I made an unofficial discord server for r/oldyoutubelayout. Check it out!</a></p>
      
      <hr>
      
      <h3>Contact & Links:</h3>
      <a href="https://m.youtube.com/channel/UCQLq2oiuDgt9MKjP4LA24dA" class="win7-button" target="_blank">YouTube Channel</a>
      <a href="https://www.reddit.com/u/iloveneoni_so-much5/s/PeSb501Rkb" class="win7-button" target="_blank">Reddit Profile</a>
      <a href="https://dsc.gg/tech-collection-club" class="win7-button" target="_blank">Discord Server</a>
       <a href="https://www.reddit.com/r/techcollectionclub/s/o1M7r9dCgC" class="win7-button" target="_blank">MY SUBREDDIT!</a>
      <div class="win7-text-display">Roblox: CHUPUUO123</div>
      <div class="win7-text-display">Spotify: techsavvy.guy456</div>
    </div>
  </div>

  <div class="taskbar">
    <div class="start-btn" onclick="showClassicError('Start menu currently unavailable.')"></div>
    <div class="system-tray">
      <div id="clock">12:00 PM</div>
      <div id="date" style="font-size: 9px;">5/10/2026</div>
    </div>
  </div>

  <div id="errorBox">
    <div class="error-title"><span>System Error</span><span style="cursor:pointer" onclick="hideError()">X</span></div>
    <div class="error-body">
      <div class="error-icon-classic">X</div>
      <span id="errorMessage">An unknown error occurred.</span>
    </div>
    <div style="text-align: center; padding-bottom: 15px;">
      <button class="classic-btn" onclick="hideError()">OK</button>
    </div>
  </div>

  <script>
    const appWindow = document.getElementById('mainApp');
    const errBox = document.getElementById('errorBox');
    const errMsg = document.getElementById('errorMessage');

    // Maximize logic added back
    function maximizeWindow() {
      appWindow.classList.toggle('maximized');
    }

    function closeWindow() {
      appWindow.style.display = 'none';
      alert("FATAL ERROR 0x0000005: RAM OVERFLOW!\n\nJust kidding. Your friend vocaloid.01 tried to crash your browser, but I'm too savvy for that! Refresh the page to bring the window back.");
    }

    function minimizeWindow() {
      appWindow.style.display = 'none';
      showClassicError('You minimised the window!! Please refresh the page.');
    }

    function showClassicError(text) {
      errMsg.innerText = text;
      errBox.style.display = 'block';
    }

    function hideError() {
      errBox.style.display = 'none';
    }

    function updateClock() {
      const now = new Date();
      let h = now.getHours();
      let m = now.getMinutes();
      let ampm = h >= 12 ? 'PM' : 'AM';
      h = h % 12 || 12;
      m = m < 10 ? '0' + m : m;
      document.getElementById('clock').innerHTML = h + ':' + m + ' ' + ampm;
      document.getElementById('date').innerHTML = (now.getMonth() + 1) + '/' + now.getDate() + '/' + now.getFullYear();
    }
    setInterval(updateClock, 1000);
    updateClock();
  </script>

</body>
</html>

