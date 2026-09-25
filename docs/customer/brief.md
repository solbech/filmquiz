# Customer Brief

> Source: `docs/customer/Filmmusikquiz.docx`, the customer's own
> description, originally written in Danish. Translated to English and
> reformatted into headings below — content and meaning are otherwise
> unchanged, not interpreted or analyzed.
>
> **This file is never edited by Claude** beyond faithful
> translation/reformatting of the source document. Interpretation belongs
> in `docs/product/spec.md`.

## Film music quiz

I think the time has passed for a movie quiz the way we used to know it:
with screenshots that people had to guess. Pretty much all screenshots get
eaten by a reverse image search these days, and then there's not much fun
left in it.

Where there can be something fun to gain, on the other hand, is doing the
same thing, just with audio clips from soundtracks. A blatant rip-off of
this site (which, only just now, I see has added the option to write
free-text answers instead of just multiple choice!):
https://www.movie-music-quiz.com/

That quiz, however, is a bit too fancy-smancy for my taste, with a
confusing graphical background, a 60-second time pressure, and various
other crap. There are, however, also elements I do like — e.g. that once
you've guessed correctly, it shows what others guessed, how many guessed
correctly, etc. Check it out.

What I'd actually like is a kind of mix of the movie quiz (where you
logged in and guessed, and precisely because you were logged in, could
return to the quiz later) and the quiz mentioned above.

If I try to describe it in your terms, from a participant and an
administrator perspective respectively, it could be something like this.

## Participant

The first time, the participant is met by a welcome page describing what
the quiz is about. After that, they can either log in or sign up as a
user.

Once signed up as a user, they now have the option to choose which round
of the quiz to enter (or perhaps, analogous to the quiz above, which
genre they'd like to be quizzed in).

When clicking into a specific round, the user is presented with a list or
a row of numbered tiles they can choose freely between. The number is up
for discussion. In the movie quiz we ran 40 titles — 8 extremely easy, 8
easy, 8 medium, 8 challenging, and 8 hard. It could also be 20, with 4 in
each difficulty level instead.

When clicking into one of the 20/40 options, the user is presented with a
page containing the following:

- a blurred CD cover (alternatively, a square field with a large question
  mark)
- a player
- a text field where they can enter their answer

When the player is pressed, an audio clip of approx. 30-60 seconds plays.
The clip can be listened to as many times as desired.

To guess, the user types a movie title into the free-text field. If they
answer incorrectly, they get a generic message that the answer was wrong;
try again.

If they answer correctly, the following happens:

- the blurred CD cover is replaced by the actual cover
- next to the cover is the movie's title
- below that is the composer of the music
- at the bottom, the year of the movie's premiere
- the free-text field disappears

Once a user has correctly guessed a title, their progress in the quiz is
automatically saved, so the quiz doesn't need to be completed in a single
sitting.

Once a user has correctly guessed all audio clips, they get a message
along the lines of "Congratulations! You've completed the quiz" or
similar. The user can freely enter the same round again, but then all the
answers are simply revealed, and there's no free-text field. They can
listen to the audio clips if they want, but they can't guess — because
they've already completed this round.

## Administrator

This part is harder for me to write, because I'm probably limited by not
knowing what the realistic options are.

The great thing, of course, would be a back-end where, on a page, you
could press a button — "Create quiz" — after which you'd be directed to
one or more pages where you:

- Upload an audio file
- Upload a CD cover
- Enter the correct title, composer name, and year
- Enter a number of alternative correct guesses that are also accepted as
  correct if people type them
  - Example: An audio clip is from "Raiders of the Lost Ark". Other
    accepted answers are "Indiana Jones" or "Jagten på den forsvundne
    skat" (the Danish release title)
  - Example: An audio clip is from "Die Hard With a Vengeance". Other
    accepted answers are "Die Hard 3", "Die Hard Mega Hard", or maybe
    even just "Die Hard"

When I ran the movie quiz back then, the entire back-end was completely
"analog" — correct answers, years, alternative answers, etc. had to be
typed into an Excel spreadsheet, which had to be converted to CSV and then
imported into a specific table in the underlying SQL database. It was a
pain and a chore. It must be possible to do better today.
