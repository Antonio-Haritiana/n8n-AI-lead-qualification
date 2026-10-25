# Test Cases — AI Lead Qualification Workflow

## 1. Objective

Validate that the n8n workflow correctly processes leads, classifies them using Google Gemini, sends personalized emails through Gmail, and notifies the team through Slack for Hot leads only.

## 2. Test Environment

- **Workflow:** n8n AI Lead Qualification
- **CRM:** HubSpot
- **AI model:** Google Gemini
- **Email service:** Gmail
- **Notification service:** Slack
- **Test data:** Fictional lead information

## 3. Test Cases

### TC-01: Hot Lead — End-to-End Test

**Input:** A lead reports an urgent business problem and expresses strong interest in finding a solution.

**Expected Results:**
- Contact is created or updated in HubSpot.
- AI returns a valid JSON response.
- Qualification status is `Hot`, with a score between 70 and 100.
- Personalized email is sent successfully.
- Slack notification is triggered.

**Actual Results:** All expected actions completed successfully.

**Status:** Pass 

**Evidence:**
- `screenshots/01-hot-lead-execution.png`
- `screenshots/02-hot-lead-ai-output.png`
- `screenshots/03-hot-lead-email.png`
- `screenshots/04-hot-lead-slack.png`

---

### TC-02: Warm Lead — Conditional Branching

**Input:** A lead expresses interest but has moderate urgency.

**Expected Results:**
- AI returns a `Warm` classification with a score between 40 and 69.
- Personalized email is sent successfully.
- No Hot-lead Slack notification is triggered.

**Actual Results:** All expected actions completed successfully.

**Status:** Pass.

**Evidence:** 
- `screenshots/05-warm-lead-ai-output.png`
- `screenshots/06-warm-lead-execution.png`
---

### TC-03: Cold Lead — Conditional Branching

**Input:** A lead expresses limited interest and has no immediate need.

**Expected Results:**
- AI returns a `Cold` classification with a score between 0 and 39.
- Personalized email is sent successfully.
- No Hot-lead Slack notification is triggered.

**Actual Results:**  All expected actions completed successfully.

**Status:** Pass.

**Evidence:** 
- `screenshots/07-cold-lead-ai-output.png`
- `screenshots/08-cold-lead-execution.png`
---

### TC-04: CRM Field Mapping

**Input:** Submit a form with a fictional first name, last name, email, and enquiry details.

**Expected Results:**
- Contact information matches the submitted form.
- Enquiry details reach the AI Agent correctly.

**Actual Results:** All expected actions completed successfully.

**Status:** Passed.

**Evidence:** 
- `screenshots/09-1-form_data.png`
- `screenshots/09-hubspot-field-mapping1.png`
- `screenshots/09-hubspot-field-mapping2.png`

---

### TC-05: AI Output Validation

**Input:** Inspect the AI Agent output after a form submission.

**Expected Results:**
- Output is valid JSON.
- All required fields are present.
- Lead score is within 0–100.
- Qualification status matches the score thresholds.
- Email content does not invent unsupported information.

**Actual Results:** All expected actions completed successfully.

**Status:** Passed

**Evidence:** 
- `screenshots/02-hot-lead-ai-output.png`
- `screenshots/05-warm-lead-ai-output.png`
- `screenshots/07-cold-lead-ai-output.png`
---

### TC-06: Email Delivery

**Input:** Submit a test lead using an email address you control.

**Expected Results:**
- Correct recipient, subject, and body.
- Email is received in the test inbox.

**Actual Results:** All expected actions completed successfully.

**Status:** Passed.

**Evidence:** 
- `screenshots/03-hot-lead-email.png`
- `screenshots/10-warm-lead-email.png`
- `screenshots/11-cold-lead-email.png`
---

### TC-07: Duplicate Lead

**Input:** Submit the same test email address twice.

**Expected Results:**
- Existing HubSpot contact is updated rather than creating an unintended duplicate, if the node is configured to match contacts by email.

**Actual Results:** Existing HubSpot contact is updated, not duplicated (in our example it is the company name that is updated)

**Status:** Passed

**Evidence:** 
- `screenshots/09-hubspot-field-mapping1.png`
- `screenshots/12-hubspot-update-field-mapping1.png`
---

### TC-08: Missing or Invalid Input

**Input:** Test a missing optional field or an invalid email where the form permits it.

**Expected Results:**
- Invalid data is rejected or handled safely.
- Missing optional data does not cause unexpected failures.

**Actual Results:** Invalid data such as email is not permitted, only a valid one is allowed 
Missing optional data does not cause unexpected failure but I think it is better for the AI qualification and lead follow up to have those fields all required (it can for example save time for further investigation if we have all information already there)

**Fix:** Require all fields to be filled

**Status:** Pass with a fix

**Evidence:** 
- `screenshots/13-invalid-email-address.png`
- `screenshots/14-ai-output-missing-optianal-field.png`
- `screenshots/15-required-field.png`

## 4. Test Summary

| Test ID | Scenario | Status |
|---|---|---|
| TC-01 | Hot lead | Pass|
| TC-02 | Warm lead | Pass |
| TC-03 | Cold lead | Pass |
| TC-04 | CRM field mapping | Pass |
| TC-05 | AI output validation | Pass |
| TC-06 | Email delivery | Pass |
| TC-07 | Duplicate lead | Pass |
| TC-08 | Missing or invalid input | Pass with a fix |


## 5. Conclusion

Final conclusions are based on the recorded execution results and supporting evidence. Passing these tests does not guarantee production readiness or AI classification accuracy.

