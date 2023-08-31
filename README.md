# FunCAPTCHA

A next-generation game-based CAPTCHA. Difficulty is highly scalable with multiple customization options and simplicity in adding new icons for identification. Easy and not frustrating for humans to solve (confirmed via survey) while being very difficult for bots to get past.

## Technical Aspect

Uses [SvelteKit](https://kit.svelte.dev), with the CAPTCHA being an svg and [gsap](https://greensock.com/docs/v3/GSAP) being used for interactivity.

To use this in your repo, copy the code in `src/lib/*` and import `Captcha.svelte` in where you want to use it. Add extra components under `svgs`, formatted with props like the rest of them.
