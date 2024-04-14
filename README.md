# TALL-STANDARDS

Our coding guides, tips and standards for [TALL stack](https://tallstack.dev) development.

## Technology Tips:

- **T**ailwindCSS:

  - [ ] TODO!

- **A**lpineJS:

  - Using the dedicated `x-init` is recommended, to distinguish it from the other methods in `x-data`.
    - Wrapping the code in a closure is very much recommended as well: `x-init="() => {doSomething(); doAnother();}"`.

  - You're free to inline `x-data` object and write the tall code! But when the feature is ready, link it into an `Alpine.data()` file.
    - When you have it inlined though, you may encounter issues with double-quotes (`""`) breaking the attribute's. The solution is to use a pair of single-quotes (`''`) for `x-data` itself. And then, in some rare cases, you indent double-quotes inside others using Blade: `.post("{{ route("login") }}",` or \` (back-ticks), to wrap around URLs, for instance. 

- **L**ivewire:

  - Use `<livewire:component-name />` tag to call livewire components when they're not full-pages.

  - API calls can never be done from within Livewire in its persistant session setup.

    - Instead you should dispatch out to the front-end and `axios` from there, then you're free to send the results back.
      - If there are data sent back to livewire, it must be received by a public method, and securing it would be by comparing a previously stored hash of the input.

    - Because of this, the current authentication flow is done via API and through the front-end (and Telegram) as well.

  - [ ] How does hooks work from livewire to alpine? Do document me when you re-write narrations timeline

- **L**aravel:

  - Whenever there is inheritance (extends) and constants or static methods are to be dealt with, please use `static::` over `self::`.

  - When trying to access input properties that are on a `$request`, please do use `$request->input('propertyName')` instead of accessing it directly.

  - Updating a validation constraint in a model's data trait, must be accounted for in its migration as well; and vice-versa.
    - Whereas the property orders in the data trait is based on the migration's.

  - There should not be any syncronization between migrations and models' data, because that's how migrations are migratable; stage!

  - Fillable properties on models should be in the order that they're shown in the UI.
    - There are no fillable properties for pivot models.

  - Casts come after fillable properties on the model.
    - Use casts method instead of the property in case of non-static values.

  - Doing arrays real quick is done via the array service helper's wrap method.

  - Having a Facade setup instead of an ordinary service class gives performance and testing advantages to say the least.
    - Do not forget, however, that the actual class would have non-static methods. And they'll still work like they're static!

  - If long conditions are to be split spilling over the next two lines or so, make sure to have `||` or `&&` at the beginning of subsequent lines.

- Fillament:

  - Be careful when using a $state in a closure, as validations won't apply on them if it's reactive (live).

  - During Fillament fields data grabbing (submission), it's necessary to take out values quickly from the form's getState method.
    - It is recommended to reset the form using fill method and right after using the fields.

## Version Control:

We strongly recommend using [Graphite](https://graphite.dev) workflow. Just install it globally as a front-end package using [bun](https://bun.sh) or [npm](https://npm.org). And then check out its workflow explained by reading this [chat](https://chat.openai.com/share/e/be5df3ea-13d4-4c22-9402-a8608736108c) with our ally!

The only thing to note is that the "PR's parent" comment is misleading. When you're stacking PRs, you should `gt checkout` ensuring that you stay on this previous PR. And then, of course, commit with `gt create --all --message "this new X PR that depends on Y PR or whatever"`. And finally using `gt submit --stack` where the `stack` flag is important. And should you checkout into a previous PR in the stack, you'd need to do `gt modify --all` **BEFORE** doing `gt submit` again.

And it's all about the `gt sync` command before **ANYTHING** and after each submission to keep everything up-to-date and removing anything unnecessary. And also `gt ls` or `gt short log` to show everything happenning.
