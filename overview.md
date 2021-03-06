## How Portable My Spotify?
### Exporting My Saved Music

During the recent Spotify protests, the ease with which one could transfer Spotify playlists to competing services came up a lot–but I was disappointed to discover, when I tried to migrate my playlists to Tidal, that the free versions of both recommended transfer apps have 250-song restrictions (and the paid versions are subscription apps, billed annually!)

I'm not above dishing out a few bucks for the sake of convenience, but given my recent workouts with the Spotify API, I couldn't help but wonder: just how much less convenient would building a personal playlist exporter really be?

Make no mistake: for you it'll be a breeze–assuming you're comfortable with React and at least curious about Remix–since I've reduced the process to just two problem sequences, elaborated at the links below. (Also, one can still freely access playlist and other info after deactivating a premium Spotify membership.)

But it wasn't horribly inconvenient for me, either–credit mainly to Brittany Chiang, whose recent newline.co course Build a Spotify Connect App (free online at the moment) is a concise masterclass in best practices for REST API client-building. (And whose code and architecture I used as a starting point.) In particular, she walks us through best practices for two of the trickier prerequisites to robust API exploitation: building out an Authorization Code OAuth flow and masterminding a complex, multi-part API query using <code>axios.all()</code>. 

The two main modifications I made to Brittany's code were 1. adapting the OAuth flow to use Remix's routing and 2. orchestrating complex API calls with StepZen & GraphQL rather than Axios and REST (and focusing my query on Liked Songs, my most personally meaningful Spotify scorecard.)

The authorization flow, which <a href="./authflow.md">I describe in detail here</a>, forced me to consider the proper storage of an <code>auth_token</code> in a Remix project, which led me to Remix's fairly painless approach to Session,  <code>createCookieSessionStorage</code> in specific.

The multi-part Spotify API request, which <a href="./stepzen.md">I describe in detail here</a>, uses StepZen to transform Spotify's elaborate, multi-call REST sequences into concise, single-call GraphQL requests. Using GraphQL pagination, fetching my 519-track diary of Liked Songs boils down to a simple <code>while</code> statement in my Remix Loader. 