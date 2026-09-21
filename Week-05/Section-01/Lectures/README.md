[baremetal_ads1115.txt](https://github.com/user-attachments/files/32471783/baremetal_ads1115.txt)## Below is the Lecture which we covered in the Section-01.


## Embedded Systems & Microcontroller Fundamentals
Hardware & software architecture, datasheet study, and hands-on register access — taught on the STRIVE-Iα SoC (SweRV EH1, RV32IMAC)

[Embedded_Systems_MCU_Fundamentals.pdf](https://github.com/user-attachments/files/32471670/Embedded_Systems_MCU_Fundamentals.pdf)

======================================================

## C & Embedded C Fundamental

[Workshop_Theory (1).pptx](https://github.com/user-attachments/files/32471673/Workshop_Theory.1.pptx)

======================================================

## Baremetal_ads1115
 * ONE I2C transfer to ADS1115 @ 0x48 — no Wire library.
 * Talks to the AVR TWI hardware registers directly (Mega 2560 / Uno).

## Code:

 * baremetal_ads1115.ino
 * ---------------------
 * ONE I2C transfer to ADS1115 @ 0x48 — no Wire library.
 * Talks to the AVR TWI hardware registers directly (Mega 2560 / Uno).
 *
 * Wiring (Mega 2560):  SDA=20  SCL=21  ADDR=GND  VDD=5V  GND=GND
 * Wiring (Uno):        SDA=A4  SCL=A5  (same sketch)
 *
 * What students should see on Serial (9600):
 *   START ok
 *   ADDR ACK
 *   DATA ACK (x3)
 *   STOP
 *   DONE — one transfer complete
 *
 * Mapping to Wire:
 *   Wire.begin()                     -> twi_init()
 *   beginTransmission + write + end  -> START, addr, bytes, STOP
 */

#include <avr/io.h>
#include <util/delay.h>

#define ADS1115_ADDR  0x48

/* ---- TWI (I2C) status codes from ATmega datasheet ---- */
#define TW_START        0x08
#define TW_MT_SLA_ACK   0x18
#define TW_MT_DATA_ACK  0x28

static uint8_t twi_status(void) {
  return TWSR & 0xF8;
}

static void twi_wait(void) {
  while (!(TWCR & (1 << TWINT))) { }
}

/* Wire.begin() */
static void twi_init(void) {
  /* 16 MHz / (16 + 2*TWBR) = 100 kHz  =>  TWBR = 72, prescaler = 1 */
  TWSR = 0;          /* prescaler 1 */
  TWBR = 72;
  TWCR = (1 << TWEN); /* enable TWI hardware */
}

static uint8_t twi_start(void) {
  TWCR = (1 << TWINT) | (1 << TWSTA) | (1 << TWEN);
  twi_wait();
  return twi_status();
}

static uint8_t twi_write(uint8_t data) {
  TWDR = data;
  TWCR = (1 << TWINT) | (1 << TWEN);
  twi_wait();
  return twi_status();
}

static void twi_stop(void) {
  TWCR = (1 << TWINT) | (1 << TWSTO) | (1 << TWEN);
  while (TWCR & (1 << TWSTO)) { }  /* wait until STOP finishes */
}

/*
 * ONE transfer = one START ... STOP on the bus:
 *   START
 *   addr 0x48 + W          (wire byte 0x90)
 *   0x01  config pointer
 *   0xC3  config MSB
 *   0x83  config LSB
 *   STOP
 */
static void one_transfer(void) {
  uint8_t st;

  Serial.println(F("--- one bare-metal I2C transfer ---"));

  st = twi_start();
  Serial.print(F("START status=0x"));
  Serial.println(st, HEX);
  if (st != TW_START) {
    Serial.println(F("FAIL: START"));
    return;
  }

  /* (0x48 << 1) | 0 = 0x90 */
  st = twi_write((ADS1115_ADDR << 1) | 0);
  Serial.print(F("ADDR+W status=0x"));
  Serial.println(st, HEX);
  if (st != TW_MT_SLA_ACK) {
    Serial.println(F("FAIL: no ACK from 0x48 (check SDA/SCL/ADDR)"));
    twi_stop();
    return;
  }

  st = twi_write(0x01);   /* config register pointer */
  Serial.print(F("DATA 0x01 status=0x"));
  Serial.println(st, HEX);
  if (st != TW_MT_DATA_ACK) { twi_stop(); return; }

  st = twi_write(0xC3);   /* config MSB */
  Serial.print(F("DATA 0xC3 status=0x"));
  Serial.println(st, HEX);
  if (st != TW_MT_DATA_ACK) { twi_stop(); return; }

  st = twi_write(0x83);   /* config LSB */
  Serial.print(F("DATA 0x83 status=0x"));
  Serial.println(st, HEX);
  if (st != TW_MT_DATA_ACK) { twi_stop(); return; }

  twi_stop();
  Serial.println(F("STOP"));
  Serial.println(F("DONE — one transfer complete"));
}

void setup() {
  Serial.begin(9600);
  while (!Serial) { }

  Serial.println(F("Bare-metal TWI (no Wire lib)"));
  Serial.println(F("Mega: SDA=20 SCL=21 | Uno: SDA=A4 SCL=A5"));

  twi_init();
  one_transfer();   /* run once */
}

void loop() {
  /* empty — single transfer already done in setup() */
}

======================================================

