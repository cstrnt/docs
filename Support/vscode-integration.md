# VSCode Integration

Fig works in the VSCode integrated terminal, if the following settings are updated:

1. Set `terminal.integrated.inheritEnv` to `false`

2. Set `editor.accessibilitySupport` to `"off"` (or `"on"` if applicable)
	Fig will still work if the `editor.accessibilitySupport` field is not set, but VSCode will prompt you to make a choice because it detects that an app is using the Accessibility API.


Fig also installs a VSCode extension in order to get notified when the active terminal changes. *You may need to restart VSCode after you install Fig in order for the extension to start running.*

### Could not install VSCode integration automatically

![VSCode Integration Error](/docAssets/support/guide/vscode-integration-error.png)

If you ran into this error, please update your VSCode settings manually.

You can do this by opening VSCode and pressing `Command` `,` to quickly open the settings page. Then update the **Accessibility Support** and **Inherit Env** preferences.


If you feel comfortable sharing your VSCode settings file, please run `fig report $(echo "VSCode Settings: " && cat ~/Library/Application\ Support/Code/User/settings.json )` to help us debug.  