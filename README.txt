EXAM BOARD  v0.9 (beta)
Designed by Armin Jamshidpey (code written with the assistance of a generative AI tool).
Copyright (c) 2026 Armin Jamshidpey, MIT License (see LICENSE)
=========================================================

PLEASE READ FIRST: BETA SOFTWARE, USE WITH CAUTION
  This is a beta version. It is a visual aid for the exam room and
  nothing more. It does not replace the proctors, the official
  announcements, the official clock, or the exam regulations of
  your institution. Proctors remain fully responsible for the
  conduct of the exam: for announcing and enforcing start and end
  times, for deciding when students may leave or go to the
  washroom, and for checking that what the screen shows is
  correct. Always confirm the room PC's clock and the control
  file before the exam starts, and keep an ordinary clock visible
  as well. Use at your own risk; see LICENSE for the warranty
  disclaimer.

WHAT IT IS
  Exam Board is for an exam that takes place in several rooms at
  once. Each room's projector shows the same page: a large clock
  taken from one shared server, the exam's start and end times,
  the announcements (written in LaTeX, so corrections with formulas
  display properly), and whether washroom breaks and hand-in are
  allowed right now. The coordinator edits ONE text file on the web
  server, and every room updates within seconds, so all students
  see the same announcement, the same start time and the same end
  time, whichever room they are sitting in.

  How it helps
  - Consistency: every room shows exactly the same announcement at
    the same time, however many rooms the exam is spread over.
  - Persistence: a correction stays on the screen, so students who
    were not listening the first time can still read it.
  - Accessibility: students who are hard of hearing or use hearing
    aids get the announcement in writing, not only by voice. The
    reverse also matters: proctors are asked to read every new
    announcement aloud the first time it appears, for students with
    low vision and anyone who cannot read the screen clearly from
    their seat. The page intentionally does not
    read announcements out itself, because microphone and speaker
    setups differ from room to room and a screen cannot know
    whether it was heard; a proctor can.
  - Ad-free: unlike free online clock sites projected in exam
    rooms, it shows nothing but the exam information.

FILES
  exam-live.html   the display page (open this on the room PC)
  exam.txt         the control file (the coordinator edits this)
  katex/           math rendering library (leave as is)
  exam-board.html  the stand-alone version: the BACKUP. It needs no
                   server and no internet. If the website is down or
                   the room has no network, open this file instead;
                   the proctor types the announcements and
                   switches the keys by hand. Before the exam, copy
                   it to a USB stick or share it in advance through
                   the exam's communication channel (e.g. the MS
                   Teams channel for the exam). (Details further down.)
  README.txt       this file
  CHANGELOG.txt    what changed in each version
  LICENSE          MIT License for Exam Board
  katex/LICENSE    MIT License for the bundled KaTeX library

SETUP (once)
  1. Upload the whole directory to the course website, e.g.
        https://your.site/course/examboard/
  2. On each room PC open
        https://your.site/course/examboard/exam-live.html
     and press F11 for full screen.

BEFORE EVERY EXAM: CHECKLIST (proctor or coordinator)
  [ ] Just before the exam: open the page in the room, on the
      podium PC, with the projector on. Press F11.
  [ ] The toolbar says "clock: server" (not "this PC").
  [ ] The toolbar does NOT say "Check exam.txt: ..." in orange. If
      it does, fix exam.txt until the message goes away.
  [ ] From the back row you can read the red key text and the
      announcement. If not, use the Theme button (light background
      often projects better) or raise fontsize: in exam.txt.
  [ ] exam.txt has today's course, start, end and windows.
  [ ] exam-board.html (the backup) is in the room: on a USB stick,
      or shared in advance through the exam's communication channel
      (e.g. the MS Teams channel for the exam).
  [ ] You know who edits exam.txt during the exam and how to reach
      them.
  [ ] During the exam: read every new announcement aloud the first
      time it appears on the screen.

DURING THE EXAM (coordinator)
  Edit exam.txt and save/upload it. All screens update within ~5 s.
  The toolbar shows "Updated <time>" so you can confirm it arrived.
  If the file contains a mistake (a time that is not HH:MM, an end
  before the start, a hand-in window outside the exam, a misspelled
  setting name, ...) the toolbar instead shows "Check exam.txt: ..."
  in orange with the reason. The screen keeps working with what it
  could understand; fix the file and the message disappears.

  department: text shown top-left (default: Cheriton School of
              Computer Science; leave empty to hide)
  logo:       image file shown before the department name (default
              logo.png). Put the official logo of the University of
              Waterloo, or of your own university, in this directory
              as logo.png. If the file is missing, no logo is shown;
              nothing else breaks.
  course:     text shown after the department name
  timeserver: where the clock comes from. EMPTY (the default) = the
              clock of the server hosting this page, read from the
              Date header of every exam.txt fetch. Or a URL of a time
              service, checked once a minute, e.g.
                 timeserver: https://worldtimeapi.org/api/timezone/Etc/UTC
              The reply may be JSON with a utc_datetime / datetime /
              dateTime / currentDateTime field, or any page whose
              Date header the browser is allowed to read (a service on
              another host must send Access-Control-Expose-Headers:
              Date). If the time server cannot be reached the page
              falls back to the room PC's clock and says so in the
              toolbar ("clock: this PC (time server unreachable)").
  start:      09:00          (24-hour, HH:MM)
  end:        11:30
  duration:   110            length in minutes; use INSTEAD of end:
                             (end = start + duration)
  display:    clock          (default, recommended) big display shows
                             the time of day
              countdown      big display shows the time REMAINING until
                             the end, e.g. 1:39:52, with "remaining"
                             under it; at the end it shows 0:00 and
                             "TIME IS UP" in red. The time of day stays
                             visible, small, in the toolbar.

              Why we recommend the clock: a clock and a countdown carry
              the same information, but they feel different in the
              room. A clock simply says what time it is and lets each
              student plan from the start and end times shown beneath
              it. A countdown draws the eye to a number that is always
              shrinking, and for many students that reads as "you are
              running out", a small, constant source of pressure for
              the whole exam, and most of all for those who are already
              anxious. The clock gives everyone the same facts without
              that undertone. It is also what most exam regulations
              expect, and some (e.g. JCQ in the UK) do not permit
              countdown clocks in exam rooms at all. The countdown
              option is there for coordinators who prefer it; please
              choose it with the students' experience in mind, and
              check your institution's exam rules first.
  handin:     10:00-11:20    hand-in is "Allowed" during this window
  washroom:   09:30-11:15    washroom is "Allowed" during this window
  handin-override:    on | off | (blank = automatic)
  washroom-override:  on | off | (blank = automatic)
  endmessage:     text shown in red in place of the clock from the
                  end time on (default: "Time is up. Please remain
                  in your seats until all papers have been
                  collected.")
  releasemessage: text shown in green after the proctor presses the
                  "Papers collected" button (default: "All papers
                  have been collected. You may leave now.")
  fontsize:   44             max text size, shrinks to fit
  instructions:              LaTeX block shown BEFORE the start time
  announcement:              LaTeX block shown FROM the start time on

  Before the start time the screen shows the instructions and, in
  place of the clock, "Don't start yet, read above" in red (the
  current time is still visible, small, in the toolbar). At the
  start time it switches to the clock and the announcements by
  itself. No start time = clock and announcements at all times.

  AT THE END: when the end time passes, the clock is replaced by the
  endmessage in red; the keys stay as they are. A "Papers collected"
  button appears in the toolbar of each room's screen (and only after
  the end time). When the proctor has collected every paper in THAT
  room they click it: the screen turns to the green releasemessage
  and the keys disappear. This is local to that room's PC, other
  rooms are not affected, which is right because collection finishes
  at different times. Clicking the button again undoes it.

  EXTENDING THE EXAM: if the exam is interrupted (a fire alarm, say)
  and the coordinator extends it by putting a later end time in
  exam.txt, every screen returns to the clock and the announcements
  within a few seconds, and the "Papers collected" button disappears
  until the new end time. A room that had already pressed the button
  is reset as well.

  HOW THE LATEX WORKS (in both the instructions and announcement
  blocks): this is not a LaTeX compiler and there is no preamble, no
  \usepackage and no \begin{document}. Write the block as you would
  write a short paragraph inside a LaTeX document.
  - Math between $...$, \(...\), \[...\] or $$...$$ is typeset by
    KaTeX (the library in the katex/ directory) with the usual LaTeX
    fonts. It knows practically all ordinary math: \frac, \int,
    \sum, \sqrt, \text{}, Greek letters, \mathbb, matrices,
    aligned, etc. (amsmath-style commands are built in).
  - Outside math, only these are understood: \textbf{}, \emph{},
    \textit{}, \underline{}, \\ (line break), a blank line for a
    new paragraph, \begin{itemize} \item ... \end{itemize},
    \begin{enumerate} ... \end{enumerate}, and % comments.
    Any other command outside math is shown as literal text, so you
    will see it on the screen and can fix the file.
  - In particular, macros you have defined yourself (\newcommand,
    \def, \DeclareMathOperator in your course or exam files) are
    not available here. Write the formula out in full.
  - A mistake inside a formula is shown in red; it never breaks the
    page. The screens re-render within about 5 seconds of saving.

SEVERAL ROOMS / SECTIONS
  Make a second control file (e.g. room-b.txt) and open
        exam-live.html?file=room-b.txt
  on that room's PC. Each file is independent.

STAND-ALONE VERSION (BACKUP): exam-board.html
  A single file that runs with no server and no internet. It is in
  this directory so that every room always has a fallback: if the live
  page cannot load exam.txt (status text turns orange) or the network
  is gone, open exam-board.html from the directory, from a USB stick
  or from the exam's communication channel (e.g. MS Teams) and carry
  on by hand. Open it in a browser and press F11.
  - Type announcements in the top box (plain text, no LaTeX).
    A- / A+ change the size; Clear and Undo as expected.
  - Click the keys, or press 1 / 2, to switch Allowed / Not allowed.
  - The gear (⚙) menu, top right: 12/24-hour clock, show seconds,
    show date, department name (default Cheriton School of Computer
    Science), rename the keys. It shows logo.png from the same
    directory if present, so keep logo.png next to it on the USB
    stick or in the shared channel. In a key label, \\ starts a
    second, smaller line, e.g.
        Washroom\\(need to wait for a Proctor):
  - Settings and the last message are remembered on that PC.

USING IT AT ANOTHER UNIVERSITY OR DEPARTMENT
  Nothing is hard-wired to Waterloo. To make it yours:
  1. Logo: put your institution's logo in this directory as logo.png
     (PNG or SVG, any size; it is shown about 30 px tall, so a wide
     wordmark looks best). To use another file name, set
         logo: ourlogo.svg
     in exam.txt. The stand-alone exam-board.html only looks for
     logo.png next to itself.
  2. Department name: in exam.txt set
         department: School of Mathematics, Example University
     (or leave it empty to show no department). In the stand-alone
     version, type it in the gear (⚙) menu once; it is remembered.
     To change the built-in default, open either .html file in a
     text editor and replace the text
         Cheriton School of Computer Science
     (it appears twice in each file).
  3. Key labels and wording ("Washroom (need to wait for a Proctor)",
     "Hand-in paper", "Allowed / Not allowed"): in exam-live.html
     search for  class="key"  and edit the text inside <span>s; the
     words Allowed / Not allowed are in the function setKey(). In
     exam-board.html the labels are in the gear menu; the Allowed /
     Not allowed words are in setKey() as well.
  4. Clock format: exam-live.html shows 12-hour time; for 24-hour,
     in function tick() remove the two lines that set ampm and
     h = h % 12 || 12. The stand-alone version has a 24-hour switch
     in the gear menu.
  5. Language: all visible English strings are in the two .html
     files as plain text; nothing is generated, so a find-and-replace
     is enough to translate it.

  A note on the key colours: the keys are red and green, AND they say
  "Allowed" / "Not allowed" in words. Both are deliberate. A small
  group of people cannot reliably tell red from green, so the words
  carry the meaning and the colour only reinforces it. If you restyle
  the keys, keep the words (or add a symbol); never let colour be the
  only cue.

BUGS, QUESTIONS AND SUGGESTIONS
  Please report them on the GitHub project's Issues page:
      https://github.com/arminjamshidpey/exam-board/issues
  Include the version (top of this file), which file you were using
  (exam-live.html or exam-board.html), the browser, and what you
  expected to see. For a display problem a photo of the screen or a
  screenshot helps a lot. Pull requests are welcome.

LICENSE
  Exam Board is open source under the MIT License: you may use,
  copy, modify and redistribute it freely, including at other
  institutions, provided the copyright notice and the LICENSE file
  stay with it. The header comment at the top of each .html file
  carries that notice; please leave it in place.
  The bundled KaTeX library (katex/) is also MIT-licensed, by Khan
  Academy and contributors; its notice is in katex/LICENSE.

NOTES
  - Time: exam-live.html takes the time from the SERVER that hosts
    the page and exam.txt (the Date header of every fetch), so all
    rooms show the same time whatever the room PC's clock says. The
    toolbar says "clock: server" once that has happened; "clock: this
    PC" means the page has not reached the server yet. With a
    timeserver: line it says "clock: time server". The stand-alone
    exam-board.html has no server and shows the room PC's clock, so
    check that clock when using the backup.
  - Needs a web server (opening the .html by double-click will not
    load exam.txt, browsers block that). Any static host works.
  - Nothing is stored anywhere; refreshing the page is always safe.
  - Lost connection: the status text turns orange and the last
    received information stays on screen.
