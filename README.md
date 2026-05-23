# Implementasi Mikrokontroler Motor Servo dan Integrated Inter-Circuit (I2C)

## 📌 Deskripsi Proyek
Proyek ini merupakan implementasi sistem kendali motor servo berbasis **ESP32** dengan memanfaatkan **potensiometer** sebagai input analog dan **LCD I2C 16x2** sebagai media monitoring sudut servo secara real-time.  

Nilai analog dari potensiometer dibaca oleh ADC pada ESP32, kemudian dikonversi menjadi sinyal PWM untuk mengatur posisi motor servo. Sistem ini dirancang untuk memahami konsep dasar **embedded system**, komunikasi **I2C**, pengendalian aktuator, serta integrasi perangkat keras menggunakan mikrokontroler ESP32.

---

## 🖼️ Dokumentasi Sistem

<img width="280" height="214" alt="image" src="https://github.com/user-attachments/assets/35018a83-154e-4482-ab62-69fb8218aeae" />

<img width="258" height="251" alt="image" src="https://github.com/user-attachments/assets/f09c5247-f67f-411a-b1c2-fa1aa50a7e6a" />

---

## 🛠️ Alat dan Komponen
- ESP32 Dev Module  
- Motor Servo  
- Potensiometer  
- LCD 16x2 I2C  
- Breadboard  
- Kabel Jumper  
- Kabel USB Data  

---

## 🔌 Konfigurasi Pin

### Potensiometer
| Pin Potensiometer | ESP32 |
|-------------------|--------|
| Pin Tengah        | GPIO34 |
| Pin Kiri          | 3.3V   |
| Pin Kanan         | GND    |

### Motor Servo
| Pin Servo         | ESP32 |
|-------------------|--------|
| VCC (Merah)       | 5V     |
| GND (Coklat)      | GND    |
| Signal (Oranye)   | GPIO18 |

### LCD I2C
| Pin LCD | ESP32 |
|----------|--------|
| VCC      | 5V     |
| GND      | GND    |
| SDA      | GPIO21 |
| SCL      | GPIO22 |

### Kode Arduino
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <ESP32Servo.h>

// Inisialisasi LCD dengan alamat I2C 0x27 dan ukuran 16x2
LiquidCrystal_I2C lcd(0x27, 16, 2);

// Inisialisasi servo
Servo myServo;

// Pin
const int potPin = 34;      // pin analog untuk potensiometer (GPIO34 ADC)
const int servoPin = 18;    // pin untuk servo

int potValue = 0;
int angle = 0;

void setup() {
  // Setup LCD
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("Kontrol Servo");

  // Attach servo ke pin
  myServo.attach(servoPin, 500, 2400); // ESP32 perlu batas PWM (500-2400 us)

  delay(1000);
}

void loop() {

  // Baca potensiometer
  potValue = analogRead(potPin);

  // Konversi nilai (0-4095 ADC ESP32) ke derajat (0-180)
  angle = map(potValue, 0, 4095, 0, 180);

  // Gerakkan servo
  myServo.write(angle);

  // Tampilkan di LCD
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Sudut Servo:");
  
  lcd.setCursor(0, 1);
  lcd.print(angle);
  lcd.print((char)223); // simbol derajat °
  lcd.print("   ");

  delay(200);
}
---

## ⚙️ Langkah Implementasi

1. Siapkan seluruh alat dan komponen.  
2. Rangkai komponen sesuai dengan konfigurasi pin.  
3. Hubungkan ESP32 ke laptop menggunakan kabel USB data.  
4. Buka **Arduino IDE**.  
5. Install library berikut melalui menu:  
   `Tools → Manage Libraries`
   - `ESP32Servo`
   - `LiquidCrystal I2C` by Frank de Brabander  

6. Pilih board ESP32:
   `Tools → Board → ESP32 Arduino → ESP32 Dev Module`

7. Pilih port ESP32:
   `Tools → Port → COM ESP32`

8. Upload program ke ESP32 dan jalankan sistem.  

---

## 📊 Hasil Percobaan
Berdasarkan hasil percobaan, integrasi ESP32, potensiometer, LCD, dan motor servo berhasil menerapkan sistem kendali sederhana secara efektif. Potensiometer digunakan sebagai input sudut servo yang diproses oleh ESP32 melalui ADC dan dikonversi menjadi sinyal PWM. Sistem mampu merespons perubahan input dengan baik, sementara LCD menampilkan informasi sudut servo secara real-time.

Proyek ini membantu memahami dasar mikrokontroler, sensor, aktuator, dan komunikasi antarkomponen pada embedded system sebagai dasar pengembangan sistem IoT dan otomasi yang lebih kompleks.

---

## 💻 Teknologi yang Digunakan
- Arduino IDE  
- ESP32  
- PWM (Pulse Width Modulation)  
- ADC (Analog to Digital Converter)  
- I2C Communication Protocol  

---

## 📚 Tujuan Pembelajaran
- Memahami penggunaan ADC pada ESP32  
- Mengendalikan motor servo menggunakan PWM  
- Mengimplementasikan komunikasi I2C pada LCD  
- Mengintegrasikan sensor, aktuator, dan display dalam satu sistem embedded  

---

## 👨‍💻 Author
**Puspita**  
Computer Engineering Student — IPB University
