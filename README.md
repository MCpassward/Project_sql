##SQL Schema and Query Operations for University Database
      
1. Table Creation
    Department Table:
    
       CREATE TABLE Department(
       dept_id NUMBER PRIMARY KEY,
       dept_name VARCHAR2(30)
       );

    Student Table:
   
       CREATE TABLE Student(
       student_id NUMBER PRIMARY KEY,
       student_name VARCHAR2(50),
       dept_id NUMBER REFERENCES Department(dept_id)
       );
   
    Enrolled_In Table:

       CREATE TABLE Enrolled_In(
       student_id NUMBER,
       course_name VARCHAR2(50),
       FOREIGN KEY(student_id) REFERENCES Student(student_id)
       );

    Fees Table

       CREATE TABLE Fees(
       student_id NUMBER,
       dept_id NUMBER,
       amount NUMBER,
       FOREIGN KEY(student_id) REFERENCES Student(student_id),
       FOREIGN KEY(dept_id) REFERENCES Department(dept_id)
       );

2. Inserting Data into Tables
    Inserting Departments:

       INSERT INTO Department VALUES(101, 'Computer Science');
       INSERT INTO Department VALUES(102, 'Mathematics');
       INSERT INTO Department VALUES(103, 'Physics');
       INSERT INTO Department VALUES(104, 'Biology');

    Inserting Students:

       INSERT INTO Student VALUES(201, 'Alice Johnson', 101);
       INSERT INTO Student VALUES(202, 'Bob Smith', 102);
       INSERT INTO Student VALUES(203, 'Charlie Brown', 103);
       INSERT INTO Student VALUES(204, 'Diana Prince', 104);

    Inserting Enrollments:

       INSERT INTO Enrolled_In VALUES(201, 'Data Structures');
       INSERT INTO Enrolled_In VALUES(202, 'Linear Algebra');
       INSERT INTO Enrolled_In VALUES(203, 'Quantum Mechanics');
       INSERT INTO Enrolled_In VALUES(204, 'Cell Biology');

    Inserting Fees:
   
       INSERT INTO Fees VALUES(201, 101, 5000);
       INSERT INTO Fees VALUES(202, 102, 4500);
       INSERT INTO Fees VALUES(203, 103, 5500);
       INSERT INTO Fees VALUES(204, 104, 6000);
    
3. Altering the Student Table
    Adding new columns to the Student table

       ALTER TABLE Student ADD age NUMBER;
       ALTER TABLE Student ADD phone_no VARCHAR2(15);
       ALTER TABLE Student ADD gender VARCHAR2(10);
       ALTER TABLE Student ADD marital_status VARCHAR2(10);

    Updating the Student Table
    Updating specific student information:

       UPDATE Student
       SET phone_no = '0789998888'
       WHERE student_id = 201;

    This updates Alice Johnson's phone number

       UPDATE Student
       SET age = 22
       WHERE student_id = 202;

    This updates Bob Smith's age to 22

       UPDATE Student
       SET marital_status = 'single'
       WHERE student_id = 203;

5. Select Queries
    Joining Student and Fees to display student names and fees

       SELECT Student.student_name, Fees.amount
       FROM Student
       JOIN Fees ON Student.student_id = Fees.student_id;

    Joining Student and Department to display student names and department names:

       SELECT Student.student_name, Department.dept_name
       FROM Student
       JOIN Department ON Student.dept_id = Department.dept_id;

    Retrieving all students older than 21

       SELECT *
       FROM Student
       WHERE age > 21;

    Retrieving distinct student names:

       SELECT DISTINCT student_name
       FROM Student;
    
    Retrieving maximum, minimum, and average fees:

       SELECT MAX(amount), MIN(amount), AVG(amount)
       FROM Fees;

    Joining Student and Enrolled_In to show student names and courses:

       SELECT DISTINCT Student.student_name, Enrolled_In.course_name
       FROM Student
       JOIN Enrolled_In ON Student.student_id = Enrolled_In.student_id;

    Retrieving students with fees greater than 5000:

       SELECT Student.student_name, Fees.amount
       FROM Student
       JOIN Fees ON Student.student_id = Fees.student_id
       WHERE Fees.amount > 5000;

    Counting the number of students per department:

       SELECT Student.dept_id, COUNT(*)
       FROM Student
       GROUP BY Student.dept_id;

     Joining multiple tables to retrieve student, department, and fee information:

       SELECT Student.student_name, Department.dept_name, Fees.amount
       FROM Student, Department, Fees
       WHERE Student.dept_id = Department.dept_id
       AND Student.student_id = Fees.student_id;
   ![conceptual diagram](https://github.com/user-attachments/assets/665f8a65-1c93-4aff-8976-8b27f4703bdb)

    
