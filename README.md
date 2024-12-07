
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Earn Together - Home</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
   <style>
   /* General Reset */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Roboto', Arial, sans-serif;
    color: #333;
    line-height: 1.6;
    background-color: #f4f4f9;
    overflow-x: hidden;
}

.container {
    width: 90%;
    max-width: 1200px;
    margin: 0 auto;
}

/* Header */
header {
    background-color: #1a73e8;
    color: white;
    padding: 15px 20px;
    position: sticky;
    top: 0;
    z-index: 1000;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

header .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

header h1 {
    font-size: 1.8rem;
}

/* Hamburger Button */
.hamburger {
    background: none;
    border: none;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 20px;
    width: 25px;
}

.hamburger .line {
    width: 100%;
    height: 3px;
    background-color: white;
    border-radius: 3px;
    transition: all 0.3s ease;
}

/* Sidebar */
.sidebar {
    position: fixed;
    top: 0;
    left: -300px;
    width: 250px;
    height: 100%;
    background-color: #1a73e8;
    color: white;
    box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
    z-index: 1000;
    padding: 20px;
}

.sidebar ul {
    list-style: none;
}

.sidebar ul li {
    margin-bottom: 15px;
}

.sidebar ul li a {
    color: white;
    font-size: 1.1rem;
    transition: color 0.3s ease;
}

.sidebar ul li a:hover {
    color: #ff9800;
}

/* Overlay */
.overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
    z-index: 500;
}

/* Sidebar Open */
.sidebar.open {
    left: 0;
}

.overlay.visible {
    opacity: 1;
    visibility: visible;
}

/* Hero Section */
.hero {
    text-align: center;
    padding: 60px 20px;
    background: linear-gradient(to right, #1a73e8, #00c6ff);
    color: white;
}

.hero h2 {
    font-size: 2.5rem;
}

.hero p {
    margin: 20px 0;
}

.hero .btn {
    background-color: #ff9800;
    color: white;
    padding: 10px 20px;
    font-size: 1rem;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.3s ease;
}

.hero .btn:hover {
    background-color: #e68a00;
}

/* About Section */
.about {
    text-align: center;
    padding: 40px 20px;
    background-color: white;
}

.about h2 {
    font-size: 2rem;
    margin-bottom: 20px;
}

.about .features {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.feature {
    margin: 10px;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    width: 250px;
}

/* Footer */
footer {
    background-color: #333;
    color: white;
    text-align: center;
    padding: 10px;
    font-size: 0.9rem;
}

footer a {
    color: #ff9800;
    margin: 0 5px;
    transition: color 0.3s ease;
}

footer a:hover {
    color: #fff;
}

/* Responsive Design */
@media (max-width: 768px) {
    header h1 {
        font-size: 1.5rem;
    }

    .hero h2 {
        font-size: 2rem;
    }

    .feature {
        width: 90%;
    }
}
</style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container">
            <h1>Earn Together</h1>
            <button class="hamburger" id="hamburger">
                <span class="line"></span>
                <span class="line"></span>
                <span class="line"></span>
            </button>
        </div>
    </header>

    <!-- Sidebar Navigation -->
    <nav class="sidebar" id="sidebar">
        <ul>
            <li><a href="index.html">Home</a></li>
            <li><a href="services.html">Services</a></li>
            <li><a href="about.html">About</a></li>
            <li><a href="contact.html">Contact</a></li>
            <li><a href="announcement.html">Announcement</a></li>
        </ul>
    </nav>

    <!-- Overlay -->
    <div class="overlay" id="overlay"></div>

    <!-- Hero Section -->
    <section class="hero">
        <div class="container">
            <h2>Welcome to Earn Together</h2>
            <p>Invest Your Today For Your Better Tomorrow<br>Director - Chiranjeev</p>
            <a href="invoice.html" class="btn">Join Us Today</a>
        </div>
    </section>

    <!-- About Section -->
    <section class="about">
        <div class="container">
            <h2>Why Choose Us?</h2>
            <p>We provide customized, data-driven stock market solutions tailored to your financial goals.</p>
            <div class="features">
                <div class="feature">
                    <h3>Personalized Strategies</h3>
                    <p>Our solutions are designed to fit your specific investment needs and goals.</p>
                </div>
                <div class="feature">
                    <h3>Expert Guidance</h3>
                    <p>Our team of seasoned professionals ensures you stay ahead in the market.</p>
                </div>
                <div class="feature">
                    <h3>Transparent Practices</h3>
                    <p>We believe in maintaining complete transparency with our clients.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <p>&copy; 2024 Earn Together. All Rights Reserved.</p>
            <p>Follow us on 
                <a href="#"><i class="fab fa-facebook-f"></i></a>
                <a href="https://youtube.com/@jaiswalmusic.official?si=Y_cKeMyW8gBVdlGC" target="_blank"><i class="fab fa-youtube"></i></a>
                <a href="#"><i class="fab fa-linkedin-in"></i></a>
                <a href="#"><i class="fab fa-instagram"></i></a>.
            </p>
        </div>
    </footer>

    <script>const hamburger = document.getElementById("hamburger");
const sidebar = document.getElementById("sidebar");
const overlay = document.getElementById("overlay");

hamburger.addEventListener("click", () => {
    sidebar.classList.toggle("open");
    overlay.classList.toggle("visible");
});

overlay.addEventListener("click", () => {
    sidebar.classList.remove("open");
    overlay.classList.remove("visible");
});
</script>


</body>
</html>
