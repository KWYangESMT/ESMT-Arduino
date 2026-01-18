# ESMT ER813x Family Arduino Porting

This SDK provides board packages for Arduino platform. Currently only Arduino v2.x
is tested. Please make sure update your Arduino IDE to v2.x or higher version.

## Installation
  1. Add additional boards manager URLs
     
    1.1 Select Peferences from File pull-down menu.
    1.2 Select Settings pane on Preferences window.
    1.3 Copy the following URL and paste on to the editbox of Addtional boards manager URLs
        https://github.com/KWYangESMT/ESMT-Arduino/raw/refs/heads/main/er8130tc01_evk/package_esmt_index.json
    1.4 Press OK button on Preferences window.
    
  2. Install board package

    2.1 Open BOARD MANAGER from the side bar of Arduino IDE window.
    2.2 Type "esmt" in the search box of BOARD MANAGER. ESMT ER813x Boards should be dispaly in the board list
    2.3 Press INSTALL

  3. Notifications
     
     For the first time installation, a GNU ARM toolchain would be downloaded from 
     
