# Team Scratch Pad

> [NOTE]  
> Unlike traditional repos, everything is gitignored in this, and nothing goes  
> to git by default.  Only shared-notes/, shared-ideas/, templates/, and this README are tracked in git — everything else in this  
> repo is gitignored. If you want to merge a specific folder in the future, add the exception in .gitignore.

Use this repo as your local space to create files and work with Claude without  
worrying about them ending up in git. Put personal, throwaway working files  
under personal-notes/ — they stay on your machine only. If something is worth  
the team seeing, put it under shared-notes/ or shared-ideas/ instead so it's tracked and  
visible to everyone in the workspace.

personal-notes

- Local scratch space for collecting inputs with Claude. Gitignored — not checked in, not shared.

shared-notes

- Same idea, but checked in and shared with the team. Visible in the workspace, tracked in git.

shared-ideas

- Team-visible ideas, tracked in git — each promoted idea is its own file, so it can be  
edited and iterated on independently. Not where you capture — where you promote to,  
once you've decided (on a second look, usually with more context) that an idea is worth  
the team seeing. Use the `scratch-ideas` Claude skill for the capture (in your own  
IDEAS.md at the repo root) → file away → promote flow.

templates

- Starter files (e.g. TODO.md) tracked here for everyone to reuse. Copy one into  
personal-notes/ (or the repo root) to get your own working copy — the copy lives  
outside templates/, so it's gitignored automatically and your edits stay local.
