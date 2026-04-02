# Workers' Compensation Claims Tracking System

This capstone project is a comprehensive solution that tracks workers' compensation claims for an HR department in Salesforce. It will demonstrate your proficiency in core aspects of Salesforce development, from data modeling and DML to Apex classes and triggers. The goal is to build a system that manages the full lifecycle of a workers' comp claim — from the initial incident report through settlement — while automatically flagging employees who represent elevated risk based on their claims history.

One guiding principle should be: would you use this system, or would you put it into your production org?

## Project Details

- The capstone project can be done on a team (3 members max) or individually.
- All team members should be working in separate orgs, and all metadata necessary should be stored in the GitHub repository.
- Members are expected to collaborate and share ideas with one another. This could be done through Slack and virtual meetings.
- Collaboration with members outside of your team is encouraged, but all aspects of the project should be understood and explainable by each member of your team.
- You are provided an empty GitHub repository.
- All requirements are not well defined on purpose to allow creativity and to prepare for independence in a work setting.
- Ask questions to your instructor for further clarification of the requirements!

## Planning

**Week 1**

- Read and review all aspects of the project carefully.
- Delegate requirements to teammates. This will require a meeting and project group agreement. When doing this keep in mind everyone's availability is not the same.
- Set up the GitHub repository and configure individual Salesforce orgs.
- Review the provided CSV files and determine what objects and fields are needed based on the column headers.
- Configure the Employee and Claim custom objects, related objects, and fields.

**Week 2**

- Import the provided CSV data using the Data Import Wizard. Do not manually enter records.
- Focus on more straightforward requirements and programmatic solutions.
- Practice branching and merging into the GitHub repository.

**Week 3**

- Focus on the trigger logic and supporting Apex classes.
- Work on additional requirements (claim duration, status automation, high-value flag).
- Begin unit tests if you are going for optional credit.

**Week 4**

- Finalize any features being built.
- Add any additional polish to the code and record pages.
- Review teammate's code for best practices and formatting.
- Prepare and merge any final code to the main branch of your repository for review.
- Practice demoing/run-through of solutions created as a team.
- [Review the capstone presentation expectations and rubric.](#presentation-expectations--rubric)
- Schedule your presentation with your instructor.
- All metadata (classes, triggers, objects, etc.) needed to deploy the code should be included in the repo.

**Week 5 — Final Review**

- Deliverables:
  - Notify your instructor via Slack you are ready for review along with a link to your repository.
  - Provide login credentials to a Salesforce org that has the capstone project implemented.
- No more changes to the repository should be made.
- Rehearse your presentation with the team and prepare for the real presentation.
- Developer guests who are not your instructor may join the capstone presentation to add a different perspective.
- Teams will be given 1 week after the presentation to make any revisions to their codebase and submit for an additional code review.

## Notes

- You probably won't finish all the requirements, but features on the main branch should be "production ready" (formatted, well-commented, following best practices, etc.).
- It is recommended to focus on a few features that you know and are designed with best practices in mind instead of having multiple half-done features.
- Feel free to use project management tools to break down and organize the project.
- Salesforce is a powerful system, and many of the requirements could be solved using declarative features. Use declarative solutions for basic requirements like creating objects and configuring page layouts. When dealing with business logic and automation, opt for a programmatic solution.
- Flows are not allowed — this is a programming assessment.
- It is recommended to create a new Trailhead Playground or Developer org so that existing automation does not interfere with Capstone requirements.
- It is recommended to create a permission set to enable the sharing and field-level security of objects and fields.

---

## Overview

- **Data Model:** Build the objects and fields needed to track employees, claims, and the insurance companies that handle them. The model must support realistic scenarios like multiple employees on a single claim (e.g., a group accident) and multiple claims per employee across different insurers.
- **Data Import:** You will be given CSV files. Your job is to figure out what objects and fields are needed based on the data, create them, and import the records using the Data Import Wizard — not by hand.
- **Claims Lifecycle:** Track a claim from incident through settlement, including status changes and financial data.
- **Employee Risk Flagging:** Create trigger logic that automatically flags employees as Standard, Medium Risk, or High Risk based on their claims volume and/or payout totals with each insurance provider. This is the core programmatic requirement.
- **Claim Duration Tracking:** Calculate how many days a claim has been open and store it on the Claim record using Date math.
- **Employee Claims Summary:** Keep a running total of claims count and total payout amount on each Employee record, updated automatically whenever claim relationships change.
- **Claim Status Automation:** Enforce business rules when a claim's status changes — automatically record the settlement date when a claim is settled, and validate that key fields are in order before allowing certain status transitions.
- **High-Value Claim Flag:** Automatically mark claims that exceed a payout threshold so they stand out for review.
- **Unit Tests (optional):** Write Apex unit tests with at least 75% code coverage so the code can be deployed to production.

---

## Requirements

### Data Model

Build the objects and fields needed to support the system. At minimum the following must be present, though you may add additional fields and objects as you see fit.

**Account (Standard Object)**

Use the standard Account object to represent insurance companies.

- Name — the insurance company name (e.g., Liberty Mutual, MetLife, Travelers)
- Add additional fields as needed (phone, address, etc.)

**Contact (Standard Object)**

Use the standard Contact object to represent people who work at the insurance companies.

- Standard fields: First Name, Last Name, Email, Phone
- Linked to the insurance company Account via the standard Account lookup

**Employee (Custom Object)**

Create a custom object to represent the employees of the company that may file workers' comp claims.

Create the following fields:

- Name — full name of the employee
- Department — text or picklist field for the employee's department
- Title — job title
- Hire Date — date field
- Risk Level — picklist field with values: Standard, Medium Risk, High Risk. This field is set automatically by trigger logic and should not require manual input.
- Add additional fields as needed

**Claim (Custom Object)**

Create a custom object to store individual workers' compensation claims.

Create the following fields:

- Claim Number — auto-number or text field to uniquely identify the claim
- Date Filed — date the claim was submitted
- Incident Date — date the workplace incident occurred
- Status — picklist field to track the current state of the claim. Options should include: Open, In Review, Settled, Denied, Closed
- Settlement Amount — currency field representing the amount paid out on the claim
- Insurance Provider — lookup to Account (the insurance company handling this claim)
- Notes — long text area for any additional details
- Add additional fields as needed

**Employee Claim (Junction Object)**

Create a custom junction object that links Employees to Claims. This object enables a many-to-many relationship, which is needed because a single claim can involve multiple employees (e.g., a group accident) and an employee can have multiple claims over time.

- Employee — lookup to Employee
- Claim — lookup to Claim

### Data Import

CSV files are provided in the `data/` folder of this repository. Your tasks are:

1. Open each CSV file and review the column headers and sample data. Determine what objects, fields, and data types you need to create in Salesforce before importing.
2. Create all necessary custom objects and fields first. Do not start importing until your schema is ready.
3. Import records in dependency order — Accounts before Contacts, Employees and Claims before Employee Claims.
4. Use the Salesforce Data Import Wizard or Data Loader. Do not manually create records.
5. Verify your imported data by checking record counts and that relationship lookups (e.g., Insurance Provider on a Claim) resolved correctly.

**Provided files:**

| File | Records | Notes |
|---|---|---|
| Accounts.csv | 5 | Insurance companies |
| Contacts.csv | 10 | Insurer contacts; requires Account Name to resolve the Account lookup |
| Employees.csv | 40 | Company employees; import before Claims |
| Claims.csv | 75 | Requires Insurance Provider (Account Name) to resolve the lookup |
| Employee_Claims.csv | 78 | Junction records; import last, after both Employees and Claims are in |

> **Tip:** The Employee_Claims file requires matching on both Employee Name and Claim Number simultaneously. The Data Import Wizard may not support this for custom junction objects — you may need to use the Data Loader for this file.

The instructor will validate that data was imported — not typed in manually — by reviewing record counts and created timestamps.

### Employee Risk Flagging

Create a trigger and supporting Apex class that automatically evaluates an employee's risk level based on their claims history and updates the Risk Level field on the Employee object.

**Trigger details:**

- Object: Employee Claim (the junction object)
- Events: after insert, after update, after delete, after undelete
- The trigger should recalculate the risk level for all employees affected by the DML operation

**Logic:**

- For each affected employee, look up all of their related claims and group the data by insurance provider
- Accumulate either the number of claims or the total settlement amount (or both) per provider using a Map
- Apply the following thresholds:
  - **High Risk** — the employee has too many claims or too high a total payout with a single provider (thresholds TBD)
  - **Medium Risk** — the employee is approaching but has not yet reached the High Risk threshold (thresholds TBD)
  - **Standard** — the employee does not meet the criteria for either risk level
- Update the Risk Level field on the affected Employee records
- The trigger must be bulkified — no SOQL or DML inside loops

The logic must use a Map to group totals by insurer. A simple claim counter without per-provider grouping will not satisfy this requirement.

### Claim Duration Tracking

Add a `Days Open` Number field to the Claim object. Write Apex that calculates the number of days between the Incident Date and today (or the Date Filed if the claim is Settled or Denied) and stores it on the record.

This logic should run whenever a Claim is inserted or updated. Use the `Date` class and date arithmetic — this is a practical application of the date and math concepts covered in the course.

**Example:** An incident that occurred on January 10th and was filed on January 15th and is still open as of today should show the number of calendar days since the incident occurred.

### Employee Claims Summary

Add two fields to the Employee object:

- `Total Claims` — Number field tracking how many claims this employee has been involved in across all time
- `Total Settlement Amount` — Currency field tracking the sum of all settled claim payouts this employee is associated with

Write Apex logic (called from the Employee Claim trigger or a separate trigger on Claim) that keeps these fields accurate whenever Employee Claim records are inserted, updated, or deleted. This requires SOQL to query related records, a loop to calculate the totals, and DML to update the Employee.

These fields give HR a quick snapshot on the employee record without having to manually add up related list records.

### Claim Status Automation

Add a `Settlement Date` Date field to the Claim object. Write a trigger (or add logic to an existing Claim trigger) that enforces the following rules automatically:

- When Status changes to **Settled**: set Settlement Date to today if it is currently blank. Validate that Settlement Amount is greater than zero — a claim cannot be marked Settled with a $0 payout.
- When Status changes to **Denied**: clear the Settlement Amount field (set it to 0).
- Validate that Incident Date is not in the future and is not after the Date Filed — a realistic claim cannot be reported before it happened.

Use `addError()` on the record to prevent the save and display a meaningful error message to the user when a validation fails.

### High-Value Claim Flag

Add an `Is High Value` Checkbox field to the Claim object. Write Apex logic that automatically checks this box whenever the Settlement Amount exceeds a threshold you define (e.g., $15,000).

This flag should be evaluated on insert and update. If the Settlement Amount is later reduced below the threshold or the claim is denied, the checkbox should be unchecked automatically.

This is a good opportunity to practice using an `if/else` in a trigger context and thinking about how field values should respond to changes over time.

### Record Pages

Configure record pages for the Employee and Claim objects so the most relevant information is easy to find. Use standard and custom components as appropriate. Related lists (e.g., Claims on an Employee, Employees on a Claim) should be visible and useful.

### Unit Tests (Optional)

Writing Apex unit tests is optional for this capstone but is encouraged if you want to go further. Unit tests are required to deploy code to a production org, and they are commonly asked about in Salesforce developer interviews.

If you choose to write tests, aim for at least 75% code coverage and include both positive scenarios (the happy path) and negative scenarios (invalid inputs, edge cases).

---

## Presentation Expectations & Rubric

### Presentation Expectations

**Overview**

The main goal of this presentation is to showcase what the team has created according to the capstone project requirements through coding and the knowledge gained during the course. It serves as a platform for team members to present their creations and articulate the challenges faced and the solutions developed.

One guiding principle should be: would you use this system, or would you put it into your production org?

**Part 1 (20 minutes) — User-Centric Features and Configuration**

- Present the functionalities constructed as if introducing them to someone who would use the org.
- Delve into the organization's setup, configuration, and any interesting "behind-the-scenes" elements.
- The format should resemble a training session or product demonstration, with emphasis on practicality and user interaction.

**Part 2 (20 minutes) — Code Deep Dive**

- Transition into the technical aspects by showcasing the code behind key features.
- Every team member is expected to discuss at least one section of the code.
- Highlights should include the construction methodology, interesting code segments, and potential enhancements for future iterations.
- This segment will adopt an interview project review or code review format.

**Part 3 (10 minutes) — Instructor Questions**

- The instructor will probe deeper, inquiring about the data model and the code's architecture.
- This session may involve constructive critiques, identification of potential issues, and suggestions for future improvements.

**Part 4 (10 minutes) — Reflections and Conclusions**

- The team will collectively share reflections about the project, focusing on team dynamics, collaboration, and the overall journey.
- The instructor will provide concluding remarks, summarize observations, and impart final thoughts.

**Execution Protocol**

While a singular team member can manage the screen sharing for consistency, it's imperative that each participant articulates their contributions, elaborating on their design decisions and implementation rationale.

**Additional**

- The session will be recorded so the team can review how they performed and improve.
- Guests who are not your instructor may join the capstone presentation to add a different perspective but will only leave comments in the live session chat.
- Revisions to the codebase will be allowed for up to 1 week after the presentation is complete.

---

### Rubric

**Total: 100/100 Points**
68 points are required to pass along with no significant bad practices in the codebase.

**1. Data Model and Setup (5 Points)**

- Identification and justification of standard vs. custom objects used (2 points)
- Proper configuration of fields (including data types and relationships) (1 point)
- Logical and efficient record page design using standard and custom components (1 point)
- Best practices followed in data modeling and object relationships (1 point)

**2. Code Review (40 Points)**

- Clarity and organization of code (8 points)
- Best practices followed in Apex and other components (8 points)
- Proper error handling and data validation (7 points)
- Efficient class, method, and variable names; meaningful comments in the code (7 points)
- Complex requirements/functionality — trigger logic, Maps, bulk safety (10 points)

**3. Demonstration (25 Points)**

- Working functionality of the system (10 points)
- Handling of edge cases and unexpected inputs (10 points)
- Presentation organization and flow (3 points)
- Enhancements beyond scope/requirements provided (2 points)

**4. Testing — Optional (15 Points)**

Unit tests are not required for this capstone but can be completed for full points in this category.

- Comprehensive unit tests covering at least 75% of the Apex code (6 points)
- Bulk record tests and positive/negative test scenarios (5 points)
- Proper assertions in test classes (4 points)

**5. Collaboration and Version Control (10 Points)**

- Effective use of GitHub for version control (4 points)
- Relevant metadata committed to the repository (3 points)
- Evidence of collaboration among team members (3 points)

**6. Q&A Session (5 Points)**

- Ability to answer questions about the code and design choices (3 points)
- Ability to handle feedback and suggest improvements (2 points)

*Note: This rubric is a guideline, and instructors can adjust the point allocations based on their emphasis and priorities. All sections of the rubric may not apply to your specific project.*

*If you fail to meet the points necessary to pass, your team may be required to present again. Teams will have one week after the presentation to make any revisions to their codebase and submit for an additional code review by the instructor.*

*Points will automatically be taken off for showing the developer console. — this is a joke, but also not a joke.*

---

## Instructor Notes

**Instructor:**

**Org Info:**

**Presentation Recording Link:**
