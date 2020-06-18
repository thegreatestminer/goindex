![GoIndex](https://raw.githubusercontent.com/thegreatestminer/goindex/master/themes/logo.png)  
  
GoIndex  
---
*Cloudflare Workers + Google Drive Directory Index* | A modification of the now-defunct GoIndex project developed by [donwa](https://www.github.com/donwa).

[***Please read LICENSE.md before using this project.***](https://raw.githubusercontent.com/thegreatestminer/goindex/master/LICENSE.md)

Modifications from the original:

- 1000 byte filesize measure changed to 1024
- Column headers have been changed to English (Name, Date modified, Size)
- Removed `?a=view` feature, as it's useless for my intentions.
- *to be determined*

## How to use

1. Create a Google Drive remote using [rclone](https://rclone.org/). **YOU WILL HAVE TO CREATE YOUR OWN** `client_id` **AND** `client_secret` **VALUES. FOLLOW THIS [GUIDE](https://rclone.org/drive/#making-your-own-client-id) IF YOU DO NOT KNOW HOW TO MAKE ONE.
2. Run `rclone config file` in a terminal to determine the path for `rclone.conf`.  
3. Open `rclone.conf` and take note of `client_id`, `client_secret`, `refresh_token`, and `root_folder_id`. If you have designated a shared (team) drive instead of a folder, then **you must create a folder in the selected shared drive, and take note of that new folder's ID.**
4. Create a worker at [Cloudflare Workers](https://workers.cloudflare.com/).
5. Copy the contents of [index.js](https://raw.githubusercontent.com/thegreatestminer/goindex/master/index.js) and paste it into the "Script" section of the worker.
6. Configure `authConfig`. (example below)
7. Make sure you configured everything properly by clicking on Preview and refreshing the display.
8. Press **Save and Deploy**, and you're done!

#### Example authConfig

```
var authConfig = {
    "siteName": "GoIndex", // Website title, I recommend changing this
    "root_pass": "index",  // Leave blank for no password
    "theme" : "material",  // Available themes: material, classic
    "client_id": "",       // Create your own client_id and client_secret values and put them here.
    "client_secret": "",   // https://rclone.org/drive/#making-your-own-client-id
    "refresh_token": "",   // Take from rclone.conf remote
    "root": "root"         // Folder ID for root directory. THIS CAN NOT BE A SHARED DRIVE ID! (but it can be a folder ID inside a shared drive.)
};
```
