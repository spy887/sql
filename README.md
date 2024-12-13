<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Codes</title>
    </head>
    <style>
        textarea {
          width: 500px; 
          height: 50px; 
          resize: vertical;  
        }
    </style>
      
    <body>

    <h1></h1>
    
    <p>Jump to sections: 
        <a href="#sqlfunc">SQL Functions</a>,
        <!--<a href="#"></a>,
        <a href="#"></a>,
        <a href="#"></a>,
        <a href="#"></a>,
        <a href="#"></a>,-->
        
    </p>
    
    <h3 id="sqlfunc">SQL Functions</h3>
    <p>a. Display the employee name concatenated with the employee number.<br>
        <textarea>
            SELECT CONCAT(employee_name, employee_number) AS concatenated_info FROM employees;

        </textarea>
    </p>
    <p>Display Half of Employee's Name in Uppercase and Half in Lowercase:<br>
        <textarea>
            SELECT 
    UPPER(SUBSTR(employee_name, 1, LENGTH(employee_name) / 2)) ||
    LOWER(SUBSTR(employee_name, LENGTH(employee_name) / 2 + 1)) AS formatted_name
FROM employees;

        </textarea>
    </p>
    <p>Display Date Two Months After Joining:<br>
        <textarea>
            SELECT 
            employee_name, 
            date_of_joining, 
            ADD_MONTHS(date_of_joining, 2) AS new_date
        FROM employees;
        
        </textarea>
    </p>

    <p>Display Rounded Date in Various Formats:<br>
        <textarea>
            SELECT 
            TRUNC(date_of_joining, 'YEAR') AS rounded_year,
            TRUNC(date_of_joining, 'MONTH') AS rounded_month,
            TRUNC(date_of_joining, 'DAY') AS rounded_day
        FROM employees;
        
        </textarea>
    </p>

    <p>Display Commission or Default Text:<br>
        <textarea>
            SELECT 
            employee_name, 
            NVL(commission, 'No Commission') AS commission_status
        FROM employees;
        
        </textarea>
    </p>

    <p>2. Write a PL/SQL Program to Exemplify the Concept of Triggers<br>Create the Audit Table<br>
        <textarea>
            CREATE TABLE salary_audit (
                audit_id NUMBER PRIMARY KEY,
                employee_id NUMBER,
                old_salary NUMBER(10, 2),
                new_salary NUMBER(10, 2),
                change_date DATE,
                changed_by VARCHAR2(100)
            );
            
        </textarea>
    </p>

    <p> Create the Trigger<br>
        <textarea>
            CREATE OR REPLACE TRIGGER trg_salary_update
            AFTER UPDATE OF salary ON employees
            FOR EACH ROW
            BEGIN
                INSERT INTO salary_audit (audit_id, employee_id, old_salary, new_salary, change_date, changed_by)
                VALUES (
                    salary_audit_seq.NEXTVAL, -- Assuming a sequence named `salary_audit_seq` exists for generating IDs
                    :OLD.employee_id,
                    :OLD.salary,
                    :NEW.salary,
                    SYSDATE,
                    USER
                );
            END;
            /
            
        </textarea>
    </p>

    <p>Create a Sequence for the Audit Table<br>
        <textarea>
            CREATE SEQUENCE salary_audit_seq START WITH 1 INCREMENT BY 1;

        </textarea>
    </p>

    <p>Test the Trigger<br>
        <textarea>
            -- Update a salary
UPDATE employees
SET salary = salary + 1000
WHERE employee_id = 1;

-- Check the audit table
SELECT * FROM salary_audit;

        </textarea>
    </p>

    
    
    
   <!-- <h3 id=""></h3> 
    <p>
        <textarea></textarea>
    </p>

    <h3 id=""></h3>
    <p>
        <textarea></textarea>
    </p>
    
    <h3 id=""></h3> 
    <p>
        <textarea></textarea>
    </p>

    <h3 id=""></h3>
    <p>
        <textarea></textarea>
    </p>
    
    <h3 id=""></h3> 
    <p>
        <textarea></textarea>
    </p>
    -->


    
    
    
    
    
    
    

    </body>
</html>
