---
name: prd-drafter
description: "Use this skill whenever the user wants to create, draft, or update a Product Requirement Document (PRD). Triggers include: any mention of 'PRD', 'product requirement document', 'requirement doc', or requests to turn a feature idea, ticket, meeting notes, or brief into a structured requirements document. Also use when the user asks to add user stories, acceptance criteria, or a problem statement for a feature, or to reformat an existing requirements write-up into a PRD. Do NOT use for general technical design docs, RFCs, or architecture docs that are not framed as product requirements." 
---


## Before writing
 
Gather what's needed from the input the user gives (ticket, notes, chat, transcript). 
If any of the information required for creating PRD are missing, ask the user rather than inventing them. 


## PRD Format 

When generating a PRD, you must follow this standard. 

The general filename rule is:
  - `prd-[feature].md` for the PRD file.
  - For supporting files, no specific rule

For PRD (product requirement document), it must contain the following items (in the given sequence):

[Title: PRD - Product / Feature Name]

- Document Information
  + Product / Feature Name: ...
  + Author: The assignee's username
  + Date: blank
  + Version: blank

- Table of Contents
  Includes items up to the second-level header

- Overview
  + Background: Why are we building this?
  + Objective: What problem are we solving?
  + Goals: What do we want to achieve?

- Problem Statement
  + Describe the user pain point or business problem.
  + Who is affected (the key users)?
  + Why is this important now?

- Functional Requirements
  + Ensure the functional requirements are designed to solve the problem statement.
  + Write all the functional user stories here. For each user story, it must contain:
    - title
    - statement: **As a** <type of user>, **I want** <goal>, **so that** <reason/benefit>.
    - requirement detail explaining the statement
    - acceptance criteria, in **given-when-then** format

- Non-Functional Requirements  
  Leave it blank

- Dependency & Constraints  
  State explicitly any limitations (e.g., only for desktop web, not mobile yet).

- Success Metrics
  + How do we measure success?
  + Example:
    - Increase signup conversion to 2000 new user/month
    - Reduce drop-off rate by 10%.
    - Improve task completion time by a minimum of 30 minutes
