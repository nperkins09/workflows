Planning
- Overall project vision markdown file
- Submit to AI for review and reveal hidden gaps / areas of improvement for version 1
- Create a plan/ development roadmap
Development
- Have AI scaffold the project
- Work with AI in building one file at a time
Testing
- Conduct tests and codebase health checks
- Repeat to next file

Notes

- Need and want design docs/specs for both the AI and for Humans. The docs are useful to AI to build the project in a well-architected manner as well as for humans to read and understand the underlying architecture.
- Integrating AI into the codebase

Human Managed
  Project_Overview.md
  prompts


## Planning

1. Create a markdown file called <Project>_Overview.md that provides details about the project. No fancy formatting just stream of conciousness
  - Sections
    - Workflow
    - Project Summary
    - Tech Stack
    - Constraints
2. Feed the overview and Planning_Claude.md markdown files into Claude Cowork and ask it to do the following:
  - Review the Project_Overview.md
  - Ask it to provide a list of questions it has about the architecture; store the questions in a markdown file; provide an answer section after each question.

**prompt**

```
I have attached a markdown file called <project>_Overview.md that provides details about a project I intend to build.
Review the document. Before we plan anything, ask questions until you understand the project's re> quirements. Store the questions in a markdown file called 'Questions_v1.md'.
Provide a section underneath every question for me to answer. Once I answer the questions I will send the completed document to you and we will repeat until you understand all of the project requirements.
Please number the questions.
```
3. Answer every question, upload the question markdown file to Claude and ask it if there are any more questions. Repeat until ts satisfied.
  - <prompt>
```
I have answered every question in the Questions markdown file and uploaded it. Please review my answers, if you have any more questions about the project requirements before we begin drafting the official project design documents then store the questions in a markdown file called 'Questions_v[x].md'. Replace the x in Questions_v[x].md with an incremental number following the last Questions markdown file. So if the last file was Questions_v1.md then it becomes Questions_v2.md. Follow the same pattern as Questions_v1.md.
```
4. Ask it to create a Plan.md -> A scaffold/development plan/Roadmap/Tasks list by code file.
  - <prompt>
```
Given the project overview and all of the question markdown files. Without writing any code, propose a plan: project structure, key modules and their responsibilities, data models, libraries, and the order to build things in. Save the agreed plan to PLAN.md with sections for goal, scope, tech decisions, structure, current status, decisions log, and open questions. In separate markdown file called Tasks.md create a checklist of slices in build order (each with a short definition of done), make this file so that when I go through each task as I complete them I can mark it as done.
```
5. Review, revise, and approve official plan.md
  If revision necessary
    - <prompt>
```
Given plan.md, please make the following revisions:
1.
2.
3.
```
6. Ask it to create a claude.md for this project; include personal coding standards according to plan.md
  - <prompt>
```
Based on the documents uploaded so far please create a claude.md for this project. I will review and revise with my own coding standards and requirements.
```
## Development

1. Ask it to scaffold the project; No code just the files
  - <prompt>
```
Set up the project skeleton from PLAN.md: pyproject.toml with uv, a src/ layout, pytest, ruff, and mypy in strict mode, a basic README, and one trivial passing test. Run all the checks to confirm everything works, then initialize git and make the first commit.
```
2. Have AI develop the testing suite per file before development
  - <prompt>
```
Before building this, create the test suite needed to for this task. Make sure the test coverage is at least 85%.
```
3. Develop with AI one file at a time using a different session from the testing one.
  - Be sure to commit after every file.
  - Allow AI to update documentation after every commit
  - <prompt>
```
Read Plan.md and Tasks.md. Work on task <#>
```

## Testing

1. Run Testing suite to check
  - Everything must pass
  - Code coverage must be >= 85%
2. Use a testing sub agent to check code quality
  - <prompt>
```
I've run the test suite and everything returns green. Check off slice <#> in Tasks.md, propose a commit message for these changes.
```

## Deployment
1. Update Tasks.md
2. Push to Repo with Proposed GitHub Commit Message