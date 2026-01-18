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
    
    3.1 For the first time installation, a GNU ARM toolchain would be downloaded from official website. If network
        connection timeout occurred while downloading, please follow the instructions to extend timeout limit.
      
      3.1.1 Close Arduino IDE and find the file arduino-cli.yaml in C:\Users\user_name\.arduinoIDE
      3.1.2 Open arduino-cli.yaml in a text editor
      3.1.3 Add the configuration into the file
            network:
                connection_timeout: 1800s
      3.1.4 Open Arduino IDE and install package again.
      
    3.2 To support UART downloading in Arduino IDE, a bootloader must be downloaded first. Bootloader can be downloaded from:
      https://github.com/KWYangESMT/ESMT-Arduino/blob/main/er8130tc01_evk/ArduinoLoader.bin
    
## Supported Examples
  Currently only Examples\01.Basics\Blink is supported.