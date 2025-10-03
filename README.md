Electronics Store

A full-featured e-commerce store built with Vue.js 3 and Bootstrap 5 for selling electronic products with a complete authentication system, shopping cart, and wishlist management.

🌟 Features
Authentication System

User Registration: Create a new account with data stored in Firebase

Login: Authenticate users with email and password

Protected Pages: All pages are protected and only accessible after login

Logout: Option to log out of the account

Product Management

View Products: Display all products with images, prices, and details

Product Categories: Categorize products by type (Smartphones, Laptops, Tablets, etc.)

Filter by Brand: Filter products by brand (Apple, Samsung, Dell, etc.)

Advanced Search: Search by product names, categories, and brands

Auto Filter Selection: When searching, the matching filter is automatically selected in the sidebar

Shopping Cart

Add to Cart: Add products to the shopping cart

Manage Quantity: Increase or decrease product quantities in the cart

Remove from Cart: Remove products from the cart

Calculate Total: Automatically calculate the total price

Save Cart: Save cart contents in localStorage

Wishlist

Add to Wishlist: Add favorite products by clicking the heart icon

Wishlist Page: View all favorited products in a dedicated page

Remove from Wishlist: Remove products from the wishlist

Wishlist Counter: Show the number of favorited products in the Header

User Interface

Responsive Design: Works on all devices (Mobile, Tablet, Desktop)

Bootstrap 5: Built with Bootstrap for styling and layout

Easy Navigation: Clear navigation bar in the Header

Professional Icons: Uses Bootstrap Icons

🛠️ Technologies Used

Vue.js 3 – Main framework

Vue Router – Page routing

Pinia – State management

Bootstrap 5 – UI styling

Bootstrap Icons – Icons library

Firebase API – User data and authentication storage

localStorage – Store cart and wishlist locally

📁 Project Structure
electronics-store/
├── public/
│ └── index.html
├── src/
│ ├── assets/
│ │ └── style.css
│ ├── components/
│ │ ├── CategoryCard.vue
│ │ ├── FooterComponent.vue
│ │ ├── HeaderComponent.vue
│ │ └── ProductCard.vue
│ ├── router/
│ │ └── index.js
│ ├── store/
│ │ ├── authStore.js
│ │ ├── cartStore.js
│ │ └── productsStore.js
│ ├── views/
│ │ ├── CartPage.vue
│ │ ├── FavoritesPage.vue
│ │ ├── HomePage.vue
│ │ ├── LoginPage.vue
│ │ ├── ProductDetailsPage.vue
│ │ ├── ProductsPage.vue
│ │ └── SignupPage.vue
│ ├── App.vue
│ └── main.js
├── package.json
└── README.md

🚀 Installation & Running
Requirements

Node.js (v14 or later)

npm or yarn

Steps

Clone the repository

git clone <repository-url>
cd electronics-store

Install dependencies

npm install

Run in development mode

npm run serve

Open in browser
Go to: http://localhost:8080

Build for production
npm run build

⚙️ Configuration
Firebase API

The project uses Firebase API to store user data. Current API endpoint:

https://vue-test-e0e1e-default-rtdb.firebaseio.com/users.json

To change the API endpoint:

Open src/store/authStore.js

Search for apiUrl

Replace the URL with your Firebase API

Customizing Products

To add or edit products:

Open src/store/productsStore.js

Edit the products array in the state

Add new products or edit existing ones

Example product structure:

{
id: 1,
name: 'iPhone 14 Pro',
price: 999,
image: '/placeholder.svg?height=200&width=200',
category: 'Smartphones',
brand: 'Apple',
description: 'Product description here',
rating: 4.5
}

📖 User Guide
For New Users

Sign Up

Click "Sign Up" in the Header

Enter name, email, and password

Click "Register"

Log In

Click "Login" in the Header

Enter email and password

Click "Login"

Browse Products

From Home, click on any category

Or go directly to the "Products" page

Search for Products

Use the search bar in the Header

Type product name, category, or brand

Press Enter or click the search button

Add to Cart

Click "Add to Cart" on the product card

Or go to the product details page and click "Add to Cart"

Add to Wishlist

Click the heart icon on the product card

View favorites by clicking the heart icon in the Header

Manage Cart

Click the cart icon in the Header

Increase or decrease quantity

Remove products from the cart

🎨 Customization
Colors

Edit src/assets/style.css to change colors:

:root {
--primary-color: #007bff;
--secondary-color: #6c757d;
--success-color: #28a745;
--danger-color: #dc3545;
--warning-color: #ffc107;
}

Fonts

Edit src/assets/style.css to change fonts:

body {
font-family: 'Arial', sans-serif;
}

🔒 Security

All pages are protected by authentication

No page is accessible without login

Passwords are stored in Firebase

Local data (cart & wishlist) is stored in localStorage

📝 Notes

Project uses demo product data

Images are placeholders

Can be connected to a real API for product management

Payment gateway integration can be added

🤝 Contribution

Feel free to contribute:

Fork the repo

Create a new branch (git checkout -b feature/AmazingFeature)

Commit changes (git commit -m 'Add some AmazingFeature')

Push to branch (git push origin feature/AmazingFeature)

Open a Pull Request

📄 License

This project is open-source and free to use.

📞 Contact

If you have any questions or suggestions, feel free to get in touch.

Built with ❤️ using Vue.js & Bootstrap
