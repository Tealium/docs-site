---
title: Global consent parameters
description: The Consent Prompt Manager and the Consent Preferences Manager use parameters to represent translatable text that displays in the prompts.
url: https://docs.tealium.com/consent/client-side/consent-management/global-parameters/
---
## How it works

The [Consent Prompt Manager]() and the [Consent Preferences Manager]() use parameters to represent translatable text that displays in the prompts. The prompts are generated using CSS, HTML, and JavaScript where these parameters are referenced using the syntax `{{parameter_name}}`. When the code is generated, each `{{parameter}}` is replaced by its configured value. These parameters and values can then be defined at the account level or in each profile.

Additional languages can also be configured at the account level. This makes it easy to create translations of your parameters at the account level and make them available to all profiles within your account.

Parameters are set separately for the **Explicit Consent Prompt Manager** and the **Consent Preferences Manager**.

## Managing global consent resources

The global consent resources are accessed from the **Admin** menu at the upper-right of the screen. Only users with the Manage Account permission have access to this feature.

Use the following steps to access the global consent resources:

1. In the admin menu, click **Global Consent Customization** from the drop-down menu. The **Global Consent Customization** dialog appears.
1. Select the tab for the feature you want to manage, **Explicit Consent Prompt** or **Consent Preferences Dialog**.  
    ![](/images/iq-tag-management/consent-manager-global-consent-customization.jpg)

### Setting parameter values

The consent features use the following built-in parameters:

* **Title** `{{title}}`  
The main heading of the prompt.
* **Message** `{{message}}`  
Your message to customers to inform them about your tracking intentions and links to other resources such as a privacy policy or contact form.
* **Opt-in/Opt-out** `{{opt_in}} / {{opt_out}}`  
The two options available:
    * opt-in - grant consent
    * opt-out - deny consent

* **Confirmation Button** `{{confirmation_button}}`  
The label on the submission button.

Enter a value for any of these parameters and click **Apply**.

### Adding custom parameters

Custom parameters can be added to further customize your prompts. These parameters can be referenced within the built-in parameters or within the CSS/HTML/JavaScript code.

As a best practice, avoid putting translatable text directly in the HTML or JavaScript. Instead, customize the code with`{{parameters}}`and define that content using custom parameters.

Use the following steps to add a custom parameter:

1. Scroll down to the **Custom Parameters** section and click **&#43; Add Parameter**.  
    ![](/images/iq-tag-management/consent-manager-custom-parameters.jpg)  
The **Custom Parameter** dialog appears.
1. Enter a name for the parameter.
1. Click **Apply**.  
The new custom parameter appears in the list.
1. Enter a value for the new parameter.  
This value will be substituted where the parameter is referenced.
1. Click **Finish**.

### Adding a language

The consent features are built with automatic language detection. The language setting is detected in the browser, for example, the two-character language code &#34;de&#34; for German. If the language detected is configured, this code presents the corresponding version of the prompt. The prompts are configured in English (&#34;en&#34;) as the default.

Use the following steps to add a language:

1. To the right of **Language** in the side panel, click **&#43; Add**.  
The **Add Language** dialog appears.
1. Select the language from the list and click **Apply**.  
The new language displays under English (en) in the **Language** side panel.
1. Click the new language to configure the content for that language.
1. Enter the translated values in the parameter fields.
1. If the new language will be the default language, check the **Make Default Language** checkbox.  
    ![](/images/iq-tag-management/consent-manager-make-default-language-checkbox.jpg)
1. Click **Finish**.

### Save/Publish workflow

The global consent parameters are saved at the account level, therefore you do not need to save and publish to save your changes. To save the changes so that they are reflected at the profile level, you must save and publish the profile.

The following steps describe the workflow for updating and publishing global consent parameters:

1. In the admin menu, click **Global Consent Customization**.
1. Make changes to the parameters and click **Apply**.  
It is not necessary to do a save/publish.
1. Switch to the profile that you want to update.  
When the profile loads, the latest global consent parameters will be imported and the **Save/Publish** button will display in orange to indicate that unsaved changes are present.
1. To preview the latest global changes, go to the **Consent Management** screen and click **Preview**.
1. Verify the updates and close the preview window.
1. Click **Save/Publish** and follow your normal release process for publishing to Dev/QA/Prod.

Steps 3 – 5 must be performed for each profile that inherits the global consent parameters.
