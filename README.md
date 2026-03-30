# Agent Skills

A shared skills repository for installing focused skills into other projects.

## Project Structure

| Skill                  | Purpose                       | Install                                                                         |
| ---------------------- | ----------------------------- | ------------------------------------------------------------------------------- |
| `creating-figures`     | Scientific figures with TikZ  | `npx skills add https://github.com/isomoes/skills --skill creating-figures`     |
| `find-skills`          | Discover useful skills        | `npx skills add https://github.com/isomoes/skills --skill find-skills`          |
| `ieee-journal-writing` | IEEE journal writing support  | `npx skills add https://github.com/isomoes/skills --skill ieee-journal-writing` |
| `isomoes-writing`      | Weekly reports and tech blogs | `npx skills add https://github.com/isomoes/skills --skill isomoes-writing`      |
| `pdf`                  | PDF extraction and form tools | `npx skills add https://github.com/isomoes/skills --skill pdf`                  |

## How To Use

From another project, install one skill by name:

```bash
npx skills add https://github.com/isomoes/skills --skill creating-figures
```

For general repo installs, a practical layout looks like this:

```text
repo-A/                    # your application project
repo-B/                    # another application project
skills/                    # central shared skills repo
```

Then in each project, install the specific skill you want:

```bash
cd repo-A
npx skills add https://github.com/isomoes/skills --skill creating-figures

cd ../repo-B
npx skills add https://github.com/isomoes/skills --skill pdf
```

Install any specific skill with the same pattern:

```bash
npx skills add https://github.com/isomoes/skills --skill creating-figures
npx skills add https://github.com/isomoes/skills --skill find-skills
npx skills add https://github.com/isomoes/skills --skill ieee-journal-writing
npx skills add https://github.com/isomoes/skills --skill isomoes-writing
npx skills add https://github.com/isomoes/skills --skill pdf
```

This gives you:

- one central repo to maintain
- one CLI command to import a specific skill into any project
- no need to copy all skills everywhere

If you are also using OpenAI Codex, its docs say Codex supports installed skills and symlinked skill folders when scanning skill locations. That can be useful for local shared development instead of repeated installs.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
