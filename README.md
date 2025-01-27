import pandas as pd
from textblob import TextBlob

# Load TripAdvisor data from CSV
file_path = "[path_to_your_file.csv](../../tripadvisor_20240830184151.csv)"  # Replace with your file path
data = pd.read_csv(f[ile_path](../../tripadvisor_20240830184151.csv))

# Ensure the column containing reviews is named 'Review'
# If the column name is different, replace 'Review' with the correct column name
if 'Review' not in data.columns:
    print("Column 'Review' not found. Check your dataset for the correct column name.")
else:
    # Add new columns for polarity and subjectivity
    data['Polarity'] = data['Review'].apply(lambda x: TextBlob(str(x)).sentiment.polarity)
    data['Subjectivity'] = data['Review'].apply(lambda x: TextBlob(str(x)).sentiment.subjectivity)

    # Add a new column for sentiment classification based on polarity
    def classify_sentiment(polarity):
        if polarity > 0:
            return 'Positive'
        elif polarity < 0:
            return 'Negative'
        else:
            return 'Neutral'

    data['Sentiment'] = data['Polarity'].apply(classify_sentiment)

    # Save results to a new CSV file
    output_file = "sentiment_analysis_results.csv"
    data.to_csv(output_file, index=False)

    print(f"Sentiment analysis completed. Results saved to {output_file}.")
