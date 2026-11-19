# **Spec for Talk-to-data analyst** 

## **1. Problem** 

Managers often depend on data teams to answer simple business questions, such as total sales, top-performing products, monthly revenue, or pending purchase orders. This creates delays because someone must write SQL, query the database, analyse the results, and prepare reports. 

Build an AI Data Analyst that allows users to ask questions in plain English and receive accurate results, generated SQL, charts, and simple explanations. 

## **2. Success** 

Successfully answer at least 90% of the 30 evaluation questions with the correct expected results. SQL must be valid, read-only, and safely executed. Results must be supported by actual database data. 

## **3. Users** 

- **Business Managers:** Ask business questions in natural language and view results. 

- **Data Analysts:** Validate generated SQL and investigate results. 

- **Administrators:** Manage database access, permissions, and safety configurations. 

Users can query data, but database modification operations must never be permitted. 

## **4. Data** 

- Use a synthetic business database with no real company or confidential data. 

- Include relevant tables such as sales, products, customers, orders, and purchase orders. 

- Maintain realistic relationships, dates, amounts, and records for analysis. 

- Create 30 evaluation questions with predefined expected results. 

- Keep evaluation answers separate from the agent's accessible data. 

## **5. Tools (3 MCP Tools)** 

## **1.** get_schema 

- Input: Optional table name. 

- Output: Table names, columns, data types, and relationships. 

- Retrieves database schema so the agent understands available data. 

## **2.** run_select 

   - Input: Generated SQL SELECT query. 

   - Output: Query results, column names, and execution status. 

   - Executes safe, read-only SQL against the database. 

**3.** make_chart 

   - Input: Query results, chart type, and relevant column names. 

   - Output: A suitable chart visualization. 

   - Creates charts such as bar, line, or pie charts based on the query results. 

## **6. Guardrails** 

- Use a read-only database user. 

- Allow SELECT queries only; reject INSERT, UPDATE, DELETE, DROP, ALTER, and other modification operations. 

- Enforce a maximum row limit. 

- Set query execution timeouts. 

- Validate SQL before execution. 

- Display generated SQL to the user. 

- Prevent unauthorized access to database tables. 

- Never fabricate results, numbers, or charts. 

- Base explanations only on actual query results. 

## **7. Evals** 

Test the agent against 30 questions with predefined expected answers. 

Measure: 

- Correctness of generated SQL. 

- Query execution success. 

- Accuracy of returned results. 

- Correct chart selection. 

- Accuracy of explanations. 

- Unsafe SQL rejection. 

**Target:** At least 90% of questions answered correctly. Evaluate against actual expected values, not approximate or manually assumed results. 

## **8. Attacks** 

Test these 10 failure scenarios: 

1. User asks the agent to execute a DELETE query. 

2. User attempts to inject SQL through a question. 

3. User requests unrestricted access to database tables. 

4. User asks to bypass row limits. 

5. User requests a query that runs indefinitely or is computationally expensive. 

6. User attempts to access unauthorized or sensitive columns. 

7. SQL contains multiple statements. 

8. User tries to manipulate the agent into inventing results. 

9. Database returns empty or unexpected results. 

10. Query execution fails or times out. 

The system must reject unsafe requests, enforce database restrictions, and accurately report failures. 

## **9. Out of Scope** 

- INSERT, UPDATE, DELETE, or any database modification. 

- Database administration or schema modification. 

- Direct production database access. 

- Predictive analytics or machine-learning forecasting. 

- Automated business decisions. 

- Data modification through AI-generated SQL. 

- Complex enterprise BI dashboards. 

- Integration with multiple live enterprise databases. 

