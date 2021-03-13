# Fig icon is bouncing

You need to enable accessibility permissions. See below.

## How do I enable Accessibility Permissions

Fig Menu (◧) → Settings → Developer → Request Accessibility Permission

(This should take you to System Preferences → Security & Privacy → Accessibility)

- Click the lock icon to unlock (you will be prompted for your password)
- If Fig is unchecked, check it. If Fig is checked, toggle it off and then check it again.

## I am getting this error in my shell when running a Fig command or going to a new line

```bash
› Could not connect to fig.app.

  QUICK FIX
  Check if Fig is active. (You should see the ◧ Fig icon in your menu bar).

→ If not, run open -b com.mschrage.fig to relaunch the app.

  Please email hello@withfig.com if this problem persists.
```

1. Check if the Fig app is open (the ◧ Fig icon should be in your menu bar)

If it's open:
- Restart Fig ( ◧ → Restart)
- Potentially kill Fig from Activity Monitor
- See the section on "Quitting Fig" for more details.

If it's closed:
- Open Fig