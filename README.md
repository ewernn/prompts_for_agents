# create-main-md

Instructions for AI to generate navigation documentation for any repository.

## Usage

1. Drop `create-main.md` into any repository
2. AI agent creates `main.md` navigation document

## Example: nanoGPT

![Running create-main.md on nanoGPT](./example-usage.png)

Generated `main.md` helps AI agents navigate nanoGPT without asking questions.

![Generated main.md](./example-output.png)

## Principle

Delete first, add second. Documentation is complete when there's nothing left to remove.

```
├── create-main.md      # AI instructions
├── README.md           # This file
└── nanoGPT/           # Example
    └── main.md        # Generated output
```