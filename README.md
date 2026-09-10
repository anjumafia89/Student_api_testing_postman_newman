# 🎓 Student Details API – Automated Testing Framework (Postman + Newman)

This is a set of automated API tests for a Student Management API, built using **Postman**, **JavaScript**, and **Newman**.

It tests the full **Create → Read → Update → Delete (CRUD)** flow of the API, connects the requests to each other, creates random test data automatically, and checks that every response is correct.

---

## 🚀 What This Project Does

- **Tests all 4 main API actions**: Create, Read, Update, and Delete a student record
- **Creates fake test data automatically** — random first/middle/last name and random date of birth, so you don't have to type new data every time you run the tests
- **Connects the requests together** — when a student is created, its `id` is saved automatically and reused in the next requests (Get, Update, Delete), so everything works as one flow
- **Checks the results automatically** — after each request, the tests check the status code and make sure the data returned matches the data that was sent
- **Uses variables instead of fixed values** — things like `base_url`, `id`, and student info are stored as environment variables, so nothing is hardcoded
- **Creates a clean HTML report** after every run, showing what passed, what failed, and the full request/response details

## 🧰 Tools Used

| Tool | What it's used for |
|---|---|
| Postman | Building and testing the API requests |
| JavaScript (Postman scripts) | Writing the test logic |
| Newman | Running the tests from the command line |
| newman-reporter-htmlextra | Making the HTML report |
| moment.js | Generating random dates of birth |

## 📂 Project Structure

```
StudentsDetails.postman_collection.json
    → the API requests and test scripts

Student_details_Environment.postman_environment.json
    → the environment variables (base_url, id, etc.)

reports/newman-run-report.html
    → the generated test report

README.md
```

## 🔄 How the Tests Run, Step by Step

1. **Get_Student** — get the list of all students
2. **Create_Student** — create a new student with random data; the new student's `id` is saved for the next steps
3. **Created_student** — check that the student was created correctly with the right data
4. **Update_student** — update that same student with new random data
5. **Updated_student_data** — check that the update actually worked
6. **Delete_student** — delete the student
7. **Delete_student_verify** — check that the student is really gone

## ▶️ How to Run This

**Option 1 — Using Postman**
1. Import the two JSON files (`StudentsDetails.postman_collection.json` and `Student_details_Environment.postman_environment.json`) into Postman
2. Select the environment, and fill in the `base_url` value with the API's URL
3. Click "Run" on the collection

**Option 2 — Using Newman (command line)**
```bash
npm install -g newman newman-reporter-htmlextra

newman run StudentsDetails.postman_collection.json \
  -e Student_details_Environment.postman_environment.json \
  -r htmlextra \
  --reporter-htmlextra-export ./reports/newman-run-report.html
```

## 📊 Test Run Results

| What | Result |
|---|---|
| Requests run | 7 |
| Test scripts | 2 |
| Total time | ~5.6s |
| Average response time | ~2s |

> **Note:** In one run, `Create_Student` failed because the `base_url` variable was empty — I traced the issue back and confirmed the fix is to always set `base_url` before running the tests. Keeping this note here on purpose, to show how the issue was found and understood.

The full report (with all request/response details) is here: [`reports/newman-run-report.html`](./reports/newman-run-report.html).
