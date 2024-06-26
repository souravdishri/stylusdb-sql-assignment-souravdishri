![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)
<h1 align="center">StylusDB SQL</h1>
<p align="center">
A SQL database engine written in JavaScript

[![GitHub Repo](https://img.shields.io/badge/GitHub-Repo-green.svg)](https://github.com/souravdishri/stylusdb-sql-assignment-souravdishri)
[![GitHub Repo](https://img.shields.io/github/stars/ChakshuGautam/stylusdb-sql?style=social)](https://github.com/souravdishri/stylusdb-sql-assignment-souravdishri)
</p>

> **Disclaimer**:
This database is for educational purposes only. It is not intended for production use. It is written ground up in JavaScript and is a great way to learn how databases work. You can find the tutorial in the [docs](./docs) directory.

### Features
- [x] `INSERT`, `DELETE`, `SELECT`
- [ ] `UPDATE`, `CREATE TABLE`, `DROP TABLE`
- [x] CLI
- [ ] NPM Package

### Installation

```bash
npm i stylusdb-sql
```

### Usage

#### SELECT
Assuming you have a CSV file called `student.csv` with the following data:
```
id,name,age
1,John,25
2,Jane,25
```
```javascript
const { executeSELECTQuery } = require('stylusdb-sql');
const query = 'SELECT id, name FROM student WHERE age = 25';
const result = await executeSELECTQuery(query);

// result = [{ id: '1', name: 'John' }, { id: '2', name: 'Jane' }]
```

#### INSERT
```javascript
const { executeINSERTQuery } = require('../../src/queryExecuter');
const { readCSV, writeCSV } = require('../../src/csvStorage');
async function createGradesCSV() {
    const initialData = [
        { student_id: '1', course: 'Mathematics', grade: 'A' },
        { student_id: '2', course: 'Chemistry', grade: 'B' },
        { student_id: '3', course: 'Mathematics', grade: 'C' }
    ];
    await writeCSV('grades.csv', initialData);
}
await createGradesCSV();
const insertQuery = "INSERT INTO grades (student_id, course, grade) VALUES ('4', 'Physics', 'A')";
await executeINSERTQuery(insertQuery);
```

Verify the new entry in `grades.csv`:
```csv
student_id,course,grade
1,Mathematics,A
2,Chemistry,B
3,Mathematics,C
4,Physics,A
```

#### DELETE
```javascript
async function createCoursesCSV() {
    const initialData = [
        { course_id: '1', course_name: 'Mathematics', instructor: 'Dr. Smith' },
        { course_id: '2', course_name: 'Chemistry', instructor: 'Dr. Jones' },
        { course_id: '3', course_name: 'Physics', instructor: 'Dr. Taylor' }
    ];
    await writeCSV('courses.csv', initialData);
}
 await createCoursesCSV();

// Execute DELETE statement
const deleteQuery = "DELETE FROM courses WHERE course_id = '2'";
await executeDELETEQuery(deleteQuery);

// Verify the course was removed
const updatedData = await readCSV('courses.csv');
const deletedCourse = updatedData.find(course => course.course_id === '2');
```

### CLI Usage

Open a terminal and run the following command to start the CLI:
```bash
stylusdb-sql
```
Execute a query as shown below.
<img src="https://github.com/souravdishri/stylusdb-sql-assignment-souravdishri/blob/main/docs/tutorials/assets/tutorial-19.gif?raw=true" />

### Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md)