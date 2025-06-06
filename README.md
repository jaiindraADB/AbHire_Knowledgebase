Login Failed: ReferenceError: axios is not defined
    at HTMLButtonElement.<anonymous> (signin.html:358:26)
const corsProxy = "https://cors-anywhere.herokuapp.com/";
    const apiURL = "https://abhirebackend.onrender.com/auth/login";
    
      const email = document.getElementById("Email").value;
      const password = document.getElementById("Password").value;
      const button = document.getElementById('signin');
      button.addEventListener('click', async function(e) {
      e.preventDefault();


      try {
        const response = await axios.post( apiURL, {
          email,
          password
        }, {
          headers: {
            "Content-Type": "application/json"
          }
        });

        console.log("✅ Login Success:");
        alert("Login successful." );

        // You can now store the token, redirect, or call another API
        // localStorage.setItem("token", response.data.token);
        // window.location.href = "/dashboard.html";

      } catch (error) {
        console.error("❌ Login Failed:", error);
        alert("Login failed: " + (error.response?.data?.message || error.message));
      }
      })
