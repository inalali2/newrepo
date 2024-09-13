
Project Specification: Research Grant Council Database

1. Introduction

The database layout we've created is a blueprint for a government organization called the Research Grant Council.
It helps manage research grants by tracking grant competitions, applications, reviewers, and meetings. This setup ensures efficient organization, review, and decision-making.

Tables:

grant_Competition: Stores information about grant competitions.
researcher: Contains details of researchers applying for grants.
collaborators: Represents the many-to-many relationship between grant applications and collaborators.
meetings: Tracks reviewer participation in grant selection committee meetings.
reviewer: Stores information about reviewers.
grant_Application: Holds data about grant applications, including requested amounts, principal investigators, and application status.

Triggers:

conflict_of_interest: Prevents conflicts of interest by raising an error if a reviewer is associated with a researcher from the same institution.
award_money_generator: Automatically generates an awarded amount for grant applications marked as "Awarded."
status_updated/status_updated_not: Updates application status based on review completion in meetings, setting the status to "Awarded" or "Not Awarded" accordingly.

Overview:

Data Integrity: Foreign keys ensure referential integrity within the database.
Triggers: Handle automatic updates and integrity checks, improving system efficiency and reliability.
Error Handling: Triggers manage conflicts of interest and automate application status updates.


2. Description of Schema

1. grant_Competition:

cid: Primary key representing the competition ID.
title: Title of the grant competition (e.g., "Quantum Computing Research Grant").
deadline: Deadline for submitting grant proposals.
description: Brief description of the grant competition.
area_of_study: Area of study or research focus (e.g., "Computer Science", "Biology").
status: Current status of the competition (open or closed).

2. researcher:
   
rid: Primary key representing the researcher ID.
fName: First name of the researcher.
lName: Last name of the researcher.
emailID: Email address of the researcher.
uni_name: Name of the university or organization the researcher is affiliated with.

3. collaborators:

   
aid: Foreign key referencing the grant_Application table.
collaborator_id: Foreign key referencing the researcher table, representing the collaborator's ID.
This table establishes a many-to-many relationship between grant applications and collaborators.

4. meetings:
   
date: Date of the meeting.
reviewer_id: ID of the reviewer participating in the meeting.
aid: Foreign key referencing the grant_Application table.
reviewed: Indicates whether the grant application has been reviewed (1 for reviewed, 0 for not reviewed).

5. reviewer:

reviewer_id: Primary key representing the reviewer ID.
fName: First name of the reviewer.
lName: Last name of the reviewer.
emailID: Email address of the reviewer.
institution_name: Name of the institution or organization the reviewer is affiliated with.

6. grant_Application:
   
aid: Primary key representing the grant application ID.
amt_req: Requested amount for the grant application.
cid: Foreign key referencing the grant_Competition table.
principle_inv: ID of the principal investigator for the grant application.
app_status: Status of the grant application (e.g., "submitted", "awarded", "not awarded").
amt_awarded: Amount awarded for the grant application.
status_date: Date of the status update of the grant application.

3. Project Assumptions

Principal Investigator and Collaborators: Only the principal investigator applies for the grant. Other researchers involved are listed as collaborators.

Funds Allocation: Funds are designated to the principal investigator, who is responsible for distribution.

Reviewers: Each application will have three reviewers. Reviewers provide reviews in Boolean form (1 for granted, 0 for denial).

Meeting Participants: Only reviewers participate in meetings discussing grant applications.

Decision Making Process: Decisions are made during meetings, with applications discussed on specific dates. Multiple applications may be discussed on the same date, but no additional dates are assigned.

Automatic Award Generation: If at least two out of three reviewers recommend granting money, the award will be granted automatically.

Automatic Status Update: The status of an application will be updated to "Awarded" if at least two reviewers recommend granting money.

Amount Awarded Constraint: The amount awarded is always less than the requested amount.

Automatic Status Date Update: The status_date attribute is automatically updated after meetings to reflect the decision date.
