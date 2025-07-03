# AIgenda

Breadcrumbs for me, to keep track during the Vise Coding.

Next Goal:

## Iter 1: Walking skeleton

As a Trainer I can browse the AIgenda site,
enter my name, and push a button `plan a session`.
Then I reach a new page where I see a countdown timer, preset to 20 minutes: 00:20:00.

When I hit the button `start`, the timer starts counting down.
When it reaches 00:00:00, I see a button `end session`,
a doorbell sound is played, and the timer is reset to 00:20:00.

A another button `share session` is also available.
When I hit this button, I can share the session with a link
with the attendees of the training session.

An attendee that uses that link can see the session,
but cannot interact with it. When the session ends,
the the doorbell sound is played on the attendee's browser as well.

### Steps

1. Make a simple but nice Frontend page with Vue, Tailwind that works as described above,
   with a countdown timer, and a button to start the timer. On Localhost.

2. Deploy that page to somewhere publicly available, like Vercel or Netlify or GitHub Pages.
   TODO: where to deploy?

3. Implement share session link functionality:
   - When the Trainer clicks `share session`, a link is generated.
   - The link should be unique for each session.
   - The link should allow the Person to view the session without interaction.


## Iter 2: Propagate state changes

As a Trainer when I pause the timer, attendees should notice that the timer is paused.
When I resume the timer, attendees should notice that the timer is resumed.
When I reset the timer, attendees should notice that the timer is reset.
Within up to 5 seconds is acceptable.

For state propagation in Iter 2, no custom Node/Express backend needed. 
Use WebSocket-as-a-Service (Pusher/Ably) or Firebase Realtime Database to sync timer states 
between trainer and attendees. 
Deploy the Vue/Tailwind frontend to Vercel for automatic GitHub deployments. 
Both Pusher and Firebase offer sufficient free tiers and work directly from the frontend without server infrastructure.

