import pandas as pd
import matplotlib.pyplot as plt

# Step 1: Create a sample dataset (or load your own CSV)
data = {
    'Title': ['The Great Gatsby', '1984', 'Pride and Prejudice', 'The Catcher in the Rye', 'Dune', 'To Kill a Mockingbird'],
    'Author': ['F. Scott Fitzgerald', 'George Orwell', 'Jane Austen', 'J.D. Salinger', 'Frank Herbert', 'Harper Lee'],
    'Genre': ['Fiction', 'Dystopian', 'Romance', 'Fiction', 'Sci-Fi', 'Fiction'],
    'Price': [10.99, 8.99, 12.50, 9.99, 15.99, 11.49],
    'Rating': [4.2, 4.5, 4.7, 4.0, 4.8, 4.6]
}

# Create a DataFrame
df = pd.DataFrame(data)

# Step 2: Save the DataFrame to a CSV file (optional)
df.to_csv('books.csv', index=False)

# Step 3: Load the CSV file
df = pd.read_csv('books.csv')

# Step 4: Basic Data Exploration
print("Dataset Info:")
print(df.info())
print("\nFirst few rows:")
print(df.head())

# Step 5: Data Analysis
# Average price by genre
avg_price_by_genre = df.groupby('Genre')['Price'].mean().round(2)
print("\nAverage Price by Genre:")
print(avg_price_by_genre)

# Top-rated books (Rating >= 4.5)
top_rated = df[df['Rating'] >= 4.5][['Title', 'Author', 'Rating']].sort_values(by='Rating', ascending=False)
print("\nTop-Rated Books (Rating >= 4.5):")
print(top_rated)

# Step 6: Data Visualization
# Bar plot of average price by genre
avg_price_by_genre.plot(kind='bar', color='skyblue')
plt.title('Average Book Price by Genre')
plt.xlabel('Genre')
plt.ylabel('Average Price ($)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Step 7: Save the analysis results to a new CSV
df['Price_Category'] = pd.cut(df['Price'], bins=[0, 10, 15, float('inf')], labels=['Low', 'Medium', 'High'])
df.to_csv('books_analyzed.csv', index=False)
print("\nAnalysis saved to 'books_analyzed.csv'")
