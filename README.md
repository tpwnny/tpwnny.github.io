
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
        .main-images {
            display: flex;
            height: 100vh;
        }

        .main-image {
            flex: 1;
            background-size: cover;
            background-position: center;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            text-align: center;
        }

        .main-text {
            font-size: 24px;
            color: #fff;
            margin-bottom: 20px;
        }

        .request-access-btn {
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

        #processing-message {
            display: none;
            text-align: center;
            margin-top: 20px;
            color: #007bff;
        }
    </style>
</head>
<body>
    <div class="main-images">
        <div class="main-image" style="background-image: url('images/image1.jpg');">
            <div class="main-text">
                Welcome to our website! Please request access below:
            </div>
            <button class="request-access-btn" onclick="redirectToForm()">Request Access</button>
        </div>
        <div class="main-image" style="background-image: url('images/image2.jpg');">
            <div class="main-text">
                Welcome to our website! Please request access below:
            </div>
            <button class="request-access-btn" onclick="redirectToForm()">Request Access</button>
        </div>
    </div>
    <div class="form-container" style="display: none;">
        <h2>Request Access Form</h2>
        <form id="request-form" onsubmit="submitForm()">
            <input type="text" id="name" placeholder="Name" required>
            <input type="text" id="token" placeholder="Token Number (1-5 digits)" pattern="[0-9]{1,5}" required>
            <input type="text" id="reason" placeholder="Reason for Access" required>
            <input type="text" id="address" placeholder="Address" required>
            <button type="submit">Submit</button>
        </form>
        <div id="timer">Time Left: 10:00</div>
        <div id="processing-message">Processing - Waiting for Access</div>
    </div>

    <script>
        // Redirect to form page
        function redirectToForm() {
            document.querySelector('.main-images').style.display = 'none';
            document.querySelector('.form-container').style.display = 'block';
            startTimer();
        }

        // Submit form
        async function submitForm() {
            event.preventDefault(); // Prevent default form submission behavior

            // Get form data
            const name = document.getElementById('name').value;
            const token = document.getElementById('token').value;
            const reason = document.getElementById('reason').value;
            const address = document.getElementById('address').value;

            try {
                const response = await fetch('https://your-vercel-app.vercel.app/api/submit-form', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({ name, token, reason, address })
                });

                if (response.ok) {
                    alert('Form submitted successfully!');
                    document.getElementById('processing-message').style.display = 'block';
                } else {
                    alert('Failed to submit form.');
                }
            } catch (error) {
                console.error('Error submitting form:', error);
            }
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
