Interior Design Voice AI Agent
This project automates lead qualification and client communication for Interia, a growing interior design firm. The system uses n8n for workflow automation and Vapi/ElevenLabs for voice synthesis.

Technologies Used
n8n: Automation platform.

Vapi/ElevenLabs: Voice AI tools for creating the agent.

Airtable/Google Sheets: Lead management.

Twilio: For making outbound calls.

OpenAI: For advanced conversation intelligence (optional).

Setup Instructions
1. Airtable/Google Sheets Setup:
Create the following tables:

Leads: Stores lead details (Name, Contact, Status, etc.)

Call Records: Logs call details (start time, call status, etc.)

2. n8n Workflow Setup:
Import the n8n JSON workflow into your instance.

Set up API integrations for Twilio and Vapi/ElevenLabs.

Configure triggers to periodically fetch new leads from Airtable/Google Sheets.

3. Voice Agent Configuration (Vapi/ElevenLabs):
Set up your voice agent with the required persona.

Define the conversation flow and qualification logic in Vapi/ElevenLabs.

4. Twilio Configuration:
Integrate Twilio with n8n for outbound calls.

Configure test phone numbers for the system.

How It Works
Lead Retrieval: Leads with the "TBC" status are fetched from Airtable/Google Sheets.

Voice Interaction: The voice agent calls the lead, collects information, and qualifies the lead.

Lead Status Update: Based on the outcome, the lead status is updated in Airtable/Google Sheets (e.g., "In-Progress," "Called," "Failed").

Edge Case Handling
Unanswered Calls: Retry after 1 minute, mark as "Failed" after two attempts.

Abusive Language: The agent responds politely and ends the call.

Callback Requests: Reschedule calls based on the client’s request.

Running the System
Automated Workflow: Use the n8n workflows to automate lead management.

Monitor Progress: Check Airtable/Google Sheets for lead status updates and call results.
