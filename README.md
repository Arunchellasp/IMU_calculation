# Inclination Calculation from Accelerometer and Gyroscope Data

## Overview

This project demonstrates how to calculate the **inclination** (specifically **pitch** and **roll**) using raw **accelerometer** and **gyroscope** data. The accelerometer data is provided in **g** (gravitational force), and gyroscope data in **dps** (degrees per second).

The inclination is calculated using only the **accelerometer** data for simplicity. For more accurate orientation, sensor fusion (e.g., Kalman or complementary filters) combining accelerometer and gyroscope is typically used.

---

## Input Data Format

| Delta time (ms) | Board Temp. (°C) | AX (g) | AY (g) | AZ (g) | GX (dps) | GY (dps) | GZ (dps) |
|-----------------|------------------|--------|--------|--------|----------|----------|----------|
| 99              | 42.164           | -0.002 | -0.989 | -0.106 | -1.129   | -1.129   | 0.305    |
| 99              | 42.164           | -0.002 | -0.990 | -0.106 | -1.129   | -1.099   | 0.305    |

---

## Inclination Calculation

We calculate **roll** and **pitch** using the following formulas (based on static accelerometer data):

### Formulas

- **Roll** (rotation around the X-axis):

 <img width="289" alt="image" src="https://github.com/user-attachments/assets/5b108c20-4cf6-486b-87e4-7674ba6ce445" />


- **Pitch** (rotation around the Y-axis):

<img width="361" alt="image" src="https://github.com/user-attachments/assets/10a9689f-a28e-4be1-bbf0-bbcf49f7f102" />

---

## Example Calculation (using first row)

Given:
- AX = -0.002 g
- AY = -0.989 g
- AZ = -0.106 g

### Step-by-step:

#### Roll:

<img width="338" alt="image" src="https://github.com/user-attachments/assets/be87ee5a-0e13-4083-a6bf-165ef7c73264" />


#### Pitch:

<img width="568" alt="image" src="https://github.com/user-attachments/assets/ec92a6cf-b792-4e4d-9f27-1950346e718c" />

---

## Notes

- This calculation assumes that the device is stationary.
- Gyroscope data can be used for dynamic orientation tracking using sensor fusion algorithms.
- Make sure to filter accelerometer data to remove high-frequency noise before using it.

## Excel Formulas (using first row)

### **Mathematical Formulas**

- **Roll (°)** = `atan2(AY, AZ) × 180/π`
- **Pitch (°)** = `atan2(-AX, sqrt(AY² + AZ²)) × 180/π`

---

Assuming your Excel sheet has these columns starting from row 2:

- AX in cell `C2`
- AY in cell `D2`
- AZ in cell `E2`

Then use:

- **Roll (°):**
  ```excel
  =ATAN2(D2, E2) * 180 / PI()
  ```
  Alternate In Excel (assuming AX in cell D2, AY in E2, AZ in F2):
  ```excel
  =DEGREES(ATAN2(D2, SQRT(E2^2 + F2^2)))
  ```

- **Pitch (°):**
   ```excel
    =ATAN2(-C2, SQRT(D2^2 + E2^2)) * 180 / PI()
  ```
    Alternate In Excel (assuming AX in cell D2, AY in E2, AZ in F2):
     ```excel
     =DEGREES(ATAN2(E2, SQRT(D2^2 + F2^2)))
  ```
