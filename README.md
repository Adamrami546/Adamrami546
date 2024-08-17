<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Like Button</title>
    <style>
        .like-button {
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .like-button:disabled {
            background-color: #0056b3;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <h1>Like Button Example</h1>
    <button id="likeButton" class="like-button">Like</button>
    <p>Likes: <span id="likeCount">0</span></p>

    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const likeButton = document.getElementById('likeButton');
            const likeCount = document.getElementById('likeCount');

            // Fetch the initial like count
            fetch('/likes')
                .then(response => response.json())
                .then(data => {
                    likeCount.textContent = data.likes;
                });

            // Add event listener to the like button
            likeButton.addEventListener('click', () => {
                fetch('/like', {
                    method: 'POST'
                })
                .then(response => response.json())
                .then(data => {
                    likeCount.textContent = data.likes;
                })
                .catch(error => console.error('Error:', error));
            });
        });
    </script>
</body>
</html>
