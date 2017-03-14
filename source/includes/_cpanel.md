# Bitext Control Panel

Everything you need to work with Bitext, including text analysis tools, account management, access to Bitext products and services, support, and an interactive API testing tool – which lets you test the Bitext API – are all accessible right from in the Bitext control panel.

Each time you log in to Bitext, you arrive at the main page of the Bitext control panel. There are four tabs on the left-hand side of the main page: My Profile, My Subscriptions, Add Subscriptions, API Test Tool and Quick Start Guide.

## My Profile

Your account information is accessible from the My Profile tab on the left-hand side of the control panel.

To update your personal information or change your password, click Personal Info. The API Credentials area is particularly important because it is here that you will find the authentication token that you need to make any requests to the Bitext API from your own code.

The My Profile screen is also accessible from the top right-hand corner of the control panel, where your email appears. When you click your email, a dropdown menu gives you two options:

* **Log Out:**
Close your control panel session
* **My Profile:**
View and edit your account information

<img alt="Control panel image 1" src="/images/cpanel-1.png" />

## My Subscriptions


The first time you log in to Bitext, the My Subscriptions screen will appear empty, and you will be prompted to either test drive Bitext using the API Test Tool, or add a subscription to your account on the Add Subscriptions page (see the Add Subscriptions section below for instructions).

Subscriptions are paid on a monthly basis via credit card and may be cancelled at any time. All subscriptions enable 50 MB of text analysis requests/month. If you have needs for larger volumes of text analysis, please contact us at api@bitext.com.

The My Subscriptions screen displays a list of your current subscriptions, including the following details about each one:

* **Language:**
The language in which you have the Bitext API activated (English, Spanish, etc.)

* **Subscriptions:**
The type of text analytics service(s) that you have activated for that particular language (sentiment analysis, entity extraction, etc.).

You may see indications to the right of your subscriptions to alert you about things you should be aware of.

If you see "Trial" it means that this subscription is in a 30-day free trial period. If you click, you will see the end date of the Trial.

"Not Active" indicates that there is an issue with the subscription that may be related to payment or to having exceeded your monthly MB limit. If you click, details will be displayed.

* **MB Used:**
All subscriptions allow for 50 MB of text analytics requests. This column indicates how much you have used. When you have used up your requests, the number appears in red.

The following buttons appear to the right of each item in the list, and allow you to add or cancel services.

* **Subscribe:**
This button appears next to services you have previously used that are no longer active. When you click Subscribe, you will go to our secure payment portal to enter payment details so you can set up your monthly payment and begin using the service immediately. To turn a Trial subscription into a paid subscription, click the "Add Payment" button and you will be directed to our secure payment gateway where you can enter payment details.

* **Cancel:**
This button allows you to cancel your paid subscriptions. Your Bitext service will remain active until the end of the billing cycle. You will see a tag to the right of the subscription that says "Your last month".

<img alt="Control panel image 2" src="/images/cpanel-2.png" />

## Add Subscriptions

Bitext subscriptions are always free for 30 days, with 50 MB of usage, no credit card required. Once you have added a subscription, it will appear in your **My Subscriptions** list as a "Trial".

To add a subscription, use the form at the bottom of the **Add Subscriptions** screen. First select a language from the dropdown menu (English, Spanish, etc.) and then select the subscription you want to use for that language (sentiment analysis, entity extraction, etc.) To see the details of the subscription you have selected, click Subscription Details.

Click Subscribe, and your 30-day free Trial of the selected product will begin. If you are sure you want to continue with Bitext and don’t want to wait until your Trial ends to enter payment details, you can enter them right now by clicking the box in the Select a subscription form that says **Add payment details now**.

The system will direct you to our secure payment gateway where you can set up your monthly payment. As soon as the 30-day trial period ends, your subscription will begin.

If you don’t want to do this now, you can do it at any time in the future, by simply clicking the Add Payment button that appears to the right of the subscription on the **My Subscriptions** page.

If you have not upgraded your Trial subscription to a paid subscription, we will send you reminder when the Trial period is about to expire. If, at the end of your trial period, you have not entered your payment information, your subscription will become inactive, but you can reactivate it at any time by simply clicking the Add Payment button.

You can cancel a subscription at any time by clicking Cancel button to the right of the subscription on the **My Subscriptions** screen.

<img alt="Control panel image 3" src="/images/cpanel-3.png" />

## Api Test Tool

The API Test Tool lets you test out different Bitext API services using easy interactive graphics. It’s a great way to test the different text analysis services to decide which one is right for you.

The tool consists of a screen with a text area, where you can enter a selection of text for analysis (max 400 characters).

Above the text area are three dropdown menus, from which you choose the kind of analysis you want to perform, and how you want to view your results.

* **Language:**
First, select the language of the text you are using to test Bitext (English, Spanish, etc.)

* **Text Analysis Service:**
Select the service you want to test on your text. (sentiment analysis, entity extraction, etc.)

* **Output Type:**
Select one of the two output types available for your analysis: JSON code or a very user-friendly graphical representation, which allows you to see all the parts of your analysis with colored visual cues.

<img alt="Control panel image 4" src="/images/cpanel-4.png" />

Once you have entered a text and selected the kind of analysis you want to perform, click the Analyze Text button. If you have chosen to see your results as JSON, the analysis will appear in JSON to the right of the text area.

<img alt="Control panel image 5" src="/images/cpanel-5.png" />

If you have selected to view your results graphically, the analyzed text will appear directly in the text area, with a legend to the right of the text area to help you understand the icons and color coding.

For example, if you have done an entity extraction, all entities found in the text will appear with a red background, with an icon to the right that identifies the type of entity. If you have done a concept extraction, all concepts found in the text will appear with a red background, with an icon to the right that identifies the type of concepts. And if you have done a categorization, all categorized sentences will appear with a red background, with an icon to the right that identifies the category.

<img alt="Control panel image 6" src="/images/cpanel-6.png" />

In a sentiment analysis, each significant word is highlighted. A legend appears to the right of the text area to help you understand the analysis.

* Sentiment topics (topics identified as being the target of a positive or negative opinion) are depicted in bold font, inside a rectangular box

* Positive sentiment texts (positive opinions about a sentiment topic) appear with green background.

* Negative sentiment texts (negative opinions about a sentiment topic) appear with red background.

* A small superscript number links the sentiment texts with their respective sentiment topics.

<img alt="Control panel image 7" src="/images/cpanel-7.png" />

## Coding Plan

In order to use the Bitext categorization service, you need to create a coding plan first, so that the Bitext engine understands what you are looking for. A coding plan is simply a set of categories and words (or terms) that relate to the information you want Bitext to extract from your data.

For example, if you are a hotel chain that wants to quickly understand the contents of thousands of customer reviews, you might create the categories Price, Quality and Customer Service. For each of these categories you would then add and associate related words or terms. For example, the terms "expensive", "cheap" and "overpriced" would likely be associated with the category Price. When Bitext detects these words in a sentence, it automatically assigns them to the category Price.

The Bitext API Test Tool has a default coding plan template that is useful for reviews about technological devices. The categories it uses (in English) are Application, Product, Quality, Price, Service, and Image. In the future, there will be additional coding plan templates available that relate to specific sectors. Default Bitext coding plans cannot be deleted of modified, but can be used as templates to create your own coding plans.

<img alt="Control panel image 8" src="/images/cpanel-8.png" />

Creating your own coding plans allows for customizability. You can be sure that the exact words your customers are most likely to use will be flagged and categorized by the Bitext engine. To create a coding plan, click ‘Add Coding Plan’ from the subitem of the next level menu.

<img alt="Control panel image 9" src="/images/cpanel-9.png" />

New coding plans are created by filling out the form on the right-hand side of the screen. If you want to use an existing coding plan as your base, select a template from the dropdown list of templates at the bottom of the form.

As soon as you have submitted the form, your new coding plan will appear in the list on the left-hand side of the screen. Each coding plan is automatically assigned a ‘key,’ which is a numeric value that is used in the code to identify the correct coding plan for the analysis. Every time the endpoint ‘categories’ is used, this ‘key’ must be entered in the code.

To set up the coding plan you have created, click on it from the list at left. A setup tool will open. It is here where you create categories and words that are related to your coding plan

<img alt="Control panel image 10" src="/images/cpanel-10.png" />

The categories box on the left-hand side will be empty initially. To add a category, enter its name in the ‘Add new’ field and click Save. The Terms box on the right-hand side will also be empty until you manually add the terms that you want the Bitext engine to flag in your database.

Once you have entered all your trigger words in the Terms box, you can simply drag & drop each one to its associated category box on the left-hand side of the screen. When Bitext encounters this word or term in your text, it will automatically assign it to the correct category.

So, returning to the example of a hotel chain that needs to understand customer reviews, you would first create the category Price in the Categories box. Then, in the Terms box on the right-hand side, manually enter terms like "expensive", "cheap" or "overpriced." Then you would assign those terms to the appropriate category by dragging and dropping them. Whenever Bitext detects these words, it will automatically associate them with the Price category.
