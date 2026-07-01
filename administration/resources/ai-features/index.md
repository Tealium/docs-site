---
title: Tealium AI Features
description: Tealium offers AI features to enhance your experience in the product interface.
url: https://docs.tealium.com/administration/resources/ai-features/
---
## Introduction

Tealium AI features are designed to enhance your experience by providing intelligent assistance within the product interface. These features are released independently, allowing for incremental updates and improvements.

Access to AI features is managed at the account level and the profile level to allow flexible control over how AI functionality is used within your organization.

## Settings

AI settings are controlled at the account level to determine which AI features are available and at the profile level where you enable or disable those features.

### Requirements

Access to Tealium AI settings requires the following:

* Account admin role

### Account-level settings

Account-level settings determine whether AI functionality is enabled for the account and which features can be managed at the profile level. These settings let you control which AI features can be used across all profiles.

There are two types of account-level settings: global AI functionality and individual AI features.

**Global AI Functionality**

The global AI setting controls whether AI features are available for the account and all profiles.

* **Enabled**: Enables AI functionality for the account and activates the AI feature toggles.
* **Disabled**: Disables AI functionality for the account and all profiles and deactivates the AI feature toggles.

**Individual AI Features**

The individual feature setting controls whether that feature is allowed to be enabled at the profile level.

* **Enabled**: Allows the feature to be turned on or off at the profile level.
* **Disabled**: Deactivates the feature for all profiles, preventing it from being managed at the profile level.

### Profile-level settings

Profile-level settings control which AI features are active within a specific profile.

To enable or disable a feature at the profile level, it must first be enabled at the account level. By default, AI features are disabled at the profile level.

**Individual AI Features**

* **Enabled**: Turns on the feature for all users in the profile.
* **Disabled**: Turns off the feature for all users in the profile.

## Features

Tealium AI features include the following:

### AI Note Generation

The AI Note Generation feature (also known as NoteGen Agent) automatically generates clear, contextually relevant notes for supported configuration components, such as Tealium iQ variables and AudienceStream audiences. This makes it easier for users to quickly understand a component&#39;s configuration and purpose.

![](/images/administration/notegen.png)

Click **AI Note** below the **Notes** field to generate a note for the selected configuration component.

![](/images/administration/notegen-accept.png)

Click **Accept** to use that note.

AI Note Generation is currently available for the following configuration components:

* Tealium iQ variables
* AudienceStream audiences

AI Note Generation for additional configuration components will be added in the future.

### Tealium AI Assistant

The Tealium AI Assistant provides answers to questions about configuring and using Tealium. In addition to general queries, the AI Assistant includes preconfigured buttons for advanced tasks:

* **Latest Profile Version Summary**: Provides a summary of configuration changes made to the profile in the latest published version. Works for both client-side and server-side profiles.
* **Find an Attribute**: Assists in locating server-side attributes based on natural language searches. For example, to find any attributes that use rolling sum enrichments or any attributes referenced by badges.

Access the AI Assistant by clicking the icon at the right side of the top header, as shown below.

![](/images/administration/ai-assistant-icon.png)

#### Ask a question

The AI Assistant provides a simple interface for asking questions, as shown in the following figure.

![](/images/administration/ai-assistant-initial-screen.png)

After you ask a question, the AI Assistant provides an answer. You may need to scroll down to see the complete response. A **Sources** link is included at the end of the response, which provides links to related documentation on [docs.tealium.com](https://docs.tealium.com/).

To get help from the AI Assistant, enter your question in the text box at the bottom of the screen. The question and the results are displayed.

The following example shows the results of asking &#34;How do I create a new attribute?&#34;.

![](/images/administration/ai-assistant-example-question.png)

The following example shows an expanded **Sources** link at the end of the response:

![](/images/administration/ai-assistant-sources-link.png)

----

## Terms of Service for the Tealium AI Assistant

**Effective Date: November 6, 2025**

This Terms of Service (&#34;TOS&#34;) governs your use of the AI Assistant, which is provided and operated by Tealium Inc. (&#34;Tealium&#34;). By using the AI Assistant, you agree that you: (a) are authorized by your employer to use services that include artificial intelligence-enabled technologies, and (b) will comply with these terms. 

1. **Purpose and Functionality.** The AI Assistant is an AI-powered chatbot designed to answer questions about how to use and configure Tealium’s software-as-a-service products. The AI Assistant is built on the AWS Bedrock platform. **The results are not reviewed by a human.** Therefore, use of the AI Assistant is not a substitute for professional advice.

1. **Ability to Opt Out; Additional Questions.** If, for any reason, you do not want to use the AI Assistant, you can contact your assigned CSM for assistance with opting out. You can also email legal@tealium.com to opt out or to ask any questions about this TOS.

1. **User Responsibilities.**
By using the AI Assistant, you agree that you will:  
    * Use it only for lawful purposes.
    * Not input any data that you collect or orchestrate through the use of Tealium’s services (which may be called “Customer Data” or something similar in your master services agreement with Tealium), as the AI Assistant is not designed for processing such information.
    * Not input any other personal data. Personal data means information that relates to an identified or identifiable individual, such as a name, email address, phone number, location data, or IP address. The AI Assistant is not designed for processing such information.

1. **Data Protection and Privacy.**  
    * The AI Assistant processes user interactions in accordance with applicable laws and regulations, including, without limitation, the GDPR, the CCPA, and the European Union Artificial Intelligence Act (the “EU AI Act”).
    * Conversations are not used for model training, but may be monitored for compliance reasons. Conversations are deleted every 30 days.

1. **Compliance with the EU AI Act**  
    * The AI Assistant is classified as a limited-risk AI system under the EU AI Act.
    * Users are informed that they are interacting with AI.
    * Transparency measures ensure that responses are generated autonomously without human review.

1. **Additional thoughts about the AI Assistant**  
    * As with any AI system, Tealium cannot and does not guarantee the accuracy or reliability of AI Assistant responses.
    * Tealium is not liable for any harm arising from reliance on AI Assistant responses.
    * We are still here to help if the AI Assistant doesn’t answer your question. Never hesitate to reach out to your assigned CSM or other Tealium team member if you need additional help. 

1. **Modifications to the TOS.** Tealium reserves the right to update these Terms of Service. Users will be notified of significant changes.
