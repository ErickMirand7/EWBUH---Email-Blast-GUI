# EWBUH---Email-Blast-GUI
NOTE: I USED CLAUDE TO HELP me write this, I edited and over saw everything.

1. What This Tool Does
The EWB-UH Email Blast Tool is a desktop application that lets any chapter officer send polished,
on-brand email reminders to members directly from the chapter's Gmail account (uoh.ewb@gmail.com).
You pick a template, fill in the event details, optionally attach a flyer or newsletter, and send to your whole
list in a few clicks.
Key things it handles for you:
• Branded emails — every message goes out with the EWB logo, official colors, a professional
signature, and a sent-timestamp.
• Five templates — General Body Meeting, Project Meeting, Board Meeting, Volunteer Event, and a
flexible Other option.
• Saved member list — recipients are remembered between sessions.
• Image & PDF attachments — flyers embed inline; newsletters attach as downloadable files.
• Safe sending — a confirmation screen and a live progress indicator prevent accidental or duplicate
blasts.
Good to know: This tool runs entirely on your computer and talks straight to Gmail. There is no
website, login portal, or subscription — just the Python file and the logo image in one folder.
2. First-Time Setup
2.1 Install Python and Pillow
The tool needs Python 3.8 or newer. Most Macs already have Python through Anaconda. To display the
logo, you also need the Pillow library. Open the Terminal and run:
pip install pillow
If Pillow isn't installed the app still runs — the logo simply won't appear.
2.2 Keep the files together
Place these two files in the same folder. The recipient list file is created automatically the first time you add
someone.
ewb_email_blast.py ¬ the application
ewb_logo.png ¬ the chapter logo
ewb_recipients.json ¬ auto-created, holds your saved list
2.3 Set up the Gmail App Password
For security, Gmail will not let a script log in with the normal account password. You need a special
16-character App Password tied to the chapter account. This is a one-time setup (and only needs redoing
EWB-UH EMAIL BLAST TOOL | USER GUIDE
Engineers Without Borders — University of Houston Chapter Page 3
when a new officer takes over). Steps:
1 Sign in to uoh.ewb@gmail.com in a browser.
2 Go to myaccount.google.com ® Security.
3 Turn on 2-Step Verification if it isn't already on.
4 Search App Passwords in the search bar and open it.
5 Create a new one named EWB Email Blast.
6 Copy the 16-character code Google shows you (it appears only once).
7 Paste it into the APP_PASSWORD line near the top of the Python file.
The line in the file looks like this:
SENDER_EMAIL = "uoh.ewb@gmail.com"
APP_PASSWORD = "xxxx xxxx xxxx xxxx" # paste your code here
Security reminder: The App Password gives full send access to the chapter Gmail. Never post
the file with a real password to a public place like GitHub. If a code is ever exposed, delete it in the
Google security page and generate a new one.
3. Launching the App
Open the Terminal, move into the folder where the files live, and run the program. For example, if the files
are in a folder called EWB.Email.Blast:
cd ~/Coding\ Projects/EWB.Email.Blast
python ewb_email_blast.py
The window will open with two tabs at the top: Compose (the main tool) and How It Works (a built-in
quick reference).
Common mistake: Typing just ewb_email_blast.py won't work — you must put python in front of
it so the computer knows to run it with Python.
4. Using the Compose Screen
The Compose tab is split into two halves: the Recipients panel on the left, and the email builder on the
right.
4.1 Adding and removing recipients
1 In the Add Recipient box, type just the username — for example, jdoe — not the whole address.
EWB-UH EMAIL BLAST TOOL | USER GUIDE
Engineers Without Borders — University of Houston Chapter Page 4
2 Pick the domain from the dropdown next to it (@gmail.com, @uh.edu, @cougarnet.uh.edu, and more).
Choose Custom to type a full address.
3 Press Enter or click Add. The address appears in the list above.
4 To remove someone, click their address in the list, then click Remove.
Your list saves automatically, so it will still be there next time you open the app.
4.2 Filling in your sender info
Enter your Name and Position in the Sender Info fields. These flow into the email signature automatically.
A live preview strip shows how the signature will read.
4.3 Choosing a template
Pick a template from the dropdown and click Load to fill the Subject and Body. Each template has its own
tone:
Template Tone & Best Use
General Body Meeting Warm and welcoming — for all-member meetings.
Project Meeting Professional but friendly — for project teams.
Board Meeting Formal, with a full agenda — for officers/board only.
Volunteer Event Upbeat and inviting — for service opportunities.
Other A flexible friendly base for any announcement.
4.4 Setting the date and editing the body
The Event Date field auto-fills with today's date and automatically replaces the [DATE] placeholder when
you send. Edit it if your event is on a different day. In the body, replace every placeholder in square
brackets — [LOCATION], [TIME], [AGENDA ITEM 1], and so on — with your real details. You can freely
rewrite any of the text, and use Cmd+Z / Cmd+Shift+Z to undo and redo.
5. Attaching Images and PDFs
Click the + Attach Image / PDF button just above the message body to include files. You can select
several at once. The tool treats them two different ways:
• Images (PNG, JPG, GIF, WEBP) are embedded inline — they appear right inside the email body. This
is perfect for event flyers and graphics.
• PDFs and other files are added as normal attachments that recipients can download. This is perfect
for newsletters.
EWB-UH EMAIL BLAST TOOL | USER GUIDE
Engineers Without Borders — University of Houston Chapter Page 5
A small count shows next to the button (for example, “2 attachment(s): flyer.png, newsletter.pdf”). Click
that text to clear all attachments and start over.
Important: Do not try to paste an image directly into the body text box — it won't work. Always use
the Attach Image / PDF button. Keep each file under 20 MB; Gmail's total message limit is 25 MB.
6. Previewing and Sending
Before sending, click Preview to read the plain-text version of your email and confirm the details look
right.
When you're ready, click Send Blast. A confirmation window titled Ready to Send? appears,
summarizing the subject, sender, recipient count, date, and any attachments, along with the full recipient
list. Review it, then click Yes, Send Blast to send or Cancel to go back.
What happens while it sends
The status line at the bottom of the screen updates to show progress — “Sending… 2 of 5 sent” — and the
cursor becomes a spinning wheel. Each email is sent individually, so a list of several people takes a few
seconds.
Please be patient and do NOT click Send again while it's working. Sending takes a few seconds
and clicking repeatedly could send duplicate emails. When it's done, a “Send Complete” box shows
how many were delivered and the exact time.
7. Troubleshooting
“Gmail rejected the login” / Authentication Failed
This almost always means the App Password is wrong, expired, or was made on the wrong account. Make
sure it was generated while signed into uoh.ewb@gmail.com, and that it is copied exactly (the spaces
are fine). If in doubt, delete the old one in the Google security page and generate a fresh one, then update
the APP_PASSWORD line.
“command not found” when launching
You probably typed the file name without python in front of it, or you're not in the right folder. Use cd to
move into the folder, then run python ewb_email_blast.py.
The logo doesn't show in the app
Make sure ewb_logo.png is in the same folder as the script, and that Pillow is installed (pip install
pillow). The emails will still send correctly either way.
Nothing happens / the window freezes when sending
EWB-UH EMAIL BLAST TOOL | USER GUIDE
Engineers Without Borders — University of Houston Chapter Page 6
Give it a few seconds — sending is working in the background and the status line will update. If it truly
hangs, check your internet connection and that the App Password is still valid.
8. Handing the Tool to the Next Officer
This tool is meant to outlast any single president. When you pass it on:
1 Have the new officer update the Name and Position fields — these drive the email signature.
2 Generate a fresh Gmail App Password for the chapter account and update the APP_PASSWORD line
in the file.
3 Share the whole folder. The saved recipient list carries over automatically.
The How It Works tab inside the app repeats these steps, so a new officer can get going without a
handoff meeting.
Questions or handoff help: Erick Miranda · erick202080@gmail.com · 832-872-5819
Built in Python for the chapter. Go forth and email responsibly!
