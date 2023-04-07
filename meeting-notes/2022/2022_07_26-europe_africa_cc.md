# scikit-image Community Call

**Time:** Tuesday, July 26, 10:00 – 11:00am Pacific
**Present:** Marianne, Lars, Greg, Alex

## Topics

### Some misunderstanding on SKIP 4

- What does Stéfan mean when he talks about "continuing with 1.1, 1.2, ..."

- (Greg) "Juan's plan to not do any releases after 1.0"
    - Maybe deprecations or so

- We would need to maintain two branches

- (Marianne) version = 1.0 but we changed strategies
    - "Remove version right after 1.0?"
    - 1.0 should be basically a frozen version of what we have so far?
    - What about the new deprecation cycles?

- (Greg) Pretty disruptive after 1.0?
    - "If we have a version after 1.0 we just leave the deprecated API available?"

- (Lars) 1.0 release with deprecations warning, or 1.0 as "stable final version"
    - What do we want to tell the community with 1.0?
    - Keep SKIP 4 as close to as intended

- (Greg) Makes more sense

- (Alex) Should we vote SKIP 4? Is it accepted?
    - Problematic to reject SKIP 4 and get back to SKIP 3

- SKIP 4 seems convoluted; people that voted it are not around anymore
    - We need to figure out the deprecation cycle

- (Lars) advantages/disadvantages on both parts
    - Do we specify a grace period?
    - We need to ping the other core developers

- (Greg) Issue to discuss SKIP 4 and update the section on deprecations

- Steering committee?

- (Greg) Jarrod wants to discuss SKIP 4

- (Lars) If SKIP 4: how would we handle the deprecation cycle?
    - If not: what should we do?

- (Greg) Kinda tough to get back to SKIP 3 again
    - (Alex) That was a joke :)

- We need another meeting w/ everyone to discuss what to do
- (Alex) [skimage#6448](https://github.com/scikit-image/scikit-image/issues/6448) is a good place to discuss this

### Road to 1.0

- 0.20?
    - We need to revise SKIP 4; plan is to never release 0.20
    - Maybe add deprecations, release cycles, ...?
    - Maybe will give Juan, Stéfan the time to discuss it again

- Release process
    - (Greg) Pushing the version tag should suffice
    - Maybe having 0.20 would release the pressure of having 1.0
    - (Marianne) Willing to give a try on the release process

- Anything tagged for 0.20/1.0?
    - (Greg) Point everything to 1.0?
    - Keep a conservative approach to add deprecations wisely at this point

### Extras

- (Marianne) Emma will give a skimage tutorial in Basel
    - Lars is interested to go

- (Greg) We have funds for travelling
    - CZI Annual Meeting: Sep 18th–21st
    - Remote participation available

- OpenCollective
    - Last funding

- (Greg) No "official" time for skimage anymore :)
- Lars's situation

