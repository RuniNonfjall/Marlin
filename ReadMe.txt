Firmeware update at 14/04-2022
Tevo Tornado, ramps/pin_MKS_GEN_L.h

Printer name: Stakkalin

Marlin 2.0.9.3
-25 dec. 2021


Mega2560 Build

This is an atempt to reset all the changes and errors, that might have occured, 
after multible attempts to install a faulty BL_Touch. So we Flash a fresh firmware to fix bug.

Printer has 1 MK8 extruder, an all metal Switz hotend, 100kOhm thermistor (nr.1)
No fillament runout sensor and no BL_Touch

Changes:
Name "Stakkalin"

BootScreen can go Fuck It Self (You take to much of my time)

Enabled!
/**
 * Hotend Idle Timeout
 * Prevent filament in the nozzle from charring and causing a critical jam.
 */
#define HOTEND_IDLE_TIMEOUT
#if ENABLED(HOTEND_IDLE_TIMEOUT)
  #define HOTEND_IDLE_TIMEOUT_SEC (5*60)    // (seconds) Time without extruder movement to trigger protection
  #define HOTEND_IDLE_MIN_TRIGGER   180     // (°C) Minimum temperature to enable hotend protection
  #define HOTEND_IDLE_NOZZLE_TARGET   0     // (°C) Safe temperature for the nozzle after timeout
  #define HOTEND_IDLE_BED_TARGET      0     // (°C) Safe temperature for the bed after timeout
#endif


Switched port TH1 to TH2. The TH1 port is Shorted/Dead/Broken.

//Marlin>src>pins>Ipc1769>pins_FLY_CDY.h

//
// Temperature Sensors
//
#define TEMP_0_PIN                      P0_26_A3  // (T4)
#define TEMP_1_PIN                      P0_25_A2  // (T3)
#define TEMP_2_PIN                      P0_24_A1  // (T2)
#define TEMP_BED_PIN                    P0_23_A0  // (T1)

The extruder is an bowden MK8, so new steps pr. mm is 95
/**
 * Default Axis Steps Per Unit (steps/mm)
 * Override with M92
 *                                      X, Y, Z [, I [, J [, K]]], E0 [, E1[, E2...]]
 */
#define DEFAULT_AXIS_STEPS_PER_UNIT   { 80, 80, 400, 400 }
So new steps pr. mm
#define DEFAULT_AXIS_STEPS_PER_UNIT   { 80, 80, 402, 95 }


Bed max temperature 80 degc. 
The Glue is not buildt for such heat
Was set to 150 degc, way to hot.

#define BED_MAXTEMP      80


Consider to enable classic jerk
/**
 * Default Jerk limits (mm/s)
 * Override with M205 X Y Z E
 *
 * "Jerk" specifies the minimum speed change that requires acceleration.
 * When changing speed and direction, if the difference is less than the
 * value set here, it may happen instantaneously.
 */
//#define CLASSIC_JERK
#if ENABLED(CLASSIC_JERK)
  #define DEFAULT_XJERK  8.0
  #define DEFAULT_YJERK  8.0
  #define DEFAULT_ZJERK  0.4
  //#define DEFAULT_IJERK  0.3
  //#define DEFAULT_JJERK  0.3
  //#define DEFAULT_KJERK  0.3