# Movies app in svelteKit

made this project to learn sveltekit, this is just a replica of a older project I made in javascript - [Movies-app](https://github.com/KailashGanesh/Movies-app)

I also deployed it with vercel - [https://movies-app-svelte.vercel.app/](https://movies-app-svelte.vercel.app/)

it was a breeze to deploy with vercel. import the repo and it did the rest.

# Features
- displays the first page of the themoviedb api on load (did't use svletekit's server side rendering here which I could have done)
- searching for movies (used svelte store to access the search query from different components)
- navigation to next and previous pages (svelte's reactive statements are awesome here)