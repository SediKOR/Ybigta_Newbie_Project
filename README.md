# Ybigta_Newbie_Project : Context-based profanity filtering

## Project Direction
  - **Goal**: Implement a profanity filter for game domain chats  
    (e.g., "씨발" -> "**", "수박씨발라먹어" -> "수박씨발라먹어")
  - However, due to practical constraints, we worked with the available resources as much as possible.
	- Using a profanity dataset, we labeled profanity and non-profanity as 1 and 0, respectively.
	- We intended to use game chat data, but due to copyright issues, we built the dataset by crawling comments from the gaming site 'Inven.'
	- We implemented a homepage that fetches comments in real time and blinds them when they contain contextual profanity.

## Why Implement Chat Filtering?
  - It’s important to maintain a healthy environment in game chat.
  - Healthy chat is informative, fosters knowledge sharing, and provides learning opportunities.
  - It promotes diversity and inclusion by creating a positive chat environment for young people as they grow.
  - Building a profanity-free community prevents unnecessary conflict.
  - Therefore, censoring profanity and labeling words appropriately as safe is crucial.

### The Challenge of Judging Profanity and Implementing Filtering
  - This challenge arises from the nature of the Korean language.  
    There are sentences that are not profane but sound similar to profanity (e.g., "조카크레파스18색").
  - We trained the model by focusing on hard positive sentences (actual profanity) and hard negative sentences (non-profane words that sound like profanity).

## Dataset
  - We created a dataset of profanity and non-profanity (137,830 entries in total).
  - Due to the difficulty of obtaining chat data, we built the dataset using article comments and corporate datasets for profanity classification.
  - Profanity accounted for 65.05% of the total data.

## Model
  - Due to the domain requirements, we needed a model that could understand Korean well. Hence, we used KoBERT, a pre-trained language model.
  - We adapted the sentiment analysis model architecture from KoBERT, modifying it to suit our task.
  - To enhance the model's performance and prevent overfitting, we added a dense layer and applied the dropout technique.

## Hyperparameter Adjustment
  - We encountered low validation accuracy and adjusted several hyperparameters to improve performance (learning rate, warmup proportion, dropout, etc.).

## Optimization Process
  - We optimized the task by adjusting activation functions, epochs, steps, random seed, etc.

- Within two weeks, training performance improved by more than 50 times.
- The final model demonstrated strong performance without overfitting compared to the initial version.

## Real-World Application Results
  - Initial model accuracy: ~50%
  - Our model's accuracy: ~75%
  - Verification was conducted by randomly selecting hard positive, soft positive, soft negative, and hard negative samples.
	- For negative samples, both soft and hard profanity classification performed well.
	- For positive samples, the model achieved about 57% accuracy, with lower performance in detecting English profanity, phonological profanity, and non-written forms.
	- Still, our model outperformed existing models.

## Crawling
  - Due to the difficulty of applying a filtering model to chat data, we collected in-box comments and tested our model with them.
  - We collected data by randomly fetching 3 comments per post from the top 10 posts on a given topic.
  - Static and dynamic crawling were executed in parallel to improve speed.
  - Randomized selection was used to avoid bias toward specific posts.
  - We collected details that could be utilized as text data:
	- Efficient dynamic crawling and parallel processing were employed for faster crawling and end-to-end model application.
    - We improved the homepage by comparing error handling and the time required.
  - We implemented the site using React and Firebase as the database. The site design was inspired by Inven, with a profanity filtering toggle that allowed users to block comments with profanity.

## How It Works
  - Our model can be applied to the gaming domain in a similar role to NAVER Cleanbot, which works with an LSTM-based ELMO model.
  - Contributing to fostering a positive gaming culture and creating a safe community is essential, especially as toxic language often affects gaming environments.
  - By addressing shortcomings in our model and tracking a decrease in abusive content exposure after applying Cleanbot, we aim to enhance filtering capabilities in the gaming industry and improve its public perception.

## Limitations
  - To implement an efficient filtering function, further dataset improvements and accurate labeling are needed. Fast loading speed is also essential.
  - The dataset needs more diversity in terms of profanity inclusion criteria, and additional data is required.
