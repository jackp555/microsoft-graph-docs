# Microsoft Graph Quick Start FAQ

This FAQ addresses questions and issues that you might encounter as you run through one of the [Microsoft Graph Quick Starts](https://developer.microsoft.com/en-us/graph/quick-start).

## What do the quick starts do?

Regardless of the platform you choose, each quick start does the following:

- Registers a new application for you in the [Application Registration Portal](https://apps.dev.microsoft.com). This is why we ask you to sign in with a Microsoft account when you **Get an app ID**. If your application will require an app secret, the quick start will create one for you. 
- Downloads a copy of sample code stored in a GitHub repo. You can see these repos in the [MicrosoftGraph organization](https://github.com/microsoftgraph?utf8=%E2%9C%93&q=connect) on GitHub.
- Inserts the new app ID, and wher necessary the app secret, into a configuration file inside the sample code stored in the GitHub repo. We don’t want to send sensitive information inside an HTTP request, so we ask you to copy the app secret after we create the new application, and then copy it into a form in the quick start before you download a copy of the sample.
- Prompts you to download the fully configured sample. After you download and unzip the sample code, you'll have a client or web application that should run, assuming that you've installed the specified prerequisites (IDEs, web frameworks, and so on) in your development environment.


## Why won't my  ASP.NET, UWP, or Xamarin project build?

If a sample that uses .NET libraries fails to build in Visual Studio, one or more of your projects might be running up against the 260-character Windows path length limit. Xamarin solutions, in particular, are susceptible to this, especially Android projects inside Xamarin solutions. Try moving the solution to a location at or close to the root directory. 

## If a web platform quick start provides REST and SDK samples, can I run them both at the same time?

Yes, you can run both samples at the same time. Just make sure that one of them isn't running on the default port. This means that when you start your test web server, you'll need to specify a port number for at least one version of the sample.

## I didn’t get an email and I see no errors or exceptions. Why didn't this work?

If the sample appears to send an email but you don't see it in your Inbox, check your junk or spam folder. If you're sending the message from a test tenant, the message might get flagged as spam.

## I get an error when I try to sign in and authorize the sample app. What steps can I take to fix this? 

First try to run the sample app in an InPrivate or Incognito window. Sometimes web browser cache settings can cause the authorization step to fail, especially if you sign in with multiple Microsoft accounts. If that doesn't work, please follow up with us on [Stack Overflow](https://stackoverflow.com/questions/tagged/microsoft-graph). Be sure to tag your question with microsoft-graph and copy the error information into the question.

## Why do some quick starts include an app secret and others don’t?

Server-side web applications that need to make secure calls to the Microsoft Graph API require app secrets. This is why the quick starts for ASP.NET MVC, Node.js, PHP, and Ruby provide an app secret.

## Why doesn't the Angular quick start give me an app secret when all the other web platform quick starts do?

An app secret is required only for server-side web applications.

## Why does my quick start contain a Readme file?

Each quick start registers a new application and creates a zip file that contains the contents of a GitHub repo. It updates the files in the repo so that you don't have to configure the sample application in the repo. You'll find these repos in the [MicrosoftGraph organization](https://github.com/microsoftgraph?utf8=%E2%9C%93&q=connect) on GitHub.

Feel free to look at the repo associated with each quick start, file issues there, and/or follow the instructions in the Readme to register your own application. Follow the **Just give me the sample code** link under step 2 of each quick start to go to the associated repo.

## Why did the sample give me an image containing a thought bubble?

Most of the samples provided by the quick starts get your profile picture and upload it to the root directory of your OneDrive account. If you sign in with a Microsoft account (live.com, hotmail.com), Microsoft Graph can't currently fetch your profile picture, so we fall back to the thought bubble image. The sample also uses this image if your account doesn't have a profile picture.

## Why do you provide a **[Manage your app](https://apps.dev.microsoft.com)** link after I get an app ID?

We provide this link because the app ID step registers a new application for you in the [Application Registration Portal](https://apps.dev.microsoft.com). We provide this link so that you can view the settings for this application, delete the application, or even update the settings for the application after you run the sample. 

## Didn't find what you need?

If this FAQ didn't address a question you have or a problem you encountered with one or more of the quick starts, please report your question or problem on [Stack Overflow](https://stackoverflow.com/questions/tagged/microsoft-graph). 

If your problem is related to the code sample provided by the quick start, you can also file an issue in the GitHub sample repo. You can find the repo by following the **Just give me the sample code** link under step 2 for each quick start.
