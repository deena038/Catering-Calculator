<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Catering Calculator - Dish Breakdown</title>

<style>
    body {
        font-family: Arial, sans-serif;
        background: #f4f6f8;
        padding: 20px;
    }
    .container {
        max-width: 500px;
        margin: auto;
        background: white;
        padding: 20px;
        border-radius: 12px;
        box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
    h2 {
        text-align: center;
    }
    input {
        width: 100%;
        padding: 10px;
        margin: 6px 0;
        border: 1px solid #ccc;
        border-radius: 8px;
    }
    .dish {
        background: #f9f9f9;
        padding: 10px;
        margin-bottom: 10px;
        border-radius: 10px;
    }
    button {
        width: 100%;
        padding: 12px;
        margin-top: 10px;
        background: #28a745;
        color: white;
        border: none;
        border-radius: 8px;
        font-size: 16px;
    }
    button:hover {
        background: #218838;
    }
    .result {
        margin-top: 15px;
        padding: 10px;
        background: #e9f7ef;
        border-radius: 8px;
    }
</style>
</head>

<body>

<div class="container">
    <h2>Catering Calculator</h2>

    <div id="dishes">

        <div class="dish">
            <input type="text" placeholder="Dish name (e.g. Fish Fry)" class="name">
            <input type="number" placeholder="Ingredient cost ($)" class="cost">
        </div>

    </div>

    <button onclick="addDish()">+ Add Another Dish</button>

    <label>Labor Cost ($)</label>
    <input type="number" id="labor">

    <label>Other Expenses ($)</label>
    <input type="number" id="other">

    <label>Profit Margin (%)</label>
    <input type="number" id="margin">

    <button onclick="calculate()">Calculate Total</button>

    <div class="result" id="result"></div>
</div>

<script>
function addDish() {
    let div = document.createElement("div");
    div.className = "dish";
    div.innerHTML = `
        <input type="text" placeholder="Dish name" class="name">
        <input type="number" placeholder="Ingredient cost ($)" class="cost">
    `;
    document.getElementById("dishes").appendChild(div);
}

function calculate() {
    let names = document.getElementsByClassName("name");
    let costs = document.getElementsByClassName("cost");

    let totalIngredients = 0;
    let breakdown = "";

    for (let i = 0; i < costs.length; i++) {
        let name = names[i].value || "Dish " + (i + 1);
        let cost = parseFloat(costs[i].value) || 0;

        totalIngredients += cost;
        breakdown += `${name}: $${cost.toFixed(2)}<br>`;
    }

    let labor = parseFloat(document.getElementById("labor").value) || 0;
    let other = parseFloat(document.getElementById("other").value) || 0;
    let margin = parseFloat(document.getElementById("margin").value) || 0;

    let totalCost = totalIngredients + labor + other;
    let profit = (totalCost * margin) / 100;
    let sellingPrice = totalCost + profit;

    document.getElementById("result").innerHTML = `
        <b>Breakdown:</b><br>${breakdown}<br>
        <hr>
        <b>Ingredients Total:</b> $${totalIngredients.toFixed(2)}<br>
        <b>Labor:</b> $${labor.toFixed(2)}<br>
        <b>Other:</b> $${other.toFixed(2)}<br>
        <b>Total Cost:</b> $${totalCost.toFixed(2)}<br>
        <b>Profit:</b> $${profit.toFixed(2)}<br>
        <b>Selling Price:</b> $${sellingPrice.toFixed(2)}
    `;
}
</script>

</body>
</html>
