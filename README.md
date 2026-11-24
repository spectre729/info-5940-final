# info-5940-final

## Team name and netID

Yiyang Cheng yc3259

to be filled...

## Coding Agent and AI-DLC version


also to be filled

## Problem and rationale for using LLMs

Students and recent graduates looking for jobs and internships often have to search across job boards, read lengthy descriptions, and decide whether each opportunity fits their background. Broad search results and recommendations can leave candidates spending time on roles that do not match their skills, experience level, or preferences. Repeating this process to find newly posted opportunities adds to the effort. Our project aims to reduce that manual screening by providing scheduled, personalized recommendations that prioritize jobs and internships posted within the last 72 hours.

An LLM is useful for comparing the varied language in job descriptions with the skills, projects, and experiences described in a candidate's resumes and profile. Candidates may maintain several resumes that emphasize different parts of their background, so the product will bring that information, pasted profile text, and manual additions into a user-reviewed profile. The LLM can use this context to identify relevant connections and explain why a role may be worth considering, including gaps or uncertain requirements. Recommendations should link to source listings, with posting dates and eligibility details grounded in those sources rather than assumed by the model. The goal is to help candidates make informed application decisions and spend less time repeatedly screening listings. Networking, recruiter discovery, and application essay assistance are stretch goals beyond the core discovery workflow.

## Planned LLM integration

The planned workflow uses an LLM to extract skills, projects, and experience from uploaded resumes and pasted profile text, then combine them with manually entered preferences into a profile the user can review and correct. During job discovery, the LLM will compare retrieved listings with this profile, prioritize potentially relevant opportunities, and generate explanations grounded in the candidate's experience and the listing. It should highlight missing qualifications or unclear requirements rather than inventing a match. The proposed agentic component will use a limited set of retrieval tools to search supported sources and inspect listing details before producing recommendations; specific sources and tool interfaces will be defined during design.

Scheduling, saved results, duplicate detection, and notification delivery will be handled by application code. Users will receive results in the app by default, with email delivery available as an option. Posting dates and other factual details must come from retrieved sources, with unavailable information marked as unknown. The planned LLM provider and model are still to be selected based on the team's available access, cost constraints, and tests of profile extraction and job-matching quality; this choice must be documented before the README is finalized.

## Project scope and feasibility

By the December 16 final-project deadline, our target is a locally running application for students and recent graduates that accepts multiple resumes, pasted profile text, and manual preferences; builds a user-reviewed candidate profile; and periodically retrieves and explains relevant jobs and internships, prioritizing postings from the last 72 hours. The MVP will support reviewing and saving recommended opportunities, suppressing duplicate listings, and choosing in-app or email delivery. The exact refresh frequency and behavior when the local application is closed remain to be defined. Networking opportunities, hiring-manager and recruiter discovery, application essay assistance, and automated resume rewriting are outside the committed MVP. Interview and online-assessment tracking from the reference system are also excluded.

To keep the project manageable, we plan to limit retrieval to a small set of supported sources and focus on one complete profile-to-recommendation workflow. The product only needs to run on the team's laptops, so cloud deployment is not required. Source access, model quality and cost, resume extraction, and reliable scheduling and email delivery are the main feasibility risks to validate early. A fixed set of sample profiles and listings will support repeatable evaluation of matching explanations, factual grounding, freshness handling, and duplicate suppression, alongside a live retrieval demonstration. The team still needs to confirm source access and model availability before treating this scope as a validated implementation plan.

## Collaboration plan

to be filled
