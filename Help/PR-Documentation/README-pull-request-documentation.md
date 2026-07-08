# Creating a Pull Request Template

A pull request template is a file that automatically adds existing text into the PR description box when a user opens a new pull request.

This helps provide a consistent format so users know what information to include, such as what changed, how it was tested, and any screenshots or related notes.

## How to Create One

1. In the repo, create a file named:

   `pull_request_template.md`

   or:

   `PULL_REQUEST_TEMPLATE.md`

2. Add the text you want users to fill out when they open a PR.

Example:

```md
## Summary
Explain what changed.

## Testing
Describe how you tested this.

## Mantis Bug Number
0000

## Resolved in build#
0101

## Screenshots
Add screenshots if needed.
```

<img width="1914" height="941" alt="create-pull_request_template md" src="https://github.com/user-attachments/assets/de77d3e1-2fbf-4d69-a6c3-9532143a08fd" />


3. When a user opens a new pr, the template text should automatically appear in the pr description box.
<img width="1910" height="944" alt="pr-template-example" src="https://github.com/user-attachments/assets/d5cdbadb-c388-46f3-a7f0-4da97077b093" />

