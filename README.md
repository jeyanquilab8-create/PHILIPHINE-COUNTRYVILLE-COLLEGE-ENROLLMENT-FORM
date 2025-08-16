<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Login & Enrollment Form - Philippine Countryville College</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      margin: 0; padding: 0;
      background: linear-gradient(120deg, #89f7fe, #66a6ff);
    }
    header {
      background: linear-gradient(90deg, #1e3c72, #2a5298);
      color: white; text-align: center; padding: 25px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.3);
    }
    main {
      max-width: 550px; margin: 40px auto;
      background: #fff; padding: 30px;
      border-radius: 15px;
      box-shadow: 0 6px 20px rgba(0,0,0,0.2);
    }
    form label { font-weight: 600; display: block; margin-bottom: 8px; }
    input, select, textarea {
      width: 100%; padding: 12px; margin-bottom: 20px;
      border: 1px solid #ccc; border-radius: 8px;
    }
    input:focus, select:focus, textarea:focus {
      border-color: #2a5298; box-shadow: 0 0 6px rgba(42,82,152,0.5);
      outline: none;
    }
    button {
      background: #2a5298; color: white;
      padding: 12px 25px; border: none;
      border-radius: 8px; cursor: pointer;
      font-size: 16px; margin-right: 10px;
    }
    button:hover { background: #1e3c72; transform: scale(1.05); }
    footer {
      text-align: center; margin-top: 40px;
      padding: 20px;
      background: linear-gradient(90deg, #2a5298, #1e3c72);
      color: #ddd; font-size: 14px;
    }
    #enrollmentSection, #success, #registerSection { display: none; }
    #success { text-align: center; }
    #success h2 { color: green; margin-bottom: 20px; }
  </style>
</head>
<body>
  <header>
    <h1>Philippine Countryville College</h1>
  </header>

  <main>
    <!-- LOGIN -->
    <section id="loginSection">
      <h2>🔐 Login</h2>
      <form id="loginForm">
        <label>Username:</label>
        <input type="text" id="loginUser" required>
        <label>Password:</label>
        <input type="password" id="loginPass" required>
        <button type="submit">Login</button>
      </form>
      <p style="color:red; display:none;" id="loginError">❌ Invalid account!</p>
      <p>No account? <a href="#" onclick="showRegister()">Create one</a></p>
    </section>

    <!-- REGISTER -->
    <section id="registerSection">
      <h2>🆕 Create Account</h2>
      <form id="registerForm">
        <label>Username:</label>
        <input type="text" id="regUser" required>
        <label>Password:</label>
        <input type="password" id="regPass" required>
        <button type="submit">Register</button>
      </form>
      <p style="color:red; display:none;" id="registerError">⚠ Username already exists!</p>
      <p>Already have an account? <a href="#" onclick="showLogin()">Back to Login</a></p>
    </section>

    <!-- ENROLLMENT -->
    <section id="enrollmentSection">
      <h2>📝 Enrollment Form</h2>
      <form id="enrollmentForm">
        <label>Full Name:</label>
        <input type="text" id="fullname" required>
        <label>Email:</label>
        <input type="email" id="email" required>
        <label>Course:</label>
        <select id="course" required>
          <option value="">-- Select Course --</option>
          <option value="bsit">BSIT</option>
          <option value="bscs">BSCS</option>
          <option value="bsba">BSBA</option>
        </select>
        <label>Address:</label>
        <textarea id="address" rows="3" required></textarea>
        <button type="submit">Submit</button>
        <button type="reset">Clear</button>
      </form>
    </section>

    <!-- SUCCESS -->
    <div id="success">
      <h2>✅ Enrollment Successful!</h2>
      <p>Thank you for enrolling.</p>
      <button onclick="window.print()">🖨 Print</button>
    </div>
  </main>

  <footer>
    <p>&copy; 2025 Philippine Countryville College. All rights reserved.</p>
  </footer>

  <script>
    const loginSection = document.getElementById("loginSection");
    const registerSection = document.getElementById("registerSection");
    const enrollmentSection = document.getElementById("enrollmentSection");
    const success = document.getElementById("success");

    function showRegister(){
      loginSection.style.display="none";
      registerSection.style.display="block";
    }
    function showLogin(){
      registerSection.style.display="none";
      loginSection.style.display="block";
    }

    // REGISTER
    const registerForm = document.getElementById("registerForm");
    const registerError = document.getElementById("registerError");
    registerForm.addEventListener("submit", e=>{
      e.preventDefault();
      const user = document.getElementById("regUser").value;
      const pass = document.getElementById("regPass").value;
      let accounts = JSON.parse(localStorage.getItem("accounts")) || {};
      if(accounts[user]){
        registerError.style.display="block";
      } else {
        accounts[user]=pass;
        localStorage.setItem("accounts", JSON.stringify(accounts));
        alert("✅ Account created! Please login.");
        showLogin();
      }
    });

    // LOGIN
    const loginForm = document.getElementById("loginForm");
    const loginError = document.getElementById("loginError");
    loginForm.addEventListener("submit", e=>{
      e.preventDefault();
      const user = document.getElementById("loginUser").value;
      const pass = document.getElementById("loginPass").value;
      let accounts = JSON.parse(localStorage.getItem("accounts")) || {};
      if(accounts[user] && accounts[user]===pass){
        loginSection.style.display="none";
        enrollmentSection.style.display="block";
      } else {
        loginError.style.display="block";
      }
    });

    // ENROLLMENT
    const enrollmentForm = document.getElementById("enrollmentForm");
    enrollmentForm.addEventListener("submit", e=>{
      e.preventDefault();
      enrollmentSection.style.display="none";
      success.style.display="block";
    });
  </script>
</body>
</html>
