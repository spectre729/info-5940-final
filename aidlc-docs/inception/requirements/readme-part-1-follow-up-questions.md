# README part 1 follow-up questions

The first answers establish students/recent graduates as the initial audience, resume/profile-based matching with manual additions, scheduled discovery prioritizing postings from the last 72 hours, and all bonus features as stretch goals. The existing four-hour task is a reference, not yet a confirmed MVP frequency. These follow-ups clarify remaining behavior without changing earlier answers.

## Question 1: Profile input

How should the MVP receive resume and LinkedIn information?

A) User uploads resumes and pastes LinkedIn/profile text; no direct LinkedIn connection.

B) User uploads resumes and the product retrieves LinkedIn information from a profile URL through a supported access method to be verified.

C) Other (describe after the answer tag).

[Answer]: For the MVP, we should go with option A. 

## Question 2: Combined skills

How should multiple resumes and manual additions form the candidate profile?

A) Combine extracted skills into one user-reviewed profile, allowing corrections and preserving the source of each claim.

B) Keep resumes separate and let the user select one per search, with manual additions.

C) Other (describe after the answer tag).

[Answer]: Let's go with option A. Assuming users have multiple resume, the agent should mix and match various experiments and bullet points to best match a job description that the user is interested in

## Question 3: Scheduled delivery

What cadence and delivery channel should the MVP commit to? Specify any different cadence and whether scheduling only while the local app is running is acceptable.

A) Every four hours while the local app runs, with results shown in the app.

B) Every four hours while the local app runs, with results delivered by email.

C) Other (describe cadence, channel, and expected behavior while the app is closed).

[Answer]: I think this should be up to the user to decide if they want results in the app or through email. We should implement both and use the app as the default setting
