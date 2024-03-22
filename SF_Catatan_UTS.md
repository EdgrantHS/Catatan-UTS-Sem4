# **Sistem Siber Fisik**
Link Emas: `https://emas2.ui.ac.id/course/view.php?id=60011`

# Week 1 (Perkenalan dan pengantar)
## Kontak: F. Astha Ekadiyanto
- astha.ekadiyanto@uilac.id
- 082113554956
- Ruangan di CIL Pusgiwa lantai 3  
## Others
- Menggunakan AVR microcontroler  
- Disarankan baca buku Muhammad Ali Mazidi, Sarmad Naimi &Sepehr Naimi, The AVR Microcontroller and Embedded Systems: Using Assembly and C, Pearson New International Edition, Pearson, Essex, 2015
- Lee & Seshia, "Introduction to Embedded Systems - A Cyber- Physical Systems Approach", 2nd edition, UC- Berkeley, 2015 https://ptolemy.berkeley.edu/books/leeseshia/releases/LeeSeshia_DigitalV2_2.pdf
- ATMEL AVR Instruction Set Manual, https://ww1.microchip.com/downloads/en/devicedoc/atmel-0856-avr-instruction-set-manual.pdf
- AVR Simulator IDE
- `AVR Microchip Studio 5.1.208` or `Atmel Studio 6/7`
## Komposisi Penilian
- Praktikum - 20%
- Tugas/Quiz - 10%
- UTS/Proposal - 30%
- Final Project - 40%
- Attendence minimal 75% - syarat mengikuti ujian akhir

# Week 2 (Introduction to computing)
- prosesor ambil memory dalam word (multiple bit) kalau mau bit khusus harus masking
## RAM & ROM
Here's a quick definition of each term: `Hasil GPT`
- **ROM (Read-Only Memory):** A type of non-volatile storage that is typically used to store firmware or application software in plug-in cartridges.
- **Mask ROM:** A type of ROM in which the data is written during the manufacturing process and cannot be reprogrammed by the user.
- **PROM (Programmable ROM):** A form of ROM that the user can program once. Once programmed, the data on it cannot be changed and remains permanent.
- **EPROM (Erasable Programmable ROM):** A type of ROM that can be erased by exposing it to strong ultraviolet light and then reprogrammed.
- **EEPROM (Electrically Erasable Programmable ROM):** A type of ROM that can be electrically erased and reprogrammed multiple times.
- **Flash EPROM:** A type of EEPROM that allows for blocks of memory to be erased and reprogrammed in a single action or "flash."
- **RAM (Random Access Memory):** A type of computer memory that can be accessed randomly, meaning any byte of memory can be accessed without touching the preceding bytes. RAM is volatile, meaning it requires power to maintain the stored information.
- **SRAM (Static RAM):** A type of RAM that uses bistable latching circuitry to store each bit. It is faster and more reliable than DRAM but is more expensive. It does not need to be periodically refreshed. Isinya FF
- **DRAM (Dynamic RAM):** A type of RAM that stores each bit of data in a separate capacitor. It is more dense and less expensive than SRAM but requires periodic refreshing to maintain the data. Isinya kapasitor
- **NV-RAM (Non-Volatile RAM):** A type of RAM that retains data without requiring power, combining the speed of RAM with the permanence of ROM.
## Hyperthreading
- 1 cpu thread menjalankan 2 thread secara bersamaan menggunakan cache
## Von Neumann Architecture vs Harvard Architecture
- von Neumann: instruksi dan data di memory sama, memory dan data memory di memory sama. jadi busnya satu
- Harvard: instruksi dan data memory di memory berbeda. Faster, can be 1 cycle

# Week 3
- sector yang sering menggunakan semikonduktor : industri otomotif
## Microcontroller vs Microprosesor
- **Microprosesor**: isinya prosesor saja, ram rom io itu dihubungin external
    - Keterbatasannya adalah pinnya/interfacenya
- **Microcontroler**: Udah lengkap isinya udah ada ram, rom, serial port, timer, IO
    - Everything in one chip
## Others
- **System On Chip**: seakrang zamannya bbukan microcontroller, dah jadi SOC (Multirate system, clocknya gak sinkron)
- the future of chips adalah energy eficiency, cuman dinyalain saat dibutuhkan
- H flag, carry dari lower byte ke higher byte
## Tipe microcontroller
- 8 bit
    - AVR
    - PIC
    - HCS12
    - 8051
- 32 bit
    - ARM
    - PIC32
## AVR Internal Architecture
- Program bus dan memory bus dipisah
- Instruksi dan data dipisah di memory dan di bus juga terpisah
- Tidak ada bus, setiap output pin fungsinya khusus
- Tapi pinnya biasanya multifunction, untuk fungsi khusus dan untuk io parallel
- pin yang tidak dishare cuman yg gak bisa
    - vcc, gnd, clock(xtal1, xtal2), reset, analog-digital converter
## AVR Part Number
## AVR CPU
- RISC architecture
- Harvard architecture
- Component
    - ALU
    - 32 regs
    - PC reg
    - Instruction Decoder & IR
    - Flags
- Hanya 16 dari 32 register yang bisa di LDI, R16 akan load ke R0. R16-31 untuk load from input
## AVR Data Adress Space
- ada tablenya
- 0-1F: general purpose reg
- 20-5f: I/O regs
- 50-FFFF: general purpose ram

# Week 4
## Jump and Call
- compaer (a < b) pakai carry flag sub
- v: overflow flag, register gak bisa hold hasil data alu
- c: bit setelah msb 1
    - kalau dalam sub sama, tapi mungkin mul beda
## Stack
- sp, stack pointer, lokasi memori stack kosong
- untuk akses data, butuh tambah dulu
- untuk call dan ret, pakai stack pointer
- kalau ada pop, push, bisa manipulasi return address
## Time delay
- branch penalty = 2 cycle, 1 cycle saat comparenya false

# Week (IO)

