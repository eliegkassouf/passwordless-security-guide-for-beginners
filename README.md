# Elie's Passwordless & Security Guide for Beginners

## Intro
- ℹ️ It's 4AM where I'm located. I'm taking a little break from work to write this.
- ✳️ I will revise this at a later time and update any discrepancies. 
- ❓ Why am I writing this?
  - I've seen a lot of terrible implementations of "security" and how people handle data carelessly.
  - Security is a very large concern now a days and everyone needs to feel safe and understand that you cannot be easily breached.
- ‼️ I will add code examples eventually when I'm not very busy.
-  ⚠️ Please do not copy and paste. Please reference this url. I will make sure to update over time.


## Contents
- [Getting Started](#getting-started)
- [OAUTH2](#oauth2)
- [I Need A Username Field / I Already Have One](#i-need-a-username-field--i-already-have-one)
- [2FA](#2fa)
- [reCaptcha](#recaptcha)
- [Application Validation](#application-validation)
- [Device/IP Validation](#deviceip-validation)
- [Rate Limiting](#rate-limiting)
- [Resetting Tokens Periodically](#resetting-tokens-periodically)
- [Third Party Firewall and Services](#third-party-firewall-and-services)
- [Encrypt LocalStorage](#encrypt-localstorage)
- [AWS Security Groups](#aws-security-groups)
- [Other Notes](#other-notes)


## Getting Started
- This guide is for anyone looking to secure their services.
- Consider each section as a *layer*. We can use the layers independently or combine them together to create and manage simple/complex rules.
- Always use HTTPS in production. Most external services won't allow you to use HTTP anyway.
- The easiest way to protect your users is not letting them store passwords at all. 
- You cannot expect all your users to understand the importance of security and you cannot expect everyone to know what a password manager is let alone pay for one. 
- Some people will always be ignorant and it's important we don't allow the bad actors to put everyone else at risk.
- We can circumvent a lot of attacks and headaches by simply adopting a *passwordless* policy.
- If you don't want to use external services for auth, I recommend you create your own library/repo and maintain accordingly so it's re-usable for different projects. This will help cut down on technical debt and repetition. It's a good practice in general.  



## OAUTH2
- Using OAUTH2 is a great way to get started!
- Companies like *Apple*, *Google*.. have already invested lots of money into security. Let them handle the login/registration process and use the return token to retrieve the users email address.
 - _//Todo: Add code examples for oauth2_


## I Need A Username Field / I Already Have One
- Still need to display a username field/already have those fields? - Good news!
- You can transition your users from password to *passwordless* by generating and sending a simple numeric or complex alpha-numeric code and asking the user to verify it.
- You may ask or argue that the user is not going to login to their email every time and thats a fair assumption. 
- We can simplify this daunting task by allowing users to login/register with a *Phone Number*.  
- Why Phone Numbers? Safari, iOS and Android allow you to seamlessly paste the security code without having to navigate away. 
- Twilio/SendGrid combination is perfect. If you're dead set on writing the logic yourself, please be careful (not recommended).
- Phone Numbers allow you to get *personal* with your users and if you use this feature correctly you can increase traffic. 
- ‼️ Please don't send useless notifications via SMS/Call. You will get blocked! *It's <b>very</b> important we don't annoy our users because we want them to respond quickly when security issues or very important notifications need to be actioned*.


## 2FA
- 2FA is very important and a good way to increase security. 
- *Time-Based One-Time Password* are a great way to get started by allowing users to use password managers / authenticator apps.
- We can can also re-use our SendGrid/Twilio implementation. Just make sure to use a different address than the primary login.
- The ability to allow users to change/update or add multiple 2FA methods. - It happens, people lose access to primary devices.


## reCaptcha 
- Throwing an invisible reCaptcha box will not hurt to increase security. 
- Again we don't want to annoy our users with this feature. 
- Recommended for Registration/Login.


## Application Validation
- If you don't expect anyone else to connect to your backend services, we can add a layer of security here by only allowing the backend to communicate with *authorized* apps only and blocking everything else right off the bat. There are several ways to handle this.
- _//Todo: Add code examples for app validation


## Device/IP Validation
- We can block out a lot of attacks/unwanted visitors by using services like IP Data Co, IPify to validate the users inital request to our service and monitoring it throughout the session.
- You can make up your own rules easily and stop users on certain devices, from certain regions and check for VPN status as well as threat level.


## Rate Limiting
- Rate limiting helps us stop DDoS attacks or robots trying to scrape data.
- Combining Rate Limiting and Device/IP Validation, we can identify, flag and block a bad actor right away.


## Resetting Tokens Periodically
- Tokens are how users can identify themselves with your backend services. You can pair tokens with reCaptcha, Device/IP Validation, App Validation and Rate Limiting to make it even harder for bad actors to attack backend services. 
- To increase the difficulty we can reset the token and re-validate as often as every 5 mins. Make sure this process is seamless, and only re-prompt validation if you really need to. 
- No one wants to re-enter a password every 5 mins but we need to make sure we're covering all of our bases. We can combine all the methods above to come up with an accurate prediction.


## Third Party Firewall and Services
- Third party services like CloudFlare and Heroku Add-ons are great!
- They allow you to seamlessly add more layers and they will handle most of the heavy lifting for you. 
- Not everyone can afford to go down this route but if you can afford it, I highly recommend it!


## Encrypt LocalStorage
- I've seen too many sites with raw data just sitting there for the taking.
- This data is accessible from other windows and vulnerable to XSS attacks. 
- Encrypt using AES (in production). 
- Don't store sensitive data here even if encrypted.


## AWS Security Groups
- If you're using Amazon Web Services, make sure to limit production access by using security groups.
- AWS can only do so much to protect you and it's up to you at the end of the day to setup these rules.

## Other Notes
- If not already obvious, enable 2FA on all your dev services.
- The simplest breaches start by employees/devs being careless.
- An employee luncheon/training every so often wouldn't hurt to keep everyone up to date.
