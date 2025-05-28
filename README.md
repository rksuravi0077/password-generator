Password Generation Logic:<br><br>

1. User Input:<br>
 - Length of the password (N)<br>
 - Choice for including special characters ('Yes' or 'No')<br>
 - Choice for including numbers ('Yes' or 'No')<br><br>

2. Password Construction:<br>
 - Generate a random string of length (N-2) with alphabets (first character must be an alphabet).<br>
 - If 'use_numbers' is 'Yes', append a random number; otherwise, append a random alphabet. The password length becomes (N-1).<br>
 - If 'use_special_chars' is 'Yes', append a random special character; otherwise, append a random alphabet. The final password length becomes (N).<br><br>

3. Output:<br>
 - Display the generated password to the user.<br>
