# Dark Mode Toggle in SvelteKit (SSR)

This repository demonstrates how to integrate a dark mode toggle into a SvelteKit application.

Demo: https://sveltekit-darkmodetoggle.netlify.app/

## Idea

On the first visit of a user, we retrieve the user preference (dark or light) using a media query. We change the `data-theme` attribute of the `html` tag accordingly. This changes the CSS variables which are responsible for the theming.

The toggle button changes this attribute as well. But on top of that, we also set a `theme` cookie to make the user's choice persistent. This also has the big advantage that there will be no flashing with every new page visit. (This would happen with a `localStorage`-based implementation.) In fact, the browser sends the cookie along with the request to the page, and we use it in the server handle hook to transform the `html` accordingly which is sent back to the browser.

## References

I have used the following videos as a reference:

-   WebJeda, _Dark mode toggle (cookie based) with SSR in Sveltekit_, https://www.youtube.com/watch?v=mt56gKUeppk
-   WebJeda, _Dark mode toggle with prefers-color-scheme in Sveltekit_, https://www.youtube.com/watch?v=dORbhEZuKmE

A different, more server-side approach is taken here:

-   HuntaByte, _SvelteKit Dark Mode Toggle/Theme Selector (with SSR)_, https://www.youtube.com/watch?v=3GpZkVBjXfE

This prevents the initial flash but does not take into account the initial user preference with a media query.
