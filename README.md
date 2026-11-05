# c-programming-quiz
Mobile-friendly C Programming Quiz Portal
# C Programming Quiz – Python Flask Project

A small web-based C programming MCQ quiz. Students enter their roll number, attempt the quiz, and see their marks. Results are stored in SQLite. A teacher can view all results and download a CSV report containing roll number and marks.

## Features

- Student login using roll number
- 15 multiple-choice questions on C programming
- Automatic evaluation
- One recorded attempt per roll number
- Student result page showing roll number, marks, total marks and percentage
- Teacher/admin login
- Teacher report with all student roll numbers and marks
- Downloadable CSV report
- SQLite database; no separate database server required

## Requirements

- Python 3.9 or later
- Internet connection only for the first-time Flask installation

## Setup on Windows

1. Extract the ZIP file.
2. Open Command Prompt in the extracted `c_quiz_project` folder.
3. (Recommended) Create a virtual environment:

   ```bat
   python -m venv venv
   venv\Scripts\activate
   ```

4. Install Flask:

   ```bat
   pip install -r requirements.txt
   ```

5. Start the application:

   ```bat
   python app.py
   ```

6. Open this address in your browser:

   `http://127.0.0.1:5000`

## Student use

1. Enter the roll number on the login page.
2. Click **Start Quiz**.
3. Answer all questions and submit.
4. The result page displays the roll number and marks.

The project records only the first submitted attempt for each roll number. To allow retakes, remove or revise the duplicate-attempt checks in `app.py`.

## Teacher report

1. Open `http://127.0.0.1:5000/admin`.
2. Default teacher password: `teacher123`
3. View the student result table.
4. Click **Download CSV Report** to download `C_Quiz_Report.csv`.

Change the default password before using this project with a real class. On Windows Command Prompt, set it for the current terminal session before starting the app:

```bat
set ADMIN_PASSWORD=YourStrongPassword
set SECRET_KEY=replace-with-a-long-random-secret
python app.py
```

## Database

The application automatically creates `quiz.db` when it is first run. The `results` table stores:

- `roll_no`
- `marks`
- `total`
- `submitted_at`

Keep `quiz.db` to retain results. Back it up regularly.

## Customizing questions

Edit the `QUESTIONS` list near the top of `app.py`. Each question has:

- `question`: question text
- `options`: list of four choices
- `answer`: zero-based index of the correct option (0 to 3)

For example, `"answer": 1` means the second option is correct.

## Important deployment note

This is a classroom demonstration project. Roll-number-only login does not verify a student's identity, and Flask's built-in development server is not intended for public production deployment. For a real examination, use authenticated student accounts, HTTPS, a production server, and suitable exam controls.

## If an earlier test attempt was recorded with zero marks

The corrected quiz template fixes the question field names. If a roll number has already submitted before this correction, the project will still show that previously stored result because only one attempt is allowed. To clear only that test record, open the project folder in Command Prompt and run:

```bat
python -c "import sqlite3; c=sqlite3.connect('quiz.db'); c.execute(\"DELETE FROM results WHERE roll_no='50000'\"); c.commit(); c.close()"
```

Replace `50000` with the roll number whose test record you want to clear. Then restart the app and attempt the quiz again.
