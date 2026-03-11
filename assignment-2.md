
https://github.com/osj-halfspace/akselos-assignment-2
0. Setup the dev environment
Use the setup dev environment skill to setup our dev environment.

1. Create Company Feedback & Ideas app 
We need an internal platform where employees can share anonymous feedback and ideas. The goal is to gather input and prioritize items through voting.
Core Functionality:
Users can submit anonymous feedback and ideas
Each submission can be voted on with a scale from -2 (strongly disagree) to +2 (strongly agree)
Users can view all submissions and their current vote totals
The system should help identify the most popular ideas and feedback
Technical Requirements:
Backend: Python 
Frontend: React (modern UI/UX)
Database: In-memory storage (no persistence needed for this workshop version)
Architecture: RESTful API connecting frontend and backend

2. Add authentication 
Add user accounts and login. When a user submits feedback, store the author in the backend (in memory database). Get the author from the logged-in user session, not from a form field. Each feedback should have a field indicating whether it should be shown anonymously to others or with the author's name.
Users can log in with their credentials and can see:
Their own feedbacks, where author is always shown as themselves 
Other feedbacks with author name, if feedback is not anonymous

3. Update UI (Shadcn MCP perhaps)
We need to add a few pages and navigation to make the app easier to use. First, create a landing page with the app name and an "Enter" button. This is the first thing users see. Once they click enter, they should see the main page with the list of all feedbacks and their votes. This is the main view.
On this main page, add two buttons:
Top left: "My Feedbacks" opens a page showing only the feedbacks the current user submitted
Top right: "Add New Feedback" opens a new page with a form to submit feedback. After submitting, return to the main list.

4. Compare outputs from assignment 1 and assignment 2

What you should hopefully have experienced, is a qualitative difference in the output between assignment 1 and assignment 2.
Both in terms of quality, but also in terms of output speed.

Send a screenshot in the group chat with the side by side example between assignment 1 and 2.
If you experience an increased development speed, feel free to get creative an add a new unique feature to your system,
– or even deploy it to the cloud somewhere?

