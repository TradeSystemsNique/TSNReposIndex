# Storage

For the maintenance and storage of TSN repositories, we use Git, primarily via the MQL5 Algo Forge service.
In some cases—such as for documentation, or when a project needs to be listed in a registry that only accepts GitHub repositories—we use a GitHub mirror; however, the primary repository should reside on Forge for convenience.

Your library does not necessarily have to be on Forge.
However, please be aware of the following:
1. If you use a TSN library that imposes restrictions on where the code must be hosted, you will be limited to using code from the repository/fragment hosted on Forge—not on GitHub or elsewhere.
If you are not using such libraries, or simply wish to follow our conventions, you are free to use any other hosting platform.

## Repository Naming
We leave this up to you. It is advisable to use a prefix; for instance, some repositories within the TSN ecosystem begin with "TSN" or a unique identifier (e.g., "By*").
This is particularly useful if the project covers popular topics where naming conflicts might arise.

## Commit Naming
We do not mandate the use of a specific standard like "Conventional Commits."
However, we offer a few guidelines:
1. Use an initial capital letter—for example, if you were to follow the "Conventional Commits" style:
```
Fix(Src): Fixed a bug in the .set file parsing
```

As for the rest—content, spacing, the use of emojis, etc.—the choice is yours.
> For TSN, our own commits are often simple descriptions of the "change," or sometimes even left blank. When iterating rapidly, we don't always pause to detail every change; instead, we prefer to document final changes in CHANGELOGs or release notes. In short, you decide—we aren't imposing a strict standard, just offering this one recommendation.