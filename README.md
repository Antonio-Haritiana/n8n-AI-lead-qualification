# n8n AI Lead Qualification & Follow-Up

An n8n automation project that captures business enquiries, stores lead information in HubSpot, uses Google Gemini to qualify leads, generates personalized follow-up emails, and alerts the team about high-priority leads through Slack.

Note: 
n8n is self-hosted inside docker on my Ubuntu VM

## Workflow Overview

1. **Lead capture:** Collects business enquiries through an n8n form.
2. **CRM integration:** Creates or updates a contact in HubSpot.
3. **AI qualification:** Uses Google Gemini to assign a score from 0–100 and classify the lead as Hot, Warm, or Cold.
4. **Personalized follow-up:** Generates and sends a tailored email based on the submitted information.
5. **Hot-lead notification:** Sends a Slack notification when a lead is classified as Hot.

## Tech Stack

- n8n — workflow automation
- HubSpot — CRM and contact management
- Google Gemini — AI-powered lead qualification and email generation
- Gmail — email follow-up
- Slack — hot-lead notifications

## Requirements

- An n8n instance
- HubSpot account and configured credentials
- Google Gemini API access
- Gmail and Slack accounts with configured n8n credentials

## Setup

1. Download `workflow/lead-qualification.json`.
2. Import the JSON file into n8n.
3. Configure your own credentials for HubSpot, Google Gemini, Gmail, and Slack.
4. Verify the form fields and HubSpot property mappings.
5. Test the workflow with sample leads before enabling it for real submissions.

## Testing

Test with different sample leads to check:

- Contact creation in HubSpot
- AI classification and lead score
- Email personalization and recipient address
- Slack notification for Hot leads only

## Current Scope & Limitations

- Leads are captured through the n8n form.
- Incoming enquiries from an existing email inbox are not yet automated.
- SMS follow-up is not implemented.
- AI classifications are estimates and should be reviewed before being used for important business decisions.
- External services may have usage limits or costs.

## Future Improvements

- Capture enquiries from incoming emails.
- Add SMS follow-up.
- Add more test cases and error handling.
- Improve lead scoring with explicit, configurable business rules.

## Disclaimer

This is a portfolio project built for demonstration and learning purposes. Use your own credentials and test data. No credentials or secrets should be committed to the repository.
