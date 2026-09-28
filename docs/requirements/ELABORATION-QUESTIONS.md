# Questions for the product owner

Source: `docs/input/BUSINESS_REQUIREMENTS.md` (read-only).

These follow a **member** using the booking website from opening it to the stay ending, then an **administrator** doing the same job for the whole community.

Pick one option, or write your own. If you cannot decide, write **open**.

Already in the business note (not asked again): one booking at a time; at most 7 nights; future dates only; at most 2 upcoming bookings; a member cannot cancel after the stay has started; cancelled bookings free the dates and stay in history.

Not in this product unless you add them at the end: payments, email, extra cabins, real login, phone app.

---

# Member — from first visit to the stay ending

## Opening the website

The note says login is out of scope. People will pick from a short list of sample users (at least two members and one administrator).

**1.** When the website opens, who are they acting as?

- They choose a person first, then continue
- They start as a member, and can change to administrator if needed
- They start as an administrator, and can change to a member if needed

**Answer:**

**2.** Can an administrator also book the cabin as themselves?

- No. Administrators only manage bookings
- Yes, and they follow the same limits as members
- Yes, and they may break the usual limits in special cases

**Answer:**

---

## Seeing which dates are booked

The note: a member can see which dates the cabin is already booked.

**3.** What should a member see first?

- Which dates are free or taken
- Their own bookings, with a way to check dates and make a new one
- A short welcome, then which dates are free or taken

**Answer:**

**4.** On a date booked by someone else, what does a member see?

The note says administrators see **who** made each booking. It does not say members do.

- Only that the date is taken
- The name of the person who booked, like the group chat
- Names on their own bookings; other people’s dates only show as taken

**Answer:**

**5.** If a booking is cancelled, how do those dates look when a member is planning?

The note: cancelled bookings free the dates but remain visible in history.

- The dates look free. The cancel is only in history
- The dates look free, and history is on the same page
- The dates still show as cancelled on the calendar

**Answer:**

---

## Asking for a booking

The note: a member can request a booking for a date range.

**6.** Does “request” mean the booking is made at once, or does an administrator have to accept it?

- It is booked at once if the dates are free and the usual limits are met
- It waits for an administrator to accept or refuse. Those dates are held in the meantime
- It waits for an administrator, but other people can still try for the same dates until someone is accepted

**Answer:**

**7.** Two members ask for the same dates at nearly the same time. Who gets the cabin?

- Whoever finished asking first. The other person is told those dates are taken
- Both wait, and the administrator chooses (only if you chose waiting in question 6)
- Prefer the member who has fewer upcoming bookings; if equal, whoever asked first

**Answer:**

**8.** One booking ends on a Saturday. Can the next booking start that same Saturday?

The note says bookings must never overlap. It does not say whether leaving day and arriving day may be the same.

- Yes. One leaves, the next may arrive that day
- No. The next booking starts the day after
- Only if an administrator has allowed it for that day

**Answer:**

**9.** Can a booking start today, or only from tomorrow?

The note: bookings can only be made for future dates.

- Only from tomorrow
- Today is allowed

**Answer:**

**10.** Besides the dates, must the member add anything?

The note only mentions a date range.

- Dates only
- Dates and an optional note
- Dates and how many people are staying

**Answer:**

---

## Getting the booking

There is no email and no payment. “You have a booking” means what the website shows.

**11.** How does the member know they have the booking?

- They see a clear confirmation with the dates, and it appears in their bookings
- It appears in their bookings, with no separate confirmation
- They only have it after an administrator accepts (if you chose waiting in question 6)

**Answer:**

**12.** When they look at their own bookings, what is included?

The note: a member can see their own bookings. It does not say whether that includes past or cancelled ones.

- Only upcoming, and a stay that has already started
- Upcoming, current, past, and their own cancelled bookings
- Upcoming and current only; past and cancelled are for administrators

**Answer:**

**13.** They are at the cabin this week. Does that stay count toward the “2 upcoming” limit?

- No. They may still have two bookings in the future
- Yes. So they may only have one more in the future

**Answer:**

---

## Before the stay — changing or cancelling

The note: a member can cancel their own upcoming booking. It does not mention changing dates.

**14.** May they change the dates, or only cancel and book again?

- Only cancel (if it has not started) and make a new booking
- They may change dates on an upcoming booking, if the new dates still fit the limits
- They phone an administrator, who handles it

**Answer:**

**15.** When they cancel, should anything extra happen?

- Cancel at once
- Ask them to confirm, then cancel
- They should give a short reason

**Answer:**

**16.** After they cancel, do they still see that booking?

- Yes, in their list, shown as cancelled
- No. Only administrators keep cancelled bookings

**Answer:**

---

## During the stay and after

The note: a booking that has already started cannot be cancelled by a member. An administrator can cancel any booking.

**17.** Does anyone need to mark “arrived” or “left” on the website?

The note does not mention this.

- No. The dates on the booking are enough
- The member marks arrived and/or left
- Only an administrator marks that

**Answer:**

**18.** They want to leave early and free the rest of the week. What happens?

- The member cannot change it. An administrator may cancel if asked
- The member can give back the unused days
- The booking stays until the original end date

**Answer:**

**19.** After the stay, who can see old bookings?

The note mentions history for cancelled bookings. It does not say who may see completed stays.

- Each member sees only their own past and cancelled bookings. Administrators see everyone’s
- Any member can see who had the cabin in the past
- Only administrators see history. Members see only what is still coming

**Answer:**

---

# Administrator — looking after all bookings

The note: an administrator can see all bookings, including who made them, and can cancel any booking.

## Seeing bookings

**20.** What should an administrator see first?

- All bookings with names, dates, and whether each is upcoming, current, finished, or cancelled
- The same calendar members see, but with names and a way to cancel
- A list of bookings waiting for a yes/no first (only if you chose waiting in question 6)

**Answer:**

**21.** Is the full list enough, or do they need to narrow it?

The note does not require this.

- The full list is enough
- They should be able to look at one member, or only some dates

**Answer:**

---

## If an administrator must accept bookings

Skip 22–23 if bookings are made at once (question 6).

**22.** What may they do with a waiting booking?

- Accept or refuse. Refused ones stay in history
- Accept, refuse, or change the dates then accept

**Answer:**

**23.** If nobody answers, what happens to a waiting booking?

- It waits until it is accepted, refused, or the dates have passed
- It drops off when the start date arrives, and the dates become free

**Answer:**

---

## Booking or changing on someone’s behalf

The note does not say administrators can create or edit bookings, only view all and cancel.

**24.** May an administrator create a booking for a member (for example after a phone call)?

- No. Members create their own. Administrators only view and cancel
- Yes, in that member’s name, still following the usual limits
- Yes, and they may ignore the usual limits

**Answer:**

**25.** May an administrator change dates instead of cancelling?

- No. Cancel only
- Yes, if the stay has not finished and the new dates fit
- Yes, including ending a current stay early so later days are free

**Answer:**

---

## Cancelling

**26.** “Cancel any booking” — does that include a stay happening now, or one that already finished?

- Upcoming and current. Finished stays stay finished
- Only bookings that have not finished
- Even finished stays can be changed to cancelled

**Answer:**

**27.** If they cancel a stay that has already started, when can someone else use the cabin?

- On the remaining days, straight away
- From tomorrow
- The remaining days stay taken unless the administrator also changes the dates

**Answer:**

**28.** Should there be a reason, and who sees it?

- No reason
- A reason only administrators see
- A reason the member can see on the website (no email)

**Answer:**

**29.** Should history show who cancelled — the member or the administrator?

- No. Cancelled is enough
- Yes

**Answer:**

**30.** The cabin is unusable (for example a burst pipe). What should an administrator do here?

- Cancel the current booking
- Also mark days as closed, with no member name
- Nothing on the website. Handle it off the website; cancel only if you want the days opened

**Answer:**

**31.** Can an administrator undo a cancel?

The note does not mention this.

- No. A new booking is needed
- Yes, if those dates are still free
- Yes, even if it clashes with another booking

**Answer:**

**32.** When they look at “all bookings”, what is included?

- Every booking, including old and cancelled
- Upcoming and current first, with a way to open history

**Answer:**

---

**33.** Is there anything else the community wants that is not in the original note? Write **nothing else**, or a short list.

**Answer:**

---

Please answer **4, 6, 8, 9, and 13** first. Those change the rest of the specification.
