# 8086 Assembly Single-Digit Subtraction

A basic 8086 Assembly Language program written in MASM/TASM syntax that demonstrates how to perform arithmetic subtraction on user-inputted numbers using DOS interrupts (`INT 21H`).

## Project Overview

This program captures two separate single-digit number inputs from the user, handles formatting by adding newlines, performs a subtraction operation, and correctly adjusts the result back to ASCII format so it can be displayed as a readable number on the screen.

## How It Works & Logic

Since keyboard inputs are read as **ASCII values**, we need to convert them into actual numbers before doing arithmetic, or handle the offsets carefully. This program converts them right after input:

1. **First Input & Conversion:** Takes the first character (`AH = 1`). The ASCII value goes to `AL`. The program immediately subtracts $48$ (`SUB AL, 48`) to get the **actual numeric value** and stores it in `BL`.
   * *Example:* Input `'5'` (ASCII 53) $\rightarrow 53 - 48 = 5$. Now `BL = 5`.
2. **Second Input & Conversion:** Takes the second character, subtracts $48$ from `AL`, and stores the actual numeric value in `CL`.
   * *Example:* Input `'2'` (ASCII 50) $\rightarrow 50 - 48 = 2$. Now `CL = 2`.
3. **The Subtraction (`SUB BL, CL`):** Subtracts `CL` from `BL`.
   * *Example:* `BL` ($5$) - `CL` ($2$) = `BL` ($3$).
4. **ASCII Re-adjustment (`ADD BL, 48`):** To print the numeric result `3` on the screen, it must be turned back into its ASCII character code. Adding $48$ does this ($3 + 48 = 51$, which is the ASCII code for `'3'`).
5. **Output & Exit:** Prints the final character stored in `BL` and safely terminates the program (`AH = 4CH`).
