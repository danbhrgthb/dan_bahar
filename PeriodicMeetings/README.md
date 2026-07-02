# Periodic Meetings

This folder contains records of periodic meetings, to-dos, etc.
Longer-term goals or
tracking of individual development and projects
should be placed in `./Projects/`, `./IDP/`,
or in project-specific repositories.

## Usage

Each week (or whatever duration is appropriate),
the trainee should fill out a periodic report
using either the Issue Template or the markdown template
(described more below).
This should ideally be completed
_in advance_ of the meeting, so that the supervisor
has time to review.

Once the meeting is concluded, the trainee or supervisor
should commit the contents to a markdown file contained
in the folder, linking to relevant issues / PRs as appropriate.

### Markdown template

Use the meeting template file in the `PeriodicMeetings/` directory.

#### Basic procedure (web-based)

1. Copy the markdown contents from the file in `PeriodicMeetings/YYYY-MM-DD_template.md`
   1. To get the source code (rather than formatted for web), click the "source" or "raw"
      buttons at the top of the file on github ![Screen capture of source and raw buttons on github](https://i.imgur.com/CPyd7r0.png)
2. In the `PeriodicMeetings/` directory on github, click "Add files" and "Create new file" ![Screen capture of the "add files" menu on github](https://i.imgur.com/oNgsZVj.png)
3. Name your file with the ISO date in `YYYY-MM-DD` format (Step 1 in image)
   Eg for August 1st, 2022, use `2022-08-01.md`.
4. Copy the contents from the template into the "Edit new file" box, and edit it as appropriate
   for the current week.
5. Enter a commit message and additional description if appropriate,
   then select "create new branch", "propose new file."

![File creation dialogue on github](https://i.imgur.com/sjVvi1S.png)

6. On the resulting PR, tag your supervisor under "request review", and leave the PR open until the meeting is finished. Add additional comments as necessary
7. When the meeting is concluded, merge the PR.

#### Advanced procedure

1. If you haven't already, checkout the `main` branch, and pull any changes.
2. Each week (or whatever period), checkout a new branch for the week, eg `git checkout -b weeklymtg`
3. Copy this template and name the file with the ISO date in `YYYY-MM-DD` format.
   Eg for August 1st, 2022, use `2022-08-01.md`.
4. Update the template as appropriate for the current week.
5. Save the file commit it to your branch for this week, and then push it. Eg
   1. `git add PeriodicMeetings/2022-08-01.md` (update this with the actual path to this week)
   2. `git commit -m "add meeting notes for this week"`
   3. `git push -u origin weeklymtg` (change the branch name to what you used in step 2)
6. Open a Pull-request on github.
   After you push your branch, you should see a green button on the main page of your repo to do this.
   1. In the PR, tag your supervisor, and add any additional context that might be relevant.
   2. Submit the PR
7. During the meeing, comments / additional notes may be added to the markdown file locally,
   and then committed / pushed, which will automatically show up in the PR discussion.

Once the meeting is concluded, the PR should be merged,
and the branch deleted.
Be sure to do pull the latest main locally, and delete the branch
before starting the next week's notes, eg

```
$ git checkout main
$ git pull
$ git branch -D weeklymtg # or whatever you named it
```
