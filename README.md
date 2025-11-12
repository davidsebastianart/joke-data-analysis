# Joke Data Analysis: Uncovering Humor Patterns

This project performs a comprehensive analysis of a joke dataset sourced from a public API. The analysis includes data acquisition, cleaning, exploratory data analysis (EDA), and advanced text analysis to understand the characteristics, distribution, and common linguistic patterns within the jokes.

## 1. Data Acquisition

The first step was to gather data from the `[https://github.com/15Dkatz/official_joke_api](https://github.com/15Dkatz/official_joke_api)`.

* **Method:** Data was fetched using the Python `requests` library by calling the `/jokes/random/250` endpoint.
* **Process:** The API has a limit of 250 jokes per request. To obtain a more substantial dataset for analysis, the acquisition process was performed twice.
* **Result:** Two data batches (each containing 250 jokes) were successfully retrieved and saved into two separate CSV files (`jokes_data_1.csv` and `jokes_data_2.csv`).

## 2. Data Preparation & Cleaning

The raw data was then prepared for analysis.

* **Data Merging:** The two CSV files were read into `pandas` and concatenated into a single DataFrame (`jokes_df`) with 500 total entries.
* **Initial Inspection:** An initial check using `.info()` and `.isnull().sum()` showed the dataset had 500 rows and 4 columns (`type`, `setup`, `punchline`, `id`). All columns were non-null, indicating no missing values.
* **Deduplication:** A crucial cleaning step was removing duplicates. Jokes with identical `setup` and `punchline` combinations were identified and dropped.
* **Final Dataset:** After deduplication, the number of unique jokes was reduced from 500 to **371**. All subsequent analysis was based on this cleaned dataset.

## 3. Exploratory Data Analysis (EDA) & Visualization

With the clean data, we proceeded to uncover insights.

### a. Joke Type Distribution

* **Analysis:** We calculated the frequency of occurrence for each joke `type`.
* **Finding:** The dataset is heavily dominated by **'general'** jokes (312 out of 371). **'programming'** jokes (53) were a distant second, while 'knock-knock' (4) and 'dad' (2) jokes were rare.
* **Visualization:** A `seaborn` bar chart was created to visualize this distribution, clearly highlighting the skew across categories.

### b. Text Length Analysis

* **Analysis:** Two new feature columns (`setup_length` and `punchline_length`) were engineered to store the character length of each joke part.
* **Finding:**
    * **Setup:** Setups are generally longer, with a distribution centered around 40-50 characters.
    * **Punchline:** Punchlines are significantly shorter and more concise, with most falling in the 20-30 character range.
* **Visualization:** This insight was supported by histograms and box plots, showing the classic "moderate setup, brief punchline" structure.

### c. Advanced Text Analysis: Word Frequency

* **Method:** To identify common themes, a word frequency analysis was performed. Text from the `setup` and `punchline` columns was preprocessed (lowercased, punctuation removed, and common English stopwords removed).
* **Setup Findings:** The most common setup words include **'call'**, **'does'**, **'hear'**, and **'whats'**. This indicates many jokes are formatted as questions or "what do you call..." scenarios.
* **Punchline Findings:** The word **'because'** was by far the most dominant punchline word. This suggests that punchlines often serve as the explanatory or unexpected answer to the setup's question.
* **Visualization:** Two bar charts were generated to compare the top 20 words for both setups and punchlines.

## 4. Summary & Conclusion

This analysis successfully uncovered several key characteristics of the joke dataset:

1.  **Data Quality:** The deduplication process was critical, reducing the dataset by 25.8% (from 500 to 371) and ensuring the validity of the analysis.
2.  **Joke Composition:** The dataset primarily consists of 'general' jokes (84% of the unique data).
3.  **Joke Structure:** A clear pattern emerged where setups (avg. 40-50 chars) are consistently longer than punchlines (avg. 20-30 chars).
4.  **Linguistic Patterns:** Jokes are often structured as question-and-answer. Setups use inquisitive words ("whats," "does"), and punchlines provide an explanation, often starting with "because."

### Recommended Next Steps

* Perform sentiment analysis to rate the "darkness" or "lightness" of the jokes.
* Analyze the correlation between joke type and text length.
* Use this dataset as baseline training data for a text-generation (NLP) model to create new jokes.

## 5. Tools & Libraries Used

* **Python**
* **Pandas:** For data manipulation and cleaning.
* **Requests:** For API data acquisition.
* **Matplotlib & Seaborn:** For data visualization.
* **Re (Regex) & Collections:** For text processing and frequency analysis.
