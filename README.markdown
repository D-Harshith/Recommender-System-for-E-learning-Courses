# E-Learning Course Recommendation System

## Project Overview
This project implements a content-based recommendation system for e-learning courses using a dataset from Coursera. The system recommends courses based on similarity in course names, descriptions, skills, and difficulty levels. It leverages natural language processing (NLP) techniques, including text preprocessing, stemming, and vectorization, to create a similarity matrix for course recommendations.

## Dataset
The dataset (`Coursera.csv`) contains information about Coursera courses with the following columns:
- **Course Name**: Name of the course.
- **University**: Institution offering the course.
- **Difficulty Level**: Course difficulty (e.g., Beginner, Intermediate, Advanced).
- **Course Rating**: Numerical rating of the course.
- **Course URL**: URL to the course page.
- **Course Description**: Description of the course content.
- **Skills**: Skills associated with the course.

For the recommendation system, only `Course Name`, `Difficulty Level`, `Course Description`, and `Skills` are used, as `University`, `Course Rating`, and `Course URL` were deemed irrelevant or potentially biased.

## Dependencies
- Python 3.11
- Libraries:
  - `pandas`
  - `numpy`
  - `matplotlib`
  - `nltk`
  - `scikit-learn`

Install dependencies using:
```bash
pip install pandas numpy matplotlib nltk scikit-learn
```

Download NLTK data:
```python
import nltk
nltk.download('punkt')
```

## Methodology
1. **Data Preprocessing**:
   - Selected relevant columns: `Course Name`, `Difficulty Level`, `Course Description`, and `Skills`.
   - Replaced spaces with commas in `Course Name` and `Course Description` for consistency.
   - Removed special characters (e.g., parentheses, colons) from `Course Description` and `Skills`.
   - Created a `tags` column by concatenating `Course Name`, `Difficulty Level`, `Course Description`, and `Skills`.
   - Replaced commas with spaces in `tags` and `Course Name`, converted `tags` to lowercase, and applied stemming using NLTK's Porter Stemmer.

2. **Vectorization**:
   - Used `CountVectorizer` from `scikit-learn` with a maximum of 5,000 features and English stop words removed to convert `tags` into a numerical matrix.
   - Computed a cosine similarity matrix to measure similarity between courses.

3. **Recommendation Function**:
   - The `recommend` function takes a course name as input, finds its index in the dataset, and retrieves the top 6 most similar courses based on cosine similarity scores.
   - Handles cases where the input course is not found by listing available course names.

## Usage
1. Ensure the dataset (`Coursera.csv`) is in the same directory as the script.
2. Run the Jupyter Notebook (`Recommender System for E-learning Courses.ipynb`).
3. The script will output recommendations for the specified course or list available courses if the input is not found.

## Example Output
For the input `Introduction to Cybersecurity Tools & Cyber Attacks`:
```
Recommendations for 'Introduction to Cybersecurity Tools & Cyber Attacks':
Cybersecurity Roles Processes & Operating System Security
Cyber Threat Intelligence
Penetration Testing Incident Response and Forensics
[Additional similar courses...]
```

If the course is not found:
```
Course 'Invalid Course Name' not found in the dataset.
Available courses: ['Write A Feature Length Screenplay For Film Or Television', 'Business Strategy Business Model Canvas Analysis with Miro', ...]
```

## Notes
- Ensure the course name matches exactly (case-sensitive) with the `course_name` column in `new_df`. Use `new_df['course_name'].values` to check available names.
- The system uses `CountVectorizer` for simplicity, but `TfidfVectorizer` could be explored for potentially better results.
- The dataset contains 3,522 courses, covering various domains and difficulty levels.

## Future Improvements
- Incorporate additional features (e.g., `Difficulty Level`) into the similarity metric.
- Use more advanced NLP techniques, such as TF-IDF or word embeddings, for better text representation.
- Add a user interface (e.g., web app) for easier interaction with the recommendation system.
