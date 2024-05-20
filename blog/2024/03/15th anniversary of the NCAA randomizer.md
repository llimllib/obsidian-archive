---
updated: '2024-03-18T13:47:57Z'
created: '2024-03-18T02:08:08Z'
---
[15 years ago](https://billmill.org/ncaa_randomizer.html), I made a simple website that gives you a random NCAA bracket with win percentages weighted by [Ken Pomeroy's](https://kenpom.com/) college basketball ratings.

Every season since (maybe minus a covid year?) I've continued the tradition, and this year is no different. I really enjoy keeping a piece of code alive that has a history this long.

If you want a random-but-reasonable NCAA bracket for your office pool, look no further than [the NCAA Bracket Randomizer](https://llimllib.github.io/ncaa-bracket-randomizer/)!

## maintenance notes

- updated the teams and kenpom ratings
	- I didn't bother to calculate [a new curve](https://github.com/llimllib/ncaa-bracket-randomizer/blob/main/fitting_kenpom/fitting%20kenpom.ipynb#cell-id=6f699577) for kenpom ratings, I spot checked a few games and they looked about as expected.
	- _update_: [I bothered](https://github.com/llimllib/ncaa-bracket-randomizer/blob/main/fitting_kenpom/fitting%202024.ipynb)
- ripped out jQuery, which had survived since the first commits
- ripped out bootstrap, which I had just for a dropdown and a fancy button
- moved to google actions instead of pushing to `gh-pages`