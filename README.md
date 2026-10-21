# University Admission Expert System

A responsive Django web application that demonstrates how a rule-based expert system can help students explore degree-program eligibility. The project uses Python, Django, SQLite and Bootstrap.

> **Academic demo notice:** Eligibility thresholds and aggregate weights in this repository are illustrative examples, not official university admission policies. Verify and replace them with current rules from the universities you want to cover.

## Features

- **Admission checker:** collect student name, academic stream, Matric percentage, Intermediate percentage and optional entry-test marks.
- **Aggregate calculator:** calculate a weighted aggregate when entry-test marks are supplied; show a clearly labelled provisional academic score when they are not.
- **Explainable rule evaluation:** display facts, fired rules and reasons a program did not match.
- **Student record management:** save, search, edit and delete student analyses.
- **Database models:** maintain universities, programs, scholarship information and student records.
- **Admin dashboard:** use Django Admin to add and manage university, program, scholarship and student data.
- **Scholarship page:** list scholarship records created in the admin dashboard.
- **Responsive UI:** Bootstrap layout for desktop and mobile browsers.
- **Input validation:** server-side checks ensure marks/percentages are between 0 and 100.
- **Unit tests:** basic tests for the rule engine.

## Technology stack

| Component | Technology |
|---|---|
| Frontend | HTML5, CSS3, Bootstrap 5 |
| Backend | Python, Django |
| Database | SQLite (default, local development) |
| Rule engine | Explicit Python rules / forward-chaining-style trace |
| Editor | Visual Studio Code |

## Project structure

```text
University_Admission_Expert_System/
├── manage.py
├── requirements.txt
├── README.md
├── admission_project/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── admissions/
│   ├── admin.py
│   ├── apps.py
│   ├── engine.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
└── templates/
    └── admissions/
        ├── index.html
        ├── records.html
        ├── edit_record.html
        ├── confirm_delete.html
        └── scholarships.html
```

## Requirements

- Python 3.10 or newer
- pip
- Visual Studio Code (recommended)
- Internet connection for the Bootstrap CDN, unless Bootstrap is downloaded and served locally

Check your Python installation:

```powershell
py --version
```

## Setup on Windows / VS Code

1. Download and extract the project ZIP.
2. In VS Code, select **File → Open Folder** and open the extracted `University_Admission_Expert_System` directory.
3. Open **Terminal → New Terminal**.
4. Create a virtual environment:

   ```powershell
   py -m venv .venv
   ```

5. Activate it in PowerShell:

   ```powershell
   .venv\Scripts\Activate.ps1
   ```

   If PowerShell blocks script activation, open a Command Prompt terminal and use:

   ```bat
   .venv\Scripts\activate.bat
   ```

6. Install Django:

   ```powershell
   python -m pip install -r requirements.txt
   ```

7. Create database migrations and tables:

   ```powershell
   python manage.py makemigrations admissions
   python manage.py migrate
   ```

8. (Optional) Create an administrator login:

   ```powershell
   python manage.py createsuperuser
   ```

9. Start the local development server:

   ```powershell
   python manage.py runserver
   ```

10. Open the URLs below in your browser.

## Local URLs

- Main admission checker: <http://127.0.0.1:8000/>
- Student records: <http://127.0.0.1:8000/students/>
- Scholarships: <http://127.0.0.1:8000/scholarships/>
- Django Admin: <http://127.0.0.1:8000/admin/>

## How to add universities and scholarships

1. Create an admin account with `python manage.py createsuperuser`.
2. Open `/admin/` and sign in.
3. Add university records first.
4. Add degree programs and link each program to a university.
5. Add scholarship records and optionally associate them with a university or program.
6. Open `/scholarships/` to view scholarship records.

The database models are provided for data management. The initial rule engine in `admissions/engine.py` currently uses an explicit demonstration rule set; database program criteria are not automatically substituted into the rule engine yet. If you want the checker to use administrator-entered criteria dynamically, that can be the next enhancement.

## How the rule engine works

The engine takes the student's academic field and marks as facts, then checks each sample degree-program rule. A rule can fire when the field matches and the minimum Intermediate and entry-test conditions are satisfied. The result includes eligible programs, non-matching programs with reasons, and a trace that explains the decisions.

The current sample aggregate formula is:

- With entry-test marks: `10% Matric + 50% Intermediate + 40% Entry Test`
- Without entry-test marks: provisional academic score `(10% Matric + 50% Intermediate) / 60%`

Both are demonstration assumptions. Universities use different weightings, subject requirements, minimum marks and entry tests. Do not use this sample output as a real admission decision.

## Run tests

```powershell
python manage.py test
```

## Troubleshooting

- **`py` is not recognized:** install Python from the official Python website and select the option to add Python to PATH, then reopen VS Code.
- **`No module named django`:** activate the virtual environment and run `python -m pip install -r requirements.txt`.
- **`no such table`:** run `python manage.py makemigrations admissions` and `python manage.py migrate`.
- **PowerShell activation error:** use the Command Prompt activation command shown above.
- **Port already in use:** run `python manage.py runserver 8001` and open <http://127.0.0.1:8001/>.

## Important security notes

This is a local academic project, not a production-ready admissions service. Before public deployment, set a secure environment-based `SECRET_KEY`, set `DEBUG=False`, configure `ALLOWED_HOSTS`, use HTTPS, add authentication/permissions for sensitive student data, and consider a production database.

## Poster vs implementation

The supplied poster describes WordPress, PHP, MySQL, XAMPP and VS Code, while the uploaded HTML contains Django template tags. This project follows the Django/Python approach so the existing template syntax works. If your instructor specifically requires PHP/MySQL/WordPress, the implementation stack would need to be changed rather than simply renaming the technologies.

## License

No license has been specified. Add a license file if you intend to publish or redistribute this project.
