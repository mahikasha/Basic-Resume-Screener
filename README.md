# Basic-Resume-Screener

The provided Python script is designed to automate the processing, extraction, and scoring of resumes from a ZIP file containing `.docx` resumes. It leverages **Natural Language Processing (NLP)** techniques and file handling utilities to evaluate candidates based on:  
1. **Work Experience** (in years)  
2. **Matching Keywords** (e.g., "machine learning," "data science").  

The program assigns a score to each candidate and outputs the results.

---

## **Functional Highlights**  

### **1. Text Preprocessing Functions**  
The script uses the NLTK library for text preprocessing tasks, such as tokenization, stopword removal, punctuation removal, and lemmatization.  
- **Tokenize**: Splits the text into words.  
- **Lowercase**: Converts all tokens to lowercase for uniformity.  
- **Remove Stopwords**: Filters out common English words like *"the," "is,"* that don't add meaning.  
- **Remove Punctuation**: Removes punctuation marks from the text.  
- **Lemmatization**: Reduces words to their root forms (e.g., *running → run*).

These steps help in cleaning and standardizing the extracted resume text for further analysis.

---

### **2. File Handling**  
The code can process resumes stored in different formats:  
- `.docx`: Uses `python-docx` to extract text.  
- `.pdf` (although not fully implemented): Placeholder for PDF reading using `PyPDF2`.  
- `.txt`: Can be added for plain text file processing.  

A **ZIP Extraction** utility extracts all files from a given ZIP archive into a temporary directory for processing.

---

### **3. Keyword and Experience Extraction**  
The program identifies and extracts two key elements from each resume:  
1. **Name**:  
   - Matches patterns like "My name is ..." or "Name: ..." using regular expressions.  
2. **Experience**:  
   - Detects phrases like *"X years of experience"* and extracts the numeric value (`X`).

---

### **4. Keyword Matching**  
A predefined list of **keywords** is checked against the resume text:  
- "machine learning"  
- "data science"  
- "python"  
- "deep learning"  
- "NLP"  
- "artificial intelligence"  
- "modeling"  

The script counts the occurrences of these keywords to evaluate the relevance of the resume.

---

### **5. Scoring Mechanism**  
The scoring function evaluates candidates based on:  
1. **Experience Score**:  
   - 70 points for **5+ years**  
   - 50 points for **3-4 years**  
   - 30 points for **1-2 years**  
   - 10 points for **less than 1 year**  
2. **Keyword Score**:  
   - Each matched keyword earns **5 points**.  
   - The total keyword score is capped at **30 points**.  

**Total Score** = **Experience Score + Keyword Score** (Max 100 points).

---

### **6. Main Pipeline**  
1. **Extract ZIP**:  
   - Extracts all resumes into a specified directory.  
2. **Read and Process Resumes**:  
   - Iterates through all `.docx` files in the extracted directory.  
   - Extracts text, processes it, and calculates scores.  
3. **Screen and Rank Candidates**:  
   - For each resume, the extracted **name, experience, keywords matched,** and **score** are outputted.  
4. **Output Results**:  
   - Displays the results on the console, including the candidate's name, experience, keywords matched, and final score.

---

## **Code Execution Flow**  
1. Install required libraries (`python-docx`, `PyPDF2`, `nltk`).  
2. Download necessary NLTK resources (`stopwords`, `wordnet`, etc.).  
3. Place the ZIP file (`Resumes.zip`) containing `.docx` resumes in the specified path.  
4. Run the script:  
   ```bash
   python resume_screening.py
   ```  
5. The results are displayed as:  
   ```python
   {'Name': 'John Doe', 'Experience (years)': 5, 'Keywords Matched': 3, 'Score': 85}
   ```

---

## **Key Functions**  

| **Function Name**           | **Purpose**                                                                 |
|-----------------------------|----------------------------------------------------------------------------|
| `tokenize()`                | Tokenizes text into words using NLTK.                                      |
| `remove_stopwords()`        | Removes common stopwords from tokens.                                      |
| `apply_lemmatization()`     | Lemmatizes tokens to their root forms.                                     |
| `extract_name_experience()` | Extracts the candidate's name and experience using regex patterns.         |
| `count_keywords()`          | Counts the occurrences of predefined keywords in the text.                 |
| `calculate_score()`         | Calculates the total score based on experience and keyword matches.        |
| `read_docx()`               | Reads and extracts text from `.docx` files.                                |
| `extract_zip()`             | Extracts all files from a ZIP archive to a directory.                      |
| `process_resumes_from_zip()`| Main pipeline to process resumes and score candidates from the ZIP file.   |

---

## **Summary**  
The code effectively automates resume screening by extracting key details (name, experience) and scoring resumes based on keyword relevance and work experience. It provides a scalable solution for initial candidate shortlisting, making the recruitment process more efficient.
