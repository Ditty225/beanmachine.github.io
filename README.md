 # beanmachine.github.io
<html>
<head>
  <title>Menu Calculator</title>
    <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 250vh;
      text-align: center;
    }
	.total-box {
		display: flex;
		justify-content: center; /* Center horizontally */
		align-items: center; /* Center vertically */
		margin-top: 20px;
	}}
	
	 .calculate-button {
      width: 150px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
    }
	
	.submit-button {
      width: 150px; /* Adjust the desired width */
      height: 40px; /* Adjust the desired height */
    }
	
	.reset-button {
      width: 150px; /* Adjust the desired width */
      height: 30px; /* Adjust the desired height */
    }
    
    h1 {
      margin-bottom: 20px;
    }
    
    h2 {
      margin-top: 20px;
    }
	
	h3 {
      border: 1px solid yellow; /* Adjust the border style as needed */
      padding: 5px; /* Add padding to create space around the heading */
    }
    
    .menu-items {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      gap: 10px;
      margin-bottom: 10px;
    }
    
    .menu-items div {
      display: flex;
      align-items: center;
    }
    
    .total-box {
      display: flex;
      justify-content: flex-end;
      align-self: Center;
      margin-top: 20px;
    }
    
    .button-container {
      display: flex;
      gap: 10px;
      margin-top: 20px;
    }
	
	.menu-items div img {
      width: 50px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
      margin-left: 10px; /* Add margin as per your preference */
    }
    {
    button {
      margin-top: 20px;
	}}}}}}
  </style>
  <script>
    function calculateTotal() {
    var total = 0;
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');

    checkboxes.forEach(function(checkbox) {
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);

      if (checkbox.value === '-25%') {
        var itemPrice = total * 0.25;
        total -= itemPrice;
      } else if (checkbox.value === '-30%') {
        var itemPrice = total * 0.3;
        total -= itemPrice;
      } else if (checkbox.value === '-50%') {
        var itemPrice = total * 0.5;
        total -= itemPrice;
      } else {
        total += price * quantity;
      }
    });

    var totalElement = document.getElementById('total');
    totalElement.textContent = total.toFixed(2);

    var discountTotalElement = document.getElementById('discount-total');
    var discount = total * 0.15;
    discountTotalElement.textContent = discount.toFixed(2);
  }


    
    function submitOrder() {
    var name = document.getElementById('name').value;
    if (name.trim() === '') {
      alert('Please enter a name.');
      return;
    }

    // Collect selected items and their quantities
    var selectedItems = [];
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');
    checkboxes.forEach(function (checkbox) {
      var itemName = checkbox.nextElementSibling.textContent;
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);
      selectedItems.push({ name: itemName, quantity: quantity, price: price });
    });

    var total = 0;
    var discountTotal = 0;

    selectedItems.forEach(function (item) {
      if (item.price < 0) {
        var discountPercentage = Math.abs(item.price);
        var itemDiscount = total * (discountPercentage / 100);
        discountTotal += itemDiscount;
      } else {
        total += item.price * item.quantity;
      }
    });

    var commission = (total * 0.15).toFixed(2);
    var totalWithDiscount = total - discountTotal;

    alert('Order submitted!');

    var discordWebhookURL = 'https://discordapp.com/api/webhooks/1173564535135797248/n8UdySNPs50mEqFRjPJgk7dTEjE8QEA8qwM4-gepUTgobePZK_JjPH2nwTkRt9RrrV72';

    var xhr = new XMLHttpRequest();
    xhr.open('POST', discordWebhookURL, true);
    xhr.setRequestHeader('Content-Type', 'application/json');

    var message = {
      content: 'New order!',
      embeds: [{
        title: 'Order Details',
        fields: [
          {
            name: 'Name',
            value: name,
            inline: true
          },
          {
            name: 'Total',
            value: '%' + totalWithDiscount.toFixed(2),
            inline: true
          },
          {
            name: 'Discount Total',
            value: '%' + discountTotal.toFixed(2),
            inline: true
          },
          {
            name: 'Commission (15%)',
            value: '$' + commission,
            inline: true
          },
          {
            name: 'Ordered Items',
            value: selectedItems.map(item => `${item.name} x${item.quantity} - $${(item.price * item.quantity).toFixed(2)}`).join('\n'),
            inline: false
          }
        ]
      }]
    };

    xhr.send(JSON.stringify(message));
  }

function resetCalculator() {
  var checkboxes = document.querySelectorAll('input[type="checkbox"]');
  var quantityInputs = document.querySelectorAll('input[type="number"]');
  
  checkboxes.forEach(function(checkbox) {
    checkbox.checked = false;
  });
  
  quantityInputs.forEach(function(quantityInput) {
    quantityInput.value = 1;
  });
  
  document.getElementById('total').textContent = '0.00';
}
	function submitAndReset() {
	submitOrder();
	resetCalculator();
}

  </script>
</head>
<body>
	
<div style="margin-bottom: 25px;"></div>
 
<body style="background-color:white;">
	<img src="beanmachiine.png" alt="Company Logo!">
  <h1>The Bean Machine Calculator</h1>
  
  <h2>Menu Items</h2>

  <div style="margin-bottom: 10px;"></div>
  
  <h3>Drinks</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="125$">
    <label for="Velmachoice">Espresso - 125$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">The Bean - 150$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="125$">
    <label for="Davechoice">Orange Smoothie - 125$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="125$">
    <label for="Davechoice">Vegi Smoothie - 125$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="100$">
    <label for="Davechoice">Lemonade - 100$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="50$">
    <label for="Davechoice">Coke - 50$</label>
    <input type="number" value="1" min="1">
  </div>

<h3>Food</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="100$">
    <label for="Velmachoice">Ham Sandwich - 100$</label>
    <input type="number" value="1" min="1">
  </div>
  
<div>
    <input type="checkbox" id="uwueats" value="100$">
    <label for="Velmachoice">Beef Sandwich - 100$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="100$">
    <label for="Velmachoice">BLT Sandwich - 100$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="100$">
    <label for="Velmachoice">Turkey Sandwich - 100$</label>
    <input type="number" value="1" min="1">
  </div>

  <h3>Desserts Menu</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="75$">
    <label for="Velmachoice">Carrot Cake  - 75$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="75$">
    <label for="Velmachoice">Chocolate Muffin  - 75$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="75$">
    <label for="Velmachoice">Blueberry Muffin  - 75$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="75$">
    <label for="Velmachoice">Millionaire Shortbread  - 75$</label>
    <input type="number" value="1" min="1">
  </div>

<h3>Espresso Deals</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="1000$">
    <label for="Velmachoice">10 Espresso - 1000$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="2000$">
    <label for="Velmachoice">20 Espresso - 2000$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="3000$">
    <label for="Velmachoice">30 Espresso - 3000$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="5000$">
    <label for="Velmachoice">50 Espresso - 5000$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="8500$">
    <label for="Velmachoice">100 Espresso - 8500$</label>
    <input type="number" value="1" min="1">
  </div>

<h3>The Bean Deals</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="1000$">
    <label for="Velmachoice">10 House Blend - 1000$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="2500$">
    <label for="Velmachoice">20 House Blend - 2500$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="3500$">
    <label for="Velmachoice">30 House Blend - 3500$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="6000$">
    <label for="Velmachoice">50 House Blend - 6000$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="9500$">
    <label for="Velmachoice">100 House Blend -9500$</label>
    <input type="number" value="1" min="1">
  </div>

<h3>Gem Meals</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="1500$">
    <label for="Velmachoice">Breakfast Meal - 1500$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="2500$">
    <label for="Velmachoice">Ruby Meal - 2500$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="uwueats" value="2500$">
    <label for="Velmachoice">Diamond Meal - 2500$</label>
    <input type="number" value="1" min="1">
  </div>

<h3>Special's</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="450$">
    <label for="Velmachoice">Ditty's - 450$</label>
    <input type="number" value="1" min="1">
  </div>
  

  <h3> Discount Items</h3> 

<div>
  <input type="checkbox" id="50off" value="-50%">
  <label for="50off">Employee Discount - 50% off</label>
  <input type="number" value="1" min="1" max="1">
</div>


<div>
    <label for="name">Baristas Name:</label>
    <input type="text" id="name">
  </div>
  

<div style="margin-bottom: 25px;"></div>
 
<div class="total-box">
  <span>Total: $</span>
  <span id="total">0.00</span>
</div>

<div class="total-box">
  <span>Commision (15%): $</span>
  <span id="discount-total">0.00</span>
</div>




  <div style="margin-bottom: 45px;"></div>
  

  <button class="calculate-button" onclick="calculateTotal()">Calculate Total</button>
  <button class="submit-button" onclick="submitAndReset()">Submit Order</button>
  <button class="reset-button" onclick="resetCalculator()">Reset</button>

 
  
  
  <div style="margin-bottom: 10px;"></div>
