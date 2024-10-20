# Sentiment analysis of Udemy reviews

```ruby
require 'csv'

file_path = "db/data/Udemy_Reviews_Export_2024-10-20_20-13-07.csv"

# CSV: get an array of all ratings

ratings = []

CSV.foreach(file_path, headers: true) do |row|
  rating = row['Rating']
  ratings << rating.to_f unless rating.nil?
end

average_rating = ratings.sum / ratings.size

average_rating.round(2)

# CSV: get an array of all comments

comments = []

CSV.foreach(file_path, headers: true) do |row|
  comment = row['Comment']
  comments << comment unless comment.nil? || comment.strip.empty?
end

# Get average sentiment

sentiment_counts = { positive: 0, negative: 0, neutral: 0 }

comments.each do |comment|
  sentiment = analyzer.sentiment(comment)
  sentiment_counts[sentiment] += 1
end

# sentiment_counts
# => {:positive=>87, :negative=>16, :neutral=>10}

# Get average score

total_score = 0.0

comments.each do |comment|
  score = analyzer.score(comment)
  total_score += score
end

average_score = total_score / comments.size

# average_score
# => 1.0640205752212393
```
