<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beautiful Page</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }

        header {
            background-color: #333;
            color: white;
            padding: 10px;
            text-align: center;
        }

        section {
            margin: 20px;
        }

        .container {
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
        }

        .container div {
            width: 30%;
            background-color: #fff;
            padding: 15px;
            margin: 10px;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        footer {
            background-color: #333;
            color: white;
            padding: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <header>
        <h1>Beautiful Page</h1>
    </header>

    <section>
        <div class="container">
            <div>
                <h2>Section 1</h2>
                <p>This is the content of section 1.</p>
            </div>
            <div>
                <h2>Section 2</h2>
                <p>This is the content of section 2.</p>
            </div>
            <div>
                <h2>Section 3</h2>
                <p>This is the content of section 3.</p>
            </div>
        </div>
    </section>

    <footer>
        <p>&copy; 2024 Beautiful Page. All rights reserved.</p>
    </footer>
</body>
</html>
