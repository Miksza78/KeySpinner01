Plik index.html (strona główna):

<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KeySpinner01 - Breloki obrotowe</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>KeySpinner01</h1>
        <p>Najlepsze breloki obrotowe na rynku!</p>
    </header>

    <main>
        <section class="product">
            <img src="brelok.jpg" alt="Brelok obrotowy" />
            <h2>Brelok obrotowy KeySpinner</h2>
            <p>Stylowy, wytrzymały i funkcjonalny. Idealny dla każdego!</p>
            <strong>29,99 PLN</strong>
            <button id="buyButton">Kup teraz</button>
        </section>
    </main>

    <footer>
        <p>&copy; 2025 KeySpinner01. Wszystkie prawa zastrzeżone.</p>
    </footer>

    <script src="https://js.stripe.com/v3/"></script>
    <script src="script.js"></script>
</body>
</html>

Plik style.css (stylizacja strony):

body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f8f8f8;
    color: #333;
    text-align: center;
}

header {
    background-color: #007bff;
    color: white;
    padding: 20px 0;
}

.product {
    margin: 20px;
    padding: 20px;
    background-color: white;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

img {
    max-width: 300px;
    border-radius: 10px;
    margin-bottom: 10px;
}

button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 16px;
}

button:hover {
    background-color: #0056b3;
}

footer {
    margin-top: 20px;
    padding: 10px 0;
    background-color: #007bff;
    color: white;
}

Plik script.js (obsługa płatności Stripe):

const stripe = Stripe("YOUR_PUBLIC_STRIPE_KEY");

document.getElementById("buyButton").addEventListener("click", () => {
    fetch("/create-checkout-session", { method: "POST" })
        .then(response => response.json())
        .then(session => {
            return stripe.redirectToCheckout({ sessionId: session.id });
        })
        .catch(error => console.error("Błąd:", error));
});
