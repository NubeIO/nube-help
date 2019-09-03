
### dipSwitches Settings

- 1-3 are for interval timing - 0-7 binary:
    - 0 = 15min     //000
    - 1 = 30sec     //100
    - 2 = 1min      //010
    - 3 = 3min      //110
    - 4 = 5min      //001
    - 5 = 10min     //101
    - 6 = 30min     //011
    - 7 = 1hr       //111
- 4 Interrupt for PIR : true to attach Interrupt
- 5 Serial Print : will print the payload msg on the serial
- 6 Hard Reset : will give device new ID every time it boots
- 7-8 are Testing Mode - 0-3 binary:
    - 0 = normal mode ID set randomly from first boot or from hard_reset
    - 1 = ID : AAB2AAAA - 6Sec Intervals    //10
    - 2 = ID : BBB2BBBB - 6Sec Intervals    //01
    - 3 = ID : CCB2CCCC - 6Sec Intervals    //11
