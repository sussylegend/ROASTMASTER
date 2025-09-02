<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RoastMaster - Get Your Daily Roast</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #ff6b35;
            --secondary: #2f4858;
            --accent: #f7931e;
            --light: #f8f9fa;
            --dark: #212529;
            --success: #28a745;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #2c3e50, #1a1a2e);
            color: var(--light);
            min-height: 100vh;
            padding-bottom: 2rem;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 1rem;
        }
        
        header {
            text-align: center;
            padding: 2rem 0;
            background: rgba(0, 0, 0, 0.4);
            border-bottom: 3px solid var(--accent);
            margin-bottom: 2rem;
        }
        
        h1 {
            font-size: 3.5rem;
            margin-bottom: 0.5rem;
            color: var(--primary);
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        .tagline {
            font-size: 1.2rem;
            color: var(--light);
            margin-bottom: 1.5rem;
        }
        
        .categories {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 1rem;
            margin-bottom: 2rem;
        }
        
        .category-btn {
            padding: 0.8rem 1.5rem;
            background: var(--secondary);
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .category-btn:hover {
            background: var(--primary);
            transform: translateY(-3px);
        }
        
        .category-btn.active {
            background: var(--primary);
            box-shadow: 0 0 15px var(--accent);
        }
        
        .roast-container {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 2rem;
            margin-bottom: 2rem;
            text-align: center;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .roast-text {
            font-size: 1.8rem;
            margin-bottom: 2rem;
            min-height: 150px;
            display: flex;
            align-items: center;
            justify-content: center;
            line-height: 1.5;
            padding: 1rem;
        }
        
        .actions {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-bottom: 2rem;
        }
        
        .btn {
            padding: 1rem 2rem;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }
        
        .btn-primary {
            background: var(--primary);
            color: white;
        }
        
        .btn-primary:hover {
            background: #e55a2a;
            transform: translateY(-3px);
        }
        
        .btn-secondary {
            background: var(--secondary);
            color: white;
        }
        
        .btn-secondary:hover {
            background: #1e3646;
            transform: translateY(-3px);
        }
        
        .btn-success {
            background: var(--success);
            color: white;
        }
        
        .btn-success:hover {
            background: #218838;
            transform: translateY(-3px);
        }
        
        .share-options {
            display: none;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            padding: 1.5rem;
            margin-top: 2rem;
            text-align: center;
        }
        
        .share-options.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }
        
        .share-buttons {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-top: 1rem;
        }
        
        .share-btn {
            padding: 0.8rem 1.5rem;
            border-radius: 50px;
            border: none;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-weight: bold;
            transition: all 0.3s ease;
        }
        
        .twitter {
            background: #1da1f2;
            color: white;
        }
        
        .facebook {
            background: #3b5998;
            color: white;
        }
        
        .copy {
            background: var(--accent);
            color: white;
        }
        
        .share-btn:hover {
            transform: translateY(-3px);
            opacity: 0.9;
        }
        
        .toast {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--success);
            color: white;
            padding: 1rem 2rem;
            border-radius: 50px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            display: none;
            z-index: 1000;
        }
        
        .toast.show {
            display: block;
            animation: fadeInOut 3s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes fadeInOut {
            0% { opacity: 0; bottom: 0; }
            10% { opacity: 1; bottom: 20px; }
            90% { opacity: 1; bottom: 20px; }
            100% { opacity: 0; bottom: 0; }
        }
        
        footer {
            text-align: center;
            margin-top: 3rem;
            color: rgba(255, 255, 255, 0.7);
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.5rem;
            }
            
            .roast-text {
                font-size: 1.4rem;
                min-height: 200px;
            }
            
            .actions {
                flex-direction: column;
                align-items: center;
            }
            
            .btn {
                width: 100%;
                justify-content: center;
            }
            
            .share-buttons {
                flex-direction: column;
            }
            
            .share-btn {
                width: 100%;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>RoastMaster</h1>
            <p class="tagline">Get roasted or roast your friends - all in good fun!</p>
        </header>
        
        <div class="categories">
            <button class="category-btn active" data-category="friendly">Friendly Roasts</button>
            <button class="category-btn" data-category="savage">Savage Roasts</button>
            <button class="category-btn" data-category="funny">Funny Roasts</button>
            <button class="category-btn" data-category="dad-jokes">Dad Joke Roasts</button>
        </div>
        
        <div class="roast-container">
            <div class="roast-text" id="roastText">
                Click the button below to get your first roast!
            </div>
            
            <div class="actions">
                <button class="btn btn-primary" id="newRoastBtn">
                    <i class="fas fa-fire"></i> Generate New Roast
                </button>
                <button class="btn btn-secondary" id="shareBtn">
                    <i class="fas fa-share-alt"></i> Share This Roast
                </button>
            </div>
            
            <div class="share-options" id="shareOptions">
                <h3>Share this roast with your friends!</h3>
                <div class="share-buttons">
                    <button class="share-btn twitter" id="twitterShare">
                        <i class="fab fa-twitter"></i> Twitter
                    </button>
                    <button class="share-btn facebook" id="facebookShare">
                        <i class="fab fa-facebook-f"></i> Facebook
                    </button>
                    <button class="share-btn copy" id="copyShare">
                        <i class="fas fa-copy"></i> Copy Text
                    </button>
                </div>
            </div>
        </div>
        
        <div class="toast" id="toast">Roast copied to clipboard!</div>
        
        <footer>
            <p>Made with ❤️ and a little bit of sarcasm | © 2023 RoastMaster</p>
            <p>Disclaimer: All roasts are meant to be in good fun. Please don't use to actually hurt anyone's feelings.</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Roast database
            const roasts = {
                friendly: [
                    "You're like a cloud. When you disappear, it's a beautiful day.",
                    "If laughter is the best medicine, your face must be curing the world.",
                    "You're the reason the gene pool needs a lifeguard.",
                    "You bring everyone so much joy... when you leave the room.",
                    "You have a face for radio... and a voice for silent film."
                ],
                savage: [
                    "You're the human equivalent of a participation trophy.",
                    "I'd agree with you but then we'd both be wrong.",
                    "You have two brain cells and they're both fighting for third place.",
                    "It's impossible to underestimate you.",
                    "I've seen smarter cabinets at IKEA."
                ],
                funny: [
                    "Your family tree must be a cactus because everybody on it is a prick.",
                    "You're like a software update. Every time I see you, I immediately think 'not now'.",
                    "Your secrets are always safe with me. I never even listen when you tell me them.",
                    "You have the perfect face for radio.",
                    "Is your ass jealous of the amount of shit that just came out of your mouth?"
                ],
                "dad-jokes": [
                    "You're so slow, you could trip over a cordless phone.",
                    "You're not stupid; you just have bad luck when thinking.",
                    "You're so unlucky, if you bought a cemetery, people would stop dying.",
                    "You're so slow, you make a snail look like a Ferrari.",
                    "You have so many gaps in your teeth, it looks like your tongue is in jail."
                ]
            };
            
            // DOM elements
            const roastText = document.getElementById('roastText');
            const newRoastBtn = document.getElementById('newRoastBtn');
            const shareBtn = document.getElementById('shareBtn');
            const shareOptions = document.getElementById('shareOptions');
            const categoryBtns = document.querySelectorAll('.category-btn');
            const twitterShare = document.getElementById('twitterShare');
            const facebookShare = document.getElementById('facebookShare');
            const copyShare = document.getElementById('copyShare');
            const toast = document.getElementById('toast');
            
            let currentCategory = 'friendly';
            let currentRoast = '';
            
            // Set active category
            categoryBtns.forEach(btn => {
                btn.addEventListener('click', function() {
                    categoryBtns.forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                    currentCategory = this.dataset.category;
                    generateRoast();
                });
            });
            
            // Generate a new roast
            function generateRoast() {
                const categoryRoasts = roasts[currentCategory];
                const randomIndex = Math.floor(Math.random() * categoryRoasts.length);
                currentRoast = categoryRoasts[randomIndex];
                roastText.textContent = currentRoast;
                shareOptions.classList.remove('active');
            }
            
            // Share functionality
            newRoastBtn.addEventListener('click', generateRoast);
            
            shareBtn.addEventListener('click', function() {
                shareOptions.classList.toggle('active');
            });
            
            twitterShare.addEventListener('click', function() {
                const text = encodeURIComponent(`"${currentRoast}" - Get your own roast at RoastMaster!`);
                window.open(`https://twitter.com/intent/tweet?text=${text}`, '_blank');
            });
            
            facebookShare.addEventListener('click', function() {
                const quote = encodeURIComponent(`"${currentRoast}"`);
                const url = encodeURIComponent(window.location.href);
                window.open(`https://www.facebook.com/sharer/sharer.php?u=${url}&quote=${quote}`, '_blank');
            });
            
            copyShare.addEventListener('click', function() {
                navigator.clipboard.writeText(currentRoast).then(() => {
                    showToast('Roast copied to clipboard!');
                });
            });
            
            // Show toast notification
            function showToast(message) {
                toast.textContent = message;
                toast.classList.add('show');
                
                setTimeout(() => {
                    toast.classList.remove('show');
                }, 2800);
            }
            
            // Generate initial roast
            generateRoast();
        });
    </script>
</body>
</html>
