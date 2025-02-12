# Password Strength Checker

This is a simple password strength checker built with Vue.js. It evaluates the strength of a password based on length, inclusion of uppercase and lowercase letters, numbers, and special characters. 

## Features
- **Username Field**: Basic input for entering a username.
- **Password Field**: Password input with toggleable visibility.
- **Password Strength Indicator**: Displays password strength visually via a progress bar.
  - **Strength levels**: Red (Weak), Orange (Moderate), Green (Strong)
  - Password strength is determined based on length and character diversity.

## Project Structure

The application has a single Vue component that includes:
- **Password strength calculation** based on several criteria.
- **Username check** to ensure the password does not contain the username.
- **Computed properties** to dynamically update strength value and color.

## Password Scoring System

The password scoring system assigns points based on several criteria to determine the strength of a password.

1. **Length**:
   - Less than 8 characters: **0 points** (weak)
   - 8-11 characters: **+20 points**
   - 12 or more characters: **+35 points**

2. **Uppercase and Lowercase Mix**:
   - If the password contains both uppercase and lowercase letters: **+25 points**

3. **Numbers**:
   - If the password contains at least one number: **+25 points**

4. **Special Characters**:
   - If the password includes any special characters (e.g., `@`, `#`, `$`): **+15 points**

5. **Common Password Check**:
   - If the password is detected as a common password (not yet implemented): **-20 points**

### Total Score
The maximum achievable score is **100 points**. The strength color changes based on the total score:
   - **0-29 points**: Red (Weak)
   - **30-69 points**: Orange (Moderate)
   - **70-100 points**: Green (Strong)

## Setup

To run the project locally:

1. Clone the repository:
    ```
    git clone https://github.com/stefanstoichkov/password-strength-checker.git   
    cd password-strength-checker
    ```
2. Install dependencies:
    ```
    npm install
    ```
3. Run the development server:
    ```
    npm run dev
    ```

The app should be available at `localhost:5173`
