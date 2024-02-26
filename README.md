class Website:
    def __init__(self, name):
        self.name = name
        self.goods = []
        self.users = {}
        self.cart = {}

    def post_goods(self, goods):
        self.goods.append(goods)

    def create_account(self, username, password):
        if username not in self.users:
            self.users[username] = password
            print(f"Account created for {username}")
        else:
            print("Username already exists. Please choose a different one.")

    def login(self, username, password):
        if username in self.users and self.users[username] == password:
            print(f"Welcome back, {username}!")
            return True
        else:
            print("Invalid username or password.")
            return False

    def add_to_cart(self, username, goods):
        if goods in self.goods:
            if username not in self.cart:
                self.cart[username] = []
            self.cart[username].append(goods)
            print(f"{goods} added to cart.")
        else:
            print(f"{goods} not found.")

    def checkout(self, username):
        if username in self.cart:
            total_price = 0
            for item in self.cart[username]:
                total_price += self.get_item_price(item)
            print(f"Total price: ${total_price}")
            del self.cart[username]
            print("Checkout successful. Thank you for your purchase!")
        else:
            print("Your cart is empty.")

    def get_item_price(self, item):
        # Add logic to fetch price for each item from a database or API
        return 10  # Dummy price for demonstration purposes

# Creating an instance of the website
nonsoglobalventure = Website("nonsoglobalventure")

# Posting goods on the website
nonsoglobalventure.post_goods("Product A")
nonsoglobalventure.post_goods("Product B")

# Creating user accounts
nonsoglobalventure.create_account("john", "password123")
nonsoglobalventure.create_account("emma", "password456")

# Logging in and adding items to cart
nonsoglobalventure.login("john", "password123")
nonsoglobalventure.add_to_cart("john", "Product A")
nonsoglobalventure.checkout("john")

# Invalid login attempt
nonsoglobalventure.login("mike", "password789")
