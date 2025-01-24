# Convert Hex to floating point

## Low level ผ่าน pointer
``` c
#include <stdio.h>

int main() {
    unsigned int hexValue = 0x4278; // ค่าเลขฐานสิบหก
    float floatValue = *(float*)&hexValue; // แปลงเป็น float

    printf("ค่าเลขฐานสิบหก: 0x%X\n", hexValue);
    printf("ค่า floating point: %f\n", floatValue);

    return 0;
}
```

## Using union
``` c
#include <stdio.h>

typedef union {
        unsigned int hexValue;
        float floatValue;
} HexFloatUnion;

int main() {
        HexFloatUnion hexFloat;
        hexFloat.hexValue = 0x4278; // ค่าเลขฐานสิบหก

        printf("ค่าเลขฐานสิบหก: 0x%X\n", hexFloat.hexValue);
        printf("ค่า floating point: %f\n", hexFloat.floatValue);

        return 0;
}
```

## High level ไม่ผ่าน pointer
``` c
#include <stdio.h>
#include <stdint.h>
#include <string.h>

float hexToFloat(uint32_t hexValue) {
        float floatValue;
        memcpy(&floatValue, &hexValue, sizeof(float));
        return floatValue;
}

int main() {
        uint32_t hexValue = 0x4278; // ค่าเลขฐานสิบหก
        float floatValue = hexToFloat(hexValue); // แปลงเป็น float

        printf("ค่าเลขฐานสิบหก: 0x%X\n", hexValue);
        printf("ค่า floating point: %f\n", floatValue);

        return 0;
}
```

## High level ไม่ผ่าน pointer
อัลกอริทึม
1. รับค่าเลขฐานสิบหกที่ต้องการแปลง
2. สร้างตัวแปร float เพื่อเก็บผลลัพธ์
3. ใช้ฟังก์ชัน memcpy เพื่อคัดลอกข้อมูลจากตัวแปรเลขฐานสิบหกไปยังตัวแปร float
4. ส่งคืนค่าผลลัพธ์ที่แปลงแล้ว
5. แสดงผลลัพธ์