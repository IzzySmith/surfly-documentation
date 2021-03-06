![logo](../images/logosmall.png)

# Button_appearance_options

### Support button appearance

|  Option | Default | Description |
| ---------------| ------------|------------|
| auto_start | false | Instead of showing a button, immediately start a session |
| autohide_button | true | Hide the Surfly button when no agent is available |
| block_until_agent_joins | true | In case of Surfly button, block the screen until a follower joins |
| end_of_session_popup_url | false | If this parameter is set, after session end the user will see a popup window with the contents from the specified URL |
| hidden | false | Do not show the button |
| position | 'bottomleft' | Positions the Surfly Support Button. The options are: 'bottomleft', 'bottomright', 'middleright' |
| QUEUE_METADATA_CALLBACK | false |  A JS callback that can provide optional metadata (see queue customization section below) |
| QUEUE_ENDPOINT | false | Custom queue endpoint (see queue customization section below) |
| QUEUE_HANDLER | false | Custom JS queue handler (see queue customization section below) |
| QUEUE_CALLBACK | false | JS callback for queue monitoring (see queue customization section below) |
| stealth_mode | true | When enabled, users can use CTRL + ENTER to start a Surfly session |
| theme_font_background | surfly-red | The support button background color |
| theme_font_color | white | The support button foreground color|
| theme_font_size | 14 | The size of the text in the button |
