# Track your resume in git

I have been using git to track my resume and job applications for over 10 years, and I constantly make improvements to this workflow.
Here is an example repo for how to track your resume with git.

Here is my current goals:

* Make it easy to modify and track resume changes
* Keep application history
* Make searching for relevant information easy

This is an example repo with example data.
This does not include my real resume or jobs I have applied for.
Commit dates have been altered so you can see what a working example looks like over time.

This may not be the best system for you depending on how much you use or like git.

## Explore this repo

You can explore this repo by cloning it and using `git` or visually from the network insights on GitHub.
Other git tools may work, but may not present the data in a helpful way because this repo is not used like a typical code repo.

## How to track your resume in git

Put your resume in git.
This should include the .pdf you submitted and any files you used to generate that PDF.

I always track the files with my full name so they are named the same thing.
Naming consistency helps with tracking changes and switching branches.

```
ls

Justin Garrison.md
Justin Garrison.pdf
```

If you use a word doc, markdown, html, etc. it should be tracked.
If you use a 3rd party tool to generate the PDF (e.g. https://ohmycv.app/) you should put that information in a readme.txt file.

```
cat readme.txt

used: https://ohmycv.app
```

If you use CLI tools to generate the PDF (e.g. `laytex` or `pandoc`) you should create a Makefile or [justfile](https://github.com/casey/just) to generate the pdf.

```
cat justfile

pdf
    pandoc "Justin Garrison.md" -o "Justin Garrison.pdf"
```

This makes it easier to edit and generate the asset to submit to the job application.

At minimum you should track the source file(s) and submitted resume.

When you make changes to the resume without applying for a new job you can commit your changes with any commit message you want.

## How to track applications

I don't always customize my resume for each application, but I still want a way to track what jobs I applied for.
This was hard to do for two reasons:

1. Appending git messages and git tags wasn't great for tracking job requirements
1. Branching was harder to remember/use without a regular "main" branch

Whenever I apply to a role I export the job description—print to pdf—to the repo and commit it as jd.pdf.
This lets me always reference what job I applied for when, and gives me a permanent record of the job description.

Job postings only exist online for a short time so keeping a record has been very helpful.

This doesn't work well for jobs I've applied for without a job description (direct apply to manager), jobs I've applied to via LinkedIn "Easy Apply", or jobs I've applied to via my phone.

What I do in those cases is:

* If I apply directly do the hiring manager I email myself a note of who I emailed and the role title to add to a jd.txt file
* If I'm on mobile, I export the page to a PDF and email it to myself to add to the repo later
* If I apply through LinkedIn Easy Apply I save the link and later add it to jd.txt

This helps me track the majority of jobs I apply for in git with consistent file naming.

I haven't been using LinkedIn Easy Apply for very long, and as far as I can tell job posting links don't expire.
Someone please let me know if they do expire or you know a better way to export a LinkedIn job posting.

## Branch management

I have branches for different job families, and companies.
The main branch is usually a generic form of my current resume format.
I only commit to main when I change how my resume looks or use a new tool to generate it.

For example, when I apply at a new company, I make a branch.
Some companies I only apply to one job, others I apply to many jobs.

Sometimes those jobs are all a similar type of role (e.g. software engineer), but sometimes they're different job families (e.g. manager, SRE).
Keeping separate branches for each job type let's me keep relevant information in one branch and cherry pick the resume into the company branch when I apply for a role.

A typical application workflow at a new company might look something like this.

```
git checkout role-sre
git switch -C cool-co
vim "Justin Garrison.html"
<Make edits>
just pdf # generate PDF file
just jd "https://example.com/job" # download job description into jd.pdf
git add .
git commit -m "Apply: SRE job at cool-co"
```

If I find more jobs at "Cool Co." I can re-use this resume with an updated jd.pdf file and add a new commit for the new role.

## Optional things

Some other things I've tried tracking and gave up on for various reasons.

* Interviews
* Job offers
* Contacts/notes

For a while I was tracking application status updates and interviews in my git repo.
It was cool to see the timeline, but it became too much work to maintain.

It was more work partially because the job I interviewed for wasn't always the job I applied for.
Some companies also have many layers of interviews and I would forget to update the repo after a phone screen or after traveling for an in-person interview.

Offers come via email or a phone call and usually have multiple documents (at least they do at big companies) and I didn't want to dump all that stuff in git.
Health benefits, retirement, base pay, and other perks were never consistent and instead of keeping them in git I keep them in my note taking app.

Contacts and names are handy to have, but I never found a consistent way to store them.
Sometimes I would put them in git commit messages and sometimes I would put them in a contacts.txt file.

Either way, I would track them but when I would eventually want to look them up again they usually didn't work at the company anymore.
There have been people I've interviewed with at multiple companies and it was harder to track them as part of an application process.

