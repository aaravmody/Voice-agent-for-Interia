# Interior Design Voice AI Agent

## Overview

The Interior Design Voice AI Agent automates lead qualification and client communication for **Interia**, an interior design firm. This system integrates multiple technologies to streamline the process of handling incoming leads, qualifying potential clients, and managing client communications.

## Technologies Used

- **n8n**: Workflow automation platform.
- **Vapi**: Voice synthesis tools for creating the AI agent.
- **Airtable**: Platforms for lead management.
- **Twilio**: Service for making outbound calls.
- **OpenAI**: Optional integration for advanced conversational intelligence.

## Setup Instructions

### 1. Airtable/Google Sheets Setup

- **Leads Table**: Create a table with the following columns:
  - `id`: Unique identifier for each lead.
  - `First Name`: Lead's first name.
  - `Last Name`: Lead's last name.
  - `Mobile`: Lead's mobile number.
  - `Email`: Lead's email address.
  - `Status`: Current status of the lead (e.g., TBC, In-Progress, Called, Failed).
  - `Attempt`: Number of call attempts made.
  - `Date Time`: Date and time of the lead's submission.
  - `Summary`: Brief summary of the lead's inquiry.
  - `Assignee`: Assigned staff member.
  
- **Call Records Table**: Create a table with the following columns:
  - `id`: Unique identifier for each call record.
  - `callproviderID`: Identifier for the call provider.
  - `phonenumberID`: Identifier for the phone number used.
  - `customernumber`: Customer's phone number.
  - `type`: Type of call (e.g., outbound, inbound).
  - `started`: Call start time.
  - `ended`: Call end time.
  - `milliseconds`: Duration of the call in milliseconds.
  - `cost`: Cost of the call.
  - `ended reason`: Reason for call termination.
  - `transcript`: Transcript of the call.

### 2. n8n Workflow Setup

- **Workflow 1: Outbound Calling**
  - **Trigger**: Schedule the workflow to run at regular intervals.
  - **Action**: Fetch leads with the status "TBC" from Airtable/Google Sheets.
  - **Process**: Initiate calls through Vapi/ElevenLabs and update the lead status to "In-Progress".

- **Workflow 2: Call Result Processing**
  - **Trigger**: Set up a webhook to receive call results.
  - **Action**: Process different call outcomes (e.g., successful, unanswered, failed).
  - **Process**: Update lead statuses based on outcomes and create detailed call records in Airtable/Google Sheets.

### 3. Voice Agent Configuration (Vapi/ElevenLabs)

- **Agent Setup**: Configure the voice agent with a professional and warm persona.
- **Conversation Flow**: Define the structured conversation path, including:
  - Introduction and purpose of the call.
  - Need discovery and information gathering.
  - Qualification assessment.
  - Next steps based on qualification.
  - Professional closing.

- **Qualification Questions**: Program the agent to ask key questions regarding:
  - Budget alignment.
  - Project location.
  - Timeline expectations.
  - Scope of the project.
  - Property size.

### 4. Twilio Configuration

- **Integration**: Connect Twilio with n8n to handle outbound calls.
- **Test Numbers**: Configure test phone numbers to simulate client interactions during development.

## How It Works

1. **Lead Retrieval**: The system fetches leads with the "TBC" status from Airtable/Google Sheets at scheduled intervals.
2. **Voice Interaction**: The voice agent contacts each lead, introduces itself, asks qualifying questions, and gathers necessary information.
3. **Lead Status Update**: Based on the conversation outcome, the lead's status is updated in Airtable/Google Sheets (e.g., "In-Progress," "Called," "Failed").
4. **Call Logging**: Detailed records of each call, including transcripts and outcomes, are stored in the Call Records Table for future reference.

## Edge Case Handling

- **Unanswered Calls**: If a call is not answered, the system retries after 1 minute. After two failed attempts, the lead is marked as "Failed" with the reason "Unreachable".
- **Abusive Language**: The agent is programmed to respond professionally to inappropriate language and end the call politely if necessary.
- **Identity Denial**: If a client denies making an inquiry, the agent apologizes for the confusion and verifies the contact information.
- **Callback Requests**: The system allows clients to request callbacks at specific times, which are scheduled accordingly.

## Running the System

- **Automated Workflow**: The n8n workflows automate the process of fetching leads, initiating calls, and updating statuses.
- **Monitoring**: Regularly check Airtable/Google Sheets for updates on lead statuses and review call records for quality assurance.

## Evaluation Criteria

- **Functionality**: Ensure that the workflows correctly fetch leads, initiate calls, and update statuses as intended.
- **Voice Agent Effectiveness**: The agent should efficiently qualify leads while maintaining a professional and helpful demeanor.
- **Error Handling**: The system should gracefully manage edge cases such as unanswered calls and inappropriate language.
