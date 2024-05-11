<!--index.php-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menu and Order</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            margin: 0;
            background-color: #D8AE7E; 
        }
        .container {
            width: 400px;
            margin-top: 50px;
            text-align: center;
        }
        .menu {
            margin-bottom: 20px;
            text-align: left;
        }
        .total-cost {
            display: none;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Welcome to the Canteen!</h1>
    <p>Here are the Menu and their Prices:</p>
    <ul class="menu">
        <li>Carbonara - 70 PHP</li>
        <li>Meals w/ Rice (Any Ulam) - 80 PHP</li>
        <li>Palabok - 50 PHP</li>
        <li>Coke - 20 PHP</li>
        <li>Gulaman - 15 PHP</li>
    </ul>

    <form id="order-form" method="post" action="<?php echo $_SERVER['PHP_SELF']; ?>">
        <label for="menu">Menu:</label>
        <select id="menu" name="menu">
            <option value="Carbonara">Carbonara</option>
            <option value="Meals w/ Rice">Meals w/ Rice (Any Ulam)</option>
            <option value="Palabok">Palabok</option>
            <option value="Coke">Coke</option>
            <option value="Gulaman">Gulaman</option>
        </select><br>

        <label for="quantity">Quantity:</label>
        <input type="number" id="quantity" name="quantity" min="1" value="1"><br>

        <label for="cash">Cash:</label>
        <input type="number" id="cash" name="cash" min="0" step="0.01"><br>

        <button type="submit" id="submit-button" style="background-color: #FF5733;">Submit</button>
    </form>

    <div class="total-cost">
        <h2 id="total-cost-heading">Total Cost of the order:</h2>
        <p id="total-cost"></p>
        <h2 id="change-heading">Your Change:</h2>
        <p id="change"></p>
        <p>Thank you for Ordering! Come Back Again~</p>
    </div>
</div>

<script>
    const menuPrices = {
        "Carbonara": 70,
        "Meals w/ Rice": 80,
        "Palabok": 50,
        "Coke": 20,
        "Gulaman": 15
    };

    const orderForm = document.getElementById("order-form");
    const submitButton = document.getElementById("submit-button");
    const totalCostDiv = document.querySelector(".total-cost");
    const totalCostHeading = document.getElementById("total-cost-heading");
    const totalCostPara = document.getElementById("total-cost");
    const changeHeading = document.getElementById("change-heading");
    const changePara = document.getElementById("change");

    orderForm.addEventListener("submit", function(event) {
        event.preventDefault();
        const formData = new FormData(orderForm);
        const selectedMenu = formData.get("menu");
        const quantity = parseInt(formData.get("quantity"));
        const cash = parseFloat(formData.get("cash"));

        const totalCost = menuPrices[selectedMenu] * quantity;
        const change = cash - totalCost;

        totalCostHeading.innerHTML = "";
        totalCostPara.textContent = "";
        changeHeading.innerHTML = "";
        changePara.textContent = "";

        totalCostDiv.style.display = "block";
        submitButton.style.backgroundColor = "#66CC66"; 

        const resultWindow = window.open('', '_blank');
        resultWindow.document.write('<h2>Total Cost of the order:</h2>');
        resultWindow.document.write('<p>' + totalCost + ' PHP</p>');
        resultWindow.document.write('<h2>Your Change:</h2>');
        resultWindow.document.write('<p>' + change + ' PHP</p>');
        resultWindow.document.write('<p>Thank you for Ordering! Come Back Again~</p>');
        resultWindow.document.body.style.backgroundColor = '#D8AE7E'; 

        resultWindow.focus();
    });
</script>

</body>
</html>