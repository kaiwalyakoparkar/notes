# Issue Template

## Bug report 🐛

```yml
name: Bug Report 🐛
description: File a bug report
title: "[Bug]: <title>"
labels: ["bug"]
body:
  - type: markdown
    attributes:
      value: |
        Thanks for taking the time to fill out this bug report! Please provide as many screenshots as possible to perfectly convey the bug report :)
  - type: textarea
    id: what-happened
    attributes:
      label: What happened?
      description: Also tell us, what did you expect to happen?
      placeholder: Tell us what you see!
      value: "A bug happened!"
    validations:
      required: true
  - type: dropdown
    id: browsers
    attributes:
      label: What browsers are you seeing the problem on?
      multiple: true
      options:
        - Firefox
        - Chrome
        - Safari
        - Microsoft Edge
        - Brave
  - type: textarea
    attributes:
      label: Anything else?
      description: |
        Links? References? Anything that will give us more context about the issue you are encountering!

        Tip: You can attach images or log files by clicking this area to highlight it and then dragging files in.
    validations:
      required: false
  - type: checkboxes
    id: terms
    attributes:
      label: Code of Conduct
      description: By submitting this issue, you agree to follow our [Code of Conduct](https://example.com)
      options:
        - label: I agree to follow this project's Code of Conduct
          required: true
```

## Docs Request 📄

```yml
name: Documentation request
description: Change regarding improving the docs to be more accessible
title: '[Docs] <Title>'
labels: ['documentation']
body:
  - type: textarea
    attributes:
      label: Category of documentation update
      description: |
        What category does this change fall under.For example Typo error, New category addition, Rephrasing the sentences, fixing broken links etc 
    validations:
      required: true
  - type: textarea
    attributes:
      label: Describe the change you think might work
      description: Please describe the change & need of change in atmost detail possible.
    validations:
      required: false
```

## Feature Request 🚀

```yml
name: Feature request
description: Suggest an idea for this project
title: '[Feat] <Title>'
labels: ['enhancement']
body:
  - type: textarea
    attributes:
      label: Would you like to have a new feature? Please describe.
      description: A clear and concise description of what the feature is
      placeholder: Ex. Whenever I try to do (xyz) then [...]
    validations:
      required: false
  - type: textarea
    attributes:
      label: How would this feature be beneficial for the project
      description: A clear and concise description about the importance of the feature
    validations:
      required: false
  - type: textarea
    attributes:
      label: Additional context
      description: Add any other context or screenshots about the feature request here.
    validations:
      required: false
```