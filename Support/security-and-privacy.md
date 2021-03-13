# **Security**

We understand that connecting web apps to your local development environment is powerful and therefore a potential concern. Here are the steps Fig takes to ensure your and your company's data is secure:

**All Fig Apps:**

- are open source
- are hosted by Fig on Fig's server
- are vetted by Fig before being updated and/or added to the Fig App Store
- must accurately display the permissions it requests
  - As the user, you choose to **opt in** to these permissions
  - The permissions are explained more in the [Fig App Store page](notion://www.notion.so/get-started/the-fig-app-store)

### Fig Vetting / Security Review

Before being listed on the Fig App Store, apps undergo a security check by Fig. An app is usually approved provided it accurately requests the right permissions.

An app is rejected if:

- It does not request all necessary permissions for Fig APIs and other actions like HTTP requests which are listed in the Fig App Store.
- It contains any known malware or spam
- It has the potential to send any sensitive data to the cloud without a proper login process or a more explicit user opt-in that is more than what is listed on the App Store
- It is not open source or willing for Fig to open source its code while it is listed on the App Store
- it has no documentation

**Fig web**

`fig web` acts purely as a browser. Fig does inject the Fig.js runtime into websites previewed using Fig Web. This means websites cannot run shell commands locally in your environment.

There are two exceptions where `fig web` is given access to the fig runtime:

1. `http://localhost` is allowed access for local testing purposes
2. Private sites that have been white labelled for you / your organization.
   - This is possible in Fig's enterprise plan. Learn more at [Fig for Teams](notion://www.notion.so/other/fig-for-teams)

# Privacy and Your Data

Fig does not send sensitive data to the cloud. Your and your companies data is processed locally your device.

Fig apps are developed by Fig and other 3rd party developers. All Fig apps undergo a security review before being added and updated. Fig apps are hosted on fig's servers

Each Fig App has its own set of permissions surrounding its use. which you choose to opt into before downloading.

## **Critical Telemetry**

Fig anonymously tracks the usage of its cli by sending a ping to [withfig.com](http://withfig.com). This helps our product and customer teams. The ping includes:

- an anonymous user ID defined on installation
- current Fig version
- the domain name of your email (e.g. [withfig.com](http://withfig.com) for [brendan@withfig.com](mailto:brendan@withfig.com))
- a redacted version of your cli request after the main command (e.g. `fig run xxxx.xxxx` for `fig run index.html`)

This ping is NOT tied to your email address or any other personally identifiable information. This cannot be disabled.

## **Other Telemetry**

Fig also tracks usage statistics such as page views, sidebar interactions. These are sent to [withfig.com](http://withfig.com). This information is linked to your email address. You can disable it entirely at any time.

For our complete privacy policy, see https://withfig.com/privacy/