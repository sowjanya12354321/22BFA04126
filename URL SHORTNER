<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>URL Shortener App</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet" />
  <style>
    body {
      font-family: 'Roboto', sans-serif;
      margin: 0;
      padding: 20px;
      background: #f7f7f7;
    }

    h1 {
      color: #333;
      text-align: center;
    }

    .container {
      max-width: 800px;
      margin: auto;
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    input {
      width: 100%;
      padding: 8px;
      margin-top: 5px;
      margin-bottom: 15px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }

    button {
      background: #1976d2;
      color: white;
      padding: 10px 15px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }

    button:hover {
      background: #1565c0;
    }

    .url-block {
      border-bottom: 1px solid #eee;
      padding: 10px 0;
    }

    .analytics {
      font-size: 0.9em;
      color: #444;
      margin-top: 10px;
    }

    .error {
      color: red;
      font-size: 0.9em;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Simple URL Shortener</h1>

    <div id="formContainer"></div>

    <button onclick="submitUrls()">Shorten URLs</button>

    <h2>Shortened Links</h2>
    <div id="resultsContainer"></div>
  </div>

  <script>
    const MAX_URLS = 5;
    const urlEntries = [];
    const analytics = {};

    // Initial form setup
    function loadForm() {
      const formContainer = document.getElementById('formContainer');
      for (let i = 0; i < MAX_URLS; i++) {
        const div = document.createElement('div');
        div.innerHTML = `
          <label>Original URL:</label>
          <input type="text" id="url${i}" placeholder="https://example.com" />

          <label>Shortcode (optional):</label>
          <input type="text" id="code${i}" placeholder="abc123" />

          <label>Validity (minutes, optional):</label>
          <input type="number" id="validity${i}" placeholder="Default 30 min" />
        `;
        formContainer.appendChild(div);
      }
    }

    // Util: Generate shortcode
    function generateCode(length = 6) {
      return Math.random().toString(36).substring(2, 2 + length);
    }

    // Click tracker
    function handleClick(shortcode) {
      const entry = JSON.parse(localStorage.getItem(shortcode));
      if (!entry) return alert("URL expired or not found.");
      
      // Track click
      const ts = new Date().toISOString();
      const from = "localhost"; // Simulated source
      const geo = "India"; // Simulated location

      if (!analytics[shortcode]) analytics[shortcode] = [];
      analytics[shortcode].push({ timestamp: ts, source: from, location: geo });

      alert("Redirecting to: " + entry.url);
      // Simulate redirection
      window.open(entry.url, "_blank");
    }

    // Submit URLs
    function submitUrls() {
      const results = document.getElementById('resultsContainer');
      results.innerHTML = '';

      for (let i = 0; i < MAX_URLS; i++) {
        const url = document.getElementById(url${i}).value.trim();
        const codeInput = document.getElementById(code${i}).value.trim();
        const validity = parseInt(document.getElementById(validity${i}).value) || 30;

        if (!url) continue;

        try {
          new URL(url); // Validate URL
        } catch {
          alert(Invalid URL at position ${i + 1});
          return;
        }

        const shortcode = codeInput || generateCode();
        if (localStorage.getItem(shortcode)) {
          alert(Shortcode "${shortcode}" already exists);
          return;
        }

        const expires = Date.now() + validity * 60 * 1000;
        const entry = { url, created: new Date().toISOString(), expires };

        localStorage.setItem(shortcode, JSON.stringify(entry));

        const div = document.createElement('div');
        div.className = 'url-block';
        div.innerHTML = `
          <b>Short URL:</b> <a href="#" onclick="handleClick('${shortcode}')">http://localhost:3000/${shortcode}</a><br/>
          <b>Expires at:</b> ${new Date(expires).toLocaleString()}
          <div class="analytics" id="analytics-${shortcode}"></div>
        `;
        results.appendChild(div);
      }
    }

    window.onload = loadForm;
  </script>
</body>
</html>
