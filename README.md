[webpack-dev-server] Loopback: http://localhost:3000/
 const submitbutton = document.getElementById('Submit');
        submitbutton.addEventListener('click', async () => {
        const email = document.getElementById('email').value.trim();
        const password = document.getElementById('password').value.trim();
       const data = {
         email,
            password
       }
        const corsProxy = "https://cors-anywhere.herokuapp.com/";
        const apiURL = "https://abhirebackend.onrender.com/auth/login";
        
                fetch(corsProxy + apiURL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(data)
      })
      .then(res => res.json())
      .then(data => console.log("Login Success:", data))
      .catch(err => console.error("Login Failed:", err));
              });
[webpack-dev-server] Server started: Hot Module Replacement enabled, Live Reloading enabled, Progress disabled, Overlay enabled.
bundle.js:456 [HMR] Waiting for update signal from WDS...
index.js:112 Uncaught TypeError: Cannot read properties of null (reading 'addEventListener')
    at HTMLDocument.eval (index.js:112:16)
eval	@	index.js:112
