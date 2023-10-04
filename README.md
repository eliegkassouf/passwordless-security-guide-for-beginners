# Elie's Guide to Passwordless Security for Beginners

## Introduction

- **Purpose**: 
  - With the increasing number of subpar security implementations and careless data handling, there is an urgent need to spread awareness and provide guidance on effective security measures.
  - Ensuring data security is a paramount concern today. It is vital that everyone feels secure and understands the significance of strong security measures.

- **Note**: In the near future, I plan to incorporate code examples for better clarity.

- **A Word of Caution**: While utilizing third-party services for authentication might seem straightforward, if you're inclined to manage it yourself, remember that storing passwords in plain text or even in base64 is a grave mistake. Utilizing SHA-256 is decent, but [bcrypt is preferred](https://security.stackexchange.com/questions/4781/do-any-security-experts-recommend-bcrypt-for-password-storage). Ideally, eschew storing passwords entirely. Not only will this save you significant time and effort, but using an email or phone number for notifications also provides an immediate alert system that challenges attackers.

## Table of Contents
1. [Getting Started](#getting-started)
2. [OAUTH2](#oauth2)
3. [Handling Username Fields](#handling-username-fields)
4. [2-Factor Authentication (2FA)](#2-factor-authentication-2fa)
5. [reCaptcha](#recaptcha)
6. [Application Validation](#application-validation)
7. [Device/IP Validation](#deviceip-validation)
8. [Rate Limiting](#rate-limiting)
9. [Periodic Token Reset](#periodic-token-reset)
10. [Third-Party Firewall & Services](#third-party-firewall--services)
11. [Local Storage Encryption](#local-storage-encryption)
12. [Request Data Encryption](#request-data-encryption)
13. [AWS Security Measures](#aws-security-measures)
14. [Additional Recommendations](#additional-recommendations)

## Getting Started
- This comprehensive guide aims to aid in enhancing the security of your services.
- Consider each section as a distinct layer of security. These layers can either function independently or cohesively to establish and regulate diverse rules.
- Employing HTTPS is non-negotiable for production. It is, in fact, a requirement for most external services.
- An optimal way to safeguard your users is by omitting password storage entirely.
- Recognize that not all users will grasp the essence of robust security measures. It's thus imperative to mitigate the risks posed by potential security breaches.
- Adopting a *passwordless* approach can significantly reduce potential threats and complications.
- For those inclined to refrain from external authentication services, it is wise to craft a personalized library or repository. This reusable resource will minimize redundancy and streamline various projects.

## OAUTH2
- Embracing OAUTH2 provides a robust start to secure user authentication.
- Tech giants like Apple and Google have already allocated significant resources to ensure top-tier security. Leveraging their login and registration processes, and then using the returned token to fetch the user's email, is a prudent approach.
- **Future Additions**: Code examples showcasing OAUTH2 implementation.

✳️ Fundamental insights on OAUTH2, credits to @RottenRonnie. [See Issue](https://github.com/eliegkassouf/passwordless-security-guide-for-beginners/issues/1)

## Handling Username Fields
- Need to maintain a username field or have existing fields? There's a solution!
- Transitioning users from password-based to *passwordless* systems can be achieved by generating a verification code, either numeric or alpha-numeric, for user validation.
- Utilizing phone numbers as a means of user identification simplifies this task. Major platforms like Safari, iOS, and Android support easy pasting of security codes.
- Leveraging the Twilio/SendGrid duo is advisable. If you're keen on crafting your own logic, exercise extreme caution.
- Effective utilization of phone numbers can foster a deeper connection with users, potentially boosting engagement. However, refrain from sending frivolous SMS or call notifications. It's paramount to ensure that users respond swiftly when confronted with pressing security issues or vital alerts.

## 2-Factor Authentication (2FA)
- Implementing 2FA significantly bolsters security.
- The *Time-Based One-Time Password* system is an excellent starting point, allowing users to employ password managers or authenticator apps.
- The existing SendGrid/Twilio infrastructure can also serve this purpose. Ensure that a different address than the primary one is used for login.
- Catering to the inevitability of users losing access to primary devices, allowing flexibility in changing or adding multiple 2FA methods is advised.

## reCaptcha
- Introducing an invisible reCaptcha box is a subtle yet effective enhancement to security.
- Aim to enhance security without impinging on user experience.
- Ideal for deployment during registration and login phases.

## Application Validation
- If external access to your backend services isn't anticipated, fortify security by permitting only *authorized* applications to interact with the backend. Multiple strategies can facilitate this.
- Always deploy CORS (Cross-Origin Resource Sharing). Validating the application itself, alongside the request, can be achieved through precise coding.

## Device/IP Validation
- Services like IP Data Co and IPify allow initial user request validation and continuous session monitoring. This offers a way to preempt potential threats.
- By crafting custom rules, restricting access from specific devices or regions becomes feasible.

## Rate Limiting
- Introducing rate limiting can effectively thwart DDoS attacks and unauthorized data scraping.
- A synergistic approach, combining rate limiting with device/IP validation, can swiftly detect and deter malicious entities.

## Periodic Token Reset
- User tokens are vital credentials for backend service interactions. Enhancing token security with auxiliary measures like reCaptcha, device/IP validation, and rate limiting can deter potential threats.
- For advanced security, consider resetting and revalidating tokens periodically. However, ensure that the user experience remains fluid.

## Third-Party Firewall & Services
- Services like CloudFlare and Heroku offer extensive protection without the hassle of manual configuration.
- While this might not be feasible for everyone due to financial constraints, it's a valuable investment for those who can afford it.

## Local Storage Encryption
- Storing raw data without encryption is a glaring vulnerability.
- Always employ AES for encryption in production settings.
- Regardless of encryption, storing sensitive data in local storage is inadvisable.

## Request Data Encryption
- HTTPS should be the default communication protocol.
- In scenarios involving highly sensitive data, encrypting the request data enhances security. However, this added layer can complicate testing and debugging processes.

## AWS Security Measures
- For those utilizing Amazon Web Services, security groups are indispensable for restricting production access.
- While AWS offers robust protection, the onus is on users to configure these security measures optimally.

## Additional Recommendations
- Activate 2FA across all developer services.
- Remember, even minor oversights can lead to significant security breaches.
- Periodic employee training sessions can ensure that everyone remains updated on best security practices.
