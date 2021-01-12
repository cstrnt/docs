# The Fig App Store

The Fig App Store lets users browse and download apps built specifically for the Fig platform. All apps on the App Store are open source.

Installing an app will add it to your [Sidebar](https://docs.withfig.com/get-started/fig-home/the-sidebar) and also make it accessible through the [Fig CLI](https://docs.withfig.com/the-fig-cli).

To open an app you have installed, simply run `fig app_identifier` where the app_identifier is the unique name of the appear. This appears under the app name under my apps. Some examples:

- `fig curl`
- `fig dir`
- `fig psql`
- `fig google hello world`

The current Fig App Store is very simple but is getting revamped by early August as described below.

![img](../assets/Future Of Fig/fig-app-store/appStore.png)

# **Next Version of the App Store**

*(The next version of the* ***Fig App Store\*** *will be available by the end of July / early August)*

Clicking an app will feature a popup window that contains:

- A longer description
- Documentation 
  - Including subcommands and examples
- Screenshots and demos
- Version history
- Author information
- Links to open source repo
- Permission (below)
- App installation and usage analytics

## **Permissions**

Security and Privacy is something Fig takes seriously. Before apps are listed on the App Store, they are vetted by Fig. You can read more about the vetting process on the [Security & Privacy page](https://docs.withfig.com/other/privacy-and-security).

Before installing an App, a user must agree to the permissions each app is requesting. These permissions will be available on each App's page and are alerted again before you install an app. If you do not agree to the permissions, do not install or open the app. If you are unsure, all apps on the Fig Apps are open source meaning you can verify the code yourself.

### ***\*Examples of permissions include:\****

- Access to HTTP requests
- Read from the filesystem
- Write to the file system
- Execute shell commands in the background
- Insert commands in your terminal
- Run commands in your terminal
- Run potentially dangerous commands (such as `rm`)