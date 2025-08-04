# our
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>THINK TITLE</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet"/>
  <style>
    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(to bottom right, #e6f0ff, #ffffff);
    }
    .chat-bubble {
      animation: fadeIn 0.3s ease-in-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
  </style>
</head>
<body class="text-gray-800">

  <header class="bg-blue-700 text-white py-4 shadow-md">
    <div class="max-w-6xl mx-auto px-4 flex justify-between items-center">
      <h1 class="text-2xl font-bold tracking-wide">SHOPIFY.COM</h1>
      <a href="#" class="bg-white text-blue-700 px-4 py-2 rounded-md font-semibold hover:bg-blue-100 transition">Premium Access 💎</a>
    </div>
  </header>

  <main class="max-w-4xl mx-auto px-4 py-10">
    <section class="mb-6">
      <h2 class="text-2xl font-semibold mb-4">💬 Chat with Us</h2>
      <div id="chat-window" class="bg-white p-4 rounded-lg border h-80 overflow-y-auto mb-4 space-y-3 shadow">
        <div class="chat-bubble bg-blue-100 px-4 py-2 rounded-md w-max">Hey! Ask me anything about your order or products!</div>
      </div>
      <div class="flex gap-2">
        <input id="chat-input" type="text" placeholder="Type something like 'I need a watch for ₹250'..." class="flex-1 px-4 py-2 border rounded-md" />
        <button onclick="sendMessage()" class="bg-blue-700 text-white px-4 py-2 rounded-md hover:bg-blue-800 transition">Send</button>
      </div>
    </section>
  </main>

  <footer class="text-center py-6 text-sm text-gray-500">
    © 2025 ShopHub. Shopping is Simple with us! 💙.
  </footer>

  <script>
    const chat = document.getElementById("chat-window");

    const products = [
      {
        name: "Black Analog Watch",
        price: 250,
        category: "watch",
        rating: 4.5,
        img: "https://images.unsplash.com/photo-1511376777868-611b54f68947",
        link: "https://shopify.com/fake-watch-link"
      },
      {
        name: "Stylish Bedcover Set",
        price: 499,
        category: "bedcover",
        rating: 4.7,
        img: "https://images.unsplash.com/photo-1616627981904-dcc3b2bb64fa",
        link: "https://shopify.com/fake-bedcover-link"
      },
      {
        name: "Bluetooth Earbuds",
        price: 799,
        category: "earbuds",
        rating: 4.3,
        img: "https://images.unsplash.com/photo-1577641785731-f6dbf3f5c0e2",
        link: "https://shopify.com/fake-earbuds-link"
      }
    ];

    function generateStars(rating) {
      const fullStars = Math.floor(rating);
      const halfStar = rating % 1 >= 0.5 ? '⭐️' : '';
      return '⭐️'.repeat(fullStars) + halfStar;
    }

    function sendMessage() {
      const input = document.getElementById("chat-input");
      const userText = input.value.trim();

      if (!userText) return;

      // Add user message
      const userBubble = document.createElement("div");
      userBubble.className = "chat-bubble bg-blue-200 px-4 py-2 rounded-md w-max ml-auto";
      userBubble.innerText = userText;
      chat.appendChild(userBubble);
      input.value = "";

      // Bot typing...
      setTimeout(() => {
        const botBubble = document.createElement("div");
        botBubble.className = "chat-bubble bg-gray-100 px-4 py-2 rounded-md w-max";

        const lower = userText.toLowerCase();
        let found = false;

        // Order status
        if (lower.includes("where") && lower.includes("order")) {
          botBubble.innerText = "Your order is being packed right now at our warehouse 🏭. Estimated delivery: 2 days 🚚";
        }
        else {
          for (let p of products) {
            if (lower.includes(p.category) || lower.includes(p.name.toLowerCase()) || lower.includes(p.price.toString())) {
              found = true;
              botBubble.innerHTML = `
                Here's something you’ll love 😍:<br>
                <strong>${p.name}</strong><br>
                Price: ₹${p.price}<br>
                Rating: ${generateStars(p.rating)}<br>
                <a class="text-blue-600 underline" href="${p.link}" target="_blank">View on Shopify</a><br>
                <img src="${p.img}" alt="${p.name}" class="w-32 h-32 mt-2 rounded-md"/>
              `;
              break;
            }
          }
          if (!found) {
            botBubble.innerText = "Oops 😔 I couldn’t find that. Try something like 'bedcover', 'earbuds', or a budget 💰";
          }
        }

        chat.appendChild(botBubble);
        chat.scrollTop = chat.scrollHeight;
      }, 800);
    }
  </script>

</body>
</html>
