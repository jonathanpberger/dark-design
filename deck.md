class: center middle

# Hi :-)

---

# Using Dark Design patterns (for good!) in Agile UX practice.

Jonathan Berger, 2015

Agile Experience Design
SpooOOOOooooky October Meetup, 2015

---

# What is "Dark Design"?

---

# It's a *technique*, not a value claim

---

# It's not always bad

---

# Case study: cops

---

# the client


???

- philanthropic foundation
- focused on social justice
- "how can we do the most good?"

---

# Wrongful convictions

???

- death row inmates exonerated by DNA evidence
- lots of social science wrt bias, lineups
- easy to study? who cares!
- spare innocent people from death row!

---

# the app

--

- cops create a lineup

--

- witnesses pick the suspect out of the lineup


???

- remember that movie "The Usual Suspects?"

---

![The Usual Suspects](usual_suspects.jpg)

???

- This is many ppl think of when we hear "lineup"

---

# The Science

- Simultaneous Array
- Sequential Array


---

# using dark design

---

# example

--

## Story: Officer can select fillers

When the officer is on the lineup edit screen, she will see as the bottom section of that screen, "Fillers".

She should have the ability to select fillers either through sideloading (iOS imported/cameral roll photos) or from our in-application photo database.

If she chooses the photo database:

If the witness description or suspect has been entered, a search query will be synthesized based on that data and she will go directly to the Filler selection screen. If she has previously been through filler selection for this lineup, the previous search will be saved and re-executed (or results cached, I don't care right now) when she enters the screen.

If neither witness description nor suspect has been entered, she will go to the "Filler search" screen to enter search criteria.

If the search is synthesized, this will be the process for doing so:
 * For each of the following criteria: gender, race, age, hair.
   > If there is a witness description and there is a suspect description and the suspect is consistent with the witness description: use the witness description (could be single- or multi-valued). For example, if the witness said "white or asian" and the suspect is white, search for white or asian fillers.
   > If there is a suspect description and it is not consistent with the witness description: use the suspect description. For example, if the witness said "asian" and suspect is while, search for white fillers.
   > If there is a suspect description but no witness description, or vice-versa, use what you have.
   > If there is no description for this attribute, allow any value.
 * Do not restrict the search on height or weight in a synthetic search.

The filler selection screen will have, as a title, "Filler selection for case #______". If there is no case number entered yet, it will read "Filler selection".

On the left rail, you will see, from the top:
 * A textual description of the search criteria, constructed in a similar fashion to the witness ID descriptions in #68391808. There is an "Edit Search" button, which, if tapped, will take the user to the "Filler search" screen.
 * The witness description of the perp (if populated). If not populated, include pane but put word "None" in advisory style in place of description.
 * The suspect description, in a similar textual format. A small icon of the suspect photo should also appear (if populated). Similar "None" treatment if no suspect selected.
 * A pane of currently-selected filler photos, in the order in which they were selected. This pane is entitled "Fillers" (not what it says in the mock). If no filler photos have yet been selected, the pane says "tap photos to select fillers". The list should show photos in a grid view (hypothesis: two-wide), with the tile height chosen such that, if there are enough photos to overflow what's visible on the screen, a partial row of photos will "peek" out to provide a scrolling affordance.

If the suspect photo is tapped, it should embiggen. [No mock, but similar to the "Filler Detail" view, described below.] That embiggening should include a large suspect photo (same size as later witness presentation) and non-descriptive data about the suspect (name, date of birth, ID#). The embiggened view should have a single button, "Close".

When on the filler selection screen, the right side will have a scrolling list of current search results. Use "Polaroid" style from suspect photo selection. The list should show photos in a grid view (hypothesis: two-wide), with the tile height chosen such that, if there are enough photos to overflow what's visible on the screen, a partial row of photos will "peek" out to provide a scrolling affordance.

If you tap a filler photo on the right side, it will embiggen into the filler detail view with the controls allowing you to [cancel] or [add filler to lineup].

If a photo on the right side has already been selected for this lineup (regardless of if that photo was selected as a part of this filler selection invocation or not), it should have a "selected" state: the photo is dimmed and there's a big-ass checkbox on top of it. (Checkbox is getting smaller than in these mocks.)

If you tap a selected filler photo (whether you tap it on the left or the right), you see the embiggened "filler detail" view with the controls allowing you to [cancel] or [remove filler from lineup].

If the officer selects "Edit Search" near the search criteria (or if she invokes filler selection without having chosen witness or suspect details), she will see a "filler search" screen which will be populated with the most recent filler search criteria.

The "filler search" screen looks similar to the "witness description" edit screen: similar controls & behavior. Note that the attached mock doesn't show a textual summary, but I think we should keep it in.

Search criteria, when passed to the backend:
 * Handle attributes as "AND of IN": e.g. if "Male", race: "Black" and hair: "Brown" and "Black" are selected, the query is: gender IN (male) AND race IN (black) and hair IN (brown, black)
 * Handle values (age, height, weight) by selecting a set of photos within a comfortable range on either side (not well-defined) and then ranking for how close to the target the results are (with a distance metric for multiple attributes, with a weighting that treats age as more important than weight which is more important that height).
   > Consider using infinite scroll for more results with further & further distance on age/height/weight.
   > Evaluate BMI as the distance metric for height & weight.

There is a "Done" button somewhere (to be argued about: mock has it at lower-left, the rest of our UI has it at upper-right). When it is tapped, the user returns to the lineup edit screen with the current state.

-- fragment as:

Question: how to do paging of results

1. Synthesize search, show resulting photos, tap to embiggen, able to select, selected photos on left, done saves as fillers. [Don't allow entry into this flow unless witness and/or suspect has been chosen.]

2. Add checkboxes for selected photos

3. Ability to tap left or checked to de-select photos with embiggenizer.

4. Add witness description to left.

5. Add search description to left.

6. Able to edit search with searchy screen like witness description.

7. If filler selection is chosen when no witness or suspect description, start in search screen.

1000000. Possibly in the future: Refactor sideloading UI to use this kind of UI on a helicar.


---

# example 2

---

# example 3

---

# Thanks!

- <http://jonathanpberger.com/talks>
- Say hi on twitter at `@jonathanpberger`
- or `jonathanpberger` on github, twitter, gmail, etc...

