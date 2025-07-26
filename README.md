# Codealpha-stock
# Hardcoded stock prices
stock_prices = {
    "AAPL": 180,
    "TSLA": 250,
    "GOOGL": 2700,
    "AMZN": 3400
}

def calculate_investment():
    total_investment = 0
    user_stocks = {}

    while True:
        stock = input("Enter stock name (or 'done' to finish): ").upper()
        if stock == 'DONE':
            break
        if stock not in stock_prices:
            print("Stock not available. Try again.")
            continue

        try:
            quantity = int(input(f"Enter quantity for {stock}: "))
        except ValueError:
            print("Invalid quantity. Enter an integer.")
            continue

        user_stocks[stock] = quantity
        total_investment += stock_prices[stock] * quantity

    print(f"\nTotal Investment: ${total_investment}")

    # Optionally save to file
    save = input("Do you want to save the result to a file? (yes/no): ").lower()
    if save == 'yes':
        with open("investment_summary.csv", "w") as file:
            file.write("Stock,Quantity,Price per Stock,Total Value\n")
            for stock, qty in user_stocks.items():
                total_value = stock_prices[stock] * qty
                file.write(f"{stock},{qty},{stock_prices[stock]},${total_value}\n")
            file.write(f"\nTotal Investment: ${total_investment}\n")
        print("Summary saved to investment_summary.csv")

if __name__ == "__main__":
    calculate_investment()
