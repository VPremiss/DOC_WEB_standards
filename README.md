# Guides & Tips

- **L**ivewire:

  - [ ] How does hooks work from livewire to alpine? Do document me when you re-write narrations timeline

- **L**aravel:

  - Doing arrays real quick is done via the array service helper's wrap method.

- Fillament:

  - Be careful when using a `$state` in a closure, as validations won't apply on them if it's reactive (live).

  - During Fillament fields data grabbing (submission), it's necessary to take out values quickly from the form's getState method.
    - It is recommended to reset the form using fill method and right after using the fields.


<br>

# Version Control

We strongly recommend using [Graphite](https://graphite.dev) workflow. Just install it globally as a front-end package using [bun](https://bun.sh) or [npm](https://npm.org). And then check out its workflow explained by reading this [chat](https://chat.openai.com/share/e/be5df3ea-13d4-4c22-9402-a8608736108c) with our ally!

The only thing to note is that the "PR's parent" comment is misleading. When you're stacking PRs, you should `gt checkout` ensuring that you stay on this previous PR. And then, of course, commit with `gt create --all --message "this new X PR that depends on Y PR or whatever"`. And finally using `gt submit --stack` where the `stack` flag is important. And should you checkout into a previous PR in the stack, you'd need to do `gt modify --all` **BEFORE** doing `gt submit` again.

And it's all about the `gt sync` command before **ANYTHING** and after each submission to keep everything up-to-date and removing anything unnecessary. And also `gt ls` or `gt short log` to show everything happenning.


<br>

# Environment Setup

If you're on MacOS or Windows, check out [Laravel Herd](https://herd.laravel.com/) to offer you everything you need out of the box.

And if you're on Linux, however, check out this bash script-driven CLI project: [lara-stacker](https://github.com/GoodM4ven/lara-stacker).
