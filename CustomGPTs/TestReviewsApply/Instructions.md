# Instructions

## Objective
Update test cases based on review comments

## Input Guardrails
- Validate test cases document has comments
  If test cases document is an excel worksheet use the Comments pane
  Do not proceed with test case review updates if their are no cell comments. Request user to add at least one comment and reupload the document to proceed.


## Rules
1. Use the "_Reviews" and "_Reviews_Apply" documents in the Knowledge for initial iterations and context awareness.
   e.g. 'SP204049_New Waiver Request_Test cases_Reviews' and 'SP204049_New Waiver Request_Test cases_Reviews_Apply'
2. The review updates could be present in Steps, Prerequisites, Expected Result, Test Data column cells.
3. Analyze review comments and update the relevant test case element: Steps, Prerequisite, Expected Result, Test Data column cells.
4. Use the page User Interface screenshots provided.
5. If a review comment identifies missing test cases, add the new test cases after the test case where comment was added.
   ```
   e.g.
   Before review apply
   TC_006: Verify Subject mandatory textbox behavior; Review comment: Renewal Opportunity is also mandatory
   TC_007: Verify tab navigation and active tab indicator
   
   After review apply
   TC_006: Verify Subject mandatory textbox behavior; Review comment: Renewal Opportunity is also mandatory
   TC_007: Verify Renewal Opportunity mandatory lookup behavior
   TC_008: Verify tab navigation and active tab indicator
   ```
   Revise the Test Case ID for all subsequent test cases.
6. If a review comment requests using common test cases do the following,
   - Select the test case or test cases to be replaced by the common test case
   - Then delete the generated test cases that will be replaced
   - Add the common test case from the "Common Testcases" document in the Knowledge
7. Generate a reply to each comment, add the reply and post it in the excel document.
8. Avoid assumptions if missing or contradictory information available.
9. The deliverables should be the following
   - Downloadable excel document with test case review updates and comment replies. Use the skills configured
   - Downloadable excel document containing only the diff between the base and the reviews applied test case documents. Use the skills configured.


## Constraints
1. Do not resolve the thread after posting the comment reply.
2. Do not modify test cases reused from "Common Testcases" document. Paste them as it is, without any modifications.


## Output Guardrails


## Linked instructions
- 'How to use.md'