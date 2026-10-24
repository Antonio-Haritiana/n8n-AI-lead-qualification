# n8n AI Lead Qualification & Follow-Up

An n8n automation project that captures business enquiries, stores lead information in HubSpot, uses Google Gemini to qualify leads, generates personalized follow-up emails, and alerts the team about high-priority leads through Slack.

Note: 
n8n is self-hosted inside docker on my Ubuntu VM

## Project Overview

Businesses often handle incoming enquiries manually, which can delay responses and make it difficult to prioritize potential customers.

This project demonstrates how workflow automation and generative AI can streamline that process. When a lead submits a form, the workflow stores or updates their contact in HubSpot, uses Google Gemini to evaluate the lead, generates a personalized follow-up email, and notifies the team through Slack when a lead is classified as Hot.

**Project goal:** Demonstrate practical skills in workflow automation, AI integration, CRM operations, conditional logic, and API-based service integration.

## Key Features

- **Lead capture:** Collect enquiry information through an n8n form.
- **CRM integration:** Create or update contact records in HubSpot.
- **AI-powered qualification:** Use Google Gemini to classify leads as Hot, Warm, or Cold and assign a score from 0 to 100.
- **Qualification reasoning:** Generate an explanation for the assigned lead score.
- **Personalized follow-up:** Generate and send a tailored email through Gmail.
- **Conditional notifications:** Send a Slack notification only when a lead is classified as Hot.
- **Structured AI output:** Process the model's response as JSON for use in subsequent workflow steps.

## Workflow Architecture

1. **Form Trigger** — Receives a new lead's information.
2. **HubSpot** — Creates the contact record.
3. **AI Agent (Google Gemini)** — Evaluates the lead, assigns a score and category, and generates a personalized email.
4. **Conditional Branch** — Checks whether the lead qualifies as Hot.
5. **Slack** — Notifies the team about Hot leads.
6. **Edit Fields and Gmail** — Prepares the email fields and sends the personalized follow-up.

## Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow orchestration and automation logic |
| HubSpot | Contact management and CRM |
| Google Gemini | AI-powered lead qualification and email generation |
| Gmail | Automated email follow-up |
| Slack | High-priority lead notifications |

## Lead Qualification Logic

The AI assigns a score from 0 to 100 and classifies each lead using the following thresholds:

| Category | Score | Workflow behavior |
|---|---:|---|
| Hot | 70–100 | Sends a personalized email and triggers a Slack notification |
| Warm | 40–69 | Sends a personalized email |
| Cold | 0–39 | Sends a personalized email |

The AI also provides a short explanation for its classification. These scores are AI-generated assessments, not guaranteed predictions of conversion.

## Example AI Output

```json
{
  "qualification_status": "Hot",
  "lead_score": 90,
  "reasoning": "The lead indicates a strong need and high urgency.",
  "firstname": "Alex",
  "client_email_address": "alex@example.com",
  "personalized_email": "Subject: Following up on your enquiry\n\nHi Alex,\n\nThank you for reaching out. Based on the needs you shared, I'd be happy to discuss how we may be able to help.\n\nWould you be available for a short conversation this week?\n\nBest regards"
}
```

*This is illustrative sample data, not a real customer's information or a guaranteed model response.*

## Setup and Usage

### Prerequisites

- An n8n instance
- A HubSpot account with appropriate access
- Google Gemini API access
- A Gmail account and configured credentials in n8n
- A Slack workspace and configured credentials in n8n

Some services may have usage limits or costs depending on the account and current provider terms.

### Installation

1. Download `workflow/lead-qualification.json` from this repository.
2. Open your n8n instance and import the workflow JSON.
3. Configure your own credentials for HubSpot, Google Gemini, Gmail, and Slack.
4. Verify the form fields and their mappings to the HubSpot contact properties.
5. Configure the Slack notification recipient for your own workspace.
6. Submit test leads representing Hot, Warm, and Cold scenarios.
7. Verify contact creation or updates, AI output, email delivery, and Slack notification behavior.

**Important:** Credential setup and field mapping may require adjustments based on your accounts and n8n version.

## Testing

The workflow should be tested with different lead scenarios before being used with real customers.

| Test case | Expected result |
|---|---|
| Hot lead | Contact is processed, personalized email is sent, and Slack notification is triggered |
| Warm lead | Contact is processed and personalized email is sent without a Hot-lead Slack alert |
| Cold lead | Contact is processed and personalized email is sent without a Hot-lead Slack alert |
| Missing or invalid input | Behavior should be checked and appropriate validation or error handling added if needed |

Actual results depend on the submitted data, model response, and external service configuration.

## Current Scope and Limitations

This project currently focuses on **form-based lead intake**.

The following capabilities are not yet implemented:

- Monitoring an email inbox for new enquiries
- SMS follow-up
- Advanced error handling and retry logic
- Human approval before sending AI-generated emails
- Persistent tracking and evaluation of AI qualification accuracy

The workflow is a portfolio demonstration and should be tested and reviewed before production use.

## Potential Improvements

- Add email-triggered lead capture.
- Integrate SMS notifications or follow-ups.
- Add validation and error-handling paths.
- Introduce human review for uncertain or high-impact AI decisions.
- Build a test dataset to measure classification consistency and email quality.
- Add monitoring and reporting for workflow performance.

## Skills Demonstrated

- Visual workflow design with n8n
- CRM integration and contact data mapping
- Generative AI integration and prompt design
- Structured JSON output handling
- Conditional branching and business rules
- Automated email generation and delivery
- Slack notifications
- Workflow testing and technical documentation

## Disclaimer

This project was created for learning and portfolio demonstration purposes. It does not represent an official implementation for any specific business.

Use your own credentials, avoid committing API keys or customer data, and validate AI-generated classifications and messages before using them in real business operations.

