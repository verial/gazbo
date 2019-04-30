*?* - show options

*A n m l* -set buzzer (freq, patt, len_ms)

*B* -toggle sensor Board control

*E* - dEbug 'E'-disable all, EC-enable consoleLog, ES enable Scope\r\n"\

*P* - power control - P -disablepoweroff, PE enable poweroff, Pn power off in n seconds

*I* -enable Immediate commands:
  
  *W/S/A/D/X* -Faster/Slower/Lefter/Righter/DisableDrive
  
  *H/C/G/Q* -read Hall posn,speed/read Currents/read GPIOs/Quit immediate mode
  
  *N/O/R* - read seNsor data/toggle cOntrol/dangeR
  
*T* -send a machine test message A-ack N-nack T-test

*?* -show this

See Ascii Protocol page in [hbprotocol repo wiki](https://github.com/bipropellant/hbprotocol/wiki/ASCII-Protocol) for a more detailed explanation