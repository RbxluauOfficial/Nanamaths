<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Nanamaths</title>
  <link rel="icon" type="image/x-icon" href="logotab.ico">  
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Poppins', sans-serif;
    }
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(135deg, #ffffff, #ffffff);
    }
    .container {
      width: 100%;
      max-width: 400px;
      padding: 25px;
      background: #ffffff;
      border-radius: 12px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
      text-align: center;
      transition: transform 0.3s ease-in-out;
    }
    .logo {
      width: 100px;
      height: auto;
      margin-bottom: 15px;
    }
    h2 {
      font-weight: 600;
      margin-bottom: 15px;
      color: #333;
    }
    label {
      font-size: 14px;
      font-weight: 400;
      display: block;
      text-align: left;
      margin-top: 10px;
    }
    input {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 2px solid #ddd;
      border-radius: 8px;
      outline: none;
      font-size: 14px;
      transition: 0.3s;
    }
    input:focus {
      border-color: #ffffff;
    }
    button {
      width: 100%;
      padding: 12px;
      background: #78b6e9;
      color: #fff;
      border: none;
      border-radius: 8px;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
      transition: 0.3s;
      margin-top: 10px;
    }
    button:hover {
      background: #35638D;
      transform: scale(1.05);
    }
    .message {
      margin-top: 10px;
      padding: 10px;
      border-radius: 6px;
      font-size: 14px;
      text-align: center;
      display: none;
    }
    .success {
      background: #d4edda;
      color: #155724;
      display: block;
    }
    .error {
      background: #f8d7da;
      color: #721c24;
      display: block;
    }
    /* Hide sections by default */
    .hidden {
      display: none;
    }
    .fade-in {
      animation: fadeIn 0.5s ease-in-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(-10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>

  <!-- Main Menu -->
  <div class="container fade-in" id="main-menu">
    <img src="logo.png" alt="Logo" class="logo">
    <h2>მოგესალმებით</h2>
    <button onclick="showSection('teacher-login')">მასწავლებელი</button>
    <button onclick="showSection('student-menu')">სტუდენტი</button>
  </div>

  <!-- Teacher Login -->
  <div class="container hidden" id="teacher-login">
    <img src="logo.png" alt="Logo" class="logo">
    <h2>მასწავლებელი</h2>
    <label>სახელი</label>
    <input type="text" id="teacher-username" placeholder="შეიტანეთ სახელი">
    <label>პარული</label>
    <input type="password" id="teacher-password" placeholder="შეიტანეთ პარული">
    <button onclick="teacherLogin()">შესვლა</button>
    <button onclick="showSection('main-menu')">დაბრუნება</button>
    <div id="teacher-message" class="message"></div>
  </div>

  <!-- Student Menu -->
  <div class="container hidden" id="student-menu">
    <img src="logo.png" alt="Logo" class="logo">
    <h2>სტუდენტი</h2>
    <button onclick="showSection('student-register')">დარეგისტრი</button>
    <button onclick="showSection('student-login')">შესვლა</button>
    <button onclick="showSection('main-menu')">დაბრუნება</button>
  </div>

  <!-- Student Registration -->
  <div class="container hidden" id="student-register">
    <img src="logo.png" alt="Logo" class="logo">
    <h2>სტუდენტის რეგისტრაცია</h2>
    <label>სახელი</label>
    <input type="text" id="reg-username" placeholder="შეიტანე სახელი">
    <label>პარული</label>
    <input type="password" id="reg-password" placeholder="შეიტანე პარული">
    <button onclick="registerStudent()">რეგისტრაცია</button>
    <button onclick="showSection('student-menu')">დაბრუნება</button>
    <div id="register-message" class="message"></div>
  </div>

  <!-- Student Login -->
  <div class="container hidden" id="student-login">
    <img src="logo.png" alt="Logo" class="logo">
    <h2>სტუდენტის შესვლა</h2>
    <label>სახელი</label>
    <input type="text" id="login-username" placeholder="შეიტანე სახელი">
    <label>პარული</label>
    <input type="password" id="login-password" placeholder="შეიტანე პარული">
    <button onclick="studentLogin()">შესვლა</button>
    <button onclick="showSection('student-menu')">დაბრუნება</button>
    <div id="login-message" class="message"></div>
  </div>

  <script>
    // Teacher credentials (example)
    const TEACHER_USERNAME = "teacherofmath2";
    const TEACHER_PASSWORD = "12993212";

    // Student data storage (using localStorage)
    let students = JSON.parse(localStorage.getItem("students")) || [];

    function showSection(sectionId) {
      document.querySelectorAll(".container").forEach(section => section.classList.add("hidden"));
      document.getElementById(sectionId).classList.remove("hidden");
    }

    // Teacher login redirects to teacher.html
    function teacherLogin() {
      const username = document.getElementById("teacher-username").value;
      const password = document.getElementById("teacher-password").value;
      const message = document.getElementById("teacher-message");

      if (username === TEACHER_USERNAME && password === TEACHER_PASSWORD) {
        window.location.href = "teacher.html";
      } else {
        showMessage(message, "პარული ან სახელი არასწორად არის მითითებული!", "error");
      }
    }

    // Student registration
    function registerStudent() {
      const username = document.getElementById("reg-username").value;
      const password = document.getElementById("reg-password").value;
      const message = document.getElementById("register-message");

      if (students.some(student => student.username === username)) {
        showMessage(message, "Username already exists!", "error");
      } else {
        students.push({ username, password });
        localStorage.setItem("students", JSON.stringify(students));
        showMessage(message, "Registration successful!", "success");
      }
    }

    // Student login redirects to student.html
    function studentLogin() {
      const username = document.getElementById("login-username").value;
      const password = document.getElementById("login-password").value;
      const message = document.getElementById("login-message");

      const student = students.find(student => student.username === username && student.password === password);
      if (student) {
        window.location.href = "student.html";
      } else {
        showMessage(message, "პარული ან სახელი არასწორად არის მითითებული!", "error");
      }
    }

    function showMessage(element, text, type) {
      element.textContent = text;
      element.className = `message ${type}`;
    }
  </script>

</body>
</html>
