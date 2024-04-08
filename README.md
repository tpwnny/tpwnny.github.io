# tpwnny.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Request Access</title>
    <style>
        /* General Styling */
        body {
            margin: 0;
            font-family: Arial, sans-serif;
        }

        /* Main Image Page Styling */
        .main-image {
            position: relative;
            height: 100vh;
            background-image: url('main-image.jpg'); /* Replace with your main image */
            background-size: cover;
            background-position: center;
        }

        .request-access-btn {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            padding: 10px 20px;
            font-size: 18px;
            background-color: #007bff;
            color: #fff;
            border: none;
            cursor: pointer;
        }

        /* Form Page Styling */
        .form-container {
            max-width: 400px;
            margin: 50px auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        input[type="text"],
        input[type="email"],
        button {
            display: block;
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        button {
            background-color: #007bff;
            color: #fff;
            border: none;
            cursor: pointer;
        }

        #timer {
            text-align: center;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="main-image">
        <!-- Main Image Here -->
        <button class="request-access-btn" onclick="redirectToForm()">Request Access</button>
    </div>
    <div class="form-container" style="display: none;">
        <h2>Request Access Form</h2>
        <form id="request-form" onsubmit="submitForm()">
            <input type="text" id="name" placeholder="Name" required>
            <input type="email" id="email" placeholder="Email" required>
            <input type="text" id="reason" placeholder="Reason for Access" required>
            <input type="text" id="address" placeholder="Address" required>
            <button type="submit">Submit</button>
        </form>
        <div id="timer">Time Left: 10:00</div>
    </div>

    <script>
        // Redirect to form page
        function redirectToForm() {
            document.querySelector('.main-image').style.display = 'none';
            document.querySelector('.form-container').style.display = 'block';
            startTimer();
        }

        // Submit form
        function submitForm() {
            event.preventDefault(); // Prevent default form submission behavior

            // Simulate delay before asking for address
            setTimeout(() => {
                let address = prompt("Please enter your address:");
                if (address) {
                    alert("Form submitted successfully!");
                }
            }, 2000);
        }

        // Timer for the form page
        let timerDisplay = document.getElementById('timer');
        let timeLeft = 600; // 10 minutes

        function countdown() {
            let minutes = Math.floor(timeLeft / 60);
            let seconds = timeLeft % 60;

            timerDisplay.textContent = `Time Left: ${minutes < 10 ? '0' : ''}${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;

            if (timeLeft <= 0) {
                clearInterval(timerInterval);
                alert("Time's up! Please submit the form.");
                document.getElementById('request-form').submit();
            } else {
                timeLeft--;
            }
        }

        function startTimer() {
            let timerInterval = setInterval(countdown, 1000);
        }
    </script>
</body>
</html>
